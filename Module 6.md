# Module 6 - Layer 3 – Session 2

### Q1. Capture and analyze ARP packets using Wireshark. Inspect the ARP request and reply frames when your device attempts to find the router's MAC address. Discuss the importance of ARP in packet forwarding.

ARP is the protocol used by hosts to find out MAC address or the physical address of the device. The hosts in a network communicate to other hosts/ external networks using the router so knowing the MAC address of the router is essential. When the host connects to the internet, one of the primary functions it carries out after requesting for IP address (if DHCP server is enabled) is to learn the MAC address of the router. 

As it can be seen, the host machine sends an _ARP request as a broadcast message_ to the hosts in the network. The destination IP address is that of the router (192.168.1.1). 

![image](https://github.com/user-attachments/assets/e126547d-c563-4220-8c5e-e1f169158869)

When this request packet reaches the router, it learns the MAC address of the host which sent the request from the Source MAC Address field and sends back a Unicast Reply. The receiving host learns the router's MAC address using the Source MAC Address field. 

![image](https://github.com/user-attachments/assets/c84840bf-35dd-4d4d-919e-adbc5211f68f)

Thus, ARP Request is always a Broadcast Message whereas ARP Reply is an Unicast Message. ARP plays a vital role in packet forwarding. Since all the packets flow through all 7 layers of the OSI model, when the packet flows through Layer 2, the Source and Destination MAC address is added as the header to the data. ARP, which operates at LAYER 2, plays a vital role in not only allowing the hosts to learn MAC addresses without which packets cannot be sent to other devices, ARP replies allows the switch to learn the hosts that are connected to its interfaces and updates them in the MAC address table.

### Q2. Manually configure static routes on a router to direct packets to different subnets. Use the ip route command and verify connectivity using ping and traceroute.


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
