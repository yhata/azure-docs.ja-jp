---
title: 'トラブルシューティング: ダウンロードした Azure Active Directory アクティビティ ログにデータが見つからない | Microsoft Docs'
description: ダウンロードした Azure Active Directory アクティビティ ログにデータが見つからない問題の解決策を提供します。
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: compliance-reports
ms.date: 01/15/2018
ms.author: rolyon
ms.reviewer: dhanyahk
ms.openlocfilehash: 6878ff8175514b97fbeab70b932349ce400394dd
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "34589867"
---
# <a name="i-cant-find-any-data-in-the-azure-active-directory-activity-logs-i-have-downloaded"></a>ダウンロードした Azure Active Directory アクティビティ ログにデータが見つかりません


## <a name="symptoms"></a>現象

アクティビティ ログ (監査またはサインイン) をダウンロードしましたが、選択した期間のレコードがまったく表示されません。 なぜですか? 

 ![レポート](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>原因

Azure Portal でアクティビティ ログをダウンロードする場合は、新しい順に並べ替えられた最新の 12 万件のレコードに制限されます。 

## <a name="resolution"></a>解決策

[Azure AD Reporting API](active-directory-reporting-api-getting-started.md) を利用すると、任意の時点のレコードを最大 100 万件取得できます。 Reporting API を呼び出して、増分方式で一定期間 (たとえば、毎日や毎週) のレコードを取得するスクリプトを定期的に実行することをお勧めします。

## <a name="next-steps"></a>次の手順
「[Azure Active Directory レポートに関する FAQ](active-directory-reporting-faq.md)」を参照してください。

