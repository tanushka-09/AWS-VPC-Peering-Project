# Test Plan and Evidence Checklist

Capture your own terminal output and AWS console screenshots. Do not mark a test passed until you have run it and saved evidence.

## 1. Instance identity

On each EC2 host:
```bash
hostname
hostname -I
```
Save screenshots showing which host produced the output.

## 2. Forward private ping (App-A → App-B)

On App-A:
```bash
ping -c 4 10.20.1.10
```
Expected after peering routes and security rules are correct: four replies and `0% packet loss`.

## 3. Reverse private ping (App-B → App-A)

On App-B:
```bash
ping -c 4 10.10.2.188
```
Expected after peering routes and security rules are correct: four replies and `0% packet loss`.

## 4. SSH through the bastion

From your laptop, use your configured SSH ProxyJump setup to connect to App-B. The workbook's sample command is `ssh ewb-app-b` after the SSH config is correctly configured. Do not upload private keys to GitHub or paste them into this repository.

## 5. Isolation check

In the EC2 console, confirm App-A and App-B have no public IPv4 addresses. Save a redacted screenshot.

## 6. Controlled failure and recovery

1. In App-B's security group, temporarily remove only the inbound ICMP Echo Request rule from App-A (`10.10.2.188/32`).
2. Repeat the forward ping from App-A. Replies should stop.
3. Restore the exact ICMP rule.
4. Repeat the ping. Replies should resume.
5. Capture all three states: normal success, controlled failure, restored success.

Keep the SSH rule in place throughout the test.

## 7. Suggested evidence filenames

- `01-vpcs-subnets.png`
- `02-route-tables.png`
- `03-peering-active.png`
- `04-security-groups.png`
- `05-forward-ping-success.png`
- `06-reverse-ping-success.png`
- `07-ssh-through-bastion.png`
- `08-controlled-failure.png`
- `09-recovery-success.png`
- `10-private-instances-no-public-ip.png`
- `11-cleanup.png`

Redact account IDs and any sensitive details that are not required for evaluation.
