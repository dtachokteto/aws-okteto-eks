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
1. Get the arn from the s3 bucket, create the S3 Policy and attach it to okteto-s3 user. The arn should also be in the terraform output
1. change directory to the root of the repository and folder s3-policy-json (`cd ../s3-policy-json`)
1. edit the s3-user-policy.json file with your bucket name 
1. Run `aws iam create-policy --policy-name okteto-user-s3 --policy-document file://s3-user-policy.json`
1. to attach the policy to the okteto-s3 user get the policy Arn from the output and run: `aws-okteto-eks % aws iam attach-user-policy --policy-arn <instert policy arn> --user-name okteto-s3`
1. change directory to the root of the repository and folder okteto-helm (`cd ../okteto-helm`)
1. edit config.yaml with your License key, subdomain, and Cluster Endpoint. save
1. 

# Project Details

1. Source module Repository https://github.com/orgs/terraform-aws-modules/repositories 
1. terraform-aws-eks repository is inserted in the eks_managed_node_group for easy upgrading

## Clean Up
1. To destroy the resources created by this Terraform project, run `terraform destroy`. This will remove the VPC, subnets, security groups, EC2 bast , EKS cluster
1. aws iam delete-policy --policy-arn arn:aws:iam::0123456789101:policy/okteto-user-s

## Future update
- Terraform the s3 policy to s3 user group.  
- Create new diagram
- Change the name of the S3 bucket
- Add Domain and certificate from AWS

