---
title: "aaaEnable ведения журналов диагностики для событий пакетных - Azure | Документы Microsoft"
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
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="beaf1-103">События журнала для диагностики и мониторинга решений пакетной службы</span><span class="sxs-lookup"><span data-stu-id="beaf1-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="beaf1-104">Как и многие службы Azure hello пакетная служба создает для определенных ресурсов во время hello ресурсов hello время существования журнала событий.</span><span class="sxs-lookup"><span data-stu-id="beaf1-104">As with many Azure services, hello Batch service emits log events for certain resources during hello lifetime of hello resource.</span></span> <span data-ttu-id="beaf1-105">Можно включить события toorecord журналы диагностики пакета Azure для ресурсов, таких как пулы и задачи и затем использовать журналы hello для оценки, диагностики и мониторинга.</span><span class="sxs-lookup"><span data-stu-id="beaf1-105">You can enable Azure Batch diagnostic logs toorecord events for resources like pools and tasks, and then use hello logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="beaf1-106">Журналы диагностики пакетной службы содержат такие события, как создание пула, удаление пула, начало задачи, завершение задачи и т. п.</span><span class="sxs-lookup"><span data-stu-id="beaf1-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="beaf1-107">В этой статье описывается ведение журнала событий для ресурсов пакетной службы, а не журнала выходных данных задач и заданий.</span><span class="sxs-lookup"><span data-stu-id="beaf1-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="beaf1-108">Дополнительные сведения о хранении hello выходные данные заданий и задач см. в разделе [выходные данные заданий и задач сохранения пакетной службы Azure](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="beaf1-108">For details on storing hello output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="beaf1-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="beaf1-109">Prerequisites</span></span>
* [<span data-ttu-id="beaf1-110">Учетная запись пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="beaf1-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="beaf1-111">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="beaf1-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="beaf1-112">toopersist журналы диагностики пакета, необходимо создать учетную запись хранилища Azure, где Azure будет хранить журналы hello.</span><span class="sxs-lookup"><span data-stu-id="beaf1-112">toopersist Batch diagnostic logs, you must create an Azure Storage account where Azure will store hello logs.</span></span> <span data-ttu-id="beaf1-113">Эту учетную запись хранения вы укажете в процессе [включения ведения журналов диагностики](#enable-diagnostic-logging) для учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="beaf1-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="beaf1-114">Hello учетной записи хранилища, укажите при включении сбора журналов не является hello таким же как hello связанное хранение учетной записи ссылка tooin [пакетов приложений](batch-application-packages.md) и [сохраняемости результат выполнения задачи](batch-task-output.md) статей.</span><span class="sxs-lookup"><span data-stu-id="beaf1-114">hello Storage account you specify when you enable log collection is not hello same as a linked storage account referred tooin hello [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="beaf1-115">Вы являетесь **плата** для hello данные, хранящиеся в вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="beaf1-115">You are **charged** for hello data stored in your Azure Storage account.</span></span> <span data-ttu-id="beaf1-116">К ним относятся журналы диагностики hello, рассматриваемые в данной статье.</span><span class="sxs-lookup"><span data-stu-id="beaf1-116">This includes hello diagnostic logs discussed in this article.</span></span> <span data-ttu-id="beaf1-117">Не забывайте об этом, когда разрабатываете [политику хранения журналов](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="beaf1-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="beaf1-118">Включение ведения журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="beaf1-118">Enable diagnostic logging</span></span>
<span data-ttu-id="beaf1-119">Ведение журналов диагностики для учетной записи пакетной службы по умолчанию отключено.</span><span class="sxs-lookup"><span data-stu-id="beaf1-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="beaf1-120">Необходимо явно включить сбор данных диагностики для каждой учетной записи пакета необходимо toomonitor:</span><span class="sxs-lookup"><span data-stu-id="beaf1-120">You must explicitly enable diagnostic logging for each Batch account you want toomonitor:</span></span>

[<span data-ttu-id="beaf1-121">Как tooenable сбора журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="beaf1-121">How tooenable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="beaf1-122">Рекомендуется прочитать hello полного [Обзор служб Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain статьи не только влияние ведения журнала tooenable, однако hello журнала категории понимание поддерживаемые hello различных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="beaf1-122">We recommend that you read hello full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain an understanding of not only how tooenable logging, but hello log categories supported by hello various Azure services.</span></span> <span data-ttu-id="beaf1-123">Например, пакетная служба Azure в настоящее время поддерживает только одну категорию журналов: **журналы служб**.</span><span class="sxs-lookup"><span data-stu-id="beaf1-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="beaf1-124">Журналы служб</span><span class="sxs-lookup"><span data-stu-id="beaf1-124">Service Logs</span></span>
<span data-ttu-id="beaf1-125">Azure пакетной службы журналы содержат события, генерируемой hello пакетной службы Azure во время существования hello ресурса пакета как пула или задачи.</span><span class="sxs-lookup"><span data-stu-id="beaf1-125">Azure Batch Service Logs contain events emitted by hello Azure Batch service during hello lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="beaf1-126">Каждое событие, генерируемой пакета сохраняется в указанный hello учетной записи хранилища в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="beaf1-126">Each event emitted by Batch is stored in hello specified Storage account in JSON format.</span></span> <span data-ttu-id="beaf1-127">Например, это текст hello образца **создание событий пула**:</span><span class="sxs-lookup"><span data-stu-id="beaf1-127">For example, this is hello body of a sample **pool create event**:</span></span>

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

<span data-ttu-id="beaf1-128">Текст каждого события находится в .json указан файл в hello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="beaf1-128">Each event body resides in a .json file in hello specified Azure Storage account.</span></span> <span data-ttu-id="beaf1-129">Если требуется tooaccess hello журналы напрямую, вы можете tooreview hello [схемы из журналов диагностики в учетной записи хранения hello](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="beaf1-129">If you want tooaccess hello logs directly, you may wish tooreview hello [schema of Diagnostic Logs in hello storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="beaf1-130">События журнала службы</span><span class="sxs-lookup"><span data-stu-id="beaf1-130">Service Log events</span></span>
<span data-ttu-id="beaf1-131">в настоящее время Hello пакетная служба создает hello следующие службы журнала событий.</span><span class="sxs-lookup"><span data-stu-id="beaf1-131">hello Batch service currently emits hello following Service Log events.</span></span> <span data-ttu-id="beaf1-132">Этот список может оказаться неполным, если с момента последнего обновления этой статьи были добавлены новые события.</span><span class="sxs-lookup"><span data-stu-id="beaf1-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="beaf1-133">**События журнала службы**</span><span class="sxs-lookup"><span data-stu-id="beaf1-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="beaf1-134">[Pool create][pool_create]</span><span class="sxs-lookup"><span data-stu-id="beaf1-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="beaf1-135">[Pool delete start][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="beaf1-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="beaf1-136">[Pool delete complete][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="beaf1-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="beaf1-137">[Pool resize start][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="beaf1-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="beaf1-138">[Pool resize complete][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="beaf1-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="beaf1-139">[Task start][task_start]</span><span class="sxs-lookup"><span data-stu-id="beaf1-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="beaf1-140">[Task complete][task_complete]</span><span class="sxs-lookup"><span data-stu-id="beaf1-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="beaf1-141">[Task fail][task_fail]</span><span class="sxs-lookup"><span data-stu-id="beaf1-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="beaf1-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="beaf1-142">Next steps</span></span>
<span data-ttu-id="beaf1-143">Добавление toostoring событий журнала диагностики в учетную запись хранилища Azure, можно также записывать tooan пакетной службы журнала событий [концентратор событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md), а затем отправить их слишком[анализа журналов Azure](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="beaf1-143">In addition toostoring diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them too[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="beaf1-144">Журналы диагностики Azure поток tooEvent концентраторы</span><span class="sxs-lookup"><span data-stu-id="beaf1-144">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="beaf1-145">Поток пакетная события диагностики toohello высокомасштабируемых данных входящих сообщений служба концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="beaf1-145">Stream Batch diagnostic events toohello highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="beaf1-146">Концентраторы событий способны принимать миллионы событий в секунду, позволяя преобразовать и сохранять их с помощью любого поставщика аналитики в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="beaf1-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="beaf1-147">Анализ журналов диагностики Azure с помощью Log Analytics</span><span class="sxs-lookup"><span data-stu-id="beaf1-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="beaf1-148">Отправка в журналы диагностики tooLog Analytics, где можно проанализировать их на портале Operations Management Suite (OMS) hello или экспортировать их для анализа в Power BI или Excel.</span><span class="sxs-lookup"><span data-stu-id="beaf1-148">Send your diagnostic logs tooLog Analytics where you can analyze them in hello Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
