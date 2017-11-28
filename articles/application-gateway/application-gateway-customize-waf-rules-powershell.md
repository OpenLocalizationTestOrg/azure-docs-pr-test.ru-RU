---
title: "правила брандмауэра приложения web aaaCustomize в шлюз приложений Azure — PowerShell | Документы Microsoft"
description: "Это статье содержатся сведения о работе правил toocustomize брандмауэр веб-приложения в шлюз приложений с помощью PowerShell."
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
ms.openlocfilehash: f320e687b0f621515255469dac8e375cdd900dda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="e1f41-103">Настройка правил брандмауэра веб-приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1f41-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1f41-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="e1f41-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="e1f41-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1f41-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="e1f41-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e1f41-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="e1f41-107">брандмауэр веб-приложения Azure шлюза приложения Hello (WAF) обеспечивает защиту веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="e1f41-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="e1f41-108">Эти протоколы предоставляются Привет открыть Web приложения безопасности проекта (OWASP) задайте правило Core (CRS).</span><span class="sxs-lookup"><span data-stu-id="e1f41-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="e1f41-109">Некоторые правила могут приводить к ложным срабатываниям и блокировке реального трафика.</span><span class="sxs-lookup"><span data-stu-id="e1f41-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="e1f41-110">По этой причине использование шлюза приложений содержит группы правил toocustomize возможность hello и правила.</span><span class="sxs-lookup"><span data-stu-id="e1f41-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="e1f41-111">Дополнительные сведения о hello конкретных групп правил и правил см. в разделе [список правил и групп правил CRS брандмауэра приложения web](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="e1f41-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="e1f41-112">Просмотр правил и групп правил</span><span class="sxs-lookup"><span data-stu-id="e1f41-112">View rule groups and rules</span></span>

<span data-ttu-id="e1f41-113">Привет, следующие примеры кода показывают, как tooview правила и группы, которые можно настроить для шлюза приложения с поддержкой WAF правил.</span><span class="sxs-lookup"><span data-stu-id="e1f41-113">hello following code examples show how tooview rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="e1f41-114">Просмотр групп правил</span><span class="sxs-lookup"><span data-stu-id="e1f41-114">View rule groups</span></span>

<span data-ttu-id="e1f41-115">Следующий пример показывает как Hello tooview группы правил:</span><span class="sxs-lookup"><span data-stu-id="e1f41-115">hello following example shows how tooview rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="e1f41-116">следующие выходные данные Hello является усеченное ответа от предшествующих пример hello:</span><span class="sxs-lookup"><span data-stu-id="e1f41-116">hello following output is a truncated response from hello preceding example:</span></span>

```
OWASP (Ver. 3.0):

    REQUEST-910-IP-REPUTATION:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            910011     Rule 910011
            910012     Rule 910012
            ...        ...

    REQUEST-911-METHOD-ENFORCEMENT:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            911011     Rule 911011
            ...        ...

OWASP (Ver. 2.2.9):

    crs_20_protocol_violations:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            960911     Invalid HTTP Request Line
            981227     Apache Error: Invalid URI in Request.
            960000     Attempted multipart/form-data bypass
            ...        ...
```

## <a name="disable-rules"></a><span data-ttu-id="e1f41-117">Отключение правил</span><span class="sxs-lookup"><span data-stu-id="e1f41-117">Disable rules</span></span>

<span data-ttu-id="e1f41-118">Hello следующий пример отключает правила `910018` и `910017` на шлюз приложений:</span><span class="sxs-lookup"><span data-stu-id="e1f41-118">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="e1f41-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1f41-119">Next steps</span></span>

<span data-ttu-id="e1f41-120">После настройки вашей отключенные правила, вы узнаете как tooview WAF журналов.</span><span class="sxs-lookup"><span data-stu-id="e1f41-120">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="e1f41-121">Дополнительные сведения см. в разделе [Журналы диагностики](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="e1f41-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
