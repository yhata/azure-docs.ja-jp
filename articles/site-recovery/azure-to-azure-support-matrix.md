---
title: Azure 間でのレプリケートに関する Azure Site Recovery のサポート マトリックス | Microsoft Docs
description: ディザスター リカバリー (DR) のニーズに応じて、リージョン間で Azure 仮想マシン (VM) を Azure Site Recovery でレプリケートするときのサポートされるオペレーティング システムと構成についてまとめます。
services: site-recovery
author: sujayt
manager: rochakm
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.date: 05/31/2018
ms.author: sujayt
ms.openlocfilehash: 19c439e1182086b91d05f8bb23bc6c07c34a12a2
ms.sourcegitcommit: 59fffec8043c3da2fcf31ca5036a55bbd62e519c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34716314"
---
# <a name="support-matrix-for-replicating-from-one-azure-region-to-another"></a>Azure リージョン間でレプリケートするためのマトリックスのサポート



この記事では、リージョン間で Azure 仮想マシンをレプリケートおよび復旧するときの、Azure Site Recovery のサポートされる構成とコンポーネントをまとめます。

## <a name="user-interface-options"></a>ユーザー インターフェイスのオプション

**ユーザー インターフェイス** |  **サポートされるかどうか**
--- | ---
**Azure Portal** | サポートされています
**クラシック ポータル** | サポートされていません
**PowerShell** | [PowerShell を使用した Azure から Azure へのレプリケーション](azure-to-azure-powershell.md)
**REST API** | 現在、サポートされていません
**CLI** | 現在、サポートされていません


## <a name="resource-move-support"></a>リソースの移動のサポート

**リソースの移動の種類** | **サポートされるかどうか** | **解説**  
--- | --- | ---
**リソース グループ間の資格情報コンテナーの移動** | サポートされていません |リソース グループ間で Recovery Services コンテナーを移動できません。
**リソース グループ間のコンピューティング、ストレージ、およびネットワークの移動** | サポートされていません |レプリケーションを有効にした後、仮想マシン (またはストレージ、ネットワークなどの関連するコンポーネント) を移動する場合は、レプリケーションを無効にしてから、仮想マシンのレプリケーションを再度有効にする必要があります。



## <a name="support-for-deployment-models"></a>デプロイ モデルのサポート

**デプロイ モデル** | **サポートされるかどうか** | **解説**  
--- | --- | ---
**クラシック** | サポートされています | クラシック仮想マシンをレプリケートした場合は、クラシック仮想マシンとしてのみ復旧できます。 その仮想マシンを、Resource Manager 仮想マシンとして復旧することはできません。 仮想ネットワークを使用しないで、Azure リージョンに直接クラシック VM をデプロイする場合は、サポートされていません。
**Resource Manager** | サポートされています |

>[!NOTE]
>
> 1. ディザスター リカバリー シナリオで、あるサブスクリプションから別のサブスクリプションに Azure 仮想マシンをレプリケートする処理はサポートされていません。
> 2. サブスクリプション全体の Azure 仮想マシンの移行はサポートされていません。
> 3. 同じリージョン内の Azure 仮想マシンの移行はサポートされていません。
> 4. クラシック デプロイ モデルから Resource Manager デプロイ モデルへの Azure 仮想マシンの移行はサポートされていません。

## <a name="support-for-replicated-machine-os-versions"></a>レプリケートされるマシンの OS バージョンのサポート

次のサポートは、ここで示す OS で実行される任意のワークロードに適用可能です。

#### <a name="windows"></a>Windows

- Windows Server 2016 (サーバー コア、デスクトップ エクスペリエンス搭載サーバー)*
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1 以降

