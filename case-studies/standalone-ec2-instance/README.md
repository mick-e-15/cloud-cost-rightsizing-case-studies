# EMR Core Node – Rightsizing & Risk Analysis

## Resource
- **Type:** EC2 (EMR-managed core node)
- **Instance ID:** i-05e26ea89ed3531fd
- **Region:** us-east-2
- **Instance Type:** r6gd.12xlarge
- **Owner:** Data Infrastructure / AutoJoin

## Utilization Signals
- CPU shows burst-driven spikes with idle headroom between jobs
- Memory dominated by JVM and batch job components (~400 GB node)
- Load increases during job execution windows
- No sustained disk or network pressure

## Cost Signal
- Daily net amortized cost: ~$23/day
- Cost is stable and predictable
- Individually small, material at cluster scale
- Cost derived via resource-level AWS CUR query (daily net amortized cost)

## Decision Logic
- This node is part of an EMR-managed cluster
- Low utilization reflects batch workload patterns, not waste

**Safe action:** Review cluster sizing, job parallelism, and node count  
**Unsafe action:** Resize or terminate individual instances

## Final Classification
- **Status:** Valid signal, not directly actionable
- **Optimization type:** Cluster-level
- **Risk if misapplied:** High

## FinOps Takeaway
This instance-level signal was used to validate cluster economics, not to trigger resizing. True optimization opportunities exist at the EMR cluster configuration and job parallelism level, not per-node rightsizing.
