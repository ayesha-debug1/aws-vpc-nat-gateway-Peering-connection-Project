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


## Testing and results 

1.Added IGW rule to the default route table and associated a subnet, making it a public subnet
2.Created custom route table under same vpc and added nat gateway rule and associated subnet , making it a private subnet
3.created nategateway 
4.tested natgateway connection by ssh to private server, ping and then internet connectivity
5.configured peering connection with the requester and accepter vpc
6.added peering connection rule to route table of vpc 1 with other vpc IP
7.added peering connection rule to the route table of vpc 2 with other VPC ip
8.tested peering connection from one ec2 to another 








