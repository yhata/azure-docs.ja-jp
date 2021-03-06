---
title: PowerShell で Azure Analysis Services を管理する | Microsoft Docs
description: PowerShell を使用した Azure Analysis Services 管理。
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: reference
ms.date: 05/22/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: b4e819bdce971e92e4b2d99e68f51ddbf8a22182
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "34597469"
---
# <a name="manage-azure-analysis-services-with-powershell"></a>PowerShell で Azure Analysis Services を管理する

この記事では、Azure Analysis Services サーバーおよびデータベース管理タスクを実行するときに使用する PowerShell コマンドレットについて説明します。 

サーバー管理のタスクには、 Azure Resource Manager (リソース) コマンドレット および Analysis Services (サーバー) コマンドレットを使用する、サーバーの作成または削除、操作の中断または再開、サービスレベル（層）の変更などがあります。 ロール メンバーの追加や削除、処理、パーティション分割など、その他のデータベース管理タスクでは、SQL Server Analysis Services と同じ SqlServer モジュールに含まれるコマンドレットが使われます。

## <a name="permissions"></a>アクセス許可
ほとんどの PowerShell タスクでは、管理している Analysis Services サーバーに対する管理者権限が必要となります。 スケジュールされた PowerShell タスクは無人操作です。 スケジューラを実行するアカウントにも、Analysis Services サーバーに対する管理者権限が必要です。 

AzureRm コマンドレットを使用したサーバー操作の場合、自分のアカウントまたはスケジューラを実行するアカウントが、[Azure のロールベースのアクセス制御 (RBAC)](../role-based-access-control/overview.md) でリソースの所有者ロールに属していることも必要になります。 

## <a name="resource-management-operations"></a>管理リソース管理操作 
モジュール-[AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)

|コマンドレット|説明| 
|------------|-----------------| 
|[Get-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|サーバー インスタンスの詳細を取得します。|  
|[New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|サーバー インスタンスを作成します。|   
|[新しい AzureRmAnalysisServicesFirewallConfig](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesfirewallconfig)|新しい Analysis Services ファイアウォール構成を作成します。|   
|[新しい AzureRmAnalysisServices ファイアウォールルール](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesfirewallrule)|新しい Analysis Services ファイアウォールルールを作成します。|   
|[Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|サーバー インスタンスを削除します。|  
|[Resume-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|サーバー インスタンスを再開します。|  
|[Suspend-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|サーバー インスタンスを中断します。| 
|[Set-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|サーバー インスタンスを変更します。|   
|[Test-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|サーバー インスタンスの存在をテストします。| 

## <a name="server-management-operations"></a>サーバー管理操作

モジュール-[Azure.AnalysisServices](https://www.powershellgallery.com/packages/Azure.AnalysisServices)

|コマンドレット|説明| 
|------------|-----------------| 
|[Add-AzureAnalysisServicesAccount](/powershell/module/azure.analysisservices/add-azureanalysisservicesaccount)|認証済みアカウントを追加して、Azure Analysis Services サーバー コマンドレットの要求に使用します。| 
|[Export-AzureAnalysisServicesInstance]()|Add-AzureAnalysisServicesAccount コマンドに指定された、　現在ログインしている環境にある Analysis Services サーバーのインスタンスからログをエキスポートします|  
|[Restart-AzureAnalysisServicesInstance](/powershell/module/azurerm.analysisservices/restart-azureanalysisservicesinstance)|Add-AzureAnalysisServicesAccount コマンドに指定された、現在ログインしている環境にある Analysis Services サーバーのインスタンスを再起動します。|  
|[Sync-AzureAnalysisServicesInstance](/powershell/module/azurerm.analysisservices/restart-azureanalysisservicesinstance)|AzureAnalysisServicesAccount コマンドで指定されている、現在ログインしている環境での、すべてのクエリのスケール アウト インスタンスへに、 Analysis Services サーバーの指定したインスタンス上に指定されたデータベースを同期します|  

## <a name="database-operations"></a>データベース操作

Azure Analysis Services のデータベース操作では、SQL Server Analysis Services と同じ [SqlServer](https://www.powershellgallery.com/packages/SqlServer) モジュールが使われます。 ただし、すべてのコマンドレットが、Azure Analysis Services でサポートされているわけではありません。 

SqlServer モジュールには、タスク固有のデータベース管理コマンドレットと、Tabular Model Scripting Language (TMSL) クエリまたはスクリプトを受け入れる汎用 Invoke-ASCmd コマンドレットが用意されています。 以下の SqlServer モジュールのコマンドレットは、Azure Analysis Services でサポートされます。

  
|コマンドレット|説明|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|データベース ロールにメンバーを追加します。| 
|[Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|Analysis Services データベースをバックアップします。|  
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|データベース ロールからメンバーを削除します。|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|TMSL スクリプトを実行します。|
|[Invoke-ProcessASDatabase](https://msdn.microsoft.com/library/mt651773.aspx)|データベースを処理します。|  
|[Invoke-ProcessPartition](https://msdn.microsoft.com/library/hh510164.aspx)|パーティションを処理します。| 
|[Invoke-ProcessTable](https://msdn.microsoft.com/library/mt651774.aspx)|テーブルを処理します。|  
|[Merge-Partition](https://msdn.microsoft.com/library/hh479576.aspx)|パーティションをマージします。|  
|[Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|Analysis Services データベースを復元します。| 
  

## <a name="related-information"></a>関連情報

* [SQL Server PowerShell モジュールのダウンロード](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [SQL Server Management Studio (SSMS) のダウンロード](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [PowerShell ギャラリーの Sql Server モジュール](https://www.powershellgallery.com/packages/SqlServer)    
* [互換性レベル 1200 以上の表形式モデル プログラミング](https://msdn.microsoft.com/library/mt712541.aspx)
