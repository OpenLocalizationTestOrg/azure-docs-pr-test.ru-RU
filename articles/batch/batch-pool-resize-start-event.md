---
title: "Событие начала изменения размера пула пакетной службы Azure | Документы Майкрософт"
description: "Справочник по событию начала изменения размера пула пакетной службы."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 826cd984d26b923ba38562e05a2e75c399be9121
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="e6e4c-103">Событие начала изменения размера пула</span><span class="sxs-lookup"><span data-stu-id="e6e4c-103">Pool resize start event</span></span>

 <span data-ttu-id="e6e4c-104">Это событие создается, когда начинается изменение размера пула.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="e6e4c-105">Так как изменение размера пула является асинхронным событием, можно ожидать, что после окончания этой операции возникнет событие завершения изменения размера пула.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-105">Since the pool resize is an asynchronous event, you can expect a pool resize complete event to be emitted once the resize operation completes.</span></span>

 <span data-ttu-id="e6e4c-106">В следующем примере показан текст для события начала изменения размера пула с 0 до 2 узлов, когда такое изменение выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-106">The following example shows the body of a pool resize start event for a pool resizing from 0 to 2 nodes with a manual resize.</span></span>

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|<span data-ttu-id="e6e4c-107">Элемент</span><span class="sxs-lookup"><span data-stu-id="e6e4c-107">Element</span></span>|<span data-ttu-id="e6e4c-108">Тип</span><span class="sxs-lookup"><span data-stu-id="e6e4c-108">Type</span></span>|<span data-ttu-id="e6e4c-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="e6e4c-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="e6e4c-110">poolId</span><span class="sxs-lookup"><span data-stu-id="e6e4c-110">poolId</span></span>|<span data-ttu-id="e6e4c-111">Строка</span><span class="sxs-lookup"><span data-stu-id="e6e4c-111">String</span></span>|<span data-ttu-id="e6e4c-112">Идентификатор пула.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-112">The id of the pool.</span></span>|
|<span data-ttu-id="e6e4c-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="e6e4c-113">nodeDeallocationOption</span></span>|<span data-ttu-id="e6e4c-114">Строка</span><span class="sxs-lookup"><span data-stu-id="e6e4c-114">String</span></span>|<span data-ttu-id="e6e4c-115">Указывает, когда можно удалить узлы из пула, если его размер уменьшается.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-115">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="e6e4c-116">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="e6e4c-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="e6e4c-117">**requeue** — завершает выполняющиеся задачи и повторно ставит их в очередь.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="e6e4c-118">Задачи будут запущены повторно при включении задания.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-118">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="e6e4c-119">Узлы удаляются сразу после завершения задач.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="e6e4c-120">**terminate** — завершает выполняющиеся задачи.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="e6e4c-121">Задачи не будут запущены повторно.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-121">The tasks will not run again.</span></span> <span data-ttu-id="e6e4c-122">Узлы удаляются сразу после завершения задач.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="e6e4c-123">**taskcompletion** — разрешает завершить текущие выполняющиеся задачи.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-123">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="e6e4c-124">Во время ожидания новые задачи не планируются.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="e6e4c-125">Узлы удаляются после выполнения всех задач.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="e6e4c-126">**Retaineddata** — разрешает завершить текущие выполняющиеся задачи и затем ожидает, пока истекут сроки хранения данных для всех задач.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-126">**Retaineddata** - Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="e6e4c-127">Во время ожидания новые задачи не планируются.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="e6e4c-128">Узлы удаляются после истечения сроков хранения для всех задач.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="e6e4c-129">По умолчанию используется значение requeue.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-129">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="e6e4c-130">Если размер пула увеличивается, устанавливается значение **invalid**.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-130">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="e6e4c-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="e6e4c-131">currentDedicated</span></span>|<span data-ttu-id="e6e4c-132">Int32</span><span class="sxs-lookup"><span data-stu-id="e6e4c-132">Int32</span></span>|<span data-ttu-id="e6e4c-133">Число вычислительных узлов, назначенных пулу.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-133">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="e6e4c-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="e6e4c-134">targetDedicated</span></span>|<span data-ttu-id="e6e4c-135">Int32</span><span class="sxs-lookup"><span data-stu-id="e6e4c-135">Int32</span></span>|<span data-ttu-id="e6e4c-136">Число вычислительных узлов, запрошенных для пула.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-136">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="e6e4c-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="e6e4c-137">enableAutoScale</span></span>|<span data-ttu-id="e6e4c-138">Bool</span><span class="sxs-lookup"><span data-stu-id="e6e4c-138">Bool</span></span>|<span data-ttu-id="e6e4c-139">Указывает, корректируется ли размер пула автоматически с течением времени.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-139">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="e6e4c-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="e6e4c-140">isAutoPool</span></span>|<span data-ttu-id="e6e4c-141">Bool</span><span class="sxs-lookup"><span data-stu-id="e6e4c-141">Bool</span></span>|<span data-ttu-id="e6e4c-142">Определяет, создан ли пул с помощью механизма AutoPool задания.</span><span class="sxs-lookup"><span data-stu-id="e6e4c-142">Speficies whether the pool was created via a job's AutoPool mechanism.</span></span>|
