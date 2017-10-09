---
title: "Работоспособность решения в OMS aaaAgent | Документы Microsoft"
description: "Эта статья является предполагаемым toohelp понять, как toouse toomonitor это решение hello работоспособности агентов непосредственно reporting tooOMS или System Center Operations Manager."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: magoedte
ms.openlocfilehash: 071b14b4ab7af6680ae458eaa331246755c5bb56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#  <a name="agent-health-solution-in-oms"></a>Решение для мониторинга работоспособности агентов в OMS
Hello агента работоспособности решения в OMS позволяет понять, для всех агентов hello отчетов непосредственно рабочей области OMS toohello или tooOMS подключено групп управления System Center Operations Manager, являющиеся отвечать на запросы и отправка рабочих данных.  Вы можно также хранить список развертывается количество агентов, где они распределены географически и выполнять другие осведомленности toomaintain запросы распределения hello агентов, развернутых в Azure, других облачных средах или в локальной.    

## <a name="prerequisites"></a>Предварительные требования
Прежде чем развертывать это решение, убедитесь в настоящее время установлена поддерживаемая [агентов Windows](../log-analytics/log-analytics-windows-agents.md) отчетов рабочей области OMS toohello или reporting tooan [группы управления Operations Manager](../log-analytics/log-analytics-om-agents.md) интеграции с вашей Рабочая область OMS.    

## <a name="solution-components"></a>Компоненты решения
Это решение состоит из следующих ресурсов, которые добавляются в рабочей области tooyour и непосредственно подключенные агенты или Operations Manager подключенной группы управления hello.

### <a name="management-packs"></a>Пакеты управления
Если группе управления System Center Operations Manager подключенной tooan рабочей области OMS, hello следующие пакеты управления в Operations Manager установлено.  После добавления этого решения пакеты управления также будут установлены на компьютерах с Windows, подключенных напрямую. Нет ничего tooconfigure или управляемые с помощью этих пакетов управления.

* Пакет аналитики канала Direct оценки работоспособности помощника Microsoft System Center (Microsoft.IntelligencePacks.HealthAssessmentDirect)
* Пакет аналитики канала сервера оценки работоспособности помощника Microsoft System Center (Microsoft.IntelligencePacks.HealthAssessmentViaServer).  

Дополнительные сведения об обновлении пакетов управления решения см. в разделе [tooLog подключение Operations Manager Analytics](../log-analytics/log-analytics-om-agents.md).

## <a name="configuration"></a>Конфигурация
Добавить hello агента работоспособности решения tooyour рабочую область OMS hello процесс описывается в [добавить решения](../log-analytics/log-analytics-add-solutions.md). Дополнительная настройка не требуется.


## <a name="data-collection"></a>Сбор данных
### <a name="supported-agents"></a>Поддерживаемые агенты
Привет, в следующей таблице описываются hello подключенных источников, которые поддерживаются в этом решении.

| Подключенный источник | Поддерживаются | Описание |
| --- | --- | --- |
| Агенты Windows | Да | События пульса собираются от прямых агентов Windows.|
| Группа управления System Center Operations Manager | Да | События пульса собираются из агентов группам управления toohello отчетов каждые 60 секунд и затем передается tooLog Analytics. Прямое подключение от tooLog агенты Operations Manager Analytics не требуется. Периодический сигнал событий данные будут отправлены из службы анализа журналов toohello репозитория для hello управления группы.|

## <a name="using-hello-solution"></a>С помощью решения hello
При добавлении рабочая область OMS hello решения tooyour hello **агента работоспособности** плитки будут добавлены tooyour мониторинга OMS. Она отражает hello общее число агентов и количество hello не отвечает агентов в hello последние 24 часа.<br><br> ![Плитка решения "Работоспособность агентов" на панели мониторинга](./media/oms-solution-agenthealth/agenthealth-solution-tile-homepage.png)

Щелкните hello **агента работоспособности** плитки приветствия tooopen **агента работоспособности** панели мониторинга.  панель мониторинга Hello, включает столбцы hello hello в следующей таблице. Каждый столбец перечислены события верхнего десять hello по количеству, соответствующие что столбца критерии для hello указанный диапазон времени. Можно выполнить поиск журнала, который предоставляет hello весь список, выбрав **все** hello справа внизу каждого столбца или щелкните заголовок столбца hello.

| столбец | Описание |
|--------|-------------|
| Число агентов по времени | Тенденция изменения числа агентов в течение семи дней для агентов Linux и Windows.|
| Число агентов, не отвечающих на запросы | Список агентов, которые еще не отправлены периодический сигнал в hello за последние 24 часа.|
| Распределение по типам ОС | Число агентов Windows и Linux в вашей среде.|
| Распределение по версиям агентов | Секция версий другой агент hello, установленных в вашей среде и количество для каждого из них.|
| Распределение по категориям агентов | Секции hello различных категорий агентов, отправляющих события пульса: прямой агентов, агенты OpsMgr или hello сервер управления Operations Manager.|
| Распределение по группам управления | Секция hello различные группы управления SCOM в вашей среде.|
| Географическое расположение агентов | Секция hello разных стран, где имеется агентов и общее число hello число агентов, которые были установлены в каждой стране.|
| Число установленных шлюзов | Hello количество серверов, которые имеют hello установлен шлюз OMS и список этих серверов.|

