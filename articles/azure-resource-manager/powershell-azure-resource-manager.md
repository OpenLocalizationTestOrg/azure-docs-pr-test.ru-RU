---
title: "Управление решениями Azure с помощью PowerShell | Документация Майкрософт"
description: "Воспользуйтесь Azure PowerShell и Resource Manager для управления ресурсами."
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
ms.openlocfilehash: ff42e5cb29005c5f4b97babdae58bef9382071f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="7fa57-103">Управление ресурсами с помощью Azure PowerShell и Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7fa57-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7fa57-104">Портал</span><span class="sxs-lookup"><span data-stu-id="7fa57-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="7fa57-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="7fa57-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="7fa57-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fa57-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="7fa57-107">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="7fa57-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="7fa57-108">В этой статье вы узнаете, как управлять решениями с помощью Azure PowerShell и Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7fa57-108">In this article, you learn how to manage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="7fa57-109">Если вы не знакомы с Resource Manager, то см. статью [Общие сведения о диспетчере ресурсов Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7fa57-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="7fa57-110">Этот раздел посвящен задачам управления.</span><span class="sxs-lookup"><span data-stu-id="7fa57-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="7fa57-111">Вы сможете выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="7fa57-111">You will:</span></span>

1. <span data-ttu-id="7fa57-112">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="7fa57-112">Create a resource group</span></span>
2. <span data-ttu-id="7fa57-113">Добавление ресурса в группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="7fa57-113">Add a resource to the resource group</span></span>
3. <span data-ttu-id="7fa57-114">Добавление тега к ресурсу</span><span class="sxs-lookup"><span data-stu-id="7fa57-114">Add a tag to the resource</span></span>
4. <span data-ttu-id="7fa57-115">Запрос ресурсов на основе имен или значений тегов</span><span class="sxs-lookup"><span data-stu-id="7fa57-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="7fa57-116">Применение и удаление блокировки ресурса</span><span class="sxs-lookup"><span data-stu-id="7fa57-116">Apply and remove a lock on the resource</span></span>
6. <span data-ttu-id="7fa57-117">Удаление группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="7fa57-117">Delete a resource group</span></span>

