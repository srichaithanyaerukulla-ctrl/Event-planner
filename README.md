# Gatherly — final hosting package

Gatherly is a deterministic event-planning MVP. It does **not** use or require an AI model, model training, external AI APIs, or model credentials. Its event-plan endpoint combines editable planning rules with a searchable catalogue of 1,000 predefined operational measures.

## What is included

- Responsive workspace: overview, planning timeline, budget tracker, vendor pipeline, guest list, and change-impact preview.
- Event setup for weddings, birthdays, and community events.
- Local browser persistence plus JSON workspace and CSV budget/guest exports.
- Netlify Functions for deterministic plan generation and health status.
- Exactly 1,000 uniquely identified measures across 25 domains, including 120 event-type-specific measures.
- Search and domain filtering across the full catalogue; event-specific recommendations are selected from 12 distinct domains.
- Automated validation suite (`npm test`) with no third-party package dependencies.

## Deploy on Netlify

1. Extract this ZIP. The folder containing `netlify.toml`, `package.json`, `public/`, and `netlify/` is the project root.
2. Push that folder's contents to a GitHub repository, or use Netlify's manual deploy for a static-only preview. **For plan generation, deploy through Git-based Netlify or Netlify CLI so Functions are included.**
3. In Netlify, choose **Add new project → Import from Git** and select the repository.
4. Use the included settings: publish directory `public`, functions directory `netlify/functions`, and no build command required.
5. Deploy. No environment variables or AI credentials are required.
6. Verify the deployed site, `/.netlify/functions/health`, and `/.netlify/functions/plan`.

## Local development and tests

- Static preview: `python -m http.server 8000 --directory public`
- Run the automated checks: `npm test` (Node.js 20+ recommended).
- To test Netlify Functions locally, install the Netlify CLI and run `netlify dev` from this project root.

## Data and privacy model

The MVP stores its workspace in the current browser's `localStorage`. It does not sync data to a server or share data across devices. Workspace data can be exported by the organizer. Avoid entering sensitive guest information.

Before onboarding real customers, add authentication, a durable database, per-user authorization and data isolation, backups, retention/deletion controls, rate limits, monitoring, and an independent security/privacy review. The current package is not a production multi-tenant SaaS.

## Scope and limitations

- Vendor names, quotes, availability, reviews, venue capacity, and local legal requirements are not looked up or verified by Gatherly.
- Budget allocations and generated plans are editable planning assumptions, not professional advice or guaranteed prices.
- No payments, bookings, invitation delivery, messaging, or third-party account integrations are implemented.
- Safety, medical, accessibility, food-allergy, and permission measures are planning prompts. Confirm event-specific requirements with qualified professionals, venues, providers, and local authorities.

## The 1,000-measure catalogue

`public/data/gatherly_measures_1000.json` is the browser-served catalogue. `data/gatherly_measures_1000.json` is its source copy. Each record includes a stable ID, domain, applicable event type, scenario, action, rationale, priority, planning stage, trigger, and verification instruction. The catalogue contains 40 measures per domain across 25 domains. All 1,000 records have unique IDs and action text.

## Quality assurance

Run `npm test`. The suite validates the 1,000 records and required fields, domain coverage, three event-type plan flows, recommendation diversity, event-type matching, invalid input rejection, health endpoint, static asset presence, and initial app rendering. Static files were also served locally and returned HTTP 200 during the release check. See `QA_REPORT.md` for the recorded checks.

## Deployment status

This is a hosting-ready source package; it has **not** been published to a public URL. Publishing requires access to the owner's GitHub/Netlify account. Do not treat a successful local test as proof of a live deployment.
