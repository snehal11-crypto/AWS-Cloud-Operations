# EC2 Down Runbook

## Problem

EC2 instance is not responding.

---

## Step 1 — Check Instance State

Check whether the EC2 instance is running, stopped, or terminated.

```bash
aws ec2 describe-instances \
--instance-ids <INSTANCE_ID> \
--query 'Reservations[].Instances[].State.Name'
