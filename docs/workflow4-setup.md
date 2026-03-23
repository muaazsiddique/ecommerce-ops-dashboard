# Workflow 4: Smart Alerts Engine

## Overview
Checks Daily Dashboard metrics against thresholds and sends Slack alerts when KPIs are in danger zones.

## Architecture
[Search Dashboard] → [Router] → Path 1: Low ROAS → Slack + Log
                              → Path 2: Low Orders → Slack + Log
                              → Path 3: High CPA → Slack + Log

## Alert Thresholds
| Alert | Condition | Action |
|-------|-----------|--------|
| Low ROAS | ROAS < 2.0 | Slack warning: ads losing money |
| Low Orders | Orders < 3 | Slack warning: sales dropped |
| High CPA | CPA > $15 | Slack warning: acquisition cost too high |

## Status: COMPLETE