---
ms.date: 03/27/2018
contributor: JKeithB
keywords: ギャラリー, PowerShell, PSGallery, GDPR
title: PowerShell ギャラリー GDPR コンプライアンス
ms.openlocfilehash: 14b82fa07df52f02f0d7577cb0eef70faa4285a2
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893248"
---
# <a name="powershell-gallery-gdpr-compliance"></a>PowerShell ギャラリー GDPR コンプライアンス

## <a name="overview"></a>概要

2018 年 5 月より、ヨーロッパの個人情報保護法、一般データ保護規制 (GDPR) が有効になります。
GDPR によって、企業、政府機関、非営利団体、および欧州連合 (EU) の人に商品やサービスを提供したり、ヨーロッパの居住者に関連するデータを収集分析したりするその他の組織に、新しい規則が課されます。
GDPR は現住所に関わらず適用されます。

> [!NOTE]
> この記事は、PowerShell ギャラリーから個人データを削除する手順を提供するため、GDPR の下での義務の遂行に役立ちます。 GDPR に関する一般的な情報をお探しの場合は、[Service Trust portal の GDPR に関するセクション](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted)を参照してください。

## <a name="personally-identifiable-data"></a>個人を特定できるデータ

PowerShell ギャラリーには、ユーザーから提供され、個人情報が含まれる可能性がある、次の情報が格納されます。

- PowerShell ギャラリーのアカウント
- PowerShell ギャラリーで公開されるアイテム
- PowerShell ギャラリー チームとの電子メールのやり取り

ほとんどのユーザーは、PowerShell ギャラリーのアカウントを作成しません。
アイテムを公開する予定がない場合や、PowerShell ギャラリーで "所有者に連絡" の機能を使用しない場合は、アカウントは必要ありません。
ユーザーから開始された電子メールのやり取りを除き、PowerShell ギャラリーにはアカウントを作成していないユーザーの個人を特定できるデータは格納されません。

PowerShell ギャラリーのアカウントを作成したユーザーは、PowerShell ギャラリーにアイテムを公開することができます。
このアイテムは、PowerShell コードになると予想されますが、個人情報を含むその他の情報が含まれることがあります。
次の情報は、PowerShell ギャラリーに公開されたすべてのアイテムを取得する方法を示します。

## <a name="dsr-export-of-powershell-gallery-data"></a>PowerShell ギャラリー データの DSR エクスポート

次のセクションは、PowerShell ギャラリーがデータ サブジェクト要求 (DSR) をどのようにサポートするかを、PowerShell ギャラリーに格納された情報をエクスポートする方法や、この情報の削除を依頼する方法について説明しています。

### <a name="email"></a>電子メール

電子メールのやり取りには、次のいずれかが含まれます。

- コード分析のスキャンで PowerShell ギャラリーに公開されたアイテムに問題が検出された場合に、PowerShell ギャラリーのアイテムの所有者に送信された電子メール
- いずれかのユーザーによって、"お問い合わせ先" ページの電子メール アドレス ([cgadmin@microsoft.com](mailto:cgadmin@microsoft.com)) を使用して PowerShell ギャラリー チームに送信された電子メール
- PowerShell ギャラリーの "所有者に連絡" 機能を使用して PowerShell ギャラリーのアイテムの所有者に電子メールを送信する登録済みユーザー

悪意のあるコードが PowerShell ギャラリーで検出された場合に想定されるセキュリティ調査をサポートするため、PowerShell ギャラリーとの間で送受信された電子メールには、90 日間のアイテム保持ポリシーが適用されます。
このポリシーにより、電子メールは 90 日後に削除されます。

90 日以内であれば、ご自分の電子メール アドレスと PowerShell ギャラリーとの間で送受信されたすべてのメールのコピーを要求することができます。
このやり取りを要求するには、"DSR Request for emails relating to this account" という件名のメールを [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com) に送信します。
メッセージの本文には、要求する内容を記述してください (例: この電子メール アドレスとの間で送受信されたすべてのメールを送ってください)。ご自分の電子メール アドレスに関する、要求から 90 日以内のすべてのメールが 7 営業日以内に送信されます。

### <a name="powershell-gallery-account-information"></a>PowerShell ギャラリーのアカウント情報

PowerShell ギャラリーのアカウントを作成している場合、次の手順を実行すると PowerShell ギャラリーに格納されているすべての個人情報を確認することができます。

1. PowerShell ギャラリーにサインインし、ユーザー名をクリックします
2. PowerShell ギャラリーのアカウントで使用される電子メール アドレスを示す [アカウント] ページが表示されます

PowerShell ギャラリーで複数のアカウントを作成した場合は、アカウントごとにこの手順を繰り返す必要があります。

### <a name="items-in-the-powershell-gallery"></a>PowerShell ギャラリーのアイテム

PowerShell ギャラリーに公開されたアイテムのエクスポートを迅速に行うため、PowerShell ギャラリーに "GetPSGalleryItemsForAuthor" のスクリプトを公開しました。
このスクリプトにより、アイテムに格納された作成者情報に基づき、PowerShell ギャラリーに配置されたすべてのアイテムのすべてのバージョンのコピーがエクスポートされます。

> [!NOTE]
> 作成者は、自分のアイテムを公開するときに、アイテム マニフェストに格納されます。
> 作成者が PowerShell ギャラリーで使用するアカウントと同じ ID である保証はありません。
> [作成者] フィールドで他の値を使用する場合は、このスクリプトを使用するときに、その値を指定する必要があります。

スクリプトは次の PowerShell コマンドを使用してダウンロードできます。

```powershell
Save-Script Get-repository psgallery
```

これで、次の PowerShell コマンドを実行してスクリプトを直接実行できるようになります。

```powershell
# cd <local folder location>
.\GetPSGalleryItemsForAuthor.ps1
```

作成者と、自分のシステム上でアイテムを保存するフォルダーを指定するように求められます。

## <a name="deleting-personal-data-from-the-powershell-gallery"></a>PowerShell ギャラリーから個人データを削除する

ご自分の PowerShell ギャラリーのアカウント、または PowerShell ギャラリーで所有しているアイテムを削除するには、"GDPR Request for items relating to this account" という件名のメールを cgadmin@microsoft.com に送信します。
メッセージの本文には、削除を依頼する情報を記述します。 たとえば、次のように入力します。

- アイテム "アイテム名" のバージョン x.y.z を削除してください
- アイテム "アイテム名" のすべてのバージョンを削除してください
- 私の PowerShell ギャラリー アカウントを削除してください

PowerShell ギャラリーの管理者が 7 営業日以内に返信します。
指定したアイテムは、要求が送信された後、30 日以内に削除されます。