### What is a Computer Network?
A computer network is a collection of interconnected devices (like computers, routers, or servers) that communicate and share resources such as data, files, and internet access.

---
### Types of Computer Networks
- PAN (Personal Area Network): Very small, for one person. (e.g., connecting your phone to your Bluetooth headphones).
- LAN (Local Area Network): Covers a small area like a single building or home. (e.g., your home Wi-Fi network).
- MAN (Metropolitan Area Network): Covers a larger area, like a city or a university campus.
- Covers a very large geographical area, like a country or even the whole world. The Internet is the biggest example of a WAN.

---
### What is Network Topology?
It refers to how devices are arranged and connected in a network.
- Star Topology: All devices connect to a central hub or switch. This is the most common one used in home and office LANs today.
- Bus Topology: All devices share a single common cable. (This is an older, less common method).
- Ring Topology: Devices are connected in a circle, with data passing from one to the next.
- Mesh Topology: Every device is connected to every other device. This is highly reliable but expensive.

---
### What is Bandwidth?
It's the maximum amount of data that can be sent over a connection in a given amount of time (measured in Mbps or Gbps). More width = higher bandwidth.

---
### What is Latency?
Latency is the delay. It's the time it takes for a single piece of data to get from the start to the destination (measured in milliseconds).  

For video streaming, you need high bandwidth (a wide highway) to get all the data. For online gaming, you need low latency (a fast car) so your actions are instant
---

### What is an IP address?
An IP (Internet Protocol) address is a unique number assigned to every device on a network. It acts like a mailing address (like a house address) that tells the network exactly where to send data.
- IPv4: The older version. It uses a 32-bit address (e.g., 172.217.14.228). It can provide about 4.3 billion unique addresses, which we have now run out of.
- IPv6: The new version. It uses a 128-bit address (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334). It provides a virtually limitless number of addresses for all the new devices connecting to the internet.

