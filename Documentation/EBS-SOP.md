# EBS Standard Operating Procedure (SOP)

## 1. Purpose

This document defines the standard procedure for checking,
monitoring, and troubleshooting Amazon Elastic Block Store (EBS)
volumes.

The objective is to maintain proper storage configuration,
identify unused volumes, and verify EBS volume health and
attachments.

---

## 2. EBS Volume Inventory

Use the following AWS CLI command to list EBS volumes:

```bash
aws ec2 describe-volumes \
--query 'Volumes[].[VolumeId,Size,VolumeType,State,Attachments[0].InstanceId,AvailabilityZone]' \
--output table
```

The output provides:

* Volume ID
* Size
* Volume Type
* State
* Attached EC2 Instance
* Availability Zone

---

## 3. Check EBS Volume Details

To view complete details of all EBS volumes:

```bash
aws ec2 describe-volumes --output table
```

For a specific volume:

```bash
aws ec2 describe-volumes \
--volume-ids <volume-id>
```

Replace `<volume-id>` with the actual EBS volume ID.

---

## 4. EBS Volume States

### In-use

The EBS volume is currently attached to an EC2 instance.

### Available

The EBS volume is not currently attached to an EC2 instance.

Unused EBS volumes should be reviewed because they can continue
to generate storage charges.

---

## 5. EBS Troubleshooting

### Problem: EBS volume is not attached

Checks:

1. Verify the volume ID.
2. Check the volume state.
3. Verify the Availability Zone.
4. Check whether the target EC2 instance is running.
5. Verify that the volume and EC2 instance are in the same Availability Zone.
6. Check whether the volume is already attached to another instance.

Command:

```bash
aws ec2 describe-volumes \
--volume-ids <volume-id>
```

---

### Problem: EBS volume is not visible inside EC2

Checks:

1. Verify the volume is attached to the correct EC2 instance.
2. Check the device name.
3. Check the operating system for the attached device.
4. Check filesystem information.
5. Check whether the filesystem is mounted.

Linux commands:

```bash
lsblk
```

```bash
df -h
```

```bash
sudo fdisk -l
```

---

## 6. EBS Volume Monitoring

Important items to monitor:

* Volume state
* Volume size
* Volume type
* Volume attachment
* Availability Zone
* EBS performance metrics
* Unused volumes

CloudWatch can be used to monitor EBS-related metrics.

---

## 7. EBS Snapshot

Create a snapshot of an EBS volume:

```bash
aws ec2 create-snapshot \
--volume-id <volume-id> \
--description "EBS backup"
```

Verify snapshots:

```bash
aws ec2 describe-snapshots \
--owner-ids self \
--output table
```

Snapshots should be managed according to the organization's
backup and retention policy.

---

## 8. EBS Operational Checklist

Before making changes:

* [ ] Verify Volume ID
* [ ] Verify volume state
* [ ] Verify volume size
* [ ] Verify volume type
* [ ] Verify attached EC2 instance
* [ ] Verify Availability Zone
* [ ] Confirm backup requirements
* [ ] Confirm impact before detaching or modifying the volume

---

## 9. Documentation

Maintain the following information for each EBS volume:

| Field             | Value |
| ----------------- | ----- |
| Volume ID         |       |
| Size              |       |
| Type              |       |
| State             |       |
| Attached Instance |       |
| Availability Zone |       |
| Purpose           |       |
| Snapshot/Backup   |       |

---

## 10. Validation

Run the following command to validate the EBS environment:

```bash
aws ec2 describe-volumes \
--query 'Volumes[].[VolumeId,State,Size,VolumeType,Attachments[0].InstanceId,AvailabilityZone]' \
--output table
```

Confirm that:

* All required volumes exist.
* Required volumes are attached to the correct instances.
* Volume states are correct.
* Volume types and sizes are as expected.
* Availability Zones are correct.
* Unused volumes have been identified for review.
