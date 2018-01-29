---
title: "Ошибки в Azure, связанные с недоступностью номера SKU | Документация Майкрософт"
description: "В этой статье объясняется, как устранить ошибки, связанные с недоступностью номера SKU при развертывании."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: support-article
ms.date: 09/13/2017
ms.author: tomfitz
ms.openlocfilehash: 25cea4ae23471d182105ca3f720aaf74f81bf8c4
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="resolve-errors-for-sku-not-available"></a>Устранение ошибок, связанных с недоступностью номера SKU

В этой статье объясняется, как устранить ошибку **SkuNotAvailable**.

## <a name="symptom"></a>Симптом

При развертывании ресурса (как правило, виртуальной машины) появляются следующие код ошибки и сообщение об ошибке:

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

## <a name="cause"></a>Причина:

Эта ошибка возникает, когда выбранный номер SKU ресурса (например, размер виртуальной машины) недоступен для указанного расположения.

## <a name="solution"></a>Решение

Чтобы устранить эту проблему, необходимо определить номера SKU, доступные в регионе. Для поиска доступных номеров SKU можно использовать PowerShell, портал или операцию REST.

### <a name="solution-1"></a>Решение 1

Воспользуйтесь командой [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) в PowerShell. Отфильтруйте результаты по расположению. Эта команда поддерживается только в Azure PowerShell последней версии.

```powershell
Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
```

Результаты включают список номеров SKU для расположения и имеющиеся ограничения для этого номера SKU.

```powershell
ResourceType                Name      Locations Restriction                      Capability Value
------------                ----      --------- -----------                      ---------- -----
availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
virtualMachines      Standard_A0 southcentralus
virtualMachines      Standard_A1 southcentralus
virtualMachines      Standard_A2 southcentralus
```

### <a name="solution-2"></a>Решение 2

В Azure CLI используйте команду `az vm list-skus`. Для фильтрации выходных данных можно использовать `grep` или другую подобную служебную программу.

```bash
$ az vm list-skus --output table
ResourceType      Locations           Name                    Capabilities                       Tier      Size           Restrictions
----------------  ------------------  ----------------------  ---------------------------------  --------  -------------  ---------------------------
availabilitySets  eastus              Classic                 MaximumPlatformFaultDomainCount=3
avilabilitySets   eastus              Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  eastus2             Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  eastus2             Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  westus              Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  westus              Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  centralus           Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  centralus           Aligned                 MaximumPlatformFaultDomainCount=3
```

### <a name="solution-3"></a>Решение 3

Воспользуйтесь [порталом](https://portal.azure.com). Войдите на портал и добавьте ресурс с помощью интерфейса. При настройке значений вы увидите доступные SKU для этого ресурса. Не нужно завершать развертывание.

![Доступные номера SKU](./media/resource-manager-sku-not-available-errors/view-sku.png)

### <a name="solution-4"></a>Решение 4

Используйте REST API для виртуальных машин. Отправьте следующий запрос:

```HTTP 
GET
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
```

Он возвращает доступные номера SKU и регионы в приведенном ниже формате.

```json
{
  "value": [
    {
      "resourceType": "virtualMachines",
      "name": "Standard_A0",
      "tier": "Standard",
      "size": "A0",
      "locations": [
        "eastus"
      ],
      "restrictions": []
    },
    {
      "resourceType": "virtualMachines",
      "name": "Standard_A1",
      "tier": "Standard",
      "size": "A1",
      "locations": [
        "eastus"
      ],
      "restrictions": []
    },
    ...
  ]
}
```

Если вам не удалось найти подходящий номер SKU в этом или любом другом регионе, который соответствует потребностям вашей компании, обратитесь в [службу поддержки Azure](https://aka.ms/skurestriction).