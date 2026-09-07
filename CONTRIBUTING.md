# Contributing

These are the working rules for every repository in the `zatto-dev` organisation. A
repository with different needs may add its own `CONTRIBUTING.md`, which then replaces
this one; otherwise, this is what applies.

Please also read the [Code of Conduct](CODE_OF_CONDUCT.md). Security problems go through
[SECURITY.md](SECURITY.md), never through an issue or a pull request.

## Where work is tracked

**Our internal tracker is the source of truth for tasks, backlog and status.** Priorities, sprints and
whether something is "in progress" live there, not on GitHub.

GitHub issues are for **code-level discussion**: a bug report with a reproduction, a
design question about a specific module, a proposal that needs review before anyone
writes code. That is a deliberate split, so:

- GitHub labels never duplicate workflow state. There are no `in progress` or `done`
  labels and there will not be. If you want status, look in our internal tracker.
- Labels describe the *thing*, not its position in a queue:
  - `type/` — `feat`, `fix`, `chore`, `docs`, `refactor`, `security`
  - `area/` — `api`, `web`, `db`, `infra`, `ci`, `deps`
  - `priority/` — `p0`, `p1`, `p2`, `p3`
  - `status/` — `triage`, `blocked`, `needs-info` (blocked-on-input states only)
  - `breaking` — standalone, for anything that breaks a public interface

## Branching

Trunk-based. `main` is always deployable.

- Branch from `main`, name it `<type>/<slug>` where `<type>` is one of `feat`, `fix`,
  `chore`, `docs`, `refactor` — for example `feat/ncr-bulk-export`, `fix/calibration-tz`.
- Keep branches short: roughly two days of work, and smaller if you can. If a branch is
  living longer than that, split the work.
- There is no `develop` branch. There are no long-lived release branches.
- Hotfixes are fixed forward: a `fix/` branch onto `main`, same as anything else.
- Rebase on `main` rather than merging `main` into your branch.

## Commits

[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/):

```
<type>(<optional scope>): <description>

[optional body]

[optional footer, e.g. BREAKING CHANGE: ...]
```

Types: `feat`, `fix`, `chore`, `docs`, `refactor`, `test`, `build`, `ci`, `perf`.
Description in the imperative, lower case, no full stop, under about 70 characters.

Because we squash-merge, **the pull request title becomes the commit message on `main`**
— so the PR title must itself be a valid Conventional Commit. Commits inside the branch
can be scrappier, but keep them conventional anyway: it makes the PR title obvious.

## Pull requests and the gate

Every change reaches `main` through a pull request. Even a one-line fix, even yours.

1. Push your branch and open a PR against `main`.
2. Fill in what changed and why, and how you tested it. Link the our internal tracker item if there is
   one.
3. Wait for the **`gate`** job. Every repository's CI ends in a single job called `gate`
   that aggregates all the checks — lint, types, tests, secret scan, SAST, workflow
   lint. One place to look.
4. **House rule: never merge a red gate.** Not "it is only the flaky test", not "CI is
   having a bad day", not "I will fix it in the next PR". On the GitHub Free plan we
   have no required status checks — nothing in the platform will stop you. The rule is
   the control. If the gate is wrong, fix the gate in its own PR.
5. Get a review where there is someone to review it. Where there genuinely is not, still
   open the PR: it is the record of what changed and why.
6. **Squash and merge** — it is the only merge method enabled. The branch is deleted
   automatically afterwards.

Do not push directly to `main`. See below for why that is on you rather than on GitHub.

## Local setup

Each repository states its own versions. Take them from the repository, not from habit.

- **Node** — the version in that repo's `.nvmrc`. It is not the same everywhere (we have
  repos on 20, 22 and 24), so `nvm use` in the repo directory rather than assuming.
- **Package manager** — whatever the `packageManager` field and the lockfile say. Most
  repos are on **pnpm, pinned to `10.33.2`**; some are on npm; one is on bun. Run
  `corepack enable` once and the pinned version is used automatically. Never mix
  package managers in a repository, and never commit a second lockfile.
- Install with a frozen lockfile (`pnpm install --frozen-lockfile`, `npm ci`) so your
  install matches CI.
- Lockfile changes belong in their own commit, ideally their own PR, labelled
  `area/deps`.

Before pushing, run whatever the repo's `package.json` scripts define — typically
`lint`, `typecheck`, `test`, `build`. The gate runs the same things; running them
locally is just faster.

## Hooks: lefthook, and why `--no-verify` is not acceptable

Every repository installs [lefthook](https://github.com/evilmartians/lefthook). The
hooks run formatting and lint on staged files, check the commit message, and — the
important one — **the pre-push hook refuses a direct push to `main`**.

This matters more here than in most organisations. We are on GitHub Free, so private
repositories get **no branch protection, no rulesets, no required reviews and no
required status checks**. There is no server-side wall. The lefthook pre-push hook is
the only *preventive* control we have, and the `guard-main.yml` workflow is only a
*detective* one — it tells us afterwards that someone pushed straight to `main`, which
is a conversation, not a rollback.

So: `git push --no-verify`, `git commit --no-verify` and `LEFTHOOK=0` are not acceptable
ways of getting past a failing hook. If a hook is wrong or too slow, fix the hook and
say so. If you genuinely have to bypass one — a broken hook mid-incident, say — tell
someone the same day.

Hooks install with `pnpm lefthook install` (or the repo's `prepare` script). If you have
cloned a repo and the hooks are not running, they were never installed; install them.

## Reviewing

- Review the change against what the PR says it does.
- Prefer a comment that says what you would do instead over one that only says no.
- Approve when it is good enough to ship, not when it is what you would have written.
- Anything security-relevant — auth, input handling, dependencies, workflow permissions,
  anything touching a secret — gets a second pair of eyes, no exceptions.

## Dependencies

Dependabot alerts and security updates are on. Security bumps are merged promptly; other
bumps are batched. Do not add a dependency to save ten lines of code, and do not add one
without checking its licence, its release history and how many transitive packages it
drags in.

## Questions

Anything not covered here: open a GitHub Discussion on the repository, or email
**hello@zatto.dev**.
