---
ms.date: 06/05/2017
keywords: PowerShell, コマンドレット
title: スクリプト ウィンドウとコンソール ウィンドウでタブ補完を使用する方法
ms.assetid: 3b752c3c-0bd0-4eca-a2d3-2d5a37fd9d84
ms.openlocfilehash: e1f8146b6113a82fd3d857c98550ec2e459715a4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954927"
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a>スクリプト ウィンドウとコンソール ウィンドウでタブ補完を使用する方法

タブ補完は、スクリプト ウィンドウまたはコマンド ウィンドウで入力するときに、自動的に提供される支援機能です。 この機能を活用するには、次の手順を実行します。

## <a name="to-automatically-complete-a-command-entry"></a>コマンドの入力を自動的に補完するには

コマンド ウィンドウまたはスクリプト ウィンドウでは、コマンドのいくつかの文字を入力し、Tab キーを押すと、目的の補完テキストを選択できます。 最初に入力したテキストで始まる項目が複数ある場合は、目的の項目が表示されるまで Tab キーを何回か押します。 タブ補完は、コマンドレット名、パラメーター名、変数名、オブジェクトのプロパティ名、またはファイルのパスを入力する場合に役立ちます。

> [!NOTE]
> スクリプト ウィンドウでは、.ps1、.psd1、.psm1 ファイルを編集している場合にのみ、Tab キーを押したときに自動的にコマンドが補完されます。 コマンド ウィンドウに入力する場合は、常にタブ補完が機能します。

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a>コマンドレット パラメーターの入力を自動的に補完するには

コマンド ウィンドウまたはスクリプト ウィンドウで、コマンドレット名を入力し、その後にダッシュを入力し、次に Tab キーを押します。

たとえば、「`Get-Process -`」と入力し、Tab キーを何回か押すと、コマンドレットの各パラメーターが順番に表示されます。

## <a name="see-also"></a>参照

- [Windows PowerShell ISE の紹介](Introducing-the-Windows-PowerShell-ISE.md)
- [PowerShell タブを作成する方法](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)