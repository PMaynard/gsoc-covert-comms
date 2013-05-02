# GSoC Proposal

## Introduction
A covert communication channel is a technique which exploits existing firewalls and intrusion detection systems (IDS). 

In Russ Rogers’ talk ”The Keys to the Kingdom”[1] he defines a covert channel as:

>”Any communication channel that can be exploited by a process to transfer informa-
>tion in a manner that violates the systems security policy.” 

Covert channels bypass firewalls and IDS, by disguising data as other protocols. This was first documented in phrack issue 49, it was called [Project loki][4]. This uses the payload field of ICMP's request packet to hide user data such as HTTP, SSH etc. In doing so most firewalls will allow the ping packet to pass though with out any issue. A working example of this is [ptunnel][2].

The proposal, be it A or B, will follow a similar path to the image below.

![net-work-flow](http://port22.co.uk/i/network-flow.png)
Taken from [my dissertationn][3].

Covert channels are not the same as an encrypted channel, with an encrypted channel it does not matter if it is discovered, as the payload will be ciphertext, which without the decryption key, would be unreadable. Whereas covert channels are designed to go unnoticed, this does not mean that a covert channel can not be encrypted.

## Use case.
### SSH? No! 
A covert channel could be used in a situation where you are behind a restrictive firewall which only allows HTTP, DNS and ICMP packets. And you wish to connect to your server using SSH.

You'd setup a proxying server on your local machine, behind the firewall. And you'd setup a covert-proxy, or end node, on your remote server. Now you would point your SSH client at your localhost, the SSH data would be sent through the covert tunnel bypassing the restrictions of the network, and out to your server.

### Open network...
You're on the go, and stumble across an open wireless network. The network gives you an IP address, but won't let you send TCP or UDP packets out to the rest of the internet, for instance to check your mail. What to do? By chance, you discover that the network will allow you to ping any computer on the rest of the internet. With ptunnel, you can utilize this feature to check your mail, or do other things that require TCP. - Taken from [ptunnel][2].

## Proposal

### A - Existing application improvements.

#### Existing Work

I've written for my final year project, a covert channel to run on GNU/Linux. It currently supports covert channels over ICMP, and has a working application proxy, and end node. Though there is an issue with buffer lengths which needs to be investigated.

Even though there is existing code, due to the nature of the final year project, I feel it would be worth while to spend some time rewriting some of the legacy code to reflect what I've learnt since implementing it.

#### Project Goals

- Primary Goals
 - Open Source the current implementation.
 - Bug fixing and hindsight re implementation of some features (inter-process communication and pre-forking)
 - Implement protocol hopping of a minimum of two (ICMP and DNS)

- Secondary Goals
 - Implement as many covert protocols as possible (Bit Manipulation of TCP and IP Headers, DNS)

#### Existing Code

Before opening the code to the public, I need to check with the university.

[https://github.com/PMaynard/covert-comms-code](code)

### B - Android from Scratch.

Using the knowledge from my final year project, I propose to design and implement a covert communication channel for the Android Operating System. Which will be able to bypass current firewalls and IDS.

#### Project Goals
- Primary Goals
 - Proxy Server - To proxy connections from android application to the covert server.
 - Covert Server - To handle covert communications, to and from the android device.
 - Implement a basic covert channel, such as ICMP.

- Secondary Goals
 - Implement as many covert protocols as possible (Bit Manipulation of TCP and IP Headers, DNS)

#### Work to be carried out

In the beginning of the project I will have to do some spike work into android packet sniffing and packet manipulation. Does this require a rooted device, etc. 

Next step would be how we should go about getting android applications to use a proxy server. 

After that we will need to implement the proxy server, written in Java for the android OS, as well as the covert server.

## References

[1] [RUSS][1]

[2] [ptunnel][2]

[3] [mydiss][3]

[4] [loki][4]

[1]: http://www.blackhat.com/presentations/bh-asia-04/bh-jp-04-pdfs/bh-jp-04-rogers.pdf        "RUSS"
[2]: http://www.cs.uit.no/~daniels/PingTunnel/index.html                                       "ptunnel"
[3]: http://users.aber.ac.uk/pem9/dissertation.pdf                                             "mydiss"
[4]: http://www.phrack.org/issues.html?id=6&issue=49                                           "loki"
