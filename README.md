# `.github` — org-wide defaults for `zatto-dev`

This repository holds the defaults that GitHub applies across the
[zatto-dev](https://github.com/zatto-dev) organisation. It contains almost no code; it
exists so that every other repository inherits the same profile, policies and templates
without each one carrying its own copy.

## This repository must stay public

GitHub only propagates community health files from a **public** `.github` repository. If
this repository is made private, the org profile page disappears and every repository
that relies on these defaults — including the private ones — silently falls back to
having no CODE_OF_CONDUCT, CONTRIBUTING, SECURITY or SUPPORT file at all. There is no
warning when that happens.

Nothing in here may contain anything that is not safe to publish: no secrets, no
tokens, no internal addresses, no client names.

## What lives here

| Path | Purpose |
| --- | --- |
| `profile/README.md` | The public org landing page at github.com/zatto-dev |
| `profile/assets/` | Logo assets referenced by the profile README |
| `README.md` | This file — internal note, not shown on the profile page |
| `CODE_OF_CONDUCT.md` | Contributor Covenant 2.1, contact `conduct@zatto.dev` |
| `CONTRIBUTING.md` | Branching, commits, review and merge rules for all repos |
| `SECURITY.md` | Vulnerability disclosure policy, contact `security@zatto.dev` |
| `SUPPORT.md` | Where to ask for help |
| `.github/ISSUE_TEMPLATE/` | Default issue forms and the template chooser |
| `.github/DISCUSSION_TEMPLATE/` | Default discussion forms |
| `.github/pull_request_template.md` | Default PR description template |

## How propagation works

A repository that has its **own** copy of a file always wins; the default is only used
when the repository has no file of that type. So a repo with special rules simply adds
its own `CONTRIBUTING.md` and stops inheriting this one.

Things that do **not** propagate, and have to be added per repository:

- `LICENSE` — never inherited; each public repo needs its own.
- GitHub Actions workflows — reusable workflows live in the shared CI repository and
  are called explicitly by each repo.
- Labels, branch settings and merge settings — applied per repository from the
  org tooling repository.
- Repository-level secrets — on the GitHub Free plan, org-level secrets are not
  readable from private repositories, so every private repo carries its own.

Default files are also not included in clones, archives or release packages. They are a
GitHub UI feature, not part of the source tree of the repositories that inherit them.

## Changing a default

Changes here affect every repository at once. Same rules as anywhere else: branch,
open a PR, get the gate green, squash-merge. See [CONTRIBUTING.md](CONTRIBUTING.md).
