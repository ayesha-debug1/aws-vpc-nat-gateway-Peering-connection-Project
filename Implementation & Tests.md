## NAT gateway implementation steps

1. Create a VPC with the required IPv4 CIDR block.
2. Create two subnets within the VPC: one public subnet and one private subnet.
3. Create an Internet Gateway (IGW) and attach it to the VPC.
4. Configure the main route table by adding a default route (`0.0.0.0/0`) pointing to the Internet Gateway.
5. Create a custom route table and add a default route (`0.0.0.0/0`) pointing to the NAT Gateway once it is available.
6. Associate the public subnet with the main route table and the private subnet with the custom route table.
7. Launch two EC2 instances in the respective subnets: one in the public subnet and another in the private subnet.
8. Create a NAT Gateway in the public subnet and allocate an Elastic IP address.
9. Connect to the public EC2 instance, securely transfer the private EC2 instance's SSH key if required, and use it to establish an SSH connection to the private EC2 instance.

<br>

## VPC Peering Implementation Steps

1. Create a second VPC with a non-overlapping IPv4 CIDR block.
2. Create a subnet within the second VPC.
3. Create an Internet Gateway (IGW) and attach it to the second VPC.
4. Configure the subnet's route table association and add an Internet Gateway route if internet access is required.
5. Launch an EC2 instance in the subnet.
6. Create a VPC Peering connection by specifying the requester VPC and accepter VPC.
7. Accept the VPC Peering connection from the accepter VPC.
8. Update the route table in the first VPC by adding a route to the second VPC's CIDR block, targeting the VPC Peering connection.
9. Update the route table in the second VPC by adding a route to the first VPC's CIDR block, targeting the same VPC Peering connection.
10. Configure security groups to allow the required traffic between the EC2 instances.
11. Test connectivity between the instances using their private IP addresses.

<br>

## Testing and results 

| Step | Description | Result |
|------|-------------|--------|
| 1 | Added a default route to the Internet Gateway in one route table and associated the public subnet. | [View screenshot](screenshots/VPC-1-routetable-igw.png) |
| 2 | Created a custom route table with a default route to the NAT Gateway and associated the private subnet. | [View screenshot](screenshots/VPC-1-routetable-nat.png) |
| 3 | Created and configured the NAT Gateway in the public subnet. | [View screenshot](screenshots/Natgateway.png) |
| 4 | Tested connectivity to the private EC2 instance via SSH, verified network connectivity using ping where permitted, and confirmed outbound internet access through the NAT Gateway. | [View screenshot](screenshots/natgateway-testing.png) |
| 5 | Established a VPC Peering connection between the requester and accepter VPCs. | [View screenshot](screenshots/vpc-peering-connection.png) |
| 6 | Added a route to the second VPC's CIDR block in the first VPC's route table, targeting the VPC Peering connection. | [View screenshot](screenshots/VPC1-peering-routetable.png) |
| 7 | Added a route to the first VPC's CIDR block in the second VPC's route table, targeting the same VPC Peering connection. | [View screenshot](screenshots/VPC2-peering-routetable.png) |
| 8 | Tested private connectivity between EC2 instances in the two VPCs using their private IP addresses. | [View screenshot](screenshots/peering-connection-testing.png) |


<br>

## CONCLUSION
<br>
This project demonstrated how to configure AWS VPC networking using public and private subnets, an Internet Gateway, a NAT Gateway, and VPC Peering. Outbound internet connectivity for private EC2 instances and private communication between two VPCs were tested through appropriate routing and security configurations. The project provided practical experience in AWS networking, traffic routing, and secure communication between cloud resources.





