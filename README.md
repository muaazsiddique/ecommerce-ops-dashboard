# E-Commerce Operations Dashboard + Smart Alerts

Automated e-commerce monitoring system that tracks orders, calculates ad performance metrics, aggregates daily KPIs, and sends intelligent Slack alerts when business metrics cross danger thresholds.

**Built with:** Make.com | Google Sheets | Looker Studio | Slack | OpenAI

---

## The Problem

E-commerce store owners waste hours every day manually checking orders, logging into ad platforms, calculating ROAS, and trying to figure out if their ads are profitable. By the time they notice a problem — like ad spend spiraling while conversions drop — they've already lost hundreds of dollars.

## The Solution

A fully automated monitoring system that:

1. **Captures every order** in real-time via webhook and logs it to a central dashboard
2. **Tracks ad spend** across Meta Ads and Google Ads campaigns with automatic CPA and ROAS calculations
3. **Aggregates daily metrics** — revenue, orders, average order value, ad performance — into one summary view
4. **Sends smart Slack alerts** the moment a KPI crosses a danger threshold, with context and recommended actions
5. **Visualizes trends** through a Looker Studio dashboard connected to live data

The store owner wakes up to either a clean dashboard (good day) or a specific, actionable Slack alert telling them exactly what went wrong and what to do about it.

---

## System Architecture

```
                    +---------------------+
                    |   WooCommerce /      |
                    |   Shopify Store      |
                    +----------+----------+
                               | Webhook (order placed)
                               v
+------------------------------------------------------+
|  WORKFLOW 1: Order Data Ingestion                    |
|  [Webhook] --> [Google Sheets: Add Order Row]        |
+-----------------------------+------------------------+
                              |
                              v
                    +---------------------+
                    |   Google Sheets     |
                    |   "Orders" Tab      |
                    +---------------------+

    +-------------------------------------------------+
    |  WORKFLOW 2: Ad Spend Tracker (Daily)            |
    |  [Search Ad Data] --> [Calculate CPA & ROAS]     |
    |  --> [Update Ad Spend Sheet]                     |
    +-------------------------------------------------+

    +-------------------------------------------------+
    |  WORKFLOW 3: Daily Metrics Aggregator            |
    |  [Search Orders] --> [Sum Revenue]               |
    |  --> [Search Ad Spend] --> [Sum Spend]            |
    |  --> [Write Daily Dashboard Row]                 |
    +-------------------------+-----------------------+
                              |
                              v
                    +---------------------+
                    |   Google Sheets     |
                    |   "Daily Dashboard" |
                    +----------+----------+
                               |
              +----------------+----------------+
              v                v                v
    +-------------+  +-------------+  +--------------+
    | WORKFLOW 4   |  |   Looker    |  |  Alert Log   |
    | Smart Alerts |  |   Studio    |  |  (Google     |
    | --> Slack    |  |  Dashboard  |  |   Sheets)    |
    +-------------+  +-------------+  +--------------+
```

---

## Workflows

| # | Workflow | Trigger | What It Does | Status |
|---|---------|---------|-------------|--------|
| 1 | Order Data Ingestion | Webhook | Catches incoming orders, logs to Google Sheets | Complete |
| 2 | Ad Spend Tracker | Scheduled (Daily) | Calculates CPA and ROAS for each campaign | Complete |
| 3 | Daily Metrics Aggregator | Scheduled (Daily) | Summarizes all daily KPIs into one dashboard row | Complete |
| 4 | Smart Alerts Engine | After WF3 | Checks thresholds, sends Slack alerts | Complete |

---

## Smart Alert Thresholds

| Alert | Trigger Condition | Slack Message |
|-------|------------------|---------------|
| Low ROAS | ROAS drops below 2.0 | Ads are losing money — consider pausing underperforming campaigns |
| Low Orders | Daily orders below 3 | Sales dropped — check website uptime and traffic sources |
| High CPA | CPA exceeds $15 | Acquisition cost too high — review targeting and landing pages |

