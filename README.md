<h1>Network Home Lab</h1>

<h2>Description</h2>
Simulate Network Home Lab with Cisco Packet Tracer. Configure 3 routers with SSH, DHCP frame relay, OSPF and security features/protocols. Configure 3 swtiches with SSH, VLAN, etherchannel, HSRP and security features/protocols. Deploy PC for remote management and PCs for verifying functionality of network services. Configure 1 firewall with ACLs, IPS/IDS, antivirus, VPN, content filtering, segmented security zones and implicit deny rules. <br />

<h2>Environments Used </h2>

- <b>Cisco Packet Tracer</b> (2.2.43) <br />

- <b>Cisco IOS C2900 Software, Version 15.1(4)M5</b>  <br />

[Software Configuration Guide](https://www.cisco.com/c/en/us/td/docs/routers/access/1900/software/configuration/guide/Software_Configuration.html)<br />

- <b>Cisco IOS Denali, Catalyst L3 Switch Software, Version 16.3.2</b> <br />

[Command Reference](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3650/software/release/16-3/command_reference/b_163_consolidated_3650_cr.html)<br />

[Software Configuration Guide](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3650/software/release/16-3/configuration_guide/b_163_consolidated_3650_cg.html)<br />

- <b>Cisco 5506-X ASA</b> (22H2) <br />

<h2>Diagram </h2>
<img src="https://i.imgur.com/tyy7e8c.png" height="80%" width="80%" />

<h2>Walk-through:</h2>
<p align="center">
 
[Download Cisco Packet Tracer](https://skillsforall.com/resources/lab-downloads?courseLang=en-US 
)<br />

<br />
<br />
Drag and frop devices as seen in the diagram. Connect devices with appropriate cabling. Run command 'show cdp neighbors' to label interfaces. Label devices with hostnames: <br/>
<img src="https://i.imgur.com/6raWWEw.png" height="80%" width="80%" />
<br />
<br />
Router basic/security, SSH and line configurations. Verfiy and save result on R1. Repeat process on all routers: <br/>
Router>en <br/>
Router#conf t <br/>
Router(config)#hostname R1 <br/>
R1(config)#security passwords min-length 5 <br/>
R1(config)#service password-encryption <br/>
R1(config)#login block-for 60 attempts 3 within 30 <br/>
R1(config)#enable secret PASSWORD <br/>
R1(config)#no ip domain-lookip <br/>
R1(config)#banner motd b <br/>
Enter: HELLO b <br/>
R1(config)#username jwczerwinski privilege 15 secret PASSWORD <br/>
R1(config)# ip domain-name corpdomain.com <br/>
R1(config)# crypto key generate rsa <br/>
Enter: 1024 <br/>
R1(config)# ip ssh version 2 <br/>
R1(config)#line console 0 <br/>
R1(config-line)#password PASSWORD <br/>
R1(config-line)#login <br/>
R1(config-line)#logging synchronous <br/>
R1(config-line)#exec-timeout 15 0 <br/>
R1(config)#line vty 0 4 <br/>
R1(config-line)#password PASSWORD <br/>
R1(config-line)# login local <br/>
R1(config-line)#logging synchronous <br/>
R1(config-line)#exec-timeout 15 0 <br/>
R1(config-line)# transport input ssh <br/>
R1(config)#do show running-config <br/>
R1#wr <br/>
<img src="https://i.imgur.com/oJ3FATv.png" height="80%" width="80%" />
<img src="https://i.imgur.com/f9lgi5f.png" height="80%" width="80%" />
<img src="https://i.imgur.com/7gwO5tg.png" height="80%" width="80%" />
<br />
<br />
Switch basic/security, SSH and line configurations. Verfiy and save result on MS1. Repeat process on all switches: <br/>
Switch>en <br/>
Switch#conf t <br/>
Switch(config)#hostname MS1 <br/>
MS1(config)#service password-encryption <br/>
MS1(config)#login block-for 60 attempts 3 within 30 <br/>
MS1(config)#enable secret PASSWORD <br/>
MS1(config)#banner motd b <br/>
Enter: HELLO b <br/>
MS1(config)#username jwczerwinski privilege 15 secret PASSWORD <br/>
MS1(config)# ip domain-name corpdomain.com <br/>
MS1(config)# crypto key generate rsa <br/>
Enter: 1024 <br/>
MS1(config)# ip ssh version 2 <br/>
MS1(config)#line console 0 <br/>
MS1(config-line)#password PASSWORD <br/>
MS1(config-line)#login <br/>
MS1(config-line)#logging synchronous <br/>
MS1(config-line)#exec-timeout 15 0 <br/>
MS1(config)#line vty 0 15 <br/>
MS1(config-line)#password PASSWORD <br/>
MS1(config-line)# login local <br/>
MS1(config-line)#logging synchronous <br/>
MS1(config-line)#exec-timeout 15 0 <br/>
MS1(config-line)# transport input ssh <br/>
MS1(config)#do show run <br/>
MS1#wr <br/>
<img src="https://i.imgur.com/JtDqSZZ.png" height="80%" width="80%" />
<img src="https://i.imgur.com/NwzxcPO.png" height="80%" width="80%" />
<img src="https://i.imgur.com/bLpRQgD.png" height="80%" width="80%" />
<br />
<br />
Configure static IP addressing on routers per diagram. Verify results and repeat for all router interfaces: <br/>
R1(config)#interface G0/0 <br/>
R1(config)#ip address 172.16.0.1 255.255.255.252  <br/>
R1(config)#description ## to MS1 ## <br/>
R1(config)#no shutdown <br/>
R1(config)#do wr <br/>
R1(config)#do show interface <br/>
R1(config)#do show ip interface brief <br/>
<img src="https://i.imgur.com/5mMABd9.png" height="80%" width="80%" />
<img src="https://i.imgur.com/p1ljvs7.png" height="80%" width="80%" />
<img src="https://i.imgur.com/DWI9Jcw.png" height="80%" width="80%" />
<br />
<br />
Configure SVI Switch Management Interfaces and default-gateways: <br/>
MS1(config)# interface vlan 1 <br/>
MS1(config-if)# description ## Management interface for this switch ## <br/>
MS1(config-if)# ip address 192.168.0.33  255.255.255.248 <br/>
MS1(config-if)# no shut <br/>
MS1(config-if)# exit <br/>
MS1(config)# ip default-gateway 172.16.0.17 <br/>
MS1(config)# do show run <br/>
<img src="https://i.imgur.com/rK05GfX.png" height="80%" width="80%" />
<br />
<br />
Configure IP routing, routed ports and IP addresses on all switch interfaces. Also, etherchannel for redudant switch connections (configure same port-channel # on both sides of connection): <br/>
MS1(config)# ip routing <br/>
MS1(config)# interface range G1/0/1 - G1/0/7 <br/>
MS1(config-if-range)# no switchport <br/>
MS1(config)# interface range G1/0/4 - G1/0/5 <br/>
MS1(config-if-range)# channel-group 1 mode active <br/>
MS1(config)# interface port-channel 1 <br/>
MS1(config-if)# ip address 192.168.0.21 255.255.255.252 <br/>
MS1(config)# interface G1/0/1 <br/>
MS1(config-if)# ip address 172.16.0.10 255.255.255.252 <br/>
<img src="https://i.imgur.com/29i0Twt.png" height="80%" width="80%" />
<br />
<br />
Configure OSPF dynamic routing on all network devices. Also, configure static routes to end points or a gateway of last resort. Verify results with 'show' and 'tracert' commands: <br/>
R2(config)#router ospf 1  <br/>
R2(config-router)#network 0.0.0.0 255.255.255.255 area 0  <br/>
R2(config)#do show ip ospf <br/>
R2(config)# ip route 0.0.0.0 255.255.255.255 172.16.0.2 <br/>
R2(config)#do show ip route <br/>
<img src="https://i.imgur.com/fVBh1K2.png" height="80%" width="80%" />
<img src="https://i.imgur.com/gbrPydo.png" height="80%" width="80%" />
<br />
<br />
Configure DHCP/DNS Server with IP addressing and routers/switches as DHCP relay agents. Verify results with 'ipconfig' command: <br/>
R2(config)#interface G0/0  <br/>
R2(config-if)#ip helper-address 172.16.0.2  <br/>
MS1(config)#interface port-channel 2  <br/>
MS1(config-if)#ip helper-address 172.16.0.2  <br/>
MS2(config)#interface G1/0/5  <br/>
MS2(config-if)#ip helper-address 172.16.0.2  <br/>
<img src="https://i.imgur.com/aNAKrgO.png" height="80%" width="80%" />
<br />
<br />
Configure HSRP version 2 on all switches and set priority in order MS1 - MS3: <br/>
Group 1 <br/>
MS1(config)#interface range g1/0/1 - g1/0/7  <br/>
MS1(config-if-range)#standby version 2  <br/>
MS1(config-if-range)#standby 1 ip 192.168.0.29 <br/>
MS1(config-if-range)#standby 1 priority 101 <br/>
MS1(config-if-range)#standby 1 preempt <br/>
MS2(config)#interface range g1/0/1 - g1/0/4  <br/>
MS2(config-if-range)#standby version 2  <br/>
MS2(config-if-range)#standby 1 ip 192.168.0.29 <br/>
MS2(config-if-range)#standby 1 priority 100 <br/>
MS3(config)#interface range g1/0/1 - g1/0/8  <br/>
MS3(config-if-range)#standby version 2  <br/>
MS3(config-if-range)#standby 1 ip 192.168.0.29 <br/>
MS3(config-if-range)#standby 1 priority 99 <br/>
show standby brief
<img src="https://i.imgur.com/TRkdq2m.png" height="80%" width="80%" />
<img src="https://i.imgur.com/zYbRv0r.png" height="80%" width="80%" />
<img src="https://i.imgur.com/533gj9O.png" height="80%" width="80%" />
