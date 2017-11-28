---
title: "Определение расположения ресурса Azure в шаблоне | Документация Майкрософт"
description: "Определение расположения ресурса в шаблоне Azure Resource Manager"
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
ms.openlocfilehash: 73e50a593c41e841dcaf184abb895406ff5001e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="2b0ca-103">Определение расположения ресурса в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2b0ca-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="2b0ca-104">При развертывании шаблона вам нужно указать расположение для каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="2b0ca-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="2b0ca-105">В этой статье описано, как определить расположения, доступные в рамках вашей подписки для каждого типа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2b0ca-105">This topic shows how to determine the locations that are available to your subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="2b0ca-106">Определение поддерживаемых расположений</span><span class="sxs-lookup"><span data-stu-id="2b0ca-106">Determine supported locations</span></span>

<span data-ttu-id="2b0ca-107">Полный список поддерживаемых расположений для каждого типа ресурсов см. в таблице [Доступность продуктов по регионам](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="2b0ca-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="2b0ca-108">Тем не менее подписка может не предусматривать доступ ко всем расположениям в этом списке.</span><span class="sxs-lookup"><span data-stu-id="2b0ca-108">However, your subscription might not have access to all the locations in that list.</span></span> <span data-ttu-id="2b0ca-109">Чтобы просмотреть список расположений, доступных для вашей подписки, используйте Azure PowerShell или командную строку Azure.</span><span class="sxs-lookup"><span data-stu-id="2b0ca-109">To see a customized list of locations that are available to your subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="2b0ca-110">В следующем примере список расположений для типа ресурса `Microsoft.Web\sites` отображается с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2b0ca-110">The following example uses PowerShell to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="2b0ca-111">В следующем примере список расположений для типа ресурса `Microsoft.Web\sites` отображается с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="2b0ca-111">The following example uses Azure CLI 2.0 to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="2b0ca-112">Определение расположения в шаблоне</span><span class="sxs-lookup"><span data-stu-id="2b0ca-112">Set location in template</span></span>

<span data-ttu-id="2b0ca-113">Определив поддерживаемые расположения для ресурсов, необходимо указать нужное расположение в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="2b0ca-113">After determining the supported locations for your resources, you need to set that location in your template.</span></span> <span data-ttu-id="2b0ca-114">Самый простой способ задать это значение — это создать группу ресурсов в расположении, которое поддерживает типы ресурсов, а затем указать для каждого расположения `[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="2b0ca-114">The easiest way to set this value is to create a resource group in a location that supports the resource types, and set each location to `[resourceGroup().location]`.</span></span> <span data-ttu-id="2b0ca-115">Можно развернуть шаблон в группы ресурсов в разных расположениях, но при этом не изменять параметры или значения в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="2b0ca-115">You can redeploy the template to resource groups in different locations, and not change any values in the template or parameters.</span></span> 

<span data-ttu-id="2b0ca-116">В следующем примере показана учетная запись хранения, которая развертывается в том же расположении, что и группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="2b0ca-116">The following example shows a storage account that is deployed to the same location as the resource group:</span></span>

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

<span data-ttu-id="2b0ca-117">Если необходимо жестко определить расположение в шаблоне, укажите имя одного из поддерживаемых регионов.</span><span class="sxs-lookup"><span data-stu-id="2b0ca-117">If you need to hardcode the location in your template, provide the name of one of the supported regions.</span></span> <span data-ttu-id="2b0ca-118">В следующем примере показано учетная запись хранения, которая всегда развертывается в Северо-центральном регионе США:</span><span class="sxs-lookup"><span data-stu-id="2b0ca-118">The following example shows a storage account that is always deployed to North Central US:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2b0ca-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2b0ca-119">Next steps</span></span>
* <span data-ttu-id="2b0ca-120">См. дополнительные рекомендации по [созданию шаблонов Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="2b0ca-120">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

