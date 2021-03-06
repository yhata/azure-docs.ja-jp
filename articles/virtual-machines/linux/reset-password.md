---
title: Azure VM 上でローカルの Linux パスワードをリセットする方法 | Microsoft Docs
description: Azure VM 上でローカルの Linux パスワードをリセットする手順を紹介します
services: virtual-machines-linux
documentationcenter: ''
author: Deland-Han
manager: cshepard
editor: ''
tags: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/03/2017
ms.author: delhan
ms.openlocfilehash: b9182ec2a974de06c2bd45928b9964f253653bf6
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2018
ms.locfileid: "27578364"
---
# <a name="how-to-reset-local-linux-password-on-azure-vms"></a>Azure VM 上でローカルの Linux パスワードをリセットする方法

この記事では、ローカルの Linux 仮想マシン (VM) のパスワードをリセットする方法をいくつか紹介します。 ユーザー アカウントが期限切れになっている場合や、単に新しいアカウントを作成したい場合は、以下の方法で新しいローカル管理者アカウントを作成し、VM へのアクセスを再取得することができます。

## <a name="symptoms"></a>現象

VM にログインすることができず、使用したパスワードが正しくないことを示すメッセージが表示される。 さらに、Azure Portal で VMAgent を使ってパスワードをリセットすることができない。 

## <a name="manual-password-reset-procedure"></a>パスワードの手動リセットの手順

1.  VM を削除し、アタッチされているディスクを維持します。

2.  OS ドライブをデータ ディスクとして、同じ場所の別のテンポラル VM にアタッチします。

3.  テンポラル VM 上で次の SSH コマンドを実行して、スーパーユーザーになります。


    ~~~~
    sudo su
    ~~~~

4.  **fdisk -l** を実行するか、システム ログを見て、新たにアタッチされたディスクを探します。 マウントするドライブ名を特定します。 次に、テンポラル VM 上で、関連するログ ファイルを参照します。

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    以下に、grep コマンドの出力例を示します。

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  **tempmount** と呼ばれるマウント ポイントを作成します。

    ~~~~
    mkdir /tempmount
    ~~~~

6.  マウント ポイントに OS ディスクをマウントします。 通常は、sdc1 または sdc2 をマウントする必要があります。 これは、切断したマシン ディスクの /etc ディレクトリのホスティング パーティションによって決まります。

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  変更を加える前に、バックアップを実行します。

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  該当するユーザーのパスワードをリセットします。

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  変更したファイルを、切断したマシンのディスク上の正しい場所に移動します。

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    ~~~~

10. ルートに戻り、ディスクをマウント解除します。

    ~~~~
    cd /
    umount /tempmount
    ~~~~

11. 管理ポータルからディスクをデタッチします。

12. VM を再作成します。

## <a name="next-steps"></a>次の手順

* [OS ディスクを別の Azure VM にアタッチして Azure VM のトラブルシューティングを行う](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: VHD から VM を削除して再デプロイする方法](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
