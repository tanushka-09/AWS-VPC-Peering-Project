# Network Plan and Configuration Checklist

## Address plan

| Resource | CIDR / address | Expected role |
|---|---|---|
| `ewb-vpc-a` | `10.10.0.0/16` | VPC A |
| `ewb-a-public` | `10.10.1.0/24` | Bastion subnet |
| `ewb-a-private` | `10.10.2.0/24` | App-A subnet |
| `ewb-vpc-b` | `10.20.0.0/16` | VPC B |
| `ewb-b-private` | `10.20.1.0/24` | App-B subnet |
| Bastion | `10.10.1.196` (actual observed) | Public administration host |
| App-A | `10.10.2.188` (actual observed) | Private workload |
| App-B | `10.20.1.10` (actual observed) | Private workload |

## Route tables to verify

| Route table | Required routes |
|---|---|
| VPC A public route table associated with `ewb-a-public` | `10.10.0.0/16` → local; `0.0.0.0/0` → Internet Gateway; `10.20.0.0/16` → peering |
| VPC A private route table associated with `ewb-a-private` | `10.10.0.0/16` → local; `10.20.0.0/16` → peering |
| VPC B private route table associated with `ewb-b-private` | `10.20.0.0/16` → local; `10.10.0.0/16` → peering |

Confirm that the VPC A private subnet is actually associated with the private route table. Do not assume the public route table's peering route covers App-A.

## Security group rules to verify

Use actual source IPs/CIDRs from your live configuration and follow least privilege.

- Bastion: inbound SSH/TCP 22 from your current public IPv4 `/32`.
- App-A: inbound SSH/TCP 22 from the bastion private IP `/32` (observed bastion IP: `10.10.1.196/32`).
- App-A: inbound ICMP Echo Request from App-B private IP `/32` (`10.20.1.10/32`).
- App-B: inbound SSH/TCP 22 from the bastion private IP `/32` (`10.10.1.196/32`).
- App-B: inbound ICMP Echo Request from App-A private IP `/32` (`10.10.2.188/32`).

Keep default outbound allow-all rules for this beginner lab unless your instructor specifies otherwise. Do not expose SSH or ICMP to `0.0.0.0/0`.
