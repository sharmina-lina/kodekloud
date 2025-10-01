# Task 35 of Terraform

## Task Overview
For this task, create an AWS VPC using Terraform with the following requirements:

The VPC name datacenter-vpc should be stored in a variable named KKE_vpc.

The VPC should have a CIDR block of 10.0.0.0/16.

## Task Implementation
Created variables.tf with the value of vpc name and main.tf for the resource VPC

variable.tf
```terraform
variable "KKE_vpc" {
  description = "Name of the VPC"
  type        = string
  default     = "datacenter-vpc"
}

```
main.tf
``` terraform
resource "aws_vpc" "main" {
  cidr_block       = "10.0.0.0/16"
  

  tags = {
    Name = "var.KKE_vpc"
  }
}
```

Then run
```bash
Terraform init
Terraform plan
terraform apply
```
