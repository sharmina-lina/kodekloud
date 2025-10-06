# Task 39 of terraform

## Task overview
create an AWS IAM role using Terraform with the following requirements:

The IAM role name iamrole_anita should be stored in a variable named KKE_iamrole.


## Task implemntation
variables.tf
```terraform
variable "KKE_iamrole" {
  description = "IAM role name"
  type        = string
  default     = "iamrole_anita"
}
```

main.tf
```terraform 
resource "aws_iam_role" "KKE_role" {
  name = var.KKE_iamrole

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action = "sts:AssumeRole"
        Effect = "Allow"
        Principal = {
          Service = "ec2.amazonaws.com"
        }
      }
    ]
  })
}
```