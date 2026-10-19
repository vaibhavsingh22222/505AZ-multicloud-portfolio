# Remaining assessed work (checklist)

## Network (`vpc.yaml`)
- [x] Recover user-authored VPC and subnet resources.
- [x] Repair missing last `TransitGatewayRouteTableId` reference (syntax only).
- [ ] Decide VPC peering (brief-required) versus tutor-approved TGW.
- [ ] Reconcile AZs and subnet CIDRs with intended deployment; avoid accidental replacements.
- [ ] Public VPC Internet Gateway, gateway attachment, public route table, default route and public subnet associations.
- [ ] Private web subnets with outbound package access (NAT or appropriate alternative).
- [ ] Review TGW default association/propagation settings; ensure no duplicate or conflicting associations.
- [ ] Review private VPC routes for management traffic and database service connectivity.

## Security (`security-groups.yaml`)
- [ ] ALB SG: 80 from clients; HTTPS when implemented.
- [ ] Web SG: 80 from ALB SG only.
- [ ] Database SG: only DB port from web SG; no public inbound DB traffic.
- [ ] Management SG: least-privilege diagnostics, managed access; no open SSH.

## Application (`application.yaml`)
- [ ] Internet-facing ALB and listener in public subnets.
- [ ] Web target group, health check path and load balancer routing.
- [ ] Web EC2 Launch Template, bootstrapping, InstanceProfile, private web subnets.
- [ ] Auto Scaling group, CPU scaling policy and ALB target group attachment.
- [ ] Management EC2 instance in Private Services VPC private subnet.
- [ ] Web application connection to the database (a reachable application, not just Apache default page).

## Database (`database.yaml`)
- [ ] Private DB subnet group spanning AZs.
- [ ] RDS primary database and read replica.
- [ ] Store credentials securely outside GitHub; no password values in templates.

## Automation & evidence
- [ ] GitHub Actions AWS authentication configured using course-approved safe method.
- [ ] CI validates templates before deployment and demonstrates CloudFormation deploy.
- [ ] Confirm AWS Academy permissions permit CloudFormation/IAM/RDS operations.
- [ ] Record actual stack state, targets healthy, DB connectivity, peering routes, and Azure integration.
- [ ] Keep commit history; acknowledge permitted AI assistance per assignment brief.

This is a PLAN, not proof that remaining requirements are implemented.
