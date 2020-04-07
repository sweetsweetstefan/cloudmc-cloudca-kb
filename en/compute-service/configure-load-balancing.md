---
title: "Configure Load Balancing"
slug: configure-load-balancing
---


Load balancing provides a way to distribute workloads across multiple compute resources. This usually increases performance and availability through redundancy. In the context of cloud.ca, this is achieved by associating load-balancing rules to a VPC's public IP address.

**Note:** You cannot configure load balancing rules on a public IP address already being used for Source NAT, VPN or Port Forwarding. Furthermore, only a single tier within a VPC can have public IP addresses dedicated to load-balancing.

In the following example, we will enable load balancing for HTTP (TCP port 80) on instances *web1* and *web2* using a simple [round-robin](https://en.wikipedia.org/wiki/Round-robin_scheduling) scheduling algorithm.

1. Go to the **Services** page.
1. Select the appropriate compute environment on the left sidebar.
1. Select the **Networking** tab.
1. From the target VPC's list item, click the **Public IPs** button.
1. Click on **Acquire IP address**
![Acquire IP address](/assets/load-balancing-en-1.jpeg) <br><br>
![IP address acquired](/assets/load-balancing-en-2.jpeg)
1. Add a load balancing rule to the newly acquired Public IP address:
![Load balancer rules](/assets/load-balancing-en-3.jpeg) <br><br>
![Add load balancer rule](/assets/load-balancing-en-4.jpeg)
1. Name your new rule, then specify the TCP port to load-balance and indicate the tier containing the target instances:
![Add load balancer rule, basic info](/assets/load-balancing-en-5.jpeg)
1. Select the desired balancing algorithm. In this case, we don't prescribe any stickiness policy and we load-balance TCP traffic:
![Add load balancer rule, policies](/assets/load-balancing-en-6.jpeg) <br><br>
![Add load balancer rule, configuration](/assets/load-balancing-en-7.jpeg)
1. Select the instances that you wish to load-balance:
![Add load balancer rule, instances](/assets/load-balancing-en-8.jpeg)
1. You will then get confirmation that the rules were successfully applied:
![Load balancer rule created](/assets/load-balancing-en-9.jpeg)
1. Click on the *Public IP addresses* link in the breadcrumb and validate that the displayed information reflects your newly created rule:
![List of public IP addresses](/assets/load-balancing-en-10.jpeg)
1. Finally, check the load-balancing rules are working as expected by running some traffic and verify if each server is serving an equal share of the requests. One way you can achieve this is by forcing each server to return a slightly different answer (e.g.: the host name of the server) in its response (or response headers).
