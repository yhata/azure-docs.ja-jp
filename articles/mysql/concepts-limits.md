---
title: Azure Database for MySQL の制限事項
description: この記事では、Azure Database for MySQL の制限 (接続数やストレージ エンジンのオプションなど) について説明します。
services: mysql
author: kamathsun
ms.author: sukamat
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 06/04/2018
ms.openlocfilehash: 3ec78b9aad45500a92a8f46f4bb2e654f97da8cb
ms.sourcegitcommit: 1b8665f1fff36a13af0cbc4c399c16f62e9884f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2018
ms.locfileid: "35264886"
---
# <a name="limitations-in-azure-database-for-mysql"></a>Azure Database for MySQL の制限事項
以降のセクションでは、容量、ストレージ エンジンのサポート、権限のサポート、データ操作ステートメントのサポート、およびデータベース サービスの機能に関する制限事項について説明します。 MySQL データベース エンジンに適用できる[一般的な制限事項](https://dev.mysql.com/doc/mysql-reslimits-excerpt/5.6/en/limits.html)も確認してください。

## <a name="maximum-connections"></a>最大接続数
価格レベルと仮想コアごとの最大接続数は次のとおりです。 

|**価格レベル**|**仮想コア数**| **最大接続数**|
|---|---|---|
|Basic| 1| 50|
|Basic| 2| 100|
|汎用| 2| 300|
|汎用| 4| 625|
|汎用| 8| 1250|
|汎用| 16| 2500|
|汎用| 32| 5000|
|メモリ最適化| 2| 600|
|メモリ最適化| 4| 1250|
|メモリ最適化| 8| 2500|
|メモリ最適化| 16| 5000|

接続数が制限を超えると、次のエラーが表示される場合があります。
> ERROR 1040 (08004): Too many connections

## <a name="storage-engine-support"></a>ストレージ エンジンのサポート

### <a name="supported"></a>サポートされています
- [InnoDB](https://dev.mysql.com/doc/refman/5.7/en/innodb-introduction.html)
- [MEMORY](https://dev.mysql.com/doc/refman/5.7/en/memory-storage-engine.html)

### <a name="unsupported"></a>サポートされていません
- [MyISAM](https://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html)
- [BLACKHOLE](https://dev.mysql.com/doc/refman/5.7/en/blackhole-storage-engine.html)
- [ARCHIVE](https://dev.mysql.com/doc/refman/5.7/en/archive-storage-engine.html)
- [FEDERATED](https://dev.mysql.com/doc/refman/5.7/en/federated-storage-engine.html)

## <a name="privilege-support"></a>権限のサポート

### <a name="unsupported"></a>サポートされていません
- DBA ロール: DBA ロールでは、多くのサーバー パラメーターおよび設定によって、誤ってサーバー パフォーマンスを低下させたり、DBMS の ACID プロパティを負数にしてしまったりする恐れがあります。 そのため、製品レベルのサービス整合性と SLA を維持するために、このサービスでは、DBA ロールを公開していません。 新しいデータベース インスタンスの作成時に構成される既定のユーザー アカウントによって、ユーザーは管理データベース インスタンスでほとんどの DDL および DML ステートメントを実行できます。 
- SUPER 権限: 同様に、SUPER 権限 ([SUPER 権限について](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_super)の記述を参照) も制限されています。

## <a name="data-manipulation-statement-support"></a>データ操作ステートメントのサポート

### <a name="supported"></a>サポートされています
- LOAD DATA INFILE - サポートされています。ただし、UNC パス (XSMB 経由でマウントされた Azure ストレージ) にリダイレクトされる [LOCAL] パラメーターを指定する必要があります。

### <a name="unsupported"></a>サポートされていません
- SELECT ...INTO OUTFILE

## <a name="functional-limitations"></a>機能制限

### <a name="scale-operations"></a>スケール操作
- 価格レベル間でのサーバーの動的スケーリングは現在サポートされていません。 つまり、Basic、汎用、メモリ最適化の各価格レベル間の切り替えはサポートされません。
- サーバー ストレージを減らすことはできません。

### <a name="server-version-upgrades"></a>サーバー バージョンのアップグレード
- データベース エンジンのメジャー バージョン間での自動移行は現在サポートされていません。

### <a name="point-in-time-restore"></a>ポイントインタイム リストア
- 別のサービス レベルやコンピューティング ユニットおよびストレージ サイズに復元することはできません。
- 削除されたサーバーへの復元はサポートされていません。

### <a name="subscription-management"></a>サブスクリプション管理
- サブスクリプションとリソース グループ間での事前作成されたサーバーの動的な移動は現在サポートされていません。

## <a name="current-known-issues"></a>現時点での既知の問題
- MySQL サーバー インスタンスでは、接続が確立された後に不正確なサーバー バージョンが表示されます。 正しいサーバー インスタンス バージョンを取得するには、MySQL プロンプトで select version(); コマンドを使用します。

## <a name="next-steps"></a>次の手順
- [各サービス レベルで使用できる内容について](concepts-pricing-tiers.md)
- [サポートされている MySQL Database バージョン](concepts-supported-versions.md)
