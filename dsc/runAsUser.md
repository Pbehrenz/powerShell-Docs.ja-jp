---
ms.date: 06/12/2017
keywords: DSC, PowerShell, 構成, セットアップ
title: ユーザーの資格情報を指定して DSC を実行する
ms.openlocfilehash: 4a6c3d8b561cd0a27be07a68f1b577f7bf764254
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893911"
---
# <a name="running-dsc-with-user-credentials"></a>ユーザーの資格情報を指定して DSC を実行する

> 適用先: Windows PowerShell 5.0、Windows PowerShell 5.1

資格情報のセットを指定して DSC リソースを実行するには、構成の中で自動 **PsDscRunAsCredential** プロパティを使います。
既定では、DSC はシステム アカウントとして各リソースを実行します。
時には、ユーザーとして実行することが必要な場合があります。たとえば、特定のユーザー コンテキストで MSI パッケージをインストールする場合や、ユーザーのレジストリ キーを設定する場合、ユーザーの特定のローカル ディレクトリにアクセスする場合、ネットワーク共有にアクセスする場合などです。

すべての DSC リソースには、任意のユーザー資格情報に設定できる **PsDscRunAsCredential** プロパティがあります ([PSCredential](/dotnet/api/system.management.automation.pscredential) オブジェクト)。
資格情報は、構成内でプロパティの値としてハードコーディングするか、[Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) に対して値を設定することができます。後者の場合は、構成のコンパイル時に資格情報を入力するように求めるプロンプトが表示されます (構成のコンパイルの詳細については、[構成](configurations.md)に関する記事を参照してください)。

> [!NOTE] 
> PowerShell 5.0 では、複合リソースを呼び出す構成での **PsDscRunAsCredential** プロパティの使用はサポートされていませんでした。
> PowerShell 5.1 では、複合リソースを呼び出す構成で **PsDscRunAsCredential** プロパティがサポートされています。
> **PsDscRunAsCredential** プロパティは PowerShell 4.0 では使用できません。

次の例では、`Get-Credential` を使って、ユーザーに資格情報を入力するようにプロンプトが出ます。
また、[Registry](registryResource.md) リソースを使って、Windows のコマンド プロンプト ウィンドウの背景色を指定するレジストリ キーを変更します。

```powershell
Configuration ChangeCmdBackGroundColor
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        Registry CmdPath
        {
            Key                  = 'HKEY_CURRENT_USER\SOFTWARE\Microsoft\Command Processor'
            ValueName            = 'DefaultColor'
            ValueData            = '1F'
            ValueType            = 'DWORD'
            Ensure               = 'Present'
            Force                = $true
            Hex                  = $true
            PsDscRunAsCredential = Get-Credential
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost';
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}

ChangeCmdBackGroundColor -ConfigurationData $configData
```

> [!NOTE]
> この例では、有効な証明書が `C:\publicKeys\targetNode.cer` に存在することと、示されている値がその証明書の拇印であることを想定しています。
> DSC 構成 MOF ファイル内の資格情報を暗号化する方法の詳細については、「[MOF ファイルのセキュリティ保護](secureMOF.md)」を参照してください。
