---
ms.date: 06/12/2017
keywords: DSC, PowerShell, 構成, セットアップ
title: DSC WindowsFeatureSet リソース
ms.openlocfilehash: 582f9b1f439056118680f6f814d2c202d0e823be
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2018
ms.locfileid: "34186730"
---
# <a name="dsc-windowsfeatureset-resource"></a>DSC WindowsFeatureSet リソース

> 適用先: Windows PowerShell 5.0

Windows PowerShell Desired State Configuration (DSC) の **WindowsFeatureSet** リソースは、役割と機能がターゲット ノードで追加または削除されることを保証するためのメカニズムを備えています。
このリソースは[複合リソース](authoringResourceComposite.md)であり、`Name` プロパティに指定されている機能ごとに [WindowsFeature リソース](windowsfeatureResource.md)を呼び出します。

Windows 機能の数を同じ状態に構成するときにこのリソースを使用します。

## <a name="syntax"></a>構文

```
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [bool] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a>プロパティ

|  プロパティ  |  説明   |
|---|---|
| 名前| 追加または削除する役割または機能の名前。 これは [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) コマンドレットの **Name** プロパティと同じものであり、役割または機能の表示名ではありません。|
| Credential| 役割または機能の追加や削除に使用する資格情報。|
| Ensure| 役割または機能を追加するかどうかを示します。 役割または機能を追加するには、このプロパティを "Present" に設定します。役割または機能を削除するには、このプロパティを "Absent" に設定します。|
| IncludeAllSubFeature| **Name** プロパティで指定した機能を使用して必要なすべてのサブ機能を含めるには、このプロパティを **$true** に設定します。|
| LogPath| リソース プロバイダーの操作を記録するログ ファイルへのパス。|
| DependsOn| このリソースを構成する前に、他のリソースの構成を実行する必要があることを示します。 たとえば、最初に実行するリソース構成スクリプト ブロックの ID が __ResourceName__ で、そのタイプが __ResourceType__ である場合、このプロパティを使用する構文は `DependsOn = "[ResourceType]ResourceName"` になります。|
| ソース| 必要に応じて、インストールに使用するソース ファイルの場所を示します。|

## <a name="example"></a>例

次の構成では、**Web-Server** (IIS) 機能、**SMTP Server** 機能、各機能のすべてのサブ機能がインストールされます。

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        }
    }
}
```