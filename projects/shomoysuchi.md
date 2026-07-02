# ShomoySuchi

**"Untis for Bangladesh"** — an enterprise SaaS school-management and timetable-scheduling platform purpose-built for the Bangladeshi educational context (SSC/HSC exams, NCTB curriculum, MPO compliance).

🌐 **Live demo: [shomoysuchi-web.onrender.com](https://shomoysuchi-web.onrender.com/)** *(free-tier hosting — first load may take ~30 s to wake up)*

![ShomoySuchi principal dashboard](../assets/shomoysuchi/home.png)

## What it does

School principals and administrators manage timetables, attendance, substitutions, and student records in one place — with Bangla localization and an exam-countdown workflow tuned to the SSC calendar.

The headline feature is the **AI timetable scheduler**: a genetic-algorithm solver (with Gemini-assisted constraints) that generates conflict-free master timetables — the problem that commercial products like Untis solve for European schools, adapted to Bangladeshi constraints (shift-based schools, MPO teacher rules).

## Architecture

| Layer | Technology |
|---|---|
| Frontend | React 18, Vite, Tailwind CSS, PWA — 39 components, feature-gated views |
| Scheduling | Genetic-algorithm solver + Gemini AI service |
| Localization | Full Bangla i18n |
| Backend | .NET 10 Web API, PostgreSQL 16, Redis 7 |
| Deployment | Docker → Render (live), Caddy |

~32K lines of code, February–June 2026.

## Why it's interesting engineering-wise

- Timetabling is NP-hard — the genetic solver encodes hard constraints (no teacher in two rooms at once) and soft preferences (minimize gaps) with fitness scoring
- It's **deployed and public** — not a localhost project: PWA, Docker packaging, real hosting
- Localization-first product thinking: the target user is a school administrator in Dhaka, not a developer

[← Back to portfolio](../README.md)
