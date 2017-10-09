---
title: "изменения tooprevent aaaLock ресурсы Azure | Документы Microsoft"
description: "Запрет на обновление или удаление критических ресурсов Azure для пользователей путем применения блокировки для всех пользователей и ролей."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a><span data-ttu-id="47e2c-103">Заблокировать tooprevent ресурсы непредвиденные изменения</span><span class="sxs-lookup"><span data-stu-id="47e2c-103">Lock resources tooprevent unexpected changes</span></span> 
<span data-ttu-id="47e2c-104">С правами администратора может потребоваться toolock подписки, группы ресурсов или ресурсов tooprevent другим пользователям в организации от случайного удаления или изменения критическим ресурсам.</span><span class="sxs-lookup"><span data-stu-id="47e2c-104">As an administrator, you may need toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="47e2c-105">Можно задать уровень блокировки hello слишком**CanNotDelete** или **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="47e2c-105">You can set hello lock level too**CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="47e2c-106">**CanNotDelete** означает авторизованные пользователи по-прежнему можно считывать и изменять ресурс, но они не могут удалить ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="47e2c-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete hello resource.</span></span> 
* <span data-ttu-id="47e2c-107">**Только для чтения** означает авторизованные пользователи могут читать ресурс, но их нельзя удалить или обновить ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="47e2c-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update hello resource.</span></span> <span data-ttu-id="47e2c-108">Применение этой блокировкой — примерно toorestricting всех авторизованных пользователей toohello разрешения, предоставляемые hello **чтения** роли.</span><span class="sxs-lookup"><span data-stu-id="47e2c-108">Applying this lock is similar toorestricting all authorized users toohello permissions granted by hello **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="47e2c-109">Применение блокировок</span><span class="sxs-lookup"><span data-stu-id="47e2c-109">How locks are applied</span></span>

<span data-ttu-id="47e2c-110">При применении блокировки в родительской области всех ресурсов в этой области наследуют hello же блокировку.</span><span class="sxs-lookup"><span data-stu-id="47e2c-110">When you apply a lock at a parent scope, all resources within that scope inherit hello same lock.</span></span> <span data-ttu-id="47e2c-111">Даже ресурсы, которые позже можно добавить блокировки hello наследовать родительской hello.</span><span class="sxs-lookup"><span data-stu-id="47e2c-111">Even resources you add later inherit hello lock from hello parent.</span></span> <span data-ttu-id="47e2c-112">наиболее строгие блокировки Hello в наследовании hello имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="47e2c-112">hello most restrictive lock in hello inheritance takes precedence.</span></span>

