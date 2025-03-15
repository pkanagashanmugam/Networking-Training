# Module 7 - Layer 3 - Session 3
# Module 8 - Layer 4

### Q1. Try Test-Connection and nslookup commands for below websites:
`nslookup` is a command used to query DNS servers to obtain information about the mapping between IP addresses and Domain names. 
- **www.google.com :**
Using the nslookup command we get the IP address as **142.250.194.164** and connectivity is verified using `ping` command as well as manually typing the IP address in the URL tab of the browser.

![image](https://github.com/user-attachments/assets/fef97dc9-ab0e-4294-a9cc-a84f68d7e588)

- **www.facebook.com :** IP address : **31.13.79.35**.

![image](https://github.com/user-attachments/assets/2453e9e4-0feb-4163-9552-35759c2b881f)

- **www.amazon.com :** IP address : **52.84.241.156**.
  
![image](https://github.com/user-attachments/assets/2b46e118-9f73-43f7-b5e1-0c7e7b1dbc12)

- **www.github.com :** IP address : **20.207.73.82**.

![image](https://github.com/user-attachments/assets/ebd9f0bf-da85-4e06-beec-3c3e8042918a)

- **www.cisco.com :** IP address : **23.10.232.78**.

![image](https://github.com/user-attachments/assets/cc5d33db-1419-4964-8e0d-8c6570b53630)

### Q2. Use Wireshark to capture and analyze DNS, TCP, UDP traffic and packet header, packet flow, options and flags.

### Q3. Explore traceroute/tracert for different websites eg:google.com and analyse the parameters in the output and explore different options for traceroute command.

### Q4. Set up trunk ports between switches and try ping between different VLANs.
VLAN in Cisco Packet Tracer can be setup by configuring the ports of a switch and logically grouping them into a VLAN. Configuration steps of the switch are given below.Similar configuration steps are carried out to all the switches involved in the network.

```
Switch>en
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#vlan 2
Switch(config-vlan)#name VLAN2
Switch(config)#vlan 3
Switch(config-vlan)#name VLAN3
Switch(config)#vlan 4
Switch(config-vlan)#name VLAN4
Switch(config)#int FastEthernet0/3
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 2
Switch(config)#int FastEthernet0/2
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 3
Switch(config)#int FastEthernet0/1
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 4
Switch(config)#int GigabitEthernet0/1
Switch(config-if)#switchport mode trunk
Switch(config-if)#switchport trunk allow vlan add 2
Switch(config-if)#switchport trunk allow vlan add 3
Switch(config-if)#switchport trunk allow vlan add 4
```

![image](https://github.com/user-attachments/assets/d065b644-f73f-47ad-a798-104d11649630)

Connectivity is verified by pinging the PCs in same VLAN. If we try to ping the PCs connected in the same LAN but different VLAN, ping fails since the ports of the switches are configured to handle VLAN traffic.

![image](https://github.com/user-attachments/assets/76962161-6ae3-4887-a67b-b6b3deb0a68b)


### Q5. Change the native VLAN on a trunk port. Test for VLAN mismatches and troubleshoot.
The Native VLAN on a trunk port is VLAN 1 by default. By changing the Native VLAN of trunk port in Switch 0 of the above configuration, we get a VLAN mismatch when we try to ping PCs in a VLAN.The native VLAN can be changed by using the following commands:
```
Switch>enable
Switch#conf t
Switch(config)#int GigabitEthernet0/1
Switch(config-if)#switchport trunk native vlan 99
```
When we try to execute the  `ping` command, we can see the VLAN mismatch error in CLI of the switch.
![image](https://github.com/user-attachments/assets/6dfebb53-91cf-450a-8970-bcac785063a4)

**TROUBLESHOOTING :**

In order to rectify this, we need to bring uniformity in Native VLANs of the trunk port. Since we had changed the Native VLAN to 99 in one of the switches, configuring the same VLAN in other switch will resolve this issue. Performing the same set of commands as mentioned above on Switch 2 and executing the `ping` command, we get:

![image](https://github.com/user-attachments/assets/f371b292-e246-4c58-84d8-0d10d630ba7d)

### Q6. Configure a management VLAN and assign an IP address for remote access. Test SSH or Telnet access to the switch.

### Q7. You have a Cisco switch and a VoIP phone that needs to be placed in a voice VLAN (VLAN 20). The data for the PC should remain in a separate VLAN (VLAN 10). Configure the switch port to support both voice and data traffic.
Firstly, 2 VLANs namely DATA(VLAN 10) and VOICE(VLAN 20) are created on the switch by using the following commands:
```
Switch>en
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#vlan 10
Switch(config-vlan)#name DATA
Switch(config-vlan)#ex
Switch(config)#vlan 20
Switch(config-vlan)#name VOICE
Switch(config-vlan)#ex
```
Then switch is then configured to allow access to connected interfaces to the VLANs using the following commands:
```
Switch(config)#int fastEthernet0/1
Switch(config-if)#switchport access vlan 10
Switch(config-if)#switchport voice vlan 20
Switch(config-if)#ex
Switch(config)#int fastEthernet0/2
Switch(config-if)#switchport access vlan 10
```
Therefore the devices connected in the networked are configured appropriately with their VLANs (either Voice or Data).
![image](https://github.com/user-attachments/assets/123d76a6-5051-4853-9e32-7bcdfcfe969c)
PCs in Data VLAN can check their connectivity using the ping command. Since they are connected to the same VLAN, the packets reach the destination PC.
![image](https://github.com/user-attachments/assets/8eece643-9169-4cbe-9c64-c69552885d18)


### Q8. You configured VLANs 10 and 20 on your switch and assigned ports to each VLAN. However, devices in VLAN 10 cannot communicate with devices in VLAN 20. Troubleshoot the issue.
A simple LAN setup is simulated and 2 VLANs 10 and 20 are configured on the switch using the VLAN setup commands. Three PCs are configured to each of the VLANs. When a PC pings another PC in the same VLAN, the ping commands completes its execution successfully. However, when a PC in VLAN 10 tries to communicate with a PC in VLAN 20, the ping command fails as the PCs configured in a VLAN will have access to the PCs connected to the PCs connected in the same VLAN i.e Intra VLAN communication is only possible. However Inter VLAN communication can be made possible by using a Router connecting to the switch's Trunk Port thereby facilitating Inter VLAN routing.

![image](https://github.com/user-attachments/assets/689e8fab-9d82-4f1e-a634-0f1fd0df09f8)


### Q9. Try Inter VLAN routing with Router.
A router is added to the network by connecting to the switch using GigabitEthernet interface. The router is configured to perform Inter VLAN routing using the following configuration commands:
```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface GigabitEthernet0/0
Router(config-if)#no shutdown
Router(config-if)#ex
Router(config)#interface GigabitEthernet0/0.10
Router(config-subif)#encapsulation dot1q 10
Router(config-subif)#ip address 192.168.1.1 255.255.255.0
Router(config-subif)#ex
Router(config)#interface GigabitEthernet0/0.20
Router(config-subif)#encapsulation dot1q 20
Router(config-subif)#ip address 192.168.2.1 255.255.255.0
Router(config-subif)#ex
Router(config)#ex
```
Router is connected to the trunk port of the switch. Thus the access of interface connecting the switch and router should be changed to trunk.
```
Switch>en
Switch#conf t
Switch(config)#int gigabitEthernet0/1
Switch(config-if)#switchport mode trunk
Switch(config-if)#ex
```
Communication takes place by finding out the MAC address of the destination PC which will not be available in the MAC address table of the switch. So the router broadcasts the ARP request to other VLAN and forwards the reply to the source PC. Then the 2 PCs with the help of router, communicate with each other.
![image](https://github.com/user-attachments/assets/72714c7a-92cf-4b80-a598-2e416a2ddf9d)

### Q10. Implement ACLs to restrict traffic based on source and destination ports. Test rules by simulating legitimate and unauthorized traffic.
We can block traffic in a network by implementing restrictions on source and destination ports. There are come well known ports like 80 for HTTP,22 for SSH and many more. We can restrict the traffic by configuring the router by executing the following commands:
```
Router(config)#ip access-list extended VLAN-ACCESS
Router(config-ext-nacl)#permit tcp 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255 eq 80
Router(config-ext-nacl)#permit tcp 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255 eq 22
Router(config-ext-nacl)#deny ip 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255
Router(config-ext-nacl)#deny ip 192.168.2.0 0.0.0.255 192.168.1.0 0.0.0.255
Router(config-ext-nacl)#ex
Router(config)#interface GigabitEthernet0/0.10
Router(config-subif)#ip access-group VLAN-ACCESS in
Router(config-subif)#ex
Router(config)#interface GigabitEthernet0/0.20
Router(config-subif)#ip access-group VLAN-ACCESS in
Router(config-subif)#ex
```
A Access Control List is created which permits only tcp traffic pertaining to ports 80 and 22 and denies all other ip traffic. The ACL can be verified by using the command `show access-lists` and when we try to ping the PC in two different VLANs, we get Destination Host Unreachable. When the command `show access-lists VLAN-ACCESS`, we find that the denying ip to 192.168.2.0 network has 50 matches.

![image](https://github.com/user-attachments/assets/12c30726-9bc8-44ce-a6db-a23104f6468f)

### Q11. Configure a standard Access Control List (ACL) on a router to permit traffic from a specific IP range. Test connectivity to verify the ACL is working as intended.
Access Control Lists can be configured to allow traffic from a specific IP range. By using combination of IP address and wildcard masks, IP can be blocked. 
```
Router(config)#access-list 10 permit 192.168.1.0 0.0.0.255
Router(config)#access-list 10 deny any
Router(config)#int GigabitEthernet0/0.20
Router(config-subif)#ip access-group 10 in
Router(config-subif)#ex
Router(config)#int GigabitEthernet0/0.10
Router(config-subif)#ip access-group 10 in
Router(config-subif)#ex
```
When we try to ping a PC from VLAN2, the request times out whereas when we try to ping a PC from the same VLAN it completes successfully.
![image](https://github.com/user-attachments/assets/0b942e7f-6a81-4b43-9fda-4ac8738e4bf3)

### Q12. Create an extended ACL to block specific applications, such as HTTP or FTP traffic. Test the ACL rules by attempting to access blocked services.
An extended ACL is created to block specific applications like HTTP and FTP using their port numbers and any other ip connection is allowed. In order to verify this Access List, we try to communicate with the host 192.168.2.5 using telnet and a connection refused message returns. If we try to communicate with the same host using ping, execution is successful thus ACL blocks the services successfully.
![image](https://github.com/user-attachments/assets/c5e0b656-2bf7-4439-80c7-9de44e1e6abc)


### Q13. Try Static NAT, Dynamic NAT and PAT to translate IPs.

### Q14. Download iperf in laptop/phone and make sure they are in same network. Try different iperf commands with tcp, udp, birectional, reverse, multicast, parallel options and analyze the bandwidth and rate of transmission, delay, jitter etc.
