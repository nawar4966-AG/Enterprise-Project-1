# Verification Guide and Screenshots
This document contains all validation commands required to verify the functionality of the entire topology.
Each section includes the commands to run and the expected results.

## 1. Layer 3 Routing Verification
### 1.1 OSPF Neighbor Adjacency 
Run on: Modem, ISP1, ISP2, ISP4
`show ip ospf neighbor`
Expected:
- At least one FULL adjacency per router (usually with ISP).

  <img width="646" height="142" alt="image" src="https://github.com/user-attachments/assets/3e268126-bbde-4be2-8698-2a0f752063a6" />

### 1.2 Routing Table Verification
Run on all routers:
`show ip route`
Expected:
- OSPF routes (marked with “O”) for all remote VLAN subnets.
- Connected gateways for local VLANs (marked “C”).
- Default routes (marked with “S*”)

  <img width="583" height="346" alt="image" src="https://github.com/user-attachments/assets/7beba071-fbce-4810-9037-5af0bba42a76" />
  
  <img width="565" height="341" alt="image" src="https://github.com/user-attachments/assets/c12b1da8-a8f8-49ed-abdc-b232b31a2b83" />



## 2. PAT NATing
Run on Modem:
`show ip nat translations`
Expected:
- The NAT IP first then the private IP followed by the destination IP (the Server) from the PCs who only tried to Ping or HTTP a device outside the network

  <img width="579" height="347" alt="image" src="https://github.com/user-attachments/assets/2015c3a6-99ed-466e-8053-49dd48077db0" />


## 3. DHCP (R1)
### 3.1 DHCP Bindings
Run on R1:
`show ip dhcp binding`
Expected:
- Dynamic bindings for PCs in each VLAN

  <img width="576" height="165" alt="image" src="https://github.com/user-attachments/assets/6c8b0dfe-3fe4-4572-a802-63ff4e3adbd9" />

### 3.2 DHCP Pools
`show ip dhcp pool`
Expected:
- Pools for VLANs with correct usage counters.

  <img width="626" height="659" alt="image" src="https://github.com/user-attachments/assets/4ba1c076-9f95-4949-9344-b3ea4b8cc202" />


## 4. VLAN, VTP & Trunking Verification
### 4.1 VLAN Existence
Run on access switches:
`show vlan brief`
Expected:
- VLAN IDs 10,20,30,40 depending on site
- Ports in correct VLANs

  <img width="578" height="239" alt="image" src="https://github.com/user-attachments/assets/d0ca21e5-90a0-4f44-bf6b-e1b508c98033" />

  
### 4.2 VTP Status
Run on switches:
`show vtp status`
Expected:
- VTP domain matches site domain (scal)
- Server switch: Mode = server
- Downstream switches: Mode = client

  <img width="543" height="250" alt="image" src="https://github.com/user-attachments/assets/96a51088-4671-41f1-889f-7c38864793b5" />

  <img width="537" height="236" alt="image" src="https://github.com/user-attachments/assets/872e2991-7190-4836-8894-15611205c8c8" />

  
### 4.3 Trunk Verification
`show interfaces trunk`
Expected:
- Correct allowed VLANs
- EtherChannel interfaces bundled as Po1 and Po2
- Mode: trunk

  <img width="498" height="291" alt="image" src="https://github.com/user-attachments/assets/0988e19e-0b3b-4558-ab74-30ee241538d9" />


## 5. EtherChannel Verification
On all Switches:
`show etherchannel summary`
Expected:
- LACP protocols
- Ports marked (P) for “bundled and in use”

  <img width="538" height="259" alt="image" src="https://github.com/user-attachments/assets/ea4b43ed-462f-4d60-b08c-8bee1531a066" />


## 6. Spanning Tree (PVST)
### 6.1 STP Mode
On access switches:
`show spanning-tree summary`
Expected:
- Mode: pvst
- Only Primary VLANs are note blocked 

  <img width="529" height="326" alt="image" src="https://github.com/user-attachments/assets/1d26cccf-eb52-4416-98c9-93cb61f15133" />


### 6.2 Per VLAN Root Role
On all Switches:
`show spanning-tree`
Expected:
- Primary root matches design (SW1 for VLAN 10/20 etc.)
- Secondary root matches opposite distribution switch

  <img width="550" height="571" alt="image" src="https://github.com/user-attachments/assets/2ed6e6af-9779-4899-96a6-7b592757b56f" />

  <img width="550" height="614" alt="image" src="https://github.com/user-attachments/assets/f4c1c3fb-0f69-4e0a-81cb-c60d4cdad41e" />


## 7. Management Plane Verification
### 7.1 SSH
On any PC from VLAN 10 for example.
CMD:
`ssh -l admin 10.10.10.100` 
Expected:
- Prompted for SSH ID and PW.

  <img width="388" height="168" alt="image" src="https://github.com/user-attachments/assets/041f32be-b6b5-4bc6-9f7c-eb066afe11e5" />


### 7.2 Port Security
On access switches:
`show port-security`
`show port-security address`

<img width="511" height="131" alt="image" src="https://github.com/user-attachments/assets/278ac500-202e-4773-9802-7d1cf97c12c4" />

<img width="554" height="185" alt="image" src="https://github.com/user-attachments/assets/d43b771a-51df-47de-a394-5f70a84645c4" />



## 8. ACL Behavior Verification
Test each ACL from the affected PCs:
### ACL 110: PC7 cannot HTTP the server
From a PC in VLAN 10:
`http://60.60.60.1`
Expected: Request Timeout

<img width="697" height="293" alt="image" src="https://github.com/user-attachments/assets/d60090ac-73f8-44d5-afe9-6b0a002fe46a" />


### ACL 110: PC6 cannot ping the server
From PC6:
`ping 60.60.60.1` 
Expected: Fail

<img width="565" height="358" alt="image" src="https://github.com/user-attachments/assets/ced0363f-7fe4-4e3d-886c-e3ea6fd2bec9" />


## 9. End-to-End Connectivity Tests
From various PCs:
`ping 60.60.60.1` 

<img width="488" height="345" alt="image" src="https://github.com/user-attachments/assets/35221aaf-0b3d-4226-a1a5-aa7f96303ec2" />

From various PCs:
`http://60.60.60.1` 

<img width="702" height="368" alt="image" src="https://github.com/user-attachments/assets/c99aaef7-57cc-405c-91ce-7891e26b750d" />


From R1:
`ping 60.60.60.1`
`traceroute 60.60.60.1`
Expected:
- All permitted traffic reaches the destination
- OSPF-learned routes and default route used in traceroute passing on 5 router ports

  <img width="496" height="135" alt="image" src="https://github.com/user-attachments/assets/930a5319-b6bb-4099-a686-f47566502ff3" />

  <img width="380" height="146" alt="image" src="https://github.com/user-attachments/assets/4c3fe95d-82d1-45f8-91a1-66c2c23e9768" />


## 10. Final Status Check (All Devices)
Run:
`show ip interface brief`
`show running-config`
`show startup-config`
Expected:
- No down/down critical interfaces
- Configs saved properly
- No unexpected VLANs or trunks
