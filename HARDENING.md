<!-- markdownlint-disable -->

# Hardening Report: AndreMiras--coveralls-python-action/v20200412

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **AndreMiras--coveralls-python-action/v20200412** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/push.yml references actions using mutable tag-based refs instead of pinned 40-character SHA digests, making the workflow vulnerable to supply-chain attacks if those tags are moved or compromised. Failing references: `actions/checkout@v2` (used in both the `test` job and `coveralls_finish` job) and `actions/setup-python@v1` (used in the `test` job).

Locations:

- `.github/workflows/push.yml:7`
- `.github/workflows/push.yml:8`
- `.github/workflows/push.yml:35`

### missing-permissions (severity: medium)

The workflow file .github/workflows/push.yml has no top-level `permissions:` key and neither of its jobs (`test`, `coveralls_finish`) defines a job-level `permissions:` block. Without explicit permissions, the workflow inherits the default repository permissions, which may be overly broad (e.g., write access to contents). A minimal permissions block should be added.

Locations:

- `.github/workflows/push.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1) Pinned actions/checkout@v2 to @0717577d45739eb3c851188b29f50ed6c0b2194e (both occurrences in 'test' and 'coveralls_finish' jobs). 2) Pinned actions/setup-python@v1 to @0f07f7f756721ebd886c2462646a35f78a8bc4de. 3) Added top-level `permissions: {}` block to enforce least-privilege access.

