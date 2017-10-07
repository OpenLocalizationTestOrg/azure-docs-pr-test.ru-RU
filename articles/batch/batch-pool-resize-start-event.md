---
title: "AAA» события запуска изменения размера пула пакетной службы Azure | Документы Microsoft»"
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="1d019-103">Событие начала изменения размера пула</span><span class="sxs-lookup"><span data-stu-id="1d019-103">Pool resize start event</span></span>

 <span data-ttu-id="1d019-104">Это событие создается, когда начинается изменение размера пула.</span><span class="sxs-lookup"><span data-stu-id="1d019-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="1d019-105">Поскольку изменения размера пула hello асинхронного события, можно ожидать завершения toobe событие завершения изменения размера пула, создается после hello операцию изменения размера.</span><span class="sxs-lookup"><span data-stu-id="1d019-105">Since hello pool resize is an asynchronous event, you can expect a pool resize complete event toobe emitted once hello resize operation completes.</span></span>

 <span data-ttu-id="1d019-106">Следующий пример, что показано hello тело событие начала изменения размера пула для пула, изменение размера от 0 too2 узлов с ручной Hello изменения размера.</span><span class="sxs-lookup"><span data-stu-id="1d019-106">hello following example shows hello body of a pool resize start event for a pool resizing from 0 too2 nodes with a manual resize.</span></span>

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

|<span data-ttu-id="1d019-107">Элемент</span><span class="sxs-lookup"><span data-stu-id="1d019-107">Element</span></span>|<span data-ttu-id="1d019-108">Тип</span><span class="sxs-lookup"><span data-stu-id="1d019-108">Type</span></span>|<span data-ttu-id="1d019-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="1d019-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="1d019-110">poolId</span><span class="sxs-lookup"><span data-stu-id="1d019-110">poolId</span></span>|<span data-ttu-id="1d019-111">Строка</span><span class="sxs-lookup"><span data-stu-id="1d019-111">String</span></span>|<span data-ttu-id="1d019-112">Идентификатор Hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="1d019-112">hello id of hello pool.</span></span>|
|<span data-ttu-id="1d019-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="1d019-113">nodeDeallocationOption</span></span>|<span data-ttu-id="1d019-114">Строка</span><span class="sxs-lookup"><span data-stu-id="1d019-114">String</span></span>|<span data-ttu-id="1d019-115">Указывает, когда узлы могут быть удалены из пула hello, если hello размер пула уменьшается.</span><span class="sxs-lookup"><span data-stu-id="1d019-115">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="1d019-116">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="1d019-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="1d019-117">**requeue** — завершает выполняющиеся задачи и повторно ставит их в очередь.</span><span class="sxs-lookup"><span data-stu-id="1d019-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="1d019-118">задачи Hello запустится еще раз, когда включено задание hello.</span><span class="sxs-lookup"><span data-stu-id="1d019-118">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="1d019-119">Узлы удаляются сразу после завершения задач.</span><span class="sxs-lookup"><span data-stu-id="1d019-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="1d019-120">**terminate** — завершает выполняющиеся задачи.</span><span class="sxs-lookup"><span data-stu-id="1d019-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="1d019-121">задачи Hello не запускается повторно.</span><span class="sxs-lookup"><span data-stu-id="1d019-121">hello tasks will not run again.</span></span> <span data-ttu-id="1d019-122">Узлы удаляются сразу после завершения задач.</span><span class="sxs-lookup"><span data-stu-id="1d019-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="1d019-123">**taskcompletion** — разрешить выполняющихся toocomplete задачи.</span><span class="sxs-lookup"><span data-stu-id="1d019-123">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="1d019-124">Во время ожидания новые задачи не планируются.</span><span class="sxs-lookup"><span data-stu-id="1d019-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="1d019-125">Узлы удаляются после выполнения всех задач.</span><span class="sxs-lookup"><span data-stu-id="1d019-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="1d019-126">**Retaineddata** — разрешить выполнение текущих задач toocomplete, а затем подождите, пока все задач tooexpire периодов хранения данных.</span><span class="sxs-lookup"><span data-stu-id="1d019-126">**Retaineddata** - Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="1d019-127">Во время ожидания новые задачи не планируются.</span><span class="sxs-lookup"><span data-stu-id="1d019-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="1d019-128">Узлы удаляются после истечения сроков хранения для всех задач.</span><span class="sxs-lookup"><span data-stu-id="1d019-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="1d019-129">значение по умолчанию Hello — повторной постановки в очередь.</span><span class="sxs-lookup"><span data-stu-id="1d019-129">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="1d019-130">Если увеличить размер пула hello, а затем hello значение слишком**недопустимый**.</span><span class="sxs-lookup"><span data-stu-id="1d019-130">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="1d019-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="1d019-131">currentDedicated</span></span>|<span data-ttu-id="1d019-132">Int32</span><span class="sxs-lookup"><span data-stu-id="1d019-132">Int32</span></span>|<span data-ttu-id="1d019-133">Hello количество вычислительных узлов в настоящее время назначен toohello пула.</span><span class="sxs-lookup"><span data-stu-id="1d019-133">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="1d019-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="1d019-134">targetDedicated</span></span>|<span data-ttu-id="1d019-135">Int32</span><span class="sxs-lookup"><span data-stu-id="1d019-135">Int32</span></span>|<span data-ttu-id="1d019-136">количество вычислительных узлов, которые запрашиваются для пула hello Hello.</span><span class="sxs-lookup"><span data-stu-id="1d019-136">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="1d019-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="1d019-137">enableAutoScale</span></span>|<span data-ttu-id="1d019-138">Bool</span><span class="sxs-lookup"><span data-stu-id="1d019-138">Bool</span></span>|<span data-ttu-id="1d019-139">Указывает, изменяется ли размер пула hello со временем.</span><span class="sxs-lookup"><span data-stu-id="1d019-139">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="1d019-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="1d019-140">isAutoPool</span></span>|<span data-ttu-id="1d019-141">Bool</span><span class="sxs-lookup"><span data-stu-id="1d019-141">Bool</span></span>|<span data-ttu-id="1d019-142">Указывает ли пул hello была создана с помощью механизма автоматический пул задания.</span><span class="sxs-lookup"><span data-stu-id="1d019-142">Speficies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
