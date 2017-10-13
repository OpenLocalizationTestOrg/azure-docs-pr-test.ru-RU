---
title: "Решение для управления оповещениями в Operations Management Suite (OMS) | Документация Майкрософт"
description: "Решение для управления оповещениями в Log Analytics помогает анализировать все оповещения в вашей среде.  Помимо консолидации оповещений, созданных в OMS, оно импортирует в Log Analytics оповещения из подключенных групп управления System Center Operations Manager."
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
ms.openlocfilehash: 4a394ead09794c52e92dbd2db8be8166d1fab83b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>Решение управления оповещениями в Operations Management Suite (OMS)

![Значок "Управление оповещениями"](media/log-analytics-solution-alert-management/icon.png)

Решение для управления оповещениями помогает анализировать все оповещения в репозитории Log Analytics.  Эти оповещения могут поступать из различных источников, например [созданных службой Log Analytics](log-analytics-alerts.md) или [импортированных из Nagios или Zabbix](log-analytics-linux-agents.md).  Это решение также импортирует оповещения из всех [подключенных групп управления System Center Operations Manager](log-analytics-om-agents.md).

## <a name="prerequisites"></a>Предварительные требования
Решение работает с любыми записями в репозитории Log Analytics, имеющими тип **Alert** (Оповещение), поэтому необходимо выполнить настройку, которая требуется для сбора этих записей.

- Для оповещений Log Analytics [создайте правила генерации оповещений](log-analytics-alerts.md), чтобы записи оповещений создавались непосредственно в репозитории.
- Для оповещений Nagios и Zabbix [настройте соответствующие серверы](log-analytics-linux-agents.md) на отправку оповещений в Log Analytics.
- Для оповещений System Center Operations Manager [подключите группу управления Operations Manager к рабочей области Log Analytics](log-analytics-om-agents.md).  Все оповещения, созданные в System Center Operations Manager, импортируются в Log Analytics.  

## <a name="configuration"></a>Конфигурация
Добавьте решение управления оповещениями в рабочую область OMS, как описано в статье [Добавление решений](log-analytics-add-solutions.md).  Дополнительная настройка не требуется.

## <a name="management-packs"></a>Пакеты управления
Если группа управления System Center Operations Manager подключена к рабочей области OMS, то при добавлении этого решения в System Center Operations Manager будут установлены следующие пакеты.  Для этих пакетов управления не требуются настройка или обслуживание.  

* Управление оповещениями Microsoft System Center Advisor (Microsoft.IntelligencePacks.AlertManagement)

Дополнительные сведения об обновлении пакетов управления для решений см. в статье [Подключение Operations Manager к Log Analytics](log-analytics-om-agents.md).

## <a name="data-collection"></a>Сбор данных
### <a name="agents"></a>Агенты
В следующей таблице описаны подключенные источники, которые поддерживаются этим решением.

| Подключенный источник | Поддержка | Описание |
|:--- |:--- |:--- |
| [Агенты Windows](log-analytics-windows-agents.md) | Нет |Прямые агенты Windows не создают оповещения.  Оповещения Log Analytics могут создаваться на основании событий и данных о производительности, собранных из агентов Windows. |
| [Агенты Linux](log-analytics-linux-agents.md) | Нет |Прямые агенты Linux не создают оповещения.  Оповещения Log Analytics могут создаваться на основании событий и данных о производительности, собранных из агентов Linux.  Оповещения Nagios и Zabbix собираются с тех серверов, для которых требуется агент Linux. |
| [Группа управления System Center Operations Manager](log-analytics-om-agents.md) |Да |Оповещения, созданные в агентах System Center Operations Manager, поступают в группу управления и пересылаются в Log Analytics.<br><br>Прямое подключение агентов Operations Manager к Log Analytics не требуется. Данные об оповещениях пересылаются из группы управления в репозиторий Log Analytics. |


### <a name="collection-frequency"></a>Частота сбора
- Записи оповещений становятся доступными для решения, как только они сохраняются в репозитории.
- Данные оповещений отправляются в Log Analytics из группы управления System Center Operations Manager каждые 3 минуты.  

## <a name="using-the-solution"></a>Использование решения
Когда вы добавите решение по управлению оповещениями в рабочую область OMS, на панели мониторинга OMS появится плитка **Управление оповещениями**.  Она отображает число (и соответствующее графическое представление) активных оповещений, созданных за последние 24 часа.  Этот диапазон времени нельзя изменить.

![Плитка "Управление оповещениями"](media/log-analytics-solution-alert-management/tile.png)

Щелкните плитку **Управление оповещениями**, чтобы открыть панель мониторинга **Управление оповещениями**.  Панель мониторинга содержит столбцы, перечисленные в приведенной ниже таблице.  Каждый столбец содержит десять самых частых оповещений, соответствующих выбранным критериям для данного столбца указанной области действия и за указанный период.  Можно выполнить поиск журналов, выводящий весь список, щелкнув элемент **Просмотреть все** внизу столбца или заголовок этого столбца.

