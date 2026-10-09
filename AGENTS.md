# Agent Guide

## Project

Personal website for an introduction, project case studies, CV, and contact form. It should demonstrate backend, DevOps, cybersecurity, and software architecture through its implementation, not only describe those skills.

The repository currently contains planning documents only. No framework, application code, developer commands, CI, containers, or infrastructure are implemented yet. Treat proposed application structure and stack choices below as pending until approved and implemented.

## Structure

Proposed structure (pending):

- `specs/` — feature specifications, plans, and task lists; `specs/constitution.md` — approved project-wide principles.
- `docs/adr/` — Architecture Decision Records named `NNNN-title.md`.
- `src/` — static website and its page/component code (framework pending).
- `content/` or a translation layer — English site content, separate from components; final location pending.
- `api/` — stateless serverless contact-form function (pending; exact location may be hosting-provider-specific).
- `infra/` — infrastructure as code only if justified (optional, pending).
- `.github/workflows/` — CI/CD workflows (pending).
- `README.md` — project overview and setup, development, and operational documentation (commands pending until the app is scaffolded).

Intended stack: managed static hosting with a CDN and HTTPS, plus a stateless serverless contact API. GitHub Actions, security headers, dependency/secret scanning, platform-level rate limiting and spam protection, and monitoring are planned; all are pending. Docker, Terraform, and staging are optional and require an ADR documenting a concrete benefit. Target operating cost is $0/month except for the domain; verify current free-tier limits before selecting services. Any paid service requires an ADR.

## Spec-Driven Development

For every feature or significant change, follow these gates in order. Do not implement until the spec and the combined plan/task list are approved.

- [ ] **Spec:** Create `specs/<NNN-feature-name>/spec.md`. Describe what and why: user stories, concrete requirements, measurable acceptance criteria, and out of scope. Do not include implementation details.
- [ ] **Clarify:** Identify ambiguities and open questions. Ask before assuming; mark unresolved items `[NEEDS CLARIFICATION]`.
- [ ] **Plan and tasks:** After spec approval, create `plan.md` describing architecture, technology choices, data models, API contracts, security, and trade-offs, plus `tasks.md` with small, ordered, testable tasks and stable task IDs. Follow `specs/constitution.md`; stop for approval of both before implementation.
- [ ] **Implement:** After approval, execute one task at a time. Reference the spec/task ID in commits.
- [ ] **Verify:** Check each acceptance criterion against the finished behavior. If implementation exposes a spec gap, update and approve the spec before changing code.

Record architectural decisions in `docs/adr/NNNN-title.md`. Keep specs short, concrete, and testable; avoid unmeasurable claims such as “fast” or “secure.”

## Commands

No package manifest, task runner, test/lint configuration, or Docker files exist yet. Exact install, development, build, test, lint, and Docker commands (if containers are adopted) are **pending**; discover and document them from executable project configuration when added. Do not invent commands.

## Conventions

- Write all code, comments, specs, commit messages, documentation, and website content in English. Keep sentences simple and direct.
- Keep user-facing text out of components. Store content separately or use a translation layer so Spanish can be added later. English is the current content language; Spanish is pending.
- Use Conventional Commits and include the relevant spec/task ID (for example, `feat(012): ... [012-03]`).
- Use a dedicated task branch for each feature, fix, documentation change, or substantial spec. See **Git Workflow and Pull Requests** below.
- Match the style and tooling actually introduced by the project; no formatter or naming convention is configured yet.
- Make small, focused changes. Explain why before changing CI/CD or infrastructure configuration. Update specs and documentation when behavior changes.

## Git Workflow and Pull Requests

- Before work, inspect `git status --short --branch` and `git branch --show-current`. Preserve unrelated working-tree changes; never discard or commit them without authorization.
- Fetch with `git fetch origin`, then base the task branch on the latest `origin/main`. If `origin/main` is missing, stop and ask before using another base.
- If on `main`, create a task branch before editing. Check whether an appropriate branch already exists before creating or switching. If already on another branch, inspect its base and changes first.
- Use a dedicated branch for every task with Conventional Branch names such as `feat/contact-form`, `fix/mobile-layout`, `docs/constitution`, or `chore/ci-workflow`.
- Commit and push only on the task branch. Stage specific files; never use `git add .`. Do not force-push unless explicitly authorized.
- Run relevant checks before pushing or opening a PR. Do not bypass required checks or claim checks passed unless they ran.
- Open a PR targeting `main` after checks pass. Include a concise summary, motivation, verification results, and related spec/task links. Use `gh` when available and authenticated; otherwise push and provide the PR URL or instructions to open one.
- Keep progress visible with meaningful commits and update the PR description when scope, implementation status, or validation changes.
- Never merge automatically. Wait for explicit user authorization to merge.
- At task completion, report the branch, commits, files changed, checks performed, push status, and PR URL or why a PR could not be created.

## Security and Content

- Never commit secrets, tokens, or `.env` files. Use environment variables and maintain a `.env.example` containing placeholders only.
- Validate every user-controlled value at the API boundary; delegate rate limiting and spam protection to the hosting platform.
- Keep security headers in place. Use CSP `frame-ancestors` rather than `X-Frame-Options`; never loosen the CSP without justification. HSTS preload is not required by default.
- Review the maintenance, license, purpose, and security implications of each dependency before adding it.
- Do not include confidential employer or client information, including internal names, figures, or non-public details. Anonymize and abstract case studies.
- Use a professional, clear, honest tone. Do not exaggerate achievements.
- When editing text written by the author, briefly identify grammar or wording issues and suggest natural alternatives instead of silently rewriting it.

## Definition of Done

- Spec acceptance criteria are met, and spec, plan, tasks, and README reflect the change.
- Relevant tests and build pass; lint is clean (once these checks exist).
- No secrets are committed, and required security controls remain in place.

## Pending / Roadmap

Each item needs an approved future spec before implementation:

- Static site, content structure, and English pages — [`specs/001-static-site/spec.md`](specs/001-static-site/spec.md) (pending).
- Contact form and serverless API — [`specs/002-contact-api/spec.md`](specs/002-contact-api/spec.md) (pending).
- CI/CD, security scanning, and security headers — [`specs/003-delivery-security/spec.md`](specs/003-delivery-security/spec.md) (pending; image scanning applies if containers are adopted).
- Secrets management and any justified infrastructure as code — [`specs/004-infrastructure/spec.md`](specs/004-infrastructure/spec.md) (pending; IaC is optional).
- Spanish translation and localization — [`specs/005-spanish-i18n/spec.md`](specs/005-spanish-i18n/spec.md) (pending).
- Monitoring and operational visibility — [`specs/006-monitoring/spec.md`](specs/006-monitoring/spec.md) (pending).
