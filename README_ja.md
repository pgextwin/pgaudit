# pgAudit — Windows x64 バイナリ

[English](README.md) | 日本語

[pgAudit](https://github.com/pgaudit/pgaudit)の**非公式Windows x64バイナリ**です。PostgreSQLのセッション監査とオブジェクト監査のログを記録します。

## ダウンロードと対応環境

[最新の公開Release](https://github.com/pgextwin/pgaudit/releases/latest)から、利用中のPostgreSQLメジャーバージョン向けのZIPを選んでください。[過去のReleases](https://github.com/pgextwin/pgaudit/releases)も確認できます。PostgreSQL **14〜18**向けの公開状況は[pgextwinカタログ](https://pgextwin.github.io/website/ja/)を参照してください。PostgreSQL 14のコミュニティサポートは2026年11月12日に終了します。

## インストール

1. バックアップを取り、[上流ドキュメント](https://github.com/pgaudit/pgaudit)で導入要件を確認します。
2. 既存ファイルを置き換える前にPostgreSQLを停止します。対応するZIP内のlib/とshare/extension/のファイルを、PostgreSQLの同名ディレクトリへ配置します。
3. pgAuditはPostgreSQLメジャーバージョンごとに上流のバージョンが異なります。postgresql.confのshared_preload_librariesへpgauditを追加して起動します。オブジェクト監査などで必要な場合は、上流の手順に従ってCREATE EXTENSION pgaudit;を実行してください。
4. 設定の反映後にPostgreSQLを起動し、検証環境で動作を確認してください。

ReleaseのSHA256SUMS.txtでZIPの整合性を確認できます。SPDX形式のSBOM、脆弱性レポート、署名付き証明の有無もReleaseで確認できます。

## ライセンス

機能、設定、制限事項は[上流のpgAudit](https://github.com/pgaudit/pgaudit)を参照してください。本配布は上流公式のWindows版ではありません。ライセンスは同梱の表記に従います。
