---
title: "aaaAzure поставщиков ресурсов и типы ресурсов | Документы Microsoft"
description: "Описывает hello поставщиков ресурсов, поддерживающих диспетчера ресурсов, их схемы и доступные версии API и hello областей, которые можно разместить ресурсы hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="903e3-103">Поставщики и типы ресурсов</span><span class="sxs-lookup"><span data-stu-id="903e3-103">Resource providers and types</span></span>

<span data-ttu-id="903e3-104">При развертывании ресурсов, необходимо часто tooretrieve сведения о hello поставщиков ресурсов и типов.</span><span class="sxs-lookup"><span data-stu-id="903e3-104">When deploying resources, you frequently need tooretrieve information about hello resource providers and types.</span></span> <span data-ttu-id="903e3-105">В этой статье раскрываются следующие темы:</span><span class="sxs-lookup"><span data-stu-id="903e3-105">In this article, you learn to:</span></span>

* <span data-ttu-id="903e3-106">просмотр всех поставщиков ресурсов в Azure;</span><span class="sxs-lookup"><span data-stu-id="903e3-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="903e3-107">проверка состояния регистрации поставщика ресурсов;</span><span class="sxs-lookup"><span data-stu-id="903e3-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="903e3-108">регистрация поставщика ресурсов;</span><span class="sxs-lookup"><span data-stu-id="903e3-108">Register a resource provider</span></span>
* <span data-ttu-id="903e3-109">просмотр типов ресурсов для поставщика ресурсов;</span><span class="sxs-lookup"><span data-stu-id="903e3-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="903e3-110">просмотр допустимых расположений для типа ресурса;</span><span class="sxs-lookup"><span data-stu-id="903e3-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="903e3-111">просмотр допустимых версий API для типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="903e3-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="903e3-112">Можно выполнить следующие действия через портал hello, PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="903e3-112">You can perform these steps through hello portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="903e3-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="903e3-113">PowerShell</span></span>

