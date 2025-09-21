# Task 26 

## Task Overview
Attach the elastic-ip from the instance  datacenter-ec2-eip to the datacenter-ec2 instance using Terraform only.

## Task details

### Step 1:
Open the main.tf
Add this below blok to Associate Elastic IP with EC2 instance

```
resource "aws_eip_association" "ec2_eip_assoc" {
  instance_id   = aws_instance.ec2.id
  allocation_id = aws_eip.ec2_eip.allocation_id
} 
```

### Step 2:
Apply all the command

```terraform init
terraform plan
terraform apply
```

