---
title: "Deploy Virtual Machine using Terraform"
slug: deploy-virtual-machine-using-terraform
---


Using [Terraform](https://www.terraform.io/) to create instances based on custom size compute resources.

### Prerequisite

- [Terraform](https://www.terraform.io/downloads.html) installed locally
- cloud.ca terraform driver installed [https://github.com/cloud-ca/terraform-provider-cloudca](https://github.com/cloud-ca/terraform-provider-cloudca)
- your cloud.ca *api_key*
- *environment_id*
- *network_id*,  network tier from a VPC.


### Resource definition

Refer to the [driver documentation](https://github.com/cloud-ca/terraform-provider-cloudca/tree/development/cloudca#cloudca_instance) for latest attributes :

```
resource "cloudca_instance" "prod-app01" {
  environment_id = "4cad744d-bf1f-423d-887b-bbb34f4d1b5b"
  name = "prod-app01"
  network_id = "672016ef-05ee-4e88-b68f-ac9cc462300b"
  template = "CentOS 7.4 HVM"
  compute_offering = "Standard"
  ssh_key_name = "my_ssh_key"
  root_volume_size_in_gb = 100
  cpu_count = 1
  memory_in_mb = 1024
}
```

Create multiple instance of the same type :

```
resource "cloudca_instance" "prod-app" {
  count = "10"
  environment_id = "4cad744d-bf1f-423d-887b-bbb34f4d1b5b"
  name = "prod-app${count.index}"
  network_id = "672016ef-05ee-4e88-b68f-ac9cc462300b"
  template = "CentOS 7.4 HVM"
  compute_offering = "Standard"
  ssh_key_name = "my_ssh_key"
  root_volume_size_in_gb = 100
  cpu_count = 1
  memory_in_mb = 1024
}
```
