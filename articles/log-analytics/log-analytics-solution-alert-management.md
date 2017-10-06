---
title: "aaaAlert решение для управления в Operations Management Suite (OMS) | Документы Microsoft"
description: "Hello решение для управления оповещениями в службе анализа журналов позволяет анализировать все предупреждения hello в вашей среде.  В дополнение tooconsolidating предупреждения, созданные в OMS он импортирует предупреждения от подключенных групп управления System Center Operations Manager в службе анализа журналов."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fe5d534e-0418-4e2f-9073-8025e13271a8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: aff9bd8d88839c5227bb9ec3a1b5209a3cd7cdf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>Решение управления оповещениями в Operations Management Suite (OMS)

![Значок "Управление оповещениями"](media/log-analytics-solution-alert-management/icon.png)

Hello решение для управления оповещениями позволяет анализировать все предупреждения hello в репозитории анализа журналов.  Эти оповещения могут поступать из различных источников, например [созданных службой Log Analytics](log-analytics-alerts.md) или [импортированных из Nagios или Zabbix](log-analytics-linux-agents.md).  Hello решения также импортирует предупреждения из любого [подключенные группы управления System Center Operations Manager](log-analytics-om-agents.md).

## <a name="prerequisites"></a>Предварительные требования
Hello решение работает с какие-либо записи в хранилище аналитики журналов hello с типом **предупреждения**, поэтому необходимо выполнить любые необходимые toocollect настроен этих записей.

- Для анализа журналов оповещений [создать правила оповещений](log-analytics-alerts.md) toocreate записи оповещений непосредственно в репозитории hello.
- Оповещения Nagios и Zabbix [настройки этих серверов](log-analytics-linux-agents.md) toosend предупреждения tooLog Analytics.
- Для предупреждений System Center Operations Manager [подключения рабочую область службы анализа журналов управления группы Operations Manager tooyour](log-analytics-om-agents.md).  Все оповещения, созданные в System Center Operations Manager, импортируются в Log Analytics.  

## <a name="configuration"></a>Конфигурация
Добавить tooyour решение управления оповещениями hello, рабочую область OMS hello процесс описывается в [добавить решения](log-analytics-add-solutions.md).  Дополнительная настройка не требуется.

## <a name="management-packs"></a>Пакеты управления
Если группе управления System Center Operations Manager подключенной tooyour рабочей области OMS, hello следующие пакеты управления устанавливаются в System Center Operations Manager, при добавлении этого решения.  Нет, настройки или обслуживания необходимых пакетов управления hello.  

* Управление оповещениями Microsoft System Center Advisor (Microsoft.IntelligencePacks.AlertManagement)

Дополнительные сведения об обновлении пакетов управления решения см. в разделе [tooLog подключение Operations Manager Analytics](log-analytics-om-agents.md).

## <a name="data-collection"></a>Сбор данных
### <a name="agents"></a>Агенты
Привет, в следующей таблице описываются hello подключенных источников, которые поддерживаются в этом решении.

| Подключенный источник | Поддержка | Описание |
|:--- |:--- |:--- |
| [Агенты Windows](log-analytics-windows-agents.md) | Нет |Прямые агенты Windows не создают оповещения.  Оповещения Log Analytics могут создаваться на основании событий и данных о производительности, собранных из агентов Windows. |
| [Агенты Linux](log-analytics-linux-agents.md) | Нет |Прямые агенты Linux не создают оповещения.  Оповещения Log Analytics могут создаваться на основании событий и данных о производительности, собранных из агентов Linux.  Оповещения Nagios и Zabbix собираются с серверов, на которых требуется агент Linux hello. |
| [Группа управления System Center Operations Manager](log-analytics-om-agents.md) |Да |Оповещения, которые созданы на агентах Operations Manager поставляются toohello группы управления и пересылаются tooLog Analytics.<br><br>Прямое подключение от tooLog агенты Operations Manager Analytics не требуется. Предупреждения данные будут отправлены из службы анализа журналов toohello репозитория для hello управления группы. |


### <a name="collection-frequency"></a>Частота сбора
- Предупреждения записи являются toohello доступных решений, как только они хранятся в репозитории hello.
- Предупреждения данных отправляется из группы управления tooLog Analytics для hello Operations Manager каждые три минуты.  

## <a name="using-hello-solution"></a>С помощью решения hello
При добавлении рабочей области OMS tooyour решение управления оповещениями hello hello **Управление оповещениями** Плитка добавляется tooyour мониторинга OMS.  Эта Плитка отображается число и графическое представление hello число текущие активные оповещения, которые были созданы в рамках hello последние 24 часа.  Этот диапазон времени нельзя изменить.

![Плитка "Управление оповещениями"](media/log-analytics-solution-alert-management/tile.png)

Щелкните hello **Управление оповещениями** плитки приветствия tooopen **Управление оповещениями** панели мониторинга.  панель мониторинга Hello, включает столбцы hello hello в следующей таблице.  Каждый столбец список hello top 10 предупреждений, сопоставляя счетчик указан, критерий столбца hello области и временной диапазон.  Можно выполнить поиск журнала, который предоставляет hello весь список, щелкнув **все** внизу hello hello столбца или щелкнув заголовок столбца hello.

