---
title: "Включение ведения журнала диагностики для событий пакетной службы в Azure | Документация Майкрософт"
description: "Запись и анализ событий журнала диагностики для ресурсов учетной записи пакетной службы Azure, таких как пулы и задачи."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7bc6fd9921ab0f2374ace33ea5c1ab93a78f860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="1e2e1-103">События журнала для диагностики и мониторинга решений пакетной службы</span><span class="sxs-lookup"><span data-stu-id="1e2e1-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="1e2e1-104">Как и многие другие службы Azure, пакетная служба генерирует события журналов для некоторых ресурсов в течение их жизненного цикла.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-104">As with many Azure services, the Batch service emits log events for certain resources during the lifetime of the resource.</span></span> <span data-ttu-id="1e2e1-105">Вы можете включить журналы диагностики для пакетной службы Azure, чтобы собирать события таких ресурсов, как пулы и задачи, а затем использовать эти журналы для диагностики и мониторинга.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-105">You can enable Azure Batch diagnostic logs to record events for resources like pools and tasks, and then use the logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="1e2e1-106">Журналы диагностики пакетной службы содержат такие события, как создание пула, удаление пула, начало задачи, завершение задачи и т. п.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="1e2e1-107">В этой статье описывается ведение журнала событий для ресурсов пакетной службы, а не журнала выходных данных задач и заданий.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="1e2e1-108">Сведения о сохранении выходных данных заданий и задач вы найдете в статье [Сохранение выходных данных заданий и задач пакетной службы Azure](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="1e2e1-108">For details on storing the output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1e2e1-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1e2e1-109">Prerequisites</span></span>
* [<span data-ttu-id="1e2e1-110">Учетная запись пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="1e2e1-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="1e2e1-111">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="1e2e1-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="1e2e1-112">Чтобы сохранять журналы диагностики пакетной службы, следует создать учетную запись хранения. В этом хранилище Azure будет хранить журналы.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-112">To persist Batch diagnostic logs, you must create an Azure Storage account where Azure will store the logs.</span></span> <span data-ttu-id="1e2e1-113">Эту учетную запись хранения вы укажете в процессе [включения ведения журналов диагностики](#enable-diagnostic-logging) для учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="1e2e1-114">Учетная запись хранения, которую вы указываете при включении сбора журналов, не совпадает со связанной учетной записью хранения, которая упоминается в статьях о [пакетах приложений](batch-application-packages.md) и о [сохраняемости результатов выполнения задач](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="1e2e1-114">The Storage account you specify when you enable log collection is not the same as a linked storage account referred to in the [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="1e2e1-115">Вы будете **оплачивать** данные, размещенные в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-115">You are **charged** for the data stored in your Azure Storage account.</span></span> <span data-ttu-id="1e2e1-116">В том числе и журналы диагностики, о которых идет речь в этой статье.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-116">This includes the diagnostic logs discussed in this article.</span></span> <span data-ttu-id="1e2e1-117">Не забывайте об этом, когда разрабатываете [политику хранения журналов](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="1e2e1-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="1e2e1-118">Включение ведения журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="1e2e1-118">Enable diagnostic logging</span></span>
<span data-ttu-id="1e2e1-119">Ведение журналов диагностики для учетной записи пакетной службы по умолчанию отключено.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="1e2e1-120">Ведение журналов диагностики следует явно включить для каждой учетной записи пакетной службы, которые нужно отслеживать.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-120">You must explicitly enable diagnostic logging for each Batch account you want to monitor:</span></span>

[<span data-ttu-id="1e2e1-121">Как включить сбор журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="1e2e1-121">How to enable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="1e2e1-122">Мы рекомендуем полностью прочитать статью [Обзор журналов диагностики Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md), чтобы не только научиться включать ведение журнала, но и узнать, какие категории журналов поддерживаются различными службами Azure.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-122">We recommend that you read the full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article to gain an understanding of not only how to enable logging, but the log categories supported by the various Azure services.</span></span> <span data-ttu-id="1e2e1-123">Например, пакетная служба Azure в настоящее время поддерживает только одну категорию журналов: **журналы служб**.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="1e2e1-124">Журналы служб</span><span class="sxs-lookup"><span data-stu-id="1e2e1-124">Service Logs</span></span>
<span data-ttu-id="1e2e1-125">Журналы пакетной службы Azure содержат события, генерируемые пакетной службой Azure на всем протяжении существования ресурса пакетной службы, например пула или задачи.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-125">Azure Batch Service Logs contain events emitted by the Azure Batch service during the lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="1e2e1-126">Каждое событие, генерируемой пакетной службой, хранится в формате JSON в указанной учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-126">Each event emitted by Batch is stored in the specified Storage account in JSON format.</span></span> <span data-ttu-id="1e2e1-127">Например, так выглядит текст **события создания пула**:</span><span class="sxs-lookup"><span data-stu-id="1e2e1-127">For example, this is the body of a sample **pool create event**:</span></span>

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

<span data-ttu-id="1e2e1-128">Содержание каждого события находится в JSON-файле, размещенном в указанной учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-128">Each event body resides in a .json file in the specified Azure Storage account.</span></span> <span data-ttu-id="1e2e1-129">Если вам нужен прямой доступ к журналам, вы можете изучить [схему журналов диагностики в учетной записи хранилища](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="1e2e1-129">If you want to access the logs directly, you may wish to review the [schema of Diagnostic Logs in the storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="1e2e1-130">События журнала службы</span><span class="sxs-lookup"><span data-stu-id="1e2e1-130">Service Log events</span></span>
<span data-ttu-id="1e2e1-131">В настоящее время пакетная служба генерирует следующие события журнала службы.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-131">The Batch service currently emits the following Service Log events.</span></span> <span data-ttu-id="1e2e1-132">Этот список может оказаться неполным, если с момента последнего обновления этой статьи были добавлены новые события.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="1e2e1-133">**События журнала службы**</span><span class="sxs-lookup"><span data-stu-id="1e2e1-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="1e2e1-134">[Pool create][pool_create]</span><span class="sxs-lookup"><span data-stu-id="1e2e1-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="1e2e1-135">[Pool delete start][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="1e2e1-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="1e2e1-136">[Pool delete complete][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="1e2e1-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="1e2e1-137">[Pool resize start][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="1e2e1-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="1e2e1-138">[Pool resize complete][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="1e2e1-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="1e2e1-139">[Task start][task_start]</span><span class="sxs-lookup"><span data-stu-id="1e2e1-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="1e2e1-140">[Task complete][task_complete]</span><span class="sxs-lookup"><span data-stu-id="1e2e1-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="1e2e1-141">[Task fail][task_fail]</span><span class="sxs-lookup"><span data-stu-id="1e2e1-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1e2e1-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e2e1-142">Next steps</span></span>
<span data-ttu-id="1e2e1-143">Помимо хранения событий журнала диагностики в учетной записи хранения Azure вы можете настроить потоковую передачу событий журнала пакетной службы в [концентратор событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md) для передачи в [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e2e1-143">In addition to storing diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them to [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="1e2e1-144">Потоковая передача журналов диагностики Azure в концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="1e2e1-144">Stream Azure Diagnostic Logs to Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="1e2e1-145">Потоковая передача диагностических событий пакетной службы в концентраторы событий, которые представляют собой масштабируемую службу приема данных.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-145">Stream Batch diagnostic events to the highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="1e2e1-146">Концентраторы событий способны принимать миллионы событий в секунду, позволяя преобразовать и сохранять их с помощью любого поставщика аналитики в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="1e2e1-147">Анализ журналов диагностики Azure с помощью Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1e2e1-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="1e2e1-148">Отправьте журналы диагностики в Log Analytics, где вы сможете проанализировать их с помощью портала OMS (Operations Management Suite) или экспортировать для анализа в Power BI или Excel.</span><span class="sxs-lookup"><span data-stu-id="1e2e1-148">Send your diagnostic logs to Log Analytics where you can analyze them in the Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
