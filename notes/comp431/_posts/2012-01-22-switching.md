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

### Forwarding ###
- The process of moving packets among routes from a source to a destination
- There are various approaches
- Datagram networks must look up address each forward
- Virtual circuits determine hops only once
- Delayed expense vs. Long call setup

#### Datagram Network: ####
- Each packet carries a destination address
- Destination address used to look up next hop
- Route (next hop) may change at any time

#### Virtual circuit (path) network:
- packets carry a 'tag' (virtual circuit ID) that determines next hop
- path determined at call setup time & lives throughout call
- Routers maintain per-call path state
