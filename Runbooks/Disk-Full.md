# Disk Full Runbook

## Problem

Disk usage is greater than 90%.

High disk utilization can cause:

- Application failures
- Unable to write logs
- Database errors
- Service interruptions
- System instability

---

## Detection

Disk usage can be detected using CloudWatch monitoring or by checking the EC2 instance manually.

Example:

```bash
df -h
