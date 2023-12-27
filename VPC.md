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
* AWS managed NAT, higher bandwidth, high availabilit
* Pay per hour usage
* NAT gateway is created in specific AZ, uses an elastic IP
* Requires Internet Gateway
* No security groups requires.















