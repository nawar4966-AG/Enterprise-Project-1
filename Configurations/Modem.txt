en  
conf t  
hostname Modem  
interface gig0/0/0  
no shutdown  
ip address 192.168.1.200 255.255.255.0  
interface gig0/0/1  
no shutdown  
ip address 20.20.20.100 255.255.255.0  
router ospf 1   
network 20.20.20.0 0.0.0.255 area 0   
network 192.168.1.0 0.0.0.255 area 0  
ip route 10.10.10.0 255.255.255.0 192.168.1.100   
ip route 10.20.20.0 255.255.255.0 192.168.1.100   
ip route 10.30.30.0 255.255.255.0 192.168.1.100   
ip route 10.40.40.0 255.255.255.0 192.168.1.100   
interface gig0/0/0   
ip nat inside  
interface gig0/0/1   
ip nat outside  
ex   
access-list 1 permit 10.10.10.0 0.0.0.255   
access-list 2 permit 10.20.20.0 0.0.0.255   
access-list 3 permit 10.30.30.0 0.0.0.255   
access-list 4 permit 10.40.40.0 0.0.0.255   
ip nat inside source list 1 interface gig0/0/1 overload   
ip nat inside source list 2 interface gig0/0/1 overload   
ip nat inside source list 3 interface gig0/0/1 overload   
ip nat inside source list 4 interface gig0/0/1 overload  
ex  
wr  
