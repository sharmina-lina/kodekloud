# Task 36 of Terraform

## Task Overview
For this task is to create an AWS Security Group using Terraform with the following requirements:
The Security Group name devops-sg should be stored in a variable named KKE_sg.
## Task Implemntation
1. Create two file variables.tf and main.tf

variables.tf 
```terraform
variable "KKE_sg" {
  description = "Name of the Security Group"
  type        = string
  default     = "datacenter-sg"
}
```

main.tf
```terraform
resource "aws_security_group" "datacenter_sg" {
  name        = var.KKE_sg
  description = "Security group for Datacenter"
  

  tags = {
    Name = var.KKE_sg
  }
}

```