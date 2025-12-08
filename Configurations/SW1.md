en  
conf t  
hostname SW1  
vtp mode client  
vtp domain scal  
vtp password 1234  
interface range f0/5 - 10  
switchport mode trunk  
ex  
interface range f0/5 - 8  
channel-group 2 mode passive    
ex  
interface range f0/1 - 2  
switchport access vlan 10  
interface range f0/3 - 4  
switchport access vlan 20  
ex  
spanning-tree mode pvst   
spanning-tree vlan 10,20 root primary  
spanning-tree vlan 30,40 root secondary  
interface range f0/1 - 4  
switchport mode access  
switchport port-security  
switchport port-security maximum 1  
switchport port-security mac-address sticky  
switchport port-security violation shutdown  
interface range f0/11 - 24  
shutdown  
end  
wr  
