en  
conf t  
hostname ServerSW  
vtp mode server  
vtp domain scal  
vtp password 1234  
vlan 10  
name a  
vlan 20  
name b  
vlan 30  
name c  
vlan 40  
name d  
interface range f0/1 - 9  
switchport mode trunk  
ex  
interface range f0/1 - 4  
channel-group 1 mode active  
interface range f0/5 - 8  
channel-group 2 mode active  
end  
wr  
