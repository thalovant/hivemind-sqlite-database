# FAQ

## Why is filelock pinned exactly?

3.20.3 contains the earlier fixes and predates the newer affected features.
A broad 3.x range can select an affected version. See the primary ranges and
verified limits in [dependency security](docs/dependency-security.md).

## Does this alter runtime behavior?

[SQLiteDB](hivemind_sqlite_database/__init__.py) is unchanged. The regression tests exercise classic
lock contention and real dependency metadata. Python >=3.10 is required by filelock3.20.3; Python 3.9 is not supported.
The supported bus client requires bitstring>=4.1.1,<5. Schema-v2 Client
compatibility requires plugin-manager>=0.6.0a1,<0.9. Test extras match the
existing policy-E2E workflow: hivescope0.4.0a2, core4.3.0a2, agent0.2.0a1 and
manager0.6.0a1. SQLite behavior and schema remain unchanged.

## Can this fork replace the current listener's SQLite package?

No. It is a legacy schema implementation that uses `Client.crypto_key`.
The modern quota plugin requires manager>=0.10 and cannot co-install with this
fork's honest support range. The maintained listener uses SQLite0.4.3a9.
The dependency repair neither publishes this fork nor changes listener adoption.

