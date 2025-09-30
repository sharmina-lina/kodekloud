# Task 34 of Terraform

## Task Overview
Terraform – Upload File to Existing S3 Bucket
This Terraform configuration creates an **S3 bucket** (if not already created) and uploads a local file (`/tmp/xfusion.txt`) to that bucket.

## Task implementation
Add below resource block to upload life in S3 bucket
```bash
resource "aws_s3_object" "xfusion_file" {
  bucket = aws_s3_bucket.my_bucket.id
  key    = "xfusion.txt"          # name of the object in S3
  source = "/tmp/xfusion.txt"     # local file path
  etag   = filemd5("/tmp/xfusion.txt")}
```
