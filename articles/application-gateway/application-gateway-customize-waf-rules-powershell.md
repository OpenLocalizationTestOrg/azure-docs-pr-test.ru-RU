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
# <a name="customize-web-application-firewall-rules-through-powershell"></a>Настройка правил брандмауэра веб-приложения с помощью PowerShell

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

брандмауэр веб-приложения Azure шлюза приложения Hello (WAF) обеспечивает защиту веб-приложений. Эти протоколы предоставляются Привет открыть Web приложения безопасности проекта (OWASP) задайте правило Core (CRS). Некоторые правила могут приводить к ложным срабатываниям и блокировке реального трафика. По этой причине использование шлюза приложений содержит группы правил toocustomize возможность hello и правила. Дополнительные сведения о hello конкретных групп правил и правил см. в разделе [список правил и групп правил CRS брандмауэра приложения web](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Просмотр правил и групп правил

Привет, следующие примеры кода показывают, как tooview правила и группы, которые можно настроить для шлюза приложения с поддержкой WAF правил.

### <a name="view-rule-groups"></a>Просмотр групп правил

Следующий пример показывает как Hello tooview группы правил:

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

следующие выходные данные Hello является усеченное ответа от предшествующих пример hello:

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

## <a name="disable-rules"></a>Отключение правил

Hello следующий пример отключает правила `910018` и `910017` на шлюз приложений:

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Дальнейшие действия

После настройки вашей отключенные правила, вы узнаете как tooview WAF журналов. Дополнительные сведения см. в разделе [Журналы диагностики](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
