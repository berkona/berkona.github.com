---
layout: default
title: Homework 5|Interoperability
---

> Jonathan Monroe

# Homework 5: Interoperability

## Partners:
- Robin Saltz
- Gregory Monroe

First I logged into `classroom.cs.unc.edu`.
According to ifconfig, at the time of the test, the network state was such:

```
eth0      Link encap:Ethernet  HWaddr 00:26:B9:75:62:41
          inet addr:152.2.129.144  Bcast:152.2.143.255  Mask:255.255.240.0
          inet6 addr: fe80::226:b9ff:fe75:6241/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1655745632 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1957238338 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:284921861521 (265.3 GiB)  TX bytes:2819412673048 (2.5 TiB)

eth1      Link encap:Ethernet  HWaddr 00:26:B9:75:62:42
          BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 b)  TX bytes:0 (0.0 b)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:17821884 errors:0 dropped:0 overruns:0 frame:0
          TX packets:17821884 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:7663429758 (7.1 GiB)  TX bytes:7663429758 (7.1 GiB)

virbr0    Link encap:Ethernet  HWaddr 52:54:00:B8:4F:F3
          inet addr:192.168.122.1  Bcast:192.168.122.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:15718 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 b)  TX bytes:10259220 (9.7 MiB)

virbr0-nic Link encap:Ethernet  HWaddr 52:54:00:B8:4F:F3
          BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:500
          RX bytes:0 (0.0 b)  TX bytes:0 (0.0 b)


```

I then proceeded to setup the server:

```
-bash-4.1$ cd /home/jwmonroe/comp431/submissions/server_files/
-bash-4.1$ java -cp ../HW5/ FTPServer 4223 &
[1] 7900
```

I then confirmed the server was running:

```
-bash-4.1$ jobs
[1]+  Running                 java -cp ../HW5/ FTPServer 4223 &
```

In a separate terminal, I logged into `bluetang.cs.unc.edu`, and checked its network state:

```
-bash-4.1$ ifconfig -a
em1       Link encap:Ethernet  HWaddr 00:26:B9:75:66:3C
          inet addr:152.2.128.63  Bcast:152.2.143.255  Mask:255.255.240.0
          inet6 addr: fe80::226:b9ff:fe75:663c/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:206054378 errors:0 dropped:0 overruns:0 frame:0
          TX packets:41556248 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:41726202485 (38.8 GiB)  TX bytes:25267918158 (23.5 GiB)

em2       Link encap:Ethernet  HWaddr 00:26:B9:75:66:3D
          inet addr:10.2.140.7  Bcast:10.2.143.255  Mask:255.255.240.0
          inet6 addr: fe80::226:b9ff:fe75:663d/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:164084768 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1749 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:18210896426 (16.9 GiB)  TX bytes:368241 (359.6 KiB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:12908827 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12908827 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:2923591572 (2.7 GiB)  TX bytes:2923591572 (2.7 GiB)

virbr0    Link encap:Ethernet  HWaddr 52:54:00:DC:E7:90
          inet addr:192.168.122.1  Bcast:192.168.122.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:13 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 b)  TX bytes:2688 (2.6 KiB)

virbr0-nic Link encap:Ethernet  HWaddr 52:54:00:DC:E7:90
          BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:500
          RX bytes:0 (0.0 b)  TX bytes:0 (0.0 b)

```

## Test 1, Unix to Unix

I then opened bluetang's FTP program and attempted to download all five files.