| столбец | Описание |
|:--- |:--- |
| критические оповещения; |Все оповещения с уровнем серьезности "Критическое" группируются по имени.  Щелкните имя оповещения, чтобы выполнить поиск журналов, возвращающий все записи для данного оповещения. |
| предупреждающие оповещения; |Все оповещения с уровнем серьезности "Предупреждение" группируются по имени.  Щелкните имя оповещения, чтобы выполнить поиск журналов, возвращающий все записи для данного оповещения. |
| Активные оповещения SCOM |Все оповещения, собранные из Operations Manager, с любым состоянием, кроме *Закрыто*, группируются по источнику оповещения. |
| все активные оповещения. |Все оповещения с любым уровнем серьезности группируются по имени. Включает только оповещения Operations Manager с любым состоянием, кроме *Закрыто*. |

Если прокрутить панель мониторинга вправо, там вы найдете несколько распространенных запросов. Любой запрос можно щелкнуть, чтобы выполнить [поиск по журналам](log-analytics-log-searches.md) и получить информацию об оповещениях.

![Панель мониторинга "Управление оповещениями"](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Записи Log Analytics
Решение для управления оповещениями анализирует все записи с типом **Alert**.  Оповещения, созданные Log Analytics или собранные из Nagios или Zabbix, не направляются в решение напрямую.

Решение импортирует оповещения из System Center Operations Manager и создает соответствующую запись для каждого оповещения, для которого указан тип **Alert**, а SourceSystem имеет значение **OpsManager**.  У этих записей есть свойства, приведенные в таблице ниже.  

| Свойство | Описание |
|:--- |:--- |
| Тип |*Предупреждение* |
| SourceSystem |*OpsManager* |
| AlertContext |Подробные сведения об элементе данных, вызвавшем создание оповещения в формате XML. |
| AlertDescription |Подробное описание оповещения. |
| AlertId |GUID оповещения. |
| AlertName |Имя оповещения. |
| AlertPriority |Приоритет оповещения. |
| AlertSeverity |Серьезность оповещения. |
| AlertState |Последнее состояние разрешения для предупреждения. |
| LastModifiedBy |Имя последнего пользователя, изменившего оповещение. |
| ManagementGroupName |Имя группы управления, где было создано оповещение. |
| RepeatCount |Указывает, сколько раз было создано такое оповещение для того же отслеживаемого объекта с момента разрешения. |
| ResolvedBy |Имя пользователя, разрешившего оповещение. Пусто, если оповещение пока не разрешено. |
| SourceDisplayName |Отображаемое имя отслеживаемого объекта, сгенерировавшего оповещение. |
| SourceFullName |Полное имя отслеживаемого объекта, сгенерировавшего оповещение. |
| TicketId |Идентификатор запроса для предупреждения, если среда System Center Operations Manager дополнена процессом назначения запросов для оповещений.  Пустой, если идентификатор билета не назначен. |
| TimeGenerated |Дата и время создания оповещения. |
| TimeLastModified |Дата и время последнего изменения оповещения. |
| TimeRaised |Дата и время генерации оповещения. |
| TimeResolved |Дата и время разрешения оповещения. Пусто, если оповещение пока не разрешено. |

## <a name="sample-log-searches"></a>Пример поисков журналов
Следующая таблица содержит примеры поисков по журналам для получения записей оповещений, собранных этим решением. 

| Запрос | Описание |
|:--- |:--- |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR |Критические оповещения, созданные за последние 24 часа. |
| Type=Alert AlertSeverity=warning TimeRaised>NOW-24HOUR |Предупредительные оповещения, созданные за последние 24 часа. |
| Type=Alert SourceSystem=OpsManager AlertState!=Closed TimeRaised>NOW-24HOUR &#124; measure count() as Count by SourceDisplayName |Источники с активными оповещениями, возникшие за последние 24 часа. |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR AlertState!=Closed |Все критические оповещения, созданные за последние 24 часа и остающиеся активными. |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-24HOUR AlertState=Closed |Все критические оповещения, созданные за последние 24 часа и уже закрытые. |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; measure count() as Count by AlertSeverity |Оповещения, созданные за последние 1 день и сгруппированные по уровню серьезности. |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; sort RepeatCount desc |Оповещения, созданные за последние 1 день и сгруппированные по числу повторений. |


>[!NOTE]
> Если ваша рабочая область переведена на [новый язык запросов Log Analytics](log-analytics-log-search-upgrade.md), указанные выше запросы будут изменены следующим образом.
>
>| Запрос | Описание |
|:---|:---|
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) |Критические оповещения, созданные за последние 24 часа. |
| Alert &#124; where AlertSeverity == "warning" and TimeRaised > ago(24h) |Предупредительные оповещения, созданные за последние 24 часа. |
| Alert &#124; where SourceSystem == "OpsManager" and AlertState != "Closed" and TimeRaised > ago(24h) &#124; summarize Count = count() by SourceDisplayName |Источники с активными оповещениями, возникшие за последние 24 часа. |
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) and AlertState != "Closed" |Все критические оповещения, созданные за последние 24 часа и остающиеся активными. |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(24h) and AlertState == "Closed" |Все критические оповещения, созданные за последние 24 часа и уже закрытые. |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; summarize Count = count() by AlertSeverity |Оповещения, созданные за последние 1 день и сгруппированные по уровню серьезности. |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; sort by RepeatCount desc |Оповещения, созданные за последние 1 день и сгруппированные по числу повторений. |


## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о генерации оповещений из Log Analytics см. в статье [Оповещения в Log Analytics](log-analytics-alerts.md).
