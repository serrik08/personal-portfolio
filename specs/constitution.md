# personal-portfolio Constitution

Applies to specifications, plans, implementation, and operations. Demonstrate engineering judgment through specs, ADRs, the CI pipeline, security headers, and a “How this site is built” page—not unnecessary infrastructure. Plans define numeric thresholds such as budgets, rate limits, secret rotation, and test coverage.

## Cost

- **P-COST-01 — Target $0/month except for the domain; paid services require an ADR.**
  Reason: Avoid recurring costs that do not provide a clear project benefit.
  Verify: Before selecting a service, its ADR records current free-tier limits, pricing, expected cost, and benefit.

## Security

- **P-SEC-01 — Keep secrets out of source, logs, and build artifacts.**
  Reason: Exposed secrets can compromise the site and its services.
  Verify: Secret scanning runs on every commit and blocks findings; CI rejects tracked `.env`, `.env.local`, `*.pem`, `*.key`, and `credentials.json`. `.env.example` has placeholders only. Plans define runtime injection, missing-secret behavior, and rotation.
- **P-SEC-02 — Enforce HTTPS and restrictive security headers.**
  Reason: Browser security controls reduce common attack paths.
  Verify: Production redirects HTTP to HTTPS and returns HSTS, CSP with `frame-ancestors`, and `X-Content-Type-Options`; CSP `script-src` excludes `'unsafe-inline'` and `'unsafe-eval'`. HSTS preload is not required by default.
- **P-SEC-03 — Validate API input and minimize personal data.**
  Reason: Untrusted input and unnecessary personal data increase security and privacy risks.
  Verify: API plans define server-side validation and input limits; rate limiting and spam protection use platform controls. Do not log or store submitted personal data beyond what is needed to deliver the message. Use contextual output encoding and, if a database is added, parameterized SQL.
- **P-SEC-04 — Scan dependencies, source, and container images when used.**
  Reason: Known vulnerabilities and unsafe container privileges should be found before release.
  Verify: CI scans dependencies and source; critical/high dependency findings block merge and deployment. If containers are adopted, run them as non-root and block publication and deployment for critical/high image findings.

## Architecture

- **P-ARCH-01 — Default to managed static hosting and a stateless serverless API.**
  Reason: This meets the site’s needs with low operational overhead.
  Verify: Use a managed static host with CDN and HTTPS, a stateless serverless contact API, and PR previews for merge candidates; production is the primary environment.
- **P-ARCH-02 — Add infrastructure only for a documented benefit.**
  Reason: Unneeded components increase cost and maintenance.
  Verify: An ADR documents the need, benefit, and trade-offs for additional infrastructure. Docker, Terraform, and staging are optional and each requires an ADR; do not introduce Kubernetes or distributed components just to demonstrate them.

## Performance and accessibility

- **P-PERF-01 — Define measurable performance budgets and enforce them with lab tests.**
  Reason: Performance expectations should be explicit and repeatable.
  Verify: Plans define budgets; Lighthouse CI is the performance gate under consistent conditions. RUM is optional and requires an ADR. Document budget exceptions with measured impact and mitigation.
- **P-PERF-02 — Target WCAG 2.2 Level AA for primary pages and journeys.**
  Reason: Essential content should work with different input methods and assistive technologies.
  Verify: Automated and manual checks cover keyboard use, focus, forms, contrast, and screen-reader use. A pull request template checklist records manual accessibility verification.

## Quality

- **P-QUAL-01 — Require passing quality gates before merge.**
  Reason: Changes should meet defined checks before reaching `main`.
  Verify: CI checks formatting, lint, types, tests, production build, security, accessibility, applicable performance budgets, and PR-preview smoke tests; plans define coverage thresholds. The author reviews the diff; no second-person approval is required.
- **P-QUAL-02 — Test behavior and release candidates according to risk.**
  Reason: Tests should catch regressions without relying on unreliable results.
  Verify: Relevant unit, integration, and end-to-end tests are deterministic; smoke tests run against the PR preview before merge.

## DevOps

- **P-DEVOPS-01 — Automate pull-request checks and production deployment.**
  Reason: Automation makes changes and releases repeatable.
  Verify: GitHub Actions runs required checks on every PR; merging to `main` deploys automatically and runs smoke tests against production. A failed production smoke test triggers the rollback procedure in P-DEVOPS-02.
- **P-DEVOPS-02 — Monitor production and recover failed releases.**
  Reason: Problems should be detectable and releases recoverable.
  Verify: Configure availability monitoring and alerts, retain platform logs, use structured backend logs if applicable, and document a rollback or redeployment procedure that is triggered by failed production smoke tests.

## Content and honesty

- **P-CONT-01 — Protect confidential employer, client, and collaborator information.**
  Reason: Public work must not expose private information or systems.
  Verify: Before publication, check for confidential data, credentials, non-public URLs, proprietary code, and identifying details. Use authorized disclosures or anonymized examples with synthetic data. A pull request template checklist records this review.
- **P-CONT-02 — Make truthful claims and identify project context.**
  Reason: Readers should understand what experience and results are yours.
  Verify: Distinguish personal contributions from team outcomes, professional work from personal projects or learning, and never invent credentials, roles, responsibilities, or results.
- **P-CONT-03 — Publish supportable metrics and keep content current.**
  Reason: Unsupported figures can misrepresent results or disclose sensitive information.
  Verify: Metrics have shareable evidence or a documented calculation; label estimates, omit confidential figures, and review public content every six months and when facts or permissions change.

## Language and i18n

- **P-I18N-01 — Centralize UI translations and structure translatable content.**
  Reason: Translation should not require rewriting components or duplicating pages.
  Verify: Components use locale keys and portfolio content uses structured files; a heavyweight i18n framework requires a documented need.
- **P-I18N-02 — Enable a locale only when its required content is complete.**
  Reason: Users should not see partially translated pages.
  Verify: CI checks required keys and content for enabled locales; show the English/Español switcher only when Spanish is complete, with no raw keys or silent fallback.
- **P-I18N-03 — Preserve locale-specific meaning and accessibility.**
  Reason: Translated pages should remain accurate and usable.
  Verify: Use locale-aware formatting and the correct `lang`; preserve technical identifiers and factual values, and check equivalent essential content, accessibility, metadata, and layouts in each enabled locale.

## Development process

- **P-PROC-01 — Use approval gates for significant changes and a light workflow for routine fixes.**
  Reason: Approval keeps substantial work aligned without burdening routine maintenance.
  Verify: Approve the spec first, then the plan and task list together before implementation; validate against acceptance criteria. Small low-risk fixes need no full spec. Treat AI output as proposals and keep changes within approved scope.
- **P-PROC-02 — All development changes must be made on task branches based on the latest `main` and integrated through pull requests targeting `main`.**
  Reason: Protect `main` and keep each task reviewable and traceable.
  Verify: Fetch `origin/main` before branching, run relevant checks before opening a PR, and wait for explicit user authorization before merging.
- **P-PROC-03 — Record significant decisions in ADRs.**
  Reason: Important trade-offs should remain visible.
  Verify: ADRs in `docs/adr/NNNN-title.md` document context, decision, alternatives, consequences, and status; mark superseded decisions.

## Governance

- **P-GOV-01 — Amend this constitution through an ADR.**
  Reason: Project-wide principles should change deliberately and transparently.
  Verify: Each amendment’s ADR records its rationale, changes, and impact.
