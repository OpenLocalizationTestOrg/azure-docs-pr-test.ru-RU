---
title: "Политики ресурсов Azure для сетевых ресурсов | Документация Майкрософт"
description: "Описываются политики Azure Resource Manager для управления развертыванием сетевых ресурсов."
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
ms.openlocfilehash: bca66bbdd9da9b3e4099d0d961f42c9368a17f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-to-network-resources"></a><span data-ttu-id="76888-103">Применение политик ресурсов к сетевым ресурсам</span><span class="sxs-lookup"><span data-stu-id="76888-103">Apply resource policies to network resources</span></span>
<span data-ttu-id="76888-104">В этой статье приведен пример [политики ресурсов](resource-manager-policy.md), которую можно применить к шлюзам виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="76888-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply to Azure virtual network gateways.</span></span> <span data-ttu-id="76888-105">Эта политика обеспечивает согласованность шлюзов, развертываемых в организации.</span><span class="sxs-lookup"><span data-stu-id="76888-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="76888-106">Определение допустимого номера SKU шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="76888-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="76888-107">Приведенная ниже политика ограничивает номера SKU, которые могут быть развернуты для шлюзов виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="76888-107">The following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="76888-108">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="76888-108">Next steps</span></span>
* <span data-ttu-id="76888-109">После определения правила политики (как показано в приведенных выше примерах) необходимо создать определение политики и назначить ей область.</span><span class="sxs-lookup"><span data-stu-id="76888-109">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="76888-110">Областью может быть подписка, группа ресурсов или ресурс.</span><span class="sxs-lookup"><span data-stu-id="76888-110">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="76888-111">Сведения о назначении политик с помощью портала см. в статье [Назначение политик ресурсов и управление ими с помощью портала Azure](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="76888-111">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="76888-112">Сведения о назначении политик с помощью REST API, PowerShell или Azure CLI см. в статье [Назначение политик ресурсов и управление ими](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="76888-112">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="76888-113">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="76888-113">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

