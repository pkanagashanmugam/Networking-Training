# Module 1 - Communication Fundamentals
# Module 2 - Evolution of Computer Networks

### Q1. Consider a case, a folder has multiple files and how would copy it to destination machine path (Try using SCP, cp options in Linux)
The `scp` command stands for **_Secure Copy Protocol_** which is an efficient method to copy files from one host to another in a network. Using the general syntax of 
```
$ scp [options] source destination
```
We transfer a file from the kali user to hadoop user using the below command which performs the copy operation post authentication
```
scp understanding_ping.txt hadoop@kali:/home/hadoop/
```

![Screenshot (720)](https://github.com/user-attachments/assets/598a2f76-ca88-4ea3-90a1-30dc78e4e50c)

### Q2. Host a FTP and SFTP server and try PUT and GET operations.
FTP stands for _**File Transfer Protocol**_ and SFTP stands for _**Secure File Transfer Protocol**_ which is a more secure method of performing the latter command which is used to transfer file over a network in a fast and secure manner.
In order to host a FTP server in Kali Linux, the `vsftpd` package needs to be installed and configured.

**Installation and Configuration Commands:**
```
apt-get update
apt-get install vsftpd
cd /etc/
vim vsftpd.conf
->local_enable=YES
->write_enable=YES
->chroot_local_user=YES
->chroot_list_enable=YES
->chroot_list_file=/etc/vsftpd.chroot_list
touch vsftpd.chroot_list(To add list of users having access to the server)
```
![Screenshot (721)](https://github.com/user-attachments/assets/06245a98-4f80-415e-b7fc-9141da12e66c)

In this example,we have provided the **hadoop** user with access to the server.In order to start the server, the following command has to be given which starts the server post authentication
```
service vsftpd start
```
![Screenshot (724)](https://github.com/user-attachments/assets/5c48cdc5-4e90-4319-80ec-9a645231d6a5)
We can access the server using the command `ftp <ip_address>`. Server can be accessed using normal linux commands.In order to get a file from the server, `get filename` is used which saves the file from the server to the present working directory

![Screenshot (726)](https://github.com/user-attachments/assets/9516fd59-c7e8-4864-8f1d-455e4830b3d2)
![Screenshot (727)](https://github.com/user-attachments/assets/a9d92fb2-fa55-43ec-af97-f7ca111c0e47)

Alternatively, the server can also be accessed from Windows by connecting to `ftp://ip_address` from the File Explorer and files from Windows can be put into the server

![Screenshot (728)](https://github.com/user-attachments/assets/631df8c5-939b-44ac-8f45-2036dba3d5b9)
![Screenshot (729)](https://github.com/user-attachments/assets/f1acbc68-f52d-42d9-93bb-0783837f07b5)

**USING SFTP :**

The FTP server can be connected using SFTP by using the command `sftp username@ip_address`.  Files can be uploaded into the server using the command `put source destination`

![Screenshot (730)](https://github.com/user-attachments/assets/4324d8ca-5c65-4e23-bc0a-e59eb51d764a)

### Q3. Explore with Wireshark/TCP-dump/cisco packet tracer tools and learn about packets filters.
Wireshark is a packet sniffing tool which is predominantly used for networking monitoring. Since it is a GUI based tool, packets can be easily sniffed.

![Screenshot (731)](https://github.com/user-attachments/assets/566a5b73-3ab8-43e8-95be-0cfc2e019ee1)
The sniffed packets can be analyzed and filtered by using common filtering options like host,port,protocol. Like in the below example, the packets can be sniffed by using protocol name like `arp` and ip address like `ip.addr == 192.168.1.11`

![Screenshot (732)](https://github.com/user-attachments/assets/3d67bfb8-889f-4a09-8749-662ff2ee6390)
![Screenshot (733)](https://github.com/user-attachments/assets/99967c7a-be59-401f-ba1e-a2d815dabb77)

### Q4. Understand linux utility commands like - ping, arp (Understand each params from ifconfig output).
Ping is a command which is used to check network connectivity. This command can be modified using various options like -c,-q. The -c option is used to limit the packets.

![Screenshot (717)](https://github.com/user-attachments/assets/12db9327-9821-4f4f-ab29-9a9073a0f9a8)

ARP command stands for Address Resolution Protocol which is used to identify the MAC address of a host computer that is connected in the same network as the source. By sending out packets targetting the Destination IP address and flooding it over the network, the source computer gets to know the MAC address of the destination computer.

![Screenshot (718)](https://github.com/user-attachments/assets/aea86bf0-2a1a-46dd-b6ac-925f482934a3)

### Q5. Understand what happens when duplicate IPs configured in a network.
When duplicate IPs are configured in a network, it leads to a conflict scenario. This leads to connectivity issues where a packet that is intended to a specific IP will have 2 or more possible destination to send the packet to and it does not know where to send the packet to. This issue commonly arises in the cases of Static IP configuration. This scenario leads to instability in ARP tables and routing issues.
The solution to this issue is using DHCP for automatic IP configuration or simply restarting the device.

### Q6.
