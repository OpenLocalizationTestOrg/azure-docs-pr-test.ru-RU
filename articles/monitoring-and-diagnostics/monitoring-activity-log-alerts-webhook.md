---
title: "aaaUnderstand hello веб-перехватчика схемы, используемой в оповещения журнала действий | Документы Microsoft"
description: "Дополнительные сведения о схеме hello hello JSON, URL-адрес веб-перехватчика tooa учитывается при активации оповещения журнала действий."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="a8b6a-103">Веб-перехватчики для оповещений журнала действий Azure</span><span class="sxs-lookup"><span data-stu-id="a8b6a-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="a8b6a-104">Как часть определения hello группы действий можно настроить веб-перехватчика конечные точки tooreceive активности журнала уведомлений о предупреждениях.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-104">As part of hello definition of an action group, you can configure webhook endpoints tooreceive activity log alert notifications.</span></span> <span data-ttu-id="a8b6a-105">С веб-привязок можно направить эти системы tooother уведомлений для выполнения завершающей обработки или пользовательских действий.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-105">With webhooks, you can route these notifications tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="a8b6a-106">В этой статье показано, какие полезные данные hello веб-hello HTTP POST tooa перехватчика имеет следующий вид.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-106">This article shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span>

<span data-ttu-id="a8b6a-107">Дополнительные сведения об оповещениях журнала действий см. в разделе как слишком[создания предупреждения журнала действий Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="a8b6a-107">For more information on activity log alerts, see how too[create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="a8b6a-108">Сведения о группах действия в разделе как слишком[создания групп действий](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="a8b6a-108">For information on action groups, see how too[create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-hello-webhook"></a><span data-ttu-id="a8b6a-109">Проверка подлинности веб-перехватчика hello</span><span class="sxs-lookup"><span data-stu-id="a8b6a-109">Authenticate hello webhook</span></span>
<span data-ttu-id="a8b6a-110">веб-перехватчика Hello при необходимости можно использовать токены авторизации для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-110">hello webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="a8b6a-111">Здравствуйте, URI сохраняется маркера идентификатором, например, веб-перехватчика `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-111">hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="a8b6a-112">Схема полезных данных</span><span class="sxs-lookup"><span data-stu-id="a8b6a-112">Payload schema</span></span>
<span data-ttu-id="a8b6a-113">полезные данные JSON Hello, содержащихся в hello операции POST различается в зависимости от полей data.context.activityLog.eventSource hello полезных данных.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-113">hello JSON payload contained in hello POST operation differs based on hello payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="a8b6a-114">Common</span><span class="sxs-lookup"><span data-stu-id="a8b6a-114">Common</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a><span data-ttu-id="a8b6a-115">Administrative</span><span class="sxs-lookup"><span data-stu-id="a8b6a-115">Administrative</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a><span data-ttu-id="a8b6a-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="a8b6a-116">ServiceHealth</span></span>
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

<span data-ttu-id="a8b6a-117">Сведения о конкретной схеме оповещений журнала действий для уведомлений о работоспособности службы см. в статье [Уведомления о работоспособности службы](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="a8b6a-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="a8b6a-118">Конкретной схемы на все другие предупреждения журнала действий Подробнее [Обзор журнала действий Azure hello](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a8b6a-118">For specific schema details on all other activity log alerts, see [Overview of hello Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="a8b6a-119">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="a8b6a-119">Element name</span></span> | <span data-ttu-id="a8b6a-120">Описание</span><span class="sxs-lookup"><span data-stu-id="a8b6a-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a8b6a-121">status</span><span class="sxs-lookup"><span data-stu-id="a8b6a-121">status</span></span> |<span data-ttu-id="a8b6a-122">Используется для оповещений на основе метрик.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-122">Used for metric alerts.</span></span> <span data-ttu-id="a8b6a-123">Всегда устанавливайте слишком «активированной» для предупреждения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-123">Always set too"activated" for activity log alerts.</span></span> |
| <span data-ttu-id="a8b6a-124">context</span><span class="sxs-lookup"><span data-stu-id="a8b6a-124">context</span></span> |<span data-ttu-id="a8b6a-125">Контекст события hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-125">Context of hello event.</span></span> |
| <span data-ttu-id="a8b6a-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="a8b6a-126">resourceProviderName</span></span> |<span data-ttu-id="a8b6a-127">поставщик ресурсов Hello hello влияния ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-127">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="a8b6a-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="a8b6a-128">conditionType</span></span> |<span data-ttu-id="a8b6a-129">Всегда имеет значение Event.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-129">Always "Event."</span></span> |
| <span data-ttu-id="a8b6a-130">name</span><span class="sxs-lookup"><span data-stu-id="a8b6a-130">name</span></span> |<span data-ttu-id="a8b6a-131">Имя правила оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-131">Name of hello alert rule.</span></span> |
| <span data-ttu-id="a8b6a-132">id</span><span class="sxs-lookup"><span data-stu-id="a8b6a-132">id</span></span> |<span data-ttu-id="a8b6a-133">Идентификатор ресурса hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-133">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="a8b6a-134">Описание</span><span class="sxs-lookup"><span data-stu-id="a8b6a-134">description</span></span> |<span data-ttu-id="a8b6a-135">Описание предупреждения, задается при создании предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-135">Alert description set when hello alert is created.</span></span> |
| <span data-ttu-id="a8b6a-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="a8b6a-136">subscriptionId</span></span> |<span data-ttu-id="a8b6a-137">Идентификатор подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="a8b6a-138">Timestamp</span><span class="sxs-lookup"><span data-stu-id="a8b6a-138">timestamp</span></span> |<span data-ttu-id="a8b6a-139">Время, на какие hello было создано событие hello служба Azure, которая обработала запрос hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-139">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="a8b6a-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="a8b6a-140">resourceId</span></span> |<span data-ttu-id="a8b6a-141">Идентификатор ресурса hello влияния ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-141">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="a8b6a-142">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="a8b6a-142">resourceGroupName</span></span> |<span data-ttu-id="a8b6a-143">Имя группы ресурсов hello hello влияния ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-143">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="a8b6a-144">properties</span><span class="sxs-lookup"><span data-stu-id="a8b6a-144">properties</span></span> |<span data-ttu-id="a8b6a-145">Набор `<Key, Value>` пары (то есть, `Dictionary<String, String>`), содержит сведения о событии hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="a8b6a-146">event</span><span class="sxs-lookup"><span data-stu-id="a8b6a-146">event</span></span> |<span data-ttu-id="a8b6a-147">Элемент, который содержит метаданные о событии hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-147">Element that contains metadata about hello event.</span></span> |
| <span data-ttu-id="a8b6a-148">authorization</span><span class="sxs-lookup"><span data-stu-id="a8b6a-148">authorization</span></span> |<span data-ttu-id="a8b6a-149">свойства управления доступом на основе ролей Hello hello события.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-149">hello Role-Based Access Control properties of hello event.</span></span> <span data-ttu-id="a8b6a-150">Эти свойства являются действие hello, hello роль и область hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-150">These properties usually include hello action, hello role, and hello scope.</span></span> |
| <span data-ttu-id="a8b6a-151">category</span><span class="sxs-lookup"><span data-stu-id="a8b6a-151">category</span></span> |<span data-ttu-id="a8b6a-152">Категория событий hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-152">Category of hello event.</span></span> <span data-ttu-id="a8b6a-153">Поддерживаются следующие значения: Administrative, Alert, Security, ServiceHealth, Recommendation.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="a8b6a-154">caller</span><span class="sxs-lookup"><span data-stu-id="a8b6a-154">caller</span></span> |<span data-ttu-id="a8b6a-155">Адрес электронной почты hello пользователя, выполнившего операцию hello, утверждение имени участника-пользователя или утверждение имени участника-службы на основе доступности.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-155">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="a8b6a-156">Может иметь значение NULL для определенных системных вызовов.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="a8b6a-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="a8b6a-157">correlationId</span></span> |<span data-ttu-id="a8b6a-158">Обычно GUID в строковом формате.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-158">Usually a GUID in string format.</span></span> <span data-ttu-id="a8b6a-159">События с correlationId принадлежат toohello большего действие и обычно обладают correlationId.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-159">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="a8b6a-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="a8b6a-160">eventDescription</span></span> |<span data-ttu-id="a8b6a-161">Описание статический текст hello события.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-161">Static text description of hello event.</span></span> |
| <span data-ttu-id="a8b6a-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="a8b6a-162">eventDataId</span></span> |<span data-ttu-id="a8b6a-163">Уникальный идентификатор для события hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-163">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="a8b6a-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="a8b6a-164">eventSource</span></span> |<span data-ttu-id="a8b6a-165">Имя hello службы Azure или инфраструктуры созданный hello события.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-165">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="a8b6a-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="a8b6a-166">httpRequest</span></span> |<span data-ttu-id="a8b6a-167">Hello запрос обычно включает hello clientRequestId, clientIpAddress и метод HTTP (например, ПОМЕСТИТЕ).</span><span class="sxs-lookup"><span data-stu-id="a8b6a-167">hello request usually includes hello clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="a8b6a-168">level</span><span class="sxs-lookup"><span data-stu-id="a8b6a-168">level</span></span> |<span data-ttu-id="a8b6a-169">Одно из последующих значений hello: критическое, ошибка, предупреждение, информационное сообщение и Verbose.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-169">One of hello following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="a8b6a-170">operationId</span><span class="sxs-lookup"><span data-stu-id="a8b6a-170">operationId</span></span> |<span data-ttu-id="a8b6a-171">Как правило, GUID совместно hello событий, соответствующих toosingle операции.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-171">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="a8b6a-172">operationName</span><span class="sxs-lookup"><span data-stu-id="a8b6a-172">operationName</span></span> |<span data-ttu-id="a8b6a-173">Имя операции hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-173">Name of hello operation.</span></span> |
| <span data-ttu-id="a8b6a-174">properties</span><span class="sxs-lookup"><span data-stu-id="a8b6a-174">properties</span></span> |<span data-ttu-id="a8b6a-175">Свойства события hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-175">Properties of hello event.</span></span> |
| <span data-ttu-id="a8b6a-176">status</span><span class="sxs-lookup"><span data-stu-id="a8b6a-176">status</span></span> |<span data-ttu-id="a8b6a-177">Строка.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-177">String.</span></span> <span data-ttu-id="a8b6a-178">Состояние операции hello.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-178">Status of hello operation.</span></span> <span data-ttu-id="a8b6a-179">Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="a8b6a-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="a8b6a-180">subStatus</span></span> |<span data-ttu-id="a8b6a-181">Обычно содержит код состояния HTTP hello hello соответствующего вызова REST.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-181">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="a8b6a-182">Может также включать другие строки, описывающие подсостояние.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="a8b6a-183">Обычные значения подсостояния: OK (код состояния HTTP: 200), Created (код состояния HTTP: 201), Accepted (код состояния HTTP: 202), No Content (код состояния HTTP: 204), Bad Request (код состояния HTTP: 400), Not Found (код состояния HTTP: 404), Conflict (код состояния HTTP: 409), Internal Server Error (код состояния HTTP: 500), Service Unavailable (код состояния HTTP: 503), Gateway Timeout (код состояния HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="a8b6a-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a8b6a-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8b6a-184">Next steps</span></span>
* <span data-ttu-id="a8b6a-185">[Дополнительные сведения о журнале действий hello](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a8b6a-185">[Learn more about hello activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="a8b6a-186">[Using Azure Automation to take action on Azure Alerts](http://go.microsoft.com/fwlink/?LinkId=627081) (Использование службы автоматизации Azure для выполнения действий по уведомлениям Azure).</span><span class="sxs-lookup"><span data-stu-id="a8b6a-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="a8b6a-187">[Используйте логику приложения toosend SMS через Twilio из Azure предупреждения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a8b6a-187">[Use a logic app toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="a8b6a-188">Этот пример предназначен для метрики оповещений, но может быть измененный toowork с предупреждением журнала действий.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-188">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="a8b6a-189">[Используйте логику приложения toosend резерв сообщение от Azure предупреждение](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a8b6a-189">[Use a logic app toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="a8b6a-190">Этот пример предназначен для метрики оповещений, но может быть измененный toowork с предупреждением журнала действий.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-190">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="a8b6a-191">[Использовать toosend логику приложения, очередь сообщений tooan Azure из Azure предупреждения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a8b6a-191">[Use a logic app toosend a message tooan Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="a8b6a-192">Этот пример предназначен для метрики оповещений, но может быть измененный toowork с предупреждением журнала действий.</span><span class="sxs-lookup"><span data-stu-id="a8b6a-192">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
