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
