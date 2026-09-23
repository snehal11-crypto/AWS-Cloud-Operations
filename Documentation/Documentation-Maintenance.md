# Documentation Maintenance

Documentation should be reviewed regularly to ensure that SOPs and runbooks remain accurate and useful.

## Maintenance Workflow

Monthly
   ↓
Review SOPs
   ↓
Check AWS changes
   ↓
Update commands
   ↓
Update screenshots
   ↓
Update troubleshooting
   ↓
Commit changes
   ↓
Peer review
   ↓
Merge

## Documentation Review Schedule

| Document | Owner | Version | Review Frequency |
|----------|-------|---------|------------------|
| EC2 SOP | Cloud Ops | 1.2 | Monthly |
| EBS SOP | Cloud Ops | 1.1 | Monthly |
| IAM SOP | Security | 1.3 | Quarterly |
| CloudWatch SOP | Cloud Ops | 1.2 | Monthly |

## Maintenance Checklist

### SOP Review

- Check whether AWS services or features have changed.
- Verify AWS CLI commands.
- Verify resource names and examples.
- Check IAM permissions.
- Check security recommendations.
- Update outdated procedures.

### Screenshot Review

- Replace outdated AWS Console screenshots.
- Ensure screenshots match the current AWS Console.
- Remove unnecessary or sensitive information.

### Troubleshooting Review

- Verify troubleshooting commands.
- Add newly discovered issues.
- Remove obsolete troubleshooting steps.
- Update resolution procedures.

## Version Control

Every significant documentation change should update the document version.

Example:

```text
Version 1.0
Initial documentation

Version 1.1
Updated AWS CLI commands

Version 1.2
Updated screenshots and troubleshooting steps
