# 505AZ CloudFormation recovery starter

**Not a functional deployment.** This ZIP recreates the file layout and resource planning notes after accidental deletion. You must write and validate the resource definitions yourself, using course materials. The module brief says AI-generated functional project code is not permitted.

## Files
- `aws/cloudformation/vpc.yaml`: two VPCs, subnets, routes, network connectivity
- `aws/cloudformation/security-groups.yaml`: tier-to-tier security
- `aws/cloudformation/compute.yaml`: ALB, target group, launch template, Auto Scaling, management EC2
- `aws/cloudformation/database.yaml`: RDS primary and read replica
- `aws/cloudformation/main.yaml`: orchestration design
- `.github/workflows/deploy.yml`: intentionally non-deploying starter

## Existing console infrastructure (do not duplicate blindly)
Web VPC `vpc-05ff63b183772a2d5` (10.10.0.0/16); Private VPC (10.20.0.0/16); ALB `Web-Application-ALB`; target group `Web-Target-Group`; ASG `Web-Server-Auto-Scaling-Group`. Manual Transit Gateway setup exists, but brief explicitly requests peering. Check with tutor.

## Recovery suggestion
GitHub normally retains deleted files in history. Open repository > Commits, locate the commit before deletion, open the file and restore its contents in a new commit. This recovers your actual authored work and commit history rather than replacing it with a starter.

## Safety and marking reminders
- Do not create a CloudFormation stack using these placeholders.
- Existing manually created infrastructure is not automatically adopted by CloudFormation. Resource import is a separate procedure and resource-type support varies.
- The assignment requires CloudFormation-managed provisioning, GitHub Actions automation, private web tier, management EC2, RDS read replica, and peered VPCs. Discuss your Transit Gateway substitution with your tutor.
- Never commit secrets. Keep incremental commits and follow your brief's AI-use acknowledgement requirements.
