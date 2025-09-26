This project is meant to serve as a foundational primer for common tools used in the command line. I am using a VirtualBox Ubuntu virtual machine as my work environment.

1. **Identify Network Interfaces and IP Addresses**

- Command: **ifconfig**
  _ifconfig_ stands for "interface configuration." This command-line tool is used to view and configure network interfaces. It will display all network interfaces along with their associated IP addresses. The output of the command will show:
  - **inet addr**: the IP address assigned to the interface. 
  - **Netmask**: defines which portion of the IP address is the network and which is the host. Network will have “255” in the octet, while the host part will have any other number besides 0, 255 and 256.
  - **Broadcast address**: used to send data to all hosts on the network.
  - **Ether / MAC address**: physical hardware address of your network card.
  - **RX/TX packets, errors, dropped**: RX is received and TX is transmitted; shows the number of packets handled. Errors/drops may indicate network issues.
  - **MTU**: Maximum Transmission Unit. Largest size of a packet that can be transmitted\*\*
  
    ![ifconfig_VirtualBox](https://github.com/user-attachments/assets/142e0402-798f-4679-9bcb-740ecbb175f8)


2. **Check Open Ports**

- Command: **sudo netstat -tuln** or **ss -tuln**
  The _netstat_ command is a network utility that displays active network connections, ports that are open and listening, as well as various statistics on your local machine. _-tuln_ is equivalent to combining the flags -t (TCP), -u (UDP), -l (show only _listening_ sockets), -p (program; show the PID and name of the program) and -n (show _numeric_ addresses). This command is useful in helping identify unnecessary open ports that could be potential entry points for attackers.

  ![netstat_VirtualBox](https://github.com/user-attachments/assets/7ce50ad5-c45a-4e3d-8d20-97013b57eaf3)


3. **Analyze Network Connections**

- Command: **sudo lsof -i -P -n**
  This command will list all the open files and the processes that opened them. _lsof_ stands for 'list open files'. In Linux, everything is considered a file. Using this command, a user can detect any unexpected or unauthorized connections to your server. The -i flag will list all network files, along with their purposes. The -P and -n flags prevent the resolution of port numbers and IP addresses, making the output easier to read and faster to generate.
 
  ![lsof_command_VirtualBox](https://github.com/user-attachments/assets/719b420f-6d20-45bf-8bb2-382928cd73e7)


4. **Perform Network Scanning with Nmap**

- Command: **sudo nmap -sS -0 localhost**
  Nmap is short for network mapper. It is a free, open-source piece of software that is used for network scanning. At its core, Nmap is used to discover hosts and services on a computer network by sending packets and analyzing the responses. The Nmap command allows you to scan your server to identify open ports and active services. It can help you discover services that are unintentionally exposed. Nmap is extremely powerful and needs to be used with caution, as scanning private networks can be illegal.

  ![nmap VirtualBox](https://github.com/user-attachments/assets/112b829e-342e-4370-8eb9-bd6a68d36829)


5. **Check for Open Ports on the Server's Network**

- Command: **sudo nmap -sP 192.168.1.0/24**
  The Nmap command can also be used to identify all live hosts on your local network.
  
  ![nmap livehosts](https://github.com/user-attachments/assets/d44ac5a8-2629-47a1-964e-7746d010fb9c)

  ![nmap VirtualBox2](https://github.com/user-attachments/assets/43357c95-86fa-4f59-a648-f6fe173c3787)


6. **Check for Services and Versions**

- Command: **sudo nmap -sV localhost**
  This command will scan for open ports and attempt to determine the service and version running on each port. This is helpful with identifying outdated or vulnerable software. The _-sV_ option enables version detection, providing detailed information about the services running on open ports. It is also useful for detecting any malware.
  
  ![nmap localhost](https://github.com/user-attachments/assets/4f7d2756-ce33-4601-8575-be376758581b)


7. **Identify Potential Vulnerabilities**

- Command: **sudo nmap --script vuln localhost**
  This command will allow you to use Nmap scanning to identify known vulnerabilities on the server. The **--script vuln** option will run scripts that check for various vulnerabilities.
 
  ![nmap script vuln virtualbox](https://github.com/user-attachments/assets/eb10debe-6c2e-40bf-97e8-5e067122732a)


8. **Inspect Network Traffic**

- Command: **sudo tcpdump -i eth0**
  This command will monitor network traffic on a specific interface. With the above command, it will look at eth0. Real-time traffic can be observed this way, as well as suspicious activity. In order to stop the packet analysis, press ctrl+c on the keyboard.
  
  ![tcpdump](https://github.com/user-attachments/assets/56666472-9f72-4d00-bf3d-99c44ac0dda8)


9. **Monitor Network Connections in Real-Time**

- Command: **sudo watch -n 1 netstat -tulnp**
  This command will check network connections continuously. The **-n 1** option shows that this command will update every second. This command is useful to monitor real-time network activity, such as when new connections are formed or services start. To stop this process, press ctrl+c on the keyboard.
  
  ![netstat_VirtualBox2](https://github.com/user-attachments/assets/73eea35b-c7fd-4fb2-9f20-57a58a9f7d9f)


10. **Check Firewall Rules**

- Command: **sudo ufw status verbose**
  This command will display the current rules configured for the firewall on the server. It will show which ports and services are allowed or blocked. **ufw** stands for "Uncomplicated Firewall," which is a tool designed to make it easier to configure a firewall.
  
  ![virtualbox firewall](https://github.com/user-attachments/assets/8c7b2810-3254-4e2f-8cbc-c1525c83ae52)

