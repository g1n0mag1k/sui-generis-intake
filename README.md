# Client intake form

A single static page (`index.html`) covering intake for both Deal Unlocker
and the AI Data Exposure Register, using [Netlify Forms](https://docs.netlify.com/forms/setup/)
for submission handling — no backend, database, or server code required.

## What it does

- One form, branded to match the Reviewer Brief / Gap Register document
  design (same navy/accent palette).
- A service picker (Deal Unlocker vs. AI Data Exposure Register) toggles
  service-specific fields with vanilla JS — no framework dependency.
- Submits via `fetch()` to Netlify's form endpoint and shows an inline
  success/error banner, so there's no page navigation or separate
  thank-you route to maintain.
- Honeypot field (`bot-field`) for basic spam filtering — standard Netlify
  Forms pattern, no extra config needed.
- The "referred by a law firm" field is explicitly labeled as being for
  referral credit, not a request for the referring firm's own client
  list — consistent with the ABA Rule 1.6 guardrail (never ask law firms
  for client lists).

## Deploying

**Fastest path — drag and drop:**
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop).
2. Drag this folder in. Netlify auto-detects the `<form data-netlify="true">`
   in `index.html` and wires up form handling — nothing else to configure.
3. Once deployed, go to **Site settings → Forms → Form notifications** and
   add an email notification (or a Slack/webhook one) so submissions reach
   you — otherwise they only show up in the Netlify dashboard.

**Git-connected path (recommended for the long run, so edits are versioned):**
1. Push this folder to its own repo (or a subfolder of an existing one —
   point Netlify's "base directory" at it if so).
2. In Netlify: **Add new site → Import an existing project** → connect
   the repo. Build command: none. Publish directory: `.` (or the subfolder).
3. Same form-notification step as above.

## After a submission comes in

Every submission is a new lead, not a client yet. Per the engagement
guardrails: nothing about a questionnaire answer or AI tool finding gets
sent anywhere until the client has reviewed and approved it — this form
only captures scoping information to start that conversation.

## Customizing

- Field labels/options live directly in `index.html` — no templating
  layer, intentionally, so there's nothing extra to learn to tweak a field.
- To add a third service later, duplicate a `.service-opt` block and its
  matching `.hidden-section`, and extend the JS `sections` map.
