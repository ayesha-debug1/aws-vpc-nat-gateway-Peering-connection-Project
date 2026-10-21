# aws-vpc-nat-Gateway-Peering-connection-Project



## Project Overview

This project demonstrates how to design and configure a secure AWS network using Amazon VPC, public and private subnets, an Internet Gateway, a NAT Gateway, and Peering connection.

The objective is to provide outbound internet connectivity to private application resources while enabling private communication between multiple VPCs.
<br>
<br>
## Business Problem

An organization operates application workloads and shared services in separate VPCs. Application instances need outbound internet access for software updates and external APIs, but they should not be directly exposed to the public internet.

<br>
<br>

## Proposed Solution

Configure a NAT Gateway in VPC-A to provide outbound internet access to its private EC2 instance. Establish VPC Peering between VPC-A and VPC-B, configure routing in both VPCs, and apply appropriate security rules to enable communication between resources.

<br>
<br>

## Architecture

                         Internet
                            |
                            v
                   Internet Gateway
                            |
                            v
                 +----------------------+
                 |        VPC-A         |
                 |     10.10.0.0/16     |
                 |                      |
                 |  Public Subnet       |
                 |  10.10.1.0/24        |
                 |       |              |
                 |       v              |
                 |   NAT Gateway        |
                 |       ^              |
                 |       |              |
                 |  Private Subnet      |
                 |  10.10.2.0/24        |
                 |       |              |
                 |       v              |
                 |  Application EC2     |
                 +----------+-----------+
                            |
                            | VPC Peering
                            |
                 +----------+-----------+
                 |        VPC-B         |
                 |     10.20.0.0/16     |
                 |                      |
                 |  Public Subnet      |
                 |  10.20.2.0/24        |
                 |       |              |
                 |       v              |
                 |  Shared Service EC2  |
                 +----------------------+

## Technologies

- Amazon VPC
- Public and private subnets
- Internet Gateway
- NAT Gateway
- Route tables
- Amazon EC2
- Security groups
- GitHub and Markdown documentation
  
<br>

 ## References

1. [Amazon VPC Peering](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html) — Connecting two VPCs using private IP addresses.
2. [NAT Gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) — Providing outbound internet access to instances in private subnets.
3. [VPC Route Tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html) — Configuring routes for internet access, NAT Gateway, and VPC Peering.


