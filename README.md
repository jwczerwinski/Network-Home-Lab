<h1>Network Home Lab</h1>

<h2>Description</h2>
Simulate Network Home Lab with Cisco Packet Tracer. Configure 3 routers with SSH, DHCP, OSPF and security features/protocols. Configure 3 swtiches with SSH, VLANs, etherchannel, RSTP, HSRP and security features/protocols. Deploy PC for remote management and PCs for verifying functionality of network configurations. Configure 1 firewall with ACLs, IPS/IDS, antivirus, VPN, content filtering, segmented security zones and implicit deny rules. <br />

<h2>Environments Used </h2>
- <b>Cisco Packet Tracer</b> (2.2.43) <br />
- <b>Cisco 8190HGW Router</b>  <br />
- <b>Cisco 3650-24PS Multilayer Switch</b> <br />
- <b>Cisco 5506-X ASA</b> (22H2) <br />

<h2>Diagram </h2>
<img src="https://i.imgur.com/X1JOLQk.png" height="80%" width="80%" />

<h2>Walk-through:</h2>
<p align="center">
 
[Download Cisco Packet Tracer](https://skillsforall.com/resources/lab-downloads?courseLang=en-US 
)<br />

<br />
<br />
Drag and frop devices from enviornments used and as seen in the diagram. Connect devices with  either cross-over or straight-through cabling: Cross-over - Switch to switch, router to router; Straight through - PC to switch, switch to router; Console - PC to network device (for configuration)): <br/>
<img src="https://i.imgur.com/oL73dBm.png" height="80%" width="80%" />
<br />
<br />
Router basic/security, SSH and line configurations. Verfiy results on R1. Repeat process on all routers: <br/>
Router>en <br/>
Router#conf t <br/>
Router(config)#hostname R1 <br/>
R1(config)#security passwords min-length 5 <br/>
R1(config)#service password-encryption <br/>
R1(config)#login block-for 60 attempts 3 within 30 <br/>
R1(config)#enable secret PASSWORD <br/>
R1(config)#banner motd b <br/>
Enter: HELLO b <br/>
R1(config)# ip domain-name R1.COM <br/>
R1(config)# crypto key generate rsa <br/>
Enter: 1024 <br/>
R1(config)# ip ssh version 2 <br/>
R1(config)#line console 0
R1(config-line)#password PASSWORD
R1(config-line)#login
R1(config-line)#logging synchronous
R1(config-line)#exec-timeout 15 0
R1(config)#line vty 0 4
R1(config-line)#password PASSWORD
R1(config-line)#login
R1(config-line)#logging synchronous
R1(config-line)#exec-timeout 15 0
R1(config-line)# login local
R1(config)#do show running-config <br/>
<img src="https://i.imgur.com/yiOfSjt.png" height="80%" width="80%" />
<img src="https://i.imgur.com/WOn3j9G.png" height="80%" width="80%" />
<img src="https://i.imgur.com/bua1WW5.png" height="80%" width="80%" />
<br />
<br />
Import GNS3 Appliance images: See diagram for appliances and NICs: File > Import Appliance > select images "cisco-7200.gns3a", "cisco-asav.gns3a", and "cisco-iosvl2.gns3a": <br/>
<img src="https://i.imgur.com/VtmYWLI.png" height="80%" width="80%" />
<br />
<br />


