---
title: 'チュートリアル: Azure Active Directory と Pantheon の統合 | Microsoft Docs'
description: Azure Active Directory と Pantheon の間でシングル サインオンを構成する方法について説明します。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 67758e527549827b673d00ad82911d3114a44ca7
ms.sourcegitcommit: 16ddc345abd6e10a7a3714f12780958f60d339b6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2018
ms.locfileid: "36227841"
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a>チュートリアル: Azure Active Directory と Pantheon の統合

このチュートリアルでは、Pantheon と Azure Active Directory (Azure AD) を統合する方法について説明します。

Pantheon と Azure AD の統合には、次の利点があります。

- Pantheon にアクセスする Azure AD ユーザーを制御できます。
- ユーザーが自分の Azure AD アカウントで自動的に Pantheon にサインオン (シングル サインオン) できるようにします。
- 1 つの中央サイト (Azure Portal) でアカウントを管理できます

SaaS アプリと Azure AD の統合の詳細については、「[Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](../manage-apps/what-is-single-sign-on.md)」をご覧ください。

## <a name="prerequisites"></a>前提条件

Pantheon と Azure AD の統合を構成するには、次のものが必要です。

- Azure AD サブスクリプション
- Pantheon でのシングル サインオンが有効なサブスクリプション

> [!NOTE]
> このチュートリアルの手順をテストする場合、運用環境を使用しないことをお勧めします。

このチュートリアルの手順をテストするには、次の推奨事項に従ってください。

