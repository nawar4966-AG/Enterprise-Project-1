en  
conf t  
hostname ISP4  
interface gig0/0/0  
no shutdown  
ip address 50.50.50.200 255.255.255.0  
interface gig0/0/1  
no shutdown  
ip address 60.60.60.100 255.255.255.0  
router ospf 1   
network 50.50.50.0 0.0.0.255 area 0  
network 60.60.60.0 0.0.0.255 area 0  
end  
wr  
