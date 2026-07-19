# Security Policy

This policy covers every repository in the HonorBox org. Thanks for looking —
MIT-licensed, zero-dependency code only works as a trust story if people
actually audit it, and we'd rather hear about a hole from you than from an
incident.

## Reporting a vulnerability

Use either channel — both reach the same people:

- **Email:** [honorbox@proton.me](mailto:honorbox@proton.me)
- **GitHub:** private vulnerability reporting on the affected repository —
  **Security** tab → **Report a vulnerability**. Enabled on
  [`honorbox`](https://github.com/Honorboxx/honorbox/security) and
  [`crew`](https://github.com/Honorboxx/crew/security).

Include what you can: the affected repo and file, reproduction steps or a
proof-of-concept input, and the impact as you see it. A failing test is the
best possible report; plain prose is fine too.

Please don't open a public issue for a security bug before we've had a
chance to ship a fix.

## Scope

In scope:

- **[`honorbox`](https://github.com/Honorboxx/honorbox)** — the engine:
  store build pipeline, the published store pages, checkout wiring, and the
  fulfillment code in `scripts/`.
- **Fulfillment** — everything on the path from Stripe Checkout (including
  the buyer-supplied GitHub username custom field) to the GitHub repo
  invite, and the issue-triage / refund bots. The service runs from a
  private operations repo, but its core code is public in `honorbox` and
  its input surface is the open internet.
- **[`crew`](https://github.com/Honorboxx/crew)** — the agent pack: agent
  and skill definitions, hooks, install instructions.
- Content we deliver to buyers in private repos (HonorBox Pro, Crew full) —
  report those by email.

Out of scope:

- Vulnerabilities in Stripe or GitHub themselves — report those to their
  programs.
- Anything that requires an already-compromised maintainer account or
  leaked CI secrets as a precondition.
- Volumetric denial of service against GitHub Pages.
- Raw scanner output without a demonstrated impact.

## Threat model, honestly

Store pages are maintainer-authored today. No third-party or buyer-authored
content is rendered into the store, so an HTML/markdown injection currently
needs a maintainer-authored page as its carrier. We still treat escaping
bugs as real vulnerabilities and fix them with regression tests — the
pipeline is meant to render buyer-authored content eventually, and a latent
bug goes live the day that lands.

The untrusted input that reaches our code today: the buyer's GitHub
username (a Stripe Checkout custom field) and issue text handled by the
triage bots.

## What to expect

- **Acknowledgement** within 72 hours, usually faster.
- **A triage verdict** — confirmed, can't reproduce, or out of scope, with
  reasoning — within 7 days.
- Confirmed issues get fixed in priority order of real exploitability, and
  every fix ships with a regression test.
- **No bounty.** We don't run a paid program and won't pretend otherwise.
  With your permission we credit reporters in the release notes.
- **Coordinated disclosure:** give us time to ship a fix before publishing
  details. For confirmed issues we'll agree a timeline with you; if we've
  gone silent or shipped nothing after 90 days, you're free to disclose.

## Baseline posture

So you know what's already in place before you dig:

- **No secrets in repos.** Stripe keys and GitHub tokens live only in
  Actions secrets and the runtime environment, never in code or history,
  and pushes to public repos are swept for credentials.
- **SHA-pinned Actions.** Every GitHub Action in our workflows is pinned to
  a full commit SHA, not a mutable tag.
- **Input validation.** Buyer-supplied GitHub usernames are strictly
  validated (`^[a-zA-Z0-9](?:-?[a-zA-Z0-9]){0,38}$`) before reaching any
  API call, and untrusted input is never interpolated into shell commands
  or workflow YAML.
- **Auditable by design.** The public code is MIT-licensed with zero
  runtime dependencies — the code you can read is all the code there is.

We support the latest release and `main`; older tags don't get backported
fixes.
