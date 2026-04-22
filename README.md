# SaaS Implementation Tracker

A fully connected Google Sheets template for managing SaaS customer onboarding — built to demonstrate how implementation teams can replace disconnected spreadsheets with a single, formula-driven tracking system.

Built by **Amitesh Anirudhan** as a portfolio project for implementation and customer onboarding roles.

---

## What It Does

Tracks the full customer implementation lifecycle across 5 connected sheets:

| Sheet | Purpose |
|---|---|
| 📊 Dashboard | Live KPI cards + customer overview table — auto-updates from all sheets |
| 🗂 Customers | Master customer registry — single source of truth |
| 🏁 Milestones | Phase-by-phase milestone tracking per customer |
| ✅ Action Items | Task log with owner, due date, priority, and overdue alerts |
| 📈 Progress | Phase completion heatmap — auto-calculated from Milestones |

---

## How The Sheets Connect

All sheets are linked via VLOOKUP and COUNTIFS formulas — no manual copy-pasting between tabs.

```
🗂 Customers (master)
        │
        ├──► 🏁 Milestones   (customer dropdown pulls from Customers)
        │           │
        │           └──► 📈 Progress   (COUNTIFS on Milestones per phase per customer)
        │
        ├──► ✅ Action Items  (customer dropdown pulls from Customers)
        │
        └──► 📊 Dashboard    (pulls stage, go-live from Customers
                               + milestone counts from Milestones
                               + open action count from Action Items
                               + overall % from Progress)
```

**Add a customer once in 🗂 Customers → every other sheet updates automatically.**

---

## Key Features

- **Live Dashboard** — KPI cards for total customers, active implementations, average progress, and overdue action count — all formula-driven
- **Phase Progress** — Completion % per implementation phase (Discovery → Configuration → Data Migration → Training → UAT → Go-Live) calculated automatically via COUNTIFS
- **Overdue Alerts** — Action items past their due date that are not marked Complete highlight red automatically via conditional formatting
- **Dropdown Validation** — Customer names, stage, status, and priority fields all use validated dropdowns to keep data clean
- **Color Scale** — Progress sheet uses a red → amber → green heat map based on phase completion %

---

## How To Use

### Add a new customer
1. Go to **🗂 Customers** → add a new row with name, contract date, go-live target, stage, and CSM owner
2. Go to **🏁 Milestones** → add milestone rows, selecting the customer name from the dropdown
3. Go to **✅ Action Items** → log first action items from the kickoff call
4. Go to **📈 Progress** → add a new row referencing the customer from Customers sheet
5. **📊 Dashboard** reflects everything automatically

### Update progress
- Change a milestone status to `Complete` in 🏁 Milestones → Progress % updates automatically
- Mark an action item `Complete` in ✅ Action Items → open action count on Dashboard drops automatically

---

## Tech

- **Google Sheets / Excel** (.xlsx — open directly in Google Sheets via File → Import)
- **Formulas used:** VLOOKUP, COUNTIFS, COUNTIF, COUNTA, AVERAGE, IFERROR, TODAY, AND
- **Features:** Data validation dropdowns, conditional formatting (color scale, data bars, formula-based rules)
- **Built with:** Python (openpyxl) + AI-assisted prototyping

---

## Enhancements Roadmap

- [ ] Google Apps Script — auto-email reminders for overdue action items
- [ ] Google Forms integration — customers self-report status, feeding directly into tracker
- [ ] Python script — auto-generate weekly PDF status report from sheet data
- [ ] Web app version — React frontend with persistent storage

---

## About

Built as part of a portfolio to demonstrate implementation tooling skills — specifically the ability to design systems that eliminate manual work, connect data across workstreams, and scale onboarding operations.

**Amitesh Anirudhan**
- GitHub: [github.com/amitesh0109](https://github.com/amitesh0109)
- LinkedIn: [linkedin.com/in/amitesh-anirudhan-951807193](https://linkedin.com/in/amitesh-anirudhan-951807193)
