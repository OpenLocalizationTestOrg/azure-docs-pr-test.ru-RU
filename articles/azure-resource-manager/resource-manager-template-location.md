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
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>Определение расположения ресурса в шаблонах Azure Resource Manager
При развертывании шаблона вам нужно указать расположение для каждого ресурса. В этом разделе показано, как тип расположения toodetermine hello, доступных tooyour подписки для каждого ресурса.

## <a name="determine-supported-locations"></a>Определение поддерживаемых расположений

Полный список поддерживаемых расположений для каждого типа ресурсов см. в таблице [Доступность продуктов по регионам](https://azure.microsoft.com/regions/services/). Тем не менее ваша подписка может имеет доступ tooall hello расположения в этом списке. Особый список расположений, которые являются подписки доступны tooyour toosee использовать Azure PowerShell или Azure CLI. 

Hello следующий пример использует PowerShell tooget hello расположения для hello `Microsoft.Web\sites` тип ресурса:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Hello следующий пример использует Azure CLI 2.0 tooget hello расположения для hello `Microsoft.Web\sites` тип ресурса:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>Определение расположения в шаблоне

После определения местоположения hello поддерживается для ваших ресурсов, необходимо tooset это расположение в шаблоне. Здравствуйте, наиболее простым способом tooset, это значение равно toocreate, группа ресурсов в расположении, которое поддерживает типы ресурсов hello и задать для каждого местоположения слишком`[resourceGroup().location]`. Повторное развертывание групп tooresource шаблонов hello в разных местах и не изменяют любые значения в шаблоне hello или параметры. 

Hello пример учетной записи хранилища, развернутых toohello местоположения hello группа ресурсов:

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

Если вам требуется toohardcode hello расположение в шаблон, укажите имя hello одной из областей hello поддерживается. Следующий пример Hello показаны учетной записи хранилища, который всегда развернуты tooNorth центральной части США:

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
* Рекомендации о том, как toocreate шаблонов, см. раздел [советы и рекомендации по созданию шаблонов диспетчера ресурсов Azure](resource-manager-template-best-practices.md).

