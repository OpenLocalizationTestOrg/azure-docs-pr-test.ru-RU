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
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a><span data-ttu-id="8f476-103">Журналы диагностики Azure поток tooan пространство имен концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="8f476-103">Stream Azure Diagnostic Logs tooan Event Hubs Namespace</span></span>
<span data-ttu-id="8f476-104">**[Журналы Azure диагностики](monitoring-overview-of-diagnostic-logs.md)**  может передаваться в соседние приложения tooany реального времени, использованию hello встроенных «Export концентраторов tooEvent» параметра hello портала или путем включения hello ИД правила шины службы в параметрах диагностики через hello Azure PowerShell Командлеты или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8f476-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time tooany application using hello built-in “Export tooEvent Hubs” option in hello Portal, or by enabling hello Service Bus Rule ID in a diagnostic setting via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="8f476-105">Что можно делать с журналами диагностики и концентраторами событий</span><span class="sxs-lookup"><span data-stu-id="8f476-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="8f476-106">Вот лишь несколько способов, которые можно использовать потоковую передачу возможностей для журналов диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="8f476-106">Here are just a few ways you might use hello streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="8f476-107">**Поток журналы системы ведения журнала и телеметрии стороны too3rd** — со временем, потоковая передача концентраторов событий будет toopipe механизм hello журналы диагностики в toothird сторонних систем Siem и журнала аналитические решения.</span><span class="sxs-lookup"><span data-stu-id="8f476-107">**Stream logs too3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your diagnostic logs in toothird-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="8f476-108">**Просмотреть состояние службы, потоковой передачи данных tooPowerBI «Горячий путь»** — с помощью концентраторов событий, Stream Analytics и PowerBI, можно легко преобразовать диагностических данных в режиме реального времени аналитики toonear по службами Azure.</span><span class="sxs-lookup"><span data-stu-id="8f476-108">**View service health by streaming “hot path” data tooPowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in toonear real-time insights on your Azure services.</span></span> <span data-ttu-id="8f476-109">[В этой статье документации приводятся отличный обзор как tooset копирование концентраторов событий обработки данных с Stream Analytics и использовать PowerBI как Выход](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="8f476-109">[This documentation article gives a great overview of how tooset up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="8f476-110">Вот несколько советов по настройке журналов диагностики:</span><span class="sxs-lookup"><span data-stu-id="8f476-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="8f476-111">Концентратор событий для категории журналов диагностики создается автоматически при установите флажок hello hello портала или включить с помощью PowerShell, поэтому вы хотите концентратора событий tooselect hello в пространстве имен hello с именем hello, начинающийся с **аналитики**.</span><span class="sxs-lookup"><span data-stu-id="8f476-111">An event hub for a category of diagnostic logs is created automatically when you check hello option in hello portal or enable it through PowerShell, so you want tooselect hello event hub in hello namespace with hello name that starts with **insights-**.</span></span>
  * <span data-ttu-id="8f476-112">Hello после кода SQL — это пример Stream Analytics, tooparse можно использовать все данные журнала hello в таблице PowerBI tooa запроса:</span><span class="sxs-lookup"><span data-stu-id="8f476-112">hello following SQL code is a sample Stream Analytics query that you can use tooparse all hello log data in tooa PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="8f476-113">**Построение пользовательского телеметрии и платформ ведения журнала** – Если уже имеется платформы пользовательские телеметрии или мысли о построении один hello высокомасштабируемых публикации подписки характер концентраторов событий позволяет tooflexibly приема диагностики Заносит в журнал.</span><span class="sxs-lookup"><span data-stu-id="8f476-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="8f476-114">[. В разделе руководства Dan Rosanova toousing концентраторов событий в платформу телеметрии масштабе](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="8f476-114">[See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="8f476-115">Включение потоковой передачи журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="8f476-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="8f476-116">Вы можете включить потоковую передачу журналов диагностики программно, через портал hello, или с помощью hello [интерфейсы API REST Azure монитор](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="8f476-116">You can enable streaming of diagnostic logs programmatically, via hello portal, or using hello [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="8f476-117">В любом случае создание параметра диагностики укажите пространство имен концентраторов событий и категории журнала hello и метрики, необходимо toosend в пространстве имен toohello.</span><span class="sxs-lookup"><span data-stu-id="8f476-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and hello log categories and metrics you want toosend in toohello namespace.</span></span> <span data-ttu-id="8f476-118">Концентратор событий создается в пространстве имен hello для каждой категории журнала, в которую включен.</span><span class="sxs-lookup"><span data-stu-id="8f476-118">An event hub is created in hello namespace for each log category you enable.</span></span> <span data-ttu-id="8f476-119">Категория **журналов диагностики** — это тип журналов, которые может собирать ресурс.</span><span class="sxs-lookup"><span data-stu-id="8f476-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="8f476-120">Для включения и потоковой передачи журналов диагностики из вычислительных ресурсов (например, виртуальных машин или Service Fabric) [используется другая последовательность действий](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="8f476-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="8f476-121">Hello служебной шины или концентраторов событий, пространство имен не имеет toobe в hello той же подписке, hello ресурсов выпуска журналы при условии, что hello пользователь, настраивающий приветствия имеет соответствующий RBAC доступа tooboth подписок.</span><span class="sxs-lookup"><span data-stu-id="8f476-121">hello Service Bus or Event Hubs namespace does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="8f476-122">Журналы диагностики потока с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="8f476-122">Stream diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="8f476-123">На портале hello перейдите tooAzure монитор и нажмите на **параметров диагностики**</span><span class="sxs-lookup"><span data-stu-id="8f476-123">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Раздел мониторинга Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="8f476-125">При необходимости фильтровать список hello по группе ресурсов или тип ресурса, а затем щелкните hello ресурсов, для которого вы хотите tooset параметра диагностики.</span><span class="sxs-lookup"><span data-stu-id="8f476-125">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="8f476-126">Если параметры не существует в hello ресурс, который вы выбрали, не запрошенные toocreate параметр.</span><span class="sxs-lookup"><span data-stu-id="8f476-126">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="8f476-127">Щелкните Turn on diagnostics (Включить диагностику).</span><span class="sxs-lookup"><span data-stu-id="8f476-127">Click "Turn on diagnostics."</span></span>

   ![Добавление параметра диагностики — имеющиеся параметры отсутствуют](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="8f476-129">Если имеются существующие параметры ресурсов hello, вы увидите список параметров, уже настроен на этом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="8f476-129">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="8f476-130">Нажмите Add diagnostic setting (Добавить параметр диагностики).</span><span class="sxs-lookup"><span data-stu-id="8f476-130">Click "Add diagnostic setting."</span></span>

   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="8f476-132">Присвойте имя параметра и установите флажок "hello" для **концентратора событий потока tooan**, затем выберите пространство имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="8f476-132">Give your setting a name and check hello box for **Stream tooan event hub**, then select an Event Hubs namespace.</span></span>
   
   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="8f476-134">Hello пространство имен выбран будет где создается (если это ваш первый раз, потоковая передача журналов диагностики) или передавать их потоком слишком hello концентратора событий (если уже есть ресурсы, которые передаются потоком пространства имен toothis категории журнала), и политика hello определяет hello разрешения, которые имеет механизм потоковой передачи hello.</span><span class="sxs-lookup"><span data-stu-id="8f476-134">hello namespace selected will be where hello event hub is created (if this is your first time streaming diagnostic logs) or streamed too(if there are already resources that are streaming that log category toothis namespace), and hello policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="8f476-135">В настоящее время концентратора событий потоковой передачи tooan требуются разрешения на прослушивание, передачу и управление.</span><span class="sxs-lookup"><span data-stu-id="8f476-135">Today, streaming tooan event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="8f476-136">Можно создать или изменить политики доступа общих имен концентраторов событий hello портала на вкладке Настройка hello для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="8f476-136">You can create or modify Event Hubs namespace shared access policies in hello portal under hello Configure tab for your namespace.</span></span> <span data-ttu-id="8f476-137">tooupdate один из этих параметров диагностики, hello клиента необходимо разрешение hello ListKey на правило авторизации hello концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="8f476-137">tooupdate one of these diagnostic settings, hello client must have hello ListKey permission on hello Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="8f476-138">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8f476-138">Click **Save**.</span></span>

<span data-ttu-id="8f476-139">Через несколько секунд hello новый параметр отображается в списке параметров для данного ресурса и журналы диагностики передаются потоком toothat учетной записи хранилища, как только создается новый данные события.</span><span class="sxs-lookup"><span data-stu-id="8f476-139">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are streamed toothat storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="8f476-140">С помощью командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f476-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="8f476-141">потоковой передачи через hello tooenable [командлеты PowerShell Azure](insights-powershell-samples.md), можно использовать hello `Set-AzureRmDiagnosticSetting` командлет со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="8f476-141">tooenable streaming via hello [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use hello `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="8f476-142">Hello ИД правила Service Bus представляет собой строку следующего формата: `{Service Bus resource ID}/authorizationrules/{key name}`, например `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="8f476-142">hello Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="8f476-143">С помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8f476-143">Via Azure CLI</span></span>
<span data-ttu-id="8f476-144">Потоковая передача через hello tooenable [Azure CLI](insights-cli-samples.md), можно использовать hello `insights diagnostic set` команду следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8f476-144">tooenable streaming via hello [Azure CLI](insights-cli-samples.md), you can use hello `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="8f476-145">Используйте hello в том же формате для ИД правила шины службы, как описано для командлета PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="8f476-145">Use hello same format for Service Bus Rule ID as explained for hello PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="8f476-146">Как использовать данные журнала hello из концентраторов событий?</span><span class="sxs-lookup"><span data-stu-id="8f476-146">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="8f476-147">Ниже приведен пример выходных данных из концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="8f476-147">Here is sample output data from Event Hubs:</span></span>

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

| <span data-ttu-id="8f476-148">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="8f476-148">Element Name</span></span> | <span data-ttu-id="8f476-149">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="8f476-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f476-150">records</span><span class="sxs-lookup"><span data-stu-id="8f476-150">records</span></span> |<span data-ttu-id="8f476-151">Массив всех событий журнала, включенных в этот набор полезных данных.</span><span class="sxs-lookup"><span data-stu-id="8f476-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="8f476-152">Twitter в режиме реального</span><span class="sxs-lookup"><span data-stu-id="8f476-152">time</span></span> |<span data-ttu-id="8f476-153">Время, когда hello произошло событие.</span><span class="sxs-lookup"><span data-stu-id="8f476-153">Time at which hello event occurred.</span></span> |
| <span data-ttu-id="8f476-154">category</span><span class="sxs-lookup"><span data-stu-id="8f476-154">category</span></span> |<span data-ttu-id="8f476-155">Категория журнала для этого события.</span><span class="sxs-lookup"><span data-stu-id="8f476-155">Log category for this event.</span></span> |
| <span data-ttu-id="8f476-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="8f476-156">resourceId</span></span> |<span data-ttu-id="8f476-157">Идентификатор ресурса для ресурса hello, создавшего это событие.</span><span class="sxs-lookup"><span data-stu-id="8f476-157">Resource ID of hello resource that generated this event.</span></span> |
| <span data-ttu-id="8f476-158">operationName</span><span class="sxs-lookup"><span data-stu-id="8f476-158">operationName</span></span> |<span data-ttu-id="8f476-159">Имя операции hello.</span><span class="sxs-lookup"><span data-stu-id="8f476-159">Name of hello operation.</span></span> |
| <span data-ttu-id="8f476-160">level</span><span class="sxs-lookup"><span data-stu-id="8f476-160">level</span></span> |<span data-ttu-id="8f476-161">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="8f476-161">Optional.</span></span> <span data-ttu-id="8f476-162">Указывает уровень событий журнала hello.</span><span class="sxs-lookup"><span data-stu-id="8f476-162">Indicates hello log event level.</span></span> |
| <span data-ttu-id="8f476-163">properties</span><span class="sxs-lookup"><span data-stu-id="8f476-163">properties</span></span> |<span data-ttu-id="8f476-164">Свойства события hello.</span><span class="sxs-lookup"><span data-stu-id="8f476-164">Properties of hello event.</span></span> |

<span data-ttu-id="8f476-165">Можно просмотреть список всех поставщиков ресурсов, поддерживающих streaming концентраторов tooEvent [здесь](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="8f476-165">You can view a list of all resource providers that support streaming tooEvent Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="8f476-166">Потоковая передача данных от вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="8f476-166">Stream data from Compute resources</span></span>
<span data-ttu-id="8f476-167">Можно также осуществлять потоковую передачу журналов диагностики из вычислительных ресурсов с помощью агента hello диагностики Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="8f476-167">You can also stream diagnostic logs from Compute resources using hello Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="8f476-168">[См. в статье](../event-hubs/event-hubs-streaming-azure-diags-data.md) о tooset этой копии.</span><span class="sxs-lookup"><span data-stu-id="8f476-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how tooset that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f476-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8f476-169">Next steps</span></span>
* [<span data-ttu-id="8f476-170">Дополнительные сведения о журналах диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="8f476-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="8f476-171">Приступая к работе с концентраторами событий</span><span class="sxs-lookup"><span data-stu-id="8f476-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

