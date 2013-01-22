---
layout: note
title: Jan 22, 2012 Network Switching
---

## Message Switching ##
- How fast can you transmit a 7.5Mb message over a network w/ 1.5 Mbps links
	- Each hop: you must read entire message, checksum message and then read headers and send to next switch
	- 3 hops = 15 second transmission time
- Interactive experiences are delayed
- Lossy network leads to very long delays
- `T = ((dataSize / bandwidth) * timeBetweenHops * hops)`

## Packet Switching (Store and Forward) ##
- How fast?
- 7.5 Mb = 5,000 packets of 1,500 bits
- Each packet travels to between switches in ~2 ms
- Each router can send packets faster, b/c it doesn't have to read an entire file
- `T = (packets * (packetSize / bandwidth)) * (timeBetweenHops * hops)`
- 3 hops = 4 ms, so 5,000 packets = 5 s
- ~ 3 times faster than message switching on average
- However: packets must hold sequence numbers to ensure correct ordering

## Forwarding ##
- The process of moving packets among routes from a source to a destination
- There are various approaches
- Datagram networks must look up address each forward
- Virtual circuits determine hops only once
- Delayed expense vs. Long call setup

### Datagram Network: ###
- Each packet carries a destination address
- Destination address used to look up next hop
- Route (next hop) may change at any time

#### How it works ####
- Packets contain a complete destination address: a network & host
- Router examines destination address
- Forwards packet to next closest router
- Router maintains a table of "next hop" to all destination networks
- Router maintains no per-connection state

### Virtual circuit (path) network: ###
- packets carry a 'tag' (virtual circuit ID) that determines next hop
- path determined at call setup time & lives throughout call
- Routers maintain per-call path state

#### How it works ####
- A static route is computed & assigned an ID (VC #)
- Router maintains per-connection state & must perform setup/ tear-down
- Packets contain VC id (different per router).  Why?
	- Router can only know that the VC isn't used only if it's per router
	- Otherwise: there would be a large amounts of collisions due to routers choosing the same VC
	- Much simpler problem to solve on a per-router basis

## Network Structure ##
- Taxonomy of networks
	- Telecommunication networks:
		- Circuit Switched:
			- FDM
			- TDM
		- Packet-switched:
			- Networks w/ VC
			- Datagrams

### Network Core ###
- Routers
- Network of networks

### Network Edge ###
- End systems (hosts)
	- live at edge
	- run applications
- Interaction paradigms:
	- Client/ server model:
		- Client requests, receives service from server
		- WWW browser/ server email client/ server
	- Peer-to-peer model:
		- Host interactions symmetric
		- File sharing (Napster, BitTorrent, etc)

### Access Networks ###
- Physical media: communication links
- How to connection end-systems to edge router?
	- Residential access networks
	- Institutional/ enterprise access networks
	- Mobile access networks
- Issues:
	- transmission speed?
	- shared vs. dedicated?

## Transport Services ##
- 2 main types: connection-oriented and connectionless
- Applications using TCP
	- HTTP, FTP, Telnet, SMTP
- Applications using UDP
	- DNS, streaming media, teleconferencing, internet telephony

### Connection-oriented service ###
- Goal: transfer data between end systems
- Handshaking: setup data transfer ahead of time
	- "Hello, hello back"
	- Set up "state" in two communicating hosts
- Transmit data
- Connection-oriented services on the internet: TCP [RFC 793]

### TCP Service Model ###
- Defined in the context of a 'connection'
- reliable, in-order, byte-stream
	- losses detected and recovered from
- flow control: sending won't overwhelm receiver
- congestion control: senders 'slow down sending rate' when network is congested

### Connection-less services ###
- Goal: transfer data between end systems
- Advantage: if the application doesn't not need reliability or you do not want to wait, use connection-less services
- In the wild: UDP [RFC 768]
	- unreliable data transfer
	- no flow control
	- no congestion control
