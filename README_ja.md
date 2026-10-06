# pgAudit Windows バイナリ

[English](README.md) | **日本語**

このリポジトリでは、[pgAudit](https://github.com/pgaudit/pgaudit) の **非公式 Windows x64 バイナリ**を提供します。

pgAuditはPostgreSQLメジャーごとにrelease系列が異なるため、各PostgreSQLに対応する公式tagを固定してbuildします。

| PostgreSQL | upstream ref | pgAudit | 検証PostgreSQL |
|---:|---|---:|---:|
| 14 | `1.6.3` | 1.6.3 | 14.24 |
| 15 | `1.7.1` | 1.7.1 | 15.19 |
| 16 | `16.1` | 16.1 | 16.15 |
| 17 | `17.1` | 17.1 | 17.11 |
| 18 | `18.0` | 18.0 | 18.6 |

初回のpgextwin Release tagは最新系列を代表して `v18.0-windows.1` とします。ただし各ZIPは必ず表の対応upstream refからbuildします。

## 導入

1. PostgreSQLメジャーと一致するZIPを使用します。
2. PostgreSQLを停止します。
3. `lib/pgaudit.dll` をPostgreSQLの `lib` へコピーします。
4. `share/extension/*` を `share/extension` へコピーします。
5. `postgresql.conf` の `shared_preload_libraries` に `pgaudit` を追加します。
6. PostgreSQLを再起動します。
7. 対象databaseで `CREATE EXTENSION pgaudit;` を実行します。

Windows固有の手順は [docs/windows_ja.md](docs/windows_ja.md) を参照してください。

## CIの合格条件

PG14〜18のすべてで、DLL buildだけでなく実際にPostgreSQLを起動し、pgAuditをpreloadしてExtensionを作成します。その後DDL・INSERT・SELECTを実行し、PostgreSQL server logに以下の実監査記録が出ることを確認します。

- DDL / CREATE TABLE
- WRITE / INSERT
- READ / SELECT

過去のWindows報告にあった「buildは通るが必要symbolを解決できない」「loadできても監査ログが正しく出ない」ケースを防ぐためです。

## ライセンス

LICENSEはupstream pgAuditの内容をそのまま保持し、CIで固定tagのupstream LICENSEと完全一致を検証します。

本バイナリはpgextwinによる非公式配布です。
