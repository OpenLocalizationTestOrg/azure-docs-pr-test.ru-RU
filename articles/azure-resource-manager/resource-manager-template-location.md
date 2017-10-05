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
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>Определение расположения ресурса в шаблонах Azure Resource Manager
При развертывании шаблона вам нужно указать расположение для каждого ресурса. В этой статье описано, как определить расположения, доступные в рамках вашей подписки для каждого типа ресурсов.

## <a name="determine-supported-locations"></a>Определение поддерживаемых расположений

Полный список поддерживаемых расположений для каждого типа ресурсов см. в таблице [Доступность продуктов по регионам](https://azure.microsoft.com/regions/services/). Тем не менее подписка может не предусматривать доступ ко всем расположениям в этом списке. Чтобы просмотреть список расположений, доступных для вашей подписки, используйте Azure PowerShell или командную строку Azure. 

В следующем примере список расположений для типа ресурса `Microsoft.Web\sites` отображается с помощью PowerShell:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

В следующем примере список расположений для типа ресурса `Microsoft.Web\sites` отображается с помощью Azure CLI 2.0.

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>Определение расположения в шаблоне

Определив поддерживаемые расположения для ресурсов, необходимо указать нужное расположение в шаблоне. Самый простой способ задать это значение — это создать группу ресурсов в расположении, которое поддерживает типы ресурсов, а затем указать для каждого расположения `[resourceGroup().location]`. Можно развернуть шаблон в группы ресурсов в разных расположениях, но при этом не изменять параметры или значения в шаблоне. 

В следующем примере показана учетная запись хранения, которая развертывается в том же расположении, что и группа ресурсов:

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

Если необходимо жестко определить расположение в шаблоне, укажите имя одного из поддерживаемых регионов. В следующем примере показано учетная запись хранения, которая всегда развертывается в Северо-центральном регионе США:

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

## <a name="next-steps"></a>Дальнейшие действия
* См. дополнительные рекомендации по [созданию шаблонов Azure Resource Manager](resource-manager-template-best-practices.md).

