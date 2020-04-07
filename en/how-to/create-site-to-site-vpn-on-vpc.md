---
title: "Create Site to Site IPsec VPN endpoint on a VPC"
slug: create-site-to-site-vpn-on-vpc
---

# Create Site to Site IPsec VPN endpoint on a VPC

Site to Site IPsec VPN is useful to interconnect a VPC to a Remote office, another data-center or two VPCs together.

To configure VPN, we need to [install and configure Cloudmonkey](install-and-config-cloudmonkey.md) to interact with cloud.ca API via command line.



### Prerequisites

To configure cloud.ca VPN side we need to answer following questions:

- What is the public IP of the remote site ?  `<remote_site_public_IP>`
- What is the remote site CIDR, subnet that will be reachable through the VPN from cloud.ca VPC ? ``<remote_site_internal_IP_range>``
- What is the IPsec Preshared-Secret ? `<Unique +10 alphanumeric>`
- What is the VPC UUID ? `<VPC_ID>`
- What is the project UUID; service environment id where the VPC reside ? `<PROJECT_ID>`



### VPN default configuration and encryption

| Params| cloud.ca values | IPsec |
| --- | --- | --- |
| Gateway | <remote site public IP> | |
| CIDR | <remote site internal IP range> | |
| IPsec Preshared-Key | <Unique +10 alphanumeric> | |
| IKE Encryption | aes128 | phase 1 |
| IKE Hash | sha1 | |
| IKE DH | Group 5(modp1536) | |
| ESP Encryption | aes128 | phase 2 |
| ESP Hash | sha1 | |
| Perfect Forward Secrecy | Group 5(modp1536) | |
| IKE lifetime (second) | 86400 | |
| ESP lifetime (second) | 3600 | |
| Dead Peer Detection | true | reconnect |
| Force UDP Encapsulation of ESP Packets | false | |




### Creating the VPN side via CloudMonkey

Creating the site-to-site VPN endpoint on a VPC in cloud.ca require 3 API commands:

- Active VPN gateway on the VPC
[http://cloudstack.apache.org/api/apidocs-4.8/root_admin/createVpnGateway.html](http://cloudstack.apache.org/api/apidocs-4.8/root_admin/createVpnGateway.html)
- Create remote site configuration, how the VPN is configured, what network range to route into the VPN (the remote site)
[http://cloudstack.apache.org/api/apidocs-4.8/root_admin/createVpnCustomerGateway.html](http://cloudstack.apache.org/api/apidocs-4.8/root_admin/createVpnCustomerGateway.html)
- Activate the VPN connection
[http://cloudstack.apache.org/api/apidocs-4.8/root_admin/createVpnConnection.html](http://cloudstack.apache.org/api/apidocs-4.8/root_admin/createVpnConnection.html)


#### CloudMonkey commands:

- `create vpngateway vpcid=<VPC_ID>`
- `create vpncustomergateway dpd=true esppolicy=aes128-sha1;modp1536 forceencap=false ikepolicy=aes128-sha1;modp1536 ipsecpsk=<Unique +10 alphanumeric> cidrlist=<CIDR> name=<NAME> projectid=<PROJECT_ID> gateway=<REMOTE_PUBLIC_IP>`
- `create vpnconnection s2scustomergatewayid=<PREVIOUS_COMMAND_OUTPUT_UUID> s2svpngatewayid=<FIRST_COMMAND_OUTPUT_UUID>`


##### Example:
- `create vpngateway vpcid=d86cabde-bd61-4884-8166-56fdd2fdf66e`
- `create vpncustomergateway dpd=true esppolicy=aes128-sha1;modp1536 forceencap=false ikepolicy=aes128-sha1;modp1536 ipsecpsk=StrongSecret cidrlist=10.178.52.0/22 name=vpc_to_office projectid=db3ed20c-fc05-4072-b0a3-608e33feb7b0 gateway=69.196.164.512`
- `create vpnconnection s2scustomergatewayid=7542cca9-8a6d-4bb6-811f-e08826df3955 s2svpngatewayid=30c3ecf9-7f76-4fea-abd7-cb16d4870502`


At this point, the configuration must be configured on the Office or remote VPN side where it will use the VPC SourceNAT IP as the remote site IP. then the connectivity between the two network should be working.
