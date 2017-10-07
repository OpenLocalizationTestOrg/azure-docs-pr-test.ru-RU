---
title: "AAA» события начала задачи пакета Azure | Документы Microsoft»"
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a><span data-ttu-id="41475-103">Событие начала выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="41475-103">Task start event</span></span>

 <span data-ttu-id="41475-104">Это событие создается после запланированного toostart на вычислительном узле задачи планировщиком hello.</span><span class="sxs-lookup"><span data-stu-id="41475-104">This event is emitted once a task has been scheduled toostart on a compute node by hello scheduler.</span></span> <span data-ttu-id="41475-105">Обратите внимание, что если задачу hello повторно или повторно поставлен в очередь это событие будет создаваться повторно hello же задачу, но hello число повторных попыток и версию задачи системы будет обновлен соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="41475-105">Note that if hello task is retried or requeued this event will be emitted again for hello same task, but hello retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="41475-106">Hello следующем примере показан текст hello события начала задачи.</span><span class="sxs-lookup"><span data-stu-id="41475-106">hello following example shows hello body of a task start event.</span></span>

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

|<span data-ttu-id="41475-107">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="41475-107">Element name</span></span>|<span data-ttu-id="41475-108">Тип</span><span class="sxs-lookup"><span data-stu-id="41475-108">Type</span></span>|<span data-ttu-id="41475-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="41475-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="41475-110">jobId</span><span class="sxs-lookup"><span data-stu-id="41475-110">jobId</span></span>|<span data-ttu-id="41475-111">Строка</span><span class="sxs-lookup"><span data-stu-id="41475-111">String</span></span>|<span data-ttu-id="41475-112">Идентификатор Hello hello задания, содержащий задачу hello.</span><span class="sxs-lookup"><span data-stu-id="41475-112">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="41475-113">id</span><span class="sxs-lookup"><span data-stu-id="41475-113">id</span></span>|<span data-ttu-id="41475-114">Строка</span><span class="sxs-lookup"><span data-stu-id="41475-114">String</span></span>|<span data-ttu-id="41475-115">Идентификатор Hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="41475-115">hello id of hello task.</span></span>|
|<span data-ttu-id="41475-116">taskType</span><span class="sxs-lookup"><span data-stu-id="41475-116">taskType</span></span>|<span data-ttu-id="41475-117">Строка</span><span class="sxs-lookup"><span data-stu-id="41475-117">String</span></span>|<span data-ttu-id="41475-118">Тип Hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="41475-118">hello type of hello task.</span></span> <span data-ttu-id="41475-119">Может быть установлено значение "JobManager", указывающее, что это задача диспетчера заданий, или значение "User", указывающее, что задача не относится к диспетчеру заданий.</span><span class="sxs-lookup"><span data-stu-id="41475-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="41475-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="41475-120">systemTaskVersion</span></span>|<span data-ttu-id="41475-121">Int32</span><span class="sxs-lookup"><span data-stu-id="41475-121">Int32</span></span>|<span data-ttu-id="41475-122">Это счетчик hello внутренних повторов задачи.</span><span class="sxs-lookup"><span data-stu-id="41475-122">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="41475-123">Внутренне hello пакетной службы можно повторить попытку tooaccount задачи для временных проблем.</span><span class="sxs-lookup"><span data-stu-id="41475-123">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="41475-124">Эти проблемы могут включать внутреннего планирования toorecover ошибок или попыток из вычислительных узлов в неверном состоянии.</span><span class="sxs-lookup"><span data-stu-id="41475-124">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="41475-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="41475-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="41475-126">Сложный тип</span><span class="sxs-lookup"><span data-stu-id="41475-126">Complex Type</span></span>|<span data-ttu-id="41475-127">Содержит сведения о hello вычислительных узлов, на какие hello запущена задача.</span><span class="sxs-lookup"><span data-stu-id="41475-127">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="41475-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="41475-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="41475-129">Сложный тип</span><span class="sxs-lookup"><span data-stu-id="41475-129">Complex Type</span></span>|<span data-ttu-id="41475-130">Указывает, что эта задача hello осуществляется несколькими экземплярами требуется несколько вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="41475-130">Specifies that hello task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="41475-131">Дополнительные сведения см. в статье [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).</span><span class="sxs-lookup"><span data-stu-id="41475-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="41475-132">constraints</span><span class="sxs-lookup"><span data-stu-id="41475-132">constraints</span></span>](#constraints)|<span data-ttu-id="41475-133">Сложный тип</span><span class="sxs-lookup"><span data-stu-id="41475-133">Complex Type</span></span>|<span data-ttu-id="41475-134">ограничения выполнения Hello применимые toothis задачи.</span><span class="sxs-lookup"><span data-stu-id="41475-134">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="41475-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="41475-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="41475-136">Сложный тип</span><span class="sxs-lookup"><span data-stu-id="41475-136">Complex Type</span></span>|<span data-ttu-id="41475-137">Содержит сведения о выполнении hello задачи «hello».</span><span class="sxs-lookup"><span data-stu-id="41475-137">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="41475-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="41475-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="41475-139">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="41475-139">Element name</span></span>|<span data-ttu-id="41475-140">Тип</span><span class="sxs-lookup"><span data-stu-id="41475-140">Type</span></span>|<span data-ttu-id="41475-141">Примечания</span><span class="sxs-lookup"><span data-stu-id="41475-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="41475-142">poolId</span><span class="sxs-lookup"><span data-stu-id="41475-142">poolId</span></span>|<span data-ttu-id="41475-143">Строка</span><span class="sxs-lookup"><span data-stu-id="41475-143">String</span></span>|<span data-ttu-id="41475-144">Идентификатор Hello пула hello, на какие hello запущена задача.</span><span class="sxs-lookup"><span data-stu-id="41475-144">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="41475-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="41475-145">nodeId</span></span>|<span data-ttu-id="41475-146">Строка</span><span class="sxs-lookup"><span data-stu-id="41475-146">String</span></span>|<span data-ttu-id="41475-147">Идентификатор Hello hello узла, на какие hello запущена задача.</span><span class="sxs-lookup"><span data-stu-id="41475-147">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="41475-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="41475-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="41475-149">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="41475-149">Element name</span></span>|<span data-ttu-id="41475-150">Тип</span><span class="sxs-lookup"><span data-stu-id="41475-150">Type</span></span>|<span data-ttu-id="41475-151">Примечания</span><span class="sxs-lookup"><span data-stu-id="41475-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="41475-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="41475-152">numberOfInstances</span></span>|<span data-ttu-id="41475-153">int</span><span class="sxs-lookup"><span data-stu-id="41475-153">Int</span></span>|<span data-ttu-id="41475-154">количество вычислительных узлов, предусмотренного задачу hello Hello.</span><span class="sxs-lookup"><span data-stu-id="41475-154">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="41475-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="41475-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="41475-156">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="41475-156">Element name</span></span>|<span data-ttu-id="41475-157">Тип</span><span class="sxs-lookup"><span data-stu-id="41475-157">Type</span></span>|<span data-ttu-id="41475-158">Примечания</span><span class="sxs-lookup"><span data-stu-id="41475-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="41475-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="41475-159">maxTaskRetryCount</span></span>|<span data-ttu-id="41475-160">Int32</span><span class="sxs-lookup"><span data-stu-id="41475-160">Int32</span></span>|<span data-ttu-id="41475-161">Максимальное число повторных попыток задачу hello может быть Hello.</span><span class="sxs-lookup"><span data-stu-id="41475-161">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="41475-162">Hello пакетная служба повторяет задачу, если ее код выхода имеет ненулевое значение.</span><span class="sxs-lookup"><span data-stu-id="41475-162">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="41475-163">Обратите внимание, что это значение определяет специально hello число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="41475-163">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="41475-164">Пакетная служба Hello попытаться задачу hello один раз и повторите копирование toothis ограничение.</span><span class="sxs-lookup"><span data-stu-id="41475-164">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="41475-165">Например если hello максимальное число повторных попыток равно 3, пакет пытается задачи вверх too4 времени (один начальной попытки и 3 попытки).</span><span class="sxs-lookup"><span data-stu-id="41475-165">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="41475-166">Если hello максимальное число повторных попыток равно 0, hello пакетная служба не выполняет повторную попытку запуска задачи.</span><span class="sxs-lookup"><span data-stu-id="41475-166">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="41475-167">Если hello максимальное число повторных попыток равно -1, hello пакетная служба повторяет задачи без ограничения.</span><span class="sxs-lookup"><span data-stu-id="41475-167">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="41475-168">значение по умолчанию Hello равно 0 (повторы отсутствуют).</span><span class="sxs-lookup"><span data-stu-id="41475-168">hello default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="41475-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="41475-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="41475-170">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="41475-170">Element name</span></span>|<span data-ttu-id="41475-171">Тип</span><span class="sxs-lookup"><span data-stu-id="41475-171">Type</span></span>|<span data-ttu-id="41475-172">Примечания</span><span class="sxs-lookup"><span data-stu-id="41475-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="41475-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="41475-173">retryCount</span></span>|<span data-ttu-id="41475-174">Int32</span><span class="sxs-lookup"><span data-stu-id="41475-174">Int32</span></span>|<span data-ttu-id="41475-175">Здравствуйте, число повторных попыток задачу hello пакетной службой hello.</span><span class="sxs-lookup"><span data-stu-id="41475-175">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="41475-176">Задача Hello перезапускается, если он выходит с ненулевой код выхода, копирование toohello указан MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="41475-176">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount</span></span>|
