# Task 38 of terraform

## Task overview
User variable sestup using terraform

## Task Implemntation
variables.tf 
```terraform
variable KKE_user {
    description = "IAM user name"
    type        = string
    default     = "iamuser_jim"  
}
```
main.tf
```terraform
resource "aws_iam_user" "iamuser_jim" {
  name = var.KKE_user
  
}
```