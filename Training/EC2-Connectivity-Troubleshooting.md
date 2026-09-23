# Technical Mentorship — EC2 Connectivity Troubleshooting

## Scenario

Junior Engineer:

> "How do I troubleshoot an EC2 connectivity issue?"

Senior Cloud Operations Engineer:

Instead of immediately changing configurations, follow the troubleshooting process step by step.

The objective is to identify where connectivity is failing.

---

# Troubleshooting Flow

First check instance state
        ↓
Check status checks
        ↓
Check Security Group
        ↓
Check NACL
        ↓
Check route table
        ↓
Check network gateway
        ↓
Check OS
        ↓
Check application

---

## Step 1 — Check Instance State

First confirm that the EC2 instance is running.

AWS CLI:

```bash
aws ec2 describe-instances \
--instance-ids <INSTANCE_ID> \
--query 'Reservations[].Instances[].State.Name'
