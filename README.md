# Barberoji: barbershop management system (read-only demo)

A management system I designed for a real men's barbershop and barbering academy, covering finance, payroll, courses, invoices, leads, marketing and personal management. This repository documents the demo version, which runs on fully synthetic data (Sep–Nov 2026) and is read-only, so anyone can explore it safely.

Live demo: https://barberoji-demo.lovable.app

> The data is invented. The structure, screens and business rules follow the real system, but no figure here comes from the real business.

## The problem

A small business ran on spreadsheets and memory: nobody could say quickly how much profit was left after VAT, barber revenue shares, bonuses and personal obligations, or whether the month was on track to break even. I mapped the process, defined the business rules and had the system built around them.

## What it does

| Area | What the owner sees |
|---|---|
| Home | Month at a glance: pending leads, active course cohorts, open marketing ideas, break-even progress |
| Finance | Monthly P&L, VAT, barber payroll, management bonus, break-even; Excel export and print report |
| Barbershop | Revenue per barber by week; "net to you" after bonuses and extras |
| Academy | Beginner/advanced cohorts (one start date per cohort), students, capacity, course revenue |
| Leads | Pipeline by source; pending = new / cooled / follow-up / call scheduled |
| Marketing | Spend by channel, cost per enrolled student, content ideas |
| Invoices | Invoices pending to send, per month |
| Personal | Weekly habit metrics (out of 7) and a self-score |

## Business rules (the part I designed)

* All prices include 18% VAT: `VAT = gross × 18/118`.
* Barber payroll = `revenue ÷ 1.18 × share` (50% or 60% per barber).
* A monthly management bonus and per-employee extras are deducted before the owner's profit.
* Owner's remaining cash = business profit − household, personal and loan obligations.
* Break-even revenue = `fixed costs ÷ (1 − payroll ratio − VAT ratio)`.
* Closed months are locked against edits; course capacity and stock levels are enforced in the database.

## Tech

TanStack Start + TypeScript + Tailwind/shadcn UI, Supabase (PostgreSQL) with row-level security. Built with Lovable and Claude; the process design, rules, validation and test data are mine.

Read-only demo mode: restrictive RLS policies block writes for the demo user, and a client-side guard returns a clear "demo" message instead of silently failing. A fixed demo clock makes "today" 12 Nov 2026, so the numbers never go stale.

## Quality checks

Before publishing, I audited the demo in a headless browser for every tab and month: figures vs. the database, no console errors, Excel export and print report reconciled to the finance screen (e.g. Sep/Oct/Nov gross revenue ₪127,328 / ₪137,790 / ₪58,265).

## Companion analysis

[`barbershop-analytics`](https://github.com/yammerjan/barbershop-analytics): Python + SQL notebook that analyses the same demo data (break-even, barber contribution, lead conversion with a permutation test, Monte Carlo forecast).

---
Yam Merjan, Industrial Engineering and Management student.
