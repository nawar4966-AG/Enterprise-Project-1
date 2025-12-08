# Verification Guide and Screenshots
This document contains all validation commands required to verify the functionality of the entire topology.
Each section includes the commands to run and the expected results.

## 1. Layer 3 Routing Verification
### 1.1 OSPF Neighbor Adjacency 
Run on: R1, Modem, ISP1, ISP2, ISP4
`show ip ospf neighbor`
Expected:
- At least one FULL adjacency per router (usually with ISP).
  ![[Pasted image 20251130185151.png]]
### 1.2 Routing Table Verification
Run on all routers:
`show ip route`
Expected:
- OSPF routes (marked with “O”) for all remote VLAN subnets.
- Connected gateways for local VLANs (marked “C”).
- Default routes (marked with “S*”) 
  ![[Pasted image 20251201181522.png]]

## 2. PAT NATing
Run on R1 and Modem:
`show ip nat translations`
Expected:
- Line protocol: up
  ![[Pasted image 20251130190018.png]]

## 3. DHCP (R1)
### 3.1 DHCP Bindings
Run on R1:
`show ip dhcp binding`
Expected:
- Dynamic bindings for PCs in each VLAN
  ![[Pasted image 20251130192851.png]]
### 3.2 DHCP Pools
`show ip dhcp pool`
Expected:
- Pools for VLANs with correct usage counters.
  ![[Pasted image 20251130193302.png]]

## 4. VLAN, VTP & Trunking Verification
### 4.1 VLAN Existence
Run on any switch:
`show vlan brief`
Expected:
- VLAN IDs 10,20,30,40 depending on site
- Ports in correct VLANs
  ![[Pasted image 20251130201114.png]]
  
### 4.2 VTP Status
Run on switches:
`show vtp status`
Expected:
- VTP domain matches site domain (scal)
- Server switch: Mode = server
- Downstream switches: Mode = client
  ![[Pasted image 20251201181738.png]]
  ![[Pasted image 20251201181909.png]]
  
### 4.3 Trunk Verification
`show interfaces trunk`
Expected:
- Correct allowed VLANs
- EtherChannel interfaces bundled as Po1 and Po2
- Mode: trunk
  ![[Pasted image 20251130201728.png]]

## 5. EtherChannel Verification
On all Switches:
`show etherchannel summary`
Expected:
- LACP protocols
- Ports marked (P) for “bundled and in use”
  ![[Pasted image 20251130201935.png]]

## 6. Spanning Tree (PVST)
### 6.1 STP Mode
On all Switches:
`show spanning-tree summary`
Expected:
- Mode: pvst
- Each assigned VLAN is blocking one port 
  ![[Pasted image 20251130202422.png]]

### 6.2 Per VLAN Root Role
On all Switches:
`show spanning-tree`
Expected:
- Primary root matches design (SW1 for VLAN 10/20 etc.)
- Secondary root matches opposite distribution switch
  ![[Pasted image 20251130203215.png]]
  ![[Pasted image 20251130203407.png]]

## 7. Management Plane Verification
### 7.1 SSH
On any PC from VLAN 10 for example.
CMD:
`ssh -l admin 10.10.10.100` 
Expected:
- Prompted for SSH ID and PW.
  ![[Pasted image 20251130204237.png]]

### 7.2 Port Security
On access switches:
`show port-security`
`show port-security address`


## 8. ACL Behavior Verification
Test each ACL from the affected PCs:
### ACL 110: PC7 cannot HTTP the server
From a PC in VLAN 10:
`http://60.60.60.1`
Expected: Request Timeout
![[Pasted image 20251130205219.png]]

### ACL 110: PC6 cannot ping the server
From PC6:
`ping 60.60.60.1` 
Expected: Fail
![[Pasted image 20251130210632.png]]

## 9. End-to-End Connectivity Tests
From various PCs:
`ping 60.60.60.1` 
![[Pasted image 20251130211526.png]]

From R1:
`ping 60.60.60.1`
`traceroute 60.60.60.1`
Expected:
- All permitted traffic reaches the destination
- OSPF-learned routes and default route used in traceroute passing on **5** router ports
  ![[Pasted image 20251130211731.png]]
  ![[Pasted image 20251130211843.png]]

## 10. Final Status Check (All Devices)
Run:
`show ip interface brief`
`show running-config`
`show startup-config`
Expected:
- No down/down critical interfaces
- Configs saved properly
- No unexpected VLANs or trunks