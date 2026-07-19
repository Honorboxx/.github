# Contributing to HonorBox

Thanks for taking the time to contribute. HonorBox is a small, deliberately
simple toolkit for selling digital products with just Stripe + GitHub, and its
sibling project **Crew** is an agent pack for Claude Code. These guidelines
apply to every repository in the [Honorboxx](https://github.com/Honorboxx) org.

## Ways to help

- **Report a bug** or a delivery/checkout problem → open an issue (templates
  guide you).
- **Suggest an improvement** → open an issue describing the use case first;
  small, focused changes merge fastest.
- **Send a pull request** → for typos, docs, and clearly-scoped fixes, a PR is
  welcome directly. For anything larger, open an issue first so we can agree on
  the approach before you spend time on it.
- **Security issue?** Do **not** open a public issue — see
  [SECURITY.md](https://github.com/Honorboxx/.github/blob/main/SECURITY.md).

## The bar for changes

HonorBox has two non-negotiables that keep it trustworthy:

1. **Zero runtime dependencies.** The engine is Node standard library only —
   no npm packages at runtime. A supply chain is a liability the product
   advertises not having. Build/test tooling is stdlib too (`node --test`).
2. **Tests stay green.** Pure logic lives in `scripts/lib/` and is covered by
   `node --test scripts/test/*.test.js`. If you change behavior, add or update
   a test. Money-adjacent code (fulfillment, refunds) must stay idempotent and
   fail loud.

## Local development

```bash
node --test scripts/test/*.test.js   # run the suite (no deps to install)
node scripts/build.js                # build the storefront -> dist/
```

Node ≥ 20. There is nothing to `npm install`.

## Pull request checklist

- The suite passes locally (`node --test scripts/test/*.test.js`).
- New behavior has a test; the test would fail without your change.
- No new runtime dependencies.
- No secrets, tokens, or personal data in the diff.
- Commit messages describe the change, not the tool that made it.

## Style

Match the surrounding code — its naming, comment density, and idioms. Comments
should state constraints the code can't show, not narrate what the next line
does. Keep files focused; when one grows large, that's usually a sign it's doing
too much.

## Reporting content or conduct problems

Be respectful — see the [Code of Conduct](CODE_OF_CONDUCT.md). Conduct concerns
go to **honorbox@proton.me**.
