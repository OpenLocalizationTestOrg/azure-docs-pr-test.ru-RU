---
title: "журналы диагностики aaaAzure Service Bus | Документы Microsoft"
description: "Узнайте, как tooset копирование журналов диагностики для шины обслуживания в Azure."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="4aec6-103">Журналы диагностики служебной шины</span><span class="sxs-lookup"><span data-stu-id="4aec6-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="4aec6-104">Для служебной шины Azure можно просмотреть журналы двух типов.</span><span class="sxs-lookup"><span data-stu-id="4aec6-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="4aec6-105">**[Журналы действий](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="4aec6-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="4aec6-106">Эти журналы содержат сведения об операциях, выполненных с заданием.</span><span class="sxs-lookup"><span data-stu-id="4aec6-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="4aec6-107">журналы Hello всегда включен.</span><span class="sxs-lookup"><span data-stu-id="4aec6-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="4aec6-108">**[Журналы диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="4aec6-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="4aec6-109">Вы можете настроить журналы диагностики, чтобы получать более подробные сведения обо всем, что происходит с заданием.</span><span class="sxs-lookup"><span data-stu-id="4aec6-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="4aec6-110">Действия титульных журналы диагностики с момента создания задания hello до удаления задания hello, включая обновления и действия, которые могут возникнуть при выполнении задания hello hello.</span><span class="sxs-lookup"><span data-stu-id="4aec6-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="4aec6-111">Включение журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="4aec6-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="4aec6-112">По умолчанию журналы диагностики отключены.</span><span class="sxs-lookup"><span data-stu-id="4aec6-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="4aec6-113">tooenable журналы диагностики, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="4aec6-113">tooenable diagnostic logs, perform hello following steps:</span></span>

1.  <span data-ttu-id="4aec6-114">В hello [портал Azure](https://portal.azure.com)в разделе **мониторинг + управления**, нажмите кнопку **журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="4aec6-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![журналы toodiagnostic колонке навигации](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="4aec6-116">Щелкните ресурс hello требуется toomonitor.</span><span class="sxs-lookup"><span data-stu-id="4aec6-116">Click hello resource you want toomonitor.</span></span>  

3.  <span data-ttu-id="4aec6-117">Щелкните **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="4aec6-117">Click **Turn on diagnostics**.</span></span>

    ![Включение журналов диагностики](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="4aec6-119">Для параметра **Состояние** щелкните **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="4aec6-119">For **Status**, click **On**.</span></span>

    ![Изменение состояния журналов диагностики](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="4aec6-121">Набор hello архив целевой объекты; например учетная запись хранения, концентратора событий или анализа журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="4aec6-121">Set hello archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="4aec6-122">Сохраните новые параметры диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="4aec6-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="4aec6-123">Новые параметры вступят в силу в течение 10 минут.</span><span class="sxs-lookup"><span data-stu-id="4aec6-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="4aec6-124">После этого журналы отображаются на конечном архивных hello настроен на hello **журналы диагностики** колонку.</span><span class="sxs-lookup"><span data-stu-id="4aec6-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="4aec6-125">Дополнительные сведения о настройке диагностики см. в разделе hello [Обзор Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="4aec6-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="4aec6-126">Схема журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="4aec6-126">Diagnostic logs schema</span></span>

<span data-ttu-id="4aec6-127">Все журналы хранятся в формате JSON (нотация объектов JavaScript).</span><span class="sxs-lookup"><span data-stu-id="4aec6-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="4aec6-128">Каждая запись содержит поля строки, используйте формат hello, описанные в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="4aec6-128">Each entry has string fields that use hello format described in hello following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="4aec6-129">Схема операционных журналов</span><span class="sxs-lookup"><span data-stu-id="4aec6-129">Operational logs schema</span></span>

<span data-ttu-id="4aec6-130">Регистрирует в hello **OperationalLogs** категории записи, что происходит при выполнении операций с Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4aec6-130">Logs in hello **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="4aec6-131">В частности эти журналы записать hello тип операции, включая создание очереди, использование ресурсов и состояние операции hello hello.</span><span class="sxs-lookup"><span data-stu-id="4aec6-131">Specifically, these logs capture hello operation type, including queue creation, resources used, and hello status of hello operation.</span></span>

<span data-ttu-id="4aec6-132">Операционный журнал JSON строки включать элементы, перечисленные в следующей таблице hello:</span><span class="sxs-lookup"><span data-stu-id="4aec6-132">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="4aec6-133">Имя</span><span class="sxs-lookup"><span data-stu-id="4aec6-133">Name</span></span> | <span data-ttu-id="4aec6-134">Описание</span><span class="sxs-lookup"><span data-stu-id="4aec6-134">Description</span></span>
------- | -------
<span data-ttu-id="4aec6-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="4aec6-135">ActivityId</span></span> | <span data-ttu-id="4aec6-136">Внутренний идентификатор, используемый для отслеживания</span><span class="sxs-lookup"><span data-stu-id="4aec6-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="4aec6-137">EventName</span><span class="sxs-lookup"><span data-stu-id="4aec6-137">EventName</span></span> | <span data-ttu-id="4aec6-138">Имя операции</span><span class="sxs-lookup"><span data-stu-id="4aec6-138">Operation name</span></span>           
<span data-ttu-id="4aec6-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="4aec6-139">resourceId</span></span> | <span data-ttu-id="4aec6-140">Идентификатор ресурса Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4aec6-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="4aec6-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="4aec6-141">SubscriptionId</span></span> | <span data-ttu-id="4aec6-142">Идентификатор подписки</span><span class="sxs-lookup"><span data-stu-id="4aec6-142">Subscription ID</span></span>
<span data-ttu-id="4aec6-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="4aec6-143">EventTimeString</span></span> | <span data-ttu-id="4aec6-144">Время операции</span><span class="sxs-lookup"><span data-stu-id="4aec6-144">Operation time</span></span>
<span data-ttu-id="4aec6-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="4aec6-145">EventProperties</span></span> | <span data-ttu-id="4aec6-146">Свойства операции</span><span class="sxs-lookup"><span data-stu-id="4aec6-146">Operation properties</span></span>
<span data-ttu-id="4aec6-147">Status</span><span class="sxs-lookup"><span data-stu-id="4aec6-147">Status</span></span> | <span data-ttu-id="4aec6-148">Состояние операции</span><span class="sxs-lookup"><span data-stu-id="4aec6-148">Operation status</span></span>
<span data-ttu-id="4aec6-149">Caller</span><span class="sxs-lookup"><span data-stu-id="4aec6-149">Caller</span></span> | <span data-ttu-id="4aec6-150">Объект, вызвавший операцию (портал Azure или клиент управления)</span><span class="sxs-lookup"><span data-stu-id="4aec6-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="4aec6-151">category</span><span class="sxs-lookup"><span data-stu-id="4aec6-151">category</span></span> | <span data-ttu-id="4aec6-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="4aec6-152">OperationalLogs</span></span>

<span data-ttu-id="4aec6-153">Ниже приведен пример строки JSON операционного журнала.</span><span class="sxs-lookup"><span data-stu-id="4aec6-153">Here's an example of an operational log JSON string:</span></span>

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="4aec6-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4aec6-154">Next steps</span></span>

<span data-ttu-id="4aec6-155">Посетите следующие ссылки toolearn дополнительные о Service Bus hello:</span><span class="sxs-lookup"><span data-stu-id="4aec6-155">Visit hello following links toolearn more about Service Bus:</span></span>

* [<span data-ttu-id="4aec6-156">Введение tooService шины</span><span class="sxs-lookup"><span data-stu-id="4aec6-156">Introduction tooService Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="4aec6-157">Приступая к работе со служебной шиной</span><span class="sxs-lookup"><span data-stu-id="4aec6-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
