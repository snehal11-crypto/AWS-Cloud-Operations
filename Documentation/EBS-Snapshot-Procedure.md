# EBS Snapshot Procedure

## 1. Purpose

This document defines the standard procedure for creating,
retaining, and cleaning up Amazon EBS snapshots.

The objective is to protect EBS volume data and maintain
regular backups using Amazon Data Lifecycle Manager (DLM).

---

## 2. EBS Snapshot Flow

EBS Volume
    ↓
Snapshot
    ↓
Retention
    ↓
Cleanup

The EBS volume is backed up using an EBS snapshot.
Snapshots are retained according to the configured retention policy.
Older snapshots are automatically deleted after the retention period.

---

## 3. Data Lifecycle Manager (DLM)

DLM is used to automate the creation and retention of EBS snapshots.

Example policy:

Daily Snapshot
      ↓
Keep last 7 snapshots
      ↓
Automatically delete old snapshots

---

## 4. DLM Policy Details

Policy Name:
EBS-Daily-Snapshot-Policy

Target Volumes:
EBS volumes with the required target tag

Schedule:
Daily

Snapshot Time:
Specify the configured time

Retention:
Keep the last 7 snapshots

Tags:
Backup = Daily

Execution Status:
Enabled

---

## 5. DLM Policy Configuration

The DLM policy should contain the following configuration:

- Policy type: EBS snapshot policy
- Target resource: EBS volumes
- Schedule: Daily
- Retention: 7 snapshots
- Target tag: Backup=Daily
- Policy status: Enabled

---

## 6. Snapshot Verification

List EBS snapshots using:

aws ec2 describe-snapshots \
--owner-ids self \
--region ap-south-1 \
--query 'Snapshots[].[SnapshotId,VolumeId,StartTime,State,Progress]' \
--output table

Verify:

- Snapshot ID
- Source Volume ID
- Creation time
- Snapshot state
- Snapshot progress

---

## 7. Verify DLM Policies

Use:

aws dlm get-lifecycle-policies \
--region ap-south-1

Verify:

- Policy ID
- Policy state
- Policy status
- Policy configuration

---

## 8. Snapshot Lifecycle

The snapshot lifecycle is:

1. EBS volume is identified.
2. DLM identifies the volume using the configured tag.
3. DLM creates a snapshot according to the schedule.
4. Snapshot is retained according to the retention policy.
5. Older snapshots are automatically deleted.
6. Snapshot status is monitored.

---

## 9. Execution Status

Policy Status:
Enabled

Snapshot Status:
To be verified using AWS CLI or AWS Console.

Verification Command:

aws dlm get-lifecycle-policies \
--region ap-south-1

---

## 10. Operational Checks

Regularly verify:

- DLM policy is enabled.
- Target EBS volumes have the correct tags.
- Snapshots are being created successfully.
- Snapshot retention is working.
- Old snapshots are being deleted according to policy.
- No unexpected snapshot failures are present.

---

## 11. Important Tags

Example:

Key: Backup
Value: Daily

Only EBS volumes with the required tag should be targeted
by the DLM policy.

---

## 12. Recovery

If an EBS volume needs to be restored:

1. Select the required EBS snapshot.
2. Create a new EBS volume from the snapshot.
3. Select the correct Availability Zone.
4. Attach the new volume to the required EC2 instance.
5. Mount the volume if required.
6. Verify the data.

---

## 13. Summary

EBS Volume
    ↓
DLM Policy
    ↓
Daily Snapshot
    ↓
Retain 7 Snapshots
    ↓
Automatically Delete Older Snapshots

This provides an automated and consistent EBS backup process.
