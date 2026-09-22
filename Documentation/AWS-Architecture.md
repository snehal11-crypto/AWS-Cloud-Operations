# AWS Cloud Operations — Architecture Documentation

## 1. Project Overview

This document describes the AWS infrastructure created for the
AWS Cloud Operations practical lab.

The environment demonstrates basic AWS administration,
networking, compute, storage, identity, and monitoring.

AWS services used include:

- Amazon VPC
- Amazon EC2
- Amazon EBS
- AWS IAM
- Amazon S3
- Amazon CloudWatch

## 2. AWS Architecture

```text
                          AWS Account
                              |
                              V
                    aws-admin-lab-vpc
                       10.0.0.0/16
                              |
                ┌─────────────┴─────────────┐
                |                           |
                V                           V
        Public Subnets               Private Subnets
                |                           |
        ┌───────┴───────┐           ┌───────┴───────┐
        |               |           |               |
        V               V           V               V
   Public Subnet 1  Public Subnet 2  Private Subnet 1  Private Subnet 2
   10.0.0.0/20     10.0.16.0/20     10.0.128.0/20   10.0.144.0/20
        |
        V
       EC2
        |
        V
       EBS
        |
        V
   CloudWatch


## 3. VPC Configuration

### 3.1 VPC

| Parameter | Value |
|---|---|
| VPC Name | aws-admin-lab-vpc |
| VPC ID | `vpc-0a9ef23077d6a0d8c`
| CIDR | `10.0.0.0/16` |
| Region | `eu-north-1` |
| DNS Resolution | Enabled |
| DNS Hostnames | Enabled |

### 3.2 Subnets

| Subnet | Subnet ID | CIDR | Type | Availability Zone |
|---|---|---|---|---|
| Public Subnet | `subnet-098952d0759626a8e` | `10.0.0.0/20` | Public | `eun1-az1 (eu-north-1a)` |
| Private Subnet | `subnet-095ec5022e275b717` | `10.0.128.0/20` | Private | `eun1-az1 (eu-north-1a)` |

### 3.3 Route Tables

#### Public Route Table

| Destination | Target |
|---|---|
| `10.0.0.0/16` | local |
| `0.0.0.0/0` | Internet Gateway |

The public route table provides a route from the public subnet
to the Internet Gateway.

#### Private Route Table

| Destination | Target |
|---|---|
| `10.0.0.0/16` | local |
| `pl-c3aa4faa` | VPC Endpoint (`vpce-065d56f9876768e75`) |

The private route table does not have a NAT Gateway route.
A VPC Endpoint is configured for private access to the required AWS service.

### 3.4 Internet Gateway

| Parameter | Value |
|---|---|
| Name | `aws-admin-lab-igw` |
| Internet Gateway ID | `igw-025ad60424140d9e5` |
| Attached VPC | `aws-admin-lab-vpc` |

The Internet Gateway provides internet connectivity for resources
in the public subnet.

### 3.5 NAT Gateway

NAT Gateway was not configured in the current lab environment.

No NAT Gateway was created for the private subnets.

The public subnet uses the Internet Gateway for internet connectivity.
The private subnets do not have a NAT Gateway configured.


---

# Step 4 — Document EC2

Now add:

```markdown
## 4. EC2 Configuration

### 4.1 EC2 Instance


| Parameter | Value |
|---|---|
| Instance Name | `aws-admin-lab-ec2` |
| Instance ID | `i-0dc665a5b85c5793b` |
| Instance Type | `t3.micro` |
| Operating System | `Amazon Linux 2023` |
| Region | `eu-north-1` (Europe/Stockholm) |
| Availability Zone | `eu-north-1a` |
| Private IP | `10.0.10.4` |
| Public IP | `51.20.135.56` |
| VPC | `aws-admin-lab-vpc` |
| VPC ID | `vpc-0a9ef23077d6a0d8c` |
| Subnet | `aws-admin-lab-subnet-public1-eu-north-1a` |
| Subnet ID | `subnet-098952d0759626a8e` |
| Security Group Name | `aws-admin-lab-sg1` |
| Security Group ID | `sg-0f41a0d1dc886178f` 
| IAM Role | `AWSAdminLabEC2Role` |
| Key Pair | `keypair-new` |
| Instance State | `Running` |
| Monitoring | `Disabled` |
| IMDSv2 | `Required` |

### 4.2 Attached EBS Volume


