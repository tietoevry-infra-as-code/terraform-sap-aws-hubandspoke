# AWS VPC with Transit Gateway Hub & Spoke Model

## Prerequisites
* An AWS account
* Terraform

## Usage
* Change ACCESS_KEY and SECRET_KEY values in Variables.tf
* Change the public_key value to a keypair you own
* Deploy the setup with:

``` 
$ terraform init
$ terraform plan
$ terraform apply
```


## VPC Connectivity

* The shared VPC can access dev and prod VPCs
* The dev VPCs can access each other and the shared VPC
* The prod VPCs can only access the shared VPC
