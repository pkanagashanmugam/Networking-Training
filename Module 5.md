# Module 5 - Layer 3 – Session 1
### Q1. Capture and analyze ARP packets using Wireshark. Inspect the ARP request and reply frames, and discuss the role of the sender's IP and MAC address in these packets.

ARP stands for Address Resolution Protocol whose primary function is to retrieve MAC address of a device given its IP address. So a ARP request is sent through the network having destination MAC address set to 00:00:00:00:00:00.

![image](https://github.com/user-attachments/assets/004b6977-0b58-4e33-b88a-6f573adcb887)

When the host having the specified MAC address receives the request, it responds to the request. The host which initiated the ARP request learns the desired host's MAC address by analyzing the Source MAC address field in the reply packet.

![image](https://github.com/user-attachments/assets/f928082e-71df-4eeb-aa72-8ba2f40a809a)

### Q2. Using Packet Tracer, simulate an ARP spoofing attack. Analyze the behavior of devices on the network when they receive a malicious ARP response.

ARP spoofing refers to the attack where a malicious host sends falsified ARP. This can be simulated using Packet Tracer by setting up a simple LAN network consisting of 4 End devices (having IP address in the range of 192.168.1.2 - 192.168.1.5) connected to a switch which is in turn connected to a router(IP : 192.168.1.1). 

ARP spoofing can be carried out by modifying the MAC address of the router which communicates to other networks with the MAC address of the host performing ARP spoofing. Below is the MAC address of the all devices connected in the network before it is spoofed.

![Screenshot (770)](https://github.com/user-attachments/assets/9794e825-c409-442d-b384-dc63b7bc0d4f)

Now the MAC address of the router is replaced a duplicate MAC address. The mac address table of all devices post spoofing is.

![Screenshot (771)](https://github.com/user-attachments/assets/4bea71a5-c234-42b5-8a07-12f3af6a83ed)

This creates a problem since any message/packet(s) intended to the router can be sniffed by the host with the same MAC address of the router.

![image](https://github.com/user-attachments/assets/f93b50a4-e123-41da-b352-9f2e90e867ee)

### Q3. Manually configure static IPs on the client devices(like Pc or your mobile phone) and verify connectivity using ping.

IP address on a client device can be configured in two ways either statically or using DHCP. Below is configuration of a Mobile Phone manually.

**Before Configuration :**

![WhatsApp Image 2025-03-09 at 14 25 14](https://github.com/user-attachments/assets/60491091-a15f-45a1-9813-fd40fe668174)

**After Configuration :**

![WhatsApp Image 2025-03-09 at 14 25 13](https://github.com/user-attachments/assets/32dd6453-f6c4-484c-8d5d-e400685e28e9)

**Verifying Connectivity:**

![Screenshot (769)](https://github.com/user-attachments/assets/37789fe6-4fa8-4564-b8da-209b3a9275d1)

### Q4. Use Wireshark to capture DHCP Discover, Offer, Request, and Acknowledge messages and explain the process.
DHCP follows an approach called DORA - Discover, Offer, Request and Acknowledge. Analysing the wireshark packet capture will give more details about the mentioned processes.

**DISCOVER :** This is a broadcast message sent from the client device to find the DHCP server. As it can be seen, the source IP address is not yet assigned (0.0.0.0) and the destination IP is broadcast address(255.255.255.0)

![image](https://github.com/user-attachments/assets/06db414c-9d23-4bb4-b7fa-5b3f429d95fb)

**OFFER :** In this process, the DHCP server offers an IP address to the client device.

![image](https://github.com/user-attachments/assets/bde7f352-af0d-440b-9c3b-94c9edebaf0e)

**REQUEST :** Out of the given IP address options, the client requests for an IP address to the server. The IP of the device is not yet assigned as it can be seen in the source IP address which still remains as 0.0.0.0

![image](https://github.com/user-attachments/assets/2ed3a2bb-445b-4843-a0d4-76d5987f2c7d)

**ACKNOWLEDGE :** The server offers the client with the IP address and presents some additional details such as **_Lease Time, Renewal Time and Rebinding Time_**.

![image](https://github.com/user-attachments/assets/ea67e6bd-6ac8-40dc-b181-739799525f29)

### Q5. Given an IP address range of 192.168.1.0/24, divide the network into 4 subnets. Task: Manually calculate the new subnet mask and the range of valid IP addresses for each subnet. Assign IP addresses from these subnets to devices in Cisco Packet Tracer and verify connectivity using ping between them.

**Given IP address range :** 192.168.1.0/24. In the given IP address range, the host is identified by the last 8 bits of the IP address. 

The given questions asks us to divide the network into 4 subnets. Therefore, additional 2 bits (since 2^2 =4). Therefore the IP addresses network involving subnets will be represented by **192.168.1.0/26**. Which leaves the hosts to be identified using 5 bits. There 2^5=32 hosts are possible out of which first and last IP addresses are reserved for Network Address and Broadcast Address respectively.

**VALID IP ADDRESSES FOR EACH SUBNET :**

| Subnet      | Network Address | Usable IP Range     | 
| :---:        |    :----:   |          :---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text        | And more      |

| Subnet |	Network Address	| Usable IP Range	| Broadcast Address |
| :---:        |    :----:   |          :---: | :---: |
|Subnet 1	192.168.1.0/26	192.168.1.1 – 192.168.1.62	192.168.1.63
|Subnet 2	192.168.1.64/26	192.168.1.65 – 192.168.1.126	192.168.1.127
|Subnet 3	192.168.1.128/26	192.168.1.129 – 192.168.1.190	192.168.1.191
|Subnet 4	192.168.1.192/26	192.168.1.193 – 192.168.1.254	192.168.1.255
