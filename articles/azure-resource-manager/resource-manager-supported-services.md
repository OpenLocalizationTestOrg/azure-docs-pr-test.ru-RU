---
title: "Поставщики ресурсов Azure и типы ресурсов | Документация Майкрософт"
description: "Описывает поставщиков ресурсов, которые поддерживают диспетчер ресурсов, их схемы и доступные версии API, а также регионы, допускающие размещение ресурсов."
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
ms.openlocfilehash: 6a9128f45d4199404019cee594842d59c7f1aaf3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="36c46-103">Поставщики и типы ресурсов</span><span class="sxs-lookup"><span data-stu-id="36c46-103">Resource providers and types</span></span>

<span data-ttu-id="36c46-104">При развертывании ресурсов часто бывает необходимо получить сведения о типах и поставщиках ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-104">When deploying resources, you frequently need to retrieve information about the resource providers and types.</span></span> <span data-ttu-id="36c46-105">В этой статье раскрываются следующие темы:</span><span class="sxs-lookup"><span data-stu-id="36c46-105">In this article, you learn to:</span></span>

* <span data-ttu-id="36c46-106">просмотр всех поставщиков ресурсов в Azure;</span><span class="sxs-lookup"><span data-stu-id="36c46-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="36c46-107">проверка состояния регистрации поставщика ресурсов;</span><span class="sxs-lookup"><span data-stu-id="36c46-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="36c46-108">регистрация поставщика ресурсов;</span><span class="sxs-lookup"><span data-stu-id="36c46-108">Register a resource provider</span></span>
* <span data-ttu-id="36c46-109">просмотр типов ресурсов для поставщика ресурсов;</span><span class="sxs-lookup"><span data-stu-id="36c46-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="36c46-110">просмотр допустимых расположений для типа ресурса;</span><span class="sxs-lookup"><span data-stu-id="36c46-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="36c46-111">просмотр допустимых версий API для типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="36c46-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="36c46-112">Вы можете выполнить эти шаги с помощью портала, PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="36c46-112">You can perform these steps through the portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="36c46-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36c46-113">PowerShell</span></span>

