# pgAudit — Windows x64

[日本語](README_ja.md) | English

This repository distributes **unofficial Windows x64 binaries** of [pgAudit](https://github.com/pgaudit/pgaudit). provides PostgreSQL session and object audit logging.

## Download

Use the [latest published Release](https://github.com/pgextwin/pgaudit/releases/latest) or [all Releases](https://github.com/pgextwin/pgaudit/releases). Published PostgreSQL **14–18** packages are listed in the [pgextwin catalog](https://pgextwin.github.io/website/en/). Select the ZIP for your PostgreSQL major. PostgreSQL 14 community support ends November 12, 2026.

## Installation

1. Back up your environment and review the [upstream setup guide](https://github.com/pgaudit/pgaudit).
2. Stop PostgreSQL before replacing files. Copy the files in the matching ZIP's lib/ and share/extension/ directories to your PostgreSQL installation, where present.
3. pgAudit uses a different upstream version for each PostgreSQL major. Configure shared_preload_libraries with pgaudit and start PostgreSQL. CREATE EXTENSION pgaudit; is used when required for object audit logging; follow upstream configuration and privilege guidance.
4. Start or restart PostgreSQL after applying the configuration. Confirm operation in a test environment.

Use SHA256SUMS.txt attached to the Release to verify your downloaded ZIP. Other available materials may include SPDX SBOMs, vulnerability reports, and signed attestations.

## License

The upstream project documents audit/SQL behavior, settings, and limitations. This is an independent Windows package, not an official upstream distribution. See the included license notices.
