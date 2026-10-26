# Maintenance Report

## Dependency compatibility

Actual install requirements constrain filelock to 3.20.3. Python >=3.10 is required by filelock3.20.3; Python 3.9 is not supported.
The supported bus client requires bitstring>=4.1.1,<5. Schema-v2 Client
compatibility requires plugin-manager>=0.6.0a1,<0.9. Test extras match the
existing policy-E2E workflow: hivescope0.4.0a2, core4.3.0a2, agent0.2.0a1 and
manager0.6.0a1. SQLite behavior and schema remain unchanged.

Full test extras: 70 passed, 3 skipped, with topology tests included and only
local SQLCipher unavailable. Test metadata matches the existing policy-E2E
workflow rather than selecting a different, incompatible constructor API.
Unit endpoint verification: 67 passed, 3 skipped against manager0.6.0a1 and0.8.0a3
(SQLCipher unavailable locally; e2e excluded). The unrestricted manager0.10
graph produces42 failures in the unchanged legacy Client API. A clean resolver
dry-run rejects this fork combined with the current quota plugin's manager>=0.10
requirement. This is an explicit legacy support boundary, not a production
downgrade. Wheel/sdist builds and exact built-metadata checks pass.
See [tests/test_dependency_security.py](tests/test_dependency_security.py).
No deployment, package publication, or vulnerability exception is performed.

## Transparency Report

- AI model: Codex, GPT-5-based coding agent; a more specific runtime ID is not exposed.
- Actions: inspected source/primary advisories, edited dependency constraints,
  added tests/documentation, ran tests and package checks.
- Oversight: owner-authorized remediation; changes remain subject to PR review
  and the coordinating agent's merge/release checks.

