# cloud-cost-rightsizing-case-studies
Used Datadog to analyze utilization and ownership signals across EC2, EBS, and Kubernetes resources, distinguishing true optimization candidates from intentional capacity. Paired metrics with FinOps decision logic to define safe vs unsafe actions and inform cluster-level, not instance-level, optimization.

## What’s in this repo

This repository contains real-world FinOps rightsizing case studies built from Datadog telemetry, AWS cost data, and structured decision logic.

Each case study includes:
- Resource discovery and ownership signals
- Utilization analysis (Datadog)
- Cost attribution (AWS Cost & Usage / IQL)
- Risk assessment and safe vs unsafe actions
- Final decision logic and outcome
