---
title: "Схема событий журнала действий Azure | Документация Майкрософт"
description: "Общие сведения о схеме событий для данных, генерируемых в журнал действий"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: a4ceb822e0ec3e1c1dc31ece1db761834e795f6c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="4f730-103">Схема событий журнала действий Azure</span><span class="sxs-lookup"><span data-stu-id="4f730-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="4f730-104">**Журнал действий Azure** — это журнал с подробными сведениями о событиях на уровне подписки, которые произошли в Azure.</span><span class="sxs-lookup"><span data-stu-id="4f730-104">The **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="4f730-105">В этой статье описывается схема событий по категориям данных.</span><span class="sxs-lookup"><span data-stu-id="4f730-105">This article describes the event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="4f730-106">Administrative</span><span class="sxs-lookup"><span data-stu-id="4f730-106">Administrative</span></span>
<span data-ttu-id="4f730-107">Эта категория содержит записи всех операций создания, обновления, удаления и других действий, которые выполняются через Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4f730-107">This category contains the record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="4f730-108">В качестве примеров типов событий, которые относятся к этой категории, можно назвать "создание виртуальной машины" или "удаление группы безопасности сети". Каждое действие, выполняемое пользователем или приложением с помощью Resource Manager, моделируется как операция с определенным типом ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4f730-108">Examples of the types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="4f730-109">Если тип операции — "запись", "удаление" или "действие", то любые сведения об этой операции (о ее запуске, успешном выполнении или сбое) записываются в категорию "Административная".</span><span class="sxs-lookup"><span data-stu-id="4f730-109">If the operation type is Write, Delete, or Action, the records of both the start and success or fail of that operation are recorded in the Administrative category.</span></span> <span data-ttu-id="4f730-110">Категория "Административная" также включает в себя любые изменения в управлении доступом на основе ролей, которые происходят в подписке.</span><span class="sxs-lookup"><span data-stu-id="4f730-110">The Administrative category also includes any changes to role-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="4f730-111">Пример события</span><span class="sxs-lookup"><span data-stu-id="4f730-111">Sample event</span></span>
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="4f730-112">Описания свойств</span><span class="sxs-lookup"><span data-stu-id="4f730-112">Property descriptions</span></span>
| <span data-ttu-id="4f730-113">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="4f730-113">Element Name</span></span> | <span data-ttu-id="4f730-114">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="4f730-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f730-115">authorization</span><span class="sxs-lookup"><span data-stu-id="4f730-115">authorization</span></span> |<span data-ttu-id="4f730-116">BLOB-объект со свойствами RBAC события.</span><span class="sxs-lookup"><span data-stu-id="4f730-116">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="4f730-117">Обычно включает следующие свойства: action, role и scope.</span><span class="sxs-lookup"><span data-stu-id="4f730-117">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="4f730-118">caller</span><span class="sxs-lookup"><span data-stu-id="4f730-118">caller</span></span> |<span data-ttu-id="4f730-119">Адрес электронной почты пользователя, который выполнил операцию, утверждение имени субъекта-службы или имени участника-пользователя в зависимости от доступности.</span><span class="sxs-lookup"><span data-stu-id="4f730-119">Email address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="4f730-120">каналов</span><span class="sxs-lookup"><span data-stu-id="4f730-120">channels</span></span> |<span data-ttu-id="4f730-121">Одно из следующих значений: Admin или Operation.</span><span class="sxs-lookup"><span data-stu-id="4f730-121">One of the following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="4f730-122">claims</span><span class="sxs-lookup"><span data-stu-id="4f730-122">claims</span></span> |<span data-ttu-id="4f730-123">Токен JWT, который используется Active Directory для аутентификации пользователя или приложения при выполнении этой операции в Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4f730-123">The JWT token used by Active Directory to authenticate the user or application to perform this operation in resource manager.</span></span> |
| <span data-ttu-id="4f730-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="4f730-124">correlationId</span></span> |<span data-ttu-id="4f730-125">Обычно GUID в строковом формате.</span><span class="sxs-lookup"><span data-stu-id="4f730-125">Usually a GUID in the string format.</span></span> <span data-ttu-id="4f730-126">События, которые совместно используют идентификатор correlationId, принадлежат к одному общему действию.</span><span class="sxs-lookup"><span data-stu-id="4f730-126">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="4f730-127">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="4f730-127">description</span></span> |<span data-ttu-id="4f730-128">Статическое описание события в текстовом виде.</span><span class="sxs-lookup"><span data-stu-id="4f730-128">Static text description of an event.</span></span> |
| <span data-ttu-id="4f730-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="4f730-129">eventDataId</span></span> |<span data-ttu-id="4f730-130">Уникальный идентификатор события.</span><span class="sxs-lookup"><span data-stu-id="4f730-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="4f730-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="4f730-131">httpRequest</span></span> |<span data-ttu-id="4f730-132">Большой двоичный объект, описывающий HTTP-запрос.</span><span class="sxs-lookup"><span data-stu-id="4f730-132">Blob describing the Http Request.</span></span> <span data-ttu-id="4f730-133">Обычно включает clientRequestId, clientIpAddress и method (метод HTTP,</span><span class="sxs-lookup"><span data-stu-id="4f730-133">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="4f730-134">например PUT).</span><span class="sxs-lookup"><span data-stu-id="4f730-134">For example, PUT).</span></span> |
| <span data-ttu-id="4f730-135">уровень</span><span class="sxs-lookup"><span data-stu-id="4f730-135">level</span></span> |<span data-ttu-id="4f730-136">Уровень события.</span><span class="sxs-lookup"><span data-stu-id="4f730-136">Level of the event.</span></span> <span data-ttu-id="4f730-137">Одно из следующих значений: "Critical", "Error", "Warning", "Informational" или "Verbose"</span><span class="sxs-lookup"><span data-stu-id="4f730-137">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="4f730-138">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="4f730-138">resourceGroupName</span></span> |<span data-ttu-id="4f730-139">Имя группы ресурсов для затронутого ресурса.</span><span class="sxs-lookup"><span data-stu-id="4f730-139">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="4f730-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="4f730-140">resourceProviderName</span></span> |<span data-ttu-id="4f730-141">Имя поставщика ресурса для затронутого ресурса.</span><span class="sxs-lookup"><span data-stu-id="4f730-141">Name of the resource provider for the impacted resource</span></span> |
| <span data-ttu-id="4f730-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="4f730-142">resourceId</span></span> |<span data-ttu-id="4f730-143">Идентификатор ресурса для затронутого ресурса.</span><span class="sxs-lookup"><span data-stu-id="4f730-143">Resource id of the impacted resource.</span></span> |
| <span data-ttu-id="4f730-144">operationId</span><span class="sxs-lookup"><span data-stu-id="4f730-144">operationId</span></span> |<span data-ttu-id="4f730-145">События, относящиеся к одной операции, совместно используют один GUID.</span><span class="sxs-lookup"><span data-stu-id="4f730-145">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="4f730-146">operationName</span><span class="sxs-lookup"><span data-stu-id="4f730-146">operationName</span></span> |<span data-ttu-id="4f730-147">Имя операции.</span><span class="sxs-lookup"><span data-stu-id="4f730-147">Name of the operation.</span></span> |
| <span data-ttu-id="4f730-148">properties</span><span class="sxs-lookup"><span data-stu-id="4f730-148">properties</span></span> |<span data-ttu-id="4f730-149">Набор пар `<Key, Value>` (например, Dictionary) c подробным описанием события.</span><span class="sxs-lookup"><span data-stu-id="4f730-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="4f730-150">status</span><span class="sxs-lookup"><span data-stu-id="4f730-150">status</span></span> |<span data-ttu-id="4f730-151">Строка, описывающая состояние операции.</span><span class="sxs-lookup"><span data-stu-id="4f730-151">String describing the status of the operation.</span></span> <span data-ttu-id="4f730-152">Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="4f730-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="4f730-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="4f730-153">subStatus</span></span> |<span data-ttu-id="4f730-154">Обычно содержит код состояния HTTP для соответствующего вызова REST, но может содержать и другие строковые описания подсостояния, например: OK (код состояния HTTP: 200); Created (код состояния HTTP: 201); Accepted (код состояния HTTP: 202); No Content (код состояния HTTP: 204); Bad Request (код состояния HTTP: 400); Not Found (код состояния HTTP: 404); Conflict (код состояния HTTP: 409); Internal Server Error (код состояния HTTP: 500); Service Unavailable (код состояния HTTP: 503); Gateway Timeout (код состояния HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="4f730-154">Usually the HTTP status code of the corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="4f730-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="4f730-155">eventTimestamp</span></span> |<span data-ttu-id="4f730-156">Метка времени, когда служба Azure создала событие при обработке соответствующего этому событию запроса.</span><span class="sxs-lookup"><span data-stu-id="4f730-156">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="4f730-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="4f730-157">submissionTimestamp</span></span> |<span data-ttu-id="4f730-158">Метка времени, когда событие стало доступно для запросов.</span><span class="sxs-lookup"><span data-stu-id="4f730-158">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="4f730-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4f730-159">subscriptionId</span></span> |<span data-ttu-id="4f730-160">Идентификатор подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4f730-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="4f730-161">Работоспособность службы</span><span class="sxs-lookup"><span data-stu-id="4f730-161">Service health</span></span>
<span data-ttu-id="4f730-162">Эта категория содержит записи всех инцидентов, связанных с работоспособностью службы, которые произошли в Azure.</span><span class="sxs-lookup"><span data-stu-id="4f730-162">This category contains the record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="4f730-163">В качестве примера типа события из этой категории можно назвать следующее: "В работе SQL Azure в восточной части США наблюдаются простои".</span><span class="sxs-lookup"><span data-stu-id="4f730-163">An example of the type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="4f730-164">Существует шесть разновидностей событий работоспособности службы: "Требуется действие", "Помощь при восстановлении", "Инцидент", "Обслуживание", "Сведения" и "Безопасность". Они отображаются, только если в подписке есть ресурс, на который повлияет данное событие.</span><span class="sxs-lookup"><span data-stu-id="4f730-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in the subscription that would be impacted by the event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="4f730-165">Пример события</span><span class="sxs-lookup"><span data-stu-id="4f730-165">Sample event</span></span>
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="4f730-166">Описания свойств</span><span class="sxs-lookup"><span data-stu-id="4f730-166">Property descriptions</span></span>
<span data-ttu-id="4f730-167">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="4f730-167">Element Name</span></span> | <span data-ttu-id="4f730-168">Описание</span><span class="sxs-lookup"><span data-stu-id="4f730-168">Description</span></span>
-------- | -----------
<span data-ttu-id="4f730-169">каналов</span><span class="sxs-lookup"><span data-stu-id="4f730-169">channels</span></span> | <span data-ttu-id="4f730-170">Одно из следующих значений: Admin или Operation.</span><span class="sxs-lookup"><span data-stu-id="4f730-170">Is one of the following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="4f730-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="4f730-171">correlationId</span></span> | <span data-ttu-id="4f730-172">Обычно GUID в строковом формате.</span><span class="sxs-lookup"><span data-stu-id="4f730-172">Is usually a GUID in the string format.</span></span> <span data-ttu-id="4f730-173">События, относящиеся к одному действию uber, обычно имеют общее значение correlationId.</span><span class="sxs-lookup"><span data-stu-id="4f730-173">Events with that belong to the same uber action usually share the same correlationId.</span></span>
<span data-ttu-id="4f730-174">Описание</span><span class="sxs-lookup"><span data-stu-id="4f730-174">description</span></span> | <span data-ttu-id="4f730-175">Описание события.</span><span class="sxs-lookup"><span data-stu-id="4f730-175">Description of the event.</span></span>
<span data-ttu-id="4f730-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="4f730-176">eventDataId</span></span> | <span data-ttu-id="4f730-177">Уникальный идентификатор события.</span><span class="sxs-lookup"><span data-stu-id="4f730-177">The unique identifier of an event.</span></span>
<span data-ttu-id="4f730-178">eventName</span><span class="sxs-lookup"><span data-stu-id="4f730-178">eventName</span></span> | <span data-ttu-id="4f730-179">Заголовок события.</span><span class="sxs-lookup"><span data-stu-id="4f730-179">The title of the event.</span></span>
<span data-ttu-id="4f730-180">level</span><span class="sxs-lookup"><span data-stu-id="4f730-180">level</span></span> | <span data-ttu-id="4f730-181">Уровень события.</span><span class="sxs-lookup"><span data-stu-id="4f730-181">Level of the event.</span></span> <span data-ttu-id="4f730-182">Одно из следующих значений: "Critical", "Error", "Warning", "Informational" или "Verbose"</span><span class="sxs-lookup"><span data-stu-id="4f730-182">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="4f730-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="4f730-183">resourceProviderName</span></span> | <span data-ttu-id="4f730-184">Имя поставщика ресурсов для затронутого ресурса.</span><span class="sxs-lookup"><span data-stu-id="4f730-184">Name of the resource provider for the impacted resource.</span></span> <span data-ttu-id="4f730-185">Если неизвестно, то значение будет null.</span><span class="sxs-lookup"><span data-stu-id="4f730-185">If not known, this will be null.</span></span>
<span data-ttu-id="4f730-186">тип_ресурса</span><span class="sxs-lookup"><span data-stu-id="4f730-186">resourceType</span></span>| <span data-ttu-id="4f730-187">Тип затронутого ресурса.</span><span class="sxs-lookup"><span data-stu-id="4f730-187">The type of resource of the impacted resource.</span></span> <span data-ttu-id="4f730-188">Если неизвестно, то значение будет null.</span><span class="sxs-lookup"><span data-stu-id="4f730-188">If not known, this will be null.</span></span>
<span data-ttu-id="4f730-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="4f730-189">subStatus</span></span> | <span data-ttu-id="4f730-190">Обычно для событий работоспособности службы имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="4f730-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="4f730-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="4f730-191">eventTimestamp</span></span> | <span data-ttu-id="4f730-192">Метка времени, когда событие журнала было создано и отправлено в журнал действий.</span><span class="sxs-lookup"><span data-stu-id="4f730-192">Timestamp when the log event was generated and submitted to the Activity Log.</span></span>
<span data-ttu-id="4f730-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="4f730-193">submissionTimestamp</span></span> |   <span data-ttu-id="4f730-194">Метка времени, когда событие стало доступным в журнале действий.</span><span class="sxs-lookup"><span data-stu-id="4f730-194">Timestamp when the event became available in the Activity Log.</span></span>
<span data-ttu-id="4f730-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4f730-195">subscriptionId</span></span> | <span data-ttu-id="4f730-196">Подписка Azure, в которой это событие было занесено в журнал.</span><span class="sxs-lookup"><span data-stu-id="4f730-196">The Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="4f730-197">status</span><span class="sxs-lookup"><span data-stu-id="4f730-197">status</span></span> | <span data-ttu-id="4f730-198">Строка, описывающая состояние операции.</span><span class="sxs-lookup"><span data-stu-id="4f730-198">String describing the status of the operation.</span></span> <span data-ttu-id="4f730-199">Распространенные значения: Active (Активно), Resolved (Разрешено).</span><span class="sxs-lookup"><span data-stu-id="4f730-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="4f730-200">operationName</span><span class="sxs-lookup"><span data-stu-id="4f730-200">operationName</span></span> | <span data-ttu-id="4f730-201">Имя операции.</span><span class="sxs-lookup"><span data-stu-id="4f730-201">Name of the operation.</span></span> <span data-ttu-id="4f730-202">Обычно имеет значение Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="4f730-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="4f730-203">category</span><span class="sxs-lookup"><span data-stu-id="4f730-203">category</span></span> | <span data-ttu-id="4f730-204">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="4f730-204">"ServiceHealth"</span></span>
<span data-ttu-id="4f730-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="4f730-205">resourceId</span></span> | <span data-ttu-id="4f730-206">Идентификатор ресурса для затронутого ресурса (если он известен).</span><span class="sxs-lookup"><span data-stu-id="4f730-206">Resource id of the impacted resource, if known.</span></span> <span data-ttu-id="4f730-207">В противном случае указывается идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="4f730-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="4f730-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="4f730-208">Properties.title</span></span> | <span data-ttu-id="4f730-209">Локализованное название этого сообщения.</span><span class="sxs-lookup"><span data-stu-id="4f730-209">The localized title for this communication.</span></span> <span data-ttu-id="4f730-210">По умолчанию используется английский язык.</span><span class="sxs-lookup"><span data-stu-id="4f730-210">English is the default language.</span></span>
<span data-ttu-id="4f730-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="4f730-211">Properties.communication</span></span> | <span data-ttu-id="4f730-212">Локализованные сведения сообщения с разметкой HTML.</span><span class="sxs-lookup"><span data-stu-id="4f730-212">The localized details of the communication with HTML markup.</span></span> <span data-ttu-id="4f730-213">По умолчанию используется английский язык.</span><span class="sxs-lookup"><span data-stu-id="4f730-213">English is the default.</span></span>
<span data-ttu-id="4f730-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="4f730-214">Properties.incidentType</span></span> | <span data-ttu-id="4f730-215">Возможные значения: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security.</span><span class="sxs-lookup"><span data-stu-id="4f730-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="4f730-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="4f730-216">Properties.trackingId</span></span> | <span data-ttu-id="4f730-217">Идентифицирует инцидент, с которым связано это событие.</span><span class="sxs-lookup"><span data-stu-id="4f730-217">Identifies the incident this event is associated with.</span></span> <span data-ttu-id="4f730-218">Используйте его для сопоставления событий, связанных с инцидентом.</span><span class="sxs-lookup"><span data-stu-id="4f730-218">Use this to correlate the events related to an incident.</span></span>
<span data-ttu-id="4f730-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="4f730-219">Properties.impactedServices</span></span> | <span data-ttu-id="4f730-220">Экранированный большой двоичный объект в формате JSON, описывающий службы и регионы, на которые влияет инцидент.</span><span class="sxs-lookup"><span data-stu-id="4f730-220">An escaped JSON blob which describes the services and regions that are impacted by the incident.</span></span> <span data-ttu-id="4f730-221">Список служб Services, каждая из которых содержит ServiceName, и список регионов ImpactedRegions, каждый из которых содержит RegionName.</span><span class="sxs-lookup"><span data-stu-id="4f730-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="4f730-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="4f730-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="4f730-223">Сообщение на английском языке.</span><span class="sxs-lookup"><span data-stu-id="4f730-223">The communication in English</span></span>
<span data-ttu-id="4f730-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="4f730-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="4f730-225">Сообщение на английском языке с разметкой HTML или в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="4f730-225">The communication in English as either html markup or plain text</span></span>
<span data-ttu-id="4f730-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="4f730-226">Properties.stage</span></span> | <span data-ttu-id="4f730-227">Возможные значения для AssistedRecovery, ActionRequired, Information, Incident, Security: Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="4f730-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="4f730-228">Возможные значения для Maintenance: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete.</span><span class="sxs-lookup"><span data-stu-id="4f730-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="4f730-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="4f730-229">Properties.communicationId</span></span> | <span data-ttu-id="4f730-230">Сообщение, с которым связано это событие.</span><span class="sxs-lookup"><span data-stu-id="4f730-230">The communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="4f730-231">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="4f730-231">Alert</span></span>
<span data-ttu-id="4f730-232">Эта категория содержит записи всех активаций оповещений Azure.</span><span class="sxs-lookup"><span data-stu-id="4f730-232">This category contains the record of all activations of Azure alerts.</span></span> <span data-ttu-id="4f730-233">В качестве примера типа события из этой категории можно назвать следующее: "Процент использования ЦП на виртуальной машине myVM за последние 5 минут превышал 80 %".</span><span class="sxs-lookup"><span data-stu-id="4f730-233">An example of the type of event you would see in this category is "CPU % on myVM has been over 80 for the past 5 minutes."</span></span> <span data-ttu-id="4f730-234">Различные системы Azure работают по принципу оповещений, то есть вы можете определить какое-то правило, и система будет направлять вам уведомление, когда условия этого правила выполняются.</span><span class="sxs-lookup"><span data-stu-id="4f730-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="4f730-235">Каждый раз, когда "активируется" поддерживаемый тип оповещения Azure или выполняются условия для создания уведомления, в эту категорию журнала активности также передается запись об активации.</span><span class="sxs-lookup"><span data-stu-id="4f730-235">Each time a supported Azure alert type 'activates,' or the conditions are met to generate a notification, a record of the activation is also pushed to this category of the Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="4f730-236">Пример события</span><span class="sxs-lookup"><span data-stu-id="4f730-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in the last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="4f730-237">Описания свойств</span><span class="sxs-lookup"><span data-stu-id="4f730-237">Property descriptions</span></span>
| <span data-ttu-id="4f730-238">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="4f730-238">Element Name</span></span> | <span data-ttu-id="4f730-239">Описание</span><span class="sxs-lookup"><span data-stu-id="4f730-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f730-240">caller</span><span class="sxs-lookup"><span data-stu-id="4f730-240">caller</span></span> | <span data-ttu-id="4f730-241">Всегда имеет значение Microsoft.Insights/alertRules.</span><span class="sxs-lookup"><span data-stu-id="4f730-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="4f730-242">каналов</span><span class="sxs-lookup"><span data-stu-id="4f730-242">channels</span></span> | <span data-ttu-id="4f730-243">Всегда имеет значение "Admin, Operation".</span><span class="sxs-lookup"><span data-stu-id="4f730-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="4f730-244">claims</span><span class="sxs-lookup"><span data-stu-id="4f730-244">claims</span></span> | <span data-ttu-id="4f730-245">Большой двоичный объект JSON с именем субъекта-службы (SPN) или типом ресурса обработчика предупреждений.</span><span class="sxs-lookup"><span data-stu-id="4f730-245">JSON blob with the SPN (service principal name), or resource type, of the alert engine.</span></span> |
| <span data-ttu-id="4f730-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="4f730-246">correlationId</span></span> | <span data-ttu-id="4f730-247">Глобальный уникальный идентификатор (GUID) в строковом формате.</span><span class="sxs-lookup"><span data-stu-id="4f730-247">A GUID in the string format.</span></span> |
| <span data-ttu-id="4f730-248">Описание</span><span class="sxs-lookup"><span data-stu-id="4f730-248">description</span></span> |<span data-ttu-id="4f730-249">Статическое текстовое описание события оповещения.</span><span class="sxs-lookup"><span data-stu-id="4f730-249">Static text description of the alert event.</span></span> |
| <span data-ttu-id="4f730-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="4f730-250">eventDataId</span></span> |<span data-ttu-id="4f730-251">Уникальный идентификатор события оповещения.</span><span class="sxs-lookup"><span data-stu-id="4f730-251">Unique identifier of the alert event.</span></span> |
| <span data-ttu-id="4f730-252">level</span><span class="sxs-lookup"><span data-stu-id="4f730-252">level</span></span> |<span data-ttu-id="4f730-253">Уровень события.</span><span class="sxs-lookup"><span data-stu-id="4f730-253">Level of the event.</span></span> <span data-ttu-id="4f730-254">Одно из следующих значений: "Critical", "Error", "Warning", "Informational" или "Verbose"</span><span class="sxs-lookup"><span data-stu-id="4f730-254">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="4f730-255">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="4f730-255">resourceGroupName</span></span> |<span data-ttu-id="4f730-256">Имя группы ресурсов для затронутого ресурса, если это оповещение метрики.</span><span class="sxs-lookup"><span data-stu-id="4f730-256">Name of the resource group for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="4f730-257">Для других типов оповещений это имя группы ресурсов, содержащей само оповещение.</span><span class="sxs-lookup"><span data-stu-id="4f730-257">For other alert types, this is the name of the resource group that contains the alert itself.</span></span> |
| <span data-ttu-id="4f730-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="4f730-258">resourceProviderName</span></span> |<span data-ttu-id="4f730-259">Имя поставщика ресурсов для затронутого ресурса, если это оповещение метрики.</span><span class="sxs-lookup"><span data-stu-id="4f730-259">Name of the resource provider for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="4f730-260">Для других типов оповещений это имя поставщика ресурсов для самого оповещения.</span><span class="sxs-lookup"><span data-stu-id="4f730-260">For other alert types, this is the name of the resource provider for the alert itself.</span></span> |
| <span data-ttu-id="4f730-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="4f730-261">resourceId</span></span> | <span data-ttu-id="4f730-262">Имя идентификатора ресурса для затронутого ресурса, если это оповещение метрики.</span><span class="sxs-lookup"><span data-stu-id="4f730-262">Name of the resource ID for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="4f730-263">Для других типов оповещений это идентификатор ресурса самого ресурса оповещения.</span><span class="sxs-lookup"><span data-stu-id="4f730-263">For other alert types, this is the resource ID of the alert resource itself.</span></span> |
| <span data-ttu-id="4f730-264">operationId</span><span class="sxs-lookup"><span data-stu-id="4f730-264">operationId</span></span> |<span data-ttu-id="4f730-265">События, относящиеся к одной операции, совместно используют один GUID.</span><span class="sxs-lookup"><span data-stu-id="4f730-265">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="4f730-266">operationName</span><span class="sxs-lookup"><span data-stu-id="4f730-266">operationName</span></span> |<span data-ttu-id="4f730-267">Имя операции.</span><span class="sxs-lookup"><span data-stu-id="4f730-267">Name of the operation.</span></span> |
| <span data-ttu-id="4f730-268">properties</span><span class="sxs-lookup"><span data-stu-id="4f730-268">properties</span></span> |<span data-ttu-id="4f730-269">Набор пар `<Key, Value>` (например, Dictionary) c подробным описанием события.</span><span class="sxs-lookup"><span data-stu-id="4f730-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="4f730-270">status</span><span class="sxs-lookup"><span data-stu-id="4f730-270">status</span></span> |<span data-ttu-id="4f730-271">Строка, описывающая состояние операции.</span><span class="sxs-lookup"><span data-stu-id="4f730-271">String describing the status of the operation.</span></span> <span data-ttu-id="4f730-272">Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="4f730-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="4f730-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="4f730-273">subStatus</span></span> | <span data-ttu-id="4f730-274">Обычно для оповещений имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="4f730-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="4f730-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="4f730-275">eventTimestamp</span></span> |<span data-ttu-id="4f730-276">Метка времени, когда служба Azure создала событие при обработке соответствующего этому событию запроса.</span><span class="sxs-lookup"><span data-stu-id="4f730-276">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="4f730-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="4f730-277">submissionTimestamp</span></span> |<span data-ttu-id="4f730-278">Метка времени, когда событие стало доступно для запросов.</span><span class="sxs-lookup"><span data-stu-id="4f730-278">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="4f730-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4f730-279">subscriptionId</span></span> |<span data-ttu-id="4f730-280">Идентификатор подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4f730-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="4f730-281">Поле свойств по типу оповещения</span><span class="sxs-lookup"><span data-stu-id="4f730-281">Properties field per alert type</span></span>
<span data-ttu-id="4f730-282">Поле свойств будет содержать разные значения в зависимости от источника события оповещения.</span><span class="sxs-lookup"><span data-stu-id="4f730-282">The properties field will contain different values depending on the source of the alert event.</span></span> <span data-ttu-id="4f730-283">Два распространенных поставщика событий оповещений — оповещения журнала действий и оповещения метрик.</span><span class="sxs-lookup"><span data-stu-id="4f730-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="4f730-284">Свойства оповещений журнала действий</span><span class="sxs-lookup"><span data-stu-id="4f730-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="4f730-285">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="4f730-285">Element Name</span></span> | <span data-ttu-id="4f730-286">Описание</span><span class="sxs-lookup"><span data-stu-id="4f730-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f730-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4f730-287">properties.subscriptionId</span></span> | <span data-ttu-id="4f730-288">Идентификатор подписки из события журнала действий, которое вызвало активацию данного правила оповещения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="4f730-288">The subscription ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4f730-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="4f730-289">properties.eventDataId</span></span> | <span data-ttu-id="4f730-290">Идентификатор данных события из события журнала действий, которое вызвало активацию данного правила оповещения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="4f730-290">The event data ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4f730-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="4f730-291">properties.resourceGroup</span></span> | <span data-ttu-id="4f730-292">Идентификатор группы ресурсов из события журнала действий, которое вызвало активацию данного правила оповещения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="4f730-292">The resource group from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4f730-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="4f730-293">properties.resourceId</span></span> | <span data-ttu-id="4f730-294">Идентификатор ресурса из события журнала действий, которое вызвало активацию данного правила оповещения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="4f730-294">The resource ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4f730-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="4f730-295">properties.eventTimestamp</span></span> | <span data-ttu-id="4f730-296">Метка времени события из события журнала действий, которое вызвало активацию данного правила оповещения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="4f730-296">The event timestamp of the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4f730-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="4f730-297">properties.operationName</span></span> | <span data-ttu-id="4f730-298">Имя операции из события журнала действий, которое вызвало активацию данного правила оповещения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="4f730-298">The operation name from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4f730-299">properties.status</span><span class="sxs-lookup"><span data-stu-id="4f730-299">properties.status</span></span> | <span data-ttu-id="4f730-300">Состояние из события журнала действий, которое вызвало активацию данного правила оповещения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="4f730-300">The status from the activity log event which caused this activity log alert rule to be activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="4f730-301">Свойства оповещений метрик</span><span class="sxs-lookup"><span data-stu-id="4f730-301">Properties for metric alerts</span></span>
| <span data-ttu-id="4f730-302">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="4f730-302">Element Name</span></span> | <span data-ttu-id="4f730-303">Описание</span><span class="sxs-lookup"><span data-stu-id="4f730-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f730-304">properties.RuleUri</span><span class="sxs-lookup"><span data-stu-id="4f730-304">properties.RuleUri</span></span> | <span data-ttu-id="4f730-305">Идентификатор ресурса самого правила оповещения метрики.</span><span class="sxs-lookup"><span data-stu-id="4f730-305">Resource ID of the metric alert rule itself.</span></span> |
| <span data-ttu-id="4f730-306">properties.RuleName</span><span class="sxs-lookup"><span data-stu-id="4f730-306">properties.RuleName</span></span> | <span data-ttu-id="4f730-307">Имя правила оповещения метрики.</span><span class="sxs-lookup"><span data-stu-id="4f730-307">The name of the metric alert rule.</span></span> |
| <span data-ttu-id="4f730-308">properties.RuleDescription</span><span class="sxs-lookup"><span data-stu-id="4f730-308">properties.RuleDescription</span></span> | <span data-ttu-id="4f730-309">Описание правила оповещения метрики (как указано в правиле оповещения).</span><span class="sxs-lookup"><span data-stu-id="4f730-309">The description of the metric alert rule (as defined in the alert rule).</span></span> |
| <span data-ttu-id="4f730-310">properties.Threshold</span><span class="sxs-lookup"><span data-stu-id="4f730-310">properties.Threshold</span></span> | <span data-ttu-id="4f730-311">Пороговое значение, используемое для оценки правила оповещения метрики.</span><span class="sxs-lookup"><span data-stu-id="4f730-311">The threshold value used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="4f730-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="4f730-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="4f730-313">Размер окна, используемый для оценки правила оповещения метрики.</span><span class="sxs-lookup"><span data-stu-id="4f730-313">The window size used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="4f730-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="4f730-314">properties.Aggregation</span></span> | <span data-ttu-id="4f730-315">Тип агрегата, определенный в правиле оповещения метрики.</span><span class="sxs-lookup"><span data-stu-id="4f730-315">The aggregation type defined in the metric alert rule.</span></span> |
| <span data-ttu-id="4f730-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="4f730-316">properties.Operator</span></span> | <span data-ttu-id="4f730-317">Условный оператор, используемый для оценки правила оповещения метрики.</span><span class="sxs-lookup"><span data-stu-id="4f730-317">The conditional operator used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="4f730-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="4f730-318">properties.MetricName</span></span> | <span data-ttu-id="4f730-319">Имя метрики, используемой для оценки правила оповещения метрики.</span><span class="sxs-lookup"><span data-stu-id="4f730-319">The metric name of the metric used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="4f730-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="4f730-320">properties.MetricUnit</span></span> | <span data-ttu-id="4f730-321">Единица измерения метрики, используемая для оценки правила оповещения метрики.</span><span class="sxs-lookup"><span data-stu-id="4f730-321">The metric unit for the metric used in the evaluation of the metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="4f730-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="4f730-322">Autoscale</span></span>
<span data-ttu-id="4f730-323">Эта категория содержит записи всех событий, связанных с операциями системы автоматического масштабирования, в основе которой лежат параметры автомасштабирования, определенные в подписке.</span><span class="sxs-lookup"><span data-stu-id="4f730-323">This category contains the record of any events related to the operation of the autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="4f730-324">В качестве примера типа события из этой категории можно назвать следующее: "Не удалось выполнить автоматическое увеличение масштаба".</span><span class="sxs-lookup"><span data-stu-id="4f730-324">An example of the type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="4f730-325">С помощью функции автомасштабирования можно автоматически увеличивать или уменьшать число экземпляров в поддерживаемом типе ресурсов на основе времени суток и (или) загружать данные (метрики), используя параметр автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f730-325">Using autoscale, you can automatically scale out or scale in the number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="4f730-326">Когда выполняются условия для увеличения или уменьшения масштаба, в эту категорию записываются соответствующие события (запуск, успешное выполнение или сбой).</span><span class="sxs-lookup"><span data-stu-id="4f730-326">When the conditions are met to scale up or down, the start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="4f730-327">Пример события</span><span class="sxs-lookup"><span data-stu-id="4f730-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a><span data-ttu-id="4f730-328">Описания свойств</span><span class="sxs-lookup"><span data-stu-id="4f730-328">Property descriptions</span></span>
| <span data-ttu-id="4f730-329">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="4f730-329">Element Name</span></span> | <span data-ttu-id="4f730-330">Описание</span><span class="sxs-lookup"><span data-stu-id="4f730-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f730-331">caller</span><span class="sxs-lookup"><span data-stu-id="4f730-331">caller</span></span> | <span data-ttu-id="4f730-332">Всегда имеет значение Microsoft.Insights/autoscaleSettings.</span><span class="sxs-lookup"><span data-stu-id="4f730-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="4f730-333">каналов</span><span class="sxs-lookup"><span data-stu-id="4f730-333">channels</span></span> | <span data-ttu-id="4f730-334">Всегда имеет значение "Admin, Operation".</span><span class="sxs-lookup"><span data-stu-id="4f730-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="4f730-335">claims</span><span class="sxs-lookup"><span data-stu-id="4f730-335">claims</span></span> | <span data-ttu-id="4f730-336">Большой двоичный объект JSON с именем субъекта-службы (SPN) или типом ресурса системы автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f730-336">JSON blob with the SPN (service principal name), or resource type, of the autoscale engine.</span></span> |
| <span data-ttu-id="4f730-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="4f730-337">correlationId</span></span> | <span data-ttu-id="4f730-338">Глобальный уникальный идентификатор (GUID) в строковом формате.</span><span class="sxs-lookup"><span data-stu-id="4f730-338">A GUID in the string format.</span></span> |
| <span data-ttu-id="4f730-339">Описание</span><span class="sxs-lookup"><span data-stu-id="4f730-339">description</span></span> |<span data-ttu-id="4f730-340">Статическое текстовое описание события автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f730-340">Static text description of the autoscale event.</span></span> |
| <span data-ttu-id="4f730-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="4f730-341">eventDataId</span></span> |<span data-ttu-id="4f730-342">Уникальный идентификатор события автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f730-342">Unique identifier of the autoscale event.</span></span> |
| <span data-ttu-id="4f730-343">level</span><span class="sxs-lookup"><span data-stu-id="4f730-343">level</span></span> |<span data-ttu-id="4f730-344">Уровень события.</span><span class="sxs-lookup"><span data-stu-id="4f730-344">Level of the event.</span></span> <span data-ttu-id="4f730-345">Одно из следующих значений: "Critical", "Error", "Warning", "Informational" или "Verbose"</span><span class="sxs-lookup"><span data-stu-id="4f730-345">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="4f730-346">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="4f730-346">resourceGroupName</span></span> |<span data-ttu-id="4f730-347">Имя группы ресурсов для параметра автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f730-347">Name of the resource group for the autoscale setting.</span></span> |
| <span data-ttu-id="4f730-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="4f730-348">resourceProviderName</span></span> |<span data-ttu-id="4f730-349">Имя поставщика ресурсов для параметра автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f730-349">Name of the resource provider for the autoscale setting.</span></span> |
| <span data-ttu-id="4f730-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="4f730-350">resourceId</span></span> |<span data-ttu-id="4f730-351">Идентификатор ресурса параметра автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f730-351">Resource id of the autoscale setting.</span></span> |
| <span data-ttu-id="4f730-352">operationId</span><span class="sxs-lookup"><span data-stu-id="4f730-352">operationId</span></span> |<span data-ttu-id="4f730-353">События, относящиеся к одной операции, совместно используют один GUID.</span><span class="sxs-lookup"><span data-stu-id="4f730-353">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="4f730-354">operationName</span><span class="sxs-lookup"><span data-stu-id="4f730-354">operationName</span></span> |<span data-ttu-id="4f730-355">Имя операции.</span><span class="sxs-lookup"><span data-stu-id="4f730-355">Name of the operation.</span></span> |
| <span data-ttu-id="4f730-356">properties</span><span class="sxs-lookup"><span data-stu-id="4f730-356">properties</span></span> |<span data-ttu-id="4f730-357">Набор пар `<Key, Value>` (например, Dictionary) c подробным описанием события.</span><span class="sxs-lookup"><span data-stu-id="4f730-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="4f730-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="4f730-358">properties.Description</span></span> | <span data-ttu-id="4f730-359">Подробное описание действий, выполненных системой автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f730-359">Detailed description of what the autoscale engine was doing.</span></span> |
| <span data-ttu-id="4f730-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="4f730-360">properties.ResourceName</span></span> | <span data-ttu-id="4f730-361">Идентификатор ресурса для затронутого ресурса (ресурса, в отношении которого выполнялось действие масштабирования).</span><span class="sxs-lookup"><span data-stu-id="4f730-361">Resource ID of the impacted resource (the resource on which the scale action was being performed)</span></span> |
| <span data-ttu-id="4f730-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="4f730-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="4f730-363">Число экземпляров до выполнения действия автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f730-363">The number of instances before the autoscale action took effect.</span></span> |
| <span data-ttu-id="4f730-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="4f730-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="4f730-365">Число экземпляров после выполнения действия автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f730-365">The number of instances after the autoscale action took effect.</span></span> |
| <span data-ttu-id="4f730-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="4f730-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="4f730-367">Метка времени, когда произошло действие автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f730-367">The timestamp of when the autoscale action occurred.</span></span> |
| <span data-ttu-id="4f730-368">status</span><span class="sxs-lookup"><span data-stu-id="4f730-368">status</span></span> |<span data-ttu-id="4f730-369">Строка, описывающая состояние операции.</span><span class="sxs-lookup"><span data-stu-id="4f730-369">String describing the status of the operation.</span></span> <span data-ttu-id="4f730-370">Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="4f730-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="4f730-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="4f730-371">subStatus</span></span> | <span data-ttu-id="4f730-372">Обычно для автоматического масштабирования имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="4f730-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="4f730-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="4f730-373">eventTimestamp</span></span> |<span data-ttu-id="4f730-374">Метка времени, когда служба Azure создала событие при обработке соответствующего этому событию запроса.</span><span class="sxs-lookup"><span data-stu-id="4f730-374">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="4f730-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="4f730-375">submissionTimestamp</span></span> |<span data-ttu-id="4f730-376">Метка времени, когда событие стало доступно для запросов.</span><span class="sxs-lookup"><span data-stu-id="4f730-376">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="4f730-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4f730-377">subscriptionId</span></span> |<span data-ttu-id="4f730-378">Идентификатор подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4f730-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4f730-379">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f730-379">Next steps</span></span>
* [<span data-ttu-id="4f730-380">Дополнительные сведения о журнале действий (прежнее название — журналы аудита)</span><span class="sxs-lookup"><span data-stu-id="4f730-380">Learn more about the Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="4f730-381">Потоковая передача журнала действий Azure в концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="4f730-381">Stream the Azure Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
