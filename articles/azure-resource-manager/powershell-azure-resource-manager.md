---
title: "aaaManage Azure решений с помощью PowerShell | Документы Microsoft"
description: "Используете Azure PowerShell и диспетчера ресурсов toomanage ресурсы."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="5d223-103">Управление ресурсами с помощью Azure PowerShell и Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5d223-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d223-104">Портал</span><span class="sxs-lookup"><span data-stu-id="5d223-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="5d223-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="5d223-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="5d223-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d223-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="5d223-107">REST API</span><span class="sxs-lookup"><span data-stu-id="5d223-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="5d223-108">В этой статье вы узнаете, как toomanage решений с помощью Azure PowerShell и диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5d223-108">In this article, you learn how toomanage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="5d223-109">Если вы не знакомы с Resource Manager, то см. статью [Общие сведения о диспетчере ресурсов Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5d223-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="5d223-110">Этот раздел посвящен задачам управления.</span><span class="sxs-lookup"><span data-stu-id="5d223-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="5d223-111">Вы сможете выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="5d223-111">You will:</span></span>

1. <span data-ttu-id="5d223-112">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="5d223-112">Create a resource group</span></span>
2. <span data-ttu-id="5d223-113">Добавить группу ресурсов toohello ресурсов</span><span class="sxs-lookup"><span data-stu-id="5d223-113">Add a resource toohello resource group</span></span>
3. <span data-ttu-id="5d223-114">Добавить ресурс toohello тег</span><span class="sxs-lookup"><span data-stu-id="5d223-114">Add a tag toohello resource</span></span>
4. <span data-ttu-id="5d223-115">Запрос ресурсов на основе имен или значений тегов</span><span class="sxs-lookup"><span data-stu-id="5d223-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="5d223-116">Применение и удаление блокировку ресурса hello</span><span class="sxs-lookup"><span data-stu-id="5d223-116">Apply and remove a lock on hello resource</span></span>
6. <span data-ttu-id="5d223-117">Удаление группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="5d223-117">Delete a resource group</span></span>

