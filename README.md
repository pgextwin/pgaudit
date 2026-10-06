# pgAudit Windows binaries

[日本語](README_ja.md) | **English**

This repository provides **unofficial Windows x64 binaries** of [pgAudit](https://github.com/pgaudit/pgaudit).

pgAudit maintains a PostgreSQL-major-specific release line, so each PostgreSQL major is built from the matching official upstream tag.

| PostgreSQL | Upstream ref | pgAudit | Tested PostgreSQL |
|---:|---|---:|---:|
| 14 | `1.6.3` | 1.6.3 | 14.24 |
| 15 | `1.7.1` | 1.7.1 | 15.19 |
| 16 | `16.1` | 16.1 | 16.15 |
| 17 | `17.1` | 17.1 | 17.11 |
| 18 | `18.0` | 18.0 | 18.6 |

The current pgextwin package-set Release is:

~~~text
v18.0-windows.1
~~~

The release tag represents the newest supported pgAudit series. Each ZIP records the exact upstream ref and PostgreSQL version used to build it.

## Installation

1. Use the ZIP matching the PostgreSQL major version.
2. Stop PostgreSQL before replacing the DLL.
3. Copy `lib/pgaudit.dll` to PostgreSQL's `lib`.
4. Copy `share/extension/*` to PostgreSQL's `share/extension`.
5. Add `pgaudit` to `shared_preload_libraries`.
6. Restart PostgreSQL.
7. Run:

~~~sql
CREATE EXTENSION pgaudit;
~~~

pgAudit must be preloaded before the extension is created. Configure `pgaudit.log` and the other pgAudit parameters according to the upstream documentation and your audit policy.

See [docs/windows_ja.md](docs/windows_ja.md) for the Windows-specific procedure.

## Windows build

The validated build compiles the exact pinned upstream `pgaudit.c` with MSVC x64 and generates an explicit DEF file containing:

- `Pg_magic_func`
- `_PG_init`
- SQL-callable functions found through `PG_FUNCTION_INFO_V1(...)`

This matters on Windows because historical pgAudit builds could compile while failing to expose required event-trigger symbols correctly.

## Functional CI

A successful DLL build is not sufficient. Every supported PostgreSQL major must pass:

1. exact upstream LICENSE verification,
2. MSVC x64 build,
3. PostgreSQL startup with `shared_preload_libraries=pgaudit`,
4. `CREATE EXTENSION pgaudit`,
5. execute DDL, INSERT, and SELECT statements,
6. inspect the actual PostgreSQL server log,
7. require pgAudit `AUDIT:` records for DDL, WRITE, and READ,
8. package the Windows x64 ZIP.

Pull requests and `main` validate only. A `release/<tag>` branch triggers publication after the full matrix passes.

## Licensing

The repository LICENSE is an exact copy of the pinned upstream pgAudit license. Release ZIPs copy LICENSE directly from the upstream checkout used for that package.

These binaries are unofficial pgextwin builds and are not official pgAudit binary releases.
