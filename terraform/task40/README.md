# Task 40 of Terraform
## Task overview
create an AWS IAM policy using Terraform with the following requirements:
The IAM policy name iampolicy_javed should be stored in a variable named KKE_iampolicy.

## Task Implementation
variables.tf
```terraform
variable KKE_iampolicy {
    description = "IAM policy name"
    type = string
    default = "iampolicy_javed"
}
```
main.tf
```terraform 
resource "aws_iam_policy" "policy" {
  name        = var.KKE_iampolicy
  path        = "/"
  description = "My test policy"

  # Terraform's "jsonencode" function converts a
  # Terraform expression result to valid JSON syntax.
  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action = [
          "ec2:Describe*",
        ]
        Effect   = "Allow"
        Resource = "*"
      },
    ]
  })
}
```
