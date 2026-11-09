# pgAudit Windows x64 バイナリ利用ガイド

## 1. ZIPを選択

使用中のPostgreSQLメジャーバージョンに一致するZIPを使用してください。異なるメジャーバージョン向けのDLLは流用しないでください。

## 2. ファイル配置

一般的なWindows版PostgreSQLでは:

~~~text
ZIP\lib\pgaudit.dll
  -> <PostgreSQL>\lib\pgaudit.dll

ZIP\share\extension\*
  -> <PostgreSQL>\share\extension\
~~~

へ配置します。

## 3. preload

`postgresql.conf`:

~~~conf
shared_preload_libraries = 'pgaudit'
~~~

既にプリロードする拡張機能が指定されている場合は、カンマ区切りで追加します。

設定後はPostgreSQLを再起動してください。

## 4. Extension作成

~~~sql
CREATE EXTENSION pgaudit;
~~~

## 5. 最小設定例

例としてsession auditでREAD/WRITE/DDLを対象にする場合:

~~~conf
pgaudit.log = 'read,write,ddl'
~~~

設定可能な監査クラス、オブジェクト監査、ロール、パラメータなどは、使用するpgAuditバージョンの公式ドキュメントを確認してください。監査ログは機密情報やSQLパラメータを含み得るため、保存・閲覧・ローテーション方針を含めて設計してください。

## CIで確認している内容

pgextwinではPG14〜18すべてで:

- `shared_preload_libraries=pgaudit` で起動
- `CREATE EXTENSION pgaudit`
- CREATE TABLE
- INSERT
- SELECT
- server log内の `AUDIT:` DDL/WRITE/READ記録

まで実動作確認します。

本体仕様についてはupstream pgAuditドキュメントを正規の情報源としてください。
