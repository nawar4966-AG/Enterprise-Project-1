
Router(config)#hostname ISP3  
ISP3(config)#interface gig0/0/0  
ISP3(config-if)#no shutdown  
ISP3(config-if)#ip address 40.40.40.200 255.255.255.0  
ISP3(config-if)#interface gig0/0/1  
ISP3(config-if)#no shutdown  
ISP3(config-if)#ip address 50.50.50.100 255.255.255.0

! OSPF Area 0 setup
ISP3(config)#router ospf 1  
ISP3(config-router)#network 50.50.50.0 0.0.0.255 area 0  
ISP3(config-router)#network 40.40.40.0 0.0.0.255 area 0