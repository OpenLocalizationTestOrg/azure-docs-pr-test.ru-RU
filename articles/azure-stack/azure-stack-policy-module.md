---
title: "hello aaaUse модуля политики стек Azure | Документы Microsoft"
description: "Узнайте, как подписка Azure стека tooconstrain toobehave подписки Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 937ef34f-14d4-4ea9-960b-362ba986f000
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/28/2017
ms.author: helaw
ms.openlocfilehash: a9d01b759d7c4a248f727de682a71a7655ed12d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-policy-using-hello-azure-stack-policy-module"></a><span data-ttu-id="89c50-103">Управление Azure политикой, с помощью hello модуля политики стек Azure</span><span class="sxs-lookup"><span data-stu-id="89c50-103">Manage Azure policy using hello Azure Stack Policy Module</span></span>
<span data-ttu-id="89c50-104">модуль политики стек Azure Hello позволяет tooconfigure подписку Azure с hello же управления версиями и доступность службы как стек Azure.</span><span class="sxs-lookup"><span data-stu-id="89c50-104">hello Azure Stack Policy module allows you tooconfigure an Azure subscription with hello same versioning and service availability as Azure Stack.</span></span>  <span data-ttu-id="89c50-105">модуль Hello использует hello **New AzureRMPolicyAssignment** toocreate командлет политику Azure, которая ограничивает типы ресурсов hello и служб, доступных по подписке.</span><span class="sxs-lookup"><span data-stu-id="89c50-105">hello module uses hello **New-AzureRMPolicyAssignment** cmdlet toocreate an Azure policy, which limits hello resource types and services available in a subscription.</span></span>  <span data-ttu-id="89c50-106">После завершения можно использовать приложения toodevelop подписки Azure для Azure стека.</span><span class="sxs-lookup"><span data-stu-id="89c50-106">Once complete, you can use your Azure subscription toodevelop apps targeted for Azure Stack.</span></span>  

## <a name="install-hello-module"></a><span data-ttu-id="89c50-107">Установка модуля hello</span><span class="sxs-lookup"><span data-stu-id="89c50-107">Install hello module</span></span>
1. <span data-ttu-id="89c50-108">Установите необходимую версию hello hello модуль AzureRM PowerShell, как описано в шаг 1 из [Установка PowerShell для Azure стека](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="89c50-108">Install hello required version of hello AzureRM PowerShell module, as described in Step1 of [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>   
2. [<span data-ttu-id="89c50-109">Загрузить набор средств Azure стека hello из GitHub</span><span class="sxs-lookup"><span data-stu-id="89c50-109">Download hello Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)  
3. <span data-ttu-id="89c50-110">[Configure PowerShell for use with Azure Stack](azure-stack-powershell-configure-user.md) (Настройка PowerShell для использования с Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="89c50-110">[Configure PowerShell for use with Azure Stack](azure-stack-powershell-configure-user.md)</span></span>

4. <span data-ttu-id="89c50-111">Импорт модуля AzureStack.Policy.psm1 hello:</span><span class="sxs-lookup"><span data-stu-id="89c50-111">Import hello AzureStack.Policy.psm1 module:</span></span>

   ```PowerShell
   Import-Module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-toosubscription"></a><span data-ttu-id="89c50-112">Применить политику toosubscription</span><span class="sxs-lookup"><span data-stu-id="89c50-112">Apply policy toosubscription</span></span>
<span data-ttu-id="89c50-113">Hello следующую команду можно использовать tooapply политику по умолчанию стек Azure к подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="89c50-113">hello following command can be used tooapply a default Azure Stack policy against your Azure subscription.</span></span> <span data-ttu-id="89c50-114">Перед запуском, замените *имя подписки Azure* с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="89c50-114">Before running, replace *Azure Subscription Name* with your Azure subscription.</span></span>

```PowerShell
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
$rgName = 'AzureStack'
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-tooa-resource-group"></a><span data-ttu-id="89c50-115">Группа ресурсов tooa политики применения</span><span class="sxs-lookup"><span data-stu-id="89c50-115">Apply policy tooa resource group</span></span>
<span data-ttu-id="89c50-116">Вы можете tooapply политик в более детального метод.</span><span class="sxs-lookup"><span data-stu-id="89c50-116">You may want tooapply policies in a more granular method.</span></span>  <span data-ttu-id="89c50-117">Например, возможно, других ресурсов, выполняемых в hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="89c50-117">As an example, you may have other resources running in hello same subscription.</span></span>  <span data-ttu-id="89c50-118">Вы можете задать область hello политики приложения tooa определенной группы ресурсов, используемое для тестирования приложений для Azure стека с помощью ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="89c50-118">You can scope hello policy application tooa specific resource group, which lets you test your apps for Azure Stack using Azure resources.</span></span> <span data-ttu-id="89c50-119">Перед запуском, замените *имя подписки Azure* именем своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="89c50-119">Before running, replace *Azure Subscription Name* with your Azure subscription name.</span></span>

```PowerShell
$resourceGroupName = ‘myRG01’
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a><span data-ttu-id="89c50-120">Политика в действии</span><span class="sxs-lookup"><span data-stu-id="89c50-120">Policy in action</span></span>
<span data-ttu-id="89c50-121">После развертывания hello Azure политики, возникает ошибка при попытке toodeploy ресурс, который запрещено политикой.</span><span class="sxs-lookup"><span data-stu-id="89c50-121">Once you've deployed hello Azure policy, you receive an error when you try toodeploy a resource that prohibited by policy.</span></span>  

![Результат сбоя развертывания ресурсов из-за ограничений политики](./media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a><span data-ttu-id="89c50-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89c50-123">Next steps</span></span>
[<span data-ttu-id="89c50-124">Развертывание шаблонов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="89c50-124">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)

[<span data-ttu-id="89c50-125">Развертывание шаблонов с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="89c50-125">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="89c50-126">Развертывание шаблонов с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89c50-126">Deploy Templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)
