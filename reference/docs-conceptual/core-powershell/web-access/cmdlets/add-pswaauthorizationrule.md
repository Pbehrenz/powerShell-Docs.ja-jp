---
ms.topic: reference
keywords: PowerShell, コマンドレット
ms.date: 12/12/2016
title: Add-PswaAuthorizationRule
schema: 2.0.0
ms.openlocfilehash: fe2b71dcfa870ba3f92484ae3fd3c45b3107a1bc
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523081"
---
# <a name="add-pswaauthorizationrule"></a>Add-PswaAuthorizationRule

## <a name="synopsis"></a>概要

Windows PowerShell Web Access 承認規則のセットに新しい承認規則を追加します。

## <a name="syntax"></a>構文

### <a name="usergroupnamecomputergroupname"></a>UserGroupNameComputerGroupName

```
Add-PswaAuthorizationRule -ComputerGroupName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usergroupnamecomputername"></a>UserGroupNameComputerName

```
Add-PswaAuthorizationRule -ComputerName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputergroupname"></a>UserNameComputerGroupName

```
Add-PswaAuthorizationRule [-UserName] <String[]> -ComputerGroupName <String> -ConfigurationName <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputername"></a>UserNameComputerName

```
Add-PswaAuthorizationRule [-UserName] <String[]> [-ComputerName] <String> [-ConfigurationName] <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

## <a name="description"></a>説明

**Add-PswaAuthorizationRule** コマンドレットは、Windows PowerShell(r) Web Access 承認規則のセットに新しい承認規則を追加します。

この規則には、ユーザー、コンピューター、Windows PowerShell エンドポイントを指定する必要があります。 個々のユーザー アカウント名、コンピューター名、またはグループを指定して、ユーザーとコンピューターの両方を指定できます。

Active Directory ドメインに参加しているコンピューターの場合、このコマンドレットは、コンピューターのセキュリティ識別子 (SID) を使用して規則を作成します。 そのため、サインイン ページの **[コンピューター名]** フィールドに、短い名前、完全修飾ドメイン名 (FQDN)、または IP アドレスを使用できます。

Active Directory ドメインに参加していないコンピューターの場合、このコマンドレットは、管理者が指定したコンピューター名を使用して規則を作成します。 このコンピューターに正常に接続するには、規則に指定されているとおりのコンピューター名をエンド ユーザーが正確に入力する必要があります。

ネットワーク上に同じ名前のコンピューターが複数ある場合、短い名前では複数のコンピューターに解決される可能性があります。 その結果、接続を確立するときにあいまいさが生じる可能性があります。 たとえば、"*Server1*" というワークグループ コンピューターの規則が存在し、*server1.contoso.com* という新しいコンピューターがネットワークに参加した場合、承認規則を使用した確認は成功し、PowerShell Web Access は、"*Server1*" というコンピューターに接続を確立しようとします。 指定されたワークグループ コンピューターで接続が確立されることは保証されません。試行は、"*Server1*" という名前のワークグループまたはドメイン コンピューターに対して行われます。 承認規則を作成するには、あいまいさを減らすために、対象コンピューターの FQDN を使用することをお勧めします。

承認規則は、代替資格情報ではなく、Windows PowerShell Web Access ユーザーのプライマリ サインイン資格情報を評価します (代替資格情報は、サインイン ページの **[オプションの接続設定]** セクションにある 2 つ目の資格情報セットです)。 この例については、「例 6」を参照してください。

## <a name="parameters"></a>パラメーター

### <a name="-computergroupname-string"></a>-ComputerGroupName \<String\>

この規則がアクセス権を付与している Active Directory Domain Services (AD DS) のコンピューター グループまたはローカル グループの名前を指定します。

|||
|-|-|
| エイリアス                     | なし                  |
| 必須?                   | true                  |
| 位置は?                   | 名前付き                 |
| 既定値               | なし                  |
| パイプライン入力を許可する      | True (ByPropertyName) |
| ワイルドカード文字を許可する | false                 |

