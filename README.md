# Overdue Invoice Tracker — SAP Fiori Elements App

A full-stack SAP portfolio project demonstrating end-to-end development from database layer to production-ready Fiori UI, built on the SAP BTP Trial environment.



## 🎥 Demo Video
Link: https://www.youtube.com/watch?v=Wv9wMGzD9ro


## Business Problem

Finance teams lose visibility into overdue receivables when invoice aging isn't
surfaced clearly at the point of daily work. This app gives AR teams an
at-a-glance, color-coded view of every overdue invoice — sorted by severity —
so collections follow-up is prioritized correctly instead of chased manually
through spreadsheets or SAP GUI list reports.

## Architecture

```
Custom DB Table (ZINV_HEADER)
        ↓
Interface CDS View (ZI_OVERDUE_INVOICE)
        ↓
Consumption CDS View (ZC_OVERDUE_INVOICE) — UI annotations, criticality logic
        ↓
OData V4 Service (auto-exposed via @OData.publish)
        ↓
Fiori Elements List Report / Object Page
```

This follows SAP's recommended layered CDS architecture: interface views stay
UI-agnostic and reusable, while the consumption view carries all `@UI` and
`@Semantics` annotations that drive the Fiori Elements rendering — keeping the
data model cleanly separated from presentation concerns.

## Key Technical Feature: Criticality-Driven Status Coloring

Rather than a static status field, days-overdue is calculated inline in the
CDS view and mapped to SAP's semantic criticality model, so the Fiori list
report automatically renders color-coded status chips with zero front-end
code:

```abap
@Semantics.criticality: true
    case
        when DaysOverdue > 30 then '1'   " Negative — red
        when DaysOverdue > 0  then '2'   " Critical — yellow
        else '3'                          " Positive — green
    end as Criticality
```

| Days Overdue | Criticality Code | Rendered Color |
|---|---|---|
| > 30 days | 1 | 🔴 Red (Negative) |
| 1–30 days | 2 | 🟡 Yellow (Critical) |
| Not overdue | 3 | 🟢 Green (Positive) |

## Tech Stack

- **ABAP CDS Views** (Interface + Consumption layers)
- **OData V4** service exposure
- **SAP Fiori Elements** (List Report + Object Page floorplan)
- **SAP BTP Trial** — ABAP Environment (Steampunk)
- **Eclipse ADT** for development

## Screenshots

| List Report — Overdue Invoices | Object Page Detail |
|---|---|
| ![List Report](./screenshots/list-report.png) | ![Object Page](./screenshots/object-page.png) |

<!-- Add more rows/screenshots as needed: filters, sort, criticality colors close-up -->

## What This Project Demonstrates

- Custom database table design and activation in a Steampunk (cloud ABAP) environment
- Layered CDS view architecture (interface vs. consumption)
- OData service generation and annotation-driven UI (no manual front-end coding)
- Semantic criticality mapping for business-meaningful visual cues
- End-to-end delivery: data model → service → live Fiori app

## Author

**Sharfunisa Shajahan (Nisha)** — SAP ABAP Developer, 3.5+ years SAP experience
(SD/MM/FICO/HR/MDG) at Infosys, now focused on Fiori/UI5/CDS development.

[LinkedIn](#) · [Portfolio](https://nishaweb-developer.github.io/myworks) · [Email](#)