<span data-ttu-id="903e3-114">Используйте для всех поставщиков ресурсов в Azure, а также состояние регистрации hello для вашей подписки toosee:</span><span class="sxs-lookup"><span data-stu-id="903e3-114">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="903e3-115">Она возвращает результаты, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="903e3-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="903e3-116">Регистрация поставщика ресурсов настраивает toowork вашей подписки с поставщиком ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-116">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="903e3-117">Hello области для регистрации всегда является hello подписки.</span><span class="sxs-lookup"><span data-stu-id="903e3-117">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="903e3-118">По умолчанию многие поставщики ресурсов регистрируются автоматически.</span><span class="sxs-lookup"><span data-stu-id="903e3-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="903e3-119">Тем не менее, может потребоваться toomanually зарегистрировать некоторые поставщики ресурсов.</span><span class="sxs-lookup"><span data-stu-id="903e3-119">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="903e3-120">tooregister поставщик ресурсов должен иметь разрешение tooperform hello `/register/action` операции для поставщика ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-120">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="903e3-121">Эта операция входит в состав hello участника и владельца роли.</span><span class="sxs-lookup"><span data-stu-id="903e3-121">This operation is included in hello Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="903e3-122">Она возвращает результаты, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="903e3-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="903e3-123">Невозможно отменить регистрацию поставщика ресурсов, если в подписке еще есть типы ресурсов из этого поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="903e3-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="903e3-124">toosee информацию для поставщика определенного ресурса, используйте:</span><span class="sxs-lookup"><span data-stu-id="903e3-124">toosee information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="903e3-125">Она возвращает результаты, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="903e3-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="903e3-126">Используйте типы ресурсов hello toosee поставщик ресурсов:</span><span class="sxs-lookup"><span data-stu-id="903e3-126">toosee hello resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="903e3-127">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="903e3-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="903e3-128">версия API Hello соответствует версии tooa операции REST API, выпущенных поставщиком ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-128">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="903e3-129">Как поставщик ресурсов включает новые функции, он освобождает новой версии API-интерфейса REST hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-129">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="903e3-130">Используйте tooget hello доступные API версии для типа ресурса:</span><span class="sxs-lookup"><span data-stu-id="903e3-130">tooget hello available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="903e3-131">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="903e3-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="903e3-132">Диспетчер ресурсов поддерживается во всех регионах, но ресурсы hello развертываемого может не поддерживаться во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="903e3-132">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="903e3-133">Кроме того могут существовать ограничения на свою подписку, предотвратить использование некоторых регионах, которые поддерживают ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="903e3-134">с помощью tooget расположения hello поддерживается для типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="903e3-134">tooget hello supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="903e3-135">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="903e3-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="903e3-136">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="903e3-136">Azure CLI</span></span>
<span data-ttu-id="903e3-137">Используйте для всех поставщиков ресурсов в Azure, а также состояние регистрации hello для вашей подписки toosee:</span><span class="sxs-lookup"><span data-stu-id="903e3-137">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="903e3-138">Она возвращает результаты, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="903e3-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="903e3-139">Регистрация поставщика ресурсов настраивает toowork вашей подписки с поставщиком ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-139">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="903e3-140">Hello области для регистрации всегда является hello подписки.</span><span class="sxs-lookup"><span data-stu-id="903e3-140">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="903e3-141">По умолчанию многие поставщики ресурсов регистрируются автоматически.</span><span class="sxs-lookup"><span data-stu-id="903e3-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="903e3-142">Тем не менее, может потребоваться toomanually зарегистрировать некоторые поставщики ресурсов.</span><span class="sxs-lookup"><span data-stu-id="903e3-142">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="903e3-143">tooregister поставщик ресурсов должен иметь разрешение tooperform hello `/register/action` операции для поставщика ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-143">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="903e3-144">Эта операция входит в состав hello участника и владельца роли.</span><span class="sxs-lookup"><span data-stu-id="903e3-144">This operation is included in hello Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="903e3-145">Оно возвращает сообщение о выполнении регистрации.</span><span class="sxs-lookup"><span data-stu-id="903e3-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="903e3-146">Невозможно отменить регистрацию поставщика ресурсов, если в подписке еще есть типы ресурсов из этого поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="903e3-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="903e3-147">toosee информацию для поставщика определенного ресурса, используйте:</span><span class="sxs-lookup"><span data-stu-id="903e3-147">toosee information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="903e3-148">Она возвращает результаты, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="903e3-148">Which returns results similar to:</span></span>

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

<span data-ttu-id="903e3-149">Используйте типы ресурсов hello toosee поставщик ресурсов:</span><span class="sxs-lookup"><span data-stu-id="903e3-149">toosee hello resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="903e3-150">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="903e3-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="903e3-151">версия API Hello соответствует версии tooa операции REST API, выпущенных поставщиком ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-151">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="903e3-152">Как поставщик ресурсов включает новые функции, он освобождает новой версии API-интерфейса REST hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-152">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="903e3-153">Используйте tooget hello доступные API версии для типа ресурса:</span><span class="sxs-lookup"><span data-stu-id="903e3-153">tooget hello available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="903e3-154">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="903e3-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="903e3-155">Диспетчер ресурсов поддерживается во всех регионах, но ресурсы hello развертываемого может не поддерживаться во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="903e3-155">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="903e3-156">Кроме того могут существовать ограничения на свою подписку, предотвратить использование некоторых регионах, которые поддерживают ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="903e3-157">с помощью tooget расположения hello поддерживается для типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="903e3-157">tooget hello supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="903e3-158">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="903e3-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="903e3-159">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="903e3-159">Portal</span></span>

<span data-ttu-id="903e3-160">Выберите все поставщики ресурсов в Azure, а также состояние регистрации hello для вашей подписки toosee **подписки**.</span><span class="sxs-lookup"><span data-stu-id="903e3-160">toosee all resource providers in Azure, and hello registration status for your subscription, select **Subscriptions**.</span></span>

![выбор подписок](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="903e3-162">Выберите подписку tooview hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-162">Choose hello subscription tooview.</span></span>

![указание подписки](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="903e3-164">Выберите **поставщиков ресурсов** и просмотреть список доступных поставщиков ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-164">Select **Resource providers** and view hello list of available resource providers.</span></span>

![отображение поставщиков ресурсов](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="903e3-166">Регистрация поставщика ресурсов настраивает toowork вашей подписки с поставщиком ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-166">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="903e3-167">Hello области для регистрации всегда является hello подписки.</span><span class="sxs-lookup"><span data-stu-id="903e3-167">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="903e3-168">По умолчанию многие поставщики ресурсов регистрируются автоматически.</span><span class="sxs-lookup"><span data-stu-id="903e3-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="903e3-169">Тем не менее, может потребоваться toomanually зарегистрировать некоторые поставщики ресурсов.</span><span class="sxs-lookup"><span data-stu-id="903e3-169">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="903e3-170">tooregister поставщик ресурсов должен иметь разрешение tooperform hello `/register/action` операции для поставщика ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-170">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="903e3-171">Эта операция входит в состав hello участника и владельца роли.</span><span class="sxs-lookup"><span data-stu-id="903e3-171">This operation is included in hello Contributor and Owner roles.</span></span> <span data-ttu-id="903e3-172">Выберите поставщик ресурсов tooregister **зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="903e3-172">tooregister a resource provider, select **Register**.</span></span>

![регистрация поставщика ресурсов](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="903e3-174">Невозможно отменить регистрацию поставщика ресурсов, если в подписке еще есть типы ресурсов из этого поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="903e3-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="903e3-175">Выберите toosee сведения для конкретного ресурса поставщика, **дополнительные службы**.</span><span class="sxs-lookup"><span data-stu-id="903e3-175">toosee information for a particular resource provider, select **More services**.</span></span>

![выбор других служб](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="903e3-177">Поиск **обозреватель ресурсов** и выберите его из доступных параметров hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-177">Search for **Resource Explorer** and select it from hello available options.</span></span>

![выбор обозревателя ресурсов](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="903e3-179">Выберите **Поставщики**.</span><span class="sxs-lookup"><span data-stu-id="903e3-179">Select **Providers**.</span></span>

![выбор поставщиков](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="903e3-181">Выберите hello поставщика ресурсов и ресурсов введите что tooview.</span><span class="sxs-lookup"><span data-stu-id="903e3-181">Select hello resource provider and resource type that you want tooview.</span></span>

![Выбор типа ресурсов](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="903e3-183">Диспетчер ресурсов поддерживается во всех регионах, но ресурсы hello развертываемого может не поддерживаться во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="903e3-183">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="903e3-184">Кроме того могут существовать ограничения на свою подписку, предотвратить использование некоторых регионах, которые поддерживают ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> <span data-ttu-id="903e3-185">обозреватель ресурсов Hello отображает допустимые расположения для типа ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-185">hello resource explorer displays valid locations for hello resource type.</span></span>

![Отображение расположений](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="903e3-187">версия API Hello соответствует версии tooa операции REST API, выпущенных поставщиком ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-187">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="903e3-188">Как поставщик ресурсов включает новые функции, он освобождает новой версии API-интерфейса REST hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-188">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> <span data-ttu-id="903e3-189">обозреватель ресурсов Hello отображает допустимые версии API для типа ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="903e3-189">hello resource explorer displays valid API versions for hello resource type.</span></span>

![Отображение версий API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="903e3-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="903e3-191">Next steps</span></span>
* <span data-ttu-id="903e3-192">в разделе toolearn о создании шаблонов диспетчера ресурсов [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="903e3-192">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="903e3-193">toolearn о развертывании ресурсов, в разделе [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="903e3-193">toolearn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="903e3-194">операции hello tooview для поставщика ресурсов, в разделе [Azure REST API](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="903e3-194">tooview hello operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

