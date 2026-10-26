# Dependency Security

The real installation source, `pyproject.toml`, pins `filelock==3.20.3`.
This maintains the classic FileLock interface accepted by upstream combo-lock's
`filelock~=3.0` requirement and Python 3.10. No direct URL or scanner exception
is used, and no claim is made that future advisories cannot affect this version.

## Evidence

The GitHub Advisory Database lists older affected ranges `<3.20.1`
([GHSA-w853-jp5j-5j7f](https://github.com/advisories/GHSA-w853-jp5j-5j7f)) and
`<3.20.3` ([GHSA-qmgc-5h2g-mvrw](https://github.com/advisories/GHSA-qmgc-5h2g-mvrw)).
The newer HIGH [GHSA-v4x8-3wr5-3wq8](https://github.com/advisories/GHSA-v4x8-3wr5-3wq8)
affects `>=3.20.4,<=4.2.0`; the other five published ranges begin at 3.20.4,
3.22.0, or 4.1.0. Exact 3.20.3 lies outside all eight ranges.

Python >=3.10 is required by filelock3.20.3; Python 3.9 is not supported. The supported bus client requires bitstring>=4.1.1,<5. Schema-v2 Client compatibility requires plugin-manager>=0.6.0a1,<0.9; test extras retain >=0.7.1a1 with the same upper bound. SQLite behavior and schema remain unchanged.

This is a legacy-fork compatibility boundary, not a platform-wide downgrade.
`SQLiteDB.add_item` and `SQLiteDB._row_to_client` require `Client.crypto_key`,
which manager 0.9 and later do not provide. The unrestricted graph produces
42 failures. Consumers requiring manager >=0.10, including the current quota
plugin, must use a compatible maintained SQLite release instead of this fork.
The current listener uses SQLite0.4.3a9, not this fork's0.4.0a6. No hidden or
external consumer inventory is claimed to have been exhaustively checked.

## Verification

- 67 passed, 3 skipped against manager0.6.0a1 and the supported upper endpoint
  0.8.0a3 (SQLCipher unavailable locally; e2e excluded).
- A clean resolver dry-run rejects co-installation with the modern quota plugin
  because its manager>=0.10 requirement conflicts with this real metadata bound.
- [Regression tests](../tests/test_dependency_security.py) check the installed
  dependency and real classic-lock contention/release.
- Wheel and sdist builds pass; built wheel metadata contains exact filelock==3.20.3 and no direct-URL dependency.
- [SQLiteDB](../hivemind_sqlite_database/__init__.py) remains unchanged.

A passing library test does not approve a production rollout. The consuming
application's normal build and vulnerability gates remain required.

