---
ms.date: 10/12/2017
keywords: DSC, PowerShell, 構成, セットアップ
title: 以前のバージョンの Windows PowerShell でローカル構成マネージャーを構成する
ms.openlocfilehash: 05e315539e51e31b5a496e8c595ac3695d9a0c97
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189382"
---
# <a name="configuring-the-local-configuration-manager-in-previous-versions-of-windows-powershell"></a>以前のバージョンの Windows PowerShell でローカル構成マネージャーを構成する

>適用先: Windows PowerShell 4.0

**Windows PowerShell 5.0 以降に関連する情報については、「[ローカル構成マネージャーの構成](metaConfig.md)」を参照してください。**

ローカル構成マネージャーは、Windows PowerShell Desired State Configuration (DSC) エンジンです。
すべてのターゲット ノードで実行され、DSC 構成スクリプトに含まれている構成リソースを呼び出します。
このトピックでは、ローカル構成マネージャーのプロパティを一覧表示し、ターゲット ノードでローカル構成マネージャーの設定を変更する方法について説明します。

## <a name="local-configuration-manager-properties"></a>ローカル構成マネージャーのプロパティ

設定または取得できるローカル構成マネージャーのプロパティを次に示します。

- **AllowModuleOverwrite**: 構成サービスからダウンロードされた新しい構成で、ターゲット ノードの古い構成を上書きできるかどうかを制御します。 設定可能な値は True および False です。
- **CertificateID**: 構成で渡される資格情報をセキュリティで保護するために使用される証明書の拇印。 詳細については、「[Want to secure credentials in Windows PowerShell Desired State Configuration? (Windows PowerShell Desired State Configuration で資格情報をセキュリティ保護する)](http://blogs.msdn.com/b/powershell/archive/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration.aspx)」を参照してください。
- **ConfigurationID**: プル サービスから特定の構成ファイルを取得するために使用する GUID を指定します。 この GUID によって、適切な構成ファイルにアクセスできます。
- **ConfigurationMode**: ローカル構成マネージャーによってターゲット ノードに構成が実際に適用される方法を指定します。 次の値を指定できます。
  - **ApplyOnly**: このオプションを使用すると、DSC によって構成が適用され、その後何も行われません。ただし、ターゲット ノードに直接新しい構成を送信した場合や、プル サービスに接続しており、DSC が プル サービスを確認して新しい構成を検出した場合を除きます。 ターゲット ノードの構成のずれが発生した場合、アクションは実行されません。
  - **ApplyAndMonitor**: このオプション (既定) を使用すると、新しい構成をターゲット ノードに直接送信した場合でも、プル サービスで検出された場合でも、DSC によって新しい構成が適用されます。 その後、ターゲット ノードの構成が構成ファイルからずれた場合、DSC はログで不一致を報告します。 DSC ログの詳細については、「[Using Event Logs to Diagnose Errors in Desired State Configuration (Desired State Configuration でのイベント ログを使用したエラーの診断)](http://blogs.msdn.com/b/powershell/archive/2014/01/03/using-event-logs-to-diagnose-errors-in-desired-state-configuration.aspx)」を参照してください。
  - **ApplyAndAutoCorrect**: このオプションを使用すると、新しい構成をターゲット ノードに直接送信した場合も、プル サービスで検出された場合も、DSC によって新しい構成が適用されます。 その後、ターゲット ノードの構成が構成ファイルからずれた場合、DSC はログで不一致を報告し、構成ファイルに準拠するようにターゲット ノードの構成を調整します。
- **ConfigurationModeFrequencyMins**: DSC のバックグラウンド アプリケーションがターゲット ノード上の現在の構成の実装を試行する頻度を表します (分単位)。 既定値は 15 です。 この値は、RefreshMode と組み合わせて設定することができます。 RefreshMode を PULL に設定すると、ターゲット ノードは RefreshFrequencyMins の設定間隔で構成サービスに接続し、現在の構成をダウンロードします。 RefreshMode の値に関係なく、ConfigurationModeFrequencyMins の設定間隔で、整合性エンジンは、ターゲット ノードにダウンロードされた最新の構成を適用します。 RefreshFrequencyMins は、ConfigurationModeFrequencyMins の倍数である整数に設定する必要があります。
- **Credential**: 構成サービスへの接続など、リモート リソースにアクセスするために必要な資格情報を示します (Get-Credential と同様)。
- **DownloadManagerCustomData**: ダウンロード マネージャーに固有のカスタム データを格納する配列を表します。
- **DownloadManagerName**: 構成とモジュールのダウンロード マネージャーの名前を示します。
- **RebootNodeIfNeeded**: ターゲット ノード上の特定の構成変更では、変更を適用するために再起動する必要がある場合があります。 値 **True** を指定すると、このプロパティは、構成が完全に適用されるとすぐに、追加の警告なく、ノードを再起動します。 **False** (既定値) の場合は、構成が完了しても、変更を有効にするために、ノードを手動で再起動する必要があります。
- **RefreshFrequencyMins**: プル サービスをセットアップするときに使用します。 ローカル構成マネージャーが プル サービスに接続して現在の構成をダウンロードする頻度 (分) を表します。 この値は、ConfigurationModeFrequencyMins と組み合わせて設定することができます。 RefreshMode を PULL に設定すると、ターゲット ノードは RefreshFrequencyMins の設定間隔で プル サービスに接続し、現在の構成をダウンロードします。 その後、ConfigurationModeFrequencyMins の設定間隔で、整合性エンジンがターゲット ノードにダウンロードされた最新の構成を適用します。 RefreshFrequencyMins が ConfigurationModeFrequencyMins の倍数である整数に設定されていない場合は、システムによって切り上げられます。 既定値は 30 です。
- **RefreshMode**: 設定可能な値は **Push** (既定値) と **Pull** です。 "プッシュ" 構成では、任意のクライアント コンピューターを使用して各ターゲット ノードに構成ファイル配置する必要があります。 "プル" モードでは、構成ファイルに接続およびアクセスするようにローカル構成マネージャーのプル サービスを設定する必要があります。

### <a name="example-of-updating-local-configuration-manager-settings"></a>ローカル構成マネージャー設定の更新の例

次の例に示すように、構成スクリプトのノード ブロックに **LocalConfigurationManager** ブロックを含めることによって、ターゲット ノードのローカル構成マネージャー設定を更新できます。

```powershell
Configuration ExampleConfig
{
    Node “Server001”
    {
        LocalConfigurationManager
        {
            ConfigurationID = "646e48cb-3082-4a12-9fd9-f71b9a562d4e"
            ConfigurationModeFrequencyMins = 45
            ConfigurationMode = "ApplyAndAutocorrect"
            RefreshMode = "Pull"
            RefreshFrequencyMins = 90
            DownloadManagerName = "WebDownloadManager"
            DownloadManagerCustomData = (@{ServerUrl="https://$PullService/psdscpullserver.svc"})
            CertificateID = "71AA68562316FE3F73536F1096B85D66289ED60E"
            Credential = $cred
            RebootNodeIfNeeded = $true
            AllowModuleOverwrite = $false
        }
# One or more resource blocks can be added here
    }
}

# The following line invokes the configuration and creates a file called Server001.meta.mof at the specified path
ExampleConfig -OutputPath "c:\users\public\dsc"
```

前の例のスクリプトを実行すると、目的の設定を指定および格納する MOF ファイルが生成されます。
設定を適用するには、次の例に示すように **Set-DscLocalConfigurationManager** コマンドレットを使用します。

```powershell
Set-DscLocalConfigurationManager -Path "c:\users\public\dsc"
```

> **注**: **Path** パラメーターには、前の例で構成を呼び出したときに **OutputPath** パラメーターに指定したパスと同じパスを指定する必要があります。

現在のローカル構成マネージャー設定を表示するには、**Get-DscLocalConfigurationManager** コマンドレットを使用します。
パラメーターなしでこのコマンドレットを呼び出す場合、既定では、ローカル構成マネージャーを実行しているノードのローカル構成マネージャー設定が取得されます。
別のノードを指定するには、このコマンドレットで **CimSession** パラメーターを使用します。