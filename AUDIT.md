# Audit

The security constraint is carried by the real installer, not solely by a
scanner input. [Dependency tests](tests/test_dependency_security.py) verify
exact filelock selection and lock behavior. 67 passed, 3 skipped (SQLCipher unavailable; e2e excluded).

Python >=3.10 is required by filelock3.20.3; Python 3.9 is not supported. The supported bus client requires bitstring>=4.1.1,<5. Schema-v2 Client compatibility requires plugin-manager>=0.6.0a1,<0.9; test extras retain >=0.7.1a1 with the same upper bound. SQLite behavior and schema remain unchanged.

SQLiteDB in [the runtime source](hivemind_sqlite_database/__init__.py) is not modified.
This is not a complete audit of that implementation. Future advisory checks
and consumer artifact tests remain required; [evidence](docs/dependency-security.md).

The legacy implementation accesses `Client.crypto_key`, removed by manager0.9.
An unrestricted fresh graph produces42 failures; the declared legacy range
passes67 tests with3 local SQLCipher skips at both supported endpoints. The
current quota plugin requires manager>=0.10 and is intentionally incompatible;
a clean resolver dry-run rejects that combination. Do not deploy this fork as
a replacement for the maintained SQLite0.4.3a9 in the current listener.

