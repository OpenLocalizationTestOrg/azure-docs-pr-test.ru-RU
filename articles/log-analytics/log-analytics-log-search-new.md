---
title: "Поиск aaaLog в аналитику журнала OMS | Документы Microsoft"
description: "Требуется tooretrieve поиска журнала любые данные из службы анализа журналов.  В этой статье описывается добавление новых журналов, поиск выполняется в службе анализа журналов и предоставляет основные понятия, необходимые toounderstand перед созданием."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a>Основные сведения о поисках по журналам в Log Analytics

> [!NOTE]
> В этой статье описывается поиска журналов в Azure Log Analytics с помощью hello новый язык запросов.  Можно узнать больше о новом языке hello и получить tooupgrade процедуры hello в рабочей области [обновление поиск журнала toonew рабочей области Azure Log Analytics](log-analytics-log-search-upgrade.md).  
>
> Если в рабочей области не был обновленного toohello новый язык запросов, вы должны обращаться слишком[найти данные с помощью запросов поиска журналов в службе анализа журналов](log-analytics-log-searches.md).

Требуется tooretrieve поиска журнала любые данные из службы анализа журналов.  Ли анализируете данные на портале hello, Настройка toobe правило генерации оповещений уведомление определенному условию, или извлечения данных с помощью hello API аналитики журналов, будет использовать данные поиска по журналу toospecify hello нужные.  В этой статье описывается использование поисков по журналам в Log Analytics и предоставляются основные сведения, которые необходимо знать перед их созданием. В разделе hello [дальнейшие действия](#next-steps) разделе Дополнительные сведения о создании и редактировании запросов поиска журналов, а также для ссылки на языке запросов hello.

## <a name="where-log-searches-are-used"></a>Где используются поиски по журналам

Hello различными способами, который будет использоваться запросов поиска журналов в службе анализа журналов включить hello следующие:

- **Порталы.** Интерактивный анализ данных можно выполнять в репозиторий hello с hello [портала поиска журналов](log-analytics-log-search-log-search-portal.md) или hello [Advanced Analytics портала](https://go.microsoft.com/fwlink/?linkid=856587).  Это позволяет tooedit вашей запрашивать и анализировать результаты hello в разнообразных форматах и визуализации.  Большинство запросов, создаваемых начнется одного из порталов hello, а затем копируется убедившись, что он работает правильно.
- **Правила генерации оповещений.** [Правила генерации оповещений](log-analytics-alerts.md) заранее выявляют проблемы с данными в рабочей области.  Каждое правило генерации оповещений основано на поиске по журналам, который автоматически выполняется через определенные интервалы.  результаты Hello не проверяемого toodetermine, если необходимо создать предупреждение.
- **Представления.**  Можно создавать визуализации данных toobe, включенных в панели мониторинга пользователя с [конструктор представлений](log-analytics-view-designer.md).  Поиск журнала предоставляют hello данные, используемые [плитки](log-analytics-view-designer-tiles.md) и [визуализации частей](log-analytics-view-designer-parts.md) в каждом представлении.  Можно выполнить детализацию из частей визуализации в hello поиска журналов портала tooperform провести анализ данных hello.
- **Экспорт.**  При экспорте данных из tooExcel рабочей области аналитики журналов hello или [Power BI](log-analytics-powerbi.md), создайте tooexport данных журнала поиска toodefine hello.
- **PowerShell.** Сценарий PowerShell можно запустить из командной строки или runbook службы автоматизации Azure, использующий [Get AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) tooretrieve данные из службы анализа журналов.  Этот командлет требует tooretrieve данных hello toodetermine запроса.
- **API Log Analytics.**  Hello [API поиска журналов Служба аналитики журналов](log-analytics-log-search-api.md) позволяет любому клиенту REST API tooretrieve данные из рабочей области hello.  запрос API Hello включает запрос, который выполняется для анализа журналов toodetermine hello данных tooretrieve.

![Поиск по журналам](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a>Упорядочивание данных в Log Analytics
При создании запроса, сначала нужно определить, какие таблицы содержат данные hello, которые вы ищете. Каждый [источника данных](log-analytics-data-sources.md) и [решения](../operations-management-suite/operations-management-suite-solutions.md) хранит данные в таблицах, выделенные в рабочей области аналитики журналов hello.  Документация для каждого источника данных и решение включает имя hello hello типа данных, который создает и описание каждого из его свойств.     Многие запросы потребуется только данные из одной таблицы, но другие могут использовать различные параметры tooinclude данные из нескольких таблиц.

![Таблицы](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a>Написание запроса
В основе hello журнала операций поиска в службе анализа журналов — [язык запросов широко](https://docs.loganalytics.io/) , позволяющий получать и анализировать данные из репозитория hello, различными способами.  Этот же язык запросов используется для [Application Insights](../application-insights/app-insights-analytics.md).  Изучение как toowrite запроса — критический toocreating поиска журналов в службе анализа журналов.  Начнем с простых запросов обычно и затем toouse ход выполнения более сложных функций как становятся более сложными требованиями.

Базовая структура Hello запроса является исходной таблицы, за которым следует ряд операторов, разделенных символом вертикальной черты `|`.  Можно связывать друг с другом несколько операторов toorefine hello данных и выполнения дополнительных функций.

Например предположим, что требуется, чтобы toofind hello top 10 компьютеров с hello большинство событий ошибок через hello прошлый день.

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

Или может быть необходимо toofind компьютерах, которые еще не имели периодический сигнал в последний день hello.

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

Как насчет графика с hello процессора для каждого компьютера из прошлой неделе?

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

Вы можно увидеть по образцам быстрый, независимо от типа данных, которым вы работаете, hello hello аналогичен структура запроса hello.  Его можно разбить на отдельных шагов, где hello результирующие данные из одной команды отправляется через hello конвейера toohello следующей команды.

Полную документацию по языка запросов Azure Log Analytics hello, включая учебные материалы и справочник по языку см hello [документацию по языку запросов анализа журналов Azure](https://docs.loganalytics.io/).

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о hello [порталы использовать toocreate и изменение запросов поиска журналов](log-analytics-log-search-portals.md).
- Извлечение [учебник по написанию запросов](https://go.microsoft.com/fwlink/?linkid=856078) с помощью hello новый язык запросов.