---

## Dashboard Metrics

| Metric | Description | Source |
|--------|-------------|--------|
| Total Orders | Count of orders received today | Orders tab |
| Total Revenue | Sum of all order amounts | Orders tab |
| Avg Order Value | Revenue / Orders | Calculated |
| Total Ad Spend | Sum of campaign spend | Ad Spend tab |
| Total Ad Revenue | Revenue attributed to ads | Ad Spend tab |
| ROAS | Ad Revenue / Ad Spend | Calculated |
| CPA | Ad Spend / Conversions | Calculated |
| CTR | Clicks / Impressions | Calculated |

---

## Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| Automation | Make.com | Workflow orchestration |
| Data Store | Google Sheets | Central database for all metrics |
| Visualization | Looker Studio | Interactive dashboard with live charts |
| Alerts | Slack | Real-time KPI breach notifications |
| Data Sources | WooCommerce/Shopify Webhooks | Order data ingestion |
| Ad Platforms | Meta Ads, Google Ads | Campaign performance data |

---

## Project Structure

```
ecommerce-ops-dashboard/
├── workflows/          # Make.com scenario blueprint exports
├── docs/               # Setup documentation for each workflow
│   ├── workflow1-setup.md
│   ├── workflow2-setup.md
│   ├── workflow3-setup.md
│   └── workflow4-setup.md
├── assets/             # Screenshots and dashboard images
├── sample-data/        # Test payloads for webhook testing
│   └── test-orders.json
├── .env.example        # Credential template (no real keys)
└── README.md
```

---

## Quick Start

**Prerequisites:**
- Make.com account (Core plan or higher)
- Google account (Sheets + Looker Studio)
- Slack workspace with incoming webhooks

**Setup Steps:**
1. Clone this repo
2. Create Google Sheet with 4 tabs: Orders, Ad Spend, Daily Dashboard, Alert Log
3. Create Slack channel #ecommerce-alerts with incoming webhook
4. Import Make.com scenarios and connect credentials
5. Send test orders via webhook (see sample-data/test-orders.json)
6. Connect Looker Studio to the Daily Dashboard tab

---

## Business Impact

| Without Automation | With This System |
|-------------------|-----------------|
| Manually check orders multiple times daily | Orders logged automatically in real-time |
| Log into Meta Ads + Google Ads separately | All ad metrics in one unified dashboard |
| Calculate ROAS by hand in spreadsheets | CPA and ROAS calculated automatically |
| Notice problems hours or days late | Slack alert within minutes of KPI breach |
| No historical tracking of daily performance | 30-day trend data with visual charts |
| 2-3 hours/day on manual reporting | 0 hours — fully automated |

---

## Customization Guide

This system is designed to be easily adapted for any e-commerce client:

- **Swap data source:** Replace the test webhook with a real WooCommerce/Shopify webhook — zero workflow changes needed
- **Add ad platforms:** Add rows to the Ad Spend tab for TikTok Ads, Pinterest Ads, etc.
- **Adjust thresholds:** Change the Router filter values in WF4 to match the client's targets
- **Add alerts:** Add more Router paths for metrics like conversion rate drops or revenue targets
- **Scale:** Works for stores doing 10 orders/day or 10,000 orders/day

---

## Sample Alert (Slack)

```
ROAS ALERT — Ads Are Losing Money!

Date: 2026-03-23
ROAS: 1.5 (Threshold: 2.0)
Ad Spend: $445
Ad Revenue: $356

You spent more on ads than you earned back.
Consider pausing underperforming campaigns.
```

---

## Author

**Muaaz Siddique**

AI Automation Specialist | Make.com and n8n Workflows | RAG Chatbots | Business Process Automation

- GitHub: [github.com/muaazsiddique](https://github.com/muaazsiddique)
- Upwork: [Available for hire](https://www.upwork.com/freelancers/muaazsiddique)

---

## License

This project is available for reference and portfolio purposes. For commercial implementation, please contact the author.
