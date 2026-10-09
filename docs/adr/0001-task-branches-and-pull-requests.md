# ADR-0001: Task Branches and Pull Requests

- Status: Accepted
- Date: 2026-10-09

## Context

The project uses Spec-Driven Development and needs an auditable path from an approved task to an integrated change. `main` is the shared source of truth and should remain stable. Agent instructions alone do not technically prevent direct pushes to `main`.

## Decision

Make development changes on dedicated task branches based on the latest `origin/main`. Run relevant checks, push the task branch, and open a pull request targeting `main`. Do not merge automatically; wait for explicit user authorization. Do not force-push unless explicitly authorized.

## Alternatives considered

- Commit directly to `main`: fewer steps, but no task isolation or pull-request review record.
- Use task branches without pull requests: isolates work, but loses the required integration review and verification record.
- Use task branches and pull requests: selected for traceability and controlled integration.

## Consequences

Each task requires a branch, relevant validation, and a pull request. This adds steps but keeps `main` stable and leaves a reviewable record. GitHub branch protection and required CI checks must be configured separately to enforce the policy technically.
