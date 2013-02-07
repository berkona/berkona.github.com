---
title: FTP Programming
date: February 07 2013 11:20
layout: note
---

UDP vs. TCP
-----------

UDP only looks at the destination socket.  TCP is tied to both end points, UDP is tied only to one end point.

TCP Service
------------

TCP does not provide timing or minimum bandwidth guarantees.

URLs
-----

Domain Name
: first part of the url, DNS name of the server and where to find the machine
Server Port
: (optional) specifies a port to connect to on the server
Path Name
: How to location the object within the server's filesystem

HTTP
----

Implements a client & server model.  The protocol is independent of who sends the request or what operating system the client or server is running.

HTTP uses TCP sockets.  Typically HTTP uses port 80.  HTTP is an application-layer protocol.  HTTP messages specified by RFC 1945 (HTTP 1.0) & RFC 2616 (HTTP 1.1)

HTTP 1.0
: One request, response interaction per connection
HTTP 1.1
: Persistent connections - connection doesn't close at server response
: Pipelined connections - writing to a socket multiple times without waiting for a response each time.  Speeds up

HTTP is 'stateless.'  Server maintains no information about past browser requests.  Why?  Some servers are distributed&em;they don't have the ability to share memory between processes.  The process might crash, and if you maintained state the server would have to restore the state.  How? Databases? This increases the complexity of the protocol.

Two types of HTTP message formats: *request* and *response* messages, both written in ASCII text format.

HTTP Example
============

1) User enters URL: www.unc.edu/someDept/home.index

2) Referenced object contains HTML text & references to 10 JPEG images

3) Browser sends HTTP 'GET' request to server

4) Server retrieves and sends the file

5) Browser will read the file and sequentially make 10 separate requests for the embedded JPEG images.

See HTTP 1.0 example slide

HTTP Message Protocol
=====================
```
method <SP> path <SP> version <CR><LF> // Request line
header field name ":" value <CR><LF> //Optional
```

```
GET /~jasleen HTTP/1.0
Connection: Keep-Alive
User-Agent: Mozilla/4.74 [en] (WinNT; U)
Host: example.com
Accept: x-type/mime-type
Accept-Encoding: gzip
Accept-Language: en
Accept-Charset: iso-8859-1,*,utf-8
Cookie: DOMAIN=8a8b64
```
