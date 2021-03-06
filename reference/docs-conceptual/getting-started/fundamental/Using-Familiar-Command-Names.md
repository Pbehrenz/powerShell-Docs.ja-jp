---
ms.date: 08/27/2018
keywords: PowerShell, コマンドレット
title: 使い慣れたコマンド名の使用
ms.assetid: 021e2424-c64e-4fa5-aa98-aa6405758d5d
ms.openlocfilehash: c5665f64fd832eb9c807f413a8e879f63db7f8c6
ms.sourcegitcommit: c170a1608d20d3c925d79c35fa208f650d014146
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2018
ms.locfileid: "43353251"
---
# <a name="using-familiar-command-names"></a>使い慣れたコマンド名の使用

PowerShell では、代替名でコマンドを参照するエイリアスをサポートしています。 エイリアスがあることで、他のシェルの経験があるユーザーは、既に知っている一般的なコマンド名を PowerShell のほぼ同じ操作に利用できます。

エイリアスは、新しい名前を別のコマンドに関連付けます。 たとえば、PowerShell には、出力ウィンドウをクリアする `Clear-Host` という内部関数があります。 コマンド プロンプトに `cls` または `clear` エイリアスのどちらかを入力できます。 PowerShell はこれらのエイリアスを解釈して、`Clear-Host` 関数を実行します。

この機能は、ユーザーが PowerShell を習得するうえで役立ちます。 最初に、ほとんどの **cmd.exe** および Unix ユーザーには、既に名前を知っているコマンドのレパートリーが多数あります。 同等の PowerShell のコマンドでは、同一の結果が得られない場合があります。 しかし、十分に近い結果になるので、PowerShell のコマンド名を知らなくてもユーザーが既知のコマンドを利用することは可能です。 新しいコマンド シェルを習得するうえで、"指が覚えている" ことはもう 1 つの主なストレス要因になります。 長年にわたって **cmd.exe** を使用してきた場合、画面をクリアするには、反射的に `cls` コマンドを入力してしまうでしょう。 `Clear-Host` のエイリアスがなければ、エラー メッセージを受け取ってしまい、出力をクリアするにはどうすればいいかわからないでしょう。

PowerShell で使用できる一般的な **cmd.exe** および UNIX コマンドのいくつかを次の一覧に示します。

|||||
|-|-|-|-|
|cat|dir|マウント|rm|
|cd|echo|move|rmdir|
|chdir|erase|popd|sleep|
|clear|h|ps|sort|
|cls|history|pushd|tee|
|copy|kill|pwd|型|
|del|lp|r|write|
|diff|ls|ren||

`Get-Alias` コマンドレットでは、エイリアスに関連付けられたネイティブな PowerShell コマンドの実際の名前が表示されます。

```powershell
PS> Get-Alias cls
```

```Output
CommandType     Name                               Version    Source
-----------     ----                               -------    ------
Alias           cls -> Clear-Host
```

## <a name="interpreting-standard-aliases"></a>標準エイリアスの解釈

前述したエイリアスは、他のコマンド シェルとの名前の互換性を目的として設計されていました。
PowerShell に組み込まれているほとんどのエイリアスは、簡略化を目的として設計されています。 名前が短いほど入力は簡単になりますが、エイリアスが何を参照しているかを把握していない場合、読みにくくなります。

PowerShell のエイリアスでは、わかりやすさと簡潔さのバランスを取る試みがなされています。 PowerShell では、一般的な名詞と動詞に対して、標準となる一連のエイリアスを使用しています。

たとえば、次のような省略形があります。

| 名詞または動詞 | 省略形 |
|--------------|--------------|
| 取得          | g            |
| 設定          | s            |
| 項目         | i            |
| インストール先     | l            |
| コマンド      | cm           |
| エイリアス        | al           |

以下のエイリアスは、省略名を知っていれば理解できます。

| コマンドレット名    | エイリアス |
|----------------|-------|
| `Get-Item `    | gi    |
| `Set-Item`     | si    |
| `Get-Location` | gl    |
| `Set-Location` | sl    |
| `Get-Command`  | gcm   |
| `Get-Alias`    | gal   |

PowerShell のエイリアスを使い慣れたら、**sal** エイリアスは `Set-Alias` を参照していると簡単に推測できるようになります。

## <a name="creating-new-aliases"></a>新しいエイリアスの作成

`Set-Alias` コマンドレットを使用して、独自のエイリアスを作成できます。 たとえば、次のステートメントは、前述した標準のコマンドレットのエイリアスを作成します。

```powershell
Set-Alias -Name gi -Value Get-Item
Set-Alias -Name si -Value Set-Item
Set-Alias -Name gl -Value Get-Location
Set-Alias -Name sl -Value Set-Location
Set-Alias -Name gcm -Value Get-Command
```

PowerShell では、起動時に類似のコマンドを内部で使用しますが、これらのエイリアスは変更できません。
これらのコマンドのいずれかを実行しようとすると、エイリアスを変更できないことを示すエラーが表示されます。 たとえば、次のように入力します。

```
PS> Set-Alias -Name gi -Value Get-Item
Set-Alias : Alias is not writeable because alias gi is read-only or constant and cannot be written to.
At line:1 char:10
+ Set-Alias  <<<< -Name gi -Value Get-Item
```