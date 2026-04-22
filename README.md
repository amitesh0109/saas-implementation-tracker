# SaaS Implementation Tracker

A fully connected, dynamic spreadsheet for managing SaaS customer onboarding, built to demonstrate how implementation teams can replace disconnected spreadsheets with a single, formula-driven tracking system.

Works in both **Microsoft Excel** and **Google Sheets** with no setup required.

Built by **Amitesh Anirudhan** | [github.com/amitesh0109](https://github.com/amitesh0109) | Built with Claude AI

---

## What It Does

Tracks the full customer implementation lifecycle across 5 connected sheets:

| Sheet | Purpose |
|---|---|
| 📊 Dashboard | Live KPI cards + customer overview updates automatically when customers are added |
| 🗂 Customers | Master customer registry single source of truth |
| 🏁 Milestones | Phase-by-phase milestone tracking per customer |
| ✅ Action Items | Task log with owner, due date, priority, and automatic overdue alerts |
| 📈 Progress | Phase completion heatmap auto-calculated from Milestones |

---

## How It Works

### Single source of truth
Add a customer once in 🗂 Customers. Every other sheet updates automatically, no manual copying, no duplicate data entry.

### Pre-populated formulas (works in Excel & Google Sheets)
All 20 customer slots in the Dashboard and Progress sheets are pre-filled with formulas. Empty slots stay blank until a customer is added. No QUERY functions pure COUNTIFS, VLOOKUP, and IF formulas that work identically in both Excel and Google Sheets.

### Data flow
```
🗂 Customers (master — add customers here)
        │
        ├──► 🏁 Milestones   (customer dropdown pulls from Customers)
        │           │
        │           └──► 📈 Progress   (COUNTIFS counts complete milestones per phase)
        │
        ├──► ✅ Action Items  (customer dropdown pulls from Customers)
        │
        └──► 📊 Dashboard    (IF + VLOOKUP pulls customer data per pre-populated row
                               + COUNTIFS for milestone counts and open actions
                               + Overall % pulled from Progress sheet)
```

---

## Key Features

- **Fully dynamic Dashboard** — pre-populated for 20 customers using IF/VLOOKUP formulas. Add a customer in the Customers sheet → Dashboard row fills in automatically
- **Phase Progress via COUNTIFS** — completion % per phase (Discovery → Configuration → Data Migration → Training → UAT → Go-Live) calculated automatically by counting Complete milestones per customer per phase
- **Overdue Alerts** — action items past their due date that are not marked Complete highlight red automatically via conditional formatting
- **Dropdown Validation** — customer names, stage, status, and priority fields use validated dropdowns to keep data clean
- **Color Scale** — Progress sheet uses red → amber → green heatmap per phase based on completion %
- **Live KPI Cards** — total customers, active implementations, average progress, and overdue action count all update automatically
- **Works in Excel & Google Sheets** — no QUERY functions, no Google Sheets-only features

---

## How The Key Formulas Work

### IF + VLOOKUP (Dashboard — pulls customer data per row)
```excel
=IF('🗂 Customers'!B5="", "", '🗂 Customers'!B5)
```
Each Dashboard row is linked to a specific Customers row. If the Customers row is empty, the Dashboard row shows blank. As soon as you add a customer name, the entire row populates automatically.

### COUNTIFS (Progress — phase completion %)
```excel
=IF($B6="", "", IFERROR(
  COUNTIFS(Milestones!Phase, "Configuration", Milestones!Customer, B6, Milestones!Status, "Complete")
  /
  COUNTIFS(Milestones!Phase, "Configuration", Milestones!Customer, B6)
, "-"))
```
Counts milestones where phase = "Configuration" AND customer = this row AND status = "Complete", divided by total milestones for that phase and customer. Updates live as you mark milestones complete in the Milestones sheet.

### Overdue Alert (Action Items — conditional formatting)
```excel
=AND($F6<>"Complete", $E6<TODAY(), $B6<>"")
```
Highlights a row red if: status is not Complete AND due date is in the past AND customer name is not empty.

### Dashboard Milestones Done
```excel
=IF(B11="", "", COUNTIFS(Milestones!Customer, B11, Milestones!Status, "Complete") & " / " & COUNTIF(Milestones!Customer, B11))
```
Shows as "3 / 7" — complete milestones out of total for that customer.

---

## How To Use

### Open the file
- **Google Sheets**: Go to [drive.google.com](https://drive.google.com) → New → File Upload → select the `.xlsx` → right-click → Open with Google Sheets
- **Excel**: Download and open directly

### Add a new customer
1. Go to **🗂 Customers** → type the customer name, contract date, go-live target, stage, and CSM owner in the next empty row
2. Go to **🏁 Milestones** → add milestone rows, selecting the customer from the dropdown
3. Go to **✅ Action Items** → log first action items from the kickoff call
4. **📊 Dashboard and 📈 Progress update automatically** — no extra steps

### Update progress
- Change a milestone status to `Complete` in 🏁 Milestones → Progress % and Dashboard milestone count update automatically
- Mark an action item `Complete` in ✅ Action Items → open action count on Dashboard drops automatically

---

## Tech

- **Google Sheets / Excel** (`.xlsx` — no setup required in either)
- **Formulas:** COUNTIFS, COUNTIF, COUNTA, VLOOKUP, IF, IFERROR, AVERAGEIF, TODAY, AND
- **Features:** Data validation dropdowns, conditional formatting (color scale, data bars, formula-based overdue rules)
- **Pre-populated:** 20 customer slots (extend by copying formulas down in Dashboard and Progress)
- **Built with:** Python (openpyxl) + Claude AI

---

## Enhancements Roadmap

- [ ] Google Apps Script — auto-email reminders for overdue action items
- [ ] Google Forms integration — customers self-report status updates directly into the tracker
- [ ] Python script — auto-generate weekly PDF status report from sheet data
- [ ] Web app version — React frontend with persistent storage

---

## About

Built as a portfolio project to demonstrate implementation tooling skills specifically the ability to design systems that eliminate manual work, connect data across workstreams, and scale customer onboarding operations.

**Amitesh Anirudhan**
- GitHub: [github.com/amitesh0109](https://github.com/amitesh0109)
- LinkedIn: [linkedin.com/in/amitesh-anirudhan-951807193](https://linkedin.com/in/amitesh-anirudhan-951807193)
