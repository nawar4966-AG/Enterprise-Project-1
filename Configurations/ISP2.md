en
conf t
hostname ISP2  
interface gig0/0/0  
no shutdown  
ip address 30.30.30.200 255.255.255.0  
interface gig0/0/1  
no shutdown  
ip address 40.40.40.100 255.255.255.0
router ospf 1  
network 40.40.40.0 0.0.0.255 area 0  
network 30.30.30.0 0.0.0.255 area 0
end
wr
