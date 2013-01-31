---
title: Protocols and Service Layers
date: January 31 2013 11:55
layout: note
---

What is a protocol?  A set of conventions governing how you format data and how
respond and talk to each other.  All communication activity on the Internet is
governed by protocols.  Specific messages are sent and specific actions are
taken when messages are received.  Protocols define a format and order of messages
sent and received and actions taken upon receipt.

## Protocol Layers ##

Networks are composed of many 'pieces'.  Solution: decompose functions into a
stack of function 'layers'.  Each layer provides 'services' to the layer above
it and uses the services below it.  Allows implementation of layers to be
separate as long as the interface of the layer remains the same.  Each layer
can treat everything below it in the stack as a 'black box'.  Each layer talks
with its peer layer in a distributed system.  Layer headers act like stacks.

Why? Explicit structure allows identifying and relating complex system's pieces.
Modularization eases maintenance.  Changing implementation doesn't affect other
parts of the system.

Could it be harmful?  There is additional data added on by each layer.  If the
black box is mis-implemented, it could result in subtle errors.

## Layer Functions ##

### Error Control ###
Error control makes the logical channel between layers reliable.

### Flow Control ###

Avoid overwhelming a peer by sending data

### Segmentation &amp; Reassembly ###

Partitioning large message into smaller ones and reassembling them

### Multiplexing ###

Interleaving data signals.