| Parameter | Value |
|---|---|
| Volume ID | `vol-00d75f532bc3740ac` |
| Device | `/dev/xvda` |
| Volume Type | `gp3` |
| Size | `8 GiB` |
| Encryption | `No` |

The EBS volume `vol-00d75f532bc3740ac` is attached to the EC2
instance `aws-admin-lab-ec2` as the root device `/dev/xvda`.
It is an 8 GiB `gp3` volume and is currently in use.
The volume is not encrypted.

# 5. Monitoring and Alerting

Amazon CloudWatch is used to monitor the EC2 instance and its
infrastructure metrics in the AWS Admin Lab.

## 5.1 CloudWatch Metrics

The EC2 instance is monitored using Amazon CloudWatch.

The following metrics are available:

- CPUUtilization
- NetworkIn
- NetworkOut

### 5.5 Notification Mechanism

SNS notification was not configured in the current lab environment.

CloudWatch alarms can be integrated with Amazon SNS in a production
environment to send notifications when monitoring thresholds are
breached.


- StatusCheckFailed

These metrics can be used to monitor the health and performance
of the EC2 instance.

## 5.2 CloudWatch Alarm

No CloudWatch alarm was configured in the current lab environment.

CloudWatch alarms can be configured in the future to monitor
metrics such as CPUUtilization and trigger notifications when
defined thresholds are exceeded.

## 5.3 CloudWatch Log Groups

No custom CloudWatch Log Group was configured in the current
lab environment.

## 5.4 Metric Filter

No custom CloudWatch metric filter was configured in the current
lab environment.

---

# 6. Operational Responsibilities

The AWS Cloud Operations activities demonstrated in this lab include:

- AWS infrastructure administration
- VPC and subnet management
- Route table management
- Internet Gateway management
- EC2 administration
- EBS volume management
- IAM administration
- S3 administration
- CloudWatch monitoring
- Infrastructure health monitoring
- Incident troubleshooting
- Operational automation
- AWS CLI and shell scripting
- Documentation management
- Runbook maintenance

# 7. Architecture Validation

The AWS environment was validated to confirm that the configured
infrastructure components are working as expected.

## 7.1 Network Validation

The following network checks were performed:

- Verified that the `aws-admin-lab-vpc` VPC exists.
- Verified the VPC CIDR as `10.0.0.0/16`.
- Verified the configured public and private subnets.
- Verified subnet CIDR ranges and Availability Zones.
- Verified public route table associations.
- Verified private route table associations.
- Verified that the Internet Gateway is attached to the VPC.
- Verified the public route `0.0.0.0/0` points to the Internet Gateway.
- Verified that no NAT Gateway is configured in the current lab.
- Verified the configured VPC Endpoint in the private route tables.
- Verified security group association with the EC2 instance.

## 7.2 EC2 Validation

The following EC2 checks were performed:

- Verified that the `aws-admin-lab-ec2` instance is in the `Running` state.
- Verified the EC2 instance type as `t3.micro`.
- Verified the private IP address.
- Verified the public IP address.
- Verified that the EC2 instance is deployed in the public subnet.
- Verified the VPC association.
- Verified the subnet association.
- Verified the security group association.
- Verified the attached EBS volume.
- Verified that the EBS root volume is attached as `/dev/xvda`.
- Verified EC2 connectivity using EC2 Instance Connect.

## 7.3 EBS Validation

The following EBS checks were performed:

- Verified that the EBS volume is attached to the EC2 instance.
- Verified the volume ID.
- Verified the volume type as `gp3`.
- Verified the volume size as `8 GiB`.
- Verified the device name as `/dev/xvda`.
- Verified that the volume is in the `in-use` state.

## 7.4 IAM Validation

The following IAM checks were performed:

- Verified that an IAM role is attached to the EC2 instance.
- Verified that the EC2 instance uses an IAM role instead of storing
  AWS access keys on the server.
- Verified that the required permissions are provided through the
  IAM role.

## 7.5 CloudWatch Validation

The following CloudWatch checks were performed:

- Verified that CloudWatch metrics are available for the EC2 instance.
- Verified `CPUUtilization`.
- Verified `NetworkIn`.
- Verified `NetworkOut`.
- Verified `StatusCheckFailed`.

The following CloudWatch components were not configured in the
current lab environment:

- Custom CloudWatch alarm
- Custom CloudWatch Log Group
- Metric Filter
- SNS notification

## 7.6 NAT Gateway Validation

```text
NAT Gateway: Not configured in the current lab environment.
