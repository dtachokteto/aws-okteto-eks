# Okteto Terraform EKS installer

#### This Terraform project creates a custom VPC with public and private subnets, an EKS cluster with a network interface in the public subnet, and two EKS node groups in the public and private subnets. IAM roles are created for the EKS cluster and node groups, and the necessary policies are attached to them. Additionally, 


![alt text](Diagram.jpeg)


## Prerequisites
Before you can run this project, you must have the following tools installed:

- Terraform v1.2 or higher
- AWS CLI v2 or higher
- A Domain name in 


You must also have AWS credentials set up on your local machine. <br>

## Getting Started
Follow these steps to get started with this Terraform project:aws sts get-caller-identity


1. Clone the repository
1. Navigate to the project directory
1. cd eks_managed_node_group edit variables.tf under change "region" to the region you would like to deploy
1. Run `terraform init` `terraform plan` to initialize the project and validate configuration
1. Run `terraform apply` to create the resources in AWS
1. Wait for the terraform apply command to finish executing
1. Run `aws sts get-caller-identity`
1. Run `aws eks update-kubeconfig --region `region-code` --name okteto-environments` (where region-code is the region of your VPC)
1. Test `kubectl get svc`

### you now have an enterprise EKS Cluster complete with the minimum requirements for Okteto 
1. New Okteto Development VPC
1. All IAM roles and policies for creating and running an EKS cluster
1. Node Group and auto-scalling 
    a. Node's with 250GB volumes
    a. Amazon Linux 
    a. instance type 6i.xlarge
    a. S3 Bucket
    a. User for S3 Bucket
1. EKS Cluster named okteto-enviironments running Kubernetes Version 1.25

## Installing Okteto
1. Get the arn from the s3 bucket, create the S3 Policy and attach it to okteto-s3 user. 

# Project Details

1. Source module Repository https://github.com/orgs/terraform-aws-modules/repositories 
1. terraform-aws-eks repository is inserted in the eks_managed_node_group for easy upgrading

## Clean Up
To destroy the resources created by this Terraform project, run `terraform destroy`. This will remove the VPC, subnets, security groups, EC2 bast , EKS cluster

## Future update
- Terraform the s3 policy to s3 user group.  
- Create new diagram
- Change the name of the S3 bucket
- Add Domain and certificate from AWS

