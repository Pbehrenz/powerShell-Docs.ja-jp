---
ms.date: 2017-06-09
schema: 2.0.0
keywords: powershell
title: RequireLicenseAcceptanceScript
ms.openlocfilehash: 7092fb2e63b9e2b1eca59cd418317631bff8b172
ms.sourcegitcommit: cd66d4f49ea762a31887af2c72d087b219ddbe10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2017
---
# <a name="requiring-license-acceptance-for-scripts"></a><span data-ttu-id="0acb5-103">スクリプトでのライセンス同意の必須化</span><span class="sxs-lookup"><span data-stu-id="0acb5-103">Requiring License Acceptance for Scripts</span></span>

<span data-ttu-id="0acb5-104">ライセンス同意は、スクリプトではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="0acb5-104">License Acceptance is not supported for scripts.</span></span> <span data-ttu-id="0acb5-105">ただし、ライセンスへの同意が必要なモジュールにスクリプトが依存するシナリオはサポートされています。</span><span class="sxs-lookup"><span data-stu-id="0acb5-105">However, the scenario where a script depends on a module that requires license acceptance is supported.</span></span>

<span data-ttu-id="0acb5-106">スクリプト コマンド (Install-Script/Save-Script/Update-Script) では、ユーザーがライセンスを確認する場合と同じ動作をする新パラメーター -AcceptLicense がサポートされます。</span><span class="sxs-lookup"><span data-stu-id="0acb5-106">Script commands(Install-Script/Save-Script/Update-Script) support a new parameter -AcceptLicense that behaves as though user saw the license.</span></span> <span data-ttu-id="0acb5-107">-AcceptLicense を指定しない場合、ユーザーには依存モジュールの license.txt が示され、このライセンスに同意するように求められます。</span><span class="sxs-lookup"><span data-stu-id="0acb5-107">If -AcceptLicense is not specified; the user will be shown license.txt for dependent module and prompted to accept the license.</span></span>

## <a name="examples"></a><span data-ttu-id="0acb5-108">例</span><span class="sxs-lookup"><span data-stu-id="0acb5-108">EXAMPLES</span></span>

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="0acb5-109">例 1: ライセンスへの同意が必要な依存関係があるスクリプトをインストールする</span><span class="sxs-lookup"><span data-stu-id="0acb5-109">Example 1: Install Script with dependencies requiring license acceptance</span></span>
<span data-ttu-id="0acb5-110">スクリプト "ScriptRequireLicenseAcceptance" は、モジュール "ModuleRequireLicenseAcceptance" に依存しています。</span><span class="sxs-lookup"><span data-stu-id="0acb5-110">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="0acb5-111">ユーザーにはライセンスへの同意が求められます。</span><span class="sxs-lookup"><span data-stu-id="0acb5-111">User is prompted to Accept License.</span></span>
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance

License Acceptance
MIT License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): 
```

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="0acb5-112">例 2: -AcceptLicense を使用してライセンスへの同意が必要な依存関係があるスクリプトをインストールする</span><span class="sxs-lookup"><span data-stu-id="0acb5-112">Example 2: Install Script with dependencies requiring license acceptance and -AcceptLicense</span></span>
<span data-ttu-id="0acb5-113">スクリプト "ScriptRequireLicenseAcceptance" は、モジュール "ModuleRequireLicenseAcceptance" に依存しています。</span><span class="sxs-lookup"><span data-stu-id="0acb5-113">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="0acb5-114">-AcceptLicense を指定したため、ライセンスへの同意は求められません。</span><span class="sxs-lookup"><span data-stu-id="0acb5-114">User is not prompted to accept license as -AcceptLicense is specified.</span></span>
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a><span data-ttu-id="0acb5-115">詳細情報</span><span class="sxs-lookup"><span data-stu-id="0acb5-115">More details</span></span>
### <a name="require-license-acceptance-support-for-modulesmodulerequirelicenseacceptancemd"></a>[<span data-ttu-id="0acb5-116">モジュールに対するライセンス同意リクエストのサポート</span><span class="sxs-lookup"><span data-stu-id="0acb5-116">Require License Acceptance support for Modules</span></span>](../module/RequireLicenseAcceptance.md)

### <a name="require-license-acceptance-support-on-powershellgallerypsgallerypsgalleryrequireslicenseacceptancemd"></a>[<span data-ttu-id="0acb5-117">PowerShellGallery でのライセンス同意リクエストのサポート</span><span class="sxs-lookup"><span data-stu-id="0acb5-117">Require License Acceptance support on PowerShellGallery</span></span>](../../psgallery/psgallery_requires_license_acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationpsgallerypsgallerydeploytoazureautomationrequirelicenseacceptancemd"></a>[<span data-ttu-id="0acb5-118">Azure Automation へのデプロイで表示されるライセンス同意リクエスト</span><span class="sxs-lookup"><span data-stu-id="0acb5-118">Require License Acceptance on Deploy to Azure Automation</span></span>](../../psgallery/psgallery_deploy_to_azure_automation_requireLicenseAcceptance.md)