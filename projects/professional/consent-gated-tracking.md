# Consent-gated marketing tracking on a real-estate website

**September 2026 · Nuxt 4 site, AWS Amplify hosting, Cookiebot consent · sole engineer**

An Austrian real-estate agency wanted marketing measurement on its public website: web
analytics, search-ads conversions, a social pixel and an AI-ads pixel. The constraint was
that nothing may load or set a cookie before the visitor agrees in the consent banner.

## What I built

- **Four tags behind consent**, each rendered as a blocked script and released by the
  consent platform only for its own category: analytics after "statistics", the three
  advertising tags after "marketing". No tag manager: the tags are in the codebase, so a
  change goes through review and release like any other code.
- **A tag renders only when its id is configured**, and a malformed id fails the build.
  Production ids live in the hosting environment for the production branch alone, so test
  builds physically cannot send data to live accounts.
- **Six conversion events**, wired from the real UI: form submissions, brochure requests,
  booking and phone and e-mail clicks, plus a "visitor stayed over two minutes" event that
  fires once per browser tab, survives in-page navigation, and reports late if consent is
  given after the two minutes have passed.
- **Withdrawal handling.** Consent platforms cannot unload a script that is already
  running. Each pixel gets its own switch driven by the consent events, and the page
  reloads once when a visitor takes back a consent they had given, after which everything
  is blocked again.

## How it was verified

Manual clicking does not scale to four tags in two languages with six consent paths, so I
wrote a **headless-browser harness** driving the real consent banner over the DevTools
protocol. Per run it records every network request, the consent state, which scripts are
active, cookies and page-view counts, and writes screenshots plus a JSON trace.

Scenarios: before any choice, decline, statistics only, allow all, late consent,
in-page navigation, reload, withdrawal, consent again — German and English, against test
ids so no live account is touched.

## What it caught

The test environment used placeholder ids, which behave subtly differently from live
ones. After go-live I ran the same harness against production and found that **after a
visitor withdrew consent, the analytics and ads tags kept sending page views on in-page
navigation** — cookieless and flagged as "denied", but still leaving the browser until the
next full page load. Placeholder ids never showed it, because they have no property
settings to trigger those page views.

I wrote it up, built the reload fix, tested it locally against the real banner, shipped it
as a patch release the same evening, and re-verified on the live site in both languages:
one reload on withdrawal, then nothing sent at all. Documentation that had claimed those
tags "stop on their own" was corrected, since it had been written from the placeholder-id
tests.

## Outcome

Two releases in one evening, roughly five minutes from push to live each time. Every
consent path evidenced with screenshots and request traces, which is what a data-protection
review actually asks for. The measurement gap between finding and fixing was about an hour.

**Skills:** Nuxt/Vue, TypeScript, consent and privacy engineering (GDPR, Consent Mode),
GA4 and ads pixels, CI/CD on AWS Amplify, browser automation for test evidence, release
management, technical writing for non-technical stakeholders.
