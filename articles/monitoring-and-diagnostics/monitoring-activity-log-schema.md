---
title: "Схема событий журнала активности aaaAzure | Документы Microsoft"
description: "Понимание hello схемы событий для данных, которые передаются в журнал действий hello"
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
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="7c483-103">Схема событий журнала действий Azure</span><span class="sxs-lookup"><span data-stu-id="7c483-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="7c483-104">Hello **журнал действий Azure** — это журнал, позволяет контролировать все события уровня подписки, которые произошли в Azure.</span><span class="sxs-lookup"><span data-stu-id="7c483-104">hello **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="7c483-105">Данная статья содержит hello схема событий в категории данных.</span><span class="sxs-lookup"><span data-stu-id="7c483-105">This article describes hello event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="7c483-106">Administrative</span><span class="sxs-lookup"><span data-stu-id="7c483-106">Administrative</span></span>
<span data-ttu-id="7c483-107">Эта категория содержит запись hello всех создавать, выполнять операции обновления, удаления и action через диспетчер ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c483-107">This category contains hello record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="7c483-108">Примеры типов событий, отображаемые в этой категории относятся hello «создайте виртуальную машину» и «удалить сетевую группу безопасности «всех действий, выполненных пользователем или приложения с помощью диспетчера ресурсов моделируется как операцию для определенного типа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c483-108">Examples of hello types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="7c483-109">Если тип операции hello записи, Delete или действие, hello начала hello и успех или сбой данной операции записываются в hello административную категорию.</span><span class="sxs-lookup"><span data-stu-id="7c483-109">If hello operation type is Write, Delete, or Action, hello records of both hello start and success or fail of that operation are recorded in hello Administrative category.</span></span> <span data-ttu-id="7c483-110">Административная категория Hello также включает любой элемент управления доступом на основе toorole изменения в подписку.</span><span class="sxs-lookup"><span data-stu-id="7c483-110">hello Administrative category also includes any changes toorole-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7c483-111">Пример события</span><span class="sxs-lookup"><span data-stu-id="7c483-111">Sample event</span></span>
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

