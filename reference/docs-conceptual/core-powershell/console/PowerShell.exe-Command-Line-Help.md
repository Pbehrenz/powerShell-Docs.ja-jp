---
ms.date: 08/14/2018
keywords: PowerShell, コマンドレット
title: PowerShell.exe コマンドラインのヘルプ
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: c7f35511e876e8e5189d8a2b949555603d43f731
ms.sourcegitcommit: 56b9be8503a5a1342c0b85b36f5ba6f57c281b63
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2018
ms.locfileid: "43133163"
---
# <a name="powershellexe-command-line-help"></a>PowerShell.exe コマンドラインのヘルプ

PowerShell.exe を使用して、Cmd.exe などの別のツールのコマンド ラインから PowerShell セッションを起動したり、PowerShell.exe を PowerShell コマンド ラインで使用して、新しいセッションを開始したりすることができます。 パラメーターを使用して、セッションをカスタマイズします。

## <a name="syntax"></a>構文

```syntax
PowerShell[.exe]
       [-Command { - | <script-block> [-args <arg-array>]
                     | <string> [<CommandParameters>] } ]
       [-EncodedCommand <Base64EncodedCommand>]
       [-ExecutionPolicy <ExecutionPolicy>]
       [-File <FilePath> [<Args>]]
       [-InputFormat {Text | XML}]
       [-Mta]
       [-NoExit]
       [-NoLogo]
       [-NonInteractive]
       [-NoProfile]
       [-OutputFormat {Text | XML}]
       [-PSConsoleFile <FilePath> | -Version <PowerShell version>]
       [-Sta]
       [-WindowStyle <style>]

PowerShell[.exe] -Help | -? | /?
```

## <a name="parameters"></a>パラメーター

### <a name="-encodedcommand-base64encodedcommand"></a>-EncodedCommand <Base64EncodedCommand>

Base 64 エンコード文字列版のコマンドを許可します。 複雑な引用符や中かっこを必要とするコマンドを PowerShell に渡す場合にこのパラメーターを使用します。

### <a name="-executionpolicy-executionpolicy"></a>-ExecutionPolicy <ExecutionPolicy>

現在のセッションの既定の実行ポリシーを設定し、$env:PSExecutionPolicyPreference 環境変数に保存します。 このパラメーターは、レジストリに設定された PowerShell 実行ポリシーを変更しません。 有効な値の一覧など、PowerShell 実行ポリシーについては、「[about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies)」を参照してください。

### <a name="-file-filepath-parameters"></a>-File <FilePath> \[<Parameters>]

スクリプトで作成される関数と変数を現在のセッションで使用できるように、指定したスクリプトをローカル スコープ ("ドット ソース形式") で実行します。 スクリプト ファイルのパスと (存在する場合) パラメーターを入力します。 **File** は、コマンド内の最後のパラメーターにする必要があります。 **-File** パラメーターの後に入力されたすべての値は、スクリプト ファイルのパスとそのスクリプトに渡されるパラメーターとして解釈されます。

スクリプトに渡されるパラメーターは、(現在のシェルによる解釈の後で) リテラル文字列として渡されます。 たとえば、cmd.exe で環境変数値を渡す場合は、cmd.exe 構文 `powershell -File .\test.ps1 -Sample %windir%` を使用します。この例では、スクリプトはリテラル文字列 `$env:windir` を受け取り、その環境変数の値 `powershell -File .\test.ps1 -Sample $env:windir` は受け取りません。

### <a name="-inputformat-text--xml"></a>\-InputFormat {Text | XML}

PowerShell に送信されるデータの形式を記述します。 使用できる値は、"Text" (テキスト文字列) と "XML" (シリアル化された CLIXML 形式) です。

### <a name="-mta"></a>-Mta

マルチスレッド アパートメントを使用して、PowerShell を起動します。 このパラメーターは、PowerShell 3.0 で導入されました。 PowerShell 3.0 では、シングルスレッド アパートメント (STA) が既定値です。 PowerShell 2.0 では、マルチスレッド アパートメント (MTA) が既定値です。

### <a name="-noexit"></a>-NoExit

スタートアップ コマンドを実行後、終了しません。

### <a name="-nologo"></a>-NoLogo

スタートアップ時に著作権の見出しを非表示にします。

### <a name="-noninteractive"></a>-NonInteractive

ユーザーに対話的なプロンプトを表示しません。

### <a name="-noprofile"></a>-NoProfile