| столбец | Описание |
|:--- |:--- |
| критические оповещения; |Все оповещения с уровнем серьезности "Критическое" группируются по имени.  Щелкните имя оповещения toorun поиска журналов, возвращения всех записей для данного предупреждения. |
| предупреждающие оповещения; |Все оповещения с уровнем серьезности "Предупреждение" группируются по имени.  Щелкните имя оповещения toorun поиска журналов, возвращения всех записей для данного предупреждения. |
| Активные оповещения SCOM |Все оповещения собранные из Operations Manager с помощью любое состояние, отличное от *закрыто* сгруппированы по источнику оповещения, созданные hello. |
| все активные оповещения. |Все оповещения с любым уровнем серьезности группируются по имени. Включает только оповещения Operations Manager с любым состоянием, кроме *Закрыто*. |

При прокрутке вправо toohello hello панели мониторинга перечислены некоторые стандартные запросы, которые можно щелкнуть tooperform [поиска журналов](log-analytics-log-searches.md) для данных предупреждений.

![Панель мониторинга "Управление оповещениями"](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Записи Log Analytics
решение для управления оповещениями Hello анализирует все записи с типом **предупреждения**.  Оповещения создана путем анализа журналов или собираются из Nagios или Zabbix решением hello напрямую не собираются.

решение Hello импортировать предупреждения из System Center Operations Manager и создает соответствующую запись для каждого типа **предупреждения** и SourceSystem из **OpsManager**.  Эти записи имеют свойства hello в hello в следующей таблице:  

| Свойство | Описание |
|:--- |:--- |
| Тип |*Предупреждение* |
| SourceSystem |*OpsManager* |
| AlertContext |Подробные сведения о hello данных элемента, вызвавшего toobe hello предупреждения, созданные в формате XML. |
| AlertDescription |Подробное описание предупреждения hello. |
| AlertId |Идентификатор GUID hello предупреждения. |
| AlertName |Имя предупреждения hello. |
| AlertPriority |Уровень приоритета предупреждения hello. |
| AlertSeverity |Уровень серьезности предупреждения hello. |
| AlertState |Последнее состояние разрешения предупреждения hello. |
| LastModifiedBy |Имя пользователя hello, последним изменившего hello предупреждение. |
| ManagementGroupName |Имя группы управления hello, где было создано предупреждение hello. |
| RepeatCount |Время создания такого же предупреждения hello для hello же наблюдаемом объекте с момента, разрешенным. |
| ResolvedBy |Имя пользователя hello, разрешено hello оповещение. Пусто, если предупреждение hello еще не была разрешена. |
| SourceDisplayName |Отображаемое имя объекта, вызвавшего предупреждение hello наблюдения hello. |
| SourceFullName |Полное имя объекта, вызвавшего предупреждение hello наблюдения hello. |
| TicketId |Идентификатор билета hello оповещение, если среда System Center Operations Manager hello интегрирована с процессом для назначения билетов для оповещений.  Пустой, если идентификатор билета не назначен. |
| TimeGenerated |Дата и время hello предупреждение был создан. |
| TimeLastModified |Дата и время hello предупреждение последнего изменения. |
| TimeRaised |Дата и время hello предупреждение было создано. |
| TimeResolved |Дата и время hello предупреждение было устранено. Пусто, если предупреждение hello еще не была разрешена. |

## <a name="sample-log-searches"></a>Пример поисков журналов
Hello следующей таблице приведен пример запросов поиска журналов для записи оповещений, собранные этого решения. 

| Запрос | Описание |
|:--- |:--- |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR |Критические предупреждения, вызванные во время hello за последние 24 часа |
| Type=Alert AlertSeverity=warning TimeRaised>NOW-24HOUR |Предупреждения, вызванные во время hello за последние 24 часа |
| Type=Alert SourceSystem=OpsManager AlertState!=Closed TimeRaised>NOW-24HOUR &#124; measure count() as Count by SourceDisplayName |Источники с активными оповещениями, возникшее во время выполнения hello за последние 24 часа |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR AlertState!=Closed |Критические оповещения, созданные за последние 24 часа, которые все еще активны в течение hello |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-24HOUR AlertState=Closed |Предупреждения, созданные во время hello за последние 24 часа, закрытые |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; measure count() as Count by AlertSeverity |Предупреждения, вызванные за последний день, сгруппированные по серьезности hello |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; sort RepeatCount desc |Предупреждения, вызванные за последний день, отсортированные по повторяющемуся значению счетчика hello |


>[!NOTE]
> Если рабочую область был обновленного toohello [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то hello предшествующий запросы будут изменены следующие toohello:
>
>| Запрос | Описание |
|:---|:---|
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) |Критические предупреждения, вызванные во время hello за последние 24 часа |
| Alert &#124; where AlertSeverity == "warning" and TimeRaised > ago(24h) |Предупреждения, вызванные во время hello за последние 24 часа |
| Alert &#124; where SourceSystem == "OpsManager" and AlertState != "Closed" and TimeRaised > ago(24h) &#124; summarize Count = count() by SourceDisplayName |Источники с активными оповещениями, возникшее во время выполнения hello за последние 24 часа |
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) and AlertState != "Closed" |Критические оповещения, созданные за последние 24 часа, которые все еще активны в течение hello |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(24h) and AlertState == "Closed" |Предупреждения, созданные во время hello за последние 24 часа, закрытые |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; summarize Count = count() by AlertSeverity |Предупреждения, вызванные за последний день, сгруппированные по серьезности hello |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; sort by RepeatCount desc |Предупреждения, вызванные за последний день, отсортированные по повторяющемуся значению счетчика hello |


## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о генерации оповещений из Log Analytics см. в статье [Оповещения в Log Analytics](log-analytics-alerts.md).
