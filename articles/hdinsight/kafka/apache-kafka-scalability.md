---
title: Apache Kafka のスケーラビリティの向上 - Azure HDInsight | Microsoft Docs
description: スケーラビリティが向上するように Azure HDInsight 上の Apache Kafka クラスター用の管理ディスクを構成する方法を説明します。
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: cgronlun
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: ''
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/30/2018
ms.author: larryfr
ms.openlocfilehash: 1a104f4b4dee340f43c1dba01b83cb80e138a9ec
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "34626725"
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>HDInsight 上の Apache Kafka 用に記憶域とスケーラビリティを構成する

HDInsight 上の Apache Kafka によって使われる複数の管理ディスクを構成する方法を説明します。

HDInsight 上の Kafka は、HDInsight クラスターの仮想マシンのローカル ディスクを使います。 Kafka は I/O が非常に多いため、[Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md) を使ってノードごとに高いスループットと多くの記憶域を提供します。 従来の仮想ハード ドライブ (VHD) を Kafka 用に使う場合は、各ノードは 1 TB に制限されます。 管理ディスクの場合は、複数のディスクを使ってクラスターの各ノードを 16 TB にできます。

次の図は、管理ディスクを使う前と使った後の HDInsight 上の Kafka を比較したものです。

![HDInsight 上の Kafka で、VM ごとに単一の VHD を使った場合と、VM ごとに複数の管理ディスクを使った場合の比較](./media/apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>管理ディスクを構成する: Azure Portal

1. 「[HDInsight クラスターの作成](../hdinsight-hadoop-create-linux-clusters-portal.md)」の手順に従って、Portal を使ってクラスターを作成する一般的な手順を理解します。 Portal の作成プロセスは実行しないでください。

2. __[クラスター サイズ]__ セクションの __[Disks per worker node\(ワーカー ノードごとのディスク数\)]__ フィールドを使って、ディスクの数を構成します。

    > [!NOTE]
    > 管理ディスクの種類は、__Standard__ (HDD) または __Premium__ (SSD) です。 Premium ディスクは、DS および GS シリーズの VM で使われます。 他の種類の VM はすべて Standard を使います。

    ![ワーカー ノードごとのディスク数が強調表示されている [クラスター サイズ] セクションの画像](./media/apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>管理ディスクを構成する: Resource Manager テンプレート

Kafka クラスターのワーカー ノードによって使われるディスクの数を制御するには、テンプレートの次のセクションを使います。

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

[https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json) に、管理ディスクを構成する方法を示す完全なテンプレートがあります。

## <a name="next-steps"></a>次の手順

HDInsight 上の Kafka の操作の詳細については、次のドキュメントを参照してください。

* [MirrorMaker を使用した HDInsight での Kafka のレプリカの作成](apache-kafka-mirroring.md)
* [HDInsight での Kafka に Apache Storm を使用する](../hdinsight-apache-storm-with-kafka.md)
* [HDInsight での Kafka に Apache Spark を使用する](../hdinsight-apache-spark-with-kafka.md)
* [Azure 仮想ネットワーク経由で Kafka に接続する](apache-kafka-connect-vpn-gateway.md)

* [Kafka での管理ディスクに関する HDInsight ブログ](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)