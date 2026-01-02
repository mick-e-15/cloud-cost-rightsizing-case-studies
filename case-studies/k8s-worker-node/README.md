# Kubernetes Worker Node – Capacity Signal, Not Direct Rightsizing

## Resource
- **Type:** EC2 (Kubernetes worker node)
- **Orchestration:** EKS / Karpenter-managed
- **Role:** Shared cluster capacity (not standalone compute)
- **Ownership:** Platform / Kubernetes team

## Utilization Signals (Datadog)
- CPU averages below ~40% with burst-driven spikes
- Memory usage well below node capacity
- Low sustained disk and network IO
- Utilization varies with pod scheduling and deployments

## Cost Signal
- Node shows stable daily cost
- Individually small, material at fleet scale
- Cost cannot be evaluated independently of cluster behavior

## Why This Looks Rightsize-able at First Glance
- Apparent headroom in CPU and memory
- Periods of low utilization between workloads
- Traditional EC2 heuristics would suggest downsizing

## Risk & Friction
- Node is part of a Kubernetes scheduling pool
- Capacity must absorb:
  - Pod bursts
  - Rescheduling during node drains
  - Autoscaler behavior (Karpenter)
- Direct downsizing risks:
  - Pod eviction
  - Scheduling failures
  - Latency spikes during deploys
  - Cascading instability

## Decision Logic
- **Do NOT resize individual EC2 instances**
- Treat utilization as a **capacity signal**, not waste
- Route optimization decisions to:
  - Node pool sizing
  - Bin-packing efficiency
  - Pod request/limit tuning
  - Instance family and size mix

## Safe Action
- Share utilization evidence with platform team
- Evaluate cluster-level efficiency
- Adjust autoscaling and node pool policies

## Unsafe Action
- Manual EC2 resize
- Instance termination outside cluster logic

## Final Classification
- **Status:** Valid signal, not directly actionable
- **Optimization Type:** Structural / systemic
- **Risk Level:** Medium–High if acted on directly
- **Owner:** Platform / Kubernetes team

## FinOps Takeaway
Low utilization on Kubernetes worker nodes informs cluster design and autoscaling strategy, not instance-level rightsizing.
