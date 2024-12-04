# Scapy: Network Operations and Packet Crafting


<br>

### *Scapy is a powerful interactive network tool used for creating, analyzing, and manipulating network packets. It allows users to craft packets of various protocols, send them across networks, and capture responses for analysis. Scapy is commonly used for network penetration testing, network diagnosis, and troubleshooting. It supports protocols like IP, TCP, UDP, ICMP, DNS, and more.*

## Key Features of Scapy:

- Packet Crafting: Build custom packets with various protocols, headers, and payloads.
- Packet Sniffing and Analysis: Capture and inspect packets from live networks.
- Protocol Decoding: Parse and decode network traffic for analysis.
- Network Testing: Simulate network conditions like network attacks, or simply test network behavior.



## Installation
To install Scapy, use the following commands based on your package manager:

For Debian/Ubuntu:

```yml
  apt install scapy -y

  #For RHEL/CentOS:

  yum install epel-release -y
  yum install scapy -y
```
- Alternatively, Scapy can be installed via Python's pip:

```yml
  pip install scapy
```

- Scapy Interactive Shell
      - To use Scapy interactively, run the following command:

```yml
  scapy
```
  - This opens the Scapy shell where you can interactively craft and manipulate network packets.

### Example 1: Working with ICMP Packets
  *ICMP (Internet Control Message Protocol) is typically used for sending error messages and operational information about network communication, like ping requests and responses.*

#### Sending a Custom ICMP Request
  - Create an IP packet and an ICMP packet.
  - Set the source and destination IP addresses.
  - Send the crafted packet.

  *python code*
  ```yml
>>> x = IP()
>>> y = ICMP()
>>> x.show()   # Displays the properties of the IP packet
>>> y.show()   # Displays the properties of the ICMP packet

# Set source and destination IP addresses
>>> x.src = "1.1.1.1"
>>> x.dst = "8.8.8.8"

# Send the packet with a custom message
>>> send(x/y/"From_suraj")

```
  - In this example, an ICMP packet is crafted with a custom payload ("LOLOLOLOL"). Scapy will send it from IP 1.1.1.1 to 8.8.8.8.
    

*You can also send multiple packets using count or continuously using loop:*

```yml
>>> send(x/y, count=10)  # Send 10 packets
>>> send(x/y, loop=1)    # Send the packet indefinitely
```

### Example 2: Sending TCP Packets
  - You can also craft and send TCP packets. TCP is a connection-oriented protocol used for reliable data transmission.

#### Crafting a TCP Packet
- Create an IP packet and a TCP packet.
- Set source/destination IPs and ports.
- Send the packet.
```yml
>>> a = IP()
>>> b = TCP()
>>> a.src = "1.1.1.1"
>>> a.dst = "196.1.113.45"
>>> b.sport = 53    # Source port (e.g., DNS)
>>> b.dport = 80    # Destination port (e.g., HTTP)

>>> send((a/b), count=10)  # Send 10 TCP packets
```

  In this case, we send TCP packets with the source port set to 53 (DNS) and the destination port set to 80 (HTTP). This might simulate a DNS request over TCP or an HTTP connection.

## Scapy Use Cases:
1. Network Security Testing:
      - Denial of Service (DoS) attacks: Craft packets to flood a server.
    -Port Scanning: Identify open ports on a remote system by sending TCP packets to various ports.
    - Man-in-the-Middle (MITM) Attacks: Intercept and modify network traffic.

2. Network Troubleshooting:
    - Ping Testing: Use ICMP packets to check network connectivity.
    - Path MTU Discovery: Detect the largest packet size that can traverse the network.

3. Network Protocol Analysis:
    - Decode and analyze various network protocols like ARP, DNS, and HTTP.

4. Packet Sniffing:
    - Capture network traffic to inspect protocols and data being exchanged.


## Practical Assignment: Sending an HTTP Request To Your Nginx Server
This is  an example of crafting and sending a custom HTTP request over TCP to simulate a connection:

```yml
>>> a = IP()
>>> b = TCP()
>>> c = "GET / HTTP/1.1\r\nHost: www.example.com\r\n\r\n"

>>> a.src = "1.1.1.1"
>>> a.dst = "93.184.216.34"  # Example.com IP

>>> b.sport = 1025
>>> b.dport = 80

>>> send((a/b/c))  # Send HTTP GET request to web server
```
  In this case, Scapy sends a custom HTTP GET request to the server at 93.184.216.34 (example.com).

<br>
  

### Checking the Traffic with Wireshark
  - *You can capture and inspect the network packets using Wireshark. After sending packets with Scapy, you can analyze the captured traffic in Wireshark to verify that the packets are correctly crafted and received.*

#### Wireshark Steps:

- Start Wireshark and begin capturing on the appropriate network interface.
- Run the Scapy script to send packets.
- Use filters in Wireshark to isolate the packets, such as filtering by IP or TCP.
- For example, to filter packets between 1.1.1.1 and 8.8.8.8, you can use:

```yml
ip.src == 1.1.1.1 && ip.dst == 8.8.8.8
```

<br>

After sending a custom HTTP GET request using Scapy, we can capture and inspect the traffic in Wireshark as follows:

1. TCP Handshake:

    - The three-way handshake (SYN, SYN-ACK, ACK) establishes a TCP connection between your client (source IP) and the server (destination IP).

2. HTTP GET Request:

    - You will see the HTTP request packet containing the method GET / HTTP/1.1 with headers like Host: www.example.com.


3. HTTP Response:

    - The server responds with an HTTP 200 OK status and the requested content (HTML page).

4. Wireshark Filters:

    - Use filters like ip.src == 1.1.1.1 && ip.dst == 93.184.216.34 or tcp.port == 80 to isolate relevant packets.


*From this capture, we can verify the correct transmission of the HTTP request and response, along with the TCP connection process.*






<br>
<br>








### Conclusion

*Scapy is a versatile and powerful tool for crafting custom packets and testing network protocols. It’s used in security, troubleshooting, and testing scenarios. By learning Scapy, you can automate many aspects of network analysis and manipulation, making it an essential tool for network engineers, security professionals, and penetration testers.*