```
-bash-4.1$ ftp
ftp> open classroom.cs.unc.edu 4223
Connected to classroom.cs.unc.edu (152.2.129.144).
220 COMP 431 FTP server ready.
Name (classroom.cs.unc.edu:jwmonroe): anonymous
331 Guest access OK, send password.
Password:
230 Guest login OK.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> binary
200 Type set to I.
ftp> GET HelloWorld.java
?Invalid command
ftp> get HelloWorld.java
local: HelloWorld.java remote: HelloWorld.java
500 Syntax error, command unrecognized.
Passive mode refused.
ftp> get lan-image.jpg
local: lan-image.jpg remote: lan-image.jpg
500 Syntax error, command unrecognized.
Passive mode refused.
ftp> get phone.gif
local: phone.gif remote: phone.gif
500 Syntax error, command unrecognized.
Passive mode refused.
ftp> get state-machine.pdf
local: state-machine.pdf remote: state-machine.pdf
500 Syntax error, command unrecognized.
Passive mode refused.
ftp> get unc-logo.png
local: unc-logo.png remote: unc-logo.png
500 Syntax error, command unrecognized.
Passive mode refused.
ftp> quit
221 Goodbye.
```

## Test 2, Unix to Windows 7

Note in the above that we get a `500 Syntax error, command unrecognized.` followed by a `Passive mode refused.`.  My conclusion from this is that the FTP client for bluetang is attempting to send a command that is not in our subset of commands we have programmed.  To see if a different client would allow me to download the files, I setup the COMP431 FTPServer on my laptop (running Xubuntu 12.10) connected to my local network.  The network topography is relatively simple, a single wireless router, a separate DHCP server, and several hosts in a dhcp-leased subnet.  The executable used for my laptop was the same as that run on classrooom.  The setup was exactly the same as mentioned above in setting up classroom's server.  As a client, I used a windows host running Windows 7 Home Professional.  The result of this test proved my theory:


```
ftp> open 10.10.10.116 4223
Connected to 10.10.10.116.
220 COMP 431 FTP server ready.
User (10.10.10.116:(none)): anonymous
331 Guest access OK, send password.
Password:
230 Guest login OK.
ftp> binary
200 Type set to I.
ftp> get HelloWorld.java
200 Port command successful (10.10.10.144,2067).
150 File status okay.
250 Requested file action completed.
ftp: 114 bytes received in 0.00Seconds 114000.00Kbytes/sec.
ftp> get phone.gif
200 Port command successful (10.10.10.144,2097).
150 File status okay.
250 Requested file action completed.
ftp: 1141 bytes received in 0.01Seconds 76.07Kbytes/sec.
ftp> get lan-image.jpg
200 Port command successful (10.10.10.144,2113).
150 File status okay.
250 Requested file action completed.
ftp: 14854 bytes received in 0.01Seconds 1485.40Kbytes/sec.
ftp> get state-machine.pdf
200 Port command successful (10.10.10.144,2122).
150 File status okay.
250 Requested file action completed.
ftp: 115104 bytes received in 0.05Seconds 2449.02Kbytes/sec.
ftp> get unc-logo.png
200 Port command successful (10.10.10.144,2133).
150 File status okay.
250 Requested file action completed.
ftp: 17265 bytes received in 0.02Seconds 863.25Kbytes/sec.
ftp> quit
221 Goodbye.
```

I then transferred the files to my laptop and performed a diff for each file:

```
berkona@engineering:~/dev/comp431/server_files$ diff HelloWorld.java ~/Dropbox/host\ A/HelloWorld.java
berkona@engineering:~/dev/comp431/server_files$ diff phone.gif ~/Dropbox/host\ A/phone.gif
berkona@engineering:~/dev/comp431/server_files$ diff lan-image.jpg ~/Dropbox/host\ A/lan-image.jpg
berkona@engineering:~/dev/comp431/server_files$ diff state-machine.pdf ~/Dropbox/host\ A/state-machine.pdf
berkona@engineering:~/dev/comp431/server_files$ diff unc-logo.png ~/Dropbox/host\ A/unc-logo.png
```

## Test 3, Internet Browser Compatability

Tests with both Internet Explorer 10 and Mozilla Firefox 11 (on Windows 7 Home Professional) resulted in a "This page can't be display" and "500 Syntax error, command unrecognized." respectively.


I couldn't find anyone in class to help me test for interoperability, so I ended up enlisting some friends to help me.  I repeated tests 2 and 3 using my laptop as the server and their hosts as the client.  Test 3 on all 3 hosts resulted in identical messages, and so I have omitted the output from this report.