### <a name="-computername-string"></a>-ComputerName \<String\>

この規則がアクセス権を付与しているコンピューター名を指定します。

|||
|-|-|
| エイリアス                     | なし                  |
| 必須?                   | true                  |
| 位置は?                   | 名前付き                 |
| 既定値               | なし                  |
| パイプライン入力を許可する      | True (ByPropertyName) |
| ワイルドカード文字を許可する | false                 |

### <a name="-configurationname-string"></a>-ConfigurationName \<String\>

この規則がアクセス権を付与している Windows PowerShell セッション構成 (実行空間とも呼ばれます) の名前を指定します。

|||
|-|-|
| エイリアス                     | なし                  |
| 必須?                   | true                  |
| 位置は?                   | 名前付き                 |
| 既定値               | なし                  |
| パイプライン入力を許可する      | True (ByPropertyName) |
| ワイルドカード文字を許可する | false                 |

### <a name="-credential--pscredential"></a>-Credential  \<PSCredential\>

Windows PowerShell Web Access 承認規則の変更に使用するユーザー アカウントの **PSCredential** オブジェクトを指定します。 このパラメーターを追加しない場合、現在ログオンしているユーザー アカウントがコマンドレットにより使用されます。 承認規則をリモートから追加するために必要な **PSCredential** オブジェクトを取得するには、[Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) コマンドレットを実行します。

|||
|-|-|
| エイリアス                     | なし  |
| 必須?                   | false |
| 位置は?                   | 名前付き |
| 既定値               | なし  |
| パイプライン入力を許可する      | false |
| ワイルドカード文字を許可する | false |

### <a name="-force"></a>-Force

ユーザーに確認せずに、直ちにコマンドを実行します。 なお、単純な、または短いコンピューター名 (ドメイン名ではない名前、完全修飾されていない名前など) を入力した場合にも確認が求められます。 確認はセキュリティ上の理由で必要です。そのため、コンピューターがワークグループに参加している場合にのみ、コンピューターの追加に単純な名前を使用できます。

|||
|-|-|
| エイリアス                              | なし                                 |
| 必須?                            | false                                |
| 位置は?                            | 名前付き                                |
| 既定値                        | なし                                 |
| パイプライン入力を許可する               | false                                |
| ワイルドカード文字を許可する          | false                                |

### <a name="-rulename-string"></a>-RuleName \<String\>

この規則のフレンドリ名を指定します。

|||
|-|-|
| エイリアス                              | なし                                 |
| 必須?                            | false                                |
| 位置は?                            | 名前付き                                |
| 既定値                        | なし                                 |
| パイプライン入力を許可する               | True (ByPropertyName)                |
| ワイルドカード文字を許可する          | false                                |

### <a name="-usergroupname-string"></a>-UserGroupName \<String\[\]\>

この規則がアクセス権を付与している AD DS またはローカル グループ内の 1 つまたは複数のユーザー グループ名を指定します。

|||
|-|-|
| エイリアス                              | なし                                 |
| 必須?                            | true                                 |
| 位置は?                            | 名前付き                                |
| 既定値                        | なし                                 |
| パイプライン入力を許可する               | True (ByPropertyName)                |
| ワイルドカード文字を許可する          | false                                |

### <a name="-username-string"></a>-UserName \<String\[\]\>

この規則がアクセス権を付与している 1 つまたは複数のコンピューター名を指定します。 ユーザー名には、ゲートウェイ コンピューター上のローカル ユーザー アカウント、または AD DS のユーザーを指定できます。 形式は、`domain\user` または `computer\user` です。

|||
|-|-|
| エイリアス                              | なし                                 |
| 必須?                            | true                                 |
| 位置は?                            | 1 で保護されたプロセスとして起動されました                                    |
| 既定値                        | なし                                 |
| パイプライン入力を許可する               | True (ByValue, ByPropertyName)       |
| ワイルドカード文字を許可する          | false                                |

###  <a name="commonparameters"></a>\<CommonParameters\>

このコマンドレットでは、

