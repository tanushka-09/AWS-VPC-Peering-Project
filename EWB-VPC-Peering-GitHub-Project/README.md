# AWS VPC Peering Project — EWB Cloud Labs

A guided AWS networking project demonstrating private communication between two VPCs using VPC Peering, route tables, security groups, and a bastion host.

> **Status note:** This repository is a documentation and evidence template based on the project workbook and the steps performed so far. Update the checklist and add your own screenshots/terminal output before presenting the project as complete.

## Architecture

- **Region:** Asia Pacific (Mumbai), `ap-south-1`
- **VPC A:** `ewb-vpc-a` — `10.10.0.0/16`
  - Public subnet: `ewb-a-public` — `10.10.1.0/24`
  - Private subnet: `ewb-a-private` — `10.10.2.0/24`
  - Bastion host: actual private IP `10.10.1.196`, public IP `35.154.118.195` at the time recorded
  - App-A: actual private IP `10.10.2.188`
- **VPC B:** `ewb-vpc-b` — `10.20.0.0/16`
  - Private subnet: `ewb-b-private` — `10.20.1.0/24`
  - App-B: private IP `10.20.1.10`
- **VPC Peering:** `ewb-peering-a-b` — `pcx-093683ea5ed035089` (reported Active)

Use the live AWS console to confirm current public IPs, instance states, resource IDs, route-table associations, and security-group rules before final submission. Public IPv4 addresses may change after stopping/starting an instance.

## Goals

1. Create two non-overlapping VPCs and their subnets.
2. Keep App-A and App-B private (no public IPv4 address).
3. Establish an active VPC peering connection.
4. Add routes in both directions.
5. Allow only the required SSH and ICMP traffic.
6. Prove private connectivity and demonstrate a controlled failure/recovery.
7. Clean up lab resources after saving evidence.

## Repository contents

- `docs/NETWORK-PLAN.md` — CIDRs, routes, and security rules to verify.
- `docs/TEST-PLAN.md` — commands and evidence checklist.
- `docs/REPORT-TEMPLATE.md` — final report outline.
- `evidence/README.md` — where to add screenshots and actual test output.

## Key validation commands

Run these only from the correct host:
```bash
# On App-A: test App-B
ping -c 4 10.20.1.10

# On App-B: test App-A
ping -c 4 10.10.2.188

# On each instance
hostname
hostname -I
```

SSH to App-B through the bastion was previously successful using the private IP `10.20.1.10`. The reverse ping and controlled failure/recovery should still be captured before marking all tests complete.

## Security and cost notes

- Never upload `.pem` private keys, AWS access keys, passwords, session tokens, or personal account/billing screenshots.
- Do not open SSH or ICMP to `0.0.0.0/0`.
- The lab requires **no NAT Gateway**.
- EC2 instances, EBS volumes, and public IPv4 addresses may incur charges. Save evidence, then follow the workbook cleanup checklist and verify Billing.
- Avoid publishing account IDs, private account details, or unredacted console screenshots.

## Source

Built following the **EWB Cloud Labs — AWS VPC Peering Student Project Workbook** (October 2026). This repository is a student-created documentation package; add your own evidence and confirm every live AWS setting before submission.
