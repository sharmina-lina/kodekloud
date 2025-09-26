# Terraform Task 29

## Task Overview
Copy S3 bucket content to a local directory and delete the s3 backet.
All these using Terraform. S3 bucket name and othe rinformation provided.

## Task Implementation


Data source to reference the existing bucket

``` bash
data "aws_s3_bucket" "devops_bucket" {
  bucket = "devops-bck-5974"}
  ```

Copy S3 bucket contents locally using local-exec
```
resource "null_resource" "s3_backup" {
  provisioner "local-exec" {
    command = "mkdir -p /opt/s3-backup && aws s3 cp s3://${data.aws_s3_bucket.devops_bucket.id} /opt/s3-backup/ --recursive"
  }
}

```

Delete the bucket AFTER backup
```
resource "aws_s3_bucket" "devops_bucket_delete" {
  bucket = data.aws_s3_bucket.devops_bucket.id
  force_destroy = true   # ensures bucket and all objects are deleted
}
```


Ensure deletion happens after backup
```
resource "null_resource" "delete_depends_on" {
  depends_on = [null_resource.s3_backup, aws_s3_bucket.devops_bucket_delete]
}

```