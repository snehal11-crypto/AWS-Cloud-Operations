# EC2 Knowledge Base

## What is it?

Amazon EC2 (Elastic Compute Cloud) provides resizable virtual servers in AWS.

## Why do we use it?

We use EC2 to run:

- Applications
- Web servers
- Backend services
- Automation scripts
- Development environments

## How do we configure it?

1. Select an AMI.
2. Select an instance type.
3. Configure VPC and subnet.
4. Configure security groups.
5. Configure key pair or Session Manager.
6. Configure storage.
7. Launch the instance.

## How do we troubleshoot it?

Check:

```bash
aws ec2 describe-instances