>[!NOTE]
>
> \* Windows Server 2016 の Nano Server はサポートされていません。

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 6.7、6.8、6.9、7.0、7.1、7.2、7.3、7.4
- CentOS 6.5、6.6、6.7、6.8、6.9、7.0、7.1、7.2、7.3、7.4
- Ubuntu 14.04 LTS Server[ (サポートされるカーネルのバージョン)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Ubuntu 16.04 LTS Server[ (サポートされるカーネルのバージョン)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Debian 7 [ (サポートされるカーネルのバージョン)](#supported-debian-kernel-versions-for-azure-virtual-machines)
- Debian 8 [ (サポートされるカーネルのバージョン)](#supported-debian-kernel-versions-for-azure-virtual-machines)
- Red Hat 互換カーネルまたは Unbreakable Enterprise Kernel リリース 3 (UEK3) を実行している Oracle Enterprise Linux 6.4、6.5
- SUSE Linux Enterprise Server 11 SP3
- SUSE Linux Enterprise Server 11 SP4

(レプリケートするマシンの SLES 11 SP3 から SLES 11 SP4 へのアップグレードはサポートされていません。 レプリケートされるマシンが SLES 11SP3 から SLES 11 SP4 にアップグレードされた場合は、アップグレード後にレプリケーションを無効にし、再度マシンを保護する必要があります。)

>[!NOTE]
>
> パスワード ベースの認証とログインを使用しており、cloud-init パッケージを使用してクラウド仮想マシンを構成する Ubuntu サーバーでは、(cloudinit 構成に応じて) フェールオーバー時にパスワード ベースのログインが無効になっている場合があります。パスワード ベースのログインは、Azure Portal でフェールオーバーされた仮想マシンの設定メニュー ([サポート + トラブルシューティング] セクションにある) からパスワードをリセットして、仮想マシンで再度有効にすることができます。

### <a name="supported-ubuntu-kernel-versions-for-azure-virtual-machines"></a>Azure 仮想マシン用のサポートされる Ubuntu カーネル バージョン

**リリース** | **モビリティ サービス バージョン** | **カーネル バージョン** |
--- | --- | --- |
14.04 LTS | 9.13 | 3.13.0-24-generic ～ 3.13.0-137-generic、<br/>3.16.0-25-generic ～ 3.16.0-77-generic、<br/>3.19.0-18-generic ～ 3.19.0-80-generic、<br/>4.2.0-18-generic ～ 4.2.0-42-generic、<br/>4.4.0-21-generic ～ 4.4.0-104-generic |
14.04 LTS | 9.14 | 3.13.0-24-generic ～ 3.13.0-141-generic、<br/>3.16.0-25-generic ～ 3.16.0-77-generic、<br/>3.19.0-18-generic ～ 3.19.0-80-generic、<br/>4.2.0-18-generic ～ 4.2.0-42-generic、<br/>4.4.0-21-generic ～ 4.4.0-112-generic |
14.04 LTS | 9.15 | 3.13.0-24-generic ～ 3.13.0-143-generic、<br/>3.16.0-25-generic ～ 3.16.0-77-generic、<br/>3.19.0-18-generic ～ 3.19.0-80-generic、<br/>4.2.0-18-generic ～ 4.2.0-42-generic、<br/>4.4.0-21-generic ～ 4.4.0-116-generic |
14.04 LTS | 9.16 | 3.13.0-24-generic ～ 3.13.0-144-generic、<br/>3.16.0-25-generic ～ 3.16.0-77-generic、<br/>3.19.0-18-generic ～ 3.19.0-80-generic、<br/>4.2.0-18-generic ～ 4.2.0-42-generic、<br/>4.4.0-21-generic ～ 4.4.0-119-generic、 |
16.04 LTS | 9.13 | 4.4.0-21-generic ～ 4.4.0-104-generic、<br/>4.8.0-34-generic ～ 4.8.0-58-generic、<br/>4.10.0-14-generic ～ 4.10.0-42-generic |
16.04 LTS | 9.14 | 4.4.0-21-generic ～ 4.4.0-112-generic、<br/>4.8.0-34-generic ～ 4.8.0-58-generic、<br/>4.10.0-14-generic ～ 4.10.0-42-generic、<br/>4.11.0-13-generic ～ 4.11.0-14-generic、<br/>4.13.0-16-generic ～ 4.13.0-32-generic、<br/>4.11.0-1009-azure ～ 4.11.0-1016-azure、<br/>4.13.0-1005-azure ～ 4.13.0-1009-azure |
16.04 LTS | 9.15 | 4.4.0-21-generic ～ 4.4.0-116-generic、<br/>4.8.0-34-generic ～ 4.8.0-58-generic、<br/>4.10.0-14-generic ～ 4.10.0-42-generic、<br/>4.11.0-13-generic ～ 4.11.0-14-generic、<br/>4.13.0-16-generic ～ 4.13.0-37-generic、<br/>4.11.0-1009-azure ～ 4.11.0-1016-azure、<br/>4.13.0-1005-azure ～ 4.13.0-1012-azure |
16.04 LTS | 9.16 | 4.4.0-21-generic ～ 4.4.0-119-generic、<br/>4.8.0-34-generic ～ 4.8.0-58-generic、<br/>4.10.0-14-generic ～ 4.10.0-42-generic、<br/>4.11.0-13-generic ～ 4.11.0-14-generic、<br/>4.13.0-16-generic ～ 4.13.0-38-generic、<br/>4.11.0-1009-azure ～ 4.11.0-1016-azure、<br/>4.13.0-1005-azure ～ 4.13.0-1012-azure |


### <a name="supported-debian-kernel-versions-for-azure-virtual-machines"></a>Azure 仮想マシン用のサポートされる Debian カーネル バージョン

**リリース** | **モビリティ サービス バージョン** | **カーネル バージョン** |
--- | --- | --- |
Debian 7 | 9.14、9.15、9.16 | 3.2.0-4-amd64 ～ 3.2.0-5-amd64、3.16.0-0.bpo.4-amd64 |
Debian 8 | 9.14、9.15、9.16 | 3.16.0-4-amd64 ～ 3.16.0-5-amd64、4.9.0-0.bpo.4-amd64 ～ 4.9.0-0.bpo.5-amd64 |

## <a name="supported-file-systems-and-guest-storage-configurations-on-azure-virtual-machines-running-linux-os"></a>Linux OS を実行している Azure 仮想マシンでサポートされるファイル システムおよびゲスト ストレージ構成

* ファイル システム: ext3、ext4、ReiserFS (Suse Linux Enterprise Server のみ)、XFS
* ボリューム マネージャー: LVM2
* マルチパス ソフトウェア: デバイス マッパー

## <a name="region-support"></a>リージョンのサポート

同じ地理クラスター内の 2 つのリージョン間で VM をレプリケートして、復旧できます。

**地理クラスター** | **Azure リージョン**
-- | --
アメリカ合衆国 | カナダ東部、カナダ中部、米国中南部、米国中西部、米国東部、米国東部 2、米国西部、米国西部 2、米国中部、米国中北部
ヨーロッパ | 英国西部、英国南部、北ヨーロッパ、西ヨーロッパ、フランス中部、フランス南部
アジア | インド南部、インド中部、東南アジア、東アジア、東日本、西日本、韓国中部、韓国南部
オーストラリア   | オーストラリア東部、オーストラリア南東部
Azure Government    | 米国政府バージニア、米国政府アイオワ、米国政府アリゾナ、米国政府テキサス、米国防総省東部、米国防総省中部
ドイツ | ドイツ中部、ドイツ北東部
中国 | 中国東部、中国北部

>[!NOTE]
>
> ブラジル南部リージョンについては、米国中南部、米国中西部、米国東部、米国東部 2、米国西部、米国西部 2、米国中北部のいずれかのリージョンに対してのみレプリケートとフェールオーバー、およびフェールバックが可能です。


## <a name="support-for-compute-configuration"></a>コンピューティング構成のサポート

**構成** | **サポートされるかどうか** | **解説**
--- | --- | ---
サイズ | 少なくとも 2 つの CPU コアと 1 GB の RAM を備えた任意の Azure VM サイズ | [Azure 仮想マシンのサイズ](../virtual-machines/windows/sizes.md)に関するページをご覧ください
可用性セット | サポートされています | ポータルで既定のオプションを使用して "レプリケーションの有効化" 手順を実行する場合、可用性セットは、ソース リージョンの構成に基づいて自動的に作成されます。 ターゲットの可用性セットは、[レプリケートされたアイテム] > [設定] > [コンピューティングとネットワーク] > [可用性セット] でいつでも変更できます。
Hybrid Use Benefit (HUB) VM | サポートされています | ソース VM で HUB ライセンスが有効になっている場合、テスト フェールオーバーまたはフェールオーバー VM でも HUB ライセンスが使用されます。
仮想マシン スケール セット | サポートされていません |
Azure ギャラリー イメージ - Microsoft が公開 | サポートされています | Site Recovery によってサポートされるオペレーティング システムで VM が実行されている場合に、サポートされます
Azure ギャラリー イメージ - サード パーティが公開 | サポートされています | Site Recovery によってサポートされるオペレーティング システムで VM が実行されている場合に、サポートされます。
カスタム イメージ - サード パーティが公開 | サポートされています | Site Recovery によってサポートされるオペレーティング システムで VM が実行されている場合に、サポートされます。
Site Recovery を使用して移行された VM | サポートされています | Site Recovery を使用して Azure に移行された VMware/物理マシンの場合は、古いバージョンのモビリティ サービスをアンインストールし、マシンを再起動してから、他の Azure リージョンにレプリケートする必要があります。

## <a name="support-for-storage-configuration"></a>ストレージ構成のサポート

**構成** | **サポートされるかどうか** | **解説**
--- | --- | ---
OS ディスクの最大サイズ | 2048 GB | ｢[VM で使用されるディスク](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)」を参照してください。
データ ディスクの最大サイズ | 4095 GB | ｢[VM で使用されるディスク](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)」を参照してください。
データ ディスクの数 | 特定の Azure VM サイズでサポートされている最大数 64 | [Azure 仮想マシンのサイズ](../virtual-machines/windows/sizes.md)に関するページをご覧ください
一時ディスク | 常にレプリケーションから除外 | 一時ディスクは常にレプリケーションから除外されます。 Azure ガイダンスに従って、一時ディスクには永続データを配置しないでください。 詳細については、[Azure VM の一時ディスク](../virtual-machines/windows/about-disks-and-vhds.md#temporary-disk)に関する記事をご覧ください。
ディスク上のデータの変更率 | 最大値は、Premium ストレージの場合はディスクあたり 10 MBps、Standard ストレージの場合はディスクあたり 2 MBps です | ディスク上の平均データ変更率が継続的に 10 MBps (Premium の場合) と 2 MBps (Standard の場合) を超えると、レプリケーションは追いつかなくなります。 ただし、データの急激な増加が時折しか発生せず、データ変更率が一時的に 10 MBps (Premium の場合) と 2 MBps (Standard の場合) を超えてから低下する場合、レプリケーションは追いつきます。 この場合、復旧ポイントは、少し後ろにずれることがあります。
Standard Storage アカウントのディスク | サポートされています |
Premium Storage アカウントのディスク | サポートされています | VM のディスクが Premium Storage アカウントと Standard Storage ストレージ アカウントに分散している場合は、ディスクごとに異なるターゲット ストレージ アカウントを選択して、ターゲット リージョンのストレージ構成を確実に同じできます。
Standard 管理ディスク | Azure Site Recovery がサポートされている Azure リージョンでサポートされます。 政府機関向けクラウドは現在はサポートされていません。  |  
Premium 管理ディスク | Azure Site Recovery がサポートされている Azure リージョンでサポートされます。 政府機関向けクラウドは現在はサポートされていません。 |
記憶域スペース | サポートされています |         
保存時の暗号化 (SSE) | サポートされています | キャッシュおよびターゲット ストレージ アカウントごとに、SSE 対応ストレージ アカウントを選択できます。     
Azure Disk Encryption (ADE) | サポートされていません |
ディスクのホット アド/削除 | サポートされていません | VM 上でデータ ディスクを追加または削除する場合は、レプリケーションを無効にしてから、もう一度 VM に対してレプリケーションを有効にする必要があります。
ディスクの除外 | サポートされていません|   一時ディスクは既定で除外されます。
記憶域スペース ダイレクト  | サポートされていません|
スケールアウト ファイル サーバー  | サポートされていません|
LRS | サポートされています |
GRS | サポートされています |
RA-GRS | サポートされています |
ZRS | サポートされていません |  
クールおよびホット ストレージ | サポートされていません | 仮想マシン ディスクは、クールおよびホット ストレージではサポートされません
仮想ネットワークの Azure Storage ファイアウォール  | いいえ  | レプリケートされたデータの格納に使用するキャッシュ ストレージ アカウントで、特定の Azure 仮想ネットワークへのアクセスを許可することはサポートされていません。
汎用目的 V2 ストレージ アカウント (ホット層とクール層の両方) | いいえ  | 汎用目的 V1 のストレージ アカウントに比べて、トランザクション コストが非常に大きくなります

>[!IMPORTANT]
> パフォーマンスの問題を回避するために、[Linux](../virtual-machines/linux/disk-scalability-targets.md) または [Windows](../virtual-machines/windows/disk-scalability-targets.md) 仮想マシンの VM ディスクのスケーラビリティおよびパフォーマンスのターゲットを確認してください。 既定の設定に従うと、Site Recovery により、ソース構成に基づいて必要なディスクとストレージ アカウントが作成されます。 設定をカスタマイズして独自の設定を選択する場合は、ソース VM のディスクのスケーラビリティおよびパフォーマンスのターゲットに従ってください。

## <a name="support-for-network-configuration"></a>ネットワーク構成のサポート
**構成** | **サポートされるかどうか** | **解説**
--- | --- | ---
ネットワーク インターフェイス (NIC) | 特定の Azure VM サイズでサポートされている NIC の最大数 | テスト フェールオーバーまたはフェールオーバー操作の一環として VM が作成されるときに、NIC が作成されます。 フェールオーバー VM 上の NIC 数は、レプリケーションを有効にしたときの、ソース VM の NIC 数によって決まります。 レプリケーションを有効にした後に NIC を追加/削除しても、フェールオーバー VM の NIC 数には影響しません。
インターネット Load Balancer | サポートされています | 復旧計画の Azure 自動化スクリプトを使用して、構成済みロード バランサーを関連付ける必要があります。
内部ロード バランサー | サポートされています | 復旧計画の Azure 自動化スクリプトを使用して、構成済みロード バランサーを関連付ける必要があります。
パブリック IP| サポートされています | 復旧計画の Azure 自動化スクリプトを使用して、既存のパブリック IP を NIC に関連付けるか、パブリック IP を作成して NIC に関連付ける必要があります。
NIC の NSG (Resource Manager)| サポートされています | 復旧計画の Azure 自動化スクリプトを使用して、NSG を NIC に関連付ける必要があります。  
サブネットの NSG (Resource Manager とクラシック)| サポートされています | 復旧計画の Azure 自動化スクリプトを使用して、NSG をサブネットに関連付ける必要があります。
VM の NSG (クラシック)| サポートされています | 復旧計画の Azure 自動化スクリプトを使用して、NSG を NIC に関連付ける必要があります。
予約済み IP (静的 IP)/発信元 IP を保持 | サポートされています | ソース VM の NIC の IP 構成が静的で、ターゲット サブネットで同じ IP を使用できる場合、その IP は、フェールオーバー VM に割り当てられます。 ターゲット サブネットで同じ IP を使用できない場合は、そのサブネット内の使用可能な IP の 1 つがこの VM 用に予約されます。 任意の固定 IP は、[レプリケートされたアイテム] > [設定] > [コンピューティングとネットワーク] > [ネットワーク インターフェイス] で指定できます。 NIC を選択し、任意のサブネットと IP を指定できます。
動的 IP| サポートされています | ソース VM の NIC の IP 構成が動的である場合は、フェールオーバー VM の NIC も既定で動的になります。 任意の固定 IP は、[レプリケートされたアイテム] > [設定] > [コンピューティングとネットワーク] > [ネットワーク インターフェイス] で指定できます。 NIC を選択し、任意のサブネットと IP を指定できます。
Traffic Manager 統合 | サポートされています | Traffic Manager は、トラフィックがソース リージョンのエンドポイントに定期的にルーティングされるように、また、ターゲット リージョンのエンドポイントにフェールオーバー時にルーティングされるように、事前に構成できます。
Azure 管理 DNS | サポートされています |
[カスタム DNS]  | サポートされています |    
非認証プロキシ | サポートされています | [ネットワーク ガイダンスのドキュメント](site-recovery-azure-to-azure-networking-guidance.md)を参照してください。    
認証済みプロキシ | サポートされていません | VM が送信接続に認証済みプロキシを使用している場合は、Azure Site Recovery でレプリケートできません。    
オンプレミスでのサイト間 VPN (ExpressRoute あり/なし)| サポートされています | Site Recovery トラフィックがオンプレミスにルーティングされないように、UDR と NSG が構成されていることを確認します。 [ネットワーク ガイダンスのドキュメント](site-recovery-azure-to-azure-networking-guidance.md)を参照してください。  
VNet 間接続 | サポートされています | [ネットワーク ガイダンスのドキュメント](site-recovery-azure-to-azure-networking-guidance.md)を参照してください。  
仮想ネットワーク サービス エンドポイント | サポートされています | 仮想ネットワークの Azure Storage ファイアウォールはサポートされていません。 レプリケートされたデータの格納に使用するキャッシュ ストレージ アカウントで、特定の Azure 仮想ネットワークへのアクセスを許可することはサポートされていません。
高速ネットワーク | サポートされていません | Accelerated Networking が有効になっている VM をレプリケートすることはできますが、フェールオーバー VM では Accelerated Networking が有効になりません。 Accelerated Networking はフェールバックのソース VM でも無効になります。


## <a name="next-steps"></a>次の手順
- [Azure VM のレプリケートに関するネットワーク ガイダンス](site-recovery-azure-to-azure-networking-guidance.md)の詳細を確認する
- [Azure VM をレプリケート](site-recovery-azure-to-azure.md)してワークロードの保護を開始する
