# Workflow 3: Daily Metrics Aggregator

## Overview
Aggregates all daily orders and ad spend into one summary row on the Daily Dashboard.

## Architecture
[Search Orders] → [Sum Revenue] → [Search Ad Spend] → [Sum Spend] → [Write Dashboard Row]

## Metrics Written
- Total Orders, Total Revenue, Avg Order Value
- Total Ad Spend, Total Ad Revenue
- ROAS, CPA, Click-Through Rate

## Status: COMPLETE