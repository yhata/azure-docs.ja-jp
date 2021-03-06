---
title: Azure AD での組織のプライバシー情報の追加 | Microsoft Docs
description: Azure Active Directory (Azure AD) Properties エリアに組織のプライバシー情報を追加する方法を説明します。
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: lizross
ms.reviewer: bpham
ms.custom: it-pro
ms.openlocfilehash: 8cdf30ed09601a31529073eaedd4ab53780157d5
ms.sourcegitcommit: fc64acba9d9b9784e3662327414e5fe7bd3e972e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2018
ms.locfileid: "34077717"
---
# <a name="how-to-add-your-organizations-privacy-info-in-azure-active-directory"></a>How-to: Azure Active Directory での組織のプライバシー情報の追加
この記事では、テナント管理者が Azure ポータルから組織の Azure Active Directory (Azure AD) テナントにプライバシー関連の情報を追加する方法を説明します｡

社内従業員と社外ゲストが組織のポリシーを確認できるよう､プライバシーに関するグローバルな問い合わせ先と組織のプライバシーに関する声明の両方を追加することを強くお勧めします｡ プライバシーに関する声明はそれぞれの会社に合わせて独自に作成､変更されるため､弁護士に相談することを強くお勧めします｡

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-dsr-and-stp-note.md)]

## <a name="access-the-properties-area-to-add-your-privacy-info"></a>プライバシー情報を追加するには､[Properties] エリアにアクセスします｡

1.  グローバル管理者として Azure Portal に サインインします。

2.  左側のナビゲーション バーで **Azure Active Directory** を選択して､**Properties** を選択します｡

    **Properties** エリアが表示されます｡

    ![Azure AD Properties エリア - プライバシー情報を強調表示した状態](./media/active-directory-properties-area/properties-area.png)

3.  従業員のプライバシー情報を追加します｡

    - **技術部連絡先｡** 社内の技術的なサポートを受けるさいの連絡先の電子メール アドレスを入力します｡
    
    - **グローバル プライバシー連絡先｡** 個人データのプライバシーに関する問い合わせをするさいの連絡先の電子メール アドレスを入力します｡ この連絡先は､データに関する違反があった場合に Microsoft が問い合わせを行う連絡先でもあります｡ 問い合わせの記載がない場合､Microsoft はグローバル管理者に問い合わせます｡

    - **プライバシーに関する声明 URL｡** 社内および社外ゲストのデータに関するプライバシーの取り扱いを説明した組織のドキュメントへのリンクを入力します｡

        >[!Important]
        >プライバシーに関する独自の声明もプライバシーに関する連絡先のどちらもない場合､**Review Permissions** ボックスには､社外ゲスト向けに､ **<_your org name_> has not provided links to their terms for you to review** (組織名> からはご利用条件を確認するためのリンクが提供されていません) という文言が表示されます｡ たとえば､このメッセージは､B2B コラボレーションでゲスト ユーザーが組織にアクセスするための招待を受けたときに表示されます｡

        ![B2B Collaboration Review Permissions ボックスとメッセージ](./media/active-directory-properties-area/active-directory-no-privacy-statement-or-contact.png)

4.  **[保存]** を選択します。

## <a name="next-steps"></a>次の手順
- [Azure Active Directory B2B コラボレーションの招待の利用](https://aka.ms/b2bredemption)
- [Azure Active Directory でユーザーのプロファイル情報を追加または変更する](/active-directory-users-profile-azure-portal.md)