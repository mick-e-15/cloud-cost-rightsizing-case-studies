# Standalone EC2 Rightsizing Case Study

## Overview
This case study documents the identification and evaluation of a standalone EC2 instance flagged for rightsizing using Datadog Cloud Cost and CloudWatch signals. Unlike cluster-managed capacity (EKS, EMR), this instance represents a true per-instance optimization candidate.

## Resource
- **Instance ID:** i-0c0ddfd8a39749f9e
- **Instance Type:** m5.4xlarge
- **Region:** ca-central-1
- **Operating System:** Windows
- **Management Model:** Standalone EC2 (no ASG, no cluster)

## Observed Signals
- CPU utilization consistently below ~50% (p95) over a 7-day window
- No burst-driven workload patterns observed
- No autoscaling, scheduler, or cluster ownership detected
- Identified via Datadog Cloud Cost rightsizing recommendation
- Monthly cost estimated at ~$830 with ~50% downsizing opportunity

## Why This Is a Valid Rightsizing Candidate
- Capacity is not shared or absorbed by a cluster
- No evidence of batch, burst, or failover-driven sizing requirements
- Persistent CPU headroom suggests overprovisioning
- Cost signal is clear and attributable at the instance level

## Risks and Gaps
- Memory utilization not available (Datadog agent not installed)
- Windows workloads may be memory-sensitive
- Disk and network behavior not fully observable

These are validation gaps, not architectural blockers.

## Decision Logic
- Do not resize blindly
- Treat this as a valid rightsizing candidate pending memory validation
- Proceed only after confirming memory and service stability

## Safe Optimization Path
- Install Datadog or CloudWatch memory monitoring
- Identify owning team via AWS tags or internal ownership mapping
- Perform controlled downsize (m5.4xlarge → m5.2xlarge)
- Monitor CPU, memory, and service health post-change

## Final Classification
- **Status:** Actionable EC2 rightsizing candidate
- **Optimization Type:** Instance-level
- **Risk Level:** Medium (observability gap)
- **Owner:** Application / platform team (to be confirmed)

## Resume-Grade Takeaway
Mapped cost and utilization for a standalone Windows EC2 instance, validated it as a true rightsizing candidate, identified observability gaps, and defined a safe, data-backed downsizing path.

