# CloudWatch Standard Operating Procedure (SOP)

## 1. Purpose

This document defines the standard procedure for monitoring
AWS resources and applications using Amazon CloudWatch.

The objective is to monitor system health, identify issues,
create alarms, and notify the operations team when thresholds
are exceeded.

---

## 2. CloudWatch Monitoring Flow

EC2
 ↓
CloudWatch
 ↓
Metrics
 ↓
Alarm
 ↓
Notification

CloudWatch collects metrics from AWS resources such as EC2
instances and evaluates these metrics against configured
alarm thresholds.

---

## 3. Metrics to Monitor

The following metrics should be monitored:

### CPUUtilization

Monitors the percentage of CPU utilization of an EC2 instance.

Example:

CPUUtilization > 80%
        ↓
CloudWatch Alarm
        ↓
SNS
        ↓
Operations Team

---

### StatusCheckFailed

Monitors EC2 instance status checks.

A failure may indicate an instance or system-level problem.

---

### NetworkIn

Monitors the amount of network traffic received by the EC2
instance.

---

### NetworkOut

Monitors the amount of network traffic sent by the EC2
instance.

---

### Disk Usage

Disk usage can be monitored using CloudWatch Agent and
custom metrics.

Example:

Disk Usage > 80%
        ↓
CloudWatch Alarm
        ↓
SNS
        ↓
Operations Team

---

### Application Errors

Application logs can be sent to CloudWatch Logs.

Example:

Application Log
      ↓
CloudWatch Logs
      ↓
Metric Filter
      ↓
ApplicationErrors Metric
      ↓
CloudWatch Alarm
      ↓
SNS Notification

---

## 4. Example CPU Alarm

Example alarm configuration:

Metric:
CPUUtilization

Condition:
CPUUtilization > 80%

Period:
5 minutes

Evaluation:
1 consecutive period

Action:
SNS notification

Flow:

CPU > 80%
     ↓
CloudWatch Alarm
     ↓
SNS
     ↓
Operations Team

---

## 5. CloudWatch Alarm States

CloudWatch alarms can have the following states:

OK:
The metric is within the configured threshold.

ALARM:
The configured threshold has been breached.

INSUFFICIENT_DATA:
CloudWatch does not have enough data to determine the alarm state.

---

## 6. CloudWatch Monitoring Procedure

### Step 1

Open the AWS Console.

Navigate to:

CloudWatch → Metrics

Select:

EC2 → Per-Instance Metrics

---

### Step 2

Select the required EC2 instance.

Check:

- CPUUtilization
- StatusCheckFailed
- NetworkIn
- NetworkOut

---

### Step 3

Review the metric graphs.

Check whether the metric is:

- Normal
- Increasing
- Decreasing
- Consistently above the expected threshold

---

### Step 4

Create a CloudWatch alarm when monitoring requires
automatic notification.

Example:

CPUUtilization > 80%

---

### Step 5

Configure the alarm action.

Use an SNS topic for notification.

Flow:

CloudWatch Alarm
      ↓
SNS Topic
      ↓
Email Notification
      ↓
Operations Team

---

## 7. Application Error Monitoring

Application errors can be monitored using CloudWatch Logs
and metric filters.

Example:

Application Log
      ↓
CloudWatch Logs
      ↓
Metric Filter: ERROR
      ↓
ApplicationErrors
      ↓
CloudWatch Alarm
      ↓
SNS

Example metric:

Namespace:
MyApplication

Metric:
ApplicationErrors

Statistic:
Sum

Period:
5 minutes

Threshold:
ApplicationErrors >= 5

---

## 8. CloudWatch Dashboard

A CloudWatch dashboard can be used to display important
monitoring metrics in one place.

Recommended widgets:

- CPUUtilization
- StatusCheckFailed
- NetworkIn
- NetworkOut
- ApplicationErrors

Example:

CloudWatch Dashboard
        ↓
EC2 Metrics
        ↓
Application Metrics
        ↓
Alarm Status

---

## 9. Troubleshooting Procedure

If a CloudWatch alarm enters the ALARM state:

1. Identify the affected resource.
2. Check the metric that triggered the alarm.
3. Check the time of the event.
4. Check EC2 status checks.
5. Check CPU utilization.
6. Check network traffic.
7. Check disk usage.
8. Check application logs.
9. Identify the root cause.
10. Take corrective action.
11. Verify that the metric returns to normal.
12. Confirm the alarm returns to OK.

---

## 10. CloudWatch CLI Checks

List CloudWatch alarms:

aws cloudwatch describe-alarms \
--region ap-south-1

List only alarm names and states:

aws cloudwatch describe-alarms \
--region ap-south-1 \
--query 'MetricAlarms[].[AlarmName,StateValue,MetricName]' \
--output table

---

## 11. Check EC2 CPU Metric

Example command:

aws cloudwatch get-metric-statistics \
--namespace AWS/EC2 \
--metric-name CPUUtilization \
--dimensions Name=InstanceId,Value=INSTANCE_ID \
--statistics Average \
--period 300 \
--start-time 2026-09-22T00:00:00Z \
--end-time 2026-09-22T01:00:00Z \
--region ap-south-1

Replace:

INSTANCE_ID

with the actual EC2 instance ID.

---

## 12. Monitoring Best Practices

- Monitor important EC2 metrics continuously.
- Configure alarms for important thresholds.
- Use SNS for notifications.
- Monitor application logs.
- Use metric filters for important application errors.
- Use dashboards for centralized monitoring.
- Investigate ALARM states promptly.
- Review alarm configuration regularly.
- Avoid unnecessary alarms that generate excessive notifications.

---

## 13. Summary

EC2
 ↓
CloudWatch
 ↓
Metrics
 ↓
CloudWatch Alarm
 ↓
SNS
 ↓
Operations Team

CloudWatch provides monitoring, alerting, logging, and
visibility into AWS resources and applications.
