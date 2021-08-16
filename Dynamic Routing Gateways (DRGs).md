# Dynamic Routing Gateways (DRGs)



Here in this talk I'm going to discuss about the Dynamic Routing Gateways or DRG.

What is DRG?
Basically DRG is noting but router, providing a path for traffic between your on-premises networks and VCNs. A DRG is a virtual router to which you can attach the following resources:

- VCNs:  you can attach multiple VCNs to a single DRG. Each VCN can be in the same or different tenancies as the DRG.
- Remote peering connections: you can peer a DRG to other DRGs (including DRGs in other regions) using remote peering connections.
- Site-to-Site VPN IPSec tunnels: you can use Site-to-Site VPN to attach two or more IPSec tunnels to your DRG to connect to on-premises networks. This is also allowed across tenancies.
- Fast Connect virtual Circuits: you can attach one or more FastConnect virtual circuits to your DRG to connect to on-premises networks.



What else?

Route Tables

-  Each DRG attachment has an associated route table which is used to route packets entering the DRG to their next hop.
- These routes can be dynamically imported and exported through these attachments. 

How to set-up?

As mentioned, DRG, must be attached to other network resources, so, while creating we have to define the type of the object:

- VCN

- VIRTUAL_CIRCUIT

- IPSEC_TUNNEL

- REMOTE_PEERING_CONNECTION

  

  All the packets are getting routed using rules in the DRG route table assigned to the attachment.
  A sigle route table can be get attached to multiple DRG attachments or 
  You can also create a dedicated route table for each attachment 