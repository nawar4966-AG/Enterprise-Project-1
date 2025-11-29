
Switch(config)#hostname SW2  
SW2(config)#vtp mode client  
SW2(config)#vtp domain scal  
SW2(config)#vtp password 1234  
SW2(config)#interface range f0/5 - 10  
SW2(config-if-range)#switchport mode trunk  
SW2(config-if-range)#ex  
SW2(config)#interface range f0/5 - 8  
SW2(config-if-range)#channel-group 1 mode passive  
SW2(config-if-range)#ex  
SW2(config)#interface range f0/1 - 2  
SW2(config-if-range)#switchport access vlan 30  
SW2(config-if-range)#interface range f0/3 - 4  
SW2(config-if-range)#switchport access vlan 40  
SW2(config-if-range)#ex  
SW2(config)#spanning-tree mode pvst  
SW2(config)#spanning-tree vlan 10,20 root secondary  
SW2(config)#spanning-tree vlan 30,40 root primary

! Port Security
SW1(config)#interface range f0/1 - 4  
SW1(config-if-range)#switchport mode access  
SW1(config-if-range)#switchport port-security  
SW1(config-if-range)#switchport port-security maximum 1  
SW1(config-if-range)#switchport port-security mac-address sticky  
SW1(config-if-range)#switchport port-security violation shutdown
SW1(config-if-range)#interface range f0/11 - 24
SW1(config-if-range)#shutdown