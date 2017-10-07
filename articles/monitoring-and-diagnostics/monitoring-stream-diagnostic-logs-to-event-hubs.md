---
title: "Журналы диагностики Azure aaaStream tooan пространство имен концентраторов событий | Документы Microsoft"
description: "Узнайте, как toostream диагностики Azure заносит в журнал tooan имен концентраторов событий."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a>Журналы диагностики Azure поток tooan пространство имен концентраторов событий
**[Журналы Azure диагностики](monitoring-overview-of-diagnostic-logs.md)**  может передаваться в соседние приложения tooany реального времени, использованию hello встроенных «Export концентраторов tooEvent» параметра hello портала или путем включения hello ИД правила шины службы в параметрах диагностики через hello Azure PowerShell Командлеты или Azure CLI.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>Что можно делать с журналами диагностики и концентраторами событий
Вот лишь несколько способов, которые можно использовать потоковую передачу возможностей для журналов диагностики hello.

* **Поток журналы системы ведения журнала и телеметрии стороны too3rd** — со временем, потоковая передача концентраторов событий будет toopipe механизм hello журналы диагностики в toothird сторонних систем Siem и журнала аналитические решения.
* **Просмотреть состояние службы, потоковой передачи данных tooPowerBI «Горячий путь»** — с помощью концентраторов событий, Stream Analytics и PowerBI, можно легко преобразовать диагностических данных в режиме реального времени аналитики toonear по службами Azure. [В этой статье документации приводятся отличный обзор как tooset копирование концентраторов событий обработки данных с Stream Analytics и использовать PowerBI как Выход](../stream-analytics/stream-analytics-power-bi-dashboard.md). Вот несколько советов по настройке журналов диагностики:
  
  * Концентратор событий для категории журналов диагностики создается автоматически при установите флажок hello hello портала или включить с помощью PowerShell, поэтому вы хотите концентратора событий tooselect hello в пространстве имен hello с именем hello, начинающийся с **аналитики**.
  * Hello после кода SQL — это пример Stream Analytics, tooparse можно использовать все данные журнала hello в таблице PowerBI tooa запроса:

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **Построение пользовательского телеметрии и платформ ведения журнала** – Если уже имеется платформы пользовательские телеметрии или мысли о построении один hello высокомасштабируемых публикации подписки характер концентраторов событий позволяет tooflexibly приема диагностики Заносит в журнал. [. В разделе руководства Dan Rosanova toousing концентраторов событий в платформу телеметрии масштабе](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="enable-streaming-of-diagnostic-logs"></a>Включение потоковой передачи журналов диагностики
Вы можете включить потоковую передачу журналов диагностики программно, через портал hello, или с помощью hello [интерфейсы API REST Azure монитор](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings). В любом случае создание параметра диагностики укажите пространство имен концентраторов событий и категории журнала hello и метрики, необходимо toosend в пространстве имен toohello. Концентратор событий создается в пространстве имен hello для каждой категории журнала, в которую включен. Категория **журналов диагностики** — это тип журналов, которые может собирать ресурс.

> [!WARNING]
> Для включения и потоковой передачи журналов диагностики из вычислительных ресурсов (например, виртуальных машин или Service Fabric) [используется другая последовательность действий](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

Hello служебной шины или концентраторов событий, пространство имен не имеет toobe в hello той же подписке, hello ресурсов выпуска журналы при условии, что hello пользователь, настраивающий приветствия имеет соответствующий RBAC доступа tooboth подписок.

## <a name="stream-diagnostic-logs-using-hello-portal"></a>Журналы диагностики потока с помощью портала hello
1. На портале hello перейдите tooAzure монитор и нажмите на **параметров диагностики**

    ![Раздел мониторинга Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. При необходимости фильтровать список hello по группе ресурсов или тип ресурса, а затем щелкните hello ресурсов, для которого вы хотите tooset параметра диагностики.

3. Если параметры не существует в hello ресурс, который вы выбрали, не запрошенные toocreate параметр. Щелкните Turn on diagnostics (Включить диагностику).

   ![Добавление параметра диагностики — имеющиеся параметры отсутствуют](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   Если имеются существующие параметры ресурсов hello, вы увидите список параметров, уже настроен на этом ресурсе. Нажмите Add diagnostic setting (Добавить параметр диагностики).

   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. Присвойте имя параметра и установите флажок "hello" для **концентратора событий потока tooan**, затем выберите пространство имен концентраторов событий.
   
   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   Hello пространство имен выбран будет где создается (если это ваш первый раз, потоковая передача журналов диагностики) или передавать их потоком слишком hello концентратора событий (если уже есть ресурсы, которые передаются потоком пространства имен toothis категории журнала), и политика hello определяет hello разрешения, которые имеет механизм потоковой передачи hello. В настоящее время концентратора событий потоковой передачи tooan требуются разрешения на прослушивание, передачу и управление. Можно создать или изменить политики доступа общих имен концентраторов событий hello портала на вкладке Настройка hello для пространства имен. tooupdate один из этих параметров диагностики, hello клиента необходимо разрешение hello ListKey на правило авторизации hello концентраторов событий.

4. Щелкните **Сохранить**.

Через несколько секунд hello новый параметр отображается в списке параметров для данного ресурса и журналы диагностики передаются потоком toothat учетной записи хранилища, как только создается новый данные события.

### <a name="via-powershell-cmdlets"></a>С помощью командлетов PowerShell
потоковой передачи через hello tooenable [командлеты PowerShell Azure](insights-powershell-samples.md), можно использовать hello `Set-AzureRmDiagnosticSetting` командлет со следующими параметрами:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

Hello ИД правила Service Bus представляет собой строку следующего формата: `{Service Bus resource ID}/authorizationrules/{key name}`, например `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.

### <a name="via-azure-cli"></a>С помощью интерфейса командной строки Azure
Потоковая передача через hello tooenable [Azure CLI](insights-cli-samples.md), можно использовать hello `insights diagnostic set` команду следующим образом:

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Используйте hello в том же формате для ИД правила шины службы, как описано для командлета PowerShell hello.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Как использовать данные журнала hello из концентраторов событий?
Ниже приведен пример выходных данных из концентраторов событий.

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| Имя элемента | Description (Описание) |
| --- | --- |
| records |Массив всех событий журнала, включенных в этот набор полезных данных. |
| Twitter в режиме реального |Время, когда hello произошло событие. |
| category |Категория журнала для этого события. |
| resourceId |Идентификатор ресурса для ресурса hello, создавшего это событие. |
| operationName |Имя операции hello. |
| level |необязательный параметр. Указывает уровень событий журнала hello. |
| properties |Свойства события hello. |

Можно просмотреть список всех поставщиков ресурсов, поддерживающих streaming концентраторов tooEvent [здесь](monitoring-overview-of-diagnostic-logs.md).

## <a name="stream-data-from-compute-resources"></a>Потоковая передача данных от вычислительных ресурсов
Можно также осуществлять потоковую передачу журналов диагностики из вычислительных ресурсов с помощью агента hello диагностики Windows Azure. [См. в статье](../event-hubs/event-hubs-streaming-azure-diags-data.md) о tooset этой копии.

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о журналах диагностики Azure](monitoring-overview-of-diagnostic-logs.md)
* [Приступая к работе с концентраторами событий](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

