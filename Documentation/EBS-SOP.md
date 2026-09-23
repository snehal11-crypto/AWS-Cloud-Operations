# EBS Standard Operating Procedure (SOP)

## 1. Purpose

This document defines the standard procedure for checking,
monitoring, and troubleshooting Amazon EBS volumes.

The objective is to maintain proper EBS volume usage,
identify unused volumes, and document EBS resources.

---
aws ec2 describe-volumes \
--region eu-north-1 \
--volume-ids vol-00d75f532bc3740ac \
--query 'Volumes[].[VolumeId,State,Size,VolumeType]' \
--output table
