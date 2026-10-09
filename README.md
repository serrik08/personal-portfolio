# Personal Portfolio

Personal website for an introduction, project case studies, a CV, and a contact form. The project aims to demonstrate backend, DevOps, cybersecurity, and software architecture through practical engineering decisions.

## Project status

This repository is at the planning stage. The constitution and agent guidance are in place, but the site, API, CI, hosting, and monitoring have not been implemented. Framework, hosting provider, and exact function layout are pending approval through the relevant specifications and plans.

## Goals and constraints

- Use managed static hosting with a CDN and HTTPS, plus a stateless serverless function for contact submissions.
- Delegate rate limiting and spam protection to the hosting platform.
- Target $0 per month except for the domain. Verify current free-tier limits before selecting services; any paid service requires an ADR.
- Keep Docker, Terraform, staging, and RUM optional. Introduce each only with an ADR documenting its benefit.
- Keep the initial site in English and make translation to Spanish possible without hardcoded UI text in components.
- Demonstrate engineering decisions through the CI pipeline, security controls, specifications, ADRs, and a planned “How this site is built” page—not unnecessary infrastructure.

## Project guidance

- [`AGENTS.md`](AGENTS.md) contains instructions for AI agents, including the SDD workflow, security rules, and repository conventions.
- [`specs/constitution.md`](specs/constitution.md) defines project-wide principles.
- Significant features require an approved specification, followed by an implementation plan and task list approved together, then task-by-task implementation and verification.
- Record significant architectural decisions in `docs/adr/` as `NNNN-title.md` ADRs.

## Proposed structure

The application structure is not implemented yet. Paths and provider-specific locations may change through approved plans.

- `specs/` — Constitution and feature specifications, plans, and task lists.
- `docs/adr/` — Architecture Decision Records.
- `src/` — Static site pages and components (framework pending).
- `content/` — Structured site content and translations (location pending).
- Serverless contact function — Provider-specific location pending.
- `.github/workflows/` — CI/CD workflows (pending).

## Development commands

Install, development, build, test, lint, and deployment commands are not available yet because no application framework or toolchain has been selected. Add exact commands here when the first implementation plan establishes them; do not assume commands that are not configured.

## Roadmap

Implementation proceeds through approved specifications:

1. Static site, content structure, and English pages — [`specs/001-static-site/spec.md`](specs/001-static-site/spec.md) (pending).
2. Contact form and serverless API — [`specs/002-contact-api/spec.md`](specs/002-contact-api/spec.md) (pending).
3. CI/CD, security scanning, and security headers — [`specs/003-delivery-security/spec.md`](specs/003-delivery-security/spec.md) (pending).
4. Secrets management and any justified infrastructure as code — [`specs/004-infrastructure/spec.md`](specs/004-infrastructure/spec.md) (pending; IaC is optional).
5. Spanish translation and localization — [`specs/005-spanish-i18n/spec.md`](specs/005-spanish-i18n/spec.md) (pending).
6. Monitoring and operational visibility — [`specs/006-monitoring/spec.md`](specs/006-monitoring/spec.md) (pending).
