---
title: Graph API の Azure Cosmos DB グローバル分散チュートリアル | Microsoft Docs
description: Graph API を使用して Azure Cosmos DB グローバル分散を設定する方法について説明します。
services: cosmos-db
keywords: グローバル分散, グラフ, gremlin
author: luisbosquez
manager: kfile
editor: cgronlun
ms.service: cosmos-db
ms.component: cosmosdb-graph
ms.devlang: na
ms.topic: tutorial
ms.date: 01/02/2018
ms.author: lbosq
ms.custom: mvc
ms.openlocfilehash: 61004a735f731cfd1303cf40b6e60cba496e942a
ms.sourcegitcommit: 6116082991b98c8ee7a3ab0927cf588c3972eeaa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2018
ms.locfileid: "34763682"
---
# <a name="set-up-azure-cosmos-db-global-distribution-using-the-graph-api"></a>Graph API を使用して Azure Cosmos DB グローバル分散を設定する

この記事では、Azure Portal を使用して Azure Cosmos DB グローバル分散をセットアップし、Graph API を使用して接続する方法を説明します。

この記事に含まれるタスクは次のとおりです。 

> [!div class="checklist"]
> * Azure Portal を使用してグローバル分散を構成する
> * [Graph API](graph-introduction.md) を使用してグローバル分散を構成する

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-graph-api-using-the-net-sdk"></a>.NET SDK で Graph API を使用して優先リージョンに接続する

Graph API は SQL API の拡張ライブラリとして公開されます。

[グローバル配布](distribute-data-globally.md)を活用するために、クライアント アプリケーションでは、ドキュメントの操作の実行に使用するリージョンの順序付き優先リストを指定できます。 これは、接続ポリシーを設定して行います。 Azure Cosmos DB アカウント構成、現在のリージョンの可用性、指定された優先リストに基づいて、書き込み操作と読み取り操作を実行する SDK によって最適なエンドポイントが選択されます。

この優先リストは、SDK を使用して接続を初期化する際に指定されます。 SDK は、Azure リージョンの順序付きリストである省略可能なパラメーター "PreferredLocations" を受け取ります。

* **書き込み**: SDK は自動的に、すべての書き込みを現在の書き込みリージョンに送信します。
* **読み取り**: 読み取りはすべて、PreferredLocations リストで使用可能な最初のリージョンに送信されます。 要求が失敗すると、クライアントはリストにある次のリージョンを試します。これが繰り返されます。 SDK は、PreferredLocations で指定されたリージョンからの読み取りのみを試みます。 このため、3 つのリージョンで Cosmos DB アカウントが利用できるものの、クライアントが PreferredLocations の非書き込みリージョンを 2 つだけ指定している場合などには、書き込みリージョンの外で読み取りが処理されません。これはフェールオーバーの場合にもあてはまります。

アプリケーションは、WriteEndpoint と ReadEndpoint の 2 つのプロパティをチェックすることで、SDK によって選択された現在の書き込みエンドポイントと読み取りエンドポイントを確認できます。これらのプロパティは SDK バージョン 1.8 以上で利用可能です。 PreferredLocations プロパティが設定されていない場合、すべての要求が現在の書き込みリージョンから処理されます。

### <a name="using-the-sdk"></a>SDK を使用する

たとえば、.NET SDK で、`DocumentClient`コンストラクターの `ConnectionPolicy` パラメーターには `PreferredLocations` というプロパティがあります。 このプロパティにリージョン名の一覧を設定できます。 [Azure リージョン][regions]の表示名を `PreferredLocations` に含めて指定できます。

> [!NOTE]
> エンドポイントの URL は、有効期間が長い定数と見なさないでください。 これらは任意のタイミングでサービスによって更新される可能性があります。 SDK はこの変更を自動的に処理します。
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect to Azure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

このチュートリアルはこれで終わりです。 [Azure Cosmos DB の一貫性レベル](consistency-levels.md)に関する記事を読んで、グローバルにレプリケートされたアカウントの整合性を管理する方法について確認できます。 また、Azure Cosmos DB におけるグローバル データベース レプリケーションの動作の詳細については、[Azure Cosmos DB を使用したデータのグローバル分散](distribute-data-globally.md)に関する記事を参照してください。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、次の手順を行いました。

> [!div class="checklist"]
> * Azure Portal を使用してグローバル分散を構成する
> * SQL API を使用してグローバル分散を構成する

これで次のチュートリアルに進むことができます。Azure Cosmos DB ローカル エミュレーターを使用してローカルで開発する方法について学びます。

> [!div class="nextstepaction"]
> [エミュレーターを使用したローカル開発](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

