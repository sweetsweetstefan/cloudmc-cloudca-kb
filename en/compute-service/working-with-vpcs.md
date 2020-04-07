---
title: "Working with VPCs"
slug: working-with-vpcs
---


For basic information about VPCs, refer to this [article](what-is-a-vpc.md).

### Create a new VPC

**Note:** For this operation to be available, your user account needs to be assigned the **Environment Admin** role on the target environment.

1. Go to the **Services** page.
1. Select the appropriate compute environment on the left sidebar.
1. Select the **Networking** tab.
1. Click on **Add VPC**.
1. Fill the Add VPC form:
   1. **Name:** Name of the VPC (ex: prod-vpc1)
   1. **Description:** Description of the VPC (ex: Production network site A)
   1. **Zone:** cloud.ca zone name where to deploy the VPC (defaul: QC-1)
   1. **CIDR:** Randomly generate private subnet. Cannot be edited.
   1. **Network Domain:** Domain Name (optional).
   1. **VPC Offering:** Choose the Service Level of this VPC
      - **Default VPC Offering:**  Basic VPC providing up to four subnets, VPC access, Public NAT, Port Forwarding and Load-Balancing.
1. Click on **Done**

### Create a new network tier

1. Go to the **Services** page.
1. Select the appropriate compute environment on the left sidebar.
1. Select the **Networking** tab.
1. From the target VPC's list item, click the **Tiers** button.
1. Click on **Add tier**.
1. Fill the Add tier form:
   1. **Name:** Name of the Tier (ex: net-web1)
   1. **Description:** Description of the Tier (ex: Production Webservers)
   1. **Select a Network offering:**  Choose the Service Level of this Tier
      - **Standard Tier:**  Regular network supporting NAT, PortForwarding. Suitable for internal application such as Database server.
      - **Load Balanced Tier:**  Same as Standard Tier but also offers the capacity to load-balance traffic across multiple instances within that tier, via load-balancing rules applied on a public IP Address. Note that only a single tier within a VPC can have this offering.
   1. **ACL:** Access Control List for communication across Tiers within the same VPC.
      - **default_allow:**  Allow all type of traffic from/to other tiers in the VPC.
      - **default_deny:**  Deny all type of traffic from/to other tiers in the VPC.
1. Click on **Done**

### Site-to-Site VPN

Site-to-site VPN offers capability to interconnect:

- Multiple VPCs
- Office to VPC
- Other Cloud provider to VPC

Site-to-Site VPNs management is currently not available via cloud.ca portal. If you need VPN connectivity contact cloud.ca support who will provide help on setting it up.

##### Considerations:

- VPC subnet does not interfere with remote site IPs.
- VPN perform user IPsec tunnel.
- VPN security handle via ACL.
