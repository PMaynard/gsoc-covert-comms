# GSoC Proposal

## Introduction
A covert communication channel is a technique which exploits existing firewalls and intrusion detection systems (IDS). 

In Russ Rogers’ talk ”The Keys to the Kingdom” [1] he defines a covert channel as:

>”Any communication channel that can be exploited by a process to transfer informa-
>tion in a manner that violates the systems security policy.” 

Covert channels are not the same as an encrypted channel, with an encrypted channel it does not matter if it is discovered, as the payload will be ciphertext, which without the decryption key, would be unreadable. Whereas covert channels are designed to go unnoticed, this does not mean that a covert channel can not be encrypted.

## Use case.
A covert channel could be used in a situation where you are behind a restrictive firewall which only allows HTTP, DNS and ICMP packets. And you wish to connect to your server using SSH.

You'd setup a proxying server on your local machine, behind the firewall. And you'd setup a covert-proxy, or end node, on your remote server. Now you would point your SSH client at your localhost, the SSH data would be sent through the covert tunnel bypassing the restrictions of the network, and out to your server.

## References

[RUSS][1].

[1]: http://www.blackhat.com/presentations/bh-asia-04/bh-jp-04-pdfs/bh-jp-04-rogers.pdf        "RUSS"
