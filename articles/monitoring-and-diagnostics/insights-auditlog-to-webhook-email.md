---
title: "веб-перехватчика, журнал действий Azure предупреждения о aaaCall | Документы Microsoft"
description: "Маршрут активности журнала событий tooother служб для пользовательских действий. Например, можно отправлять SMS, вести журнал ошибок или уведомлять команду через службу чата или обмена сообщениями."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="22354-104">Вызов webhook для оповещений журнала действий Azure</span><span class="sxs-lookup"><span data-stu-id="22354-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="22354-105">Веб-Перехватчики позволяют tooroute Azure предупреждения системы tooother уведомления для выполнения завершающей обработки или пользовательских действий.</span><span class="sxs-lookup"><span data-stu-id="22354-105">Webhooks allow you tooroute an Azure alert notification tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="22354-106">Можно использовать веб-перехватчика предупреждения tooroute его tooservices, отправляющие SMS, журнал ошибок, уведомление команды через чат и обмена сообщениями службы либо не любое количество других действий.</span><span class="sxs-lookup"><span data-stu-id="22354-106">You can use a webhook on an alert tooroute it tooservices that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="22354-107">В этой статье описывается, как tooset toobe веб-перехватчика вызывается, когда срабатывает оповещение журнал действий Azure.</span><span class="sxs-lookup"><span data-stu-id="22354-107">This article describes how tooset a webhook toobe called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="22354-108">Здесь также показано, какие полезные данные hello веб-hello HTTP POST tooa перехватчика имеет следующий вид.</span><span class="sxs-lookup"><span data-stu-id="22354-108">It also shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span> <span data-ttu-id="22354-109">Сведения по установке hello и схемы для Azure метрики предупреждения [видите эту страницу вместо](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="22354-109">For information on hello setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="22354-110">Можно также настроить журнал действий toosend оповещений по электронной почте при активации.</span><span class="sxs-lookup"><span data-stu-id="22354-110">You can also set up an Activity Log alert toosend email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="22354-111">Эта функция в настоящее время находится в предварительной версии и будет удален в одном из будущих hello.</span><span class="sxs-lookup"><span data-stu-id="22354-111">This feature is currently in preview and will be removed at some point in hello future.</span></span>
>
>

