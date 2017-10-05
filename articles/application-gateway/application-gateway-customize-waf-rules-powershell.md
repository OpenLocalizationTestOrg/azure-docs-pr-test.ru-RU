---
title: "Настройка правил брандмауэра веб-приложения для шлюза приложений Azure с помощью PowerShell | Документация Майкрософт"
description: "Эта статья содержит сведения о том, как настроить правила брандмауэра веб-приложения в шлюзе приложений с помощью PowerShell."
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
ms.openlocfilehash: 681625e40035b05c593c6161236cb80b7db576b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="59200-103">Настройка правил брандмауэра веб-приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="59200-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="59200-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="59200-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="59200-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="59200-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="59200-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="59200-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="59200-107">Брандмауэр веб-приложения (WAF) шлюза приложений Azure обеспечивает защиту веб-приложений</span><span class="sxs-lookup"><span data-stu-id="59200-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="59200-108">с помощью основного набора правил (CRS) открытого проекта безопасности веб-приложений (OWASP).</span><span class="sxs-lookup"><span data-stu-id="59200-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="59200-109">Некоторые правила могут приводить к ложным срабатываниям и блокировке реального трафика.</span><span class="sxs-lookup"><span data-stu-id="59200-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="59200-110">Поэтому шлюз приложений предоставляет возможность настроить правила и группы правил.</span><span class="sxs-lookup"><span data-stu-id="59200-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="59200-111">Дополнительные сведения о конкретных правилах и группах правил см. в статье [Список групп правил и правил CRS брандмауэра веб-приложения](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="59200-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="59200-112">Просмотр правил и групп правил</span><span class="sxs-lookup"><span data-stu-id="59200-112">View rule groups and rules</span></span>

<span data-ttu-id="59200-113">Ниже приведены примеры кода для просмотра правил и групп правил, которые можно настроить в шлюзе приложений с включенным WAF.</span><span class="sxs-lookup"><span data-stu-id="59200-113">The following code examples show how to view rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="59200-114">Просмотр групп правил</span><span class="sxs-lookup"><span data-stu-id="59200-114">View rule groups</span></span>

<span data-ttu-id="59200-115">В следующем примере показано, как просмотреть группы правил:</span><span class="sxs-lookup"><span data-stu-id="59200-115">The following example shows how to view rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="59200-116">В результатах далее представлен сокращенный ответ из предыдущего примера.</span><span class="sxs-lookup"><span data-stu-id="59200-116">The following output is a truncated response from the preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="59200-117">Отключение правил</span><span class="sxs-lookup"><span data-stu-id="59200-117">Disable rules</span></span>

<span data-ttu-id="59200-118">В следующем примере отключаются правила `910018` и `910017` в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="59200-118">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="59200-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59200-119">Next steps</span></span>

<span data-ttu-id="59200-120">После настройки с отключением правил вы можете узнать, как просматривать журналы WAF.</span><span class="sxs-lookup"><span data-stu-id="59200-120">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="59200-121">Дополнительные сведения см. в разделе [Журналы диагностики](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="59200-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
