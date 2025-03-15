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

### Q6. Configure a management VLAN and assign an IP address for remote access. Test SSH or Telnet access to the switch.

### Q7. You have a Cisco switch and a VoIP phone that needs to be placed in a voice VLAN (VLAN 20). The data for the PC should remain in a separate VLAN (VLAN 10). Configure the switch port to support both voice and data traffic.

### Q8. You configured VLANs 10 and 20 on your switch and assigned ports to each VLAN. However, devices in VLAN 10 cannot communicate with devices in VLAN 20. Troubleshoot the issue.

### Q9. Try Inter VLAN routing with Router.

### Q10. Implement ACLs to restrict traffic based on source and destination ports. Test rules by simulating legitimate and unauthorized traffic.

### Q11. Configure a standard Access Control List (ACL) on a router to permit traffic from a specific IP range. Test connectivity to verify the ACL is working as intended.

### Q12. Create an extended ACL to block specific applications, such as HTTP or FTP traffic. Test the ACL rules by attempting to access blocked services.

### Q13. Try Static NAT, Dynamic NAT and PAT to translate IPs.

### Q14. Download iperf in laptop/phone and make sure they are in same network. Try different iperf commands with tcp, udp, birectional, reverse, multicast, parallel options and analyze the bandwidth and rate of transmission, delay, jitter etc.
