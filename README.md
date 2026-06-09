# HITL 1-on-1 Tool — Setup Guide

## What's in this folder

| File | Purpose |
|---|---|
| `index.html` | The web app (open in browser or deploy to GitHub Pages) |
| `Code.gs` | Google Apps Script backend (connects to Google Sheets) |

---

## Step 1 — Deploy the Google Apps Script (Backend)

1. Go to [script.google.com](https://script.google.com) → **New Project**
2. Delete the default code and paste everything from `Code.gs`
3. Click **Deploy → New Deployment**
4. Set:
   - Type: **Web App**
   - Execute as: **Me**
   - Who has access: **Anyone** (so all leads can submit)
5. Click **Deploy** → Copy the **Web App URL**

The script will auto-create 3 sheets in your active Google Spreadsheet:
- `Sessions` — all 1-on-1 form data
- `ActionItems` — all action items with status
- `History` — cross-quarter summary for follow-ups

---

## Step 2 — Deploy the Frontend (GitHub Pages)

1. Create a new GitHub repo (e.g. `hitl-one-on-one`)
2. Upload `index.html` to the root
3. Go to **Settings → Pages → Deploy from branch → main**
4. Your URL will be: `https://your-org.github.io/hitl-one-on-one/`

Share this URL with all team leads.

---

## Step 3 — Connect the App to Google Sheets

1. Open the deployed app URL
2. Click **Settings** in the top nav
3. Paste your **Apps Script Web App URL**
4. Click **Save & Test Connection** — you should see ✅ Connected
5. Enter your name under **Default Lead Name** and save

Each lead does Step 3 once on their browser. After that, all sessions sync to the shared Google Sheet automatically.

---

## How it works for Q3 Follow-up

When a lead opens a new session for a member who was done in H1:
- The **Historical Context panel** automatically appears
- It shows the previous rating, mood, goal status, and the "one change" they requested
- Open action items from H1 are also surfaced

In Google Sheets, just filter by `quarter` column = `H1 2026` to see all H1 data, or `Q3 2026` for the next round.

---

## Data Flow

```
Lead fills form → index.html
      ↓
Saves locally (localStorage) — works offline
      ↓
If connected → POST to Apps Script
      ↓
Apps Script writes to Google Sheet (Sessions + ActionItems + History tabs)
      ↓
All leads share the same Sheet → centralised data
```

---

## Troubleshooting

| Issue | Fix |
|---|---|
| CORS error on connection test | Redeploy the Apps Script — ensure "Anyone" access |
| Data not showing for other leads | Make sure everyone has connected to the same Apps Script URL |
| Form resets on refresh | This is by design — data is saved on Submit, not on field change |

---

*Built for Meltwater HITL Content Team — H1 2026 1-on-1 cycle*
