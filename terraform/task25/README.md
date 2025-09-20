# Terraform Task

## Task Description

Change the instance type from t2.micro to t2.nano for nautilus-ec2 instance using terraform.

Make sure the EC2 instance nautilus-ec2 is in running state after the change.

## Steps Performed

1. Open the main.tf and change the instance type:
    ```
    instance_type = "t2.nano"
    ```
    
2. add the local exec block
```
provisioner "local-exec" {
    command = "aws ec2 wait instance-running --instance-ids ${self.id}"
  }

  ```