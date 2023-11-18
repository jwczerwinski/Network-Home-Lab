<h1>Network Home Lab</h1>

<h2>Description</h2>
Simulate Network Home Lab with Cisco Packet Tracer. Configure 3 routers with SSH, DHCP, OSPF and security features/protocols. Configure 3 swtiches with SSH, VLANs, etherchannel, RSTP, HSRP and security features/protocols. Deploy PC for remote management and PCs for verifying functionality of network configurations. Configure 1 firewall with ACLs, IPS/IDS, antivirus, VPN, content filtering, segmented security zones and implicit deny rules. <br />

<h2>Environments Used </h2>
- <b>Cisco Packet Tracer</b> (2.2.43) <br />
- <b>Cisco 8190HGW Router</b>  <br />
- <b>Cisco 3650-24PS Multilayer Switch</b> <br />

[Command Reference](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3650/software/release/16-3/command_reference/b_163_consolidated_3650_cr.html)<br />
[Software Configuration Guide](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3650/software/release/16-3/configuration_guide/b_163_consolidated_3650_cg.html)<br />
- <b>Cisco 5506-X ASA</b> (22H2) <br />

<h2>Diagram </h2>
<img src="https://i.imgur.com/X1JOLQk.png" height="80%" width="80%" />

<h2>Walk-through:</h2>
<p align="center">
 
[Download Cisco Packet Tracer](https://skillsforall.com/resources/lab-downloads?courseLang=en-US 
)<br />

<br />
<br />
Drag and frop devices as seen in the diagram. Connect devices with appropriate cabling: Cross-over - Switch to switch, router to router; Straight through - PC to switch, switch to router; Console - PC to network device (for configuration)): <br/>
<img src="https://i.imgur.com/oL73dBm.png" height="80%" width="80%" />
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
R1(config)#banner motd b <br/>
Enter: HELLO b <br/>
R1(config)# username jwczerwinski <br/>
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
<img src="https://i.imgur.com/yiOfSjt.png" height="80%" width="80%" />
<img src="https://i.imgur.com/qKiXYQi.png" height="80%" width="80%" />
<img src="https://i.imgur.com/bua1WW5.png" height="80%" width="80%" />
<br />
<br />
Switch basic/security, SSH and line configurations. Verfiy and save result on MS1. Repeat process on all switches: <br/>
Switch>en <br/>
Switch#conf t <br/>
Switch(config)#hostname MS1 <br/>
MS1(config)#security passwords min-length 5 <br/>
MS1(config)#service password-encryption <br/>
MS1(config)#login block-for 60 attempts 3 within 30 <br/>
MS1(config)#enable secret PASSWORD <br/>
MS1(config)#banner motd b <br/>
Enter: HELLO b <br/>
MS1(config)# username jwczerwinski <br/>
MS1(config)# ip domain-name corpdomain.com <br/>
MS1(config)# crypto key generate rsa <br/>
Enter: 1024 <br/>
MS1(config)# ip ssh version 2 <br/>
MS1(config)#line console 0 <br/>
MS1(config-line)#password PASSWORD <br/>
MS1(config-line)#login <br/>
MS1(config-line)#logging synchronous <br/>
MS1(config-line)#exec-timeout 15 0 <br/>
MS1(config)#line vty 0 4 <br/>
MS1(config-line)#password PASSWORD <br/>
MS1(config-line)# login local <br/>
MS1(config-line)#logging synchronous <br/>
MS1(config-line)#exec-timeout 15 0 <br/>
MS1(config-line)# transport input ssh <br/>
MS1(config)#do show running-config <br/>
MS1#wr <br/>
<img src="https://i.imgur.com/VtmYWLI.png" height="80%" width="80%" />
<br />
<br />


