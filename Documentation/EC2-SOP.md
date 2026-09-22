# EC2 Standard Operating Procedure (SOP)

## 1. Purpose

This document defines the standard procedure for checking,
monitoring, and troubleshooting Amazon EC2 instances.

The objective is to maintain EC2 availability, identify common
issues, and provide a consistent troubleshooting process.

---

## 2. EC2 Instance Inventory

Use the following AWS CLI command to list EC2 instances:

```bash
aws ec2 describe-instances \
--query 'Reservations[].Instances[].[InstanceId,State.Name,InstanceType,PrivateIpAddress]' \
--output table
