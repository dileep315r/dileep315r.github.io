#### Load balancers
1. The small size of the DNS packet (512 Bytes) isn’t enough to include all possible IP addresses of the servers.
2. There’s limited control over the client’s behavior. Clients may select arbitrarily from the received set of IP addresses. Some of the received IP addresses may belong to busy data centers.
3. Clients can’t determine the closest address to establish a connection with. Although DNS geolocation and anycasting-like solutions can be implemented, they aren’t trivial solutions.
4. In case of failures, recovery can be slow through DNS because of the caching mechanism, especially when TTL values are longer.
5. Stateful vs Stateless, Local vs Global vs client side. Layer 4 vs Layer 7
6. If DNS can be considered as the tier-0 load balancer, equal cost multi-path (ECMP) routers are the tier-1 LBs. From the name of ECMP, it’s evident that this layer divides incoming traffic on the basis of IP or some other algorithm like round-robin or weighted round-robin. Tier-1 LBs will balance the load across different paths to higher tiers of load balancers.
7. ECMP routers play a vital role in the horizontal scalability of the higher-tier LBs.
8. LB's hierarchy tiero - DNS, tier1 - Router, tier2 - LB1, tier3 - LB2
9. LB's can handle congestion control, SSL/TLS offloading etc to reduce burden on app servers.
10. This tier also reduces the burden on end-servers by handling low-level details like TCP-congestion control protocols, the discovery of Path MTU (maximum transmission unit), the difference in application protocol between client and back-end servers, and so on. The idea is to leave the computation and data serving to the application servers and effectively utilize load balancing commodity machines for trivial tasks. In some cases, layer 7 LBs are at the same level as the service hosts.

Handling Websocket connections
   1. Connect device to a single server throughout the lifetime of the session. 
   2. Reverse lookup server to client info to push data to the client.

#### Load balancer scaling
1. Dynamically resolve DNS to one of the load balancer addresses.
2. Client connects to the LB throughout the processing of the request.
3. Nice stackoverflow answer https://stackoverflow.com/questions/50140364/does-a-load-balancer-need-a-load-balancer

#### SSL/TLS connection and load balancers
1. SSL connections are generally terminated at user facing load balancers since
   1. Configuration of SSL/TLS is tricky. Maintenance overhead is high.
   2. Copying certificates to multiple servers increases the likelihood of exposing the certificates.
2. Client and server needs to store shared encryption keys
   1. Client to server encrypted connection terminate at LB. Terminate the connection from user client to server once the request is processed.
      1. Maintain several encrypted connections from LB to servers. Send the client request along one of the encrypted connection.
   2. Maintain encrypted connections from the microservice client to another microservice LBs as well.

#### Client side load balancing i.e kubernetes decentralised load balancing.
1. Select two servers randomly, compare the load and select the one with low load. Better load distribution than random selection.
2. Connection pool, maintain connections to set of servers instead of all servers to reduce connection overhead. Use Deterministic aperture strategy to select set of servers out of all servers.
   1. Mesh network - Each client connects to all the servers. Connection overload problem.
   2. Random aperture - Each client picks k(>= m) out of m servers randomly. Some servers may be idle.
   3. Deterministic aperture - Form ring of servers and clients, pick servers within a range of the clients.

#### LB
1. LB can operate at multiple layers i.e HTTP level, TCP level.
2. External LB maintains persistent connections to API gateway servers. Persistent connections reduce the response time by avoiding TCP handshake everytime.
3. LB handles the connection with the client. Sends the HTTP request from client to one of the servers through one of the persistent connections.
4. DNS load balancers
   1. Least cost load balancing solution. Hardware and software load balancers can be costly.
   2. Least connections, Round robin and other DNS algorithms can be used.
   3. DNS TTL is reduced for highly dynamic(i.e respond to target server errors quickly) load balancing. 
   4. DNS TTL reduction leads to increased traffic to the DNS infrastructure.
   5. Failure of load balancer in ISP leads to service outages since DNS load balancing method depends heavily on DNS infra.
      1. Online retailers, trading systems use the standard load balancing.
   6. DNS load balancing can perform geo-location load balancing i.e send traffic from certain location to a specific set(generally closest) of servers. Cloudfare DNS load balancer provides geo-location load balancing.
   7. For example Google's App Engine infrastructure still uses/recommends DNS load balancing - the procedure for Mapping Custom Domains to an app makes it appear under 4 different IP addresses.
   8. Nice answer https://softwareengineering.stackexchange.com/questions/404590/are-there-still-reasons-to-use-dns-for-load-balancing

#### [AWS LB service](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html)
1. Gateway load balancer(all traffic goes through GLB), network load balancer(Operates at Layer 4 - transport layer - TCP/UDP level), application load balancer(operates at application layer - HTTP level)
2. A load balancer accepts incoming traffic from clients and routes requests to its registered targets (such as EC2 instances) in one or more Availability Zones.
3. When you enable an Availability Zone for your load balancer, Elastic Load Balancing creates a load balancer node in the Availability Zone.
4. Cross-zone load balancing
   1. When cross-zone load balancing is enabled, each load balancer node distributes traffic across the registered targets in all enabled Availability Zones.
   2. When cross-zone load balancing is disabled, each load balancer node distributes traffic only across the registered targets in its Availability Zone.
   3. Clients send requests, and Amazon Route 53 responds to each request with the IP address of one of the load balancer nodes.
5. Zonal shift
   1. Zonal shift is a capability in Amazon Route 53 Application Recovery Controller (Route 53 ARC). With zonal shift, you can shift a load balancer resource away from an impaired Availability Zone with a single action.
6. The MTU size on load balancer nodes is not configurable. Jumbo frames (9001 MTU) are standard across load balancer nodes for Application Load Balancers, Network Load Balancers, and Classic Load Balancers. Gateway Load Balancers support 8500 MTU.
7. As traffic to your application changes over time, Elastic Load Balancing scales your load balancer and updates the DNS entry. The DNS entry also specifies the time-to-live (TTL) of 60 seconds. This helps ensure that the IP addresses can be remapped quickly in response to changing traffic.
8. Before a client sends a request to your load balancer, it resolves the load balancer's domain name using a Domain Name System (DNS) server. The DNS entry is controlled by Amazon, because your load balancers are in the amazonaws.com domain. The Amazon DNS servers return one or more IP addresses to the client. These are the IP addresses of the load balancer nodes for your load balancer.
9. NLB(Operates at Layer 4 - transport layer - TCP/UDP level) can terminate SSL/TLS connections.
   1. For TCP traffic, the load balancer selects a target using a flow hash algorithm based on the protocol, source IP address, source port, destination IP address, destination port, and TCP sequence number. The TCP connections from a client have different source ports and sequence numbers, and can be routed to different targets.
   2. Each individual TCP connection is routed to a single target for the life of the connection.
   3. For UDP traffic, the load balancer selects a target using a flow hash algorithm based on the protocol, source IP address, source port, destination IP address, and destination port. A UDP flow has the same source and destination, so it is consistently routed to a single target throughout its lifetime. Different UDP flows have different source IP addresses and ports, so they can be routed to different targets.
   4. If there are no healthy targets registered with the Network Load Balancer or if the Network Load Balancer nodes in a given zone are unhealthy, then Amazon Route 53 will direct traffic to load balancer nodes in other Availability Zones.
   5. Network Load Balancer preserves the client side source IP allowing the back-end to see the IP address of the client. This can then be used by applications for further processing.
10. [ALB](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html) - operates at HTTP level
    1. Can route the traffic based on URL, HTTP headers, custom HTTP response, authentication of users.
11. [GLB](https://docs.aws.amazon.com/elasticloadbalancing/latest/gateway/introduction.html)
    1. Gateway Load Balancers enable you to deploy, scale, and manage virtual appliances, such as firewalls, intrusion detection and prevention systems, and deep packet inspection systems. It combines a transparent network gateway (that is, a single entry and exit point for all traffic) and distributes traffic while scaling your virtual appliances with the demand.
    2. A Gateway Load Balancer operates at the third layer of the Open Systems Interconnection (OSI) model, the network layer. It listens for all IP packets across all ports and forwards traffic to the target group that's specified in the listener rule. It maintains stickiness of flows to a specific target appliance using 5-tuple (for TCP/UDP flows) or 3-tuple (for non-TCP/UDP flows).

### Direct server return
![DSR](https://support.kemptechnologies.com/hc/article_attachments/360061899171/DsrFlow.png)
1. Direct Server Return (DSR) is a method whereby traffic hits the LoadMaster on the way in and bypasses the LoadMaster on the way out. This feature was created to deal with a specific problem. When response traffic is greater than the request traffic, a load balancer could become a bottleneck.
2. Use virtual ip address magic. https://support.kemptechnologies.com/hc/en-us/articles/360031141991-How-Direct-Server-Return-DSR-works-

Questions to explore
1. Software defined network in AWS.
2. Is DNS load balancing better or software load balancing better.
3. How does AWS NLB preserves ip address of the clients.
4. Does NLB terminate connections at LB and re-uses/maintains connections to the backend server. How does the TCP packets look like after going through NLB?
5. Does ALB supports non connection termination. How does the TCP packets look like after going through ALB?
6. Good reference for [AWS NLB source ip presevation](https://www.reddit.com/r/aws/comments/mv41vs/how_do_nlbs_preserve_the_ip_address_of_clients/)
