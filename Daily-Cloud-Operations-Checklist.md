# Daily AWS Operations Checklist

## Purpose

This checklist is used by Cloud Operations engineers to perform
daily health and operational checks on AWS infrastructure.

---

## 1. EC2 Health

- [ ] Check EC2 instance state
- [ ] Check EC2 status checks
- [ ] Check for stopped or terminated instances
- [ ] Check important production instances

Command:

```bash
aws ec2 describe-instances \
--query 'Reservations[].Instances[].[InstanceId,State.Name,InstanceType]' \
--output table
