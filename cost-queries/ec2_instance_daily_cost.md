# EC2 Instance – Daily Cost Attribution

## Purpose
Attribute daily AWS cost to a **single EC2 instance** using resource-level identifiers.
Used to pair utilization signals (Datadog) with actual spend (FinOps).

## Query Pattern (CUR-style / IQL-inspired)

```sql
FROM aws_costandusage <start_date> <end_date>
WHERE bill_billing_entity = 'AWS'
  AND line_item_line_item_type != 'Tax'
  AND line_item_product_code = 'AmazonEC2'
  AND line_item_resource_id = '<ec2-instance-id>'
GROUP BY time(1d ALLOW PARTIAL)
SELECT
  ROUND(net_amortized_cost_nano / 1e9, 2) AS daily_net_amortized_cost_usd
