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



### Protocols
-   Set of rules defining how to communicate
-   Each participant must use the same protocol(s)
-   Multiple protocols are used in a single communication



### OSI Model
1.  Physical - the medium on which the electrical signals are carried
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



### TCP/IP Model
1.  Physical
2.  Link - equivalent to OSI Data Link
3.  Internet - equivalent to OSI Network
4.  Transport
    -   Transmission Control Protocol (TCP)
    -   User Datagram Protocol (UDP)
5.  Application - combines the OSI Session, Presentation and Application layers



### Internet Protocol
-   Layer 3
-   Uses IP addressing (ex. 10.250.128.7)
-   Allows for routing of data between separate physical networks
-   Connectionless protocol (no confirmation of data received)
-   Data package is called a "packet"



### IP Addresses
-   Logically assigned address
-   Layer 3
-   Four 8-bit octets represented as decimal numbers
-   Must be unique on the broadcast domain



### Transmission Control Protocol
-   Layer 4
-   Uses port numbers for addressing (1 - 65535)
-   Connection oriented (acknowledges each segment)
-   Data package is called a "segment"
-   Guarantees an ordered delivery



### User Datagram Protocol
-   Layer 4
-   Uses port numbers for addressing (1 - 65535)
-   Connectionless (no acknowledgment)
-   Data package is called a "datagram"
-   Order is not guaranteed



### Domain Name Service
-   DNS
-   Works like a phonebook
-   Translates a domain name into an IP address
-   Can translate an IP address into a domain name



### Dynamic Host Configuration Protocol
-   DHCP
-   A server dynamically assigns an IP address to the host
-   The server can assign other settings as well
    -   DNS server
    -   Gateway
    -   Hostname



### ifconfig
-   Displays information about interface configuration
    -   Hardware address
    -   IP address
    -   Broadcast address
    -   Netmask
-   Allows setting of interface configuration



### Troubleshooting Networks
-   ping
-   traceroute
-   netstat
-   dig
-   host



### ping
-   Uses ICMP
-   Can be blocked
-   Reply signifies
    -   Network interface working
    -   Destination system is running
    -   Network is passing traffic between two systems



### traceroute
-   Similar to ping
-   Sends multiple ICMP requests
    -   Increasing TTL for each request
-   Attempts up to 30 hops by default



### netstat
-   List network connections
-   Display routing table
-   Display listening ports and the processes they belong to



### dig and host
-   Domain Information Groper
-   Query a DNS server for information
-   Allows querying for different types of resource records
