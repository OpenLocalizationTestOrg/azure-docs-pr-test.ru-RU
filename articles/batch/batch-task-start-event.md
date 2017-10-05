---
title: "Событие начала выполнения задачи пакетной службы Azure | Документы Майкрософт"
description: "Справочник по событию начала выполнения задачи пакетной службы."
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
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="task-start-event"></a><span data-ttu-id="b7c78-103">Событие начала выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="b7c78-103">Task start event</span></span>

 <span data-ttu-id="b7c78-104">Это событие возникает, когда планировщик планирует задачу для запуска на вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="b7c78-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="b7c78-105">Обратите внимание, что если задача повторно выполняется или помещается в очередь, то для нее снова возникает данное событие, при этом число повторов и версия системной задачи изменяются соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="b7c78-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="b7c78-106">Ниже приведен пример текста для события начала выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="b7c78-106">The following example shows the body of a task start event.</span></span>

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|<span data-ttu-id="b7c78-107">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b7c78-107">Element name</span></span>|<span data-ttu-id="b7c78-108">Тип</span><span class="sxs-lookup"><span data-stu-id="b7c78-108">Type</span></span>|<span data-ttu-id="b7c78-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="b7c78-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="b7c78-110">jobId</span><span class="sxs-lookup"><span data-stu-id="b7c78-110">jobId</span></span>|<span data-ttu-id="b7c78-111">Строка</span><span class="sxs-lookup"><span data-stu-id="b7c78-111">String</span></span>|<span data-ttu-id="b7c78-112">Идентификатор задания, содержащего задачу.</span><span class="sxs-lookup"><span data-stu-id="b7c78-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="b7c78-113">id</span><span class="sxs-lookup"><span data-stu-id="b7c78-113">id</span></span>|<span data-ttu-id="b7c78-114">string</span><span class="sxs-lookup"><span data-stu-id="b7c78-114">String</span></span>|<span data-ttu-id="b7c78-115">Идентификатор задачи.</span><span class="sxs-lookup"><span data-stu-id="b7c78-115">The id of the task.</span></span>|
|<span data-ttu-id="b7c78-116">taskType</span><span class="sxs-lookup"><span data-stu-id="b7c78-116">taskType</span></span>|<span data-ttu-id="b7c78-117">Строка</span><span class="sxs-lookup"><span data-stu-id="b7c78-117">String</span></span>|<span data-ttu-id="b7c78-118">Тип задачи.</span><span class="sxs-lookup"><span data-stu-id="b7c78-118">The type of the task.</span></span> <span data-ttu-id="b7c78-119">Может быть установлено значение "JobManager", указывающее, что это задача диспетчера заданий, или значение "User", указывающее, что задача не относится к диспетчеру заданий.</span><span class="sxs-lookup"><span data-stu-id="b7c78-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="b7c78-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="b7c78-120">systemTaskVersion</span></span>|<span data-ttu-id="b7c78-121">Int32</span><span class="sxs-lookup"><span data-stu-id="b7c78-121">Int32</span></span>|<span data-ttu-id="b7c78-122">Это внутренний счетчик повторных попыток для задачи.</span><span class="sxs-lookup"><span data-stu-id="b7c78-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="b7c78-123">Пакетная служба может повторить попытку выполнения задачи для преодоления временных неполадок.</span><span class="sxs-lookup"><span data-stu-id="b7c78-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="b7c78-124">В таким неполадкам относятся внутренние ошибки планирования и попытки восстановления из вычислительных узлов в неисправном состоянии.</span><span class="sxs-lookup"><span data-stu-id="b7c78-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="b7c78-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="b7c78-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="b7c78-126">Сложный тип</span><span class="sxs-lookup"><span data-stu-id="b7c78-126">Complex Type</span></span>|<span data-ttu-id="b7c78-127">Содержит сведения о вычислительном узле, где выполнялась задача.</span><span class="sxs-lookup"><span data-stu-id="b7c78-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="b7c78-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="b7c78-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="b7c78-129">Сложный тип</span><span class="sxs-lookup"><span data-stu-id="b7c78-129">Complex Type</span></span>|<span data-ttu-id="b7c78-130">Указывает, что задача включает в себя несколько экземпляров и требует несколько вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="b7c78-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="b7c78-131">Дополнительные сведения см. в статье [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).</span><span class="sxs-lookup"><span data-stu-id="b7c78-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="b7c78-132">constraints</span><span class="sxs-lookup"><span data-stu-id="b7c78-132">constraints</span></span>](#constraints)|<span data-ttu-id="b7c78-133">Сложный тип</span><span class="sxs-lookup"><span data-stu-id="b7c78-133">Complex Type</span></span>|<span data-ttu-id="b7c78-134">Ограничения выполнения, применяемые к этой задаче.</span><span class="sxs-lookup"><span data-stu-id="b7c78-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="b7c78-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="b7c78-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="b7c78-136">Сложный тип</span><span class="sxs-lookup"><span data-stu-id="b7c78-136">Complex Type</span></span>|<span data-ttu-id="b7c78-137">Содержит сведения о выполнении задачи.</span><span class="sxs-lookup"><span data-stu-id="b7c78-137">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="b7c78-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="b7c78-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="b7c78-139">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b7c78-139">Element name</span></span>|<span data-ttu-id="b7c78-140">Тип</span><span class="sxs-lookup"><span data-stu-id="b7c78-140">Type</span></span>|<span data-ttu-id="b7c78-141">Примечания</span><span class="sxs-lookup"><span data-stu-id="b7c78-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="b7c78-142">poolId</span><span class="sxs-lookup"><span data-stu-id="b7c78-142">poolId</span></span>|<span data-ttu-id="b7c78-143">Строка</span><span class="sxs-lookup"><span data-stu-id="b7c78-143">String</span></span>|<span data-ttu-id="b7c78-144">Идентификатор пула, где выполнялась задача.</span><span class="sxs-lookup"><span data-stu-id="b7c78-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="b7c78-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="b7c78-145">nodeId</span></span>|<span data-ttu-id="b7c78-146">Строка</span><span class="sxs-lookup"><span data-stu-id="b7c78-146">String</span></span>|<span data-ttu-id="b7c78-147">Идентификатор узла, где выполнялась задача.</span><span class="sxs-lookup"><span data-stu-id="b7c78-147">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="b7c78-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="b7c78-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="b7c78-149">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b7c78-149">Element name</span></span>|<span data-ttu-id="b7c78-150">Тип</span><span class="sxs-lookup"><span data-stu-id="b7c78-150">Type</span></span>|<span data-ttu-id="b7c78-151">Примечания</span><span class="sxs-lookup"><span data-stu-id="b7c78-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="b7c78-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="b7c78-152">numberOfInstances</span></span>|<span data-ttu-id="b7c78-153">int</span><span class="sxs-lookup"><span data-stu-id="b7c78-153">Int</span></span>|<span data-ttu-id="b7c78-154">Число вычислительных узлов, необходимых задаче.</span><span class="sxs-lookup"><span data-stu-id="b7c78-154">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="b7c78-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="b7c78-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="b7c78-156">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b7c78-156">Element name</span></span>|<span data-ttu-id="b7c78-157">Тип</span><span class="sxs-lookup"><span data-stu-id="b7c78-157">Type</span></span>|<span data-ttu-id="b7c78-158">Примечания</span><span class="sxs-lookup"><span data-stu-id="b7c78-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="b7c78-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="b7c78-159">maxTaskRetryCount</span></span>|<span data-ttu-id="b7c78-160">Int32</span><span class="sxs-lookup"><span data-stu-id="b7c78-160">Int32</span></span>|<span data-ttu-id="b7c78-161">Максимальное количество повторных попыток для задачи.</span><span class="sxs-lookup"><span data-stu-id="b7c78-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="b7c78-162">Пакетная служба пытается выполнить задачу повторно, если ее код выхода имеет ненулевое значение.</span><span class="sxs-lookup"><span data-stu-id="b7c78-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="b7c78-163">Обратите внимание, что это значение определяет количество повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="b7c78-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="b7c78-164">Пакетная служба попытается выполнить задачу один раз, а затем будет предпринимать повторные попытки вплоть до этого предела.</span><span class="sxs-lookup"><span data-stu-id="b7c78-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="b7c78-165">Например, если максимальное число повторных попыток равно 3, пакетная служба пытается выполнить задачу до 4 раз (одна начальная попытка и 3 повторных).</span><span class="sxs-lookup"><span data-stu-id="b7c78-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="b7c78-166">Если максимальное число повторных попыток равно 0, пакетная служба не пытается выполнить задачи повторно.</span><span class="sxs-lookup"><span data-stu-id="b7c78-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="b7c78-167">Если максимальное число повторных попыток равно –1, пакетная служба может повторять попытки сколько угодно.</span><span class="sxs-lookup"><span data-stu-id="b7c78-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="b7c78-168">Значение по умолчанию — 0 (без повторных попыток).</span><span class="sxs-lookup"><span data-stu-id="b7c78-168">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="b7c78-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="b7c78-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="b7c78-170">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b7c78-170">Element name</span></span>|<span data-ttu-id="b7c78-171">Тип</span><span class="sxs-lookup"><span data-stu-id="b7c78-171">Type</span></span>|<span data-ttu-id="b7c78-172">Примечания</span><span class="sxs-lookup"><span data-stu-id="b7c78-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="b7c78-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="b7c78-173">retryCount</span></span>|<span data-ttu-id="b7c78-174">Int32</span><span class="sxs-lookup"><span data-stu-id="b7c78-174">Int32</span></span>|<span data-ttu-id="b7c78-175">Число повторных попыток выполнения задачи пакетной службой.</span><span class="sxs-lookup"><span data-stu-id="b7c78-175">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="b7c78-176">Повторная попытка выполнения задачи предпринимается в случае ненулевого кода выхода, вплоть до указанного предела MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="b7c78-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
