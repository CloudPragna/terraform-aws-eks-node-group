# Terraform IAC for AWS EKS node Group

## Prerequisites

- Terraform 0.12.x
- aws cli

## Usage

```hcl
module "examplenodgroup" {
  source            = "git::https://github.com/foss-cafe/terraform-aws-eks-node-group.git"
  create_node_group = true
  cluster_name      = "Example"
  node_group_name   = "testgroup"
  k8s_version       = 1.14
  node_role_arn     = "arn:aws:iam::xxx:role/xxxxeks-node-iam-role"
  scaling_config = {
    "desired_size" = 1
    "max_size"     = 1
    "min_size"     = 1
  }
  subnet_ids = ["subnet-xxxx", "subnet-yyyy", "subnet-zzzz"]
  additional_tags = {
    Environment = "dev"
  }
}

```
<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| terraform | ~> 0.12.24 |
| aws | ~> 2.60 |

## Providers

| Name | Version |
|------|---------|
| aws | ~> 2.60 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| additional\_tags | n/a | `map(string)` | <pre>{<br>  "createdby": "devops"<br>}</pre> | no |
| ami\_type | Type of Amazon Machine Image (AMI) associated with the EKS Node Group. Defaults to AL2\_x86\_64. Valid values: AL2\_x86\_64, AL2\_x86\_64\_GPU. | `string` | `"AL2_x86_64"` | no |
| cluster\_name | Name of the EKS Cluster | `string` | `"example-dev"` | no |
| create\_node\_group | Do you want to create Node Group | `bool` | `true` | no |
| disk\_size | Disk size in GiB for worker nodes. Defaults to 40. Terraform will only perform drift detection if a configuration value is provided | `number` | `40` | no |
| instance\_types | Set of instance types associated with the EKS Node Group. Defaults to ["t3.medium"] | `list` | <pre>[<br>  "t2.medium"<br>]</pre> | no |
| k8s\_version | Kubernetes version. Defaults to EKS Cluster Kubernetes version. Terraform will only perform drift detection if a configuration value is provided. | `string` | `"1.14"` | no |
| labels | Key-value mapping of Kubernetes labels. Only labels that are applied with the EKS API are managed by this argument. | `map(string)` | <pre>{<br>  "node_group": "dev"<br>}</pre> | no |
| node\_group\_name | Name of the Node Group | `string` | `"example"` | no |
| node\_role\_arn | Amazon Resource Name (ARN) of the IAM Role that provides permissions for the EKS Node Group. | `string` | `"arn:aws:iam::xxx:role/xxxxeks-node-iam-role"` | no |
| release\_version | AMI version of the EKS Node Group. Defaults to latest version for Kubernetes version | `string` | `"1.17.9-20200723"` | no |
| remote\_access | Configuration block with remote access settings | `map` | <pre>{<br>  "ec2_ssh_key": null,<br>  "source_security_group_ids": null<br>}</pre> | no |
| scaling\_config | Configuration block with scaling settings | `map(string)` | <pre>{<br>  "desired_size": 1,<br>  "max_size": 1,<br>  "min_size": 1<br>}</pre> | no |
| subnet\_ids | Identifiers of EC2 Subnets to associate with the EKS Node Group. | `list` | <pre>[<br>  "subnet-xxxx",<br>  "subnet-xxxx",<br>  "subnet-xxx"<br>]</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| arn | Amazon Resource Name (ARN) of the EKS Node Group. |
| id | EKS Cluster name and EKS Node Group name separated by a colon |
| resources\_autoscaling\_groups | List of objects containing information about AutoScaling Groups |
| resources\_autoscaling\_groups\_remote\_access\_security\_group\_id | Identifier of the remote access EC2 Security Group |
| status | Status of the EKS Node Group |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
