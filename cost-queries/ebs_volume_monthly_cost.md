# EBS Volume – Monthly Cost Attribution

## Purpose
Attribute AWS storage cost to a single EBS volume using resource-level identifiers.

## Query Pattern (CUR-style / IQL-inspired)

```sql
FROM aws_costandusage <start_date> <end_date>
WHERE bill_billing_entity = 'AWS'
  AND line_item_product_code = 'AmazonEC2'
  AND line_item_usage_type LIKE '%EBS:VolumeUsage%'
  AND line_item_resource_id = '<ebs-volume-id>'
GROUP BY time(1M ALLOW PARTIAL)
SELECT
  ROUND(net_amortized_cost_nano / 1e9, 2) AS monthly_cost_usd
