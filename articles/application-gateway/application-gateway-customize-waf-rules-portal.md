---
title: "правила брандмауэра приложения web aaaCustomize в шлюз приложений Azure — портал Azure | Документы Microsoft"
description: "Это статье содержатся сведения о работе правил toocustomize брандмауэр веб-приложения в приложение шлюза с портала Azure hello."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a>Настроить правила брандмауэра веб-приложения через портал Azure hello

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

брандмауэр веб-приложения Azure шлюза приложения Hello (WAF) обеспечивает защиту веб-приложений. Эти протоколы предоставляются Привет открыть Web приложения безопасности проекта (OWASP) задайте правило Core (CRS). Некоторые правила могут приводить к ложным срабатываниям и блокировке реального трафика. По этой причине использование шлюза приложений содержит группы правил toocustomize возможность hello и правила. Дополнительные сведения о hello конкретных групп правил и правил см. в разделе [список правил и групп правил CRS брандмауэра приложения web](application-gateway-crs-rulegroups-rules.md).

>[!NOTE]
> Если шлюз приложений не использует уровень WAF hello, hello параметр tooupgrade hello шлюза toohello WAF уровня приложения отображается hello правой панели. 

![Включение WAF][fig1]

## <a name="view-rule-groups-and-rules"></a>Просмотр правил и групп правил

**tooview группы правил и правила**
   1. Обзор шлюза toohello приложений, а затем выберите **брандмауэр веб-приложения**.  
   2. Выберите **Advanced rule configuration** (Расширенная настройка правил).  
   В этом представлении отображается таблица на странице приветствия все группы правил hello, в состав hello выбранный набор правил. Будут выбраны все флажки hello правило.

![Настройка отключенных правил][1]

## <a name="search-for-rules-toodisable"></a>Поиск правил toodisable

Hello **веб-приложения параметры брандмауэра** колонке предоставляет возможность hello toofilter hello правил при помощи полнотекстового поиска. результат Hello отображает только группы правил hello и правила, которые содержат текст hello, который вы ищете.

![Поиск правил][2]

## <a name="disable-rule-groups-and-rules"></a>Отключение правил и групп правил

При отключении правил можно отключить всю группу правил или определенные правила в одной или нескольких группах. 

**группы правил toodisable или определенные правила**

   1. Поиск правил hello или группы правил, которые должны toodisable.
   2. Снимите флажки hello hello правил, которые должны toodisable. 
   2. Щелкните **Сохранить**. 

![Сохранение изменений][3]

## <a name="next-steps"></a>Дальнейшие действия

После настройки вашей отключенные правила, вы узнаете как tooview WAF журналов. Дополнительные сведения см. в разделе [Журналы диагностики](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
