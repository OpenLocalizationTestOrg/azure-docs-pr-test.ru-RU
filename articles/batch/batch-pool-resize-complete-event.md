---
title: "AAA» событие завершения, изменения размера пула пакетной службы Azure | Документы Microsoft»"
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
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a><span data-ttu-id="6dbaf-103">Событие завершения изменения размера пула</span><span class="sxs-lookup"><span data-stu-id="6dbaf-103">Pool resize complete event</span></span>

 <span data-ttu-id="6dbaf-104">Это событие создается при завершении или сбое операции изменения размера пула.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-104">This event is emitted when a pool resize has completed or failed.</span></span>

 <span data-ttu-id="6dbaf-105">Hello следующем примере показан текст hello завершения события изменения размера пула пула, увеличиваются в размере и успешно завершена.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-105">hello following example shows hello body of a pool resize complete event for a pool that increased in size and completed successfully.</span></span>

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
    "resizeError": "hello operation succeeded"
}
```

|<span data-ttu-id="6dbaf-106">Элемент</span><span class="sxs-lookup"><span data-stu-id="6dbaf-106">Element</span></span>|<span data-ttu-id="6dbaf-107">Тип</span><span class="sxs-lookup"><span data-stu-id="6dbaf-107">Type</span></span>|<span data-ttu-id="6dbaf-108">Примечания</span><span class="sxs-lookup"><span data-stu-id="6dbaf-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="6dbaf-109">id</span><span class="sxs-lookup"><span data-stu-id="6dbaf-109">id</span></span>|<span data-ttu-id="6dbaf-110">Строка</span><span class="sxs-lookup"><span data-stu-id="6dbaf-110">String</span></span>|<span data-ttu-id="6dbaf-111">Идентификатор Hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="6dbaf-112">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="6dbaf-112">nodeDeallocationOption</span></span>|<span data-ttu-id="6dbaf-113">Строка</span><span class="sxs-lookup"><span data-stu-id="6dbaf-113">String</span></span>|<span data-ttu-id="6dbaf-114">Указывает, когда узлы могут быть удалены из пула hello, если hello размер пула уменьшается.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-114">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="6dbaf-115">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="6dbaf-115">Possible values are:</span></span><br /><br /> <span data-ttu-id="6dbaf-116">**requeue** — завершает выполняющиеся задачи и повторно ставит их в очередь.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-116">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="6dbaf-117">задачи Hello запустится еще раз, когда включено задание hello.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-117">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="6dbaf-118">Узлы удаляются сразу после завершения задач.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-118">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="6dbaf-119">**terminate** — завершает выполняющиеся задачи.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-119">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="6dbaf-120">задачи Hello не запускается повторно.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-120">hello tasks will not run again.</span></span> <span data-ttu-id="6dbaf-121">Узлы удаляются сразу после завершения задач.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-121">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="6dbaf-122">**taskcompletion** — разрешить выполняющихся toocomplete задачи.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-122">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="6dbaf-123">Во время ожидания новые задачи не планируются.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-123">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="6dbaf-124">Узлы удаляются после выполнения всех задач.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-124">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="6dbaf-125">**Retaineddata** — разрешить выполнение текущих задач toocomplete, а затем подождите, пока все задач tooexpire периодов хранения данных.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-125">**Retaineddata** -  Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="6dbaf-126">Во время ожидания новые задачи не планируются.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-126">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="6dbaf-127">Узлы удаляются после истечения сроков хранения для всех задач.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-127">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="6dbaf-128">значение по умолчанию Hello — повторной постановки в очередь.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-128">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="6dbaf-129">Если увеличить размер пула hello, а затем hello значение слишком**недопустимый**.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-129">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="6dbaf-130">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="6dbaf-130">currentDedicated</span></span>|<span data-ttu-id="6dbaf-131">Int32</span><span class="sxs-lookup"><span data-stu-id="6dbaf-131">Int32</span></span>|<span data-ttu-id="6dbaf-132">Hello количество вычислительных узлов в настоящее время назначен toohello пула.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-132">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="6dbaf-133">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="6dbaf-133">targetDedicated</span></span>|<span data-ttu-id="6dbaf-134">Int32</span><span class="sxs-lookup"><span data-stu-id="6dbaf-134">Int32</span></span>|<span data-ttu-id="6dbaf-135">количество вычислительных узлов, которые запрашиваются для пула hello Hello.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-135">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="6dbaf-136">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="6dbaf-136">enableAutoScale</span></span>|<span data-ttu-id="6dbaf-137">Bool</span><span class="sxs-lookup"><span data-stu-id="6dbaf-137">Bool</span></span>|<span data-ttu-id="6dbaf-138">Указывает, изменяется ли размер пула hello со временем.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-138">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="6dbaf-139">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="6dbaf-139">isAutoPool</span></span>|<span data-ttu-id="6dbaf-140">Bool</span><span class="sxs-lookup"><span data-stu-id="6dbaf-140">Bool</span></span>|<span data-ttu-id="6dbaf-141">Указывает, был ли создан пул hello через механизм задания автоматический пул.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-141">Specifies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
|<span data-ttu-id="6dbaf-142">startTime</span><span class="sxs-lookup"><span data-stu-id="6dbaf-142">startTime</span></span>|<span data-ttu-id="6dbaf-143">DateTime</span><span class="sxs-lookup"><span data-stu-id="6dbaf-143">DateTime</span></span>|<span data-ttu-id="6dbaf-144">Hello время изменения размера пула hello запуска.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-144">hello time hello pool resize started.</span></span>|
|<span data-ttu-id="6dbaf-145">endTime</span><span class="sxs-lookup"><span data-stu-id="6dbaf-145">endTime</span></span>|<span data-ttu-id="6dbaf-146">DateTime</span><span class="sxs-lookup"><span data-stu-id="6dbaf-146">DateTime</span></span>|<span data-ttu-id="6dbaf-147">Hello время изменения размера пула hello завершения.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-147">hello time hello pool resize completed.</span></span>|
|<span data-ttu-id="6dbaf-148">resultCode</span><span class="sxs-lookup"><span data-stu-id="6dbaf-148">resultCode</span></span>|<span data-ttu-id="6dbaf-149">Строка</span><span class="sxs-lookup"><span data-stu-id="6dbaf-149">String</span></span>|<span data-ttu-id="6dbaf-150">Изменение размера Hello результат hello.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-150">hello result of hello resize.</span></span>|
|<span data-ttu-id="6dbaf-151">resultMessage</span><span class="sxs-lookup"><span data-stu-id="6dbaf-151">resultMessage</span></span>|<span data-ttu-id="6dbaf-152">Строка</span><span class="sxs-lookup"><span data-stu-id="6dbaf-152">String</span></span>|<span data-ttu-id="6dbaf-153">Ошибка изменения размера Hello содержит подробные сведения hello hello результата.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-153">hello resize error includes hello details of hello result.</span></span><br /><br /> <span data-ttu-id="6dbaf-154">Если размер hello успешно его состояний, которые hello операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="6dbaf-154">If hello resize completed successfully it states that hello operation succeeded.</span></span>|