<span data-ttu-id="22354-112">Можно настроить предупреждения журнал действий по hello [командлеты PowerShell Azure](insights-powershell-samples.md#create-metric-alerts), [CLI кросс-платформенных](insights-cli-samples.md#work-with-alerts), или [API REST Azure монитор](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="22354-112">You can set up an Activity Log alert using hello [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="22354-113">В настоящее время невозможно задать один с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="22354-113">Currently, you cannot set one up using hello Azure portal.</span></span>

## <a name="authenticating-hello-webhook"></a><span data-ttu-id="22354-114">Проверка подлинности веб-перехватчика hello</span><span class="sxs-lookup"><span data-stu-id="22354-114">Authenticating hello webhook</span></span>
<span data-ttu-id="22354-115">веб-перехватчика Hello могут проходить проверку подлинности с помощью любого из этих методов:</span><span class="sxs-lookup"><span data-stu-id="22354-115">hello webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="22354-116">**Авторизация на основе маркера** -hello URI сохраняется маркера идентификатором, например, веб-перехватчика`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="22354-116">**Token-based authorization** - hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="22354-117">**Базовую авторизацию** -hello URI сохраняется имя пользователя и пароль, например, веб-перехватчика`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="22354-117">**Basic authorization** - hello webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="22354-118">Схема полезных данных</span><span class="sxs-lookup"><span data-stu-id="22354-118">Payload schema</span></span>
<span data-ttu-id="22354-119">Hello операции POST содержит следующие полезные данные JSON и схемы для всех журнал действий оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="22354-119">hello POST operation contains hello following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="22354-120">Данная схема предназначена аналогичные toohello один используемые метрики оповещений.</span><span class="sxs-lookup"><span data-stu-id="22354-120">This schema is similar toohello one used by metric-based alerts.</span></span>

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| <span data-ttu-id="22354-121">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="22354-121">Element Name</span></span> | <span data-ttu-id="22354-122">Описание</span><span class="sxs-lookup"><span data-stu-id="22354-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="22354-123">status</span><span class="sxs-lookup"><span data-stu-id="22354-123">status</span></span> |<span data-ttu-id="22354-124">Используется для оповещений на основе метрик.</span><span class="sxs-lookup"><span data-stu-id="22354-124">Used for metric alerts.</span></span> <span data-ttu-id="22354-125">Всегда устанавливайте слишком «активированной» для предупреждения в журнал действий.</span><span class="sxs-lookup"><span data-stu-id="22354-125">Always set too"activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="22354-126">context</span><span class="sxs-lookup"><span data-stu-id="22354-126">context</span></span> |<span data-ttu-id="22354-127">Контекст события hello.</span><span class="sxs-lookup"><span data-stu-id="22354-127">Context of hello event.</span></span> |
| <span data-ttu-id="22354-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="22354-128">resourceProviderName</span></span> |<span data-ttu-id="22354-129">поставщик ресурсов Hello hello влияния ресурсов.</span><span class="sxs-lookup"><span data-stu-id="22354-129">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="22354-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="22354-130">conditionType</span></span> |<span data-ttu-id="22354-131">Всегда имеет значение Event.</span><span class="sxs-lookup"><span data-stu-id="22354-131">Always "Event."</span></span> |
| <span data-ttu-id="22354-132">name</span><span class="sxs-lookup"><span data-stu-id="22354-132">name</span></span> |<span data-ttu-id="22354-133">Имя правила оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="22354-133">Name of hello alert rule.</span></span> |
| <span data-ttu-id="22354-134">id</span><span class="sxs-lookup"><span data-stu-id="22354-134">id</span></span> |<span data-ttu-id="22354-135">Идентификатор ресурса hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="22354-135">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="22354-136">Описание</span><span class="sxs-lookup"><span data-stu-id="22354-136">description</span></span> |<span data-ttu-id="22354-137">Описание предупреждения как набор во время создания оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="22354-137">Alert description as set during creation of hello alert.</span></span> |
| <span data-ttu-id="22354-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="22354-138">subscriptionId</span></span> |<span data-ttu-id="22354-139">Идентификатор подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="22354-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="22354-140">Timestamp</span><span class="sxs-lookup"><span data-stu-id="22354-140">timestamp</span></span> |<span data-ttu-id="22354-141">Время, на какие hello было создано событие hello служба Azure, которая обработала запрос hello.</span><span class="sxs-lookup"><span data-stu-id="22354-141">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="22354-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="22354-142">resourceId</span></span> |<span data-ttu-id="22354-143">Идентификатор ресурса hello влияния ресурсов.</span><span class="sxs-lookup"><span data-stu-id="22354-143">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="22354-144">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="22354-144">resourceGroupName</span></span> |<span data-ttu-id="22354-145">Имя группы ресурсов hello hello затронуто ресурсов</span><span class="sxs-lookup"><span data-stu-id="22354-145">Name of hello resource group for hello impacted resource</span></span> |
| <span data-ttu-id="22354-146">properties</span><span class="sxs-lookup"><span data-stu-id="22354-146">properties</span></span> |<span data-ttu-id="22354-147">Набор `<Key, Value>` пары (т. е. `Dictionary<String, String>`), содержит сведения о событии hello.</span><span class="sxs-lookup"><span data-stu-id="22354-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="22354-148">event</span><span class="sxs-lookup"><span data-stu-id="22354-148">event</span></span> |<span data-ttu-id="22354-149">Элемент, который содержит метаданные о событии hello.</span><span class="sxs-lookup"><span data-stu-id="22354-149">Element containing metadata about hello event.</span></span> |
| <span data-ttu-id="22354-150">authorization</span><span class="sxs-lookup"><span data-stu-id="22354-150">authorization</span></span> |<span data-ttu-id="22354-151">Hello свойства RBAC события hello.</span><span class="sxs-lookup"><span data-stu-id="22354-151">hello RBAC properties of hello event.</span></span> <span data-ttu-id="22354-152">Обычно они включают hello «действие» и «роль» hello «scope.»</span><span class="sxs-lookup"><span data-stu-id="22354-152">These usually include hello “action”, “role” and hello “scope.”</span></span> |
| <span data-ttu-id="22354-153">category</span><span class="sxs-lookup"><span data-stu-id="22354-153">category</span></span> |<span data-ttu-id="22354-154">Категория событий hello.</span><span class="sxs-lookup"><span data-stu-id="22354-154">Category of hello event.</span></span> <span data-ttu-id="22354-155">Поддерживаются следующие значения: Administrative, Alert, Security, ServiceHealth, Recommendation.</span><span class="sxs-lookup"><span data-stu-id="22354-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="22354-156">caller</span><span class="sxs-lookup"><span data-stu-id="22354-156">caller</span></span> |<span data-ttu-id="22354-157">Адрес электронной почты hello пользователя, выполнившего операцию hello, утверждение имени участника-пользователя или утверждение имени участника-службы на основе доступности.</span><span class="sxs-lookup"><span data-stu-id="22354-157">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="22354-158">Может иметь значение NULL для определенных системных вызовов.</span><span class="sxs-lookup"><span data-stu-id="22354-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="22354-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="22354-159">correlationId</span></span> |<span data-ttu-id="22354-160">Обычно GUID в строковом формате.</span><span class="sxs-lookup"><span data-stu-id="22354-160">Usually a GUID in string format.</span></span> <span data-ttu-id="22354-161">События с correlationId принадлежат toohello большего действие и обычно обладают correlationId.</span><span class="sxs-lookup"><span data-stu-id="22354-161">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="22354-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="22354-162">eventDescription</span></span> |<span data-ttu-id="22354-163">Описание статический текст hello события.</span><span class="sxs-lookup"><span data-stu-id="22354-163">Static text description of hello event.</span></span> |
| <span data-ttu-id="22354-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="22354-164">eventDataId</span></span> |<span data-ttu-id="22354-165">Уникальный идентификатор для события hello.</span><span class="sxs-lookup"><span data-stu-id="22354-165">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="22354-166">eventSource</span><span class="sxs-lookup"><span data-stu-id="22354-166">eventSource</span></span> |<span data-ttu-id="22354-167">Имя hello службы Azure или инфраструктуры созданный hello события.</span><span class="sxs-lookup"><span data-stu-id="22354-167">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="22354-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="22354-168">httpRequest</span></span> |<span data-ttu-id="22354-169">Обычно включает hello «clientRequestId», «clientIpAddress» и «method» (метод HTTP, например PUT).</span><span class="sxs-lookup"><span data-stu-id="22354-169">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="22354-170">level</span><span class="sxs-lookup"><span data-stu-id="22354-170">level</span></span> |<span data-ttu-id="22354-171">Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробно».</span><span class="sxs-lookup"><span data-stu-id="22354-171">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="22354-172">operationId</span><span class="sxs-lookup"><span data-stu-id="22354-172">operationId</span></span> |<span data-ttu-id="22354-173">Как правило, GUID совместно hello событий, соответствующих toosingle операции.</span><span class="sxs-lookup"><span data-stu-id="22354-173">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="22354-174">operationName</span><span class="sxs-lookup"><span data-stu-id="22354-174">operationName</span></span> |<span data-ttu-id="22354-175">Имя операции hello.</span><span class="sxs-lookup"><span data-stu-id="22354-175">Name of hello operation.</span></span> |
| <span data-ttu-id="22354-176">properties</span><span class="sxs-lookup"><span data-stu-id="22354-176">properties</span></span> |<span data-ttu-id="22354-177">Свойства события hello.</span><span class="sxs-lookup"><span data-stu-id="22354-177">Properties of hello event.</span></span> |
| <span data-ttu-id="22354-178">status</span><span class="sxs-lookup"><span data-stu-id="22354-178">status</span></span> |<span data-ttu-id="22354-179">Строка.</span><span class="sxs-lookup"><span data-stu-id="22354-179">String.</span></span> <span data-ttu-id="22354-180">Состояние операции hello.</span><span class="sxs-lookup"><span data-stu-id="22354-180">Status of hello operation.</span></span> <span data-ttu-id="22354-181">Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="22354-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="22354-182">subStatus</span><span class="sxs-lookup"><span data-stu-id="22354-182">subStatus</span></span> |<span data-ttu-id="22354-183">Обычно содержит код состояния HTTP hello hello соответствующего вызова REST.</span><span class="sxs-lookup"><span data-stu-id="22354-183">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="22354-184">Может также включать другие строки, описывающие подсостояние.</span><span class="sxs-lookup"><span data-stu-id="22354-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="22354-185">Обычные значения подсостояния: OK (код состояния HTTP: 200), Created (код состояния HTTP: 201), Accepted (код состояния HTTP: 202), No Content (код состояния HTTP: 204), Bad Request (код состояния HTTP: 400), Not Found (код состояния HTTP: 404), Conflict (код состояния HTTP: 409), Internal Server Error (код состояния HTTP: 500), Service Unavailable (код состояния HTTP: 503), Gateway Timeout (код состояния HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="22354-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="22354-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22354-186">Next steps</span></span>
* [<span data-ttu-id="22354-187">Дополнительные сведения о hello журнал действий</span><span class="sxs-lookup"><span data-stu-id="22354-187">Learn more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="22354-188">Выполнение скриптов службы автоматизации Azure (Runbooks) на основе оповещений Azure</span><span class="sxs-lookup"><span data-stu-id="22354-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="22354-189">[Используйте логику приложения toosend SMS через Twilio из Azure предупреждения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="22354-189">[Use Logic App toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="22354-190">В этом примере — для метрики оповещений, но может быть измененный toowork с предупреждением журнал действий.</span><span class="sxs-lookup"><span data-stu-id="22354-190">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="22354-191">[Используйте приложение логики toosend резерв сообщение от Azure предупреждение](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="22354-191">[Use Logic App toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="22354-192">В этом примере — для метрики оповещений, но может быть измененный toowork с предупреждением журнал действий.</span><span class="sxs-lookup"><span data-stu-id="22354-192">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="22354-193">[Используйте логику приложения toosend tooan сообщения очереди Azure на основе Azure предупреждения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="22354-193">[Use Logic App toosend a message tooan Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="22354-194">В этом примере — для метрики оповещений, но может быть измененный toowork с предупреждением журнал действий.</span><span class="sxs-lookup"><span data-stu-id="22354-194">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
