# Game Release Prospecting & Outreach Automation

A two-part automated sales pipeline that monitors upcoming game releases, identifies high-potential advertising prospects, finds the right contacts, and prepares them for outreach. Built with **n8n**, **SerpAPI**, **Google Sheets**, and the **Claude API**.

---

## Overview

Gaming advertisers operate in short, high-stakes launch windows. Identifying the right studios at the right moment — and finding the right person to contact — requires constant monitoring of release calendars and manual research. This pipeline automates both, from initial discovery through contact enrichment.

---

## Workflow 1 — Game Release Prospecting

**File:** `Game_Release_Prospecting_Workflow.json`

Monitors upcoming game releases and scores them for advertising potential.

### How It Works

1. **Trigger** — Scheduled cron runs on a defined cadence
2. **Discovery** — SerpAPI queries surface upcoming game releases and new studio announcements
3. **Qualification** — Claude API evaluates each result for advertiser fit (budget signals, genre, platform, audience size)
4. **Enrichment** — Studio metadata is appended (website, social, recent news)
5. **Output** — Qualified prospects are written to a Google Sheet for the contact workflow to process

---

## Workflow 2 — Game Release Contact Finder

**File:** `Game_Release_Contact_Workflow.json`

Runs every 48 hours against the prospect sheet and finds the right contacts at each studio.

### How It Works

1. **Trigger** — Runs every 48 hours automatically
2. **Read** — Pulls uncontacted prospects from Google Sheets
3. **Loop** — Iterates through each prospect individually
4. **Search** — SerpAPI searches LinkedIn and the web for marketing directors, heads of marketing, and UA contacts at each studio
5. **Extract** — Claude API parses search results and extracts structured contact data (name, role, profile URL)
6. **Update** — Google Sheets is updated with contact details and logged to a separate contact details tab

---

## Stack

| Tool | Role |
|------|------|
| **n8n** | Workflow orchestration and automation |
| **SerpAPI** | Game release discovery and contact search |
| **Claude API (Anthropic)** | Lead qualification, relevance scoring, contact extraction |
| **Google Sheets** | Prospect and contact data storage |
| **n8n Cron / Schedule trigger** | Automated cadence for both workflows |

---

## Business Impact

- Reduces manual prospecting and contact research from hours to minutes per week
- Enables outreach during the highest-intent window — pre-launch and launch week
- Surfaces the right decision-makers (marketing directors, UA leads) automatically
- Scales across genres, platforms, and regions without additional headcount

---

## Setup

1. Clone this repo
2. Import both `.json` workflow files into your n8n instance
3. Add your credentials in n8n:
   - `ANTHROPIC_API_KEY` — [Anthropic Console](https://console.anthropic.com)
   - `SERPAPI_KEY` — [SerpAPI](https://serpapi.com)
   - `Google Sheets OAuth2` — connect via n8n Google Sheets credentials
4. Update the Google Sheet ID in Workflow 2 to point to your own sheet
5. Activate both workflows — run Workflow 1 first to populate prospects, then Workflow 2 to enrich contacts

> **Note:** All credentials have been removed from the exported workflow files. n8n stores credentials separately and strips them on export.

---

## File Structure

```
/
├── Game_Release_Prospecting_Workflow.json   # Workflow 1 — discovery & qualification
├── Game_Release_Contact_Workflow.json       # Workflow 2 — contact enrichment
└── README.md
```

---

*Built to support programmatic advertising sales at scale in the gaming vertical.*