<span data-ttu-id="36c46-114">Чтобы просмотреть всех поставщиков ресурсов в Azure, а также состояние регистрации для подписки, используйте команду ниже:</span><span class="sxs-lookup"><span data-stu-id="36c46-114">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="36c46-115">Она возвращает результаты, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="36c46-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="36c46-116">Регистрация поставщика ресурсов настраивает подписку для работы с поставщиком ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-116">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="36c46-117">Областью регистрации всегда является подписка.</span><span class="sxs-lookup"><span data-stu-id="36c46-117">The scope for registration is always the subscription.</span></span> <span data-ttu-id="36c46-118">По умолчанию многие поставщики ресурсов регистрируются автоматически.</span><span class="sxs-lookup"><span data-stu-id="36c46-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="36c46-119">Тем не менее, некоторые поставщики ресурсов может потребоваться зарегистрировать вручную.</span><span class="sxs-lookup"><span data-stu-id="36c46-119">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="36c46-120">Чтобы зарегистрировать поставщик ресурсов, необходимо иметь разрешение на выполнение операции `/register/action` для поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-120">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="36c46-121">Эта операция включается в роли участника и владельца.</span><span class="sxs-lookup"><span data-stu-id="36c46-121">This operation is included in the Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="36c46-122">Она возвращает результаты, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="36c46-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="36c46-123">Невозможно отменить регистрацию поставщика ресурсов, если в подписке еще есть типы ресурсов из этого поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="36c46-124">Чтобы просмотреть сведения для конкретного поставщика ресурсов, используйте команду ниже:</span><span class="sxs-lookup"><span data-stu-id="36c46-124">To see information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="36c46-125">Она возвращает результаты, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="36c46-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="36c46-126">Чтобы просмотреть типы ресурсов для поставщика ресурсов, используйте команду ниже:</span><span class="sxs-lookup"><span data-stu-id="36c46-126">To see the resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="36c46-127">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="36c46-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="36c46-128">Версия API соответствует версии операций API REST, выполняемых поставщиком ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-128">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="36c46-129">При появлении в поставщике ресурсов новых возможностей выпускается новая версия REST API.</span><span class="sxs-lookup"><span data-stu-id="36c46-129">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="36c46-130">Чтобы получить список доступных версий API для типа ресурса, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="36c46-130">To get the available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="36c46-131">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="36c46-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="36c46-132">Диспетчер ресурсов поддерживается во всех регионах, однако развертываемые вами ресурсы могут поддерживаться не во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="36c46-132">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="36c46-133">Кроме того, на вашу подписку могут налагаться ограничения, которые препятствуют использованию определенных регионов, поддерживающих ресурс.</span><span class="sxs-lookup"><span data-stu-id="36c46-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="36c46-134">Чтобы получить список поддерживаемых расположений для типа ресурса, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="36c46-134">To get the supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="36c46-135">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="36c46-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="36c46-136">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="36c46-136">Azure CLI</span></span>
<span data-ttu-id="36c46-137">Чтобы просмотреть всех поставщиков ресурсов в Azure, а также состояние регистрации для подписки, используйте команду ниже:</span><span class="sxs-lookup"><span data-stu-id="36c46-137">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="36c46-138">Она возвращает результаты, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="36c46-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="36c46-139">Регистрация поставщика ресурсов настраивает подписку для работы с поставщиком ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-139">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="36c46-140">Областью регистрации всегда является подписка.</span><span class="sxs-lookup"><span data-stu-id="36c46-140">The scope for registration is always the subscription.</span></span> <span data-ttu-id="36c46-141">По умолчанию многие поставщики ресурсов регистрируются автоматически.</span><span class="sxs-lookup"><span data-stu-id="36c46-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="36c46-142">Тем не менее, некоторые поставщики ресурсов может потребоваться зарегистрировать вручную.</span><span class="sxs-lookup"><span data-stu-id="36c46-142">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="36c46-143">Чтобы зарегистрировать поставщик ресурсов, необходимо иметь разрешение на выполнение операции `/register/action` для поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-143">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="36c46-144">Эта операция включается в роли участника и владельца.</span><span class="sxs-lookup"><span data-stu-id="36c46-144">This operation is included in the Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="36c46-145">Оно возвращает сообщение о выполнении регистрации.</span><span class="sxs-lookup"><span data-stu-id="36c46-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="36c46-146">Невозможно отменить регистрацию поставщика ресурсов, если в подписке еще есть типы ресурсов из этого поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="36c46-147">Чтобы просмотреть сведения для конкретного поставщика ресурсов, используйте команду ниже:</span><span class="sxs-lookup"><span data-stu-id="36c46-147">To see information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="36c46-148">Она возвращает результаты, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="36c46-148">Which returns results similar to:</span></span>

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

<span data-ttu-id="36c46-149">Чтобы просмотреть типы ресурсов для поставщика ресурсов, используйте команду ниже:</span><span class="sxs-lookup"><span data-stu-id="36c46-149">To see the resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="36c46-150">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="36c46-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="36c46-151">Версия API соответствует версии операций API REST, выполняемых поставщиком ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-151">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="36c46-152">При появлении в поставщике ресурсов новых возможностей выпускается новая версия REST API.</span><span class="sxs-lookup"><span data-stu-id="36c46-152">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="36c46-153">Чтобы получить список доступных версий API для типа ресурса, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="36c46-153">To get the available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="36c46-154">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="36c46-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="36c46-155">Диспетчер ресурсов поддерживается во всех регионах, однако развертываемые вами ресурсы могут поддерживаться не во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="36c46-155">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="36c46-156">Кроме того, на вашу подписку могут налагаться ограничения, которые препятствуют использованию определенных регионов, поддерживающих ресурс.</span><span class="sxs-lookup"><span data-stu-id="36c46-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="36c46-157">Чтобы получить список поддерживаемых расположений для типа ресурса, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="36c46-157">To get the supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="36c46-158">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="36c46-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="36c46-159">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="36c46-159">Portal</span></span>

<span data-ttu-id="36c46-160">Чтобы просмотреть всех поставщиков ресурсов в Azure, а также состояние регистрации для подписки, выберите **Подписки**.</span><span class="sxs-lookup"><span data-stu-id="36c46-160">To see all resource providers in Azure, and the registration status for your subscription, select **Subscriptions**.</span></span>

