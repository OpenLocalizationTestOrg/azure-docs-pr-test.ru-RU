---
title: "aaaPersist заданий и задач вывода tooAzure хранилища с библиотекой hello файлов, принятых для .NET — пакетной службы Azure | Документы Microsoft"
description: "Узнайте, как библиотека toouse соглашения файлов пакета Azure для .NET toopersist задачи пакета и tooAzure выходные данные задания хранилища и представление hello сохраняются выходные данные в hello портал Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a><span data-ttu-id="9afff-103">Сохранение заданий и задач tooAzure данные хранилища с библиотекой hello пакетных файлов, принятых для .NET toopersist</span><span class="sxs-lookup"><span data-stu-id="9afff-103">Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="9afff-104">Одним из способов toopersist данных задачи — toouse hello [Azure пакетных файлов, принятых библиотека для .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="9afff-104">One way toopersist task data is toouse hello [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="9afff-105">Hello библиотеки соглашения файлов упрощает процесс сохранения выходных данных задачи hello tooAzure данных хранения и извлечения.</span><span class="sxs-lookup"><span data-stu-id="9afff-105">hello File Conventions library simplifies hello process of storing task output data tooAzure Storage and retrieving it.</span></span> <span data-ttu-id="9afff-106">Можно использовать библиотеку hello файлов, принятых в коде задачи и клиента &mdash; в коде задачи для сохранения файлов и в клиенте кода toolist и извлекать их.</span><span class="sxs-lookup"><span data-stu-id="9afff-106">You can use hello File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code toolist and retrieve them.</span></span> <span data-ttu-id="9afff-107">Код задачи можно также использовать hello библиотеки tooretrieve hello выходные данные вышестоящего задачи, такие как в [зависимости задач](batch-task-dependencies.md) сценария.</span><span class="sxs-lookup"><span data-stu-id="9afff-107">Your task code can also use hello library tooretrieve hello output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="9afff-108">tooretrieve выходные файлы с библиотекой hello соглашения файлов, можно найти файлы hello данное задание или задачу, указав их по Идентификатору и цели.</span><span class="sxs-lookup"><span data-stu-id="9afff-108">tooretrieve output files with hello File Conventions library, you can locate hello files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="9afff-109">Не нужно tooknow hello имена и местоположения файлов hello.</span><span class="sxs-lookup"><span data-stu-id="9afff-109">You don't need tooknow hello names or locations of hello files.</span></span> <span data-ttu-id="9afff-110">Например можно использовать все промежуточные файлы библиотеки toolist hello соглашения файлов для данной задачи или получить файл предварительного просмотра для данного задания.</span><span class="sxs-lookup"><span data-stu-id="9afff-110">For example, you can use hello File Conventions library toolist all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="9afff-111">Начиная с версии 2017 г-05-01, hello API пакетной службы поддерживает сохранение вывода данных tooAzure хранилища для задач и задание диспетчера задач, выполняемых на пулы, созданных с помощью hello конфигурации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9afff-111">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools created with hello virtual machine configuration.</span></span> <span data-ttu-id="9afff-112">Hello API пакетной службы предоставляет простой способ toopersist выходные данные в коде hello, которое создает задачу и служит в качестве библиотеку альтернативных toohello соглашения файлов.</span><span class="sxs-lookup"><span data-stu-id="9afff-112">hello Batch service API provides a simple way toopersist output from within hello code that creates a task and serves as an alternative toohello File Conventions library.</span></span> <span data-ttu-id="9afff-113">Можно изменить выходные данные toopersist пакета клиентских приложений без необходимости приложения hello tooupdate, на котором работает ваша задача.</span><span class="sxs-lookup"><span data-stu-id="9afff-113">You can modify your Batch client applications toopersist output without needing tooupdate hello application that your task is running.</span></span> <span data-ttu-id="9afff-114">Дополнительные сведения см. в разделе [сохранения данных задач tooAzure хранилища с hello API пакетной службы](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="9afff-114">For more information, see [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a><span data-ttu-id="9afff-115">Когда использовать выходные данные задачи toopersist hello соглашения файл библиотеки?</span><span class="sxs-lookup"><span data-stu-id="9afff-115">When do I use hello File Conventions library toopersist task output?</span></span>

<span data-ttu-id="9afff-116">Пакет Azure предоставляет несколько способов toopersist выходные данные задачи.</span><span class="sxs-lookup"><span data-stu-id="9afff-116">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="9afff-117">Hello соглашения файлов является наиболее подходит toothese сценариев:</span><span class="sxs-lookup"><span data-stu-id="9afff-117">hello File Conventions is best suited toothese scenarios:</span></span>

- <span data-ttu-id="9afff-118">Можно легко изменить hello код приложения hello, что ваша задача запущена toopersist файлы с помощью библиотеки файлов, принятых hello.</span><span class="sxs-lookup"><span data-stu-id="9afff-118">You can easily modify hello code for hello application that your task is running toopersist files using hello File Conventions library.</span></span>
- <span data-ttu-id="9afff-119">Во время выполнения hello задачи по-прежнему требуется tooAzure toostream данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afff-119">You want toostream data tooAzure Storage while hello task is still running.</span></span>
- <span data-ttu-id="9afff-120">Вы хотите toopersist данные из пулов, созданных с помощью hello конфигурацию облачной службы или конфигурации виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="9afff-120">You want toopersist data from pools created with either hello cloud service configuration or hello virtual machine configuration.</span></span>
- <span data-ttu-id="9afff-121">Клиентское приложение или другие задачи в hello заданий toolocate потребностей и загрузки выходных файлов задач по Идентификатору или по назначению.</span><span class="sxs-lookup"><span data-stu-id="9afff-121">Your client application or other tasks in hello job needs toolocate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="9afff-122">Вы хотите tooview выходные данные задачи в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9afff-122">You want tooview task output in hello Azure portal.</span></span>

<span data-ttu-id="9afff-123">Если ваш сценарий отличается от перечисленных выше, может потребоваться tooconsider другой подход.</span><span class="sxs-lookup"><span data-stu-id="9afff-123">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="9afff-124">Дополнительные сведения о других способах сохранения выходных данных задачи. в разделе [Persist заданий и задач вывода tooAzure хранения](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="9afff-124">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-hello-batch-file-conventions-standard"></a><span data-ttu-id="9afff-125">Что такое hello пакетных файлов, принятых standard?</span><span class="sxs-lookup"><span data-stu-id="9afff-125">What is hello Batch File Conventions standard?</span></span>

<span data-ttu-id="9afff-126">Hello [пакетных файлов, принятых standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) предоставляет схему именования контейнеров назначения hello и выходные файлы записываются toowhich пути большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="9afff-126">hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for hello destination containers and blob paths toowhich your output files are written.</span></span> <span data-ttu-id="9afff-127">TooAzure сохраненные файлы хранилища, которые соответствуют toohello стандартные соглашения файлов автоматически доступны для просмотра в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9afff-127">Files persisted tooAzure Storage that adhere toohello File Conventions standard are automatically available for viewing in hello Azure portal.</span></span> <span data-ttu-id="9afff-128">портал Hello учитывает соглашения об именовании hello и поэтому может отображать файлы, удовлетворяющие tooit.</span><span class="sxs-lookup"><span data-stu-id="9afff-128">hello portal is aware of hello naming convention and so can display files that adhere tooit.</span></span>

<span data-ttu-id="9afff-129">Hello соглашения файлов библиотеки для .NET автоматически имен вашей контейнеров хранилища и выходных файлов задач toohello стандартные соглашения файлов в соответствии с.</span><span class="sxs-lookup"><span data-stu-id="9afff-129">hello File Conventions library for .NET automatically names your storage containers and task output files according toohello File Conventions standard.</span></span> <span data-ttu-id="9afff-130">Hello файлов, принятых библиотека также предоставляет методы tooquery выходные файлы в хранилище Azure toojob идентификатор, идентификатор задачи или назначения в соответствии с.</span><span class="sxs-lookup"><span data-stu-id="9afff-130">hello File Conventions library also provides methods tooquery output files in Azure Storage according toojob ID, task ID, or purpose.</span></span>   

<span data-ttu-id="9afff-131">При разработке на языке, отличном от .NET, можно реализовать стандартного соглашения файлов hello самостоятельно в приложении.</span><span class="sxs-lookup"><span data-stu-id="9afff-131">If you are developing with a language other than .NET, you can implement hello File Conventions standard yourself in your application.</span></span> <span data-ttu-id="9afff-132">Дополнительные сведения см. в разделе [о стандартных пакетных файлов, принятых hello](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="9afff-132">For more information, see [About hello Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a><span data-ttu-id="9afff-133">Связать tooyour учетной записи хранилища Azure пакетной учетной записи</span><span class="sxs-lookup"><span data-stu-id="9afff-133">Link an Azure Storage account tooyour Batch account</span></span>

<span data-ttu-id="9afff-134">данные вывода toopersist tooAzure хранилища с помощью hello соглашения файл библиотеки, необходимо сначала связать tooyour учетной записи хранилища Azure пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9afff-134">toopersist output data tooAzure Storage using hello File Conventions library, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="9afff-135">Если вы еще не сделали этого, связать tooyour учетной записи хранилища пакетной учетной записи с помощью hello [портал Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="9afff-135">If you haven't done so already, link a Storage account tooyour Batch account by using hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="9afff-136">Перейдите tooyour пакетной учетной записи в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9afff-136">Navigate tooyour Batch account in hello Azure portal.</span></span> 
2. <span data-ttu-id="9afff-137">В разделе **Параметры** выберите **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="9afff-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="9afff-138">Если у вас еще нет учетной записи хранения, связанной с вашей учетной записью пакетной службы, нажмите кнопку **Учетная запись хранения (нет)**.</span><span class="sxs-lookup"><span data-stu-id="9afff-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="9afff-139">Выберите учетную запись хранения из списка hello для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="9afff-139">Select a Storage account from hello list for your subscription.</span></span> <span data-ttu-id="9afff-140">Для повышения производительности рекомендуется использовать учетную запись хранилища Azure, hello же регионе, что учетной записи пакетной hello запущенным задачами.</span><span class="sxs-lookup"><span data-stu-id="9afff-140">For best performance, use an Azure Storage account that is in hello same region as hello Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="9afff-141">Сохранение выходных данных</span><span class="sxs-lookup"><span data-stu-id="9afff-141">Persist output data</span></span>

<span data-ttu-id="9afff-142">toopersist заданий и задач выходных данных с библиотекой файлов, принятых hello, создать контейнер в хранилище Azure, а затем сохраните hello выходной toohello контейнер.</span><span class="sxs-lookup"><span data-stu-id="9afff-142">toopersist job and task output data with hello File Conventions library, create a container in Azure Storage, then save hello output toohello container.</span></span> <span data-ttu-id="9afff-143">Используйте hello [клиентской библиотеки хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage) в контейнере toohello выходные данные задачи кода tooupload hello задачи.</span><span class="sxs-lookup"><span data-stu-id="9afff-143">Use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code tooupload hello task output toohello container.</span></span> 

<span data-ttu-id="9afff-144">Дополнительные сведения о работе с контейнерами и большими двоичными объектами в службе хранилища Azure см. в разделе [Приступая к работе со службой хранилища больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="9afff-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="9afff-145">Сохраняются все выходные данные заданий и задач с файлов, принятых hello библиотеки хранятся в hello в одном контейнере.</span><span class="sxs-lookup"><span data-stu-id="9afff-145">All job and task outputs persisted with hello File Conventions library are stored in hello same container.</span></span> <span data-ttu-id="9afff-146">Если большого числа задач toopersist файлы hello же времени, [хранилища ограничивает](../storage/common/storage-performance-checklist.md#blobs) может применяться.</span><span class="sxs-lookup"><span data-stu-id="9afff-146">If a large number of tasks try toopersist files at hello same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="9afff-147">Создание контейнера хранилища</span><span class="sxs-lookup"><span data-stu-id="9afff-147">Create storage container</span></span>

<span data-ttu-id="9afff-148">tooAzure выходные данные задачи toopersist хранилища, сначала создайте контейнер, вызвав [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="9afff-148">toopersist task output tooAzure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="9afff-149">Этот метод расширения принимает объект [CloudStorageAccount][net_cloudstorageaccount] в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="9afff-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="9afff-150">Он создает контейнер, именованный соответствующим toohello файлов, принятых Standard Edition, таким образом, его содержимое, видимые hello Azure портал и hello методы получения, описанных далее в статье hello.</span><span class="sxs-lookup"><span data-stu-id="9afff-150">It creates a container named according toohello File Conventions standard,so that its contents are discoverable by hello Azure portal and hello retrieval methods discussed later in hello article.</span></span>

<span data-ttu-id="9afff-151">Обычно помещаются в клиентском приложении toocreate кода hello контейнер &mdash; hello приложение, которое создает ваш пулы, заданий и задач.</span><span class="sxs-lookup"><span data-stu-id="9afff-151">You typically place hello code toocreate a container in your client application &mdash; hello application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="9afff-152">Хранение выходных данных задач</span><span class="sxs-lookup"><span data-stu-id="9afff-152">Store task outputs</span></span>

<span data-ttu-id="9afff-153">Теперь, когда подготовлен контейнера в хранилище Azure, задачи можно сохранить выходной toohello контейнер с помощью hello [TaskOutputStorage] [ net_taskoutputstorage] класса, найденный в библиотеке файлов, принятых hello.</span><span class="sxs-lookup"><span data-stu-id="9afff-153">Now that you've prepared a container in Azure Storage, tasks can save output toohello container by using hello [TaskOutputStorage][net_taskoutputstorage] class found in hello File Conventions library.</span></span>

<span data-ttu-id="9afff-154">В коде задач, сначала создайте [TaskOutputStorage] [ net_taskoutputstorage] объекта, а затем при задачу hello завершил свою работу, вызовите hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] toosave метод tooAzure его выходные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afff-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when hello task has completed its work, call hello [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method toosave its output tooAzure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="9afff-155">Hello `kind` параметр hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) метод классифицирует hello сохраняются файлы.</span><span class="sxs-lookup"><span data-stu-id="9afff-155">hello `kind` parameter of hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes hello persisted files.</span></span> <span data-ttu-id="9afff-156">Существует четыре стандартных типа [TaskOutputKind] [net_taskoutputkind]: `TaskOutput`, `TaskPreview`, `TaskLog` и `TaskIntermediate.`. Также можно определить пользовательские категории выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9afff-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="9afff-157">Эти типы выходных данных позволяют toospecify, какой тип toolist выходные данные при hello позже запросе пакета сохраняются выходные значения данной задачи.</span><span class="sxs-lookup"><span data-stu-id="9afff-157">These output types allow you toospecify which type of outputs toolist when you later query Batch for hello persisted outputs of a given task.</span></span> <span data-ttu-id="9afff-158">Другими словами при перечислении hello выходные данные задачи, можно отфильтровать список hello в одном из выходных данных типа hello.</span><span class="sxs-lookup"><span data-stu-id="9afff-158">In other words, when you list hello outputs for a task, you can filter hello list on one of hello output types.</span></span> <span data-ttu-id="9afff-159">Например «приведите hello *предварительного просмотра* выходных данных для задачи *109*.»</span><span class="sxs-lookup"><span data-stu-id="9afff-159">For example, "Give me hello *preview* output for task *109*."</span></span> <span data-ttu-id="9afff-160">Дополнительные сведения о со списком и получение выходных данных отображается в [получить выходные данные](#retrieve-output) далее в статье hello.</span><span class="sxs-lookup"><span data-stu-id="9afff-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in hello article.</span></span>

> [!TIP]
> <span data-ttu-id="9afff-161">Hello тип выходных данных также определяет, где в hello Azure portal конкретного файла будет: *TaskOutput*-файлы по категориям, отображаются в списке **задач выходные файлы**, и *TaskLog*файлы отображаются в списке **задач журналы**.</span><span class="sxs-lookup"><span data-stu-id="9afff-161">hello output kind also determines where in hello Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="9afff-162">Хранения выходных данных заданий</span><span class="sxs-lookup"><span data-stu-id="9afff-162">Store job outputs</span></span>

<span data-ttu-id="9afff-163">Кроме выводит toostoring задачи, можно хранить hello выходные данные, связанные с заданием целиком.</span><span class="sxs-lookup"><span data-stu-id="9afff-163">In addition toostoring task outputs, you can store hello outputs associated with an entire job.</span></span> <span data-ttu-id="9afff-164">Например в задаче слияния hello задания подготовки к просмотру фильма может сохраняться фильма hello полностью к просмотру как выходные данные задания.</span><span class="sxs-lookup"><span data-stu-id="9afff-164">For example, in hello merge task of a movie rendering job, you could persist hello fully rendered movie as a job output.</span></span> <span data-ttu-id="9afff-165">После завершения задания клиентского приложения можно перечислить и получить выходные данные hello для задания hello и не требуется tooquery hello отдельные задачи.</span><span class="sxs-lookup"><span data-stu-id="9afff-165">When your job is completed, your client application can list and retrieve hello outputs for hello job, and does not need tooquery hello individual tasks.</span></span>

<span data-ttu-id="9afff-166">Сохранить выходные данные задания, вызывающему Привет [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] метода и укажите hello [JobOutputKind] [ net_joboutputkind] и имя файла:</span><span class="sxs-lookup"><span data-stu-id="9afff-166">Store job output by calling hello [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify hello [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="9afff-167">Как и в hello **TaskOutputKind** типа для выходных данных задачи, используйте hello [JobOutputKind] [ net_joboutputkind] toocategorize тип задания сохранения файлов.</span><span class="sxs-lookup"><span data-stu-id="9afff-167">As with hello **TaskOutputKind** type for task outputs, you use hello [JobOutputKind][net_joboutputkind] type toocategorize a job's persisted files.</span></span> <span data-ttu-id="9afff-168">Этот параметр позволяет toolater запроса (список) определенного типа выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9afff-168">This parameter allows you toolater query for (list) a specific type of output.</span></span> <span data-ttu-id="9afff-169">Hello **JobOutputKind** типа включает категорий выходных данных и предварительного просмотра, а также поддерживает создание пользовательских категорий.</span><span class="sxs-lookup"><span data-stu-id="9afff-169">hello **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="9afff-170">Хранение журналов задач</span><span class="sxs-lookup"><span data-stu-id="9afff-170">Store task logs</span></span>

<span data-ttu-id="9afff-171">В дополнение к этому toopersisting хранения toodurable файлов, когда задача или задание завершается, может потребоваться toopersist файлы, которые обновляются во время выполнения задачи hello &mdash; файлы журнала или `stdout.txt` и `stderr.txt`, например.</span><span class="sxs-lookup"><span data-stu-id="9afff-171">In addition toopersisting a file toodurable storage when a task or job completes, you may need toopersist files that are updated during hello execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="9afff-172">Для этой цели hello Azure пакетных файлов, принятых библиотека предоставляет hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] метод.</span><span class="sxs-lookup"><span data-stu-id="9afff-172">For this purpose, hello Azure Batch File Conventions library provides hello [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="9afff-173">С [SaveTrackedAsync][net_savetrackedasync], можно отслеживать файл tooa обновлений на узле hello (с интервалом, можно указать) и сохранять эти обновления tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afff-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates tooa file on hello node (at an interval that you specify) and persist those updates tooAzure Storage.</span></span>

<span data-ttu-id="9afff-174">В следующий фрагмент кода hello, мы используем [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` в хранилище Azure каждые 15 секунд во время выполнения hello задачи «hello»:</span><span class="sxs-lookup"><span data-stu-id="9afff-174">In hello following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage every 15 seconds during hello execution of hello task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="9afff-175">раздел в комментарий Hello `Code tooprocess data and produce output file(s)` — это заполнитель для кода hello, как правило, выполняет свою задачу.</span><span class="sxs-lookup"><span data-stu-id="9afff-175">hello commented section `Code tooprocess data and produce output file(s)` is a placeholder for hello code that your task would normally perform.</span></span> <span data-ttu-id="9afff-176">Например, вам может понадобиться код, который скачивает данные из службы хранилища Azure и выполняет с ними операцию преобразования или вычисления.</span><span class="sxs-lookup"><span data-stu-id="9afff-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="9afff-177">важной частью этот фрагмент кода Hello дает переноса такого кода в `using` tooperiodically блок обновления файла с [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="9afff-177">hello important part of this snippet is demonstrating how you can wrap such code in a `using` block tooperiodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="9afff-178">агент узла Hello — это программа, которая запускается на каждом узле в пуле hello и предоставляет интерфейс команды управления hello между узлом hello и hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9afff-178">hello node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="9afff-179">Hello `Task.Delay` вызов не требуется в конце hello это `using` tooensure блока, hello агента узла имеет содержимое hello tooflush времени стандарта toohello stdout.txt файл на узле hello.</span><span class="sxs-lookup"><span data-stu-id="9afff-179">hello `Task.Delay` call is required at hello end of this `using` block tooensure that hello node agent has time tooflush hello contents of standard out toohello stdout.txt file on hello node.</span></span> <span data-ttu-id="9afff-180">Эта задержка не имея ее возможные toomiss hello последние несколько секунд выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9afff-180">Without this delay, it is possible toomiss hello last few seconds of output.</span></span> <span data-ttu-id="9afff-181">Задержка может не потребоваться для всех файлов.</span><span class="sxs-lookup"><span data-stu-id="9afff-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="9afff-182">При включении отслеживания с помощью файла **SaveTrackedAsync**только *добавляет* toohello отслеживаемого файла, сохраненного tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afff-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* toohello tracked file are persisted tooAzure Storage.</span></span> <span data-ttu-id="9afff-183">Используйте этот метод только для отслеживания не Смена файлов журнала или других файлов, которые записываются toowith добавить операции toohello конец файла hello.</span><span class="sxs-lookup"><span data-stu-id="9afff-183">Use this method only for tracking non-rotating log files or other files that are written toowith append operations toohello end of hello file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="9afff-184">Извлечение выходных данных</span><span class="sxs-lookup"><span data-stu-id="9afff-184">Retrieve output data</span></span>

<span data-ttu-id="9afff-185">При извлечении материализованный выходных данных с использованием библиотеки Azure пакетных файлов, принятых hello, осуществляется в виде задач и задание ориентированное.</span><span class="sxs-lookup"><span data-stu-id="9afff-185">When you retrieve your persisted output using hello Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="9afff-186">Можно запросить hello выходных данных для данной задачи или задания без необходимости tooknow пути в хранилище Azure или даже именем файла.</span><span class="sxs-lookup"><span data-stu-id="9afff-186">You can request hello output for given task or job without needing tooknow its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="9afff-187">Вместо этого выходные файлы можно запрашивать по идентификатору задачи или задания.</span><span class="sxs-lookup"><span data-stu-id="9afff-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="9afff-188">Hello следующий фрагмент кода перебор рабочих заданий, выводит некоторые сведения о hello выходные файлы для задачи «hello» и затем загружает его файлы из хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afff-188">hello following code snippet iterates through a job's tasks, prints some information about hello output files for hello task, and then downloads its files from Storage.</span></span>

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a><span data-ttu-id="9afff-189">Просмотр выходных файлов hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9afff-189">View output files in hello Azure portal</span></span>

<span data-ttu-id="9afff-190">Hello Azure портал отобразит выходных файлов задач и журналов, которые являются сохраненного tooa связанной учетной записи хранилища Azure с помощью hello [пакетных файлов, принятых standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="9afff-190">hello Azure portal displays task output files and logs that are persisted tooa linked Azure Storage account using hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="9afff-191">Можно реализовать эти соглашения о себе в hello язык или библиотеку hello соглашения файлов можно использовать в приложениях .NET.</span><span class="sxs-lookup"><span data-stu-id="9afff-191">You can implement these conventions yourself in hello a language of your choice, or you can use hello File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="9afff-192">Отображение hello tooenable выходные файлы в портале hello, должен удовлетворять hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="9afff-192">tooenable hello display of your output files in hello portal, you must satisfy hello following requirements:</span></span>

1. <span data-ttu-id="9afff-193">[Связать учетную запись хранилища Azure](#requirement-linked-storage-account) tooyour пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9afff-193">[Link an Azure Storage account](#requirement-linked-storage-account) tooyour Batch account.</span></span>
2. <span data-ttu-id="9afff-194">Следовать toohello стандартные соглашения об именовании для файлов и контейнеров хранилища, при сохранении выходные данные.</span><span class="sxs-lookup"><span data-stu-id="9afff-194">Adhere toohello predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="9afff-195">Определение hello из этих правил можно найти в hello соглашения файлов библиотеки [README][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="9afff-195">You can find hello definition of these conventions in hello File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="9afff-196">При использовании hello [Azure пакетных файлов, принятых] [ nuget_package] toopersist библиотеки на выход, файлы сохраняются toohello стандартные соглашения файлов в соответствии с.</span><span class="sxs-lookup"><span data-stu-id="9afff-196">If you use hello [Azure Batch File Conventions][nuget_package] library toopersist your output, your files are persisted according toohello File Conventions standard.</span></span>

<span data-ttu-id="9afff-197">выходные данные задачи tooview файлы и журналы в hello портал Azure, переходы toohello задаче, выходные данные которого вас интересуют, затем выберите пункт **сохраненный выходные файлы** или **сохраненные журналы**.</span><span class="sxs-lookup"><span data-stu-id="9afff-197">tooview task output files and logs in hello Azure portal, navigate toohello task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="9afff-198">На данном рисунке показан hello **сохраненный выходные файлы** для задачи «hello» с Идентификатором «007»:</span><span class="sxs-lookup"><span data-stu-id="9afff-198">This image shows hello **Saved output files** for hello task with ID "007":</span></span>

<span data-ttu-id="9afff-199">![Выходные данные задач колонки в hello портал Azure][2]</span><span class="sxs-lookup"><span data-stu-id="9afff-199">![Task outputs blade in hello Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="9afff-200">Пример кода</span><span class="sxs-lookup"><span data-stu-id="9afff-200">Code sample</span></span>

<span data-ttu-id="9afff-201">Hello [PersistOutputs] [ github_persistoutputs] образец проекта является одним из hello [образцы кода пакетной службы Azure] [ github_samples] на GitHub.</span><span class="sxs-lookup"><span data-stu-id="9afff-201">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="9afff-202">Это решение Visual Studio показывает, как задачу toouse hello Azure пакетных файлов, принятых библиотеки toopersist вывода toodurable хранилища.</span><span class="sxs-lookup"><span data-stu-id="9afff-202">This Visual Studio solution demonstrates how toouse hello Azure Batch File Conventions library toopersist task output toodurable storage.</span></span> <span data-ttu-id="9afff-203">toorun hello образец, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9afff-203">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="9afff-204">Привет открыть проект в **Visual Studio 2015 или более новой версии**.</span><span class="sxs-lookup"><span data-stu-id="9afff-204">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="9afff-205">Добавить пакет и хранилища **учетные данные учетной записи** слишком**AccountSettings.settings** в проекте Microsoft.Azure.Batch.Samples.Common hello.</span><span class="sxs-lookup"><span data-stu-id="9afff-205">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="9afff-206">**Построение** (но не запускайте) hello решения.</span><span class="sxs-lookup"><span data-stu-id="9afff-206">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="9afff-207">Восстановите необходимые пакеты NuGet в случае появления соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="9afff-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="9afff-208">Используйте hello Azure портала tooupload [пакета приложения](batch-application-packages.md) для **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="9afff-208">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="9afff-209">Включить hello `PersistOutputsTask.exe` и ее зависимые сборки в пакете .zip hello, идентификатор приложения hello набор слишком версии пакета «PersistOutputsTask» и приложение hello слишком «1.0».</span><span class="sxs-lookup"><span data-stu-id="9afff-209">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="9afff-210">**Запуск** (выполнения) hello **PersistOutputs** проекта.</span><span class="sxs-lookup"><span data-stu-id="9afff-210">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="9afff-211">При вводе toouse технологии запрашиваемые toochoose hello сохраняемости для выполнения образца hello, **1** toorun hello выборке, используя выходные данные задачи toopersist hello соглашения файл библиотеки.</span><span class="sxs-lookup"><span data-stu-id="9afff-211">When prompted toochoose hello persistence technology toouse for running hello sample, enter **1** toorun hello sample using hello File Conventions library toopersist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9afff-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9afff-212">Next steps</span></span>

### <a name="get-hello-batch-file-conventions-library-for-net"></a><span data-ttu-id="9afff-213">Получить hello пакетных файлов, принятых библиотеки для .NET</span><span class="sxs-lookup"><span data-stu-id="9afff-213">Get hello Batch File Conventions library for .NET</span></span>

<span data-ttu-id="9afff-214">Библиотека Hello пакетных файлов, принятых для .NET можно найти в [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="9afff-214">hello Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="9afff-215">Библиотека Hello расширяет hello [CloudJob] [ net_cloudjob] и [CloudTask] [ net_cloudtask] классы за счет новых методов.</span><span class="sxs-lookup"><span data-stu-id="9afff-215">hello library extends hello [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="9afff-216">См. также hello [справочная документация](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) для файлов, принятых библиотеки hello.</span><span class="sxs-lookup"><span data-stu-id="9afff-216">Also see hello [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for hello File Conventions library.</span></span>

<span data-ttu-id="9afff-217">Hello [исходный код] [ github_file_conventions] для файлов, принятых hello библиотеки доступен на GitHub в hello Microsoft Azure SDK для .NET репозитория.</span><span class="sxs-lookup"><span data-stu-id="9afff-217">hello [source code][github_file_conventions] for hello File Conventions library is available on GitHub in hello Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="9afff-218">Другие методы сохранения выходных данных</span><span class="sxs-lookup"><span data-stu-id="9afff-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="9afff-219">В разделе [Persist заданий и задач вывода tooAzure хранения](batch-task-output.md) Обзор сохранения данных задач и задание.</span><span class="sxs-lookup"><span data-stu-id="9afff-219">See [Persist job and task output tooAzure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="9afff-220">В разделе [сохранения данных задач tooAzure хранилища с hello API пакетной службы](batch-task-output-files.md) toolearn как toopersist hello API пакетной службы toouse выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9afff-220">See [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md) toolearn how toouse hello Batch service API toopersist output data.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Селекторы сохраненных выходных файлов и журналов на портале"
[2]: ./media/batch-task-output/task-output-02.png "Выходные данные задач колонки в hello портал Azure"
