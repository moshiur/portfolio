# Guest self-check-in kiosk and back-office

**2026 · hospitality client · web kiosk, regulated guest registration, provider integration, ops tooling**

Guests arriving at a hospitality property check themselves in at an unattended terminal in the
entrance. The system collects what the law requires for guest registration, files it with the
national guest-registration and tourist-tax system, and gives reception a staff app to see and
fix what came in.

Two hard parts: the terminal has to keep working with nobody watching it, and the registration
has to be *legally* right, not merely present.

**In production since late August 2026.** One property with a single unattended terminal plus the
reception app — roughly 74 check-ins and 145 registered people in the first three weeks. The data
model is multi-property from the start; property and terminal identities are first-class.

## Stack

- **Backend** — TypeScript on Node, serverless handlers behind a managed HTTP API. Zod for schema
  validation, ULIDs, JWT for staff sessions, XML over HTTPS towards the registration provider.
- **Frontend** — Vue 3, Vite, TypeScript, Tailwind, vue-i18n in three languages (DE/EN/NL). One
  codebase serves both surfaces: the guest wizard and the reception app.
- **Kiosk runtime** — a Linux desktop running Chromium in kiosk mode from an autostart entry, with
  a USB keyboard. The app is served from the CDN; the device runs no local server.
- **Data** — a single managed NoSQL table in single-table design: registrations, per-property
  provider config snapshots, terminal identities, number-block inventory, idempotency records and
  a staff audit trail. No cache tier and no queue — provider config is cached as rows in the same
  table, a scheduled rule fires the nightly job, alarms fan out through a notification topic.
- **Infrastructure** — serverless functions, a managed HTTP API, object storage plus CDN for the
  single-page app, managed user pools for staff sign-in, parameter store for integration secrets,
  and metrics, alarms and dashboards built from what the application logs. All of it is TypeScript
  infrastructure-as-code (~1.8k lines).
- **Repo** — a monorepo with npm workspaces: frontend, backend, a shared contract package (the Zod
  schemas both sides import, so they cannot drift), and infrastructure. ~71k lines across 431
  files: ~33k source, ~30k tests, ~3k operational scripts.
- **Tests** — ~1,300 Vitest unit and component tests, one Playwright end-to-end spec, and 9
  golden-XML fixtures pinning the exact payload format the provider expects.
- **Delivery** — pull requests run lint, type-check and the full suite. Production needs a version
  tag on the release branch, a green run, then a manual approval, so merging never deploys. Cloud
  access is federated through OIDC; no long-lived keys in the repo. 21 releases went out between
  early August and mid-September 2026.

## Single-use registration numbers under concurrency

The authority issues registration numbers in blocks. Each number is legally single-use, and a
cancelled one stays consumed — so a double submit, or a retry that quietly burns a second number,
is a real defect and not a cosmetic one.

An allocator over conditional writes on the table hands out numbers, and every submission carries
an idempotency record: a repeated submit returns the original registration instead of consuming
inventory. Blocks refill from the provider before they run out.

## A provider that reports failure with HTTP 200

Roughly 70 business error codes arrive inside a *successful* HTTP response. The right reaction
differs per code — confirm, retry now, park for the nightly retry, or fail terminally — so the
codes are mapped into eight semantic buckets behind those four actions. A wrong bucket is
expensive in both directions: either a legally required registration is dropped, or the same
doomed request is re-sent every night forever.

## When the integration is the one that's wrong

The clearest production incident: certain registrations began refusing every further update from
our interface — permanently — and the nightly departure job retried them until its time window
expired, one alarm per night.

Correlating our logs against the provider's change history showed the pattern. It happened only
to records that someone had edited by hand in the **provider's own web client**, a path we did not
control and had not been told about. The fix had two halves: treat that code as terminal instead
of retryable, so the job stops fighting it, and then remove the cause — let reception add a
missing person through our own interface, proven first against the vendor's test tenant, so
nobody needs the web client.

The lesson worth keeping: when a third-party integration fails, the first job is to prove which
side is wrong, with data, before either side starts guessing.

## The terminal has no operator

An unattended terminal has to reset an abandoned check-in, dim itself overnight, and pick up new
releases without a person pressing reload. That last one was visible in production: a deployed
improvement sat unused until someone happened to refresh the browser at the desk.

The device now polls the entry document and reloads itself — but only while the welcome screen is
showing, never mid check-in and never with a warning dialog open, and with a cooldown that rules
out reload loops.

## Registration data has to be legally correct

Ordinary web-form thinking is not enough when the form is a legal document:

- **Guest categories and age bands differ per municipality**, and country-code tables differ per
  property country. Both are fetched from the provider and cached, never hard-coded.
- **Identity fields lock** once a registration has been transmitted successfully. After that, a
  change is a correction to a filing that already exists, not a fresh one.
- **Retention is enforced in the data**, as a row-level expiry of seven years plus a margin.
- **No guest data in logs** — asserted by tests that check log lines carry no guest fields.
- **Two-digit years** typed on a touch keyboard resolve their century from the field's own bounds
  rather than a pivot year. Where both centuries are legitimate — a companion field spanning 115
  years — the more recent wins, and the resolved year is shown back to the guest.

## What was mine

Architecture and effectively all backend, infrastructure and release engineering from the
mid-2026 rebuild onward: the provider adapter and its error taxonomy, persistence and the
concurrency model (idempotent commands, compare-and-set on a revision token, audit before
complete), the reception app, kiosk reliability, the CI/CD pipeline and every production release.
Plus production operations — alarm triage and incident analysis — and the decision records and
integration documentation. Also the direct line to the integration vendor, the registration
authority and the customer, which is where several of the constraints above came from.

Others contributed: an engineer scaffolded the repository, two working students and a developer
built frontend components, form models, locales and tests, and the CTO owns the hardware and
device-lockdown decisions. Two pieces — part of the staff-operations feature and the kiosk reload
mechanism — were implemented by an AI coding agent against a specification I wrote and reviewed;
the diagnosis and the design behind both were mine.

**Skills:** unattended-kiosk reliability, regulated data modelling, third-party integration and
incident diagnosis under production pressure, idempotency and concurrency on a NoSQL store,
serverless infrastructure-as-code, gated release pipelines, frequent shipping with production
support.
