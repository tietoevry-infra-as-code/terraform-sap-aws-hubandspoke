# terraform-sap-aws-hubandspoke
Terraform repository for sap on aws Infra as a Code 
Architecture
A Transit Gateway relies on Route Tables. By default, a new Route Table is created in the Transit Gateway, which populates with the routing info toward every VPC attached to the gateway (the full mesh scenario) The Terraform code in this project demonstrates a more complex scenario in which traffic is isolated based on the environment. Four VPCs are created, with two subnets each (in separate AZs):

VPC-1: in the 'dev' environment
VPC-2: in the 'dev' environment
VPC-3: in the 'shared' environment
VPC-4: in the 'prod' environment
Let's assume the 'shared' environment will host shared components, such as proxy services, tools, ... Here are the rules we want our Transit Gateway to implement:

The shared VPC can access dev and prod VPCs.
The dev VPCs can access each other, and the shared VPC
The prod VPCs can only access the shared VPC
To enable such a scenario, three Route Tables are created in the Transit Gateway, one per environment. Which means both dev VPCs attach to the same Route Table, whereas the shared and prod VPCs each attach to their respective Route Table. Each VPC gets a t2.micro Ubuntu instance to validate the network connectivity over ssh and ICMP (ping). The instance in the 'shared' is assigned a public IP so a VPN connection isn't needed. Adding the necessary Terraform resources to establish a VPN connection could be an extension of this project.

transit-gateway-architecture

The thick green links on the diagram represents the authorized traffic through the gateway.

Prerequisites
An AWS account
Terraform
Usage
Change ACCESS_KEY and SECRET_KEY values in Variables.tf
Change the public_key value to a keypair you own
Deploy the setup with:
$ terraform init
$ terraform plan
$ terraform apply
