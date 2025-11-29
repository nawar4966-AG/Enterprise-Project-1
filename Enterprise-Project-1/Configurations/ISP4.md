
Router(config)#hostname ISP4  
ISP4(config)#interface gig0/0/0  
ISP4(config-if)#no shutdown  
ISP4(config-if)#ip address 50.50.50.200 255.255.255.0  
ISP4(config-if)#interface gig0/0/1  
ISP4(config-if)#no shutdown  
ISP4(config-if)#ip address 60.60.60.100 255.255.255.0

! OSPF Area 0 setup
ISP4(config)#router ospf 1  
ISP4(config-router)#network 50.50.50.0 0.0.0.255 area 0  
ISP4(config-router)#network 60.60.60.0 0.0.0.255 area 0