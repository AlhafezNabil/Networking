## Protocols and models.
 
1.  Network Protocol Requirements:
    * Message encoding
    * Message formatting and encapsulation
    * Message size
    * Message timing
    * Message delivery options    

    - Message Delivery Options: 
        * Unicast - Information is being transmitted to a single end device.
        * Multicast - Information is being transmitted to a one or more end devices.
        * Broadcast - Information is being transmitted to all end devices.

2.  Protocol Interaction:
3. 
    - Hypertext Transfer Protocol (HTTP) - This protocol governs the way a web server and a web client interact. HTTP defines the content and formatting of the requests and responses that are exchanged between the client and server. Both the client and the web server software implement HTTP as part of the application. HTTP relies on other protocols to govern how the messages are transported between the client and server.
    - Transmission Control Protocol (TCP) - This protocol manages the individual conversations. TCP is responsible for guaranteeing the reliable delivery of the information and managing flow control between the end devices.
    - Internet Protocol (IP) - This protocol is responsible for delivering messages from the sender to the receiver. IP is used by routers to forward the messages across multiple networks.
Ethernet - This protocol is responsible for the delivery of messages from one NIC to another NIC on the same Ethernet local area network (LAN).

4.  TCP/IP Protocol Example
    - TCP/IP protocols are available for the application, transport, and internet layers. There are no TCP/IP protocols in the network access layer. The most common network access layer LAN protocols are Ethernet and WLAN (wireless LAN) protocols. Network access layer protocols are responsible for delivering the IP packet over the physical medium.

    - The figure shows an example of the three TCP/IP protocols used to send packets between the web browser of a host and the web server. HTTP, TCP, and IP are the TCP/IP protocols used. At the network access layer, Ethernet is used in the example. However, this could also be a wireless standard such as WLAN or cellular service.


## 5.  TCP/IP Protocol Suite
  - Application Layer

    Name System

    DNS - Domain Name System. Translates domain names such as cisco.com, into IP addresses.
    Host Config

    DHCPv4 - Dynamic Host Configuration Protocol for IPv4. A DHCPv4 server dynamically assigns IPv4 addressing information to DHCPv4 clients at start-up and allows the addresses to be re-used when no longer needed.
    DHCPv6 - Dynamic Host Configuration Protocol for IPv6. DHCPv6 is similar to DHCPv4. A DHCPv6 server dynamically assigns IPv6 addressing information to DHCPv6 clients at start-up.
    SLAAC - Stateless Address Autoconfiguration. A method that allows a device to obtain its IPv6 addressing information without using a DHCPv6 server.
    Email

    SMTP - Simple Mail Transfer Protocol. Enables clients to send email to a mail server and enables servers to send email to other servers.
    POP3 - Post Office Protocol version 3. Enables clients to retrieve email from a mail server and download the email to the client's local mail application.
    IMAP - Internet Message Access Protocol. Enables clients to access email stored on a mail server as well as maintaining email on the server.
    File Transfer

    FTP - File Transfer Protocol. Sets the rules that enable a user on one host to access and transfer files to and from another host over a network. FTP is a reliable, connection-oriented, and acknowledged file delivery protocol.
    SFTP - SSH File Transfer Protocol. As an extension to Secure Shell (SSH) protocol, SFTP can be used to establish a secure file transfer session in which the file transfer is encrypted. SSH is a method for secure remote login that is typically used for accessing the command line of a device.
    TFTP - Trivial File Transfer Protocol. A simple, connectionless file transfer protocol with best-effort, unacknowledged file delivery. It uses less overhead than FTP.
    Web and Web Service

    HTTP - Hypertext Transfer Protocol. A set of rules for exchanging text, graphic images, sound, video, and other multimedia files on the World Wide Web.
    HTTPS - HTTP Secure. A secure form of HTTP that encrypts the data that is exchanged over the World Wide Web.
    REST - Representational State Transfer. A web service that uses application programming interfaces (APIs) and HTTP requests to create web applications.

  - Transport layer

    Connection-Oriented

    TCP - Transmission Control Protocol. Enables reliable communication between processes running on separate hosts and provides reliable, acknowledged transmissions that confirm successful delivery.
    Connectionless

    UDP - User Datagram Protocol. Enables a process running on one host to send packets to a process running on another host. However, UDP does not confirm successful datagram transmission.

  - Internet Layer:

    Internet Protocol
    IPv4 - Internet Protocol version 4. Receives message segments from the transport layer, packages messages into packets, and addresses packets for end-to-end delivery over a network. IPv4 uses a 32-bit address.
    IPv6 - IP version 6. Similar to IPv4 but uses a 128-bit address.
    NAT - Network Address Translation. Translates IPv4 addresses from a private network into globally unique public IPv4 addresses.
    Messaging

    ICMPv4 - Internet Control Message Protocol for IPv4. Provides feedback from a destination host to a source host about errors in packet delivery.
    ICMPv6 - ICMP for IPv6. Similar functionality to ICMPv4 but is used for IPv6 packets.
    ICMPv6 ND - ICMPv6 Neighbor Discovery. Includes four protocol messages that are used for address resolution and duplicate address detection.
    Routing Protocols

    OSPF - Open Shortest Path First. Link-state routing protocol that uses a hierarchical design based on areas. OSPF is an open standard interior routing protocol.
    EIGRP - EIGRP - Enhanced Interior Gateway Routing Protocol. An open standard routing protocol developed by Cisco that uses a composite metric based on bandwidth, delay, load and reliability.
    BGP - Border Gateway Protocol. An open standard exterior gateway routing protocol used between Internet Service Providers (ISPs). BGP is also commonly used between ISPs and their large private clients to exchange routing information.

  - Network Access Layer:
    Address Resolution
    ARP - Address Resolution Protocol. Provides dynamic address mapping between an IPv4 address and a hardware address.

    Note: You may see other documentation state that ARP operates at the Internet Layer (OSI Layer 3). However, in this course we state that ARP operates at the Network Access layer (OSI Layer 2) because it's primary purpose is the discover the MAC address of the destination. A MAC address is a Layer 2 address.

    Data Link Protocols

    Ethernet - Defines the rules for wiring and signaling standards of the network access layer.
    WLAN - Wireless Local Area Network. Defines the rules for wireless signaling across the 2.4 GHz and 5 GHz radio frequencies.

6. As shown in the figure, there are two layered models that are used to describe network operations:

  - Open System Interconnection (OSI) Reference Model
  - TCP/IP Reference Model

7. This leads to segmenting messages having two primary benefits:

Increases speed - Because a large data stream is segmented into packets, large amounts of data can be sent over the network without tying up a communications link. This allows many different conversations to be interleaved on the network called multiplexing.
Increases efficiency -If a single segment is fails to reach its destination due to a failure in the network or network congestion, only that segment needs to be retransmitted instead of resending the entire data stream.

8. Sequencing: In network communications, each segment of the message must go through a similar process to ensure that it gets to the correct destination and can be reassembled into the content of the original message, as shown in the figure. TCP is responsible for sequencing the individual segments.

9. Addresses:The network and data link layers are responsible for delivering the data from the source device to the destination device. As shown in the figure, protocols at both layers contain a source and destination address, but their addresses have different purposes:

  - Network layer source and destination addresses - Responsible for delivering the IP packet from the original source to the final destination, which may be on the same network or a remote network.
  
  - Data link layer source and destination addresses - Responsible for delivering the data link frame from one network interface card (NIC) to another NIC on the same network.
  - Layer 3 Logical Address: An IP address is the network layer, or Layer 3, logical address used to deliver the IP packet from the original source to the final destination, as shown in the figure.
      * The IP packet contains two IP addresses: Source IP address - The IP address of the sending device, which is the original source of the packet.
Destination IP address - The IP address of the receiving device, which is the final destination of the packet.

  * An IP address contains two parts:
Network portion (IPv4) or Prefix (IPv6) - The left-most part of the address that indicates the network in which the IP address is a member. All devices on the same network will have the same network portion of the address.
Host portion (IPv4) or Interface ID (IPv6) - The remaining part of the address that identifies a specific device on the network. This portion is unique for each device or interface on the network.

- Note: The subnet mask (IPv4) or prefix-length (IPv6) is used to identify the network portion of an IP address from the host portion.