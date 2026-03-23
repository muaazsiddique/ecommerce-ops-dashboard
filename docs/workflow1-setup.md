# Workflow 1: Order Data Ingestion

## Overview
Captures incoming e-commerce orders via webhook and logs them to Google Sheets automatically.

## Architecture
[Webhook] → [Google Sheets: Add a Row]

## Trigger
- Custom Webhook (simulates WooCommerce/Shopify order notifications)
- In production: replace with real WooCommerce/Shopify webhook URL

## Data Fields
| Field | Description | Example |
|-------|-------------|---------|
| Order ID | Unique order identifier | ORD-20001 |
| Timestamp | ISO 8601 order time | 2026-03-23T14:30:00Z |
| Customer Name | Full name | Sarah Johnson |
| Customer Email | Contact email | sarah.johnson@email.com |
| Product | Product purchased | Wireless Earbuds Pro |
| Quantity | Units ordered | 1 |
| Unit Price | Price per unit | 49.99 |
| Total Amount | Quantity x Unit Price | 49.99 |
| Payment Method | Payment type | Credit Card |
| Order Status | Current status | Completed |
| Country | Customer country | US |

## Google Sheets Target
- Spreadsheet: E-Commerce Ops Dashboard
- Tab: Orders
- New row added per order

## Testing
Send test payloads via PowerShell:
```
Invoke-WebRequest -Uri "WEBHOOK_URL" -Method POST -ContentType "application/json" -Body '{"order_id":"ORD-20001",...}'
```
See sample-data/test-orders.json for full payloads.

## Status: COMPLETE
```

---

**File 3: The screenshot**

You should already have the screenshot saved. Make sure it's in:
```
ecommerce-ops-dashboard\assets\workflow1-order-ingestion.png