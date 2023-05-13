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
2. Navigate to the project directory
3. cd eks_managed_node_group edit main.tf under locals change "region" to the region you would like to deploy
4. Run `terraform init` `terraform plan` to initialize the project and validate configuration
5. Run `terraform apply` to create the resources in AWS
6. Wait for the terraform apply command to finish executing
7. Run `aws sts get-caller-identity`
8. Run `aws eks update-kubeconfig --region `region-code` --name okteto-environments` (where region-code is the region of your VPC)
9. Test `kubectl get svc`

### you now have an enterprise EKS Cluster complete with the minimum requirements for Okteto 
1. New Okteto Development VPC
1. All IAM roles and policies for creating and running an EKS cluster
1. Node Group and auto-scalling 
    a. Node's with 250GB volumes
    a. Amazon Linux 
    a. instance type 6i.xlarge
1. EKS Cluster named okteto-enviironments running Kubernetes Version 1.25

## Installing Okteto
1. 



# Project Details

## VPC

The VPC is created using the `vpc` Terraform module, which sets up a custom VPC with two public subnets and two private subnets. the subnets are associated with a routing table that routes traffic to the Internet Gateway for the public subnets and the NAT Gateway for the private subnets.

## EKS Cluster

The EKS cluster is created using the `aws_eks_cluster` Terraform resource and includes a network interface in the public subnet. The IAM role for the EKS cluster is created using the iam Terraform module, and the necessary policies are attached to the role using the iam_policy_attachment resource.

## EKS Node Groups

Two EKS node groups are created, one in the public subnet and one in the private subnet. The node groups are created using the `eks_node_group` Terraform resource, and the necessary IAM roles are created using the `aws_iam_role` role  and attached to the node groups using the `aws_iam_role_policy_attachment` resource.

## Further Steps

To further customize the project, you can modify the input variables in variables.tf. You can also modify the resources in the respective modules, such as bastion.tf and eks_cluster.tf, to change the configuration of the EC2 bastion host, EKS cluster, and node groups. You can also add more resources to the project as needed.

## Clean Up
To destroy the resources created by this Terraform project, run `terraform destroy`. This will remove the VPC, subnets, security groups, EC2 bast , EKS cluster

## Future update
- Change to the vpc-module.tf `azs` to a variable filled by the variables.tf