<span data-ttu-id="47e2c-113">В отличие от управления доступом на основе ролей используйте tooapply блокировки управления ограничение для всех пользователей и ролей.</span><span class="sxs-lookup"><span data-stu-id="47e2c-113">Unlike role-based access control, you use management locks tooapply a restriction across all users and roles.</span></span> <span data-ttu-id="47e2c-114">toolearn о предоставлении разрешений пользователям и ролям, в разделе [управления доступом на основе ролей Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="47e2c-114">toolearn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="47e2c-115">Диспетчер ресурсов блокировка применяется только toooperations возможно в плоскости управления hello, который состоит из операции, отправленные слишком`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="47e2c-115">Resource Manager locks apply only toooperations that happen in hello management plane, which consists of operations sent too`https://management.azure.com`.</span></span> <span data-ttu-id="47e2c-116">Hello блокировки не ограничивают как ресурсы выполнять свои функции.</span><span class="sxs-lookup"><span data-stu-id="47e2c-116">hello locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="47e2c-117">Ограничиваются изменения ресурсов, но не операции с ними.</span><span class="sxs-lookup"><span data-stu-id="47e2c-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="47e2c-118">Например блокировку только для чтения для базы данных SQL предотвращает удаление или изменение hello базы данных, но он не препятствуют создание, обновление или удаление данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="47e2c-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying hello database, but it does not prevent you from creating, updating, or deleting data in hello database.</span></span> <span data-ttu-id="47e2c-119">Данные транзакций разрешены, так как эти операции не отправляются слишком`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="47e2c-119">Data transactions are permitted because those operations are not sent too`https://management.azure.com`.</span></span>

<span data-ttu-id="47e2c-120">Применение **ReadOnly** может привести toounexpected результатов, так как некоторые операции могут показаться чтения операции фактически требуют дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="47e2c-120">Applying **ReadOnly** can lead toounexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="47e2c-121">Например, поместив **ReadOnly** блокировку учетной записи хранилища запрещает всем пользователям со списком ключей hello.</span><span class="sxs-lookup"><span data-stu-id="47e2c-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing hello keys.</span></span> <span data-ttu-id="47e2c-122">Список Hello ключи операция обрабатывается с помощью запроса POST, поскольку hello вернул ключи будут доступны для операций записи.</span><span class="sxs-lookup"><span data-stu-id="47e2c-122">hello list keys operation is handled through a POST request because hello returned keys are available for write operations.</span></span> <span data-ttu-id="47e2c-123">Еще один пример размещения **ReadOnly** блокировка на ресурс приложения службы предотвращает отображение файлов для ресурсов hello, так как для этого диалога требуется доступ на запись обозревателя серверов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="47e2c-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for hello resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="47e2c-124">Кто может создавать и удалять блокировки в вашей организации</span><span class="sxs-lookup"><span data-stu-id="47e2c-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="47e2c-125">блокировки управления toocreate или delete, необходимо иметь доступ слишком`Microsoft.Authorization/*` или `Microsoft.Authorization/locks/*` действия.</span><span class="sxs-lookup"><span data-stu-id="47e2c-125">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="47e2c-126">Hello встроенных ролей, только **владельца** и **администратор доступа пользователя** предоставляются эти действия.</span><span class="sxs-lookup"><span data-stu-id="47e2c-126">Of hello built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="47e2c-127">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="47e2c-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="47e2c-128">Шаблон</span><span class="sxs-lookup"><span data-stu-id="47e2c-128">Template</span></span>
<span data-ttu-id="47e2c-129">Hello примере показан шаблон, который создает блокировку для учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="47e2c-129">hello following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="47e2c-130">на какие tooapply блокировки hello предоставляется как параметр учетной записи хранилища Hello.</span><span class="sxs-lookup"><span data-stu-id="47e2c-130">hello storage account on which tooapply hello lock is provided as a parameter.</span></span> <span data-ttu-id="47e2c-131">Hello имя hello блокировок создается путем объединения hello имя ресурса с **/Microsoft.Authorization/** и в этом случае hello имя блокировки hello **myLock**.</span><span class="sxs-lookup"><span data-stu-id="47e2c-131">hello name of hello lock is created by concatenating hello resource name with **/Microsoft.Authorization/** and hello name of hello lock, in this case **myLock**.</span></span>

<span data-ttu-id="47e2c-132">предоставленный тип Hello — toohello определенного типа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="47e2c-132">hello type provided is specific toohello resource type.</span></span> <span data-ttu-id="47e2c-133">Для хранения данных значение too"Microsoft.Storage/storageaccounts/providers/locks типа hello».</span><span class="sxs-lookup"><span data-stu-id="47e2c-133">For storage, set hello type too"Microsoft.Storage/storageaccounts/providers/locks".</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a><span data-ttu-id="47e2c-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47e2c-134">PowerShell</span></span>
<span data-ttu-id="47e2c-135">Блокировку можно развернуть ресурсы с помощью Azure PowerShell с помощью hello [New AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) команды.</span><span class="sxs-lookup"><span data-stu-id="47e2c-135">You lock deployed resources with Azure PowerShell by using hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="47e2c-136">toolock ресурс, укажите имя hello hello ресурса, его тип ресурса и его имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="47e2c-136">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="47e2c-137">toolock группу ресурсов, укажите имя hello hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="47e2c-137">toolock a resource group, provide hello name of hello resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="47e2c-138">tooget сведения о блокировке. Используйте [Get AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="47e2c-138">tooget information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="47e2c-139">tooget все блокировки hello в подписке, используйте:</span><span class="sxs-lookup"><span data-stu-id="47e2c-139">tooget all hello locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="47e2c-140">tooget все блокировки для ресурса, используйте:</span><span class="sxs-lookup"><span data-stu-id="47e2c-140">tooget all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="47e2c-141">tooget все блокировки для группы ресурсов, используйте:</span><span class="sxs-lookup"><span data-stu-id="47e2c-141">tooget all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="47e2c-142">Azure PowerShell предоставляет другие команды для блокировки работы, таких как [набор AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate блокировку, и [AzureRmResourceLock удаление](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete блокировку.</span><span class="sxs-lookup"><span data-stu-id="47e2c-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="47e2c-143">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="47e2c-143">Azure CLI</span></span>

<span data-ttu-id="47e2c-144">Блокировку можно развернуть ресурсами с помощью Azure CLI с помощью hello [az блокировки создания](/cli/azure/lock#create) команды.</span><span class="sxs-lookup"><span data-stu-id="47e2c-144">You lock deployed resources with Azure CLI by using hello [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="47e2c-145">toolock ресурс, укажите имя hello hello ресурса, его тип ресурса и его имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="47e2c-145">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="47e2c-146">toolock группу ресурсов, укажите имя hello hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="47e2c-146">toolock a resource group, provide hello name of hello resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="47e2c-147">tooget сведения о блокировке. Используйте [списку блокировки az](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="47e2c-147">tooget information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="47e2c-148">tooget все блокировки hello в подписке, используйте:</span><span class="sxs-lookup"><span data-stu-id="47e2c-148">tooget all hello locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="47e2c-149">tooget все блокировки для ресурса, используйте:</span><span class="sxs-lookup"><span data-stu-id="47e2c-149">tooget all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="47e2c-150">tooget все блокировки для группы ресурсов, используйте:</span><span class="sxs-lookup"><span data-stu-id="47e2c-150">tooget all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="47e2c-151">Azure CLI предоставляет другие команды для блокировки работы, таких как [az блокировки обновления](/cli/azure/lock#update) tooupdate блокировку, и [удалить блокировки az](/cli/azure/lock#delete) toodelete блокировку.</span><span class="sxs-lookup"><span data-stu-id="47e2c-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) tooupdate a lock, and [az lock delete](/cli/azure/lock#delete) toodelete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="47e2c-152">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="47e2c-152">REST API</span></span>
<span data-ttu-id="47e2c-153">Можно заблокировать развернутые ресурсы с hello [API REST для управления блокировками](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="47e2c-153">You can lock deployed resources with hello [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="47e2c-154">Hello REST API позволяет toocreate и удаление блокировок и получать сведения о существующей блокировки.</span><span class="sxs-lookup"><span data-stu-id="47e2c-154">hello REST API enables you toocreate and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="47e2c-155">toocreate блокировку, запустите:</span><span class="sxs-lookup"><span data-stu-id="47e2c-155">toocreate a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="47e2c-156">Hello область может быть подписки, группы ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="47e2c-156">hello scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="47e2c-157">Hello имя блокировки — вы можете toocall hello блокировки.</span><span class="sxs-lookup"><span data-stu-id="47e2c-157">hello lock-name is whatever you want toocall hello lock.</span></span> <span data-ttu-id="47e2c-158">В качестве версии API (api-version) используйте значение **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="47e2c-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="47e2c-159">В запросе hello включите объект JSON, задающий набор свойств hello hello блокировки.</span><span class="sxs-lookup"><span data-stu-id="47e2c-159">In hello request, include a JSON object that specifies hello properties for hello lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="47e2c-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47e2c-160">Next steps</span></span>
* <span data-ttu-id="47e2c-161">Дополнительные сведения о работе с блокировкой ресурсов см. в статье [Блокировка ресурсов Azure](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx).</span><span class="sxs-lookup"><span data-stu-id="47e2c-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="47e2c-162">toolearn о логически организации ресурсов, в разделе [Using теги tooorganize ресурсов](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="47e2c-162">toolearn about logically organizing your resources, see [Using tags tooorganize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="47e2c-163">toochange, какую группу ресурсов ресурс находится в разделе [переместить группу ресурсов toonew ресурсов](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="47e2c-163">toochange which resource group a resource resides in, see [Move resources toonew resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="47e2c-164">Ограничения и соглашения можно применять внутри подписки с помощью настраиваемых политик.</span><span class="sxs-lookup"><span data-stu-id="47e2c-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="47e2c-165">Дополнительные сведения см. в разделе [политика использования ресурсов toomanage и контроля доступа](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="47e2c-165">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="47e2c-166">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="47e2c-166">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

