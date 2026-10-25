# AWS VPC Peering — Student Project Report

## 1. Project information
- Student name:
- Batch:
- Region: `ap-south-1` (Mumbai)
- Completion date:
- GitHub repository URL:

## 2. Objective
Describe how two non-overlapping VPCs are connected through VPC Peering while application servers remain private.

## 3. Architecture
Insert an architecture diagram or a screenshot of your own diagram. Label VPC CIDRs, subnet CIDRs, bastion, App-A, App-B, route tables, Internet Gateway, and peering.

## 4. Resource inventory
Record actual VPC IDs, subnet IDs, route table IDs, security group IDs, instance IDs, peering ID, and actual IP addresses. Never include private keys, passwords, or access tokens.

## 5. Routing and security
Explain the forward route and return route. Include screenshots of the three route tables and the relevant inbound security group rules.

## 6. Test results
| Test | Actual result | Evidence filename |
|---|---|---|
| Baseline ping before peering/routes | Fill in actual result | |
| App-A → App-B ping | Fill in actual result | |
| App-B → App-A ping | Fill in actual result | |
| SSH to App-B through bastion | Fill in actual result | |
| Controlled ICMP failure | Fill in actual result | |
| Recovery after restoring rule | Fill in actual result | |
| App-A and App-B have no public IP | Fill in actual result | |

## 7. Troubleshooting and learning
Describe one issue you encountered, how you diagnosed it, and how you resolved it.

## 8. Cost-safe cleanup
List the lab resources terminated/deleted and attach evidence that no lab resources remain that could incur charges. Check Billing because reporting can lag.

## 9. Conclusion
Summarize what you learned about VPC CIDRs, peering, route tables, security groups, bastion access, and private connectivity.