### <a name="property-descriptions"></a><span data-ttu-id="7c483-112">Описания свойств</span><span class="sxs-lookup"><span data-stu-id="7c483-112">Property descriptions</span></span>
| <span data-ttu-id="7c483-113">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="7c483-113">Element Name</span></span> | <span data-ttu-id="7c483-114">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="7c483-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c483-115">authorization</span><span class="sxs-lookup"><span data-stu-id="7c483-115">authorization</span></span> |<span data-ttu-id="7c483-116">Большой двоичный объект свойства RBAC события hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-116">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="7c483-117">Обычно включает hello свойства «действие», «роль» и «область».</span><span class="sxs-lookup"><span data-stu-id="7c483-117">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="7c483-118">caller</span><span class="sxs-lookup"><span data-stu-id="7c483-118">caller</span></span> |<span data-ttu-id="7c483-119">Адрес электронной почты пользователя hello, который выполнил операцию hello, утверждение имени участника-пользователя или утверждение имени участника-службы на основе доступности.</span><span class="sxs-lookup"><span data-stu-id="7c483-119">Email address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="7c483-120">каналов</span><span class="sxs-lookup"><span data-stu-id="7c483-120">channels</span></span> |<span data-ttu-id="7c483-121">Одно из hello следующие значения: «Администратор», «Операция»</span><span class="sxs-lookup"><span data-stu-id="7c483-121">One of hello following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="7c483-122">claims</span><span class="sxs-lookup"><span data-stu-id="7c483-122">claims</span></span> |<span data-ttu-id="7c483-123">токен JWT Hello используется Active Directory tooauthenticate hello пользователь или приложение tooperform эту операцию в диспетчер ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c483-123">hello JWT token used by Active Directory tooauthenticate hello user or application tooperform this operation in resource manager.</span></span> |
| <span data-ttu-id="7c483-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="7c483-124">correlationId</span></span> |<span data-ttu-id="7c483-125">Как правило, GUID в строковом формате hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-125">Usually a GUID in hello string format.</span></span> <span data-ttu-id="7c483-126">События, которые совместно используют correlationId принадлежат toohello же действию.</span><span class="sxs-lookup"><span data-stu-id="7c483-126">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="7c483-127">Описание</span><span class="sxs-lookup"><span data-stu-id="7c483-127">description</span></span> |<span data-ttu-id="7c483-128">Статическое описание события в текстовом виде.</span><span class="sxs-lookup"><span data-stu-id="7c483-128">Static text description of an event.</span></span> |
| <span data-ttu-id="7c483-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7c483-129">eventDataId</span></span> |<span data-ttu-id="7c483-130">Уникальный идентификатор события.</span><span class="sxs-lookup"><span data-stu-id="7c483-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="7c483-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="7c483-131">httpRequest</span></span> |<span data-ttu-id="7c483-132">BLOB-объектов описания hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="7c483-132">Blob describing hello Http Request.</span></span> <span data-ttu-id="7c483-133">Обычно включает hello «clientRequestId», «clientIpAddress» и «method» (метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="7c483-133">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="7c483-134">например PUT).</span><span class="sxs-lookup"><span data-stu-id="7c483-134">For example, PUT).</span></span> |
| <span data-ttu-id="7c483-135">level</span><span class="sxs-lookup"><span data-stu-id="7c483-135">level</span></span> |<span data-ttu-id="7c483-136">Уровень события hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-136">Level of hello event.</span></span> <span data-ttu-id="7c483-137">Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробный»</span><span class="sxs-lookup"><span data-stu-id="7c483-137">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="7c483-138">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="7c483-138">resourceGroupName</span></span> |<span data-ttu-id="7c483-139">Имя группы ресурсов hello hello влияния ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c483-139">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="7c483-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7c483-140">resourceProviderName</span></span> |<span data-ttu-id="7c483-141">Имя поставщика ресурсов hello hello затронуто ресурсов</span><span class="sxs-lookup"><span data-stu-id="7c483-141">Name of hello resource provider for hello impacted resource</span></span> |
| <span data-ttu-id="7c483-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="7c483-142">resourceId</span></span> |<span data-ttu-id="7c483-143">Идентификатор ресурса hello влияния ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c483-143">Resource id of hello impacted resource.</span></span> |
| <span data-ttu-id="7c483-144">operationId</span><span class="sxs-lookup"><span data-stu-id="7c483-144">operationId</span></span> |<span data-ttu-id="7c483-145">Идентификатор GUID, совместно используемые hello события, которые соответствуют tooa одной операции.</span><span class="sxs-lookup"><span data-stu-id="7c483-145">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="7c483-146">operationName</span><span class="sxs-lookup"><span data-stu-id="7c483-146">operationName</span></span> |<span data-ttu-id="7c483-147">Имя операции hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-147">Name of hello operation.</span></span> |
| <span data-ttu-id="7c483-148">properties</span><span class="sxs-lookup"><span data-stu-id="7c483-148">properties</span></span> |<span data-ttu-id="7c483-149">Набор `<Key, Value>` пары (то есть, словарь), описывающий hello подробных сведениях события hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="7c483-150">status</span><span class="sxs-lookup"><span data-stu-id="7c483-150">status</span></span> |<span data-ttu-id="7c483-151">Строка, описывающая состояние hello hello операции.</span><span class="sxs-lookup"><span data-stu-id="7c483-151">String describing hello status of hello operation.</span></span> <span data-ttu-id="7c483-152">Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="7c483-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="7c483-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="7c483-153">subStatus</span></span> |<span data-ttu-id="7c483-154">Обычно hello hello соответствующего вызова REST код состояния HTTP, но может также включать другие строки, описывающие подсостояния, таких как следующие общие значения: OK (код состояния HTTP: 200), созданный (код состояния HTTP: 201) приняты (код состояния HTTP: 202), нет содержимого (HTTP Код состояния: 204), неправильный запрос (код состояния HTTP: 400), не найдено (код состояния HTTP: 404), конфликт (код состояния HTTP: 409), Внутренняя ошибка сервера (код состояния HTTP: 500), служба недоступна (код состояния HTTP: 503), истекло время ожидания шлюза (код состояния HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="7c483-154">Usually hello HTTP status code of hello corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="7c483-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7c483-155">eventTimestamp</span></span> |<span data-ttu-id="7c483-156">Отметка времени, когда hello событий, созданных hello hello Azure служба обработки запроса соответствующее событие hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-156">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="7c483-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7c483-157">submissionTimestamp</span></span> |<span data-ttu-id="7c483-158">Отметка времени события hello стало доступно для запросов.</span><span class="sxs-lookup"><span data-stu-id="7c483-158">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="7c483-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7c483-159">subscriptionId</span></span> |<span data-ttu-id="7c483-160">Идентификатор подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="7c483-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="7c483-161">Работоспособность службы</span><span class="sxs-lookup"><span data-stu-id="7c483-161">Service health</span></span>
<span data-ttu-id="7c483-162">Эта категория содержит запись hello любой службы работоспособности инцидентов, произошедших в Azure.</span><span class="sxs-lookup"><span data-stu-id="7c483-162">This category contains hello record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="7c483-163">Пример hello тип события, отображаемые в этой категории — «SQL Azure в регионе Восток США испытывает времени простоя».</span><span class="sxs-lookup"><span data-stu-id="7c483-163">An example of hello type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="7c483-164">События работоспособности службы бывают пять видов: требуется действие вспомогательная восстановления, инцидент, обслуживания, сведения и безопасности и появятся только при наличии ресурсов, в подписке hello, которое бы повлиять hello событий.</span><span class="sxs-lookup"><span data-stu-id="7c483-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in hello subscription that would be impacted by hello event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7c483-165">Пример события</span><span class="sxs-lookup"><span data-stu-id="7c483-165">Sample event</span></span>
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
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="7c483-166">Описания свойств</span><span class="sxs-lookup"><span data-stu-id="7c483-166">Property descriptions</span></span>
<span data-ttu-id="7c483-167">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="7c483-167">Element Name</span></span> | <span data-ttu-id="7c483-168">Описание</span><span class="sxs-lookup"><span data-stu-id="7c483-168">Description</span></span>
-------- | -----------
<span data-ttu-id="7c483-169">каналов</span><span class="sxs-lookup"><span data-stu-id="7c483-169">channels</span></span> | <span data-ttu-id="7c483-170">Является одним из hello следующие значения: «Администратор», «Операция»</span><span class="sxs-lookup"><span data-stu-id="7c483-170">Is one of hello following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="7c483-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="7c483-171">correlationId</span></span> | <span data-ttu-id="7c483-172">Обычно представляет собой идентификатор GUID в строковом формате hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-172">Is usually a GUID in hello string format.</span></span> <span data-ttu-id="7c483-173">События, принадлежат toohello же действию обычно обладают hello же correlationId.</span><span class="sxs-lookup"><span data-stu-id="7c483-173">Events with that belong toohello same uber action usually share hello same correlationId.</span></span>
<span data-ttu-id="7c483-174">Описание</span><span class="sxs-lookup"><span data-stu-id="7c483-174">description</span></span> | <span data-ttu-id="7c483-175">Описание события hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-175">Description of hello event.</span></span>
<span data-ttu-id="7c483-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7c483-176">eventDataId</span></span> | <span data-ttu-id="7c483-177">Hello уникальный идентификатор события.</span><span class="sxs-lookup"><span data-stu-id="7c483-177">hello unique identifier of an event.</span></span>
<span data-ttu-id="7c483-178">eventName</span><span class="sxs-lookup"><span data-stu-id="7c483-178">eventName</span></span> | <span data-ttu-id="7c483-179">Заголовок события hello Hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-179">hello title of hello event.</span></span>
<span data-ttu-id="7c483-180">level</span><span class="sxs-lookup"><span data-stu-id="7c483-180">level</span></span> | <span data-ttu-id="7c483-181">Уровень события hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-181">Level of hello event.</span></span> <span data-ttu-id="7c483-182">Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробный»</span><span class="sxs-lookup"><span data-stu-id="7c483-182">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="7c483-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7c483-183">resourceProviderName</span></span> | <span data-ttu-id="7c483-184">Имя поставщика ресурсов hello hello влияния ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c483-184">Name of hello resource provider for hello impacted resource.</span></span> <span data-ttu-id="7c483-185">Если неизвестно, то значение будет null.</span><span class="sxs-lookup"><span data-stu-id="7c483-185">If not known, this will be null.</span></span>
<span data-ttu-id="7c483-186">тип_ресурса</span><span class="sxs-lookup"><span data-stu-id="7c483-186">resourceType</span></span>| <span data-ttu-id="7c483-187">Тип ресурса hello Hello влияния ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c483-187">hello type of resource of hello impacted resource.</span></span> <span data-ttu-id="7c483-188">Если неизвестно, то значение будет null.</span><span class="sxs-lookup"><span data-stu-id="7c483-188">If not known, this will be null.</span></span>
<span data-ttu-id="7c483-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="7c483-189">subStatus</span></span> | <span data-ttu-id="7c483-190">Обычно для событий работоспособности службы имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="7c483-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="7c483-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7c483-191">eventTimestamp</span></span> | <span data-ttu-id="7c483-192">Метка времени hello журнал событий был создан и отправлен toohello журнал действий.</span><span class="sxs-lookup"><span data-stu-id="7c483-192">Timestamp when hello log event was generated and submitted toohello Activity Log.</span></span>
<span data-ttu-id="7c483-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7c483-193">submissionTimestamp</span></span> |   <span data-ttu-id="7c483-194">Отметка времени события hello стала доступна для hello журнал действий.</span><span class="sxs-lookup"><span data-stu-id="7c483-194">Timestamp when hello event became available in hello Activity Log.</span></span>
<span data-ttu-id="7c483-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7c483-195">subscriptionId</span></span> | <span data-ttu-id="7c483-196">Здравствуйте, подписки Azure, в котором было зарегистрировано это событие.</span><span class="sxs-lookup"><span data-stu-id="7c483-196">hello Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="7c483-197">status</span><span class="sxs-lookup"><span data-stu-id="7c483-197">status</span></span> | <span data-ttu-id="7c483-198">Строка, описывающая состояние hello hello операции.</span><span class="sxs-lookup"><span data-stu-id="7c483-198">String describing hello status of hello operation.</span></span> <span data-ttu-id="7c483-199">Распространенные значения: Active (Активно), Resolved (Разрешено).</span><span class="sxs-lookup"><span data-stu-id="7c483-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="7c483-200">operationName</span><span class="sxs-lookup"><span data-stu-id="7c483-200">operationName</span></span> | <span data-ttu-id="7c483-201">Имя операции hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-201">Name of hello operation.</span></span> <span data-ttu-id="7c483-202">Обычно имеет значение Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="7c483-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="7c483-203">category</span><span class="sxs-lookup"><span data-stu-id="7c483-203">category</span></span> | <span data-ttu-id="7c483-204">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="7c483-204">"ServiceHealth"</span></span>
<span data-ttu-id="7c483-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="7c483-205">resourceId</span></span> | <span data-ttu-id="7c483-206">Идентификатор ресурса hello влияния ресурсов, если он известен.</span><span class="sxs-lookup"><span data-stu-id="7c483-206">Resource id of hello impacted resource, if known.</span></span> <span data-ttu-id="7c483-207">В противном случае указывается идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="7c483-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="7c483-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="7c483-208">Properties.title</span></span> | <span data-ttu-id="7c483-209">Hello локализованное название для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="7c483-209">hello localized title for this communication.</span></span> <span data-ttu-id="7c483-210">Используется английский язык по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-210">English is hello default language.</span></span>
<span data-ttu-id="7c483-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="7c483-211">Properties.communication</span></span> | <span data-ttu-id="7c483-212">Подробные сведения о локализации Hello hello связи с разметкой HTML.</span><span class="sxs-lookup"><span data-stu-id="7c483-212">hello localized details of hello communication with HTML markup.</span></span> <span data-ttu-id="7c483-213">По умолчанию hello является английский.</span><span class="sxs-lookup"><span data-stu-id="7c483-213">English is hello default.</span></span>
<span data-ttu-id="7c483-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="7c483-214">Properties.incidentType</span></span> | <span data-ttu-id="7c483-215">Возможные значения: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security.</span><span class="sxs-lookup"><span data-stu-id="7c483-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="7c483-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="7c483-216">Properties.trackingId</span></span> | <span data-ttu-id="7c483-217">Определяет инцидент hello, это событие, связанное с.</span><span class="sxs-lookup"><span data-stu-id="7c483-217">Identifies hello incident this event is associated with.</span></span> <span data-ttu-id="7c483-218">Используйте этот инцидент связанные tooan toocorrelate события hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-218">Use this toocorrelate hello events related tooan incident.</span></span>
<span data-ttu-id="7c483-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="7c483-219">Properties.impactedServices</span></span> | <span data-ttu-id="7c483-220">Escape-blob JSON, описывающий hello служб и регионов, которые влияет инцидент hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-220">An escaped JSON blob which describes hello services and regions that are impacted by hello incident.</span></span> <span data-ttu-id="7c483-221">Список служб Services, каждая из которых содержит ServiceName, и список регионов ImpactedRegions, каждый из которых содержит RegionName.</span><span class="sxs-lookup"><span data-stu-id="7c483-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="7c483-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="7c483-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="7c483-223">Hello взаимодействие на английском языке</span><span class="sxs-lookup"><span data-stu-id="7c483-223">hello communication in English</span></span>
<span data-ttu-id="7c483-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="7c483-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="7c483-225">Hello взаимодействие на английском языке, как обычный текст или HTML-разметка</span><span class="sxs-lookup"><span data-stu-id="7c483-225">hello communication in English as either html markup or plain text</span></span>
<span data-ttu-id="7c483-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="7c483-226">Properties.stage</span></span> | <span data-ttu-id="7c483-227">Возможные значения для AssistedRecovery, ActionRequired, Information, Incident, Security: Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="7c483-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="7c483-228">Возможные значения для Maintenance: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete.</span><span class="sxs-lookup"><span data-stu-id="7c483-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="7c483-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="7c483-229">Properties.communicationId</span></span> | <span data-ttu-id="7c483-230">связи Hello связано это событие.</span><span class="sxs-lookup"><span data-stu-id="7c483-230">hello communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="7c483-231">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="7c483-231">Alert</span></span>
<span data-ttu-id="7c483-232">Эта категория содержит hello записи для всех активаций оповещения Azure.</span><span class="sxs-lookup"><span data-stu-id="7c483-232">This category contains hello record of all activations of Azure alerts.</span></span> <span data-ttu-id="7c483-233">Пример hello тип события, отображаемые в этой категории — «% ЦП на myVM был более чем на 80 для hello за последние 5 минут.»</span><span class="sxs-lookup"><span data-stu-id="7c483-233">An example of hello type of event you would see in this category is "CPU % on myVM has been over 80 for hello past 5 minutes."</span></span> <span data-ttu-id="7c483-234">Различные системы Azure работают по принципу оповещений, то есть вы можете определить какое-то правило, и система будет направлять вам уведомление, когда условия этого правила выполняются.</span><span class="sxs-lookup"><span data-stu-id="7c483-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="7c483-235">Каждый раз, поддерживаемых Azure тип оповещения «активирует,» или hello условия выполнены toogenerate уведомление, запись активации hello также помещается toothis категории hello журнал действий.</span><span class="sxs-lookup"><span data-stu-id="7c483-235">Each time a supported Azure alert type 'activates,' or hello conditions are met toogenerate a notification, a record of hello activation is also pushed toothis category of hello Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7c483-236">Пример события</span><span class="sxs-lookup"><span data-stu-id="7c483-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
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

### <a name="property-descriptions"></a><span data-ttu-id="7c483-237">Описания свойств</span><span class="sxs-lookup"><span data-stu-id="7c483-237">Property descriptions</span></span>
| <span data-ttu-id="7c483-238">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="7c483-238">Element Name</span></span> | <span data-ttu-id="7c483-239">Описание</span><span class="sxs-lookup"><span data-stu-id="7c483-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c483-240">caller</span><span class="sxs-lookup"><span data-stu-id="7c483-240">caller</span></span> | <span data-ttu-id="7c483-241">Всегда имеет значение Microsoft.Insights/alertRules.</span><span class="sxs-lookup"><span data-stu-id="7c483-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="7c483-242">каналов</span><span class="sxs-lookup"><span data-stu-id="7c483-242">channels</span></span> | <span data-ttu-id="7c483-243">Всегда имеет значение "Admin, Operation".</span><span class="sxs-lookup"><span data-stu-id="7c483-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="7c483-244">claims</span><span class="sxs-lookup"><span data-stu-id="7c483-244">claims</span></span> | <span data-ttu-id="7c483-245">Большой двоичный объект JSON с hello имени участника-службы (имя участника-службы) или ресурс типа, обработчик оповещений hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-245">JSON blob with hello SPN (service principal name), or resource type, of hello alert engine.</span></span> |
| <span data-ttu-id="7c483-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="7c483-246">correlationId</span></span> | <span data-ttu-id="7c483-247">Идентификатор GUID в строковом формате hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-247">A GUID in hello string format.</span></span> |
| <span data-ttu-id="7c483-248">Описание</span><span class="sxs-lookup"><span data-stu-id="7c483-248">description</span></span> |<span data-ttu-id="7c483-249">Описание события оповещения hello статический текст.</span><span class="sxs-lookup"><span data-stu-id="7c483-249">Static text description of hello alert event.</span></span> |
| <span data-ttu-id="7c483-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7c483-250">eventDataId</span></span> |<span data-ttu-id="7c483-251">Уникальный идентификатор события hello для оповещения.</span><span class="sxs-lookup"><span data-stu-id="7c483-251">Unique identifier of hello alert event.</span></span> |
| <span data-ttu-id="7c483-252">level</span><span class="sxs-lookup"><span data-stu-id="7c483-252">level</span></span> |<span data-ttu-id="7c483-253">Уровень события hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-253">Level of hello event.</span></span> <span data-ttu-id="7c483-254">Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробный»</span><span class="sxs-lookup"><span data-stu-id="7c483-254">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="7c483-255">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="7c483-255">resourceGroupName</span></span> |<span data-ttu-id="7c483-256">Имя группы ресурсов hello hello влияет ресурсов является метрики предупреждение.</span><span class="sxs-lookup"><span data-stu-id="7c483-256">Name of hello resource group for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="7c483-257">Для других типов оповещений это имя hello hello группы ресурсов, содержащий предупреждение hello сам.</span><span class="sxs-lookup"><span data-stu-id="7c483-257">For other alert types, this is hello name of hello resource group that contains hello alert itself.</span></span> |
| <span data-ttu-id="7c483-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7c483-258">resourceProviderName</span></span> |<span data-ttu-id="7c483-259">Имя поставщика ресурсов hello hello влияет ресурсов является метрики предупреждение.</span><span class="sxs-lookup"><span data-stu-id="7c483-259">Name of hello resource provider for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="7c483-260">Другие типы оповещений это hello имя поставщика ресурсов hello для оповещения hello сам.</span><span class="sxs-lookup"><span data-stu-id="7c483-260">For other alert types, this is hello name of hello resource provider for hello alert itself.</span></span> |
| <span data-ttu-id="7c483-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="7c483-261">resourceId</span></span> | <span data-ttu-id="7c483-262">Имя ресурса с идентификатором hello hello влияет ресурсов является метрики предупреждение.</span><span class="sxs-lookup"><span data-stu-id="7c483-262">Name of hello resource ID for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="7c483-263">Другие типы оповещений это идентификатор ресурса hello сам ресурс предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-263">For other alert types, this is hello resource ID of hello alert resource itself.</span></span> |
| <span data-ttu-id="7c483-264">operationId</span><span class="sxs-lookup"><span data-stu-id="7c483-264">operationId</span></span> |<span data-ttu-id="7c483-265">Идентификатор GUID, совместно используемые hello события, которые соответствуют tooa одной операции.</span><span class="sxs-lookup"><span data-stu-id="7c483-265">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="7c483-266">operationName</span><span class="sxs-lookup"><span data-stu-id="7c483-266">operationName</span></span> |<span data-ttu-id="7c483-267">Имя операции hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-267">Name of hello operation.</span></span> |
| <span data-ttu-id="7c483-268">properties</span><span class="sxs-lookup"><span data-stu-id="7c483-268">properties</span></span> |<span data-ttu-id="7c483-269">Набор `<Key, Value>` пары (то есть, словарь), описывающий hello подробных сведениях события hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="7c483-270">status</span><span class="sxs-lookup"><span data-stu-id="7c483-270">status</span></span> |<span data-ttu-id="7c483-271">Строка, описывающая состояние hello hello операции.</span><span class="sxs-lookup"><span data-stu-id="7c483-271">String describing hello status of hello operation.</span></span> <span data-ttu-id="7c483-272">Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="7c483-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="7c483-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="7c483-273">subStatus</span></span> | <span data-ttu-id="7c483-274">Обычно для оповещений имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="7c483-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="7c483-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7c483-275">eventTimestamp</span></span> |<span data-ttu-id="7c483-276">Отметка времени, когда hello событий, созданных hello hello Azure служба обработки запроса соответствующее событие hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-276">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="7c483-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7c483-277">submissionTimestamp</span></span> |<span data-ttu-id="7c483-278">Отметка времени события hello стало доступно для запросов.</span><span class="sxs-lookup"><span data-stu-id="7c483-278">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="7c483-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7c483-279">subscriptionId</span></span> |<span data-ttu-id="7c483-280">Идентификатор подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="7c483-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="7c483-281">Поле свойств по типу оповещения</span><span class="sxs-lookup"><span data-stu-id="7c483-281">Properties field per alert type</span></span>
<span data-ttu-id="7c483-282">поле свойств Hello будет содержать разные значения в зависимости от источника hello hello события для оповещения.</span><span class="sxs-lookup"><span data-stu-id="7c483-282">hello properties field will contain different values depending on hello source of hello alert event.</span></span> <span data-ttu-id="7c483-283">Два распространенных поставщика событий оповещений — оповещения журнала действий и оповещения метрик.</span><span class="sxs-lookup"><span data-stu-id="7c483-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="7c483-284">Свойства оповещений журнала действий</span><span class="sxs-lookup"><span data-stu-id="7c483-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="7c483-285">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="7c483-285">Element Name</span></span> | <span data-ttu-id="7c483-286">Описание</span><span class="sxs-lookup"><span data-stu-id="7c483-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c483-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7c483-287">properties.subscriptionId</span></span> | <span data-ttu-id="7c483-288">Идентификатор подписки Hello из hello действия журнал событий, вызвавший этот toobe правило оповещения журнала активности активирован.</span><span class="sxs-lookup"><span data-stu-id="7c483-288">hello subscription ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7c483-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="7c483-289">properties.eventDataId</span></span> | <span data-ttu-id="7c483-290">Hello идентификатора данных события в журнал событий hello действие, вызвавшее активации этого правила оповещения toobe действия журнала.</span><span class="sxs-lookup"><span data-stu-id="7c483-290">hello event data ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7c483-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="7c483-291">properties.resourceGroup</span></span> | <span data-ttu-id="7c483-292">Группа ресурсов Hello из hello действия журнал событий, вызвавший этот toobe правило оповещения журнала активности активирован.</span><span class="sxs-lookup"><span data-stu-id="7c483-292">hello resource group from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7c483-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="7c483-293">properties.resourceId</span></span> | <span data-ttu-id="7c483-294">Идентификатор ресурса Hello из hello действия журнал событий, вызвавший этот toobe правило оповещения журнала активности активирован.</span><span class="sxs-lookup"><span data-stu-id="7c483-294">hello resource ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7c483-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7c483-295">properties.eventTimestamp</span></span> | <span data-ttu-id="7c483-296">Hello событий отметка времени события журнала действие hello, вызвавший этот toobe правило оповещения журнала активности активирован.</span><span class="sxs-lookup"><span data-stu-id="7c483-296">hello event timestamp of hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7c483-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="7c483-297">properties.operationName</span></span> | <span data-ttu-id="7c483-298">Имя операции Hello из hello действия журнал событий, вызвавший этот toobe правило оповещения журнала активности активирован.</span><span class="sxs-lookup"><span data-stu-id="7c483-298">hello operation name from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7c483-299">properties.status</span><span class="sxs-lookup"><span data-stu-id="7c483-299">properties.status</span></span> | <span data-ttu-id="7c483-300">состояние Hello из hello действия журнал событий, вызвавший этот toobe правило оповещения журнала активности активирован.</span><span class="sxs-lookup"><span data-stu-id="7c483-300">hello status from hello activity log event which caused this activity log alert rule toobe activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="7c483-301">Свойства оповещений метрик</span><span class="sxs-lookup"><span data-stu-id="7c483-301">Properties for metric alerts</span></span>
| <span data-ttu-id="7c483-302">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="7c483-302">Element Name</span></span> | <span data-ttu-id="7c483-303">Описание</span><span class="sxs-lookup"><span data-stu-id="7c483-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c483-304">properties.RuleUri</span><span class="sxs-lookup"><span data-stu-id="7c483-304">properties.RuleUri</span></span> | <span data-ttu-id="7c483-305">Идентификатор ресурса hello метрики правило генерации оповещений сам.</span><span class="sxs-lookup"><span data-stu-id="7c483-305">Resource ID of hello metric alert rule itself.</span></span> |
| <span data-ttu-id="7c483-306">properties.RuleName</span><span class="sxs-lookup"><span data-stu-id="7c483-306">properties.RuleName</span></span> | <span data-ttu-id="7c483-307">Имя метрики правило генерации оповещений hello Hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-307">hello name of hello metric alert rule.</span></span> |
| <span data-ttu-id="7c483-308">properties.RuleDescription</span><span class="sxs-lookup"><span data-stu-id="7c483-308">properties.RuleDescription</span></span> | <span data-ttu-id="7c483-309">Описание Hello правило генерации оповещений метрики hello (как определено правило генерации оповещений hello).</span><span class="sxs-lookup"><span data-stu-id="7c483-309">hello description of hello metric alert rule (as defined in hello alert rule).</span></span> |
| <span data-ttu-id="7c483-310">properties.Threshold</span><span class="sxs-lookup"><span data-stu-id="7c483-310">properties.Threshold</span></span> | <span data-ttu-id="7c483-311">Пороговое значение Hello вычислении hello hello метрики правила оповещения.</span><span class="sxs-lookup"><span data-stu-id="7c483-311">hello threshold value used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7c483-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="7c483-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="7c483-313">размер окна Hello вычислении hello hello метрики правила оповещения.</span><span class="sxs-lookup"><span data-stu-id="7c483-313">hello window size used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7c483-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="7c483-314">properties.Aggregation</span></span> | <span data-ttu-id="7c483-315">Hello статистической обработки типа, определенного в hello метрики правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="7c483-315">hello aggregation type defined in hello metric alert rule.</span></span> |
| <span data-ttu-id="7c483-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="7c483-316">properties.Operator</span></span> | <span data-ttu-id="7c483-317">условный оператор Hello вычислении hello hello метрики правила оповещения.</span><span class="sxs-lookup"><span data-stu-id="7c483-317">hello conditional operator used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7c483-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="7c483-318">properties.MetricName</span></span> | <span data-ttu-id="7c483-319">Имя метрики Hello hello метрику, используемую при вычислении hello hello метрики правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="7c483-319">hello metric name of hello metric used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7c483-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="7c483-320">properties.MetricUnit</span></span> | <span data-ttu-id="7c483-321">Единица измерения Hello метрики для hello метрику, используемую при вычислении hello hello метрики правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="7c483-321">hello metric unit for hello metric used in hello evaluation of hello metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="7c483-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="7c483-322">Autoscale</span></span>
<span data-ttu-id="7c483-323">Эта категория содержит запись hello любой операции toohello связанные события подсистемы автомасштабирования hello соответствии с параметрами автоматического масштабирования, установленных в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="7c483-323">This category contains hello record of any events related toohello operation of hello autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="7c483-324">Пример hello тип события, отображаемые в этой категории — «Автомасштабирования масштабирования вверх не удалось выполнить действие».</span><span class="sxs-lookup"><span data-stu-id="7c483-324">An example of hello type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="7c483-325">С помощью автоматического масштабирования, можно автоматически масштабировать или масштабирования в hello число экземпляров в типе поддерживаемых ресурсов на основе времени дня и/или загрузки данных (метрики), с помощью параметров автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="7c483-325">Using autoscale, you can automatically scale out or scale in hello number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="7c483-326">При выполнении условий hello tooscale вверх или вниз, hello start и успешно или сбой события будут регистрироваться в этой категории.</span><span class="sxs-lookup"><span data-stu-id="7c483-326">When hello conditions are met tooscale up or down, hello start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7c483-327">Пример события</span><span class="sxs-lookup"><span data-stu-id="7c483-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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

### <a name="property-descriptions"></a><span data-ttu-id="7c483-328">Описания свойств</span><span class="sxs-lookup"><span data-stu-id="7c483-328">Property descriptions</span></span>
| <span data-ttu-id="7c483-329">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="7c483-329">Element Name</span></span> | <span data-ttu-id="7c483-330">Описание</span><span class="sxs-lookup"><span data-stu-id="7c483-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c483-331">caller</span><span class="sxs-lookup"><span data-stu-id="7c483-331">caller</span></span> | <span data-ttu-id="7c483-332">Всегда имеет значение Microsoft.Insights/autoscaleSettings.</span><span class="sxs-lookup"><span data-stu-id="7c483-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="7c483-333">каналов</span><span class="sxs-lookup"><span data-stu-id="7c483-333">channels</span></span> | <span data-ttu-id="7c483-334">Всегда имеет значение "Admin, Operation".</span><span class="sxs-lookup"><span data-stu-id="7c483-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="7c483-335">claims</span><span class="sxs-lookup"><span data-stu-id="7c483-335">claims</span></span> | <span data-ttu-id="7c483-336">Большой двоичный объект JSON с помощью имени участника-службы (имя участника-службы) или ресурс типа подсистемы автомасштабирования hello hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-336">JSON blob with hello SPN (service principal name), or resource type, of hello autoscale engine.</span></span> |
| <span data-ttu-id="7c483-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="7c483-337">correlationId</span></span> | <span data-ttu-id="7c483-338">Идентификатор GUID в строковом формате hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-338">A GUID in hello string format.</span></span> |
| <span data-ttu-id="7c483-339">Описание</span><span class="sxs-lookup"><span data-stu-id="7c483-339">description</span></span> |<span data-ttu-id="7c483-340">Описание статический текст hello автомасштабирования события.</span><span class="sxs-lookup"><span data-stu-id="7c483-340">Static text description of hello autoscale event.</span></span> |
| <span data-ttu-id="7c483-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7c483-341">eventDataId</span></span> |<span data-ttu-id="7c483-342">Уникальный идентификатор события автомасштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-342">Unique identifier of hello autoscale event.</span></span> |
| <span data-ttu-id="7c483-343">level</span><span class="sxs-lookup"><span data-stu-id="7c483-343">level</span></span> |<span data-ttu-id="7c483-344">Уровень события hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-344">Level of hello event.</span></span> <span data-ttu-id="7c483-345">Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробный»</span><span class="sxs-lookup"><span data-stu-id="7c483-345">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="7c483-346">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="7c483-346">resourceGroupName</span></span> |<span data-ttu-id="7c483-347">Имя группы ресурсов hello параметра автомасштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-347">Name of hello resource group for hello autoscale setting.</span></span> |
| <span data-ttu-id="7c483-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7c483-348">resourceProviderName</span></span> |<span data-ttu-id="7c483-349">Имя поставщика ресурсов hello параметра автомасштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-349">Name of hello resource provider for hello autoscale setting.</span></span> |
| <span data-ttu-id="7c483-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="7c483-350">resourceId</span></span> |<span data-ttu-id="7c483-351">Идентификатор ресурса параметра автомасштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-351">Resource id of hello autoscale setting.</span></span> |
| <span data-ttu-id="7c483-352">operationId</span><span class="sxs-lookup"><span data-stu-id="7c483-352">operationId</span></span> |<span data-ttu-id="7c483-353">Идентификатор GUID, совместно используемые hello события, которые соответствуют tooa одной операции.</span><span class="sxs-lookup"><span data-stu-id="7c483-353">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="7c483-354">operationName</span><span class="sxs-lookup"><span data-stu-id="7c483-354">operationName</span></span> |<span data-ttu-id="7c483-355">Имя операции hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-355">Name of hello operation.</span></span> |
| <span data-ttu-id="7c483-356">properties</span><span class="sxs-lookup"><span data-stu-id="7c483-356">properties</span></span> |<span data-ttu-id="7c483-357">Набор `<Key, Value>` пары (то есть, словарь), описывающий hello подробных сведениях события hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="7c483-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="7c483-358">properties.Description</span></span> | <span data-ttu-id="7c483-359">Подробное описание того, какой механизм автоматического масштабирования hello делало.</span><span class="sxs-lookup"><span data-stu-id="7c483-359">Detailed description of what hello autoscale engine was doing.</span></span> |
| <span data-ttu-id="7c483-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="7c483-360">properties.ResourceName</span></span> | <span data-ttu-id="7c483-361">Идентификатор ресурса hello затронуто ресурсов (hello ресурса, на какие hello выполнявшаяся масштабирования)</span><span class="sxs-lookup"><span data-stu-id="7c483-361">Resource ID of hello impacted resource (hello resource on which hello scale action was being performed)</span></span> |
| <span data-ttu-id="7c483-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="7c483-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="7c483-363">Hello число экземпляров перед выполнением действия автомасштабирования hello действует.</span><span class="sxs-lookup"><span data-stu-id="7c483-363">hello number of instances before hello autoscale action took effect.</span></span> |
| <span data-ttu-id="7c483-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="7c483-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="7c483-365">Hello число экземпляров после выполнения действия автомасштабирования hello действует.</span><span class="sxs-lookup"><span data-stu-id="7c483-365">hello number of instances after hello autoscale action took effect.</span></span> |
| <span data-ttu-id="7c483-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="7c483-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="7c483-367">Hello отметка времени дату и время действия автомасштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-367">hello timestamp of when hello autoscale action occurred.</span></span> |
| <span data-ttu-id="7c483-368">status</span><span class="sxs-lookup"><span data-stu-id="7c483-368">status</span></span> |<span data-ttu-id="7c483-369">Строка, описывающая состояние hello hello операции.</span><span class="sxs-lookup"><span data-stu-id="7c483-369">String describing hello status of hello operation.</span></span> <span data-ttu-id="7c483-370">Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="7c483-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="7c483-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="7c483-371">subStatus</span></span> | <span data-ttu-id="7c483-372">Обычно для автоматического масштабирования имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="7c483-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="7c483-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7c483-373">eventTimestamp</span></span> |<span data-ttu-id="7c483-374">Отметка времени, когда hello событий, созданных hello hello Azure служба обработки запроса соответствующее событие hello.</span><span class="sxs-lookup"><span data-stu-id="7c483-374">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="7c483-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7c483-375">submissionTimestamp</span></span> |<span data-ttu-id="7c483-376">Отметка времени события hello стало доступно для запросов.</span><span class="sxs-lookup"><span data-stu-id="7c483-376">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="7c483-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7c483-377">subscriptionId</span></span> |<span data-ttu-id="7c483-378">Идентификатор подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="7c483-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c483-379">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c483-379">Next steps</span></span>
* [<span data-ttu-id="7c483-380">Дополнительные сведения о hello журнал действий (прежнее название — журналы аудита)</span><span class="sxs-lookup"><span data-stu-id="7c483-380">Learn more about hello Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="7c483-381">Поток tooEvent журнал действий Azure hello концентраторы</span><span class="sxs-lookup"><span data-stu-id="7c483-381">Stream hello Azure Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
