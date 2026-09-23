# Incident Record — INC-001

## Incident ID

INC-001

## Date

2026-09-23

## Severity

Medium

## Service

EC2

## Problem

CPU utilization reached 95%.

## Impact

Application response was slow.

## Detection

CloudWatch Alarm detected high CPU utilization.

## Investigation

1. Checked CloudWatch CPUUtilization metrics.
2. Connected to the affected EC2 instance.
3. Checked running processes using the `top` command.
4. Identified the process consuming excessive CPU.
5. Checked application logs for related errors.

## Root Cause

A high CPU-consuming process caused CPU utilization to increase to 95%.

## Resolution

Restarted the affected application process.

After restarting the process, CPU utilization decreased and application performance returned to normal.

## Verification

1. Checked CPU utilization using CloudWatch.
2. Verified CPU usage decreased.
3. Checked application status.
4. Tested application response.
5. Confirmed CloudWatch alarm returned to OK.

## Preventive Action

- Improved CloudWatch monitoring.
- Reviewed CPU alarm threshold.
- Added appropriate alerting.
- Regularly monitor CPU utilization.
- Review high CPU incidents for recurring patterns.

## Incident Flow

CloudWatch Alarm
       ↓
High CPU Detected
       ↓
Connect to EC2
       ↓
Check CPU
       ↓
Run `top`
       ↓
Identify Process
       ↓
Check Application Logs
       ↓
Restart Application Process
       ↓
Monitor CPU
       ↓
Verify Application
       ↓
Incident Resolved

## Status

Resolved
