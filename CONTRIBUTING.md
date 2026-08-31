# Contributing to Silo

Contributions are welcome from any workflow, including AI-assisted ones. Most of
Silo was written with AI assistance. Whoever submits the work is responsible for
understanding it, testing it, and explaining it; that applies to maintainers and
external contributors alike.

## Before you start

> [!IMPORTANT]
> Open an issue before implementing features, API or behavior changes, schema
> changes, large refactors, or anything else that changes product scope.
> Documentation, typo fixes, and narrow bug fixes can go straight to a pull
> request.

Silo is pre-1.0 and moves quickly. Coordinating first avoids duplicate work,
conflicts with changes already in flight, and proposals outside scope. Start in
the repository that owns the behavior:

- [`silo-server`](https://github.com/Silo-Server/silo-server) for the backend,
  web app, native API, Jellyfin compatibility, and plugin host.
- [`silo-apple`](https://github.com/Silo-Server/silo-apple) or
  [`silo-android`](https://github.com/Silo-Server/silo-android) for a client-only
  change.
- [`silo-plugin-sdk`](https://github.com/Silo-Server/silo-plugin-sdk) for plugin
  contracts, or the individual plugin repository for provider behavior.

Cross-repository behavior changes should identify every affected repository
before implementation begins.

## Reporting a problem

Use the issue tracker for the repository that owns the problem. Describe what
you observed before any root-cause theory, and paste raw logs rather than a
summary. Redact credentials, tokens, personal data, and private media details,
mark each redaction, and leave the rest untouched.

## Prepare a focused change

1. Read the repository README, its local `CONTRIBUTING.md`, and any `AGENTS.md`
   or `CLAUDE.md` before changing it.
2. Read the existing implementation and tests in the area you are changing.
3. Keep one concern per pull request; avoid unrelated cleanup or refactors.
4. Follow existing patterns and add tests for behavior changes where practical.
5. Exercise user-facing behavior in a running application when you can.
6. Review the whole diff for unintended behavior, generated-file drift, local
   paths, credentials, and stray edits.
7. For non-trivial changes, get an independent or adversarial review and
   resolve its findings before submitting.

Tests are evidence, not proof. Think about effects beyond the files you touched,
and be ready to explain the implementation, alternatives, and tradeoffs in
review.

## Validate your change

Run the focused checks while iterating, then the complete validation gate listed
in the repository's local `CONTRIBUTING.md` or CI workflow. Paste the actual
results into the pull request. Do not report a check as passing if it was
skipped, failed, or ran somewhere other than where you say it did.

## AI-assisted contributions

> [!WARNING]
> Disclose AI use in every issue and pull request. Fabricated APIs,
> observations, vulnerabilities, reproduction steps, logs, or test results get
> the contributor blocked. Bug reports must come from a real reproduction with
> raw logs.

The [AI-assisted contribution policy](https://github.com/Silo-Server/silo-server/blob/main/docs/ai-contributions.md)
defines the disclosure block, evidence standard, and enforcement. "No AI used"
is a valid disclosure; leaving it out is not.

## Open the pull request

Use a [Conventional Commit](https://www.conventionalcommits.org/) title and fill
in the pull request template. Link the issue or scope item for non-trivial work;
write `Related issue: N/A — narrow fix` only when no prior coordination was
needed. Keep the commit history intentional and the diff limited to the stated
problem.

## Review expectations

Maintainers may ask for a smaller change, a different implementation, decline
work that no longer fits, or take the idea and implement it separately. Opening
a pull request does not guarantee a merge. If scope is uncertain, ask before
building.