![выбор подписок](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="36c46-162">Выберите подписку, которую нужно просмотреть.</span><span class="sxs-lookup"><span data-stu-id="36c46-162">Choose the subscription to view.</span></span>

![указание подписки](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="36c46-164">Выберите **Поставщики ресурсов**, а затем просмотрите список доступных поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-164">Select **Resource providers** and view the list of available resource providers.</span></span>

![отображение поставщиков ресурсов](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="36c46-166">Регистрация поставщика ресурсов настраивает подписку для работы с поставщиком ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-166">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="36c46-167">Областью регистрации всегда является подписка.</span><span class="sxs-lookup"><span data-stu-id="36c46-167">The scope for registration is always the subscription.</span></span> <span data-ttu-id="36c46-168">По умолчанию многие поставщики ресурсов регистрируются автоматически.</span><span class="sxs-lookup"><span data-stu-id="36c46-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="36c46-169">Тем не менее, некоторые поставщики ресурсов может потребоваться зарегистрировать вручную.</span><span class="sxs-lookup"><span data-stu-id="36c46-169">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="36c46-170">Чтобы зарегистрировать поставщик ресурсов, необходимо иметь разрешение на выполнение операции `/register/action` для поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-170">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="36c46-171">Эта операция включается в роли участника и владельца.</span><span class="sxs-lookup"><span data-stu-id="36c46-171">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="36c46-172">Чтобы зарегистрировать поставщика ресурсов, выберите **Регистрация**.</span><span class="sxs-lookup"><span data-stu-id="36c46-172">To register a resource provider, select **Register**.</span></span>

![регистрация поставщика ресурсов](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="36c46-174">Невозможно отменить регистрацию поставщика ресурсов, если в подписке еще есть типы ресурсов из этого поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="36c46-175">Чтобы просмотреть сведения для конкретного поставщика ресурсов, выберите **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="36c46-175">To see information for a particular resource provider, select **More services**.</span></span>

![выбор других служб](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="36c46-177">Найдите **Обозреватель ресурсов** и выберите его из списка доступных вариантов.</span><span class="sxs-lookup"><span data-stu-id="36c46-177">Search for **Resource Explorer** and select it from the available options.</span></span>

![выбор обозревателя ресурсов](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="36c46-179">Выберите **Поставщики**.</span><span class="sxs-lookup"><span data-stu-id="36c46-179">Select **Providers**.</span></span>

![выбор поставщиков](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="36c46-181">Выберите поставщика ресурсов и тип ресурса, который вы хотите просмотреть.</span><span class="sxs-lookup"><span data-stu-id="36c46-181">Select the resource provider and resource type that you want to view.</span></span>

![Выбор типа ресурсов](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="36c46-183">Диспетчер ресурсов поддерживается во всех регионах, однако развертываемые вами ресурсы могут поддерживаться не во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="36c46-183">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="36c46-184">Кроме того, на вашу подписку могут налагаться ограничения, которые препятствуют использованию определенных регионов, поддерживающих ресурс.</span><span class="sxs-lookup"><span data-stu-id="36c46-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> <span data-ttu-id="36c46-185">Обозреватель ресурсов отображает допустимые расположения для типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="36c46-185">The resource explorer displays valid locations for the resource type.</span></span>

![Отображение расположений](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="36c46-187">Версия API соответствует версии операций API REST, выполняемых поставщиком ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36c46-187">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="36c46-188">При появлении в поставщике ресурсов новых возможностей выпускается новая версия REST API.</span><span class="sxs-lookup"><span data-stu-id="36c46-188">As a resource provider enables new features, it releases a new version of the REST API.</span></span> <span data-ttu-id="36c46-189">Обозреватель ресурсов отображает допустимые версии API для типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="36c46-189">The resource explorer displays valid API versions for the resource type.</span></span>

![Отображение версий API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="36c46-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36c46-191">Next steps</span></span>
* <span data-ttu-id="36c46-192">Сведения о создании шаблонов Resource Manager см. в статье [Создание шаблонов диспетчера ресурсов Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="36c46-192">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="36c46-193">Сведения о развертывании ресурсов см. в статье [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="36c46-193">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="36c46-194">Чтобы просмотреть операции для поставщика ресурсов, ознакомьтесь с [Azure REST API](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="36c46-194">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

