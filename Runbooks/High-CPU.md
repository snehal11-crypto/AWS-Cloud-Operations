# High CPU Runbook

## Issue

EC2 instance is experiencing high CPU utilization.

High CPU can cause:

- Application slowness
- Increased response time
- Service interruption
- Instance performance degradation

---

## Detection

High CPU utilization is detected through Amazon CloudWatch.

Flow:

CloudWatch Alarm
       ↓
High CPU detected
       ↓
Connect to EC2
       ↓
Check processes
       ↓
Identify process
       ↓
Check application logs
       ↓
Take corrective action
       ↓
Monitor CPU

Example CloudWatch alarm:

- Metric: CPUUtilization
- Condition: CPU utilization >= 80%
- Period: 5 minutes

---

## Investigation

### Step 1 — Connect to the EC2 instance

Connect to the affected EC2 instance using SSH or AWS Systems Manager Session Manager.

Example:

```bash
ssh -i /home/admin123/Downloads/keypair-new.pem ec2-user@51.20.135.56
