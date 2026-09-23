# Change Record

## Change ID

CHG-001

## Date

2026-09-23

## Change

Added CloudWatch CPU alarm for EC2 instance.

## Reason

To monitor EC2 CPU utilization and detect high CPU usage.

## Before

No CPU alarm was configured for the EC2 instance.

## After

CloudWatch CPU alarm was configured.

Condition:

CPU utilization > 80%

The alarm changes to ALARM when CPU utilization remains above the configured threshold.

## Implementation

1. Opened AWS CloudWatch.
2. Selected the EC2 CPUUtilization metric.
3. Created a CloudWatch alarm.
4. Configured the CPU threshold to 80%.
5. Configured the evaluation period.
6. Configured SNS notification if required.
7. Saved the alarm.

## Validation

Generated CPU load on the EC2 instance.

Example:

```bash
top
