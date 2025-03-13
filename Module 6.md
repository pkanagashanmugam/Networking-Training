![image](https://github.com/user-attachments/assets/3fa10efe-6e72-4cd4-a987-c23888109ff5)# Module 6 - Layer 3 – Session 2

### Q1. Capture and analyze ARP packets using Wireshark. Inspect the ARP request and reply frames when your device attempts to find the router's MAC address. Discuss the importance of ARP in packet forwarding.

ARP is the protocol used by hosts to find out MAC address or the physical address of the device. The hosts in a network communicate to other hosts/ external networks using the router so knowing the MAC address of the router is essential. When the host connects to the internet, one of the primary functions it carries out after requesting for IP address (if DHCP server is enabled) is to learn the MAC address of the router. 

As it can be seen, the host machine sends an _ARP request as a broadcast message_ to the hosts in the network. The destination IP address is that of the router (192.168.1.1). 

![image](https://github.com/user-attachments/assets/e126547d-c563-4220-8c5e-e1f169158869)

When this request packet reaches the router, it learns the MAC address of the host which sent the request from the Source MAC Address field and sends back a Unicast Reply. The receiving host learns the router's MAC address using the Source MAC Address field. 

![image](https://github.com/user-attachments/assets/c84840bf-35dd-4d4d-919e-adbc5211f68f)

Thus, ARP Request is always a Broadcast Message whereas ARP Reply is an Unicast Message. ARP plays a vital role in packet forwarding. Since all the packets flow through all 7 layers of the OSI model, when the packet flows through Layer 2, the Source and Destination MAC address is added as the header to the data. ARP, which operates at LAYER 2, plays a vital role in not only allowing the hosts to learn MAC addresses without which packets cannot be sent to other devices, ARP replies allows the switch to learn the hosts that are connected to its interfaces and updates them in the MAC address table.

### Q2. Manually configure static routes on a router to direct packets to different subnets. Use the ip route command and verify connectivity using ping and traceroute.

Routing is the process of selecting a path for packets to travel between or withing network(s). There are 2 types of routing that are widely used namely Static Routing and Dynamic Routing. While static routing is performed manually explicitly forwarding packets from one network to another, dynamic routing is performed automatically without the need of the network administer to mention the routes. Static routing can be performed in simple steps but it may not be efficient in large networks having larger number of nodes. 

Two simple LAN connections are setup using PCs,Switches and Routers. Both the routers are connected together. The PCs in LAN 1 are configured with IP addresses 192.168.1.10 and 192.168.1.20 with its default gateway being 192.168.1.1 and PCs in LAN 2 are configured with IP addresses 172.168.1.10 and 172.168.1.20 with their default gateway being 172.168.1.1. 

The PCs and Routers are assigned IP addresses and routers are activated.

Static IP is configured using the following commands:
```
#Router0
ip route 172.168.1.0 255.255.255.0 200.0.0.2

#Router3
ip route 192.168.1.0 255.255.255.0 200.0.0.1
```

![Screenshot (789)](https://github.com/user-attachments/assets/5291e7c4-00d6-4a5e-bc05-a4d2763bcd97)

The connection can be verified by using `ping` and `tracert` commands.The `tracert` command shows the path taken by the packet and IP addresses are changed.

![Screenshot (788)](https://github.com/user-attachments/assets/f990370e-33aa-45d0-a3e0-b80550a3baee)


### Q3. Given a network address of 10.0.0.0/24, divide it into 4 equal subnets. Calculate the new subnet mask. Determine the valid host range for each subnet. Assign IP addresses to devices in Packet Tracer and verify connectivity.


### Q4. You are given three IP addresses: 192.168.10.5, 172.20.15.1, and 8.8.8.8. Identify the class of each IP address. Determine if it is private or public.Explain how NAT would handle a private IP when accessing the internet.

An IP address is said to be a Private IP address if it falls in any one of the below mentioned ranges:
- 10.0.0.0 - 10.255.255.255 (2^24 hosts)
- 172.16.0.0 - 172.31.255.255 (2^20 hosts)
- 192.168.0.0 - 192.168.255.255 (2^16 hosts)

Therefore the above mentioned IP address are classified as :

| IP ADDRESS | IP ADDRESS CLASS | TYPE OF IP |
| :---: | :---: | :---:|
| 192.168.10.5 | CLASS C | PRIVATE |
| 172.20.15.1 | CLASS B | PRIVATE |
| 8.8.8.8 | CLASS A | PUBLIC |

When a host tries to communicate to the internet, its address gets translated to a public IP and the reply/response from the internet is traced back to the particular host. In order to carry this out efficiently, routers use Translation Table which keeps track of the Private and Public IP addresses. 

**TYPES OF TRANSLATION TABLES :**

1. Single IP Address / Static NAT : In this case, the translation table has only two columns that is Private Address and Public Address. The router keeps track of the Private IP address when it encounters an outgoing packet updates the table. Due to the limitation of using only a single IP address, this approach may seem inefficient in private networks having number of hosts and accessing the internet at the same time.

2. Using Pool of IP Addresses / Dynamic NAT : In this case, the router maintains a pool of IP address. It may use 4/5 addresses. A similar Translation Table is maintained as mentioned above.

3. Using IP Addresses and Port Numbers / Port Address Translation : In this case, the router maintains a translation table involving **Private Address, Private Port, External Address, External Port, Transport Protocol**. A combination of Private Port and External Address is used to identify the Private Address. This method works best given that Private Port numbers are unique.
   
### Q5. In Cisco Packet Tracer, configure NAT on a router to allow internal devices (192.168.1.x) to access the internet. Test connectivity by pinging an external public IP. Capture the traffic in Wireshark and analyze the source IP before and after NAT translation.

A simple LAN network is setup having IP address in the range of 192.168.1.x. The devices are connected to a router via a switch which acts as the gateway to the internet. There are two servers available - _200.0.0.5_ and _200.0.0.10_ . Based on the choice of IP, the appropriate server is accessed. 

The router is turned on, configured for NAT by using the following commands:
```
Router>enable
Router#configure terminal
Router(config)#interface GigabitEthernet0/0
Router(config-if)#ip address 192.168.1.1 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#ip nat inside
Router(config-if)#exit

Router(config)#interface GigabitEthernet0/1
Router(config-if)#ip address 200.0.0.1 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#ip nat outside
Router(config-if)#exit

Router(config)#ip access-list standard acl1
Router(config-std-nacl)#permit 192.168.1.0 0.0.0.255
Router(config-std-nacl)#exit
Router(config)#ip nat inside source list acl1 interface GigabitEthernet0/1 overload
Router(config)#exit
```

Once the router is configured with NAT settings, we try to access the server using the IP address of the server in the web browser.

![Screenshot (790)](https://github.com/user-attachments/assets/ea9e2754-f577-41fe-bbd0-ff46be0fa0a6)

The connectivity can also be verified using `ping` command. The `tracert` command traces the route taken by the packet from the source to destination IP.

![Screenshot (791)](https://github.com/user-attachments/assets/46f13cba-ce4d-42b6-8c1c-530a2f14664d)

In Packet Tracer, the simulation mode allows us to analyze packets. Using Simple PDU option, we set the source machine as the Laptop with IP 192.168.1.5 and destination as the server with IP 200.0.0.10.

**OUTGOING PACKET AT ROUTER0 :**
The source IP address will be that of the Laptop hence the Inbound PDU details will have source IP as 192.168.1.5. Since Network Address Translation takes place at the router in order to communicate with the internet, the private IP address is changed to a public IP address. Hence the Outbound PDU Details will have the Source IP replaced to 200.0.0.1.

![Screenshot (792)](https://github.com/user-attachments/assets/77bd56b6-98fb-4158-8e72-16803373771d)

![Screenshot (793)](https://github.com/user-attachments/assets/f9944745-d9b9-4586-91a8-6263a9cf9202)

**INCOMING PACKET AT ROUTER0 :**
When the reply from the Internet reaches Router0, the public IP needs to be translated back to the private IP in order to reach the host which initiated the communication. For this process, routers maintain Translation Table (as explain above) and this translation table can be viewed by using the command `show ip nat translations` in Router's CLI. The Inbound PDU Details will have a public IP address as its Destination IP. When it comes to Router0, NAT ensures that the destination IP is changed to private IP address so that it reaches the correct host.

![Screenshot (794)](https://github.com/user-attachments/assets/fa3458f3-5364-490d-92ea-27f82069c1be)

![Screenshot (795)](https://github.com/user-attachments/assets/e8191999-713e-42ec-bbb1-1a3e6094ebb8)