---
### What is a MAC address and how is it different from an IP address?
A MAC Address (Media Access Control) is a permanent, physical address burned into the network card by the manufacturer.(Each device has a network interface card, and this card has a unique MAC address assigned during manufacturing, which is why it is permanent.). It's like the serial number of the device. It's used for communication within the same local network (LAN).   
Analogy: Your MAC address is your name (it doesn't change), while your IP address is your mailing address (it can change if you move to a new network).

---
### What is DNS and How Does It Work?
DNS (Domain Name System) translates domain names (like www.google.com) into IP addresses.  
When you type google.com into your browser, your computer (Browser understands IP addresses, not names) asks a DNS server, "What's the IP address for https://www.google.com/url?sa=E&source=gmail&q=google.com?" The DNS server looks it up and sends back the IP address, allowing your browser to connect to the right server.

---
### What is ARP (Address Resolution Protocol)
(To communicate within a local network, devices need each other’s MAC address. However, they usually share or know only the IP address.)
ARP (Address Resolution Protocol) maps an IP address to a MAC address in a local network.  
[When a device wants to send data to another device on the same network, it knows the other device's IP address but doesn't know its MAC address. ARP sends out a broadcast message to everyone on the LAN, asking, "Who has this IP address?" The device with that IP replies, "I do! Here is my MAC address." The two devices can now talk directly.]

---
### What is a subnet mask?
A subnet mask divides an IP address into network and host portions, helping identify which part of the address belongs to the network.
- Network ID: Which network the device is on.
- Host ID: Which specific device it is on that network.

---
### Explain the OSI Model and its 7 layers.
It divides the complex process of communication into 7 manageable layers. Data goes down the layers on the sending computer and up the layers on the receiving computer. 
A good mnemonic is: "Please Do Not Throw Sausage Pizza Away"
- Layer 7: Application: The layer you interact with. (e.g., your web browser, email client).
- Layer 6: Presentation: Translates, encrypts, and formats data. (e.g., HTTPS encryption, JPEG).
- Layer 5: Session: Manages the "conversation" or session between two devices.
- Layer 4: Transport: Handles reliable data delivery (using TCP) or fast, unreliable delivery (using UDP). This is where port numbers are used.
- Layer 3: Network: Handles routing and logical addressing (IP addresses). This is where routers operate.
- Layer 2: Data Link: Handles physical addressing (MAC addresses) and error-checking. This is where switches operate.
- Layer 1: Physical: The actual hardware. (e.g., cables, Wi-Fi signals, fiber optics).

---
### Explain the TCP/IP model and its layers.
The TCP/IP model is a simpler, more practical model that the internet is actually based on. It has 4 layers:
- Application: Combines the OSI Application, Presentation, and Session layers. (e.g., HTTP, DNS).
- Transport: Same as the OSI Transport layer. (e.g., TCP, UDP).
- Internet: Same as the OSI Network layer. (e.g., IP, ARP).
- Network Access: Combines the OSI Data Link and Physical layers. (e.g., Ethernet, Wi-Fi).

---
### What is the difference between circuit switching and packet switching?
Circuit Switching: A dedicated, continuous connection (a "circuit") is established before any data is sent.  
Packet Switching: Data is broken into small pieces called packets. Each packet is sent independently and can take a different route to the destination, where they are reassembled. This is how the internet works. It's incredibly efficient because many users can share the same lines at the same time.  

---
### Explain simplex, half-duplex, and full-duplex communication.
- Simplex: Communication is one-way only. (e.g., a TV broadcast or a baby monitor).
- Half-Duplex: Communication is two-way, but not at the same time. (e.g., a walkie-talkie—you have to "push to talk" and then listen).
- Full-Duplex: Communication is two-way, simultaneously. (e.g., a telephone call or a Zoom meeting).

---
### What is a 3-way handshake in TCP?
It's the process TCP (a connection-oriented protocol) uses to establish a reliable connection before sending any data. It's like a formal, 3-step greeting:
- SYN (Client): The client sends a "synchronize" message, saying, "Hi, I'd like to start a connection."
- SYN-ACK (Server): The server sends a "synchronize-acknowledge" message, replying, "Great, I'm ready. I acknowledge your request."
- ACK (Client): The client sends a final "acknowledge" message, saying, "Got it! Connection established." Now, data transfer can begin.

---
### What is a port number and why is it needed?
An IP address gets data to the right computer, but a port number gets data to the right application on that computer. A port is a 16-bit number (0-65535) that identifies a specific service or process.  
For example:
- Web traffic (HTTP) uses port 80.
- Secure web traffic (HTTPS) uses port 443.
- Email (SMTP) uses port 25.

---
### What is a socket?
A socket is one endpoint of a two-way communication link. It's the "door" that an application uses to send or receive data. A socket is identified by the combination of an IP address and a Port Number.

---
### Explain flow control and congestion control in TCP.
- Flow Control: A one-to-one problem. It prevents a fast sender from overwhelming a slow receiver. The receiver tells the sender, "I only have this much buffer space," and the sender adjusts its speed.
- Congestion Control: A network-wide problem. It prevents a sender from overwhelming the entire network (the routers and links in between). The sender detects network congestion (e.g., lost packets) and slows down its sending rate for everyone's benefit.

---
### What are HTTP and HTTPS?
- HTTP (Hypertext Transfer Protocol): The standard protocol used by web browsers to request and display web pages. It's "plaintext," meaning the data is not encrypted.
- HTTPS (HTTP Secure): The secure version of HTTP. It uses SSL/TLS encryption to protect your data. This prevents attackers from "eavesdropping" on your connection, which is why you see it on all banking and e-commerce sites.

### Difference between hub, switch, bridge, and router.
- Hub (Layer 1): A "dumb" device. It just copies any data it receives on one port and broadcasts it out to all other ports. It creates a lot of unnecessary traffic.
- Bridge (Layer 2): A "smarter" device that connects two network segments. It learns the MAC addresses on each side and only forwards data if the destination MAC is on the other side.
- Switch (Layer 2): A modern, "smart" bridge with many ports. It learns the MAC address of every device connected to it and creates a direct, one-to-one connection between the sender and receiver. This is way more efficient than a hub.
- Router (Layer 3): The "smartest" device. Its job is to connect different networks together (like your home LAN to the internet WAN). It works with IP addresses, not MAC addresses. It uses a routing table to find the best path to send data to a different network.

---
### What is a gateway?
A gateway is a device (usually a router) that acts as the exit and entry point for a network. All data going to or from the internet must pass through the gateway. It's the "door" from your local network to the outside world.

---
### What is a routing table?
A routing table is a "map" or set of rules stored inside a router. It lists all the networks the router knows about and specifies the "next hop" (which router to send the packet to next) to reach a particular destination network.

---
### What is a VPN and how does it work?
A VPN, or Virtual Private Network, creates a secure, encrypted "tunnel" between your device and a remote server, over the public internet. It works by:
- Encrypting all your internet traffic.
- Sending it to the VPN server.
- The VPN server decrypts it and sends it to the final destination (e.g., the website). This hides your real IP address and prevents your ISP or anyone on your local network from seeing what you are doing online.

---
### What is a firewall and how does it secure a network?
A firewall is a security device (hardware or software) that acts as a filter between your trusted internal network and the untrusted internet. It works by inspecting incoming and outgoing traffic and deciding whether to allow or block it based on a set of predefined security rules. It's like a bouncer at a club, checking everyone who tries to enter or leave.

---
### What is load balancing?
Load balancing is the process of distributing incoming network traffic across multiple servers. Instead of one server handling all requests (which could overload it), a "load balancer" sits in front and acts like a traffic cop, intelligently spreading the work out. This improves performance, reliability, and prevents any single server from failing.

---
### What happens when you hit a URL?/ Explain how data travels from one computer to another over the Internet.
This combines many of the concepts above. Here's the short, high-level answer:
- Browser: You type https://www.google.com and press Enter.
- DNS: Your browser asks a DNS server for the IP address of www.google.com.
- TCP: Your browser opens a TCP connection to that IP on port 443 (for HTTPS) using the 3-way handshake.
- TLS: A secure (TLS) handshake happens to encrypt the connection.
- HTTP: Your browser sends an HTTP GET request to the server, asking for the webpage.
- Server: The server (likely behind a load balancer) processes the request and sends back the website's data (HTML, CSS, etc.) in an HTTP response.
- Rendering: Your browser receives the data, renders the HTML and other files, and displays the webpage for you to see.

---



