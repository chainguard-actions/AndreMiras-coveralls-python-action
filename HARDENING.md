<!-- markdownlint-disable -->

# Hardening Report: AndreMiras--coveralls-python-action/v20200413

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **AndreMiras--coveralls-python-action/v20200413** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/push.yml references actions using mutable tag refs instead of full 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced tags are moved or compromised. Failing references: 'actions/checkout@v2' (line 7, line 34) and 'actions/setup-python@v1' (line 8). These should be pinned to their full SHA digests, e.g. actions/checkout@<40-char-sha>.

Locations:

- `.github/workflows/push.yml:7`
- `.github/workflows/push.yml:8`
- `.github/workflows/push.yml:34`

### missing-permissions (severity: medium)

The workflow file .github/workflows/push.yml has no top-level 'permissions:' key and neither of its jobs ('test', 'coveralls_finish') defines a job-level 'permissions:' block. Without explicit permissions, the workflow inherits the default repository permissions, which may be overly broad. Explicit minimal permissions should be declared.

Locations:

- `.github/workflows/push.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/push.yml: (1) Pinned actions/checkout@v2 to SHA 0717577d45739eb3c851188b29f50ed6c0b2194e and actions/setup-python@v1 to SHA 0f07f7f756721ebd886c2462646a35f78a8bc4de, preserving the original tag names in comments. (2) Added top-level 'permissions: {}' to deny all permissions by default, and job-level 'permissions: contents: read' for both jobs since they require repository checkout.

