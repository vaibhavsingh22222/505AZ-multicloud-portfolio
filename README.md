# 505AZ CloudFormation recovery / guided project

## STATUS — NOT READY FOR AWS DEPLOYMENT

This archive is a **recovery and debugging package**, **not a complete functional implementation**. Your 505AZ brief allows AI for debugging but prohibits AI-generated functional assessed code. Do not submit placeholders as completed work.

### What is recovered
- `aws/cloudformation/vpc.yaml` contains **your own pasted network template** with its missing last `!Ref TransitGatewayRouteTable` completed. This file is **not the full desired networking deployment**.
- `aws/cloudformation/security-groups.yaml`: non-deployable guidance for security groups.
- `aws/cloudformation/application.yaml`: non-deployable guidance for web ALB/EC2/ASG and management EC2.
- `aws/cloudformation/database.yaml`: non-deployable guidance for RDS primary and replica.
- `aws/cloudformation/main.yaml`: non-deployable architecture/orchestration notes.
- `.github/workflows/deploy.yml`: harmless non-deploying example; build the required CI/CD workflow yourself.
- `DEPLOYMENT_GUIDE.md`: safe validation, commit and AWS rollout instructions.
- `REMAINING_WORK.md`: detailed gaps and discrepancies.

### IMPORTANT before deploying
- Your real resources already exist in AWS. A new `AWS::EC2::VPC`/TGW template creates additional resources; **CloudFormation does not automatically adopt them**.
- Module brief demands **VPC peering**, a **private web tier**, private management EC2 and **RDS read replica**, plus CI/CD. Your current design is TGW and the ASG is in public subnets. Check tutor approval if keeping these deviations.
- The pasted VPC YAML has no Internet Gateway, public route table, or public routes, even though the manual AWS environment has them.
- The source code's AZs (`us-east-1a` and `us-east-1b`) differ from the two public subnet AZs observed manually (`us-east-1c`, `us-east-1d`).
- The pasted YAML enables Transit Gateway default association and propagation unless configured otherwise; custom TGW route-table associations may conflict. Confirm before deploying.

**Start:** read `DEPLOYMENT_GUIDE.md`, then inspect and complete the YAML yourself in GitHub with incremental commits. Do not run deployment until code and architecture have been reviewed and validated.
