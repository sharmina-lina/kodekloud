# Task 27 of Terraform

## Task Overview
In this task, IAM policy and IAM user is created using Terraform, My task is to atatche the created IAM policy to the mentioned IAM user using Terraform block.

## Task Implementation
I have used the below terraform block to attach policy with user

``` bash
resource "aws_iam_user_policy_attachment" "iam_user_policy_attachment" {
  user       = aws_iam_user.user.name
  policy_arn = aws_iam_policy.policy.arn}
```

This is all about the task
Thank you!