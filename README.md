# GSoC Proposal

## Introduction
A covert communication channel is a technique which exploits existing firewalls and intrusion detection systems (IDS). 

In Russ Rogers’ talk ”The Keys to the Kingdom” [1] he defines a covert channel as:

>”Any communication channel that can be exploited by a process to transfer informa-
>tion in a manner that violates the systems security policy.” 

[Expain more about the techinical parts of a covert channel]

[Awesome Diagram HERE]

[ptunnel][2]

[mydiss][3]

Covert channels are not the same as an encrypted channel, with an encrypted channel it does not matter if it is discovered, as the payload will be ciphertext, which without the decryption key, would be unreadable. Whereas covert channels are designed to go unnoticed, this does not mean that a covert channel can not be encrypted.

## Use case.
A covert channel could be used in a situation where you are behind a restrictive firewall which only allows HTTP, DNS and ICMP packets. And you wish to connect to your server using SSH.

You'd setup a proxying server on your local machine, behind the firewall. And you'd setup a covert-proxy, or end node, on your remote server. Now you would point your SSH client at your localhost, the SSH data would be sent through the covert tunnel bypassing the restrictions of the network, and out to your server.

## Proposal

### A - Existing application imporvements.

#### Existing Work

I've written for my final year project, a covert channel to run on GNU/Linux. It currently supports covert channels over ICMP, and has a working applciation proxy, and end node. Though there is an issue with buffer lengths whcih needs to be investigated.

Even though there is existing code, due to the nature of the fianl year project, I feel it would be worth while to spend some time rewritting some of the legacy code to reflect what I've learnt since implementing it.

#### Project Goals

- Primary Goals
 - Open Source the current implementation.
 - Bug fixing and hignsight re implentation of some features (inter-proccess communcation and pre-forking)
 - Implement protocol hopping of a minimumn of two (ICMP and DNS)

- Secondary Goals
 - Implement as many covert protocols as possible (Bit Manipulation of TCP and IP Headers, DNS)

### B - Android from Scratch.

Using the knowledge from my final year project, I propose to design and implement a covert communication channel for the Android Operating System. Which will be able to bypass current firewalls and IDS.

#### Project Goals
- Primary Goals
 - Proxy Server - To proxy connections from android applcaitons to the covert server.
 - Covert Server - To handle covert communcations, to and from the android device.
 - Implement a basic covert channel, such as ICMP.

- Secondary Goals
 - Implement as many covert protocols as possible (Bit Manipulation of TCP and IP Headers, DNS)

#### Work to be carried out

In the beggining of the project I will have to do some spike work into android packet sniffing and packet manipulation. Does this require a rooted device, etc. 

Next step would be how we should go about getting android applications to use a proxy server. 

After that we will need to implement the proxy server, written in Java for the android OS, as well as the covert server.

## References

[RUSS][1]

[ptunnel][2]

[mydiss][3]

[1]: http://www.blackhat.com/presentations/bh-asia-04/bh-jp-04-pdfs/bh-jp-04-rogers.pdf        "RUSS"
[2]: http://www.cs.uit.no/~daniels/PingTunnel/index.html                                       "ptunnel"
[3]: http://users.aber.ac.uk/pem9/dissertation.pdf                                             "mydiss"
