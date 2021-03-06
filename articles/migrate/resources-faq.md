---
title: Azure Migrate - よく寄せられる質問 (FAQ) | Microsoft Docs
description: Azure Migrate についてよく寄せられる質問に対応します
author: snehaamicrosoft
ms.service: azure-migrate
ms.topic: article
ms.date: 06/06/2018
ms.author: snehaa
ms.openlocfilehash: b18d2cecfd7556ad3f05d0f63435d16bc29ebab1
ms.sourcegitcommit: 3017211a7d51efd6cd87e8210ee13d57585c7e3b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34826135"
---
# <a name="azure-migrate---frequently-asked-questions-faq"></a>Azure Migrate - よく寄せられる質問 (FAQ)

この記事には、Azure Migrate に関してよく寄せられる質問が含まれます。 この記事の内容についてさらに質問がある場合は、[Azure Migrate フォーラム](http://aka.ms/AzureMigrateForum)に投稿してください。

## <a name="general"></a>全般

### <a name="how-is-azure-migrate-different-from-azure-site-recovery"></a>Azure Migrate と Azure Site Recovery の違いは何ですか。

Azure Migrate は、オンプレミスのワークロードを検出し、Azure への移行の計画を支援するアセスメント サービスです。 [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure) は、ディザスター リカバリー ソリューションであると同時に、オンプレミスのワークロードを Azure 内の IaaS VM に移行するのを支援します。 

### <a name="how-is-azure-migrate-different-from-azure-site-recovery-deployment-planner"></a>Azure Migrate と Azure Site Recovery Deployment Planner の違いは何ですか。

Azure Migrate は移行計画ツールで、Azure Site Recovery Deployment Planner はディザスター リカバリー (DR) 計画ツールです。

**VMware から Azure への移行**: オンプレミスのワークロードを Azure に移行する場合は、移行の計画に Azure Migrate を使用します。 Azure Migrate はオンプレミスのワークロードを評価し、ガイダンス、分析情報、メカニズムを提供して、Azure への移行を支援します。 移行計画の準備ができたら、Azure Site Recovery や Azure Database Migration Service などのサービスを使用して、Azure にマシンを移行できます。

**Hyper-V から Azure への移行**: Azure Migrate は現在、Azure への移行のための VMware 仮想マシンのアセスメントのみをサポートしています。 Azure Migrate では現在、Hyper-V をサポートするよう進めております。 その間は ASR Deployment Planner を利用できます。 Azure Migrate で Hyper-V のサポートが有効になったら、Azure Migrate を使用して Hyper-V のワークロードの移行を計画できます。

**VMware/Hyper-V から Azure への障害復旧**: Azure Site Recovery (ASR) を使用して Azure のディザスター リカバリー (DR) を実行する場合は、DR の計画に ASR Deployment Planner を使用します。 ASR Deployment Planner はお使いのオンプレミス環境の ASR 固有の詳細なアセスメントを実行します。 仮想マシンのレプリケーション、フェールオーバーなど、DR 操作が適切に実行されるために ASR によって要求されるレコメンデーションを提供します。  

### <a name="does-azure-migrate-need-vcenter-server-to-discover-a-vmware-environment"></a>Azure Migrate が VMware 環境を検出するために vCenter Server は必要ですか。

はい、Azure Migrate が VMware 環境を検出するには vCenter Server が必要です。 vCenter Server で管理されていない ESXi ホストの検出はサポートされていません。

## <a name="discovery"></a>探索

### <a name="what-data-is-collected-by-azure-migrate"></a>Azure Migrate によって収集されるデータは何ですか。

Azure Migrate は、アプライアンスベースの検出とエージェントベースの検出の 2 種類の検出をサポートしています。
アプライアンスベースの検出はオンプレミスの VM に関するメタデータを収集します。以下にアプライアンスによって収集されるメタデータの全一覧を示します。

**VM の構成データ**
- (vCenter 上の) VM の表示名
- VM のインベントリ パス (vCenter でのホスト/クラスター/フォルダー)
- IP アドレス
- MAC アドレス
- オペレーティング システム
- コア、ディスク、NIC の数
- メモリ サイズ、ディスク サイズ

**VM のパフォーマンス データ**
- CPU 使用率
- メモリ使用量
- VM に接続されている各ディスクの場合:
  - ディスク読み取りスループット
  - ディスク書き込みスループット
  - ディスク読み取り操作/秒
  - ディスク書き込み操作/秒
- VM に接続されている各ネットワーク アダプターの場合:
  - ネットワーク受信
  - ネットワーク送信

エージェントベースの検出は、アプライアンスベースの検出に加えて利用できるオプションで、ユーザーがオンプレミスの VM の[依存関係を視覚化する](how-to-create-group-machine-dependencies.md)のに役立ちます。 依存関係エージェントは FQDN、OS、IP アドレス、MAC アドレス、VM 内で実行されているプロセスや VM の受信/送信 TCP 接続などの詳細を収集します。 エージェントベースの検出は省略可能で、VM の依存関係を視覚化する必要がない場合は、エージェントをインストールしないことを選択できます。

### <a name="where-is-the-collected-data-stored-and-for-how-long"></a>収集されたデータはどこに、どれくらいの期間保存されますか。

コレクター アプライアンスによって収集されたデータは、移行プロジェクトの作成中に指定した Azure の場所に格納されます。 データは Microsoft サブスクリプションに安全に格納され、ユーザーがその Azure Migrate プロジェクトを削除すると削除されます。

依存関係の視覚化で、VM にエージェントをインストールした場合、依存関係エージェントによって収集されたデータは、ユーザーのサブスクリプションで作成された米国の OMS ワークスペースに格納されます。 このデータは、ユーザーが自身のサブスクリプションで OMS ワークスペースを削除すると削除されます。 [詳細情報](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization)。

### <a name="how-does-the-collector-communicate-with-the-vcenter-server-and-the-azure-migrate-service"></a>コレクターは vCenter Server や Azure Migrate サービスとどのように通信しますか。

コレクター アプライアンスは、そのアプライアンス内のユーザーが提供した資格情報を使用して、vCenter Server (ポート 443) に接続します。 VMware PowerCLI を使用して vCenter Server を照会し、vCenter Server によって管理される VM に関するメタデータを収集します。 VM の構成データ (コア数、メモリ、ディスク数、NIC など) のほか、過去 1 か月の各 VM のパフォーマンス履歴を vCenter Server から収集します。 その後、収集されたメタデータが Azure Migrate サービスに (https を介してインターネット上で) 送信され、アセスメントが行われます。 [詳細情報](concepts-collector.md)

### <a name="is-the-data-encrypted-at-rest-and-while-in-transit"></a>保存データや転送中のデータは暗号化されますか。

はい、収集された保存データや転送中のデータは暗号化されます。 アプライアンスによって収集されたメタデータは、https を介してインターネット上で安全に Azure Migrate サービスに送信されます。 収集されたメタデータは Microsoft サブスクリプション内の [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/database-encryption-at-rest) と [Azure Blob Storage](https://docs.microsoft.com/azure/storage/common/storage-service-encryption) に格納され、保存データは暗号化されます。

依存関係エージェントによって収集されたデータも転送中に暗号化され (安全な https チャネル)、ユーザーのサブスクリプションの Log Analytics ワークスペースに格納されます。 また、保存データも暗号化されます。

### <a name="how-can-i-discover-a-multi-tenant-environment-in-azure-migrate"></a>Azure Migrate でマルチテナント環境を検出するにはどうすればよいですか。

ある環境がテナント間で共有されており、別のテナントのサブスクリプションにある特定のテナントの VM を検出しないようにするには、コレクター アプライアンスのスコープ フィールドを使用して、検出範囲を指定します。 テナントがホストを共有している場合は、特定のテナントに属する VM のみに読み取り専用アクセス権を持つ資格情報を作成してから、コレクター アプライアンスでこの資格情報を使用し、スコープをホストとして指定して検出を行います。 または、vCenter Server で共有ホストの下にフォルダー (tenant1 の場合は folder1、tenant2 の場合は folder2 とします) を作成し、tenant1 の VM を folder1 に、tenant2 の VM を folder2 に移動してから、適切なフォルダーを指定して、適宜、コレクターの検出範囲を指定することもできます。

### <a name="how-many-virtual-machines-can-be-discovered-in-a-single-migration-project"></a>1 つの移行プロジェクトで検出できる仮想マシンの数はいくつですか。

1 つの移行プロジェクトで 1500 台の仮想マシンを検出できます。 オンプレミス環境に複数のマシンがある場合は、Azure Migrate で大規模な環境を検索する方法の[詳細](how-to-scale-assessment.md)を確認してください。

## <a name="dependency-visualization"></a>依存関係の視覚化

### <a name="do-i-need-to-pay-to-use-the-dependency-visualization-feature"></a>依存関係の視覚化機能の利用には料金の支払いが発生しますか。

Azure Migrate は、追加料金なしで利用できます。 Azure Migrate の価格については、[こちら](https://azure.microsoft.com/pricing/details/azure-migrate/)を参照してください。

### <a name="can-i-use-an-existing-workspace-for-dependency-visualization"></a>依存関係の視覚化に既存のワークスペースを使用できますか。

Azure Migrate では依存関係の視覚化に既存のワークスペースを使用できません。ただし、Microsoft Monitoring Agent (MMA) はマルチホーミングをサポートしており、複数のワークスペースにデータを送信できます。 このため、既にエージェントがワークスペースにデプロイされて構成されている場合、MMA エージェントのマルチホーミングを活用し、それを (既存のワークスペースに加えて) Azure Migrate のワークスペースに構成して、機能させることができます。 MMA エージェントのマルチホーミングを有効にする方法については、[こちら](https://blogs.technet.microsoft.com/msoms/2016/05/26/oms-log-analytics-agent-multi-homing-support/)のブログで確認してください。

## <a name="next-steps"></a>次の手順

- [Azure Migrate](migrate-overview.md) の概要を確認する
- VMware 環境での[検出とアセスメント](tutorial-assessment-vmware.md)の方法を確認しする
