### AWS
#### Network implementation details
Subnet, VPN are simulated on top of original amazon network.
1. Each machine in amazon datacenter has amazon private ip and runs linux OS tailored for AWS. VMs in each machine is assigned a client/customer defined private ip.
2. VM's network packet is wrapped in another packet with amazon private ip source and amazon private ip destination addresses. Wrapper contains info about VPC as well so that the VPC is checked at source and destination for security reasons.
3. Amazon Linux OS find out the amazon private ip address for the customer packet using amazon mapping service.
   1. Mapping service data is cached locally to avoid extra network hop for finding MAC/Ip addresses.
   2. For hosts within the subnet, 
      1. Packets will be broadcast to all nodes in VLAN.
      2. Packets need not go through the subnet router.
      3. In AWS, packets may travel through router ,not sure!!
4. Kind of tunnel created. Customer view of network is simulated on amazon's network.
5. Bridge server(IG gateway, VPN gateway etc..) translates amazon specific packets to the general internet packets and vice versa.
   1. IG gateway translates private ip address of the host to the public ip and vice versa.

##### VPN
- Virtual private cloud. AWS talk says the VPN can be implemented using VRF(virtual routing and forwarding). 
- Synonymous to a data center i.e a virtual datacenter
- Can contain multiple physical/logical instances/services from multiple physical AZs
- Contains several subnets
- Subnet must belong to a availability zone
- VPN can be configured with one IG gateway to send/receive traffic to/from the internet.
- IG gateway is exposed as a single router to the customers, but it could have been set of routers in multiple AZs
- IG gateway route table can be configured.
- Route53 service provides DNS authoritative name service/server for custom domain.
- Different types of LBs available. ApplicationLB, NetworkLB.

##### Region and AZ
1. Region is a set of data centers in a location. Most of the services are region scoped i.e most of the services deployed in different regions are independent.
2. AZ(availability zone) is a datacenter or set of co-located datacenters with shared power supply. 
   1. Different AZs provide fault tolerance within a single region.

##### Subnet
1. Similar to subnet in datacenters.
   1. Subnet potential benefits in traditional networks.
      1. May reduce number of hops to reach a destination. Efficient routing.
      2. Organize network according to organizational needs.
      3. VLAN limits the broadcast space.
      4. Subnet traffic stays within the subnet.
      5. All the hosts in subnet generally stay in a similar location.
      6. Organizing a network in an efficient way is crucial for large firms
      7. IP addresses can be kept geographically localized meaning that a subnet can be used for specific staffing structures to reduce traffic and maintain efficiency and order.
2. Subnet contains instances
3. Subnet is connected to at least one router.
4. Subnet router route table can be configured with outbound and inbound traffic rules.
5. Subnet router might have been connected internally to other internal routers and IG gateway routers.
6. All IPv6 addresses are public.
7. NACL network access control list firewall rules can be configured at Subnet level.
8. Local target in route table keeps the traffic inside subnet and IG gateway target sends the traffic to IG gateway.
9. If a subnet is associated with a route table that has a route to an internet gateway, it's known as a public subnet. If a subnet is associated with a route table that does not have a route to an internet gateway, it's known as a private subnet.
10. Instances in the private subnet can't communicate with the internet over the internet gateway, even if they have public IP addresses.
11. Each subnet must reside entirely within one Availability Zone and cannot span zones.
12. By design, each subnet must be associated with a network ACL(NACL).

#### IG gateway
1. If a subnet is associated with a route table that has a route to an internet gateway, it's known as a public subnet. If a subnet is associated with a route table that does not have a route to an internet gateway, it's known as a private subnet.


##### Instance
1. EC2 instance. Compute machine with CPUs and storage. Storage is connected to the instance through special Storage Area Network(SAN).
2. Each instance by default gets a private id address and a private domain name. A public instance gets a public domain name.
3. Instance is public if it has public ip address assigned to it. Only public instances are accessible to the internet.
4. NAT gateway must be configured in order for the private instances to access the internet.
5. An instance must belong to a security group. Multiple instances can share the same security group.
6. A security group defines network firewall rules i.e allows/denies traffic.
   1. By default, all the traffic is blocked
   2. SG rules get evaluated on the instance. If the firewall allows traffic in, it will automatically allows same traffic to go out.
   3. SG can be configured to allow traffic from another SG.
7. Public IPv4 address of an instance changes if the instance is restarted. 
8. Private IPv4 address doesn't change after instance restarts.
9. Elastic IPv4 address doesn't change with instance restarts, but limited to five per account. Elastic ip address can be reconfigured to different instances dynamically. Don't use this practice though.
10. Source port numbers received by network clients from operating system are called ephemeral port numbers.
11. Configure Ephemeral portal ranges correctly in NACL rules to allow traffic back from the server.
12. Your instance is only aware of the private (internal) IP address space defined within the VPC and subnet. The internet gateway logically provides the one-to-one NAT on behalf of your instance, so that when traffic leaves your VPC subnet and goes to the internet, the reply address field is set to the public IPv4 address or Elastic IP address of your instance, and not its private IP address. Conversely, traffic that's destined for the public IPv4 address or Elastic IP address of your instance has its destination address translated into the instance's private IPv4 address before the traffic is delivered to the VPC.

#### Route table
1. Every route table contains a local route for communication within the VPC. This route is added by default to all route tables. If your VPC has more than one IPv4 CIDR block, your route tables contain a local route for each IPv4 CIDR block.
2. You can add a route to your route tables that is more specific than the local route. The destination must match the entire IPv4 or IPv6 CIDR block of a subnet in your VPC. The target must be a NAT gateway, network interface, or Gateway Load Balancer endpoint.
3. All IPv6 traffic (except for traffic within the VPC) is routed to the egress-only internet gateway.
4. There is a route for all IPv4 traffic (0.0.0.0/0) that points to an internet gateway.
5. IPv6 traffic is separate from IPv4 traffic; your route tables must include separate routes for IPv6 traffic.

#### Unanswered questions
1. Do Route tables, NACL, Security Groups work on public IPv4 address range as well?
   1. What happens if there is no route table entry for fellow subnet bound traffic and traffic gets sent to IG gateway? I think IG gateway should contain local traffic rules.
2. Do the IG gateway translates the private IPv4 address to public IPv4 address for outbound traffic?
   1. Do the instances doesn't work with public ipv4 address? Is the public ipv4 address only used for outbound traffic?
3. Does every router in AWS datacenter store the route tables of every other customer to allow for virtualization?
4. Do the instances in a single subnet map to a real subnet in the AWS datacenter?


##### References
1. [IG gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html)
2. [Good youtube video on AWS networking](https://www.youtube.com/watch?v=3qln2u1Vr2E)
3. Good reference for [AWS NLB source ip presevation](https://www.reddit.com/r/aws/comments/mv41vs/how_do_nlbs_preserve_the_ip_address_of_clients/)
