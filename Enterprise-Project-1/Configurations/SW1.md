
Switch(config)#hostname SW1  
SW1(config)#vtp mode client  
SW1(config)#vtp domain scal  
SW1(config)#vtp password 1234  
SW1(config)#interface range f0/5 - 10  
SW1(config-if-range)#switchport mode trunk  
SW1(config-if-range)#ex  
SW1(config)#interface range f0/5 - 10  
SW1(config-if-range)#channel-group 2 mode passive  
SW1(config-if-range)#ex  
SW1(config)#interface range f0/1 - 2  
SW1(config-if-range)#switchport access vlan 10  
SW1(config-if-range)#interface range f0/3 - 4  
SW1(config-if-range)#switchport access vlan 20  
SW1(config-if-range)#ex  
SW1(config)#spanning-tree mode pvst  
SW1(config)#spanning-tree vlan 10,20 root primary  
SW1(config)#spanning-tree vlan 30,40 root secondary


! Port Security
SW1(config)#interface range f0/1 - 4  
SW1(config-if-range)#switchport mode access  
SW1(config-if-range)#switchport port-security  
SW1(config-if-range)#switchport port-security maximum 1  
SW1(config-if-range)#switchport port-security mac-address sticky  
SW1(config-if-range)#switchport port-security violation shutdown
SW1(config-if-range)#interface range f0/11 - 24
SW1(config-if-range)#shutdown