PowerShell プロファイルを読み込みません。

### <a name="-outputformat-text--xml"></a>-OutputFormat {Text | XML}

PowerShell からの出力の形式を決定します。 使用できる値は、"Text" (テキスト文字列) と "XML" (シリアル化された CLIXML 形式) です。

### <a name="-psconsolefile-filepath"></a>-PSConsoleFile <FilePath>

指定された PowerShell コンソール ファイルを読み込みます。 コンソール ファイルの名前とパスを入力します。 コンソール ファイルを作成するには、PowerShell で [`Export-Console`](/powershell/module/Microsoft.PowerShell.Core/Export-Console) コマンドレットを使用します。

### <a name="-sta"></a>-Sta

シングルスレッド アパートメントを使用して、PowerShell を起動します。 PowerShell 3.0 では、シングルスレッド アパートメント (STA) が既定値です。 PowerShell 2.0 では、マルチスレッド アパートメント (MTA) が既定値です。

### <a name="-version-powershell-version"></a>-Version <PowerShell Version>

指定したバージョンの PowerShell を起動します。 指定するバージョンがシステムにインストールされている必要があります。 PowerShell 3.0 がコンピューターにインストールされている場合、有効な値は "2.0" と "3.0" です。 既定値は "3.0" です。

PowerShell 3.0 がインストールされていない場合、有効な値は "2.0" のみです。 他の値は無視されます。

詳しくは、「[Windows PowerShell のインストール](../../setup/installing-windows-powershell.md)」をご覧ください。

### <a name="-windowstyle-window-style"></a>-WindowStyle <Window style>

セッションのウィンドウ スタイルを設定します。 使用できる値は、Normal、Minimized、Maximized、および Hidden です。

### <a name="-command"></a>-Command

PowerShell のコマンド プロンプトに入力された場合と同様に、指定されたコマンド (任意のパラメーターを付与する) を実行します。 実行後は、`-NoExit` パラメーターが指定されていない限り、PowerShell は終了します。
`-Command` の後にある任意のテキストは、単一のコマンド ラインとして PowerShell に送信されます。 これは、`-File` がスクリプトに送信されたパラメーターを処理する方法とは異なります。

Command の値には、"-"、文字列、またはスクリプト ブロックを指定できます。 またはスクリプト ブロックを指定できます。 Command の値が "-" の場合、コマンド テキストは標準入力から読み取られます。

スクリプト ブロックは中かっこ ({}) で囲む必要があります。 スクリプト ブロックを指定できるのは、PowerShell.exe を PowerShell で実行する場合だけです。 スクリプトの結果は、ライブ オブジェクトとしてではなく、逆シリアル化された XML オブジェクトとして親シェルに返されます。

Command の値が文字列の場合、**Command** はコマンドの最後のパラメーターでなければなりません。コマンドの後に入力された文字は、コマンド引数として解釈されるためです。

PowerShell コマンドを実行する文字列を書き込むには、次の形式を使用します。

```powershell
"& {<command>}"
```

引用符は文字列であることを示し、呼び出し演算子 (&) によってコマンドが実行されます。

### <a name="-help---"></a>-Help、-?、/?

Powershell.exe の構文を示します。 PowerShell で PowerShell.exe のコマンドを入力している場合、コマンド パラメーターの前にスラッシュ (/) ではなくハイフン (-) を入力してください。 Cmd.exe では、ハイフンとスラッシュのいずれかを使用できます。

> [!NOTE]
> トラブルシューティング上の注意: PowerShell 2.0 では、一部のプログラムを Windows PowerShell コンソールで開始すると、LastExitCode 0xc0000142 で失敗します。

## <a name="examples"></a>例

```powershell
# Create a new PowerShell session and load a saved console file
PowerShell -PSConsoleFile sqlsnapin.psc1

# Create a new PowerShell V2 session with text input, XML output, and no logo
PowerShell -Version 2.0 -NoLogo -InputFormat text -OutputFormat XML

# Execute a PowerShell Command in a session
PowerShell -Command "Get-EventLog -LogName security"

# Run a script block in a session
PowerShell -Command {Get-EventLog -LogName security}

# An alternate way to run a command in a new session
PowerShell -Command "& {Get-EventLog -LogName security}"

# To use the -EncodedCommand parameter:
$command = "dir 'c:\program files' "
$bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
$encodedCommand = [Convert]::ToBase64String($bytes)
powershell.exe -encodedCommand $encodedCommand
```
