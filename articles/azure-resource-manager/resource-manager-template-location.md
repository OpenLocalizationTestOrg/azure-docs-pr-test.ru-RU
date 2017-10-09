---
title: "расположение ресурса aaaAzure в шаблоне | Документы Microsoft"
description: "Показано, как tooset расположение ресурса в шаблоне диспетчера ресурсов Azure"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="409fb-103">Определение расположения ресурса в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="409fb-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="409fb-104">При развертывании шаблона вам нужно указать расположение для каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="409fb-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="409fb-105">В этом разделе показано, как тип расположения toodetermine hello, доступных tooyour подписки для каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="409fb-105">This topic shows how toodetermine hello locations that are available tooyour subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="409fb-106">Определение поддерживаемых расположений</span><span class="sxs-lookup"><span data-stu-id="409fb-106">Determine supported locations</span></span>

<span data-ttu-id="409fb-107">Полный список поддерживаемых расположений для каждого типа ресурсов см. в таблице [Доступность продуктов по регионам](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="409fb-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="409fb-108">Тем не менее ваша подписка может имеет доступ tooall hello расположения в этом списке.</span><span class="sxs-lookup"><span data-stu-id="409fb-108">However, your subscription might not have access tooall hello locations in that list.</span></span> <span data-ttu-id="409fb-109">Особый список расположений, которые являются подписки доступны tooyour toosee использовать Azure PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="409fb-109">toosee a customized list of locations that are available tooyour subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="409fb-110">Hello следующий пример использует PowerShell tooget hello расположения для hello `Microsoft.Web\sites` тип ресурса:</span><span class="sxs-lookup"><span data-stu-id="409fb-110">hello following example uses PowerShell tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="409fb-111">Hello следующий пример использует Azure CLI 2.0 tooget hello расположения для hello `Microsoft.Web\sites` тип ресурса:</span><span class="sxs-lookup"><span data-stu-id="409fb-111">hello following example uses Azure CLI 2.0 tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="409fb-112">Определение расположения в шаблоне</span><span class="sxs-lookup"><span data-stu-id="409fb-112">Set location in template</span></span>

<span data-ttu-id="409fb-113">После определения местоположения hello поддерживается для ваших ресурсов, необходимо tooset это расположение в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="409fb-113">After determining hello supported locations for your resources, you need tooset that location in your template.</span></span> <span data-ttu-id="409fb-114">Здравствуйте, наиболее простым способом tooset, это значение равно toocreate, группа ресурсов в расположении, которое поддерживает типы ресурсов hello и задать для каждого местоположения слишком`[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="409fb-114">hello easiest way tooset this value is toocreate a resource group in a location that supports hello resource types, and set each location too`[resourceGroup().location]`.</span></span> <span data-ttu-id="409fb-115">Повторное развертывание групп tooresource шаблонов hello в разных местах и не изменяют любые значения в шаблоне hello или параметры.</span><span class="sxs-lookup"><span data-stu-id="409fb-115">You can redeploy hello template tooresource groups in different locations, and not change any values in hello template or parameters.</span></span> 

<span data-ttu-id="409fb-116">Hello пример учетной записи хранилища, развернутых toohello местоположения hello группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="409fb-116">hello following example shows a storage account that is deployed toohello same location as hello resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

<span data-ttu-id="409fb-117">Если вам требуется toohardcode hello расположение в шаблон, укажите имя hello одной из областей hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="409fb-117">If you need toohardcode hello location in your template, provide hello name of one of hello supported regions.</span></span> <span data-ttu-id="409fb-118">Следующий пример Hello показаны учетной записи хранилища, который всегда развернуты tooNorth центральной части США:</span><span class="sxs-lookup"><span data-stu-id="409fb-118">hello following example shows a storage account that is always deployed tooNorth Central US:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="409fb-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="409fb-119">Next steps</span></span>
* <span data-ttu-id="409fb-120">Рекомендации о том, как toocreate шаблонов, см. раздел [советы и рекомендации по созданию шаблонов диспетчера ресурсов Azure](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="409fb-120">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