<span data-ttu-id="5d223-118">В этой статье не отображается как toodeploy подписки tooyour шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5d223-118">This article does not show how toodeploy a Resource Manager template tooyour subscription.</span></span> <span data-ttu-id="5d223-119">Эти сведения см. в статье [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) (Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="5d223-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="5d223-120">Начало работы с Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d223-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="5d223-121">Если вы не установили Azure PowerShell, см. раздел [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5d223-121">If you have not installed Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="5d223-122">Если установлены в прошлом hello Azure PowerShell, но не его обновил недавно, рекомендуется установить последнюю версию hello.</span><span class="sxs-lookup"><span data-stu-id="5d223-122">If you have installed Azure PowerShell in hello past but have not updated it recently, consider installing hello latest version.</span></span> <span data-ttu-id="5d223-123">Вы можете обновить версию hello через hello метод, который используется tooinstall его.</span><span class="sxs-lookup"><span data-stu-id="5d223-123">You can update hello version through hello same method you used tooinstall it.</span></span> <span data-ttu-id="5d223-124">Например если вы использовали hello Web Platform Installer, повторный запуск и найти обновление.</span><span class="sxs-lookup"><span data-stu-id="5d223-124">For example, if you used hello Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="5d223-125">использование вашей версии hello модуля ресурсы Azure toocheck hello следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="5d223-125">toocheck your version of hello Azure Resources module, use hello following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="5d223-126">Этот раздел был обновлен для версии 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="5d223-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="5d223-127">При наличии более ранней версии работы могут не соответствовать hello, описанного в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="5d223-127">If you have an earlier version, your experience might not match hello steps shown in this topic.</span></span> <span data-ttu-id="5d223-128">Документацию о командлетах hello в этой версии см. в разделе [AzureRM.Resources модуль](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="5d223-128">For documentation about hello cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="5d223-129">Войдите в tooyour учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="5d223-129">Log in tooyour Azure account</span></span>
<span data-ttu-id="5d223-130">Прежде чем начать работу над решением, необходимо войти в tooyour учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5d223-130">Before working on your solution, you must log in tooyour account.</span></span>

<span data-ttu-id="5d223-131">toolog в tooyour учетная запись Azure, используйте hello **AzureRmAccount входа** командлета.</span><span class="sxs-lookup"><span data-stu-id="5d223-131">toolog in tooyour Azure account, use hello **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="5d223-132">Hello командлет запросит hello учетные данные входа для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="5d223-132">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="5d223-133">После входа в систему, он загружает параметры учетной записи, таким образом, они будут доступны tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d223-133">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="5d223-134">Hello командлет возвращает информацию о вашей учетной записи и hello toouse подписки для задач hello.</span><span class="sxs-lookup"><span data-stu-id="5d223-134">hello cmdlet returns information about your account and hello subscription toouse for hello tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="5d223-135">Если у вас есть несколько подписок, можно переключиться tooa другую подписку.</span><span class="sxs-lookup"><span data-stu-id="5d223-135">If you have more than one subscription, you can switch tooa different subscription.</span></span> <span data-ttu-id="5d223-136">Во-первых давайте посмотрим, все подписки hello для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5d223-136">First, let's see all hello subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="5d223-137">Отобразятся включенные и отключенные подписки.</span><span class="sxs-lookup"><span data-stu-id="5d223-137">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="5d223-138">tooswitch tooa другую подписку, укажите имя подписки hello с hello **AzureRmContext набор** командлета.</span><span class="sxs-lookup"><span data-stu-id="5d223-138">tooswitch tooa different subscription, provide hello subscription name with hello **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="5d223-139">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="5d223-139">Create a resource group</span></span>
<span data-ttu-id="5d223-140">Перед развертыванием tooyour подписки на все ресурсы, необходимо создать группу ресурсов, который будет содержать ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="5d223-140">Before deploying any resources tooyour subscription, you must create a resource group that will contain hello resources.</span></span>

<span data-ttu-id="5d223-141">использовать toocreate группу ресурсов hello **New AzureRmResourceGroup** командлета.</span><span class="sxs-lookup"><span data-stu-id="5d223-141">toocreate a resource group, use hello **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="5d223-142">Команда Hello использует hello **имя** toospecify параметра имя группы ресурсов hello и hello **расположение** toospecify параметр его расположение.</span><span class="sxs-lookup"><span data-stu-id="5d223-142">hello command uses hello **Name** parameter toospecify a name for hello resource group and hello **Location** parameter toospecify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="5d223-143">Вывод Hello имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="5d223-143">hello output is in hello following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="5d223-144">Группа ресурсов tooretrieve hello позже, используйте hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="5d223-144">If you need tooretrieve hello resource group later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="5d223-145">tooget все Здравствуйте групп ресурсов в подписке, не указано имя:</span><span class="sxs-lookup"><span data-stu-id="5d223-145">tooget all hello resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a><span data-ttu-id="5d223-146">Добавить группы ресурсов tooa ресурсов</span><span class="sxs-lookup"><span data-stu-id="5d223-146">Add resources tooa resource group</span></span>
<span data-ttu-id="5d223-147">tooadd toohello ресурсов группы ресурсов, можно использовать hello **New-AzureRmResource** командлета или командлета, toohello определенного типа ресурсов создается (как **New AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="5d223-147">tooadd a resource toohello resource group, you can use hello **New-AzureRmResource** cmdlet or a cmdlet that is specific toohello type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="5d223-148">Может оказаться проще toouse командлета, так как он включает параметры для hello свойства, необходимые для нового ресурса hello tooa определенного типа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5d223-148">You might find it easier toouse a cmdlet that is specific tooa resource type because it includes parameters for hello properties that are needed for hello new resource.</span></span> <span data-ttu-id="5d223-149">toouse **New-AzureRmResource**, необходимо знать все tooset hello свойства без необходимости вводить их.</span><span class="sxs-lookup"><span data-stu-id="5d223-149">toouse **New-AzureRmResource**, you must know all hello properties tooset without being prompted for them.</span></span>

<span data-ttu-id="5d223-150">Однако добавление ресурса с помощью командлетов может ввести в заблуждение будущих поскольку hello новый ресурс не существует в шаблоне диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5d223-150">However, adding a resource through cmdlets might cause future confusion because hello new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="5d223-151">Корпорация Майкрософт рекомендует определение hello инфраструктуры Azure решения в шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5d223-151">Microsoft recommends defining hello infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="5d223-152">Шаблоны позволяют tooreliably и повторно развернуть решение.</span><span class="sxs-lookup"><span data-stu-id="5d223-152">Templates enable you tooreliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="5d223-153">В этом примере учетная запись хранения создается с помощью командлета PowerShell, но затем создается шаблон из группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5d223-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="5d223-154">Привет, выполнив командлет создает учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="5d223-154">hello following cmdlet creates a storage account.</span></span> <span data-ttu-id="5d223-155">Вместо использования имени hello, показано в примере hello, укажите уникальное имя для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="5d223-155">Instead of using hello name shown in hello example, provide a unique name for hello storage account.</span></span> <span data-ttu-id="5d223-156">Имя Hello должен находиться в диапазоне от 3 до 24 символов и содержать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="5d223-156">hello name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="5d223-157">При использовании имени hello, показано в примере hello, сообщение об ошибке, поскольку это имя уже используется.</span><span class="sxs-lookup"><span data-stu-id="5d223-157">If you use hello name shown in hello example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="5d223-158">Если вам требуется tooretrieve этот ресурс позже, используйте hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="5d223-158">If you need tooretrieve this resource later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="5d223-159">Добавление тега</span><span class="sxs-lookup"><span data-stu-id="5d223-159">Add a tag</span></span>

<span data-ttu-id="5d223-160">Теги позволяют tooorganize ресурсы в соответствии с toodifferent свойства.</span><span class="sxs-lookup"><span data-stu-id="5d223-160">Tags enable you tooorganize your resources according toodifferent properties.</span></span> <span data-ttu-id="5d223-161">Например, может иметь несколько ресурсов в разных группах ресурсов, принадлежащих toohello же отдела.</span><span class="sxs-lookup"><span data-stu-id="5d223-161">For example, you may have several resources in different resource groups that belong toohello same department.</span></span> <span data-ttu-id="5d223-162">Можно применить отдел тег и значение toothose ресурсов toomark их как принадлежащий toohello одной категории.</span><span class="sxs-lookup"><span data-stu-id="5d223-162">You can apply a department tag and value toothose resources toomark them as belonging toohello same category.</span></span> <span data-ttu-id="5d223-163">Также можно пометить, в какой среде используется ресурс — рабочей или тестовой.</span><span class="sxs-lookup"><span data-stu-id="5d223-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="5d223-164">В этом разделе применяются теги tooonly один ресурс, но в вашей среде скорее всего, имеет смысл, tooapply теги tooall свои ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5d223-164">In this topic, you apply tags tooonly one resource, but in your environment it most likely makes sense tooapply tags tooall your resources.</span></span>

<span data-ttu-id="5d223-165">Привет, выполнив командлет применяется два учетной записи хранилища tooyour теги:</span><span class="sxs-lookup"><span data-stu-id="5d223-165">hello following cmdlet applies two tags tooyour storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="5d223-166">Теги обновляются как один объект.</span><span class="sxs-lookup"><span data-stu-id="5d223-166">Tags are updated as a single object.</span></span> <span data-ttu-id="5d223-167">tooadd ресурс tooa тег, который уже включает теги, сначала получить существующие теги hello.</span><span class="sxs-lookup"><span data-stu-id="5d223-167">tooadd a tag tooa resource that already includes tags, first retrieve hello existing tags.</span></span> <span data-ttu-id="5d223-168">Добавьте hello новый тег toohello объект, содержащий существующие теги hello и повторно применить все hello теги toohello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5d223-168">Add hello new tag toohello object that contains hello existing tags, and reapply all hello tags toohello resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="5d223-169">Поиск ресурсов</span><span class="sxs-lookup"><span data-stu-id="5d223-169">Search for resources</span></span>

<span data-ttu-id="5d223-170">Используйте hello **Find-AzureRmResource** командлет tooretrieve ресурсы для поиска различных условий.</span><span class="sxs-lookup"><span data-stu-id="5d223-170">Use hello **Find-AzureRmResource** cmdlet tooretrieve resources for different search conditions.</span></span>

* <span data-ttu-id="5d223-171">tooget ресурсов по имени, предоставляют hello **ResourceNameContains** параметр:</span><span class="sxs-lookup"><span data-stu-id="5d223-171">tooget a resource by name, provide hello **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="5d223-172">tooget все ресурсы hello в группе ресурсов обеспечивают hello **ResourceGroupNameContains** параметр:</span><span class="sxs-lookup"><span data-stu-id="5d223-172">tooget all hello resources in a resource group, provide hello **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="5d223-173">tooget все ресурсы hello имя тега и значением, обеспечивают hello **TagName** и **TagValue** параметры:</span><span class="sxs-lookup"><span data-stu-id="5d223-173">tooget all hello resources with a tag name and value, provide hello **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="5d223-174">ресурсы hello tooall с определенного типа ресурсов, обеспечивают hello **ResourceType** параметр:</span><span class="sxs-lookup"><span data-stu-id="5d223-174">tooall hello resources with a particular resource type, provide hello **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="5d223-175">Блокировка ресурса</span><span class="sxs-lookup"><span data-stu-id="5d223-175">Lock a resource</span></span>

<span data-ttu-id="5d223-176">Когда требуется toomake убедитесь, что важный ресурс не удаляется случайно или изменены, применение toohello ресурса блокировки.</span><span class="sxs-lookup"><span data-stu-id="5d223-176">When you need toomake sure a critical resource is not accidentally deleted or modified, apply a lock toohello resource.</span></span> <span data-ttu-id="5d223-177">Можно указать параметр **CanNotDelete** или **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="5d223-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="5d223-178">блокировки управления toocreate или delete, необходимо иметь доступ слишком`Microsoft.Authorization/*` или `Microsoft.Authorization/locks/*` действия.</span><span class="sxs-lookup"><span data-stu-id="5d223-178">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="5d223-179">Hello встроенных ролей эти действия предоставляются только владелец и администратор доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="5d223-179">Of hello built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="5d223-180">tooapply блокировку, используйте следующий командлет hello:</span><span class="sxs-lookup"><span data-stu-id="5d223-180">tooapply a lock, use hello following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="5d223-181">Hello ресурс блокировки в предшествующих пример hello нельзя удалить, пока блокировка hello удаляется.</span><span class="sxs-lookup"><span data-stu-id="5d223-181">hello locked resource in hello preceding example cannot be deleted until hello lock is removed.</span></span> <span data-ttu-id="5d223-182">tooremove блокировку, используйте:</span><span class="sxs-lookup"><span data-stu-id="5d223-182">tooremove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="5d223-183">Дополнительные сведения об установке блокировок см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="5d223-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="5d223-184">Удаление ресурсов или группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="5d223-184">Remove resources or resource group</span></span>
<span data-ttu-id="5d223-185">Ресурс или группу ресурсов можно удалить.</span><span class="sxs-lookup"><span data-stu-id="5d223-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="5d223-186">При удалении группы ресурсов, также удалить все ресурсы hello в пределах этой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5d223-186">When you remove a resource group, you also remove all hello resources within that resource group.</span></span>

* <span data-ttu-id="5d223-187">ресурс из группы ресурсов hello, используйте hello toodelete **Remove-AzureRmResource** командлета.</span><span class="sxs-lookup"><span data-stu-id="5d223-187">toodelete a resource from hello resource group, use hello **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="5d223-188">Этот командлет удаляет hello ресурсов, но не удаляет группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="5d223-188">This cmdlet deletes hello resource, but does not delete hello resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="5d223-189">toodelete группу ресурсов и его ресурсы используют hello **AzureRmResourceGroup удаление** командлета.</span><span class="sxs-lookup"><span data-stu-id="5d223-189">toodelete a resource group and all its resources, use hello **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="5d223-190">Для обоих командлетов предлагают tooconfirm нужно tooremove hello ресурс или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5d223-190">For both cmdlets, you are asked tooconfirm that you wish tooremove hello resource or resource group.</span></span> <span data-ttu-id="5d223-191">Если операция hello успешно удаляет hello ресурс или группа ресурсов, он возвращает **True**.</span><span class="sxs-lookup"><span data-stu-id="5d223-191">If hello operation successfully deletes hello resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="5d223-192">Выполнение сценариев Resource Manager со службой автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5d223-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="5d223-193">В этом разделе показано, как tooperform основных операций на ресурсы с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d223-193">This topic shows you how tooperform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="5d223-194">Для более сложных сценариев управления обычно требуется toocreate сценария и повторно использовать этот скрипт, при необходимости, или по расписанию.</span><span class="sxs-lookup"><span data-stu-id="5d223-194">For more advanced management scenarios, you typically want toocreate a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="5d223-195">[Служба автоматизации Azure](../automation/automation-intro.md) предоставляет способ для вас tooautomate распространенные сценарии, управляющие решений Azure.</span><span class="sxs-lookup"><span data-stu-id="5d223-195">[Azure Automation](../automation/automation-intro.md) provides a way for you tooautomate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="5d223-196">Hello следующих разделах показано, как выполнять задачи управления toouse автоматизации Azure, диспетчер ресурсов и PowerShell tooeffectively:</span><span class="sxs-lookup"><span data-stu-id="5d223-196">hello following topics show you how toouse Azure Automation, Resource Manager, and PowerShell tooeffectively perform management tasks:</span></span>

- <span data-ttu-id="5d223-197">Сведения о создании модулей Runbook см. в статье [Мой первый модуль Runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5d223-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="5d223-198">Сведения о работе с галереями сценариев см. в статье [Коллекции модулей Runbook и других модулей для службы автоматизации Azure](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="5d223-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="5d223-199">Модули Runbook, запускать и останавливать виртуальные машины, в разделе [сценарий автоматизации Azure: toocreate формата JSON с помощью тегов расписание для включения и выключения виртуальной Машины Azure](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="5d223-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="5d223-200">Сведения о модулях Runbook, запускающих и останавливающих виртуальные машины в нерабочее время, см. в статье [Решение для запуска и остановки виртуальных машин в нерабочее время [предварительная версия] в службе автоматизации](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="5d223-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d223-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5d223-201">Next steps</span></span>
* <span data-ttu-id="5d223-202">в разделе toolearn о создании шаблонов диспетчера ресурсов [разработки шаблоны Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5d223-202">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="5d223-203">в разделе toolearn о развертывании шаблонов, [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5d223-203">toolearn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="5d223-204">Можно переместить существующие ресурсы tooa новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5d223-204">You can move existing resources tooa new resource group.</span></span> <span data-ttu-id="5d223-205">Примеры см. в разделе [tooNew перемещение ресурсов группы ресурсов или подписку](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="5d223-205">For examples, see [Move Resources tooNew Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="5d223-206">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="5d223-206">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

