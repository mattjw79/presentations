# Connecting Linux to a Network
#### Matt Whitney



## Overview
-   [What is a Network?](#what-is-a-network)
-   [Protocols](#protocols)
-   [Domain Name Service](#domain-name-service)
-   [Dynamic Host Configuration Protocol](#dynamic-host-configuration-protocol)
-   [Troubleshooting Networks](#Troubleshooting-networks)




### What is a Network?
-   Group of two or more connected resources
-   Shares computing resources
    -   Printers
    -   Storage
    -   Applications

Notes: A network is a group of two or more connected resources. These resources
can be computers, printers, storage devices, etc. that are shared. The internet
is a network composed of other networks with shared resources.



### Protocols
-   Set of rules defining how to communicate
-   Each participant must use the same protocol(s)
-   Multiple protocols are used in a single communication

Notes: Protocols, or rules defining how to communicate, are used frequently in
computing. Each participant in the conversation must speak the same language
and the same is true for computers having a "conversation" over the network,
they must all speak with the same protocols. In each communication in the
computing world, there are multiple protocols in use, similar to when humans
have a conversation over a phone.



### OSI Model
1.  Physical - the medium on which the signals are carried
2.  Data Link (MAC/LLC)
    -   defines how to talk with the physical layer
    -   does error checking of transmitted data
3.  Network
    -   Addressing
    -   Routing
    -   Traffic control
4.  Transport - Reliable transmission of data segments
5.  Session - Establishes and maintains connections
6.  Presentation - Ensures information is formatted correctly for the application
7.  Application - Responsible for communicating with applications (APIs)

Notes: The OSI Model is a reference model for network communications and most
network protocols are derived from this model. The Physical layer is the medium
on which the signals are carried, such as copper wire, fiber optics or
radio waves. The Data Link layer, layer 2, is broken down into two sub layers,
the Media Access Control (MAC) and Logical Link Control (LLC) and controls how
devices access the network medium as well as providing error checking. The
third layer, Network, provides logical addressing and routing allowing the
data to be transferred between physically separate networks. The Transport
layer provides reliability and error control. The Session, Presentation and
Application layers provide connections, checkpointing, formatting and APIs.



### TCP/IP Model
1.  Physical
2.  Link - equivalent to OSI Data Link
3.  Internet - equivalent to OSI Network
4.  Transport
    -   Transmission Control Protocol (TCP)
    -   User Datagram Protocol (UDP)
5.  Application - combines the OSI Session, Presentation and Application layers

Notes: The TCP/IP Model differs from the OSI Model in the fact that it uses only
five layers rather than seven. However, the TCP/IP layers map closely to the
OSI layers with the TCP/IP Application layer mapping to layers five through
seven of the OSI Model.



### Internet Protocol
-   Layer 3
-   Uses IP addressing (ex. 10.250.128.7)
-   Allows for routing of data between separate physical networks
-   Connectionless protocol (no confirmation of data received)
-   Data package is called a "packet"

Notes: Layer three of the TCP/IP Model is the Internet Protocol. This provides
a logical addressing scheme and allows routing of traffic so that data can be
passed between physically separate networks. The addresses are known as IP
addresses and are usually shown in a decimal format with four octets separated
by periods. Layer three does not provide any confirmation that data was received
and is therefore a connectionless protocol.



### IP Addresses
-   Logically assigned address
-   Layer 3
-   Four 8-bit octets represented as decimal numbers
-   Must be unique on the subnet

Notes: IP addresses are a logically assigned address for layer three of the
TCP/IP Model. These address are usually displayed as four decimal numbers
separated by periods. The decimal numbers each represent an 8-bit binary number
and each machine within a subnet (logical devision of address space) must have
unique addresses.



### Transmission Control Protocol
-   Layer 4
-   Uses port numbers for addressing (1 - 65,535)
-   Connection oriented (acknowledges each segment)
-   Data package is called a "segment"
-   Guarantees an ordered delivery

Notes: The Transmission Control Protocol at layer four sits on top of the
Internet Protocol and provides a connection oriented session. Connection
oriented sessions guarantee the delivery of each piece of data by returning a
confirmation to the sender. In addition to the delivery guarantee, TCP also
guarantees an ordered delivery of the data. Each service that communicates
using TCP is assigned a port number, ranging from one to 65,535. Well-known
port numbers are in the range one - 1024 and are usually used for server
services.



### User Datagram Protocol
-   Layer 4
-   Uses port numbers for addressing (1 - 65535)
-   Connectionless (no acknowledgment)
-   Data package is called a "datagram"
-   Order is not guaranteed

Notes: The User Datagram Protocol is similar to TCP in the fact that it is also
a layer 4 and that it uses port numbers for each service. After that, the
similarities pretty much end. UDP is a connectionless protocol, which means
that when data is sent, the sender does not wait for acknowledgments before
sending more data. The order of data, when it is received, is also not checked
and therefore the data may arrive at the destination in a different order than
it was received.



### Domain Name Service
-   DNS
-   Works like a phonebook
-   Translates a domain name into an IP address
-   Can translate an IP address into a domain name

Notes: The Domain Name Service is a name translation service that works
similar to a phonebook for IP addresses. The most common use for a DNS system
is to lookup the IP address for a domain name. This is what the computer does
each time you type in www.google.com into your web browser. Using the domain
name to lookup an IP address is what is called a forward lookup. Reverse lookups
are allowed as well so that you can get a machine name from an IP address.
Forward and reverse lookups are not the only thing DNS does, less common
examples are mail exchange (MX) lookups, text (TXT) records, start of authority
(SOA) records, etc.



### Dynamic Host Configuration Protocol
-   DHCP
-   A server dynamically assigns an IP address to the host
-   The server can assign other settings as well
    -   DNS server
    -   Gateway
    -   Hostname

Notes: Dynamic Host Configuration Protocol is exactly what it sounds like. It
is a protocol that will dynamically configure the network settings, including
IP address, subnet, gateway, DNS resolution, and more. This happens when a
computer connects to the network, a request is broadcast over the network
medium and a server responds with the information that is needed to configure
the network.



### Troubleshooting Networks
-   ifconfig
-   ping
-   traceroute
-   netstat
-   dig
-   host

Notes: There are many utilities on a Linux system that can help with
troubleshooting network issues. The most commonly used tools are ifconfig, ping,
traceroute, netstat, dig and host.



### ifconfig
-   Displays information about interface configuration
    -   Hardware address
    -   IP address
    -   Broadcast address
    -   Netmask
-   Allows setting of interface configuration

Notes: The first on the list of troubleshooting tools is ifconfig. This command
is used for both viewing and setting network interface configurations. When run
without any arguments, it's default behavior is to print out the configuration
and statistics of any active interfaces. The statistics will show information
about how much data has been sent or received and the number of errors that have
occurred.



### ping
-   Uses ICMP
-   Can be blocked
-   Reply signifies
    -   Network interface working
    -   Destination system is running
    -   Network is passing traffic between two systems

Notes: The ping command acts similar to a sonar system. It uses the ICMP
protocol to send out a signal and then listens for a response. When ping
receives a response it shows that your network interface is working, the
network between the two machines is functioning, and the remote system is up
and connected to the network. However, if ping does not receive a response,
this does not mean there is a configuration or network problem. Many systems
block communications from ping.



### traceroute
-   Similar to ping
-   Sends multiple ICMP requests
    -   Increasing TTL for each request
-   Attempts up to 30 hops by default

Notes: Traceroute uses the same protocol as the ping command. The difference
with traceroute is that it will send out many signals, each with an increasing
number of hops that it will traverse (called a TTL). This way, each device
between the source computer and the destination computer will respond in turn,
effectively tracing the route a connection takes.



### netstat
-   List network connections
-   Display routing table
-   Display listening ports and the processes they belong to

Notes: The netstat command shows network connections, routes and interface
statistics. When using the netstat tool it will attempt to do a name lookup for
IP address, ports and user names. To turn off this feature, use the "-n" option.



### dig and host
-   Domain Information Groper (dig)
-   Query a DNS server for information
-   Allows querying for different types of resource records

Notes: The dig and host utilities work with a DNS server to resolve names to
IP addresses. Both utilities can do both a forward and reverse DNS lookups but
the dig command can query for different types of records such as SOA or MX
records.
