---
title: "правила брандмауэра приложения web aaaCustomize в шлюз приложений Azure — Azure CLI 2.0 | Документы Microsoft"
description: "Это статье содержатся сведения о работе правил toocustomize брандмауэр веб-приложения в шлюз приложений с Azure CLI 2.0 hello."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b83ffb9f6a7e0d0c8c970885d2bcb3b63d32581c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a><span data-ttu-id="0232e-103">Настройка правил брандмауэра приложения web через hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0232e-103">Customize web application firewall rules through hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0232e-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="0232e-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="0232e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0232e-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="0232e-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0232e-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="0232e-107">брандмауэр веб-приложения Azure шлюза приложения Hello (WAF) обеспечивает защиту веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="0232e-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="0232e-108">Эти протоколы предоставляются Привет открыть Web приложения безопасности проекта (OWASP) задайте правило Core (CRS).</span><span class="sxs-lookup"><span data-stu-id="0232e-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="0232e-109">Некоторые правила могут приводить к ложным срабатываниям и блокировке реального трафика.</span><span class="sxs-lookup"><span data-stu-id="0232e-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="0232e-110">По этой причине использование шлюза приложений содержит группы правил toocustomize возможность hello и правила.</span><span class="sxs-lookup"><span data-stu-id="0232e-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="0232e-111">Дополнительные сведения о hello конкретных групп правил и правил см. в разделе [список правил и групп правил CRS брандмауэра приложения web](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="0232e-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="0232e-112">Просмотр правил и групп правил</span><span class="sxs-lookup"><span data-stu-id="0232e-112">View rule groups and rules</span></span>

<span data-ttu-id="0232e-113">Привет, следующие примеры кода показывают, как tooview правила и группы, которые можно настроить правил.</span><span class="sxs-lookup"><span data-stu-id="0232e-113">hello following code examples show how tooview rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="0232e-114">Просмотр групп правил</span><span class="sxs-lookup"><span data-stu-id="0232e-114">View rule groups</span></span>

<span data-ttu-id="0232e-115">Hello в следующем примере показано, как tooview hello группы правил.</span><span class="sxs-lookup"><span data-stu-id="0232e-115">hello following example shows how tooview hello rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="0232e-116">следующие выходные данные Hello является усеченное ответа от предшествующих пример hello:</span><span class="sxs-lookup"><span data-stu-id="0232e-116">hello following output is a truncated response from hello preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  },
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_2.2.9",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
   "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "crs_20_protocol_violations",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "2.2.9",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="0232e-117">Просмотр правил в группе правил</span><span class="sxs-lookup"><span data-stu-id="0232e-117">View rules in a rule group</span></span>

<span data-ttu-id="0232e-118">Hello в следующем примере показано, как tooview правил в группе указанного правила:</span><span class="sxs-lookup"><span data-stu-id="0232e-118">hello following example shows how tooview rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="0232e-119">следующие выходные данные Hello является усеченное ответа от предшествующих пример hello:</span><span class="sxs-lookup"><span data-stu-id="0232e-119">hello following output is a truncated response from hello preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": [
          {
            "description": "Rule 910011",
            "ruleId": 910011
          },
          ...
        ]
      }
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

## <a name="disable-rules"></a><span data-ttu-id="0232e-120">Отключение правил</span><span class="sxs-lookup"><span data-stu-id="0232e-120">Disable rules</span></span>

<span data-ttu-id="0232e-121">Hello следующий пример отключает правила `910018` и `910017` на шлюз приложений:</span><span class="sxs-lookup"><span data-stu-id="0232e-121">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="0232e-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0232e-122">Next steps</span></span>

<span data-ttu-id="0232e-123">После настройки вашей отключенные правила, вы узнаете как tooview WAF журналов.</span><span class="sxs-lookup"><span data-stu-id="0232e-123">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="0232e-124">Дополнительные сведения см. в разделе [Журналы диагностики](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="0232e-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
