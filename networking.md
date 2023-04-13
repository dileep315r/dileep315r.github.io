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

### Anycast address
Anycast—This type of IP address, formally defined in IPv6, is used to identify a defined set of interfaces, usually on different devices. Anycast addresses are used to deliver packets to the “nearest” interface, where nearness is defined as a routing parameter. The same can be done in IPv4, but not as elegantly.

### GeoDNS
https://en.wikipedia.org/wiki/GeoDNS

### Linux network configuration
1. https://www.baeldung.com/linux/network-interface-configure#:~:text=Simply%2C%20a%20network%20interface%20is,networking%20to%20the%20hardware%20side.

### Linux network interfaces
1. As soon as the device driver is loaded into the Kernel a corresponding physical network interface becomes present and available.
2. Virtual network interfaces were invented to give the system administrator maximum flexibility when configuring a Linux-based operating system. A virtual network interface is generally associated with a physical network interface (eth6) or another virtual interface (eth6.9) or be stand alone such as the loopback interface lo.
3. https://openwrt.org/docs/guide-developer/networking/network.interfaces
4. https://developers.redhat.com/blog/2018/10/22/introduction-to-linux-interfaces-for-virtual-networking
5. 


### Commands
1. Command to get arp table
   1.  arp -la
2. Rough notes of the commands
   ```agsl
    routing tables || netstat
    ARP table || arp command
    icmp command for sending icmp packets
    traceroute
    icmp return message unreachable with TTL expired.
    conntrack command
    iperf3 command
    netfilter
    nft command
    iptables command
    routing hooks allow for firewall implementations in Linux
    masqurade —> apply NAT
    direct server return in load balancing
    DPDK
    XDP
    IPVS built on top of netfilter
    P4
    ```
