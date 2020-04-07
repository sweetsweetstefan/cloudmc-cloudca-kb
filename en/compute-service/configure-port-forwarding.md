---
title:  "Configure Port Forwarding"
slug:  configure-port-forwarding
---

Port forwarding provide inbound connectivity from the Internet to a specific Instance Port or Protocol. It is configured through a VPC's public IP address dedicated to the purpose of port forwarding.

Note: you cannot configure port forwarding rules on a public IP address already being used for **Source NAT**, **VPN** or **Load Balancing**.

In the following example, we will enable port forwarding for SSH (TCP port 22) of instance *preprod-redis-01* to the public IP port 22022.

1. Go to the **Services** page.
1. Select the appropriate compute environment on the left sidebar.
1. Select the **Networking** tab.
1. From the target VPC's list item, click the **Public IPs** button.
1. Click on **Acquire IP address**.

![Acquire IP address](/assets/config-port-fwd-1-en.jpeg)
![Address acquired](/assets/config-port-fwd-2-en.jpeg)

6. Add a port forwarding rule to the newly acquired Public IP address:

![Port forwarding rules](/assets/config-port-fwd-3-en.jpeg)
![Add port forwarding rule](/assets/config-port-fwd-4-en.jpeg)


7. Fill step #1 of the **Add port forwarding** rule form and click on **Next**:

![Adding rule, step 1](/assets/config-port-fwd-5-en.jpeg)

8. In step #2, select the appropriate **instance** that is the target of the port forwarding rule and click on **Done**:

![Adding rule, step 2](/assets/config-port-fwd-6-en.jpeg)
![Added rule](/assets/config-port-fwd-7-en.jpeg)

9. Validate that the port forwarding rule is working by connecting to the instance through SSH:

![Validate with SSH](/assets/config-port-fwd-9-en.jpeg)
