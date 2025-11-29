
Router(config)#hostname ISP1  
ISP1(config)#interface gig0/0/0  
ISP1(config-if)#no shutdown  
ISP1(config-if)#ip address 20.20.20.200 255.255.255.0  
ISP1(config-if)#interface gig0/0/1  
ISP1(config-if)#no shutdown  
ISP1(config-if)#ip address 30.30.30.100 255.255.255.0

! OSPF Area 0 setup
ISP1(config)#router ospf 1  
ISP1(config-router)#network 20.20.20.0 0.0.0.255 area 0  
ISP1(config-router)#network 30.30.30.0 0.0.0.255 area 0