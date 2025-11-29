# Enterprise LAN + Multi-Hop WAN (CCNA-Level Project)
## Topology
![[Pasted image 20251128224724.png]]

![[Pasted image 20251128224915.png]]

## Objective
A complete CCNA-level enterprise LAN and multi-hop WAN project implementing VLANs, STP, EtherChannel, DHCP, ACLs, NAT, SSH, inter-VLAN routing, and OSPF to provide secure, scalable connectivity from internal hosts to a remote server through multiple ISP routers.

## Technologies Used
• VLAN Segmentation
Separation of users into VLANs 10, 20, 30, and 40 with unique subnets for structured network isolation.

• Inter-VLAN Routing (Router-on-a-Stick)
Subinterfaces configured on the edge router to route traffic between VLANs.

• DHCP for Multiple VLANs
Centralized DHCP pools providing automatic IP addressing for all user networks.

• NAT Overload (PAT)
Internal VLAN networks NATed to a single public interface for outbound connectivity.

• Extended Access Control Lists (ACLs)
Traffic filtering rules applied to enforce specific user restrictions, such as blocking HTTP or ICMP to the server.

• Spanning Tree Protocol (PVST)
Loop prevention and load-balancing across the redundant Layer-2 switches.

• EtherChannel (LACP)
Bundling physical links between switches into logical Port-Channels to increase bandwidth and provide redundancy.

• VTP (VLAN Trunking Protocol)
Centralized VLAN distribution using a VTP server with multiple VTP clients (lab purposes).

• OSPF Area 0 
Dynamic routing across multiple ISP routers, forming a multi-hop routed WAN path.

• Multi-Router WAN Simulation
End-to-end communication through ISP1 → ISP2 → ISP3 → ISP4, simulating a real provider network. (ISP: Internet Service Provider)

• Static Routing
Upstream device (R1) configured with static routes to internal VLANs to ensure bidirectional connectivity.

• Secure Remote Access via SSH
Router and switch management protected through encrypted SSH sessions.

• Port Security on Access Switches
MAC-address limiting and sticky learning to prevent unauthorized hosts from connecting to access ports.

• End-to-End Server Connectivity
Internal VLAN clients reaching a remote server across multiple routed hops with ACL-based restrictions applied.

## Verification Commands

### Routers (Inter-VLAN Routing + NAT + DHCP)
show ip interface brief
show ip route
show ip dhcp binding
show ip dhcp pool
show access-lists
show ip nat translations
show ip ospf neighbor
show ip ospf interface brief

### Switches (STP, EtherChannel, VLANs)
show vlan brief
show interfaces trunk
show etherchannel summary
show vtp status

### Access Switches (Port Security + VLAN Assignments)
show port-security
show port-security interface f0/3
show port-security address
show vlan brief
show interfaces switchport

### WAN Routers (OSPF + Routing Path Verification)
show ip ospf neighbor
show ip route ospf

### Testing ACL Behavior
telnet server-ip 80 (should be denied for PC7)
ping server-ip (should be denied for PC6)

## Brief Explanation of Design Decisions
1. VLAN Segmentation
	The network is divided into multiple VLANs (10, 20, 30, 40) to separate departments and reduce broadcast domains.
2. Router-on-a-Stick for Inter-VLAN Routing
	A single router handles routing between VLANs using subinterfaces. This design demonstrates how Layer-2 networks rely on a Layer-3 device for inter-VLAN communication.
3. DHCP Centralization
	DHCP pools are configured on the router so all VLANs can receive automatic IP addressing.
4. NAT Overload at the Edge Router
	NAT (PAT) is implemented so internal private VLANs can access external networks using one public-facing interface.
5. ACL-Based Traffic Control
	ACLs are placed at the router subinterfaces to enforce simple security policies (blocking HTTP or ICMP for specific hosts).
6. PVST for Loop Prevention
	Spanning Tree is used across the Layer-2 switches to prevent loops created by redundant links, making the topology both redundant and stable.
7. EtherChannel for Redundancy and Bandwidth
	Multiple physical links between switches are bundled into Port-Channels to provide both increased bandwidth and redundancy
8. Multi-Hop WAN Simulation with OSPF
	The WAN path includes several ISP routers running OSPF Area 0 to simulate provider routing.
9. Static Routes for Return Traffic
	Upstream routers use static routes back to the internal VLANs to maintain bidirectional connectivity.
10. SSH for Secure Management
	SSH is used instead of Telnet to protect device access with encryption.