
Router(config)#hostname Modem  
Modem(config)#interface gig0/0/0  
Modem(config-if)#no shutdown  
Modem(config-if)#ip address 192.168.1.200 255.255.255.0  
Modem(config-if)#interface gig0/0/1  
Modem(config-if)#no shutdown  
Modem(config-if)#ip address 20.20.20.100 255.255.255.0

! OSPF Area 0 setup
Modem(config)#router ospf 1  
Modem(config-router)#network 20.20.20.0 0.0.0.255 area 0  
Modem(config-router)#network 192.168.1.0 0.0.0.255 area 0

! NAT (static routing)
Modem(config)#ip route 10.10.10.0 255.255.255.0 192.168.1.100 
Modem(config)#ip route 10.20.20.0 255.255.255.0 192.168.1.100 
Modem(config)#ip route 10.30.30.0 255.255.255.0 192.168.1.100 
Modem(config)#ip route 10.40.40.0 255.255.255.0 192.168.1.100 
Modem(config)#interface gig0/0/0 
Modem(config-if)#ip nat inside Modem(config-if)#interface gig0/0/1 
Modem(config-if)#ip nat outside Modem(config-if)#ex 
Modem(config)#access-list 1 permit 10.10.10.0 0.0.0.255 
Modem(config)#access-list 2 permit 10.20.20.0 0.0.0.255 
Modem(config)#access-list 3 permit 10.30.30.0 0.0.0.255 
Modem(config)#access-list 4 permit 10.40.40.0 0.0.0.255 
Modem(config)#ip nat inside source list 1 interface gig0/0/1 overload 
Modem(config)#ip nat inside source list 2 interface gig0/0/1 overload 
Modem(config)#ip nat inside source list 3 interface gig0/0/1 overload 
Modem(config)#ip nat inside source list 4 interface gig0/0/1 overload