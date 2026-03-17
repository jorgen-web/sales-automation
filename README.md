# Game Release Prospecting Automation

Automated sales prospecting pipeline that monitors upcoming game releases and triggers targeted outreach sequences for advertising partnerships. Built with **n8n**, **SerpAPI**, and the **Claude API**.

---

## What It Does

The workflow continuously monitors game release schedules and automatically identifies high-potential advertising prospects — gaming studios launching titles across PC, console, and mobile. When a qualifying release is detected, it enriches the lead with relevant metadata and prepares a personalized outreach sequence, reducing manual research from hours to minutes per prospect.

## Problem It Solves

Gaming advertisers have short, high-stakes launch windows. Identifying the right studios at the right moment — before and during a game launch — requires constant monitoring of release calendars, press releases, and gaming news sources. This pipeline automates that signal detection so outreach can happen at the optimal time.

## Stack

| Tool | Role |
|------|------|
| **n8n** | Workflow orchestration and automation |
| **SerpAPI** | Game release and studio discovery via structured search |
| **Claude API (Anthropic)** | Lead qualification, relevance scoring, and outreach copy generation |
| **HTTP Request nodes** | External data enrichment |
| **n8n Cron trigger** | Scheduled monitoring cadence |

## How It Works

1. **Trigger** — Scheduled cron runs on a defined cadence
2. **Discovery** — SerpAPI queries surface upcoming game releases and new studio announcements
3. **Qualification** — Claude API evaluates each result for advertiser fit (budget signals, genre, platform, audience size)
4. **Enrichment** — Studio metadata is appended (website, social, recent news)
5. **Output** — Qualified leads are formatted and routed for outreach or CRM entry

## Business Impact

- Reduced manual prospecting time significantly per week
- Enables outreach during the highest-intent window (pre-launch and launch week)
- Scales across genres, platforms, and regions without additional headcount

## Setup

1. Clone this repo
2. Import the `.json` workflow file into your n8n instance
3. Add your credentials:
   - `SERPAPI_KEY` — [SerpAPI](https://serpapi.com)
   - `ANTHROPIC_API_KEY` — [Anthropic Console](https://console.anthropic.com)
4. Activate the workflow

> **Note:** Credentials are not included in the exported workflow. n8n strips them automatically on export.

## File Structure

```
/
├── game-release-prospecting.json   # Main n8n workflow
├── README.md
```

---

*Built to support programmatic advertising sales at scale in the gaming vertical.*

