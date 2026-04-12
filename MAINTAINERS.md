# Maintainer Guide

Notes and recommended settings for anyone maintaining this repository.

## Recommended GitHub settings

Apply these via the GitHub web UI under **Settings**:

### Branch protection (Settings → Branches → Branch protection rules)

Create a rule for `main`:

- [x] **Require a pull request before merging** — Prevents direct pushes; all changes go through PR review.
  - [x] Require at least **1 approval**.
  - [x] Dismiss stale pull request approvals when new commits are pushed.
- [x] **Require status checks to pass before merging** — Enable once CI (e.g., link checker) is set up.
- [x] **Do not allow bypassing the above settings** — Applies rules to admins too.
- [ ] Require signed commits — Optional; nice-to-have but not critical for a docs repo.

### Interaction limits (Settings → Moderation → Interaction limits)

If spam becomes a problem:

- **Temporary interaction limit:** Restrict to existing users or contributors only. Useful during spam waves.
- **Repository-level limit:** Limit interactions to users with accounts older than 24 hours (prevents throwaway-account spam).

### General (Settings → General)

- **Features:** Disable Wikis and Projects if not in use — reduces attack surface for spam.
- **Pull Requests:** Allow only squash merging to keep history clean.
- **Automatically delete head branches** after merge.

### Topics (Settings → General → Topics)

Add these for discoverability:

```
awesome-list, finance-api, free-api, fintech, trading, quant, market-data,
open-banking, stock-api, crypto-api, fx-api, derivatives, economic-data,
financial-data, api-list
```

## Triage workflow

Quick decision tree for incoming PRs:

```
New PR arrives
  ├─ Is the checklist in the PR template filled out?
  │   └─ No → Comment "Please complete the PR checklist" → Close
  ├─ Is the entry template followed?
  │   └─ No → Comment with link to CONTRIBUTING.md → Close
  ├─ Is the API real and does the free tier exist?
  │   └─ No → Close with brief explanation
  ├─ Is the submitter affiliated and undisclosed?
  │   └─ Suspected → Ask for disclosure; close if no response in 7 days
  └─ Looks good → Review accuracy → Merge (squash)
```

## Useful GitHub Actions to add later

- **Dead link checker** — Run weekly via `lycheeverse/lychee-action` to catch broken URLs.
- **Markdown lint** — `DavidAnson/markdownlint-cli2-action` to enforce formatting.
- **Stale issue/PR bot** — `actions/stale` to auto-close issues with no activity after 30 days.

## Emergency anti-spam

If the repo gets hit by a spam wave:

1. Enable **temporary interaction limits** (24-hour-old accounts only).
2. Lock individual spam issues/PRs immediately.
3. Report spam accounts to GitHub via the "Report abuse" option on their profile.
4. Consider enabling **repository interaction limits** for 1 week.
