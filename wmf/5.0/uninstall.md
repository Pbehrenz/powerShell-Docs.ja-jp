---
ms.date: 06/12/2017
keywords: WMF, PowerShell, セットアップ
ms.openlocfilehash: 64a29aa87507e65a182837df538c5e695c420cb3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2018
ms.locfileid: "34222056"
---
# <a name="uninstallation-instructions"></a>アンインストール手順

## <a name="using-command-prompt"></a>コマンド プロンプトを使用
1.  **コマンド プロンプト**を開きます。
2.  [Windows Update スタンドアロン ランチャー](https://support.microsoft.com/en-us/kb/934307)を次のように実行します。

Windows Server 2012 R2 および Windows 8.1:
```powershell
wusa /uninstall /kb:3134758
```
Windows Server 2012:
```powershell
wusa /uninstall /kb:3134759
```
Windows Server 2008 R2 SP1 および Windows 7 SP1:
```powershell
wusa /uninstall /kb:3134760
```

## <a name="using-control-panel"></a>コントロール パネルを使用
1.  **[コントロール パネル]** を開きます。
2.  **[プログラム]** を開き、**[プログラムのアンインストール]** を開きます。
3.  **[インストールされた更新プログラムを表示]** をクリックします。
4.  インストールされた更新プログラムの一覧から **[Windows Management Framework 5.0]** を選択します。 これは *KB3134758*、*KB3134759*、または *KB3134760* に対応しています。 **[アンインストール]** をクリックします。
