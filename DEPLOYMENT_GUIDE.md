# GitHub to AWS CloudFormation: safe step-by-step guide

## 1) Move these files to GitHub
1. Download the ZIP, then extract it to your laptop.
2. Open GitHub repository `505AZ-multicloud-portfolio` and branch `main` (or a new working branch).
3. Open the `aws/cloudformation` folder. Use **Add file → Upload files** to upload the YAML files from the ZIP's matching `aws/cloudformation` folder. Note: your repository already has `vpc.yaml`, `database.yaml` and `application.yaml`. Check **History** before replacing anything; preserve original versions.
4. Commit using a descriptive message such as `Recover and debug existing CloudFormation network template`.
5. Put `deploy.yml` in **`.github/workflows/`**. This included workflow DOES NOT deploy and is intentionally only a placeholder.

## 2) Review / validate locally without creating AWS resources
- Read `REMAINING_WORK.md` and complete resources using your course materials.
- Check YAML syntax. YAML formatting success alone DOES NOT prove a successful CloudFormation deployment.
- If AWS CLI is configured for this lab, you can ask CloudFormation to parse a template without creating resources:

```bash
aws cloudformation validate-template --template-body file://aws/cloudformation/vpc.yaml --region us-east-1
```

- Repeat validation for each COMPLETE template when ready. An empty placeholder with no `Resources` may be rejected; this is expected and means it is not complete.
- Validation does not test practical network connectivity, all deployment-time constraints, or permissions.

## 3) Choose how to handle resources already created manually
**A. Deploy to separate isolated infrastructure**: remove/stop unneeded manual resources when safe and approved; verify lab costs and quotas. Code that includes VPC and TGW always creates new ones in a new CloudFormation stack.
**B. Import eligible existing resources into CloudFormation**: resource import requires CloudFormation import support, identifiers, correct matching template and prerequisites; not all resource types or configurations can be imported, so check each resource first. Do not use an ordinary Create Stack to perform an import.
**C. Use existing physical IDs as parameters** in a separate stack for new resources ONLY. This references existing resources but does not magically convert them into CloudFormation-managed ones.

Your AWS Academy lab's existing stack described as `associate Learner Lab template (academy)` is unrelated to your course IaC stack; **do not edit/delete it**.

## 4) Deploy only when templates are COMPLETE and approved
- First choose an isolated testing account/environment or a careful import plan.
- In the AWS console open **CloudFormation → Stacks → Create stack** and upload your completed template (not the current starter). Use a unique stack name.
- Review Parameters, IAM capabilities if required and all listed resources/costs.
- Inspect a **change set** before execution wherever practical. If the list unexpectedly includes extra VPCs/TGWs/RDS, stop.
- For a CLI-based safe preview, a validated completed template can be submitted with `aws cloudformation deploy --no-execute-changeset` (the command creates a change set but will not execute it); requires correct AWS permissions and configuration. Not applicable to this incomplete starter.
- Once explicitly approved, deploy and wait for `CREATE_COMPLETE`; investigate `Events` on failure rather than repeatedly redeploying blindly.

## 5) Connect to GitHub Actions (student-authored implementation)
- Add a workflow that checks out code, configures permitted AWS credentials securely, validates templates, creates/reviews changes and deploys only after approval.
- Confirm AWS Academy lab policy: your account already returned explicit deny for an Auto Scaling instance refresh and may restrict other actions.
- Never put AWS access keys or RDS passwords in public GitHub files.
- Demonstrate live: commit → GitHub Actions run → CloudFormation stack events → deployed app/database/network tests.

## 6) Assignment mismatch to resolve
The uploaded 505AZ brief requires peered VPCs, private web ASG, private management EC2, RDS primary + read replica, and GitHub Actions deploy. You have used a Transit Gateway and public web subnets manually. Obtain tutor approval for those differences or change your assessed design.