- 必要な場合を除き、運用環境は使用しないでください。
- Azure AD の評価環境がない場合は、 [こちら](https://azure.microsoft.com/pricing/free-trial/)から 1 か月の評価版を入手できます。

## <a name="scenario-description"></a>シナリオの説明
このチュートリアルでは、テスト環境で Azure AD のシングル サインオンをテストします。 このチュートリアルで説明するシナリオは、主に次の 2 つの要素で構成されています。

1. ギャラリーからの Pantheon の追加
2. Azure AD シングル サインオンの構成とテスト

## <a name="adding-pantheon-from-the-gallery"></a>ギャラリーからの Pantheon の追加
Azure AD への Pantheon の統合を構成するには、ギャラリーから管理対象 SaaS アプリの一覧に Pantheon を追加する必要があります。

**ギャラリーから Pantheon を追加するには、次の手順に従います。**

1. **[Azure Portal](https://portal.azure.com)** の左側のナビゲーション ウィンドウで、**[Azure Active Directory]** アイコンをクリックします。 

    ![Active Directory][1]

2. **[エンタープライズ アプリケーション]** に移動します。 次に、**[すべてのアプリケーション]** に移動します。

    ![[アプリケーション]][2]
    
3. 新しいアプリケーションを追加するには、ダイアログの上部にある **[新しいアプリケーション]** をクリックします。

    ![[アプリケーション]][3]

4. 検索ボックスに、「**Pantheon**」と入力します。

    ![Azure AD のテスト ユーザーの作成](./media/pantheon-tutorial/tutorial_pantheon_search.png)

5. 結果パネルで **[Pantheon]** を選択し、**[追加]** ボタンをクリックして、アプリケーションを追加します。

    ![Azure AD のテスト ユーザーの作成](./media/pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成とテスト
このセクションでは、"Britta Simon" というテスト ユーザーに基づいて、Pantheon で Azure AD のシングル サインオンを構成し、テストします。

シングル サインオンを機能させるには、Azure AD ユーザーに対応する Pantheon ユーザーが Azure AD で認識されている必要があります。 言い換えると、Azure AD ユーザーと Pantheon の関連ユーザーの間で、リンク関係が確立されている必要があります。

Pantheon で、Azure AD の **[ユーザー名]** の値を **[Username]** の値として割り当ててリンク関係を確立します。

Pantheon で Azure AD のシングル サインオンを構成してテストするには、次の構成要素を完了する必要があります。

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - ユーザーがこの機能を使用できるようにします。
2. **[Azure AD のテスト ユーザーの作成](#creating-an-azure-ad-test-user)** - Britta Simon で Azure AD のシングル サインオンをテストします。
3. **[Pantheon のテスト ユーザーの作成](#creating-a-pantheon-test-user)** - Pantheon で Britta Simon に対応するユーザーを作成し、Azure AD の Britta Simon にリンクさせます。
4. **[Azure AD テスト ユーザーの割り当て](#assigning-the-azure-ad-test-user)** - Britta Simon が Azure AD のシングル サインオンを使用できるようにします。
5. **[シングル サインオンのテスト](#testing-single-sign-on)** - 構成が機能するかどうかを確認します。

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成

このセクションでは、Azure Portal で Azure AD のシングル サインオンを有効にして、Pantheon アプリケーションでシングル サインオンを構成します。

**Pantheon で Azure AD シングル サインオンを構成するには、次の手順に従います。**

1. Azure Portal の **Pantheon** アプリケーション統合ページで、**[シングル サインオン]** をクリックします。

    ![[Configure Single Sign-On]][4]

2. **[シングル サインオン]** ダイアログで、**[モード]** として **[SAML ベースのサインオン]** を選択し、シングル サインオンを有効にします。
 
    ![[Configure Single Sign-On]](./media/pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. **[Pantheon のドメインと URL]** セクションで、次の手順を実行します。

    ![[Configure Single Sign-On]](./media/pantheon-tutorial/tutorial_pantheon_url.png)

    a.[サインオン URL] ボックスに、次のパターンを使用して、ユーザーが RightScale アプリケーションへのサインオンに使用する URL を入力します。 **[識別子]** ボックスに、`urn:auth0:pantheon:<orgname>-SSO` の形式で URL を入力します。

    b. **[応答 URL]** ボックスに、`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO` のパターンを使用して URL を入力します。

    > [!NOTE] 
    > これらは実際の値ではありません。 実際の識別子と応答 URL でこれらの値を更新します。 これらの値を取得するには、[Pantheon サポート チーム](https://pantheon.io/docs/getting-support/)に連絡してください。

4. Pantheon アプリケーションでは特定の形式の SAML アサーションが要求されるため、ユーザーの電子メール アドレスで UserIdentifier 属性値を設定する必要があります。 既定では、Azure AD は UserIdentifier 属性に UserPrincipalName を使用します。 ただし、正常に統合するには、この値がユーザーの電子メール アドレスと一致するように調整する必要があります。 統合は、適切なマッピングが行われた後にのみ機能します。

    ![[Configure Single Sign-On]](./media/pantheon-tutorial/tutorial_attribute.png)    


5. **[SAML 署名証明書]** セクションで、**[証明書 (Base64)]** をクリックし、コンピューターに証明書ファイルを保存します。

    ![[Configure Single Sign-On]](./media/pantheon-tutorial/tutorial_pantheon_certificate.png)

6. **[保存]** ボタンをクリックします。

    ![[Configure Single Sign-On]](./media/pantheon-tutorial/tutorial_general_400.png)

7. **[Pantheon 構成]** セクションで、**[Pantheon の構成]** をクリックして、**[サインオンの構成]** ウィンドウを開きます。 **[クイック リファレンス]** セクションから **SAML シングル サインオン サービスの URL** をコピーします。

    ![[Configure Single Sign-On]](./media/pantheon-tutorial/tutorial_pantheon_configure.png) 

8. **Pantheon** 側にシングルサインオンを構成するには、ダウンロードされた**証明書**および **SAML シングル サインオン サービス URL** を [Pantheon サポート チーム](https://pantheon.io/docs/getting-support/)に送信する必要があります。

     > [!Note]
     > この接続を有効にするには、電子メール ドメイン情報と日時も提供する必要があります。 詳細については、[こちら](https://pantheon.io/docs/sso-organizations/)を参照してください。

> [!TIP]
> アプリのセットアップ中、[Azure Portal](https://portal.azure.com) 内で上記の手順の簡易版を確認できるようになりました。  **[Active Directory] の [エンタープライズ アプリケーション]** セクションからこのアプリを追加した後、**[シングル サインオン]** タブをクリックし、一番下の **[構成]** セクションから組み込みドキュメントにアクセスするだけです。 組み込みドキュメント機能の詳細については、[Azure AD の組み込みドキュメント]( https://go.microsoft.com/fwlink/?linkid=845985)に関するページを参照してください。

### <a name="creating-an-azure-ad-test-user"></a>Azure AD のテスト ユーザーの作成
このセクションの目的は、Azure Portal で Britta Simon というテスト ユーザーを作成することです。

![Azure AD ユーザーの作成][100]

**Azure AD でテスト ユーザーを作成するには、次の手順に従います。**

1. **Azure Portal** の左側のナビゲーション ウィンドウで、**[Azure Active Directory]** アイコンをクリックします。

    ![Azure AD のテスト ユーザーの作成](./media/pantheon-tutorial/create_aaduser_01.png) 

2. **[ユーザーとグループ]** に移動し、**[すべてのユーザー]** をクリックして、ユーザーの一覧を表示します。
    
    ![Azure AD のテスト ユーザーの作成](./media/pantheon-tutorial/create_aaduser_02.png) 

3. ダイアログの上部にある **[追加]** をクリックして、**[ユーザー]** ダイアログを開きます。
 
    ![Azure AD のテスト ユーザーの作成](./media/pantheon-tutorial/create_aaduser_03.png) 

4. **[ユーザー]** ダイアログ ページで、次の手順を実行します。
 
    ![Azure AD のテスト ユーザーの作成](./media/pantheon-tutorial/create_aaduser_04.png) 

    a.[サインオン URL] ボックスに、次のパターンを使用して、ユーザーが RightScale アプリケーションへのサインオンに使用する URL を入力します。 **[名前]** ボックスに「**BrittaSimon**」と入力します。

    b. **[ユーザー名]** ボックスに BrittaSimon の**電子メール アドレス**を入力します。

    c. **[パスワードを表示]** を選択し、**[パスワード]** の値をメモします。

    d. **Create** をクリックしてください。
 
### <a name="creating-a-pantheon-test-user"></a>Pantheon のテスト ユーザーの作成

このセクションでは、Pantheon で Britta Simon というユーザーを作成します。 Pantheon でユーザーを追加するには、次の手順に従ってください。 

>[!NOTE] 
>SSO が機能するには、まず Pantheon でユーザーを作成する必要があります。

1. 管理者の資格情報で Pantheon にログインします。

2. **[組織]** ダッシュボード ページに移動します。
 
3. **[ユーザー]** をクリックします。

4. **[ユーザーの追加]** をクリックします。

5. ユーザーの電子メール アドレスを入力します。

6. ユーザーの役割を選択します。

7. **[ユーザーの追加]** をクリックします。

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD テスト ユーザーの割り当て

このセクションでは、Britta Simon に Pantheon へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

![ユーザーの割り当て][200] 

**Britta Simon を Pantheon に割り当てるには、次の手順に従います。**

1. Azure Portal でアプリケーション ビューを開き、ディレクトリ ビューに移動します。次に、**[エンタープライズ アプリケーション]** に移動し、**[すべてのアプリケーション]** をクリックします。

    ![ユーザーの割り当て][201] 

2. アプリケーションの一覧で **[Pantheon]** を選択します。

    ![[Configure Single Sign-On]](./media/pantheon-tutorial/tutorial_pantheon_app.png) 

3. 左側のメニューで **[ユーザーとグループ]** をクリックします。

    ![ユーザーの割り当て][202] 

4. **[追加]** ボタンをクリックします。 次に、**[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。

    ![ユーザーの割り当て][203]

5. **[ユーザーとグループ]** ダイアログで、ユーザーの一覧から **[Britta Simon]** を選択します。

6. **[ユーザーとグループ]** ダイアログで **[選択]** をクリックします。

7. **[割り当ての追加]** ダイアログで **[割り当て]** ボタンをクリックします。
    
### <a name="testing-single-sign-on"></a>シングル サインオンのテスト

このセクションでは、アクセス パネルを使用して Azure AD のシングル サインオン構成をテストします。

アクセス パネルで [Pantheon] タイルをクリックすると、Pantheon アプリケーションに自動的にサインオンします。
アクセス パネルの詳細については、[アクセス パネルの概要](../active-directory-saas-access-panel-introduction.md)に関する記事を参照してください。 

## <a name="additional-resources"></a>その他のリソース

* [SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧](tutorial-list.md)
* [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/pantheon-tutorial/tutorial_general_01.png
[2]: ./media/pantheon-tutorial/tutorial_general_02.png
[3]: ./media/pantheon-tutorial/tutorial_general_03.png
[4]: ./media/pantheon-tutorial/tutorial_general_04.png

[100]: ./media/pantheon-tutorial/tutorial_general_100.png

[200]: ./media/pantheon-tutorial/tutorial_general_200.png
[201]: ./media/pantheon-tutorial/tutorial_general_201.png
[202]: ./media/pantheon-tutorial/tutorial_general_202.png
[203]: ./media/pantheon-tutorial/tutorial_general_203.png