The following is the results from test 2 conducted on both hosts.

### Robin Saltz Test 2 Results (Host OS: Windows 7 Home Pro)

```
ftp> open 192.168.100.103 4223
Connected to 192.168.100.103.
220 COMP 431 FTP server ready.
User (192.168.100.103:(none)): anonymous
331 Guest access OK, send password.
Password:
230 Guest login OK.
ftp> binary
200 Type set to I.
ftp> GET HellowWorld.java
200 Port command successful (192.168.100.102,50374).
550 File not found or access denied.
ftp> GET HelloWorld.java
200 Port command successful (192.168.100.102,50381).
150 File status okay.
250 Requested file action completed.
ftp: 114 bytes received in 0.00Seconds 114.00Kbytes/sec.
ftp> GET lan-image.jpg
200 Port command successful (192.168.100.102,50388).
150 File status okay.
250 Requested file action completed.
ftp: 14854 bytes received in 0.12Seconds 123.78Kbytes/sec.
ftp> GET phone.gif
200 Port command successful (192.168.100.102,50392).
150 File status okay.
250 Requested file action completed.
ftp: 1141 bytes received in 0.00Seconds 1141000.00Kbytes/sec.
ftp> GET state-machine.pdf
200 Port command successful (192.168.100.102,50393).
150 File status okay.
250 Requested file action completed.
ftp: 115104 bytes received in 0.22Seconds 525.59Kbytes/sec.
ftp> GET unc-logo.png
200 Port command successful (192.168.100.102,50397).
150 File status okay.
250 Requested file action completed.
ftp: 17265 bytes received in 0.10Seconds 166.01Kbytes/sec.
ftp> quit
221 Goodbye.
```

Diff indicated bitwise identicality for each file.

### Gregory Monroe Test 2 Results (Host OS: Fedora)

```
ftp> open 192.168.100.103 4223
Connected to 192.168.100.103.
220 COMP 431 FTP server ready.
Name (192.168.100.103:monroe): anonymous
331 Guest access OK, send password.
Password:
230 Guest login OK.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> get HelloWorld.java
local: HelloWorld.java remote: HelloWorld.java
200 Port command successful (192.168.100.50,58779).
150 File status okay.
250 Requested file action completed.
114 bytes received in 0.00 secs (1568.0 kB/s)
ftp> get ^C
ftp> get  phone.gif
local: phone.gif remote: phone.gif
200 Port command successful (192.168.100.50,51534).
150 File status okay.
250 Requested file action completed.
1141 bytes received in 0.00 secs (2459.7 kB/s)
ftp> get lan-image.jpg
local: lan-image.jpg remote: lan-image.jpg
200 Port command successful (192.168.100.50,44255).
150 File status okay.
250 Requested file action completed.
14854 bytes received in 0.05 secs (266.2 kB/s)
ftp> get state-machine.pdf
local: state-machine.pdf remote: state-machine.pdf
200 Port command successful (192.168.100.50,49090).
150 File status okay.
250 Requested file action completed.
115104 bytes received in 0.10 secs (1078.5 kB/s)
ftp> get unc-logo.png
local: unc-logo.png remote: unc-logo.png
200 Port command successful (192.168.100.50,32776).
150 File status okay.
250 Requested file action completed.
17265 bytes received in 0.06 secs (269.3 kB/s)
ftp> ls
200 Port command successful (192.168.100.50,41478).
500 Syntax error, command unrecognized.
ftp> quit
221 Goodbye.
```

Diff indicated that the files were identical.

## Conclusion

Given the results of the tests above, I conclude that my server is compatibile with the Windows ftp command line client as well as some unix-based clients.  The server does not work for either Internet Explorer or Mozilla Firefox.  It would be hard to tell without further information from the browser, but given the error messages, I believe that the COMP431 Server does not support some command which the browsers send to it.  This conclusion is supported by the contrast between test 1 (unix to unix) and test 2 (unix to windows).  The error code from test 1 was also a 500.  However, in order to isolate which command is being sent, we would need more information from the client than we are given.
