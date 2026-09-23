# IAM Standard Operating Procedure (SOP)

## 1. Purpose

This document defines the standard procedure for managing
AWS Identity and Access Management (IAM) users, groups, roles,
policies, and permissions.

The objective is to provide secure and controlled access to
AWS resources using the principle of least privilege.

---

## 2. IAM Components

### IAM User

An IAM user represents an individual identity that can access
AWS resources.

Example:

Developer
    ↓
IAM User
    ↓
AWS Resources

IAM users should only be given the permissions required for
their job responsibilities.

---

### IAM Group

An IAM group is a collection of IAM users.

Example:

Developers
    ↓
IAM Group
    ↓
IAM Policy
    ↓
Required AWS Permissions

Groups make it easier to manage permissions for multiple users.

---

### IAM Role

An IAM role provides temporary credentials to AWS services,
applications, or users.

Example:

EC2
 ↓
IAM Role
 ↓
CloudWatch permissions

For EC2 automation, an IAM role is preferable to storing
long-lived access keys on the EC2 instance.

---

### IAM Policy

An IAM policy is a JSON document that defines what actions
are allowed or denied on AWS resources.

Example:

CloudWatch Policy
    ↓
Allow CloudWatch API actions
    ↓
EC2 IAM Role

---

### Permission

A permission defines what an IAM identity is allowed to do.

Example:

Allow:
cloudwatch:PutMetricData

Resource:
Required AWS resource

---

## 3. IAM Relationship

The basic IAM permission flow is:

IAM User / IAM Role
        ↓
IAM Policy
        ↓
Permission
        ↓
AWS Resource

---

## 4. EC2 IAM Role

For EC2 automation, use an IAM role instead of storing
long-lived AWS access keys on the EC2 instance.

Example:

EC2 Instance
      ↓
IAM Instance Role
      ↓
IAM Policy
      ↓
CloudWatch / S3 / Other AWS Services

The EC2 instance receives temporary credentials through
the instance metadata service.

---

## 5. Principle of Least Privilege

IAM permissions should follow the principle of least privilege.

Users and roles should receive only the permissions required
to perform their assigned tasks.

Avoid granting unnecessary permissions such as:

AdministratorAccess

unless there is a documented requirement and appropriate
authorization.

---

## 6. Check IAM Roles

Use the following AWS CLI command:

aws iam list-roles

This command lists IAM roles in the AWS account.

---

## 7. Check IAM Policies

Use:

aws iam list-policies --scope Local

The --scope Local option displays customer-managed policies
created in the AWS account.

---

## 8. IAM Operational Checks

Regularly verify:

- IAM users
- IAM groups
- IAM roles
- IAM policies
- Attached permissions
- Unused credentials
- Excessive permissions
- Access keys
- MFA configuration where applicable

---

## 9. IAM Security Best Practices

1. Follow least privilege.
2. Prefer IAM roles for AWS services.
3. Avoid storing long-lived access keys on EC2 instances.
4. Use groups to manage permissions for multiple users.
5. Use customer-managed policies when custom permissions are required.
6. Review permissions regularly.
7. Remove unused credentials and permissions.
8. Enable MFA where appropriate.
9. Avoid using the AWS account root user for daily operations.

---

## 10. IAM Verification Commands

List IAM roles:

aws iam list-roles

List customer-managed IAM policies:

aws iam list-policies --scope Local

List IAM users:

aws iam list-users

List IAM groups:

aws iam list-groups

---

## 11. Summary

IAM User
    ↓
IAM Group
    ↓
IAM Policy
    ↓
Permissions
    ↓
AWS Resources

For AWS service automation:

EC2
    ↓
IAM Role
    ↓
IAM Policy
    ↓
Required AWS Permissions

IAM roles are preferred for EC2 automation because they provide
temporary credentials instead of requiring long-lived access keys
to be stored on the instance.
