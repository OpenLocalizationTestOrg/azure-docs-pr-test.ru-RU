---
title: "Событие завершения изменения размера пула пакетной службы Azure | Документы Майкрософт"
description: "Справочник по событию завершения изменения размера пула пакетной службы."
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
ms.openlocfilehash: 7072293d98526812cb42ce9c2f8e33bfcafaa149
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-complete-event"></a><span data-ttu-id="307d6-103">Событие завершения изменения размера пула</span><span class="sxs-lookup"><span data-stu-id="307d6-103">Pool resize complete event</span></span>

 <span data-ttu-id="307d6-104">Это событие создается при завершении или сбое операции изменения размера пула.</span><span class="sxs-lookup"><span data-stu-id="307d6-104">This event is emitted when a pool resize has completed or failed.</span></span>

 <span data-ttu-id="307d6-105">Следующий пример показывает текст для события завершения изменения размера пула, когда размер пула успешно увеличивается.</span><span class="sxs-lookup"><span data-stu-id="307d6-105">The following example shows the body of a pool resize complete event for a pool that increased in size and completed successfully.</span></span>

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "The operation succeeded"
}
```

|<span data-ttu-id="307d6-106">Элемент</span><span class="sxs-lookup"><span data-stu-id="307d6-106">Element</span></span>|<span data-ttu-id="307d6-107">Тип</span><span class="sxs-lookup"><span data-stu-id="307d6-107">Type</span></span>|<span data-ttu-id="307d6-108">Примечания</span><span class="sxs-lookup"><span data-stu-id="307d6-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="307d6-109">id</span><span class="sxs-lookup"><span data-stu-id="307d6-109">id</span></span>|<span data-ttu-id="307d6-110">string</span><span class="sxs-lookup"><span data-stu-id="307d6-110">String</span></span>|<span data-ttu-id="307d6-111">Идентификатор пула.</span><span class="sxs-lookup"><span data-stu-id="307d6-111">The id of the pool.</span></span>|
|<span data-ttu-id="307d6-112">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="307d6-112">nodeDeallocationOption</span></span>|<span data-ttu-id="307d6-113">Строка</span><span class="sxs-lookup"><span data-stu-id="307d6-113">String</span></span>|<span data-ttu-id="307d6-114">Указывает, когда можно удалить узлы из пула, если его размер уменьшается.</span><span class="sxs-lookup"><span data-stu-id="307d6-114">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="307d6-115">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="307d6-115">Possible values are:</span></span><br /><br /> <span data-ttu-id="307d6-116">**requeue** — завершает выполняющиеся задачи и повторно ставит их в очередь.</span><span class="sxs-lookup"><span data-stu-id="307d6-116">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="307d6-117">Задачи будут запущены повторно при включении задания.</span><span class="sxs-lookup"><span data-stu-id="307d6-117">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="307d6-118">Узлы удаляются сразу после завершения задач.</span><span class="sxs-lookup"><span data-stu-id="307d6-118">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="307d6-119">**terminate** — завершает выполняющиеся задачи.</span><span class="sxs-lookup"><span data-stu-id="307d6-119">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="307d6-120">Задачи не будут запущены повторно.</span><span class="sxs-lookup"><span data-stu-id="307d6-120">The tasks will not run again.</span></span> <span data-ttu-id="307d6-121">Узлы удаляются сразу после завершения задач.</span><span class="sxs-lookup"><span data-stu-id="307d6-121">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="307d6-122">**taskcompletion** — разрешает завершить текущие выполняющиеся задачи.</span><span class="sxs-lookup"><span data-stu-id="307d6-122">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="307d6-123">Во время ожидания новые задачи не планируются.</span><span class="sxs-lookup"><span data-stu-id="307d6-123">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="307d6-124">Узлы удаляются после выполнения всех задач.</span><span class="sxs-lookup"><span data-stu-id="307d6-124">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="307d6-125">**Retaineddata** — разрешает завершить текущие выполняющиеся задачи и затем ожидает, пока истекут сроки хранения данных для всех задач.</span><span class="sxs-lookup"><span data-stu-id="307d6-125">**Retaineddata** -  Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="307d6-126">Во время ожидания новые задачи не планируются.</span><span class="sxs-lookup"><span data-stu-id="307d6-126">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="307d6-127">Узлы удаляются после истечения сроков хранения для всех задач.</span><span class="sxs-lookup"><span data-stu-id="307d6-127">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="307d6-128">По умолчанию используется значение requeue.</span><span class="sxs-lookup"><span data-stu-id="307d6-128">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="307d6-129">Если размер пула увеличивается, устанавливается значение **invalid**.</span><span class="sxs-lookup"><span data-stu-id="307d6-129">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="307d6-130">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="307d6-130">currentDedicated</span></span>|<span data-ttu-id="307d6-131">Int32</span><span class="sxs-lookup"><span data-stu-id="307d6-131">Int32</span></span>|<span data-ttu-id="307d6-132">Число вычислительных узлов, назначенных пулу.</span><span class="sxs-lookup"><span data-stu-id="307d6-132">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="307d6-133">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="307d6-133">targetDedicated</span></span>|<span data-ttu-id="307d6-134">Int32</span><span class="sxs-lookup"><span data-stu-id="307d6-134">Int32</span></span>|<span data-ttu-id="307d6-135">Число вычислительных узлов, запрошенных для пула.</span><span class="sxs-lookup"><span data-stu-id="307d6-135">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="307d6-136">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="307d6-136">enableAutoScale</span></span>|<span data-ttu-id="307d6-137">Bool</span><span class="sxs-lookup"><span data-stu-id="307d6-137">Bool</span></span>|<span data-ttu-id="307d6-138">Указывает, корректируется ли размер пула автоматически с течением времени.</span><span class="sxs-lookup"><span data-stu-id="307d6-138">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="307d6-139">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="307d6-139">isAutoPool</span></span>|<span data-ttu-id="307d6-140">Bool</span><span class="sxs-lookup"><span data-stu-id="307d6-140">Bool</span></span>|<span data-ttu-id="307d6-141">Определяет, создан ли пул с помощью механизма AutoPool задания.</span><span class="sxs-lookup"><span data-stu-id="307d6-141">Specifies whether the pool was created via a job's AutoPool mechanism.</span></span>|
|<span data-ttu-id="307d6-142">startTime</span><span class="sxs-lookup"><span data-stu-id="307d6-142">startTime</span></span>|<span data-ttu-id="307d6-143">DateTime</span><span class="sxs-lookup"><span data-stu-id="307d6-143">DateTime</span></span>|<span data-ttu-id="307d6-144">Время, когда было начато изменение размера пула.</span><span class="sxs-lookup"><span data-stu-id="307d6-144">The time the pool resize started.</span></span>|
|<span data-ttu-id="307d6-145">endTime</span><span class="sxs-lookup"><span data-stu-id="307d6-145">endTime</span></span>|<span data-ttu-id="307d6-146">DateTime</span><span class="sxs-lookup"><span data-stu-id="307d6-146">DateTime</span></span>|<span data-ttu-id="307d6-147">Время, когда изменение размера пула было завершено.</span><span class="sxs-lookup"><span data-stu-id="307d6-147">The time the pool resize completed.</span></span>|
|<span data-ttu-id="307d6-148">resultCode</span><span class="sxs-lookup"><span data-stu-id="307d6-148">resultCode</span></span>|<span data-ttu-id="307d6-149">string</span><span class="sxs-lookup"><span data-stu-id="307d6-149">String</span></span>|<span data-ttu-id="307d6-150">Результат изменения размера.</span><span class="sxs-lookup"><span data-stu-id="307d6-150">The result of the resize.</span></span>|
|<span data-ttu-id="307d6-151">resultMessage</span><span class="sxs-lookup"><span data-stu-id="307d6-151">resultMessage</span></span>|<span data-ttu-id="307d6-152">Строка</span><span class="sxs-lookup"><span data-stu-id="307d6-152">String</span></span>|<span data-ttu-id="307d6-153">Ошибка изменения размера содержит сведения о результате.</span><span class="sxs-lookup"><span data-stu-id="307d6-153">The resize error includes the details of the result.</span></span><br /><br /> <span data-ttu-id="307d6-154">Если размер успешно изменен, сообщается, что операция выполнена.</span><span class="sxs-lookup"><span data-stu-id="307d6-154">If the resize completed successfully it states that the operation succeeded.</span></span>|