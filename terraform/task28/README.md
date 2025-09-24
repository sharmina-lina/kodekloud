# Task 28 of Terraform

## Enabling versioning of S3 backet using terraform. S3 Bucket is already created now we need to enable versioning of S3 Bucket

## Task Implementation

1. To add versioning i need to add below block in terraform main.tf file where s3_ran_bucket is the name of S3 bucket

``` bash
resource "aws_s3_bucket_versioning" "s3_bucket_versioning" {
  bucket = aws_s3_bucket.s3_ran_bucket.id

  versioning_configuration {
    status = "Enabled"}}
```
This block enabled versioning of S3