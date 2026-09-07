# Security policy

We take security reports seriously and we would rather hear about a problem early than
read about it later. This policy applies across the `zatto-dev` organisation.

## Scope

**In scope**

- Any repository owned by [github.com/zatto-dev](https://github.com/zatto-dev), public
  or private, including its build and release tooling.
- The products we operate: Sertiq, TopSky, Transfferro, Expira, Warrio and Shy Garlic,
  together with their public web endpoints.
- Our own GitHub Actions workflows and the artefacts they produce.

**Out of scope**

- Third-party services we merely use (report those to the vendor).
- Denial of service, volumetric or brute-force testing of any kind.
- Social engineering, phishing or physical attacks against staff or clients.
- Automated scanner output with no demonstrated impact, missing best-practice headers,
  cookie flags on non-sensitive cookies, or version-number fingerprinting on its own.
- Anything requiring an already-compromised device or account.

Client-operated systems are not ours to authorise testing on. If you believe you have
found a problem in something we built but a client runs, tell us and we will pass it on.

## How to report

Pick whichever is easier:

1. **Private Vulnerability Reporting** — enabled on our public repositories. Use the
   *Security* tab on the repository concerned, then *Report a vulnerability*. This keeps
   the whole exchange private until we agree it is fixed, and is the preferred route.
2. **Email** — **security@zatto.dev**. Encryption key: see *Encryption* below.

Please include, as far as you can:

- what the issue is and which repository, product or URL it affects;
- steps to reproduce, or a minimal proof of concept;
- the impact you believe it has;
- any version, commit SHA or timestamp that helps us pin it down;
- how you would like to be credited, if at all.

**Please do not** open a public issue, pull request or discussion for a vulnerability,
and please do not post details publicly before we have had a chance to fix it. A public
issue is the one report we cannot handle quietly.

## Response targets

These are **targets**, not contractual commitments. We are a small studio; if a target
slips we will say so rather than go quiet. Working days are Monday to Friday, UK time.

| Stage | Target |
| --- | --- |
| Acknowledgement of your report | 2 working days |
| Triage and severity decision, first substantive reply | 5 working days |
| Fix or mitigation — critical | 7 calendar days |
| Fix or mitigation — high | 30 calendar days |
| Fix or mitigation — medium | 90 calendar days |
| Fix or mitigation — low | next scheduled release, best effort |
| Coordinated public disclosure | once a fix ships, and by agreement, normally within 90 days of the report |

We will keep you updated at least every 14 days while a report is open. Severity is our
assessment, using CVSS v3.1 as a guide; tell us if you disagree and we will revisit it.

## Safe harbour

If you make a good-faith effort to follow this policy, we will treat your research as
authorised. We will not pursue or support legal action against you, and if a third party
does, we will make clear that you were acting within this policy.

Good faith means: you only test against systems in scope; you stay within the minimum
access needed to demonstrate the issue; you do not access, modify, delete or retain
anyone else's data; you stop as soon as you have a proof of concept; you do not degrade
service for others; and you give us reasonable time to fix the problem before telling
anyone else. If you accidentally reach data that is not yours, stop and tell us — that
does not by itself put you outside this policy.

This safe harbour is ours to give and covers only us. It does not override the law, and
it does not bind our clients or our suppliers.

## Encryption and alternate contact

- **PGP key:** _placeholder — key and fingerprint to be published here; ask at
  security@zatto.dev for the current key before sending encrypted material._
- **Alternate contact:** if security@zatto.dev bounces or you get no acknowledgement
  within the target above, email **hello@zatto.dev** with the subject line
  `SECURITY — no response` and no technical detail, and we will open a private channel.

## Recognition

We do not run a paid bug bounty. We will credit reporters by name or handle in the
release notes or advisory for the fix, unless you would rather stay anonymous.