-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer、および -OutVariable といった一般的なパラメーターをサポートします。
詳細については、「[about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters)」を参照してください。

## <a name="inputs"></a>入力

### <a name="string"></a>String

このコマンドレットは、入力として文字列または文字列の配列を受け入れます。

### <a name="string"></a>String\[\]

このコマンドレットは、入力として文字列または文字列の配列を受け入れます。

## <a name="outputs"></a>出力

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule

このコマンドレットは、承認規則オブジェクトを返します。

## <a name="examples"></a>例

### <a name="example-1"></a>例 1

この例では、_srv2_ 上の _SMAdmins_ グループのユーザーについて、セッション構成に _PSWAEndpoint_ (制限付き実行空間) のアクセス権を付与しています。

> [!NOTE]
> このコンピューター名は完全修飾ドメイン名 (FQDN) にする必要があります。 管理者は制限付きセッション構成または実行空間を定義します。実行空間とは、エンド ユーザーが実行できるコマンドレットおよびタスクの制限された範囲です。 制限付き実行空間を定義すると、ユーザーは、許可されている Windows PowerShell(r) 実行空間内にない他のコンピューターにアクセスできなくなります。そのため、接続のセキュリティが強固になります。 セッション構成の詳細については、「[about_Session_Configurations](/powershell/module/microsoft.powershell.core/about/about_session_configurations)」または「[Windows PowerShell Web Access のインストールと使用](../install-and-use-windows-powershell-web-access.md)」を参照してください。

```powershell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a>例 2

この例では、既定の Windows PowerShell セッション構成 (`Microsoft.PowerShell`) に対するアクセス権を、ユーザー名が `contoso\user1`、`contoso\user2`、`contoso\user3` であるユーザーの *srv2* に付与します。 このコマンドレットは、3 つの規則を作成します (1 人 1 規則)。

```powershell
Add-PswaAuthorizationRule -UserName contoso\user1, contoso\user2, contoso\user3 -ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a>例 3

この例は、パイプラインを使用してユーザー名値を入力する方法を示しています。

```powershell
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule -ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a>例 4

この例は、プロパティ名を指定して、すべてのパラメーターがすべてのパイプラインの値を取得する方法を示しています。

````powershell
$o = New-Object -TypeName PSObject |
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru |
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru |
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" -PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a>例 5

この例は、`PswaServer\ChrisLocal` というローカル ユーザーに、**srv1.contoso.com** というサーバーへのアクセス権を付与する規則を追加します。

この例は、ゲートウェイがワークグループ内にあり、対象コンピューターがドメイン内にあるシナリオを示しています。 承認規則はゲートウェイ上のローカル ユーザーに適用されます。 Windows PowerShell Web Access のサインイン ページで、正常に認証するには、ユーザーが **[オプションの接続設定]** 領域で、2 つ目の資格情報を提供する必要があります。 ゲートウェイ サーバーでは、複数セットの資格情報が使用され、*srv1.contoso.com* という対象コンピューターでユーザーの認証に使用されます。

````powershell
Add-PswaAuthorizationRule -UserName PswaServer\ChrisLocal -ComputerName srv1.contoso.com -ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a>例 6

この例では、すべてのコンピューターですべてのエンドポイントに対するアクセス権をすべてのユーザーに許可します。 これで、基本的に承認規則がオフになります。

> [!NOTE]
> `*` ワイルド カード文字の使用は、セキュリティが重要な展開には推奨されません。また、テスト環境のみで使用するか、セキュリティを緩和できる展開でのみ使用してください。

````powershell
Add-PswaAuthorizationRule -UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a>参照

[Get-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592891(v=wps.630).aspx)

[Remove-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592893(v=wps.630).aspx)

[Test-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592892(v=wps.630).aspx)

[Install-PswaWebApplication](https://technet.microsoft.com/library/jj592894(v=wps.630).aspx)

[Add-Member](http://go.microsoft.com/fwlink/p/?LinkId=113280)

[New-Object](http://go.microsoft.com/fwlink/p/?LinkId=113355)

[Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936)
