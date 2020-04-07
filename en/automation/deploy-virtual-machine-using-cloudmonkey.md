---
title: "Deploy Virtual Machine using CloudMonkey"
slug: deploy-virtual-machine-using-cloudmonkey
---


Use CloudMonkey as command-line interface for cloud.ca. [CloudMonkey](https://cwiki.apache.org/confluence/display/CLOUDSTACK/CloudStack+cloudmonkey+CLI) is the official Command-line interface (CLI) for [Apache Cloudstack](http://cloudstack.apache.org/). In cloud.ca, it is possible to interact directly with the [CloudStack API](http://cloudstack.apache.org/api/apidocs-4.8/TOC_User.html) to benefit from opensource automation tools.

The following example uses compute-qc.cloud.ca's region API.

This documentation explains how to use CloudMonkey to create virtual machines into an environment that already has a VPC with networks created.

### Requirements

- CloudMonkey installed [https://doc.cloud.ca/kb/en/how-to#install-and-configure-cloudmonkey](https://doc.cloud.ca/kb/en/how-to#install-and-configure-cloudmonkey)
- Access to cloud.ca
   - Retrieve your API credentials from cloud.ca webUI in the "API keys" under user profile.
   - projectid; defined in the API keys page
- Already deployed VPC with networks

In order to deploy a virtual machine, we need to retrieve some ID parameters required by the `deploy virtual-machine` API.

### Retrieve required IDs

Before deploying a virtual machine via API call, we need to retrieve the following parameters IDs so our VM will be deployed on the right network and zone, with the proper specifications :

- serviceofferingid
- zoneid
- networkids
- templateid

#### Service Offering ID

Available service offerings:

| cloud.ca region | id | name | description |
| --- | --- | --- | --- |
| compute-qc | 20363b3b-7607-4f34-9ba3-0ad57bd44bc1 | Standard | Customizable instance based on Standard root drive |
| compute-on | a0a67feb-c5d8-471b-8088-32b02fd5b372 | Standard | Customizable instance based on Standard root drive |

Recent changes in cloud.ca introduce a new way of deploying Instances to improve user flexibility. cloud.ca now uses custom defined compute offerings. This means that instead of selecting the proper offering during virtual machine creation, users have to define the amount of memory and vCPU allocated to the Virtual-Machine.

#### Zone ID

| cloud.ca region | zone name | id |
| --- | --- | --- |
| compute-qc | QC-1 | 04afdbd1-e32d-4999-86d0-96703736dded |
| compute-qc | QC-2 | 5149f99b-f5c9-4523-8039-3f1bfe466c6b |
| compute-on | ON-1 | ea901007-056b-4c50-bb3a-2dd635fce2ab |

```
list zones filter=id,name
```

#### Network ID (used by networkids)

List available networks from a cloud.ca environment refer as a project in the CloudStack API:

1. Select the right VPC

```
list vpcs projectid=2389b5cd-2d11-4140-be33-e55005da28da filter=name,id,zonename,cidr

count = 2
vpc:
+-----------------+----------+------------------------------+--------------------------------------+
|       cidr      | zonename |             name             |                  id                  |
+-----------------+----------+------------------------------+--------------------------------------+
|  10.212.44.0/22 |   QC-2   |       engineering-qc2        | 2dfcc07d-225d-4aec-832e-d6232b828ee5 |
|  10.162.44.0/22 |   QC-1   |            q1-eng            | 64049916-96ab-4c06-a7da-2bb4639e70a7 |
+-----------------+----------+------------------------------+--------------------------------------+
```

2. From the selected VPC, choose a network

```
list networks projectid=2389b5cd-2d11-4140-be33-e55005da28da vpcid=2dfcc07d-225d-4aec-832e-d6232b828ee5 filter=id,name,displaytext,cidr

count = 2
network:
+----------------+-------------+--------------------------------------+----------+
|      cidr      | displaytext |                  id                  |   name   |
+----------------+-------------+--------------------------------------+----------+
| 10.212.45.0/24|   clusters  | 4857c729-d3b6-4672-bfc6-70df790d6372 | clusters |
| 10.212.44.0/24|    tools    | 24587393-b88a-4f0c-9741-be56e6cf33a3 |  tools   |
+----------------+-------------+--------------------------------------+----------+
```

In the example below, the selected networkid is `networkids=4857c729-d3b6-4672-bfc6-70df790d6372`.

#### Template ID

The command `list templates templatefilter=featured filter=name,displaytext,id` will return latest available templates in cloud.ca and their IDs.

```
list templates templatefilter=featured filter=name,displaytext,id
count = 11
template:
+------------------------------------------------------------------------------------------+--------------------------------------+---------------------------------+
|                                       displaytext                                        |                  id                  |               name              |
+------------------------------------------------------------------------------------------+--------------------------------------+---------------------------------+
|                     Debian 9.3 jessie (64bit) cloud-init, 2018-02-05                     | cc045ebf-3e0c-4aad-a4b9-64db33e71f49 |        Debian 9.3 (64bit)       |
|                    Debian 8.10 jessie (64bit) cloud-init, 2018-01-22                     | 32519f63-83ab-413d-9a09-cf23ab077223 |       Debian 8.10 (64bit)       |
| Windows2012r2 Standard (64bit) HVM, Service Provider license, cloudbase-init, 2018-01-18 | d8456f70-42bb-4bcf-a863-5c335c77230a | Windows Server 2012 R2 std SPLA |
|                  Ubuntu 14.04 LTS (64bit) HVM base install, 2018-01-17                   | dba6a0c8-93f2-4375-98c5-802d6989c022 | Ubuntu 14.04.5 HVM base (64bit) |
|                       CentOS 7.4.1708 HVM, cloud-init, 2018-01-04                        | 99a900aa-7522-4bf9-8a34-dfc231209915 |          CentOS 7.4 HVM         |
|                           Ubuntu 16.04.03 LTS HVM, 2017-12-28                            | c3bd17ee-e9ff-4d89-b18c-e64b607a5be3 |       Ubuntu 16.04.03 HVM       |
|             Windows2008r2 Enterprise (64bit) HVM, BYOL cca-tools, 2015-05-04             | 5899dffe-e11b-4194-a521-3f557c49cd1f | Windows Server 2008 R2 ent BYOL |
|                         CoreOS Alpha 1313.0.0 (2017-02-03-0826)                          | 42e5c312-3034-49d6-a496-b6d022fa2ed9 |           CoreOS Alpha          |
|                              CoreOS Stable release 1235.6.0                              | ed347ec3-651a-4caf-8da7-9aa0272cf586 |          CoreOS Stable          |
|  Windows2012r2 Standard (64bit) HVM, Bring Your Own License, cloudbase-init, 2016-06-27  | 11966ab8-a4e7-4149-b1c7-625ddaf633e7 | Windows Server 2012 R2 std BYOL |
|           Debian 8.5.0 jessie (64bit) PV base install, cloud-init, 2016-09-09            | 6149c2e6-60e4-48fc-93c8-45730f440292 |  Debian 8.5 PV base (64bit) old |
+------------------------------------------------------------------------------------------+--------------------------------------+---------------------------------+
```

In the example below, the template used is CentOS 7, using `id = 99a900aa-7522-4bf9-8a34-dfc231209915`.

### Deploy virtual machine

At this point, we have all our required IDs and now have to fill all parameters required for the API call to work:

| Parameter | Description | Value | Default value |
| --- | --- | --- | --- |
| serviceofferingid | ID of the VM offering | 20363b3b-7607-4f34-9ba3-0ad57bd44bc1 | compute-qc: 20363b3b-7607-4f34-9ba3-0ad57bd44bc1 <br><br> compute-on: a0a67feb-c5d8-471b-8088-32b02fd5b372 |
| zoneid | ID of the zone, use the zone defined in the VPC | 5149f99b-f5c9-4523-8039-3f1bfe466c6b | compute-qc: 5149f99b-f5c9-4523-8039-3f1bfe466c6b <br><br> compute-on: |
| projectid | ID of the project defined in the API keys page of cloud.ca portal | <UUID> | |
| networkids | network tier ID of the VPC | <UUID> | |
| templateid | ID of the OS template | <UUID> |
| keypair | name of the ssh public key | user3 | |
| name | name of the VM | myvm01 | |
| displayname | name of the VM or brief description | myvm01 | |
| details[0].cpuNumber | number of VCPU | 2 | |
| details[0].cpuSpeed | cpu speed, keep this one as 1000 | 1000 | |
| details[0].memory | Memory in MB so 1024 = 1GB | 1024 | |
| rootdisksize | Root volume size in GB, up to 100 for 100GB | 15 | 8 |

### Complete CloudMonkey example

```
deploy virtualmachine name=myvm01 displayname=myvm01 keypair=user3 projectid=2389b5cd-2d11-4140-be33-e55005da28da zoneid=5149f99b-f5c9-4523-8039-3f1bfe466c6b networkids=4857c729-d3b6-4672-bfc6-70df790d6372 templateid=99a900aa-7522-4bf9-8a34-dfc231209915 serviceofferingid=20363b3b-7607-4f34-9ba3-0ad57bd44bc1 details[0].cpuNumber=2 details[0].cpuSpeed=1000 details[0].memory=1024 rootdisksize=15
```

### Deploying a virtual machine with a data volume

Create a new virtual machine that have a larger data-volume attached to it.

- Complete the previous steps except the deploy api call.
- Select the proper disk offering and define the size.
- Create the instance

#### diskofferingid

```
list diskofferings filter=name,id,displaytext,iscustomized
```

```
list diskofferings filter=name,id,displaytext,iscustomized
count = 19
+----------------------------------------------+-----------------------------------------+--------------------------------------+
|                 displaytext                  |                   name                  |                  id                  |
+----------------------------------------------+-----------------------------------------+--------------------------------------+
|        Custom size; up to 5000 IOPS.         |           Performance, No QoS           | b5919e1b-df5d-47ec-9039-736238ec3656 |
|  Custom size; 1000 IOPS min, 5000 IOPS max.  |  Guaranteed Performance, 1000 iops min  | c546ebf3-e91b-4817-9c7d-e56e0fb33f51 |
|  Custom size; 5000 IOPS min, 7000 IOPS max.  |  Guaranteed Performance, 5000 iops min  | 23973cf3-fbb1-4789-a443-b84261d4f3bc |
| Custom size; 10000 IOPS min, 15000 IOPS max. | Guaranteed Performance, 10'000 iops min | 5f0d15f3-7abd-42d4-a8fa-6aea265eb149 |
+----------------------------------------------+-----------------------------------------+--------------------------------------+
```

In this example, we will select a data volume using "Guaranteed 1000-3000 IOPS" with a size of 30GB. This gives us: `diskofferingid=720625ae-ecfa-4cdd-b1e4-ba96961408ad size=30`

### Deploying instance with a data volume

```
deploy virtualmachine name=myvm01 displayname=myvm01 keypair=user3 projectid=2389b5cd-2d11-4140-be33-e55005da28da zoneid=5149f99b-f5c9-4523-8039-3f1bfe466c6b networkids=4857c729-d3b6-4672-bfc6-70df790d6372 templateid=99a900aa-7522-4bf9-8a34-dfc231209915 serviceofferingid=20363b3b-7607-4f34-9ba3-0ad57bd44bc1 details[0].cpuNumber=2 details[0].cpuSpeed=1000 details[0].memory=1024 rootdisksize=15 diskofferingid=b5919e1b-df5d-47ec-9039-736238ec3656 size=30
```

The added Data drive will be accessible as `/dev/xvdb` inside the instance.
