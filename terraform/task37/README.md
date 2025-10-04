# Task 37 of Terraform

## Task Overview
For this task, create an AWS Elastic IP using Terraform with the following requirement:
The Elastic IP name devops-eip should be stored in a variable named KKE_eip. The Terraform working directory is /home/bob/terraform.

## Task Implementation
Create two file variables.tf and main.tf
variables.tf 
```terraform 
variable KKE_eip {
    description = "Elastic IP name"
    type        = string
     default    = "devops-eip"
}
```
main.tf
```terraform 
resource "aws_eip" "devops_eip" {
      #vpc = true # Set to true if you want to allocate the EIP in a VPC
      tags = {
        Name = var.KKE_eip
      }
    }
```