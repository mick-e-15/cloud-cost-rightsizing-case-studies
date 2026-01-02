# Unattached EBS Volume – Cost Elimination Case Study

## Resource
- Type: EBS Volume
- Volume ID: vol-XXXXXXXX
- Region: us-east-2
- State: available (unattached)
- Size: XX GB
- Volume Type: gp3 (example)

## Discovery Signals (Datadog / AWS)
- Volume not attached to any EC2 instance
- No read/write activity observed
- No recent snapshot activity
- No Kubernetes or ASG metadata present

## Cost Signal
- Ongoing storage cost with zero utilization
- Low daily cost individually
- Material waste at scale across multiple orphaned volumes

## Risk Assessment
- Low operational risk
- No compute dependency
- Data loss risk mitigated via snapshot

## Decision Logic
This volume is not referenced by any active compute resource and shows no usage signals.

**Safe action:**
- Create snapshot
- Wait defined retention period
- Delete volume

**Unsafe action:**
- Immediate deletion without snapshot
- Deletion without confirming ownership tags

## Outcome
- Cost eliminated with no service impact
- Pattern reusable across environments

## FinOps Takeaway
Unattached EBS volumes represent true waste and are safe optimization candidates when ownership and snapshot safeguards are applied.
