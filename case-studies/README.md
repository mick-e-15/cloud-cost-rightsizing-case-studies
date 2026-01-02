# Case Studies

This folder contains individual FinOps rightsizing case studies, each documenting:
- Utilization signals (Datadog)
- Cost attribution (AWS CUR / IQL)
- Risk and ownership context
- Safe vs unsafe optimization decisions

## Case Studies Index

Each folder below represents a real-world FinOps rightsizing decision, including
utilization analysis, cost attribution, risk assessment, and final action logic.

- **[EMR Core Node – Cluster-Level Rightsizing](./emr-core-node/)**
  - EMR-managed EC2 core node
  - Batch workload with burst-driven utilization
  - Decision made at cluster level, not instance level

- **[Unattached EBS Volume – Orphaned Storage Cleanup](./ebs-unattached-volume/)**
  - Unattached EBS volume with no active dependencies
  - Snapshot-first deletion path
  - Direct, low-risk cost optimization

- **[Kubernetes Worker Node – Capacity Signal Case Study](./k8s-worker-node/)** *(next)*
  - EKS / Karpenter-managed worker nodes
  - Utilization interpreted as capacity signal
  - Optimization routed to node pools and bin-packing

- **[Standalone EC2 Instance – True Rightsizing Candidate](./standalone-ec2-instance/)** 
  - Non-managed EC2 instance
  - Sustained low utilization
  - Direct resize or scheduling opportunity
