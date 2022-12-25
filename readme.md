# Multiple AWS Region Build 
This repo builds dual VPCs in multiple AWS regions using Terraform workspaces and multiple .tf scripts.

## Overview
I am using bash scripts to build multiple terraform regions and switch between them during apply and destroy. The terraform state is stored separately 
within these workspaces. I am also using provider aliasing, as  you cannot loop through multiple providers within a single call of the vpc module. 
   
The functionality realized by these script sets is as follows: 
*  Create (2) VPCs in each of 4 AWS regions. Each VPC contains the follwoing:  
    * Two subnets (public, private with NATGW routes)
    * NAT gateway for private subnet to Internet 
    * IGW for public subnet to Internet
    * EIP associated with IGW
    * Routing tables and assocations for VPC
   
## Prerequisites
There are a a few steps to set up the environment: 
* Log in to your AWS environment and launch a CloudShell terminal window. 
* Clone repo to CloudShell, git is already installed. 
* Run *setup.sh*; this will install Terraform and a couple of other useful tools. 

*  To build multi-vpc in multi-regsion, run *create_vpcs_multiple_regions.sh*
*  To destroy everything built above, run *destroy_vpcs_multiple_regions.sh*

## Notes & Caveats 
*  The scripts are tagging all of the resources so you can track the creation and destruction in the AWS console or via other methods. The tags are specified in the provider.tf file
*  I filed one bug on the AWS module that you may encounter intermittently when running the create or destroy scripts. Rerunning the script typically works around this bug in my environment.  [https://github.com/hashicorp/terraform-provider-aws/issues/28364]
==============

