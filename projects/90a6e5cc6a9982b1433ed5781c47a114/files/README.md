# merge-relations-cleaning-lab test data

This workspace contains synthetic sales data for IMD client testing.

Main table:
- aggregate_test_sales.csv: order-level sales facts with a few intentional data-quality issues.

Related tables:
- stores.csv links by store_id and region_id.
- products.csv links by sku.
- regions.csv links by region_id.
- sales_targets.csv links by region_id and product_category.
- returns.csv links by order_id.

Suggested prompts:
- Which region has the highest net revenue?
- Compare actual sales with sales_targets by month and region.
- Find data-quality issues in aggregate_test_sales.csv.
- Which products have the highest return rate?
