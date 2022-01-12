# OSI model

## Introduction

> The Open Systems Interconnection model (OSI model) is a conceptual model that characterises and standardises the communication functions of a telecommunication or computing system without regard to its underlying internal structure and technology. Its goal is the interoperability of diverse communication systems with standard communication protocols. ([Wikipedia](https://en.wikipedia.org/wiki/OSI_model))

Simply put, the OSI model is a model used to have a better understanding of how different protocols interact with each other when two or more systems communicate. 

Each protocol involved in the communication of two or more systems can be classified in one or more of the 7 layers of the OSI model.

| Layer  | Layer name       | Protocol Data Unit (PDU)  | Description (from Wikipedia.org) |
| ------ | ---------------- | ------------------------- | -------------------------------- |
| 7      | Application      | Data                      | High-level APIs, including resource sharing, remote file access     |
| 6      | Presentation     | Data                      | Translation of data between a networking service and an application; including character encoding, data compression and encryption/decryption |
| 5      | Session          | Data                      | Managing communication sessions, i.e., continuous exchange of information in the form of multiple back-and-forth transmissions between two nodes |
| 4      | Transport        | Segment (or Datagram)     | Reliable transmission of data segments between points on a network, including segmentation, acknowledgement and multiplexing |
| 3      | Network          | Packet                    | Structuring and managing a multi-node  network, including addressing, routing and traffic control |
| 2      | Data link        | Frame                     | Reliable transmission of data frames between two nodes connected by a physical layer |
| 1      | Physical         | Bit (or Symbol)           | Transmission and reception of raw bit streams over a physical medium |

## 7 - Application Layer

The Application Layer is the top layer of the OSI model. Layer 7 protocols only define the information it needs to send accross the network, not how it will send it.

For example, as per the HTTP protocol, the client sends a `GET` payload through the network to the server. In return, the server responds with a code to let the client know if the request was successful (`200`). The HTTP protocol does not specify how or on which channel the client must communicate to reach the server.

Other examples include SMTP, SSH, FTP, LDAP, DNS, SSH, ...etc.

## 6 - Presentation Layer

The Presentation Layer protocols deal with the syntax of the message sent by the application layer. Its role is to specify and convert the format of the data sent so the other computer can understand it (if compatible). This is the layer used to encrypt/decrypt, compress/decompress, encode/decode the message.

For example, if the computer receives `aGV5`, the presentation layer should contain the information necessary about what the string represents and decode it so the Application Layer understands it (here, `hey` in `base64` encoding).

It should be noted that a lot of Layer 7 protocols make the Presentation Layer redundant, which explains why most "pure" Layer 6 protocols are unheard of. Known Layer 6 protocols could include SSL and/or TLS.

## 5 - Session Layer

> The purpose of the Session Layer is to provide the means necessary for cooperating presentation-entities to organize and to synchronize their dialogue and to manage their data exchange. 
> 
> (ISO/IEC 7498-1)

This layer could also be used to manage access tokens or transaction, for example.

Common Layer 5 protocols could include SMB, NetBIOS or SMPP.

## 4 - Transport Layer

The Transport Layer protocols deal with how a reliable and efficient connexions can be made through a network. While the work of "finding" the right system in the network is made by the Network Layer, it is the role of the Transport Layer to make sure the data has been received and to take action if it was not. Another role of the Transport Layer is to provide a way to differentiate traffic coming in and out of the same host.

Taking logistics as an example, whatever the means (trucks, planes, boats) used to transport the goods (Layer 3) it is the logistics department's responsibility to take action if the goods arrive damaged or don't arrive at all. It is also its responsibility to label outgoing packages so they can be clearly identified later.

The most well known Transport Layer protocols are TCP and UDP, which use port numbers to differentiate traffic.

## 3 - Network Layer

> The basic service of the Network Layer is to provide the transparent transfer of data between transport-entities. This service allows the structure and detailed content of submitted data to be determined exclusively by layers above the Network Layer.
>
> (ISO/IEC 7498-1)

Basically, this layer handles the way data is transported from point A to point B. The most popular protocol to transport a packet is the IPv4 protocol, which uses 32 bits addresses to route traffic to the correct destination.

Other layer 3 protocols include IPv6 and ARP.

## 2 - Data link Layer

The Data Link Layer regroups multiple protocols and usage. Layer 2 is the first layer from the bottom up to organize information (i.e. frames) and to define how information should be distributed among a small group of systems (Token Ring, Wifi).

For example, it could define what happens when a 10BASE-T cable is used to connect a computer and a switch.

Common Layer 2 protocols include ATM, CDP, Ethernet, IEEE 802.11 (Wifi), LACP (Link Aggregation Control Protocol), MAC, STP, VTP, VLAN (802.1Q), ...

## 1 - Physical Layer

The Physical Layer deals with how a medium (a cable, radio waves, ...) can transport information.

Well known "protocols" (more like standards) include USB 2.0, 1000BASE-T, DSL, ...etc.




