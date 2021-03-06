---
ms.date: 06/12/2017
keywords: DSC, PowerShell, 構成, セットアップ
title: 構成名を使用したプル クライアントのセットアップ
ms.openlocfilehash: d71376d84b9d4b0e74fdccab4b9249b2ca4263cb
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188093"
---
# <a name="setting-up-a-pull-client-using-configuration-names"></a>構成名を使用したプル クライアントのセットアップ

> 適用先: Windows PowerShell 5.0

> [!IMPORTANT]
> プル サーバー (Windows Feature *DSC-Service*) は、Windows Server のサポート対象のコンポーネントですが、新機能が提供される予定はありません。 管理対象のクライアントは、(Windows Server のプル サーバー以降の機能が含まれる) [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) または、[こちら](pullserver.md#community-solutions-for-pull-service)に列挙されているコミュニティ ソリューションのいずれかに切り替えを開始することをお勧めします。

各ターゲット ノードに対し、プル モードを使用するように指示し、プル サーバーに接続して構成を取得するための URL を指定する必要があります。
これを行うには、必要な情報を備えるようにローカル構成マネージャー (LCM) を構成する必要があります。
LCM を構成するには、**DSCLocalConfigurationManager** 属性で修飾された特別な種類の構成を作成します。
LCM の構成の詳細については、「[ローカル構成マネージャーの構成](metaConfig.md)」をご覧ください。

> **注**: このトピックは、PowerShell 5.0 に適用されます。
PowerShell 4.0 でのプル クライアントのセットアップについては、「[PowerShell 4.0 での構成 ID を使用したプル クライアントのセットアップ](pullClientConfigID4.md)」を参照してください。

次のスクリプトは、"CONTOSO-PullSrv" という名前のサーバーから構成をプルするように LCM を構成します。

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('ClientConfig')
        }
    }
}
PullClientConfigNames
```

このスクリプトでは、**ConfigurationRepositoryWeb** ブロックにプル サーバーを定義しています。
**ServerURL** プロパティには、プル サーバー用のエンドポイントを指定します。

**RegistrationKey** プロパティは、プル サーバーのすべてのクライアント ノードとそのプル サーバーとの間で共有されるキーです。
同じ値がプル サーバー上のファイルに格納されます。

**ConfigurationNames** プロパティは、クライアント ノード用の構成の名前を指定する配列です。
プル サーバーでは、このクライアント ノードの構成 MOF ファイルに *ConfigurationNames*.mof という名前を指定する必要があります。ここで、*ConfigurationNames* はこのメタ構成に設定した **ConfigurationNames** プロパティの値と一致します。

>**注:** **ConfigurationNames** に複数の値を指定する場合、構成に **PartialConfiguration** ブロックも指定する必要があります。
部分構成の詳細については、「[PowerShell Desired State Configuration の部分構成](partialConfigs.md)」を参照してください。

このスクリプトを実行すると、**PullClientConfigNames** という名前の新しい出力フォルダーが作成され、そこにメタ構成 MOF ファイルが格納されます。
この場合、メタ構成 MOF ファイルの名前は `localhost.meta.mof` になります。

構成を適用するには、**Path** をメタ構成 MOF ファイルの場所に設定して **Set-DscLocalConfigurationManager** コマンドレットを呼び出します。

```powershell
Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigNames –Verbose.
```

> **注**: 登録キーは、Web プル サーバーでのみ動作します。
SMB プル サーバーでは、引き続き **ConfigurationID** を使用する必要があります。
**ConfigurationID** を使用したプル サーバーの構成については、「[構成 ID を使用したプル クライアントのセットアップ](PullClientConfigNames.md)」を参照してください。

## <a name="resource-and-report-servers"></a>リソースおよびレポート サーバー

LCM 構成で **ConfigurationRepositoryWeb** ブロックまたは **ConfigurationRepositoryShare** ブロックのみを指定した場合 (前の例はこれに当たります)、プル クライアントは、指定されたサーバーからリソースをプルしますが、そのサーバーに対してレポートは送信しません。
構成、リソース、およびレポートについて単一のプル サーバーを使うことができますが、レポートをセットアップするために **ReportRepositoryWeb** ブロックを作成する必要があります。
次の例は、単一のプル サーバーに対して構成とリソースをプルし、レポート データを送信するようにクライアントを設定するメタ構成を示しています。

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigNames
```

また、リソース用とレポート用にそれぞれ異なるプル サーバーを指定することもできます。
リソース サーバーを指定するには、**ResourceRepositoryWeb** (Web プル サーバーの場合) または **ResourceRepositoryShare** ブロック (SMB プル サーバーの場合) を使用します。
レポート サーバーを指定するには、**ReportRepositoryWeb** ブロックを使用します。
レポート サーバーを SMB サーバーにすることはできません。
次のメタ構成は、**CONTOSO-PullSrv** から構成を取得し、**CONTOSO-ResourceSrv** からリソースを取得し、**CONTOSO-ReportSrv** に状態レポートを送信するように、プル クライアントを構成します。

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }

        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-ResourceSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '30ef9bd8-9acf-4e01-8374-4dc35710fc90'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-ReportSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '6b392c6a-818c-4b24-bf38-47124f1e2f14'
        }
    }
}
PullClientConfigNames
```

## <a name="see-also"></a>参照

* [構成 ID を使用したプル クライアントのセットアップ](PullClientConfigNames.md)
* [DSC Web プル サーバーのセットアップ](pullServer.md)