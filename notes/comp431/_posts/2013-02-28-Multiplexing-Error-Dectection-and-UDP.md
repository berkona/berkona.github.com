---
title: Transport Layer: Multiplexing Error Detection and UDP
date: February 28 2013 11:02
layout: note
---

- Executes only on the end systems.
- Transport vs. Network:
	- Transport layer is data transfer between processes
	- Network layer is data transfer between machines
- TCP: reliable, in-order, unicast
- UDP: unreliable, unordered ('best-effort'), unicast & multicast
	- Provides minimal error detection
- Unicast: 1 to 1 connection
- Multicast: 1 to many connection, selected segment of multiple recipients
	- Live streaming audio, video, similar to broadcast delivery
- Anycast: 1 to many connection, doesn't matter if all of them get it, but any one of the them should it
	- Service that is provided identically on many different servers

# Services not provided #
- Performance
- non-unicast delivery models

# Multiplexing #
- Each end-system has a single protocol 'stack'
	- Stack is shared between all applications
- Multiplexing allows multiple applications to use network simultaneously
- De-multiplexing delivers received data to appropriate application
- Based on IP addresses and sender and receiver port #s
	- Source and destination port # carried in each segment
- De-multiplexing is helped by:
	- IP address identifies the receiving machine
	- Port # identifies the receiving process
- De-multiplexing action depends on connection or connection-less.
- UDP de-multiplexes segments to the socket
	- Uses a 2-tuple: ( destIP, destPort# )
	- Socket is 'owned' by some process allocated by the OS
- TCP de-multiplexes segments to a connection

# UDP Delivery #
- best-effort delivery
- Goal: provide error detection & multiplexing but no delivery guarantees
- Characteristics of network layer determine reliability of data delivery
- 'Bare bones' transport protocol
- Segments may be lost, delivered out of order or multiple times
- No handshake between UDP sender and receiver
- Each UDP segment is handled independently of others

# Why UDP? #
- Often used for streaming multimedia applications
- Loss-tolerant applications
- Rate-sensitive applications
- Periodic or redundant data
- DNS: small messages doesn't need heavy-duty setup
- SNMP: used by systems administrators to manage the network
- Routing protocols: exchange information about link state of nodes in network

# Checksum computation #
- UDP checksum allows receiver to detect errors in transmitted segment
- Errors are 'flipped' bits
- Sender treats contents as a sequence of 16 bit ints
- Sum the segment's contents and place the 1's complement of the sum into checksum field.

# Reliability #
- Goal: provide a reliable underlying channel
- Characteristics of underlying channel determines complexity of reliable communications
- Issues: State is required at sender & receiver and number of control messages exchanged