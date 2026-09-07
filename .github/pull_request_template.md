## What and why

<!-- One or two sentences. What changes, and what problem it solves. -->

Tracker issue: <!-- full URL, e.g. <internal tracker issue URL> — paste the whole link, short refs do not autolink here -->

## How it was tested

<!-- Commands you ran, or the manual path you clicked. "CI is green" is not a test plan. -->

## Risk and rollback

<!-- Blast radius if this is wrong, and how to undo it: revert the squash commit, feature flag off, down migration, etc. -->

## Checklist

- [ ] PR title is a Conventional Commit (`feat:`, `fix:`, `chore:`, …) — it becomes the squash commit message
- [ ] `gate` is green
- [ ] No secrets, tokens or private IP addresses added (config uses placeholders)
- [ ] Docs / README / env sample updated, or not applicable
- [ ] DB migration is reversible and tested down, or not applicable
