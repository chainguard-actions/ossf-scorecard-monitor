<!-- markdownlint-disable -->

# Hardening Report: ossf--scorecard-monitor/v2.0.0-beta8

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ossf--scorecard-monitor/v2.0.0-beta8** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/code_health.yml references two Actions using mutable tag refs instead of full 40-character SHA commit digests. This exposes the workflow to supply-chain attacks if the tag is moved or the upstream repository is compromised. Failing references: `actions/checkout@v3` and `actions/setup-node@v3`. These should be pinned to their full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/code_health.yml:14`
- `.github/workflows/code_health.yml:15`

### missing-permissions (severity: medium)

The workflow file .github/workflows/code_health.yml has no top-level `permissions:` key, and the only job (`build`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g. write access to contents). A minimal explicit `permissions:` block (e.g. `contents: read`) should be added.

Locations:

- `.github/workflows/code_health.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/code_health.yml: (1) Pinned actions/checkout@v3 to full SHA a37ce9120846195fa4ece8f58b268e6043cb2f26 and actions/setup-node@v3 to full SHA 3235b876344d2a9aa001b8d1453c930bba69e610, preserving the tag in a comment for readability. (2) Added a top-level `permissions: contents: read` block to restrict the workflow token to the minimum required permissions.

