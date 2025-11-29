
Switch(config)#hostname ServerSW
ServerSW(config)#vtp mode server
ServerSW(config)#vtp domain scal
ServerSW(config)#vtp password 1234
ServerSW(config)#vlan 10
ServerSW(config-vlan)#name a
ServerSW(config-vlan)#vlan 20
ServerSW(config-vlan)#name b
ServerSW(config-vlan)#vlan 30
ServerSW(config-vlan)#name c
ServerSW(config-vlan)#vlan 40
ServerSW(config-vlan)#name d
ServerSW(config)#interface range f0/1 - 9
ServerSW(config-if-range)#switchport mode trunk
ServerSW(config-if-range)#ex
ServerSW(config)#interface range f0/1 - 4
ServerSW(config-if-range)#channel-group 1 mode active
ServerSW(config-if-range)#interface range f0/5 - 8
ServerSW(config-if-range)#channel-group 2 mode active

