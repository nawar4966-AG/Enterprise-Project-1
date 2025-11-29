
Router(config)#hostname ISP2  
ISP2(config)#interface gig0/0/0  
ISP2(config-if)#no shutdown  
ISP2(config-if)#ip address 30.30.30.200 255.255.255.0  
ISP2(config-if)#interface gig0/0/1  
ISP2(config-if)#no shutdown  
ISP2(config-if)#ip address 40.40.40.100 255.255.255.0

! OSPF Area 0 setup
ISP2(config)#router ospf 1  
ISP2(config-router)#network 40.40.40.0 0.0.0.255 area 0  
ISP2(config-router)#network 30.30.30.0 0.0.0.255 area 0