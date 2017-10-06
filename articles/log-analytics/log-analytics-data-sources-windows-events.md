---
title: "aaaCollect и анализировать журналы событий Windows в службе анализа журналов OMS | Документы Microsoft"
description: "Журналы событий Windows являются одним из источников данных наиболее распространенные hello, используемых службой аналитики журналов.  В этой статье описывается tooconfigure коллекции журналов событий Windows и сведения о записи hello их создания в репозитории OMS hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: c05648af39258443f22fd11e1d751b5ccec8c391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Источники данных для журнала событий Windows в Log Analytics
Журналы событий Windows являются одним из наиболее распространенных hello [источники данных](log-analytics-data-sources.md) для сбора данных с помощью агентов Windows, так как многие приложения записывают toohello журнал событий Windows.  Собирать события из стандартных журналов, например системы и приложений в toospecifying сложения любого пользовательского журнала, создаваемых приложениями необходимо toomonitor.

![События Windows](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Настройка журналов событий Windows
Настройка журналов событий Windows hello [меню данные в параметры журнала аналитика](log-analytics-data-sources.md#configuring-data-sources).

Служба аналитики журналов собирает только события из журналов событий Windows hello, указанных в параметрах hello.  Можно добавить журнал событий, введя имя hello журнала hello команду  **+** .  Для каждого журнала собираются только события, hello hello выбраны степени серьезности.  Проверьте hello степени серьезности для определенного журнала hello, которые должны toocollect.  Любые дополнительные критерии не может предоставить toofilter события.

При вводе hello имя журнала событий, аналитика журналов приведены общие имена журнала событий. Если требуется tooadd журнала hello не отображается в списке hello, его можно добавить в, введя в полное имя журнала hello hello. Полное имя журнала hello hello можно найти с помощью средства просмотра событий. В окне просмотра событий откройте hello *свойства* страница hello журнала и скопируйте строку hello из hello *полное имя* поля.

![Настройка событий Windows](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a>Сбор данных
Служба аналитики журналов собирает каждого события, которое соответствует выбранной уровень серьезности от отслеживаемый журнал событий, как создается событие hello.  Hello агент записывает его место в каждого, выполняющее сбор данных из журнала событий.  Если агент hello переходит в автономный режим на период времени, затем анализа журналов собирает события от последнего места остановки, даже если эти события создаются, когда агент hello находился в автономном режиме.  Есть вероятность для toonot эти события собираются, если журнал событий hello обертывает уничтожается события перезаписи, когда агент hello отключен от сети.

>[!NOTE]
>Log Analytics не собирает события аудита, созданные SQL Server, из источника *MSSQLSERVER* с идентификатором события 18453, которые содержат ключевые слова *Classic* или *Audit Success* и ключевое слово *0xa0000000000000*.
>

## <a name="windows-event-records-properties"></a>Свойства записей о событиях Windows
Записи в журнале событий Windows имеют тип **событие** и имеющих свойства hello в hello в следующей таблице:

| Свойство | Описание |
|:--- |:--- |
| Компьютер |Имя компьютера hello, hello события, собранные из. |
| EventCategory |Категория событий hello. |
| EventData |Все данные событий в формате RAW. |
| EventID |Количество событий hello. |
| EventLevel |Уровень серьезности события hello в числовой форме. |
| EventLevelName |Уровень серьезности события hello в виде текста. |
| EventLog |Имя журнала событий hello, hello события, собранные из. |
| ParameterXml |Значения параметров события в формате XML. |
| ManagementGroupName |Имя группы управления hello для агентов System Center Operations Manager.  Для других агентов это AOI-<workspace ID>. |
| RenderedDescription |Описание события со значениями параметров. |
| Источник |Источник события hello. |
| SourceSystem |Тип события агента hello были собраны. <br> OpsManager — агент Windows, подключенный напрямую или управляемый с помощью Operations Manager. <br> Linux — все агенты Linux  <br> AzureStorage – диагностика Azure |
| TimeGenerated |Дата и время события hello был создан в Windows. |
| UserName |Имя пользователя учетной записи hello, в журнал событий hello. |

## <a name="log-searches-with-windows-events"></a>Поиск журналов с помощью событий Windows
Hello следующей таблице приведены примеры различных запросов поиска журналов, которые получают записи в журнале событий Windows.

| Запрос | Описание |
|:--- |:--- |
| Type=Event |Все события Windows. |
| Type=Event EventLevelName=error |Все события Windows с указанием серьезности ошибки. |
| Type=Event &#124; Measure count() by Source |Число событий Windows по источникам. |
| Type=Event EventLevelName=error &#124; Measure count() by Source |Число событий ошибок Windows по источникам. |


>[!NOTE]
> Если рабочую область был обновленного toohello [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то hello выше запросы будут изменены следующие toohello.
>
>| Запрос | Описание |
|:---|:---|
| Событие |Все события Windows. |
| Event &#124; where EventLevelName == "error" |Все события Windows с указанием серьезности ошибки. |
| Event &#124; summarize count() by Source |Число событий Windows по источникам. |
| Event &#124; where EventLevelName == "error" &#124; summarize count() by Source |Число событий ошибок Windows по источникам. |


## <a name="next-steps"></a>Дальнейшие действия
* Настройка других анализа журналов toocollect [источники данных](log-analytics-data-sources.md) для анализа.
* Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений.  
* Используйте [настраиваемые поля](log-analytics-custom-fields.md) tooparse hello событие записывается в отдельные поля.
* Настройте [коллекцию счетчиков производительности](log-analytics-data-sources-performance-counters.md) из агентов Windows.
