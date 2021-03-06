---
title: Azure ストレージ テーブルのデータを暗号化する | Microsoft Docs
description: Azure Storage のテーブル データの暗号化について説明します。
services: storage
documentationcenter: na
author: MarkMcGeeAtAquent
manager: kfile
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/11/2018
ms.author: sngun
ms.openlocfilehash: 082e8a54cc8625a4bbdea2157f73874dbc86fde2
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "34660354"
---
# <a name="encrypt-table-data"></a>テーブル データを暗号化する
.NET Azure Storage クライアント ライブラリでは、挿入および置換操作の文字列エンティティ プロパティの暗号化がサポートされます。 暗号化された文字列はバイナリ プロパティとしてサービスで保存され、復号化された後、文字列に変換されて戻されます。    

テーブルの場合、暗号化ポリシーに加え、ユーザーは暗号化するプロパティを指定する必要があります。 これを実行するには、[EncryptProperty] 属性を指定するか (TableEntity から派生した POCO エンティティ用)、または要求オプションで暗号化リゾルバーを指定します。 暗号化リゾルバーは、パーティション キー、行キー、プロパティ名を取得するデリゲートで、プロパティを暗号化するかどうかを示すブール値を返します。 暗号化時、クライアント ライブラリはこの情報を使用して、ネットワークへの書き込み時にプロパティを暗号化するかどうかを決定します。 また、デリゲートは、プロパティの暗号化方法に関するロジックを使用する可能性にも備えます。 (X の場合、プロパティ A を暗号化し、それ以外の場合はプロパティ A および B を暗号化するなど。)エンティティの読み込み中、またはクエリの実行中は、この情報を指定する必要はありません。

## <a name="merge-support"></a>マージのサポート

現在、マージはサポートされていません。 別のキーを使用してプロパティのサブセットが以前に暗号化されている場合、新しいプロパティをマージしたり、メタデータを更新したりするとデータ損失が発生します。 マージでは、追加のサービス呼び出しをして既存のエンティティをサービスから読み込むか、プロパティごとに新しいキーを使用する必要があります。いずれの方法も、パフォーマンス上の理由でお勧めできません。     

テーブル データの暗号化については、「 [Microsoft Azure Storage のクライアント側の暗号化と Azure Key Vault](../common/storage-client-side-encryption.md)」を参照してください。  

## <a name="next-steps"></a>次の手順

- [テーブルの設計パターン](table-storage-design-patterns.md)
- [リレーションシップのモデル化](table-storage-design-modeling.md)
- [リレーションシップのモデル化](table-storage-design-modeling.md)
- [データの変更に対応した設計](table-storage-design-for-modification.md)