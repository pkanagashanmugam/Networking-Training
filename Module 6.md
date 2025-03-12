# Module 6 - Layer 3 – Session 2

### Q1. Capture and analyze ARP packets using Wireshark. Inspect the ARP request and reply frames when your device attempts to find the router's MAC address. Discuss the importance of ARP in packet forwarding.


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
