---
title: "Журналы диагностики служебной шины Azure | Документация Майкрософт"
description: "Узнайте, как настроить журналы диагностики для служебной шины в Azure."
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
ms.openlocfilehash: 72e18444c83b84c5191a0aab3dc6983517167dd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="a46d5-103">Журналы диагностики служебной шины</span><span class="sxs-lookup"><span data-stu-id="a46d5-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="a46d5-104">Для служебной шины Azure можно просмотреть журналы двух типов.</span><span class="sxs-lookup"><span data-stu-id="a46d5-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="a46d5-105">**[Журналы действий](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="a46d5-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="a46d5-106">Эти журналы содержат сведения об операциях, выполненных с заданием.</span><span class="sxs-lookup"><span data-stu-id="a46d5-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="a46d5-107">Данные журналы всегда включены.</span><span class="sxs-lookup"><span data-stu-id="a46d5-107">The logs are always enabled.</span></span>
* <span data-ttu-id="a46d5-108">**[Журналы диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="a46d5-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="a46d5-109">Вы можете настроить журналы диагностики, чтобы получать более подробные сведения обо всем, что происходит с заданием.</span><span class="sxs-lookup"><span data-stu-id="a46d5-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="a46d5-110">Журналы диагностики охватывают действия с момента создания задания до его удаления, включая обновления и действия, которые происходят во время выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="a46d5-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="a46d5-111">Включение журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="a46d5-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="a46d5-112">По умолчанию журналы диагностики отключены.</span><span class="sxs-lookup"><span data-stu-id="a46d5-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="a46d5-113">Чтобы включить ведение журналов диагностики, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="a46d5-113">To enable diagnostic logs, perform the following steps:</span></span>

1.  <span data-ttu-id="a46d5-114">На [портале Azure](https://portal.azure.com) в разделе **Мониторинг и управление** щелкните **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="a46d5-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Перемещение к колонке журналов диагностики](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="a46d5-116">Выберите ресурс, который необходимо отслеживать.</span><span class="sxs-lookup"><span data-stu-id="a46d5-116">Click the resource you want to monitor.</span></span>  

3.  <span data-ttu-id="a46d5-117">Щелкните **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="a46d5-117">Click **Turn on diagnostics**.</span></span>

    ![Включение журналов диагностики](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="a46d5-119">Для параметра **Состояние** щелкните **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="a46d5-119">For **Status**, click **On**.</span></span>

    ![Изменение состояния журналов диагностики](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="a46d5-121">Настройте нужную цель для архивирования, например учетную запись хранения, концентратор событий или Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a46d5-121">Set the archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="a46d5-122">Сохраните новые параметры диагностики.</span><span class="sxs-lookup"><span data-stu-id="a46d5-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="a46d5-123">Новые параметры вступят в силу в течение 10 минут.</span><span class="sxs-lookup"><span data-stu-id="a46d5-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="a46d5-124">После этого журналы появятся в настроенной цели для архивирования на вкладке **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="a46d5-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="a46d5-125">Дополнительные сведения о настройке системы диагностики доступны в [обзоре журналов диагностики Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a46d5-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="a46d5-126">Схема журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="a46d5-126">Diagnostic logs schema</span></span>

<span data-ttu-id="a46d5-127">Все журналы хранятся в формате JSON (нотация объектов JavaScript).</span><span class="sxs-lookup"><span data-stu-id="a46d5-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="a46d5-128">Каждая запись содержит строковые поля, использующие формат, описанный в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="a46d5-128">Each entry has string fields that use the format described in the following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="a46d5-129">Схема операционных журналов</span><span class="sxs-lookup"><span data-stu-id="a46d5-129">Operational logs schema</span></span>

<span data-ttu-id="a46d5-130">В журналах в категории **OperationalLogs** регистрируется все, что происходит во время работы служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a46d5-130">Logs in the **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="a46d5-131">В частности, в эти журналы записывается тип операции, включая создание очереди, используемые ресурсы и состояние операции.</span><span class="sxs-lookup"><span data-stu-id="a46d5-131">Specifically, these logs capture the operation type, including queue creation, resources used, and the status of the operation.</span></span>

<span data-ttu-id="a46d5-132">Строки JSON операционного журнала содержат элементы, перечисленные в приведенной ниже таблице.</span><span class="sxs-lookup"><span data-stu-id="a46d5-132">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="a46d5-133">Имя</span><span class="sxs-lookup"><span data-stu-id="a46d5-133">Name</span></span> | <span data-ttu-id="a46d5-134">Описание</span><span class="sxs-lookup"><span data-stu-id="a46d5-134">Description</span></span>
------- | -------
<span data-ttu-id="a46d5-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="a46d5-135">ActivityId</span></span> | <span data-ttu-id="a46d5-136">Внутренний идентификатор, используемый для отслеживания</span><span class="sxs-lookup"><span data-stu-id="a46d5-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="a46d5-137">EventName</span><span class="sxs-lookup"><span data-stu-id="a46d5-137">EventName</span></span> | <span data-ttu-id="a46d5-138">Имя операции</span><span class="sxs-lookup"><span data-stu-id="a46d5-138">Operation name</span></span>           
<span data-ttu-id="a46d5-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="a46d5-139">resourceId</span></span> | <span data-ttu-id="a46d5-140">Идентификатор ресурса Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a46d5-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="a46d5-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a46d5-141">SubscriptionId</span></span> | <span data-ttu-id="a46d5-142">Идентификатор подписки</span><span class="sxs-lookup"><span data-stu-id="a46d5-142">Subscription ID</span></span>
<span data-ttu-id="a46d5-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="a46d5-143">EventTimeString</span></span> | <span data-ttu-id="a46d5-144">Время операции</span><span class="sxs-lookup"><span data-stu-id="a46d5-144">Operation time</span></span>
<span data-ttu-id="a46d5-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="a46d5-145">EventProperties</span></span> | <span data-ttu-id="a46d5-146">Свойства операции</span><span class="sxs-lookup"><span data-stu-id="a46d5-146">Operation properties</span></span>
<span data-ttu-id="a46d5-147">Status</span><span class="sxs-lookup"><span data-stu-id="a46d5-147">Status</span></span> | <span data-ttu-id="a46d5-148">Состояние операции</span><span class="sxs-lookup"><span data-stu-id="a46d5-148">Operation status</span></span>
<span data-ttu-id="a46d5-149">Caller</span><span class="sxs-lookup"><span data-stu-id="a46d5-149">Caller</span></span> | <span data-ttu-id="a46d5-150">Объект, вызвавший операцию (портал Azure или клиент управления)</span><span class="sxs-lookup"><span data-stu-id="a46d5-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="a46d5-151">category</span><span class="sxs-lookup"><span data-stu-id="a46d5-151">category</span></span> | <span data-ttu-id="a46d5-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="a46d5-152">OperationalLogs</span></span>

<span data-ttu-id="a46d5-153">Ниже приведен пример строки JSON операционного журнала.</span><span class="sxs-lookup"><span data-stu-id="a46d5-153">Here's an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a46d5-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a46d5-154">Next steps</span></span>

<span data-ttu-id="a46d5-155">Чтобы узнать больше о служебной шине, перейдите по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="a46d5-155">Visit the following links to learn more about Service Bus:</span></span>

* [<span data-ttu-id="a46d5-156">Основные сведения о служебной шине</span><span class="sxs-lookup"><span data-stu-id="a46d5-156">Introduction to Service Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="a46d5-157">Приступая к работе со служебной шиной</span><span class="sxs-lookup"><span data-stu-id="a46d5-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
