# Nteworking - VPC #
CIDR -IPv4
* Classes Inter Domain Registry - a method for allocating IP addresses.
* Used in Security groups
* CIDR has 2 components
   * Base IP - represents IP contained in the range (XX.XX.XX)
   * Example : 10.0.0.0,192.168.0.0
 
   * Sunet Mask
   * defines how many bits can change in the IP
   * Example: 0,/24,/32

 # Default VPC #

  * All new accounts have a default VPC.
  * New Ec2 instances are launched ino the default VPC if no subnet is specified.
  * Also gets public and private DNS service.

 # Subnets #

  * We add public and private subnets in VPC
  * Sub range of IPV4 addresses within your VPC
  * AWS reserves 5 IP Addresses in eacch subnet.

# Internet Gateway #
 * Allows resources (eg. EC2 instances) in a VPC connect to the Internet.
 * Scales horizontally and is highly available and reduntant.
 * Must be created sepreately from a VPC.
 * One VPC can be attached to one Internet Gate wa.

# Bastion Hosts #
 * It is an EC2 instance in a public subnet.
 * We can use bastion host to SSH into our private EC2 instances.
 * The bastion host is in public subnet which is then connected to all other private subnets.

# NAT Instances #
 * Allows EC2 instances in private subnets to connect to the internet.
 * Must be launched in Public Subnet.
 * Must have elastic IP attached to it.

# NAT Gateways #
* AWS managed NAT, higher bandwidth, high availability
* Pay per hour usage
* NAT gateway is created in specific AZ, uses an elastic IP
* Requires Internet Gateway
* No security groups required.

# Network Access Control List (NACL) #
 * NACL are like firewall which control traffic from and to subnets.
 * One NACL per subnet, new subnets are assigned to default NACL
 * NACL are a great way of blocking a specific IP address at the subnet level.

# VPC Peering #
 * Privately connect two VPC's using AWS network.
 * VPC peering connection is not transitive.
 * Can create VPC peering connection between VPC's in different AWS accounts/regions.

# VPC Endpoints #
* Private endpoints that allows you to initiate a private connection to AWS services.
* Allows to connect to AWS sevices usina a private network instead of using the public network.
* They remove the need of Internet Gateway and NAT Gateway.

# Types of Endpoints #
* Interface Endpoints
* Gateway Endpoints

# AWS Site to Site VPN #
* Virtual Private Gateway ( VGW)
  * VGW is created and attached to the VPC from which you want to create Site to Site VPN connection
* Customer Gateway (CGW)
   * Software application or physical device on customer side of the VPN connection.
 
# Direct Connect #
* provides a dedicated private connection from a remote network to your VPC.
* Have to set up a Virtual Private Gateway on your VPC.

# AWS Private Link #
* Most secure and scalable way to expose a service to 1000s of VPC.
* Requires a Load Balancer and ENI.

# Transit Gateway
* For having transitive peering between thousands of VPC and on-premises
* Works with direct connect gateway, VPN connection

# VPC Traffic Mirroring #
* Allows to capture and inspect network ttraffic in your VPC.
* Capture the trffic from Source and Targets.
* Source and Target can be in the same VPC or different VPC's.















