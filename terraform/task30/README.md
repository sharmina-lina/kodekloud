# Task 30 of Terraform

## Task Overview
Delete the ec2 instance region using terraform. Make sure to keep the provisioning code, as we might need to provision this instance again later and make sure instance is in terminated state.

## Task Implementation
filters "Name=tag:Name,Values=datacenter-ec2"