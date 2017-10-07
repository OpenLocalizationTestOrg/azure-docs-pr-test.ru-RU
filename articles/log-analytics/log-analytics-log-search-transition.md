---
title: "aaaAzure аналитика журналов запроса краткий справочник по языку | Документы Microsoft"
description: "Эта статья содержит помощь по переходу toohello новый язык запросов для анализа журналов, если вы уже знакомы с языком устаревших hello."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 8b4ee3d0b5e1ec8a9f95a09e0ad9835615ad1342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transitioning-tooazure-log-analytics-new-query-language"></a>Переход на новый язык запросов tooAzure анализа журналов

> [!NOTE]
> Можно прочитать дополнительные сведения о hello нового анализа журналов языка запросов и получения hello tooupgrade процедуры обновления рабочей области на [поиска журналов Azure Log Analytics рабочей toonew](log-analytics-log-search-upgrade.md).

Эта статья содержит помощь по переходу toohello новый язык запросов для анализа журналов, если вы уже знакомы с языком устаревших hello.

## <a name="language-converter"></a>Преобразователь языка

Если вы знакомы с hello прежних версий языка запросов анализа журналов, hello toocreate hello того же запроса в новый язык hello простым способом — toouse hello преобразователь языка, установленного в портал hello поиска журналов при преобразовании рабочей области.  С помощью преобразователя hello сложнее, чем в запросе прежних версий в hello текстового поля верхнего введя и выбрав **преобразовать**.  Можно либо щелкните запрос hello toorun кнопка поиска hello или копировать и вставить его toouse то в другом месте.

![Преобразователь языка](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="cheat-sheet"></a>Краткий справочник

Hello следующей таблице представлено сравнение различных стандартных запросов tooequivalent команд между язык запросов новых и устаревших hello в службе анализа журналов Azure.

| Описание | Прежняя версия | new |
|:--|:--|:--|
| Поиск по всем таблицам      | error | Поиск по слову "ошибка" (без учета регистра) |
| Выбор данных из таблицы | Type=Event |  Событие |
|                        | Type=Event &#124; select Source, EventLog, EventID | Event &#124; project Source, EventLog, EventID |
|                        | Type=Event &#124; top 100 | Event &#124; take 100 |
| Сравнение строк      | Type=Event Computer=srv01.contoso.com   | Event &#124; where Computer == "srv01.contoso.com" |
|                        | Type=Event Computer=contains("contoso") | Event &#124; where Computer contains "contoso" (без учета регистра)<br>Event &#124; where Computer contains "Contoso" (с учетом регистра) |
|                        | Type=Event Computer=RegEx("@contoso@")  | Event &#124; where Computer matches regex ".*contoso*" |
| Сравнение данных        | Type=Event TimeGenerated > NOW-1DAYS | Event &#124; where TimeGenerated > ago(1d) |
|                        | Type=Event TimeGenerated>2017-05-01 TimeGenerated<2017-05-31 | Event &#124; where TimeGenerated between (datetime(2017-05-01) .. datetime(2017-05-31)) |
| Сравнение логических значений     | Type=Heartbeat IsGatewayInstalled=false  | Пульс | where IsGatewayInstalled == false |
| Сортировать                   | Type=Event &#124; sort Computer asc, EventLog desc, EventLevelName asc | Event &#124;| sort by Computer asc, EventLog desc, EventLevelName asc |
| Уникальные значения               | Type=Event &#124; dedup Computer &#124;| select Computer | Event &#124; summarize by Computer, EventLog |
| Расширение столбцов         | Type=Perf CounterName="% Processor Time" &#124; EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION | Perf &#124; where CounterName == "% Processor Time" &#124;| extend Utilization = iff(CounterValue > 50, "HIGH", "LOW") |
| Агрегирование            | Type=Event &#124; measure count() as Count by Computer | Event &#124; summarize Count = count() by Computer |
|                                | Type=Perf ObjectName=Processor CounterName="% Processor Time" &#124; measure avg(CounterValue) by Computer interval 5minute | Perf &#124; where ObjectName=="Processor" and CounterName=="% Processor Time" &#124; summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min) |
| Группирование с ограничением | Type=Event &#124; measure count() by Computer &#124; top 10 | Event &#124; summarize AggregatedValue = count() by Computer &#124; limit 10 |
| Объединение множеств                  | Type=Event or Type=Syslog | union Event, Syslog |
| Объединение                   | Type=NetworkMonitoring &#124; join inner AgentIP (Type=Heartbeat) ComputerIP | NetworkMonitoring &#124; join kind=inner (search Type == "Heartbeat") on $left.AgentIP == $right.ComputerIP |



## <a name="next-steps"></a>Дальнейшие действия
- Извлечение [учебник по написанию запросов](https://go.microsoft.com/fwlink/?linkid=856078) с помощью hello новый язык запросов.
- См. toohello [Справочник по языку запросов](https://go.microsoft.com/fwlink/?linkid=856079) сведения о всех команд, операторы и функции для hello новый язык запросов.  
