#### Linux Networking
### TCP vs UDP
![TCP states](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd49cf186-9875-4a44-9432-1b284e5be594_1432x596.png) 
- Packets arrive in order in TCP, out of order in UDP
- Client server establishes connection(3 way handshake) in TCP, no connection in UDP
- TCP header - 20 Bytes, UDP header - 8 Bytes
- TCP point to point, UDP unicast, multicast, broadcast
- Congestion control vs no congestion control
- Flow control vs no flow control

### IP protocol
- IP is connectionless because it treats each packet of information independently. It is unreliable because it does not guarantee delivery, meaning, it does not require acknowledgments from the sending host, the receiving host, or intermediate hosts.
- IP fragments
  - When a router receives a packet, it examines the destination address and determines the outgoing interface to use and that interface's MTU. If the packet size is bigger than the MTU, and the Do not Fragment (DF) bit in the packet's header is set to 0, then the router may fragment the packet.
  - IPv6, the next generation of the Internet Protocol, does not allow routers to perform fragmentation; hosts must perform Path MTU Discovery before sending datagrams.
  - The receiver identifies matching fragments using the source and destination addresses, the protocol ID, and the identification field. The receiver reassembles the data from fragments with the same ID using both the fragment offset and the more fragments flag. 
