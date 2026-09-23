# Application Down Runbook

## Problem

The application or web service is not responding.

Example service:

Nginx

Possible symptoms:

- Website is not accessible
- Application is not responding
- HTTP 5xx errors
- Connection refused
- Service is stopped
- Application process has failed

---

## Detection

Application downtime can be detected through:

- CloudWatch monitoring
- Application health checks
- Load Balancer health checks
- User reports
- Monitoring alerts

Flow:

Application Down
       ↓
Check Service Status
       ↓
Identify Problem
       ↓
Check Logs
       ↓
Restart Service
       ↓
Verify Service
       ↓
Test Application
       ↓
Monitor Application

---

## Investigation

### Step 1 — Check service status

Check the Nginx service:

```bash
systemctl status nginx