<span data-ttu-id="7fa57-118">В этой статье не показан процесс развертывания в подписке шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7fa57-118">This article does not show how to deploy a Resource Manager template to your subscription.</span></span> <span data-ttu-id="7fa57-119">Эти сведения см. в статье [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) (Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="7fa57-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="7fa57-120">Начало работы с Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fa57-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="7fa57-121">Если вы еще не установили Azure PowerShell, то см. статью [Get started with Azure PowerShell cmdlets](/powershell/azure/overview) (Приступая к работе с командлетами Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="7fa57-121">If you have not installed Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="7fa57-122">Если вы уже установили Azure PowerShell, но давно не выполняли обновление, то рекомендуется установить последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="7fa57-122">If you have installed Azure PowerShell in the past but have not updated it recently, consider installing the latest version.</span></span> <span data-ttu-id="7fa57-123">Обновить версию можно тем же методом, что применялся для ее установки.</span><span class="sxs-lookup"><span data-stu-id="7fa57-123">You can update the version through the same method you used to install it.</span></span> <span data-ttu-id="7fa57-124">Например, если вы использовали установщик веб-платформы, то запустите его снова и выберите параметр "Обновить".</span><span class="sxs-lookup"><span data-stu-id="7fa57-124">For example, if you used the Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="7fa57-125">Для проверки версии модуля ресурсов Azure воспользуйтесь следующим командлетом:</span><span class="sxs-lookup"><span data-stu-id="7fa57-125">To check your version of the Azure Resources module, use the following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="7fa57-126">Этот раздел был обновлен для версии 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="7fa57-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="7fa57-127">Если у вас установлена более ранняя версия, то выполняемые действия могут отличаться от шагов, описанных в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="7fa57-127">If you have an earlier version, your experience might not match the steps shown in this topic.</span></span> <span data-ttu-id="7fa57-128">Документация по командлетам, используемым в этой версии, доступна в [модуле AzureRM.Resources](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="7fa57-128">For documentation about the cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-to-your-azure-account"></a><span data-ttu-id="7fa57-129">Вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="7fa57-129">Log in to your Azure account</span></span>
<span data-ttu-id="7fa57-130">Прежде чем начать работу над решением, необходимо войти в учетную запись.</span><span class="sxs-lookup"><span data-stu-id="7fa57-130">Before working on your solution, you must log in to your account.</span></span>

<span data-ttu-id="7fa57-131">Чтобы войти в учетную запись Azure, используйте командлет **Login-AzureRmAccount**.</span><span class="sxs-lookup"><span data-stu-id="7fa57-131">To log in to your Azure account, use the **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="7fa57-132">Командлет запрашивает учетные данные входа для вашей учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="7fa57-132">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="7fa57-133">После выполнения входа он загружает параметры учетной записи, чтобы они были доступны в Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7fa57-133">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="7fa57-134">Командлет возвращает сведения об учетной записи и подписке, которые используются для выполнения задач.</span><span class="sxs-lookup"><span data-stu-id="7fa57-134">The cmdlet returns information about your account and the subscription to use for the tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="7fa57-135">При наличии нескольких подписок можно переключаться с одной подписки на другую.</span><span class="sxs-lookup"><span data-stu-id="7fa57-135">If you have more than one subscription, you can switch to a different subscription.</span></span> <span data-ttu-id="7fa57-136">Для начала давайте просмотрим все подписки для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="7fa57-136">First, let's see all the subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="7fa57-137">Отобразятся включенные и отключенные подписки.</span><span class="sxs-lookup"><span data-stu-id="7fa57-137">It returns enabled and disabled subscriptions.</span></span>

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

<span data-ttu-id="7fa57-138">Чтобы переключиться на другую подписку, укажите имя подписки с помощью командлета **Set-AzureRmContext**.</span><span class="sxs-lookup"><span data-stu-id="7fa57-138">To switch to a different subscription, provide the subscription name with the **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="7fa57-139">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="7fa57-139">Create a resource group</span></span>
<span data-ttu-id="7fa57-140">Прежде чем развертывать ресурсы в подписке, необходимо создать группу ресурсов, которая будет их содержать.</span><span class="sxs-lookup"><span data-stu-id="7fa57-140">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span></span>

<span data-ttu-id="7fa57-141">Чтобы создать группу ресурсов, используйте командлет **New-AzureRmResourceGroup** .</span><span class="sxs-lookup"><span data-stu-id="7fa57-141">To create a resource group, use the **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="7fa57-142">В команде используются параметр **Name** для указания имени группы ресурсов и параметр **Location** для указания ее расположения.</span><span class="sxs-lookup"><span data-stu-id="7fa57-142">The command uses the **Name** parameter to specify a name for the resource group and the **Location** parameter to specify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="7fa57-143">Выходные данные имеют следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7fa57-143">The output is in the following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="7fa57-144">Чтобы получить сведения о группе ресурсов, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="7fa57-144">If you need to retrieve the resource group later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="7fa57-145">Чтобы просмотреть все группы ресурсов в подписке, не указывайте имя:</span><span class="sxs-lookup"><span data-stu-id="7fa57-145">To get all the resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-to-a-resource-group"></a><span data-ttu-id="7fa57-146">Добавление ресурсов в группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="7fa57-146">Add resources to a resource group</span></span>
<span data-ttu-id="7fa57-147">Чтобы добавить ресурс в группу ресурсов, можно использовать командлет **New-AzureRmResource** или командлет для конкретного типа создаваемого ресурса (например **New-AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="7fa57-147">To add a resource to the resource group, you can use the **New-AzureRmResource** cmdlet or a cmdlet that is specific to the type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="7fa57-148">Возможно, проще использовать командлет для конкретного типа ресурса, так как он включает в себя параметры для свойств, которые необходимы для нового ресурса.</span><span class="sxs-lookup"><span data-stu-id="7fa57-148">You might find it easier to use a cmdlet that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span></span> <span data-ttu-id="7fa57-149">Чтобы использовать командлет **New-AzureRmResource**, необходимо знать все свойства и ввести их без запроса.</span><span class="sxs-lookup"><span data-stu-id="7fa57-149">To use **New-AzureRmResource**, you must know all the properties to set without being prompted for them.</span></span>

<span data-ttu-id="7fa57-150">Однако добавление ресурса с помощью командлетов может привести к путанице в будущем, потому что новый ресурс не существует в шаблоне Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7fa57-150">However, adding a resource through cmdlets might cause future confusion because the new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="7fa57-151">Корпорация Майкрософт рекомендует определять инфраструктуру решения Azure в шаблоне Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7fa57-151">Microsoft recommends defining the infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="7fa57-152">Шаблоны обеспечивают надежность развертывания и позволяют развернуть решение повторно.</span><span class="sxs-lookup"><span data-stu-id="7fa57-152">Templates enable you to reliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="7fa57-153">В этом примере учетная запись хранения создается с помощью командлета PowerShell, но затем создается шаблон из группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7fa57-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="7fa57-154">Следующий командлет создает учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="7fa57-154">The following cmdlet creates a storage account.</span></span> <span data-ttu-id="7fa57-155">Вместо имени, использованного в примере, укажите уникальное имя для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7fa57-155">Instead of using the name shown in the example, provide a unique name for the storage account.</span></span> <span data-ttu-id="7fa57-156">Это имя должно содержать от 3 до 24 знаков и состоять только из цифр и букв нижнего регистра.</span><span class="sxs-lookup"><span data-stu-id="7fa57-156">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="7fa57-157">При использовании имени из примера возникнет ошибка, так как это имя уже используется.</span><span class="sxs-lookup"><span data-stu-id="7fa57-157">If you use the name shown in the example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="7fa57-158">Чтобы получить сведения об этом ресурсе, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="7fa57-158">If you need to retrieve this resource later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="7fa57-159">Добавление тега</span><span class="sxs-lookup"><span data-stu-id="7fa57-159">Add a tag</span></span>

<span data-ttu-id="7fa57-160">Теги позволяют организовать ресурсы в соответствии с различными свойствами.</span><span class="sxs-lookup"><span data-stu-id="7fa57-160">Tags enable you to organize your resources according to different properties.</span></span> <span data-ttu-id="7fa57-161">Например, в разных группах ресурсов могут находиться ресурсы, относящиеся к одному отделу.</span><span class="sxs-lookup"><span data-stu-id="7fa57-161">For example, you may have several resources in different resource groups that belong to the same department.</span></span> <span data-ttu-id="7fa57-162">Чтобы пометить ресурсы как относящиеся к одной категории, к ним можно применить тег отдела и значение.</span><span class="sxs-lookup"><span data-stu-id="7fa57-162">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span></span> <span data-ttu-id="7fa57-163">Также можно пометить, в какой среде используется ресурс — рабочей или тестовой.</span><span class="sxs-lookup"><span data-stu-id="7fa57-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="7fa57-164">В этом примере теги применяются только к одному ресурсу, но в вашей среде, скорее всего, имеет смысл применить теги ко всем ресурсам.</span><span class="sxs-lookup"><span data-stu-id="7fa57-164">In this topic, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span></span>

<span data-ttu-id="7fa57-165">Следующий командлет применяет к учетной записи хранения два тега:</span><span class="sxs-lookup"><span data-stu-id="7fa57-165">The following cmdlet applies two tags to your storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="7fa57-166">Теги обновляются как один объект.</span><span class="sxs-lookup"><span data-stu-id="7fa57-166">Tags are updated as a single object.</span></span> <span data-ttu-id="7fa57-167">Для добавления тега к ресурсу, который уже содержит теги, сначала получите сведения о существующих тегах.</span><span class="sxs-lookup"><span data-stu-id="7fa57-167">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span></span> <span data-ttu-id="7fa57-168">Добавьте новый тег в объект, содержащий существующие теги, а затем повторно примените к ресурсу все теги.</span><span class="sxs-lookup"><span data-stu-id="7fa57-168">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="7fa57-169">Поиск ресурсов</span><span class="sxs-lookup"><span data-stu-id="7fa57-169">Search for resources</span></span>

<span data-ttu-id="7fa57-170">Используйте командлет **Find-AzureRmResource**, чтобы получить сведения о ресурсах для разных условий поиска.</span><span class="sxs-lookup"><span data-stu-id="7fa57-170">Use the **Find-AzureRmResource** cmdlet to retrieve resources for different search conditions.</span></span>

* <span data-ttu-id="7fa57-171">Чтобы найти ресурс по имени, укажите параметр **ResourceNameContains**:</span><span class="sxs-lookup"><span data-stu-id="7fa57-171">To get a resource by name, provide the **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="7fa57-172">Чтобы получить сведения о всех ресурсах в группе ресурсов, укажите параметр **ResourceGroupNameContains**:</span><span class="sxs-lookup"><span data-stu-id="7fa57-172">To get all the resources in a resource group, provide the **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="7fa57-173">Для получения сведений о всех ресурсах с именем и значением тега, укажите параметры **TagName** и **TagValue**:</span><span class="sxs-lookup"><span data-stu-id="7fa57-173">To get all the resources with a tag name and value, provide the **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="7fa57-174">Для всех ресурсов с определенным типом ресурса укажите параметр **ResourceType**:</span><span class="sxs-lookup"><span data-stu-id="7fa57-174">To all the resources with a particular resource type, provide the **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="7fa57-175">Блокировка ресурса</span><span class="sxs-lookup"><span data-stu-id="7fa57-175">Lock a resource</span></span>

<span data-ttu-id="7fa57-176">Чтобы гарантировать, что критически важный ресурс не будет случайно удален или изменен, примените к нему блокировку ресурса.</span><span class="sxs-lookup"><span data-stu-id="7fa57-176">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span></span> <span data-ttu-id="7fa57-177">Можно указать параметр **CanNotDelete** или **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="7fa57-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="7fa57-178">Для создания или удаления блокировок управления необходим доступ к действию `Microsoft.Authorization/*` или `Microsoft.Authorization/locks/*`.</span><span class="sxs-lookup"><span data-stu-id="7fa57-178">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="7fa57-179">Из встроенных ролей эти действия предоставляются только владельцу и администратору доступа пользователей.</span><span class="sxs-lookup"><span data-stu-id="7fa57-179">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="7fa57-180">Чтобы применить блокировку, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="7fa57-180">To apply a lock, use the following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="7fa57-181">Заблокированный ресурс в предыдущем примере невозможно удалить, пока не будет снята блокировка.</span><span class="sxs-lookup"><span data-stu-id="7fa57-181">The locked resource in the preceding example cannot be deleted until the lock is removed.</span></span> <span data-ttu-id="7fa57-182">Для снятия блокировки используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="7fa57-182">To remove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="7fa57-183">Дополнительные сведения об установке блокировок см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7fa57-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="7fa57-184">Удаление ресурсов или группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="7fa57-184">Remove resources or resource group</span></span>
<span data-ttu-id="7fa57-185">Ресурс или группу ресурсов можно удалить.</span><span class="sxs-lookup"><span data-stu-id="7fa57-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="7fa57-186">При удалении группы ресурсов также удаляются все ресурсы, входящие в эту группу.</span><span class="sxs-lookup"><span data-stu-id="7fa57-186">When you remove a resource group, you also remove all the resources within that resource group.</span></span>

* <span data-ttu-id="7fa57-187">Чтобы удалить ресурс из группы ресурсов, используйте командлет **Remove-AzureRmResource** .</span><span class="sxs-lookup"><span data-stu-id="7fa57-187">To delete a resource from the resource group, use the **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="7fa57-188">Этот командлет удаляет ресурс, но не удаляет группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7fa57-188">This cmdlet deletes the resource, but does not delete the resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="7fa57-189">Чтобы удалить группу ресурсов со всем ее содержимым, используйте командлет **Remove-AzureRmResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="7fa57-189">To delete a resource group and all its resources, use the **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="7fa57-190">В обоих командлетах требуется подтвердить, что вы хотите удалить ресурс или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7fa57-190">For both cmdlets, you are asked to confirm that you wish to remove the resource or resource group.</span></span> <span data-ttu-id="7fa57-191">В случае успешного выполнения операции командлет возвращает значение **True**.</span><span class="sxs-lookup"><span data-stu-id="7fa57-191">If the operation successfully deletes the resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="7fa57-192">Выполнение сценариев Resource Manager со службой автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="7fa57-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="7fa57-193">В этом разделе показано, как выполнять базовые операции с ресурсами, используя Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7fa57-193">This topic shows you how to perform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="7fa57-194">Для расширенного управления обычно требуется создать сценарий, который затем применяется при необходимости или по расписанию.</span><span class="sxs-lookup"><span data-stu-id="7fa57-194">For more advanced management scenarios, you typically want to create a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="7fa57-195">[Служба автоматизации Azure](../automation/automation-intro.md) предоставляет возможность автоматизации часто используемых сценариев, которые управляют решениями Azure.</span><span class="sxs-lookup"><span data-stu-id="7fa57-195">[Azure Automation](../automation/automation-intro.md) provides a way for you to automate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="7fa57-196">Ниже приведены статьи, в которых показано использование службы автоматизации Azure, Resource Manager и PowerShell для эффективного выполнения задач управления.</span><span class="sxs-lookup"><span data-stu-id="7fa57-196">The following topics show you how to use Azure Automation, Resource Manager, and PowerShell to effectively perform management tasks:</span></span>

- <span data-ttu-id="7fa57-197">Сведения о создании модулей Runbook см. в статье [Мой первый модуль Runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7fa57-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="7fa57-198">Сведения о работе с галереями сценариев см. в статье [Коллекции модулей Runbook и других модулей для службы автоматизации Azure](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="7fa57-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="7fa57-199">Сведения о модулях Runbook, запускающих и останавливающих виртуальные машины, см. в статье [Сценарий службы автоматизации Azure: создание расписания запуска и завершения работы виртуальной машины Azure с помощью тегов в формате JSON](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="7fa57-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="7fa57-200">Сведения о модулях Runbook, запускающих и останавливающих виртуальные машины в нерабочее время, см. в статье [Решение для запуска и остановки виртуальных машин в нерабочее время [предварительная версия] в службе автоматизации](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="7fa57-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fa57-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7fa57-201">Next steps</span></span>
* <span data-ttu-id="7fa57-202">Сведения о создании шаблонов Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7fa57-202">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7fa57-203">Сведения о развертывании шаблонов см. в статье [Развертывание приложения с использованием шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7fa57-203">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="7fa57-204">Существующие ресурсы можно переместить в новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7fa57-204">You can move existing resources to a new resource group.</span></span> <span data-ttu-id="7fa57-205">Примеры см. в статье [Перемещение ресурсов в новую группу ресурсов или подписку](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7fa57-205">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="7fa57-206">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="7fa57-206">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