![Пример панели мониторинга "Работоспособность агентов"](./media/oms-solution-agenthealth/agenthealth-solution-dashboard.png)  

## <a name="log-analytics-records"></a>Записи Log Analytics
Hello решение создает один тип записи в репозиторий OMS hello.  

### <a name="heartbeat-records"></a>Записи пульсов
Создается запись с типом **Пульс**.  Эти записи имеют свойства hello в hello в следующей таблице.  

| Свойство | Описание |
| --- | --- |
| Тип | *Пульс*|
| Категория | Значение — *Прямой агент*, *Агент SCOM*, или *Сервер управления SCOM*.|
| Компьютер | Имя компьютера.|
| OSType | Операционная система Windows или Linux.|
| OSMajorVersion | Основная версия операционной системы.|
| OSMinorVersion | Второстепенная версия операционной системы.|
| Версия | Версия агента OMS или агента Operations Manager.|
| SCAgentChannel | Значение — *Прямой* и (или) *SCManagementServer*.|
| IsGatewayInstalled | Если шлюз OMS установлен, этот параметр имеет значение *true*, в противном случае — значение *false*.|
| ComputerIP | IP-адрес компьютера hello.|
| RemoteIPCountry | Географическое расположение, в котором развернут компьютер.|
| ManagementGroupName | Имя группы управления Operations Manager.|
| SourceComputerId | Уникальный идентификатор компьютера.|
| RemoteIPLongitude | Долгота географического расположения компьютера.|
| RemoteIPLatitude | Широта географического расположения компьютера.|

Каждый агент отчетов tooan сервера управления Operations Manager отправит две Периодические сигналы, а значение свойства SCAgentChannel будет включать оба **прямой** и **SCManagementServer** в зависимости от того, что Журнал аналитика источники данных и решений, которые вы выбрали в вашей подписке OMS. Если вы вспомните данных из решений, отправляются непосредственно из Operations Manager management server toohello OMS веб-службы, либо из-за hello объем данных, собранных на агенте hello отправляются непосредственно из hello агента tooOMS веб-службы. Для подтверждения события, имеющие значение hello **SCManagementServer**, hello ComputerIP значение — IP-адрес hello hello сервера управления, так как он фактически передаются данные hello.  Для периодических сигналов, устанавливаемый SCAgentChannel слишком**прямой**, это hello общедоступный IP-адрес агента hello.  

## <a name="sample-log-searches"></a>Пример поисков журналов
Hello ниже приводится пример запросов поиска журналов для записей, собранные это решение.

| Запрос | Описание |
| --- | --- |
| Type=Heartbeat &#124; distinct Computer |Общее число агентов |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-24HOURS |Количество агентов отвечать на запросы в hello последние 24 часа |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-15MINUTES |Количество агентов отвечать на запросы в hello последние 15 минут. |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer IN {Type=Heartbeat TimeGenerated>NOW-24HOURS &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Компьютеры в сети (в hello последние 24 часа) |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer NOT IN {Type=Heartbeat TimeGenerated>NOW-30MINUTES &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Общее агенты вне сети в последние 30 минут (hello последние 24 часа) |
| Type=Heartbeat &#124; measure countdistinct(Computer) by OSType |Получение тенденции изменения числа агентов за промежуток времени по типу ОС|
| Type=Heartbeat&#124;measure countdistinct(Computer) by OSType |Распределение по типам ОС |
| Type=Heartbeat&#124;measure countdistinct(Computer) by Version |Распределение по версиям агентов |
| Type=Heartbeat&#124;measure count() by Category |Распределение по категориям агентов |
| Type=Heartbeat&#124;measure countdistinct(Computer) by ManagementGroupName | Распределение по группам управления |
| Type=Heartbeat&#124;measure countdistinct(Computer) by RemoteIPCountry |Географическое расположение агентов |
| Type=Heartbeat IsGatewayInstalled=true&#124;Distinct Computer |Число установленных шлюзов OMS |


>[!NOTE]
> Если рабочую область был обновленного toohello [языка запросов новый журнал аналитики](../log-analytics/log-analytics-log-search-upgrade.md), то hello выше запросы будут изменены следующие toohello.
>
>| Запрос | Описание |
|:---|:---|
| Heartbeat &#124; distinct Computer |Общее число агентов |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(24h) |Количество агентов отвечать на запросы в hello последние 24 часа |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(15m) |Количество агентов отвечать на запросы в hello последние 15 минут. |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer in ((Heartbeat &#124; where TimeGenerated > ago(24h) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Компьютеры в сети (в hello последние 24 часа) |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer !in ((Heartbeat &#124; where TimeGenerated > ago(30m) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Общее агенты вне сети в последние 30 минут (hello последние 24 часа) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Получение тенденции изменения числа агентов за промежуток времени по типу ОС|
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Распределение по типам ОС |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by Version |Распределение по версиям агентов |
| Heartbeat &#124; summarize AggregatedValue = count() by Category |Распределение по категориям агентов |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by ManagementGroupName | Распределение по группам управления |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by RemoteIPCountry |Географическое расположение агентов |
| Heartbeat &#124; where iff(isnotnull(toint(IsGatewayInstalled)), IsGatewayInstalled == true, IsGatewayInstalled == "true") == true &#124; distinct Computer |Число установленных шлюзов OMS |

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о генерации оповещений из Log Analytics см. в статье [Оповещения в Log Analytics](../log-analytics/log-analytics-alerts.md).
