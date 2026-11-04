# Barberoji: barbershop management system (read-only demo)

A management system I designed for a real men's barbershop and barbering academy, covering finance, payroll, courses, invoices, leads, marketing and personal management. This repository documents the demo version, which runs on fully synthetic data (Sep–Nov 2026) and is read-only, so anyone can explore it safely.

Live demo: https://barberoji-demo.lovable.app

> The data is invented. The structure, screens and business rules follow the real system, but no figure here comes from the real business.

## The problem

The barbershop and its academy ran the way most small barbershops still do: no management system at all. Revenue, payroll, expenses, leads and course enrolments lived in a paper notebook and in phone messages. Nothing connected them, so the owner could not answer the basic questions of running a business:

* How much does the business really earn, and from which source: haircuts, courses or products?
* Where is money leaving for no good reason?
* Which marketing spend actually brings in students, and what does one enrolled student cost?
* What is truly left after VAT, barber revenue shares, bonuses and personal obligations?
* Is this month on track to break even, and which barber is worth pushing to hit higher targets?

Without those answers, decisions were made on gut feeling and the real profit was only discovered, if ever, after the month had ended. This was not a software problem. It was a management problem: no visibility, no tracking of tasks, leads or marketing, and no way to organise services, products and staff in one place.

Barberoji is the fix. I mapped how the business actually works, turned it into explicit rules (VAT, revenue splits, bonuses, break-even), and built one system where every shekel, lead, student and barber's weekly haircut count is recorded once and the numbers that matter are calculated automatically.

## Screenshots

The system is in Hebrew (right to left). All figures are synthetic.

| Home (October) | Finance (October) |
|---|---|
| <img src="https://barberoji-demo.lovable.app/screenshots/home.png?v=2" alt="Home screen"> | <img src="https://barberoji-demo.lovable.app/screenshots/finance.png" alt="Finance screen"> |
| Month selector, break-even progress, open tasks, pending leads | Monthly P&L, VAT, payroll, what is left for the owner |

| Barbershop (October) | Academy (November) |
|---|---|
| <img src="https://barberoji-demo.lovable.app/screenshots/barbershop.png" alt="Barbershop screen"> | <img src="https://barberoji-demo.lovable.app/screenshots/academy.png" alt="Academy screen"> |
| Owner's net after bonuses and extras, per-barber targets | Course cohorts, students, course income |

| Marketing (October) |
|---|
| <img src="https://barberoji-demo.lovable.app/screenshots/marketing.png" alt="Marketing screen" width="60%"> |
| Spend by channel, cost per enrolled student, content ideas and shoot days |

## What it does

| Area | What the owner sees |
|---|---|
| Home | Month at a glance: pending leads, active course cohorts, open marketing ideas, break-even progress |
| Finance | Monthly P&L, VAT, barber payroll, management bonus, break-even; Excel export and print report |
| Barbershop | Revenue per barber by week; "net to you" after bonuses and extras |
| Academy | Beginner/advanced cohorts (one start date per cohort), students, capacity, course revenue |
| Leads | Pipeline by source; pending = new / cooled / follow-up / call scheduled |
| Marketing | Spend by channel, cost per enrolled student, content ideas |
| Invoices | Upload invoices (photo or file) and track which are pending, per month. Pending invoices are emailed to the accountant automatically on the 30th of each month at 09:00 (last day of the month in February), and marked as sent |
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
