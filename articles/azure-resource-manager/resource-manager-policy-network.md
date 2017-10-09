---
title: "политики ресурсов aaaAzure сетевых ресурсов | Документы Microsoft"
description: "Описание политик диспетчера ресурсов Azure для управления развертыванием hello сетевых ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: a6072c1c30db0a4e4a1cae04efc7828d14069709
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toonetwork-resources"></a><span data-ttu-id="30c7e-103">Применить ресурс политики toonetwork ресурсы</span><span class="sxs-lookup"><span data-stu-id="30c7e-103">Apply resource policies toonetwork resources</span></span>
<span data-ttu-id="30c7e-104">В этой статье приведен пример [политика ресурсов](resource-manager-policy.md) можно применить tooAzure шлюзы виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="30c7e-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply tooAzure virtual network gateways.</span></span> <span data-ttu-id="30c7e-105">Эта политика обеспечивает согласованность шлюзов, развертываемых в организации.</span><span class="sxs-lookup"><span data-stu-id="30c7e-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="30c7e-106">Определение допустимого номера SKU шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="30c7e-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="30c7e-107">следующие политики Hello ограничивает какие конфигурации могут развертываться для шлюзов виртуальных сетей:</span><span class="sxs-lookup"><span data-stu-id="30c7e-107">hello following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Network/virtualNetworkGateways"
      },
      {
        "not": {
          "field": "Microsoft.Network/virtualNetworkGateways/sku.name",
          "in": [
            "Basic",
            "VpnGw1"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="30c7e-108">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="30c7e-108">Next steps</span></span>
* <span data-ttu-id="30c7e-109">После определения правила политики (как показано в предыдущих примерах hello), требуется определение политики toocreate hello и назначьте его tooa области.</span><span class="sxs-lookup"><span data-stu-id="30c7e-109">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="30c7e-110">Hello область может быть подписки, группы ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="30c7e-110">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="30c7e-111">политики tooassign через портал hello см. [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="30c7e-111">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="30c7e-112">политики tooassign через API-Интерфейс REST, PowerShell или Azure CLI см. [назначение политики и управлять ими через сценарий](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="30c7e-112">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="30c7e-113">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="30c7e-113">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

