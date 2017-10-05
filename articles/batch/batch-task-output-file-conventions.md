---
title: "Сохранение выходных данных заданий и задач в службе хранилища Azure с помощью библиотеки соглашений об именовании файлов для .NET — пакетная служба Azure | Документы Майкрософт"
description: "Узнайте, как использовать библиотеку соглашений для пакетных файлов Azure для .NET для сохранения выходных данных задач и заданий пакетной службы в службе хранилища Azure и просматривать сохраненные выходные данные на портале Azure."
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
ms.openlocfilehash: a9de327c20463469bc91d9720aa17333a36f919e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="persist-job-and-task-data-to-azure-storage-with-the-batch-file-conventions-library-for-net-to-persist"></a><span data-ttu-id="8f59c-103">Сохранение данных заданий и задач в службе хранилища Azure с помощью библиотеки соглашений о пакетных файлах для .NET</span><span class="sxs-lookup"><span data-stu-id="8f59c-103">Persist job and task data to Azure Storage with the Batch File Conventions library for .NET to persist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="8f59c-104">Одним из способов сохранения данных задач является использование [библиотеки соглашений о пакетных файлах Azure для .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="8f59c-104">One way to persist task data is to use the [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="8f59c-105">Библиотека файлов соглашений об именовании файлов упрощает процесс сохранения выходных данных задачи в службе хранилища Azure и извлечения из данной службы.</span><span class="sxs-lookup"><span data-stu-id="8f59c-105">The File Conventions library simplifies the process of storing task output data to Azure Storage and retrieving it.</span></span> <span data-ttu-id="8f59c-106">Библиотеку соглашений об именовании файлов можно использовать в коде задачи и клиента &mdash; в коде задачи — для сохранения файлов, а в коде клиента — для получения списка файлов и их извлечения.</span><span class="sxs-lookup"><span data-stu-id="8f59c-106">You can use the File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code to list and retrieve them.</span></span> <span data-ttu-id="8f59c-107">Код задачи также может использовать библиотеку для получения выходных данных вышестоящих задач, например, как в сценарии [зависимостей задач](batch-task-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="8f59c-107">Your task code can also use the library to retrieve the output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="8f59c-108">Чтобы получить выходные файлы с помощью библиотеки соглашений об именовании файлов, можно найти файлы для данного задания или задачи, указав их по идентификатору и назначению.</span><span class="sxs-lookup"><span data-stu-id="8f59c-108">To retrieve output files with the File Conventions library, you can locate the files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="8f59c-109">Имена файлов или их расположение знать не нужно.</span><span class="sxs-lookup"><span data-stu-id="8f59c-109">You don't need to know the names or locations of the files.</span></span> <span data-ttu-id="8f59c-110">Например, можно использовать библиотеку соглашений об именовании файлов для вывода списка всех промежуточных файлов для данной задачи или получить файл предварительного просмотра для данного задания.</span><span class="sxs-lookup"><span data-stu-id="8f59c-110">For example, you can use the File Conventions library to list all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="8f59c-111">Начиная с версии 2017-05-01, API пакетной службы поддерживает сохранение выходных данных в службе хранилища Azure для обычных задач и задач диспетчера заданий, которые выполняются в пулах, созданных с конфигурацией виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8f59c-111">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools created with the virtual machine configuration.</span></span> <span data-ttu-id="8f59c-112">API пакетной службы предоставляет простой способ сохранения выходных данных в коде, который создает задачу и служит в качестве альтернативы библиотеке соглашений об именовании файлов.</span><span class="sxs-lookup"><span data-stu-id="8f59c-112">The Batch service API provides a simple way to persist output from within the code that creates a task and serves as an alternative to the File Conventions library.</span></span> <span data-ttu-id="8f59c-113">Клиентские приложения пакетной службы можно изменить для сохранения выходных данных без необходимости обновления приложения, в котором выполняется ваша задача.</span><span class="sxs-lookup"><span data-stu-id="8f59c-113">You can modify your Batch client applications to persist output without needing to update the application that your task is running.</span></span> <span data-ttu-id="8f59c-114">Дополнительные сведения можно найти в разделе [Сохранение данных задачи в службе хранилища Azure с помощью API пакетной службы](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="8f59c-114">For more information, see [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-the-file-conventions-library-to-persist-task-output"></a><span data-ttu-id="8f59c-115">Примеры использования библиотеки соглашений для именования файлов для сохранения выходных данных задачи</span><span class="sxs-lookup"><span data-stu-id="8f59c-115">When do I use the File Conventions library to persist task output?</span></span>

<span data-ttu-id="8f59c-116">Пакетная служба Azure поддерживает несколько способов сохранения выходных данных задачи.</span><span class="sxs-lookup"><span data-stu-id="8f59c-116">Azure Batch provides more than one way to persist task output.</span></span> <span data-ttu-id="8f59c-117">Соглашения об именовании файлов наилучшим образом подходит для этих сценариев:</span><span class="sxs-lookup"><span data-stu-id="8f59c-117">The File Conventions is best suited to these scenarios:</span></span>

- <span data-ttu-id="8f59c-118">Код для приложения, в котором выполняется ваша задача, можно легко изменить для сохранения файлов с помощью библиотеки соглашений об именовании файлов.</span><span class="sxs-lookup"><span data-stu-id="8f59c-118">You can easily modify the code for the application that your task is running to persist files using the File Conventions library.</span></span>
- <span data-ttu-id="8f59c-119">Требуется обеспечить потоковую передачу данных в службу хранилища Azure, пока выполняется задача.</span><span class="sxs-lookup"><span data-stu-id="8f59c-119">You want to stream data to Azure Storage while the task is still running.</span></span>
- <span data-ttu-id="8f59c-120">Требуется сохранить данные из пулов, созданных с конфигурацией облачной службы или конфигурации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8f59c-120">You want to persist data from pools created with either the cloud service configuration or the virtual machine configuration.</span></span>
- <span data-ttu-id="8f59c-121">Клиентское приложение или другие задачи в задании должны находить и скачивать выходные файлы задачи по идентификатору или назначению.</span><span class="sxs-lookup"><span data-stu-id="8f59c-121">Your client application or other tasks in the job needs to locate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="8f59c-122">Требуется просмотреть выходные данные задачи на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59c-122">You want to view task output in the Azure portal.</span></span>

<span data-ttu-id="8f59c-123">Если ваш случай отличается от перечисленных выше, возможно, придется использовать другой метод.</span><span class="sxs-lookup"><span data-stu-id="8f59c-123">If your scenario differs from those listed above, you may need to consider a different approach.</span></span> <span data-ttu-id="8f59c-124">Дополнительные сведения о других способах сохранения выходных данных задачи см. в разделе [Сохранение выходных данных заданий и задач в службе хранилища Azure](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="8f59c-124">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-the-batch-file-conventions-standard"></a><span data-ttu-id="8f59c-125">Что из себя представляет стандарт соглашений о пакетных файлах?</span><span class="sxs-lookup"><span data-stu-id="8f59c-125">What is the Batch File Conventions standard?</span></span>

<span data-ttu-id="8f59c-126">[Стандарт соглашений о пакетных файлах](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) предоставляет схему именования путей к целевым контейнерам и большим двоичным объектам, в которые записываются выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="8f59c-126">The [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for the destination containers and blob paths to which your output files are written.</span></span> <span data-ttu-id="8f59c-127">Файлы, сохраненные в службе хранилища Azure, которые соответствуют стандарту соглашений об именовании файлов, автоматически становятся доступны для просмотра на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59c-127">Files persisted to Azure Storage that adhere to the File Conventions standard are automatically available for viewing in the Azure portal.</span></span> <span data-ttu-id="8f59c-128">Портал учитывает соглашение об именовании и поэтому может отображать те файлы, которые ему соответствуют.</span><span class="sxs-lookup"><span data-stu-id="8f59c-128">The portal is aware of the naming convention and so can display files that adhere to it.</span></span>

<span data-ttu-id="8f59c-129">Библиотека соглашений об именовании файлов для .NET автоматически именует ваши контейнеры хранилища и выходных файлов задач в соответствии со стандартом соглашений об именовании файлов.</span><span class="sxs-lookup"><span data-stu-id="8f59c-129">The File Conventions library for .NET automatically names your storage containers and task output files according to the File Conventions standard.</span></span> <span data-ttu-id="8f59c-130">Библиотека соглашений об именовании файлов также поддерживает методы запроса выходных файлов в службе хранилища Azure в соответствии с идентификатором задания, идентификатором задачи или назначением.</span><span class="sxs-lookup"><span data-stu-id="8f59c-130">The File Conventions library also provides methods to query output files in Azure Storage according to job ID, task ID, or purpose.</span></span>   

<span data-ttu-id="8f59c-131">При работе на языке, отличном от .NET, можно самостоятельно реализовать в приложении стандарт соглашений об именовании файлов.</span><span class="sxs-lookup"><span data-stu-id="8f59c-131">If you are developing with a language other than .NET, you can implement the File Conventions standard yourself in your application.</span></span> <span data-ttu-id="8f59c-132">Дополнительные сведения см. в разделе [О стандарте соглашений о пакетных файлах](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="8f59c-132">For more information, see [About the Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-to-your-batch-account"></a><span data-ttu-id="8f59c-133">Связывание учетной записи хранения Azure со своей учетной записью пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8f59c-133">Link an Azure Storage account to your Batch account</span></span>

<span data-ttu-id="8f59c-134">Для сохранения выходных данных в службе хранилища Azure с помощью библиотеки соглашений об именовании файлов необходимо связать учетную запись хранения Azure с учетной записью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="8f59c-134">To persist output data to Azure Storage using the File Conventions library, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="8f59c-135">Если вы этого еще не сделали, свяжите учетную запись хранения с учетной записью пакетной службы с помощью [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f59c-135">If you haven't done so already, link a Storage account to your Batch account by using the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="8f59c-136">Войдите в свою учетную запись пакетной службы на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59c-136">Navigate to your Batch account in the Azure portal.</span></span> 
2. <span data-ttu-id="8f59c-137">В разделе **Параметры** выберите **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="8f59c-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="8f59c-138">Если у вас еще нет учетной записи хранения, связанной с вашей учетной записью пакетной службы, нажмите кнопку **Учетная запись хранения (нет)**.</span><span class="sxs-lookup"><span data-stu-id="8f59c-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="8f59c-139">Выберите учетную запись хранения в списке для своей подписки.</span><span class="sxs-lookup"><span data-stu-id="8f59c-139">Select a Storage account from the list for your subscription.</span></span> <span data-ttu-id="8f59c-140">Для обеспечения наилучшей производительности используйте учетную запись хранения Azure в одном регионе с учетной записью пакетной службы, где выполняются задачи.</span><span class="sxs-lookup"><span data-stu-id="8f59c-140">For best performance, use an Azure Storage account that is in the same region as the Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="8f59c-141">Сохранение выходных данных</span><span class="sxs-lookup"><span data-stu-id="8f59c-141">Persist output data</span></span>

<span data-ttu-id="8f59c-142">Для сохранения выходных данных заданий и задач с помощью библиотеки соглашений об именовании файлов создайте контейнер в службе хранилища Azure, а затем сохраните в нем выходные данные.</span><span class="sxs-lookup"><span data-stu-id="8f59c-142">To persist job and task output data with the File Conventions library, create a container in Azure Storage, then save the output to the container.</span></span> <span data-ttu-id="8f59c-143">Для отправки выходных данных задачи в контейнер используйте [клиентскую библиотеку службы хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage) в коде задачи.</span><span class="sxs-lookup"><span data-stu-id="8f59c-143">Use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code to upload the task output to the container.</span></span> 

<span data-ttu-id="8f59c-144">Дополнительные сведения о работе с контейнерами и большими двоичными объектами в службе хранилища Azure см. в разделе [Приступая к работе со службой хранилища больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="8f59c-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="8f59c-145">Все выходные данные заданий и задач, сохраненные с помощью библиотеки соглашений об именовании файлов, хранятся в одном и том же контейнере.</span><span class="sxs-lookup"><span data-stu-id="8f59c-145">All job and task outputs persisted with the File Conventions library are stored in the same container.</span></span> <span data-ttu-id="8f59c-146">Если большое число задач попытаются одновременно сохранить файлы, могут быть применены [пределы для регулирования хранилища](../storage/common/storage-performance-checklist.md#blobs).</span><span class="sxs-lookup"><span data-stu-id="8f59c-146">If a large number of tasks try to persist files at the same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="8f59c-147">Создание контейнера хранилища</span><span class="sxs-lookup"><span data-stu-id="8f59c-147">Create storage container</span></span>

<span data-ttu-id="8f59c-148">Для сохранения выходных данных задачи в службе хранилища Azure сначала создайте контейнер путем вызова [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="8f59c-148">To persist task output to Azure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="8f59c-149">Этот метод расширения принимает объект [CloudStorageAccount] [ net_cloudstorageaccount] в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="8f59c-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="8f59c-150">Он создает контейнер, именованный в соответствии со стандартом соглашений об именовании файлов, чтобы его содержимое можно было бы обнаружить с помощью портала Azure и методов извлечения данных, которые описаны ниже в этой статье.</span><span class="sxs-lookup"><span data-stu-id="8f59c-150">It creates a container named according to the File Conventions standard,so that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span></span>

<span data-ttu-id="8f59c-151">Обычно этот код применяется для создания контейнера в клиентском приложении &mdash;, то есть приложении, которое создает пулы, задания и задачи.</span><span class="sxs-lookup"><span data-stu-id="8f59c-151">You typically place the code to create a container in your client application &mdash; the application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference to the linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create the blob storage container for the outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="8f59c-152">Хранение выходных данных задач</span><span class="sxs-lookup"><span data-stu-id="8f59c-152">Store task outputs</span></span>

<span data-ttu-id="8f59c-153">После подготовки контейнера в службе хранилища Azure задачи могут сохранять выходные данные в контейнер с помощью класса [TaskOutputStorage][net_taskoutputstorage], находящегося в библиотеке соглашений об именовании файлов.</span><span class="sxs-lookup"><span data-stu-id="8f59c-153">Now that you've prepared a container in Azure Storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the File Conventions library.</span></span>

<span data-ttu-id="8f59c-154">В коде задачи сначала создайте объект [TaskOutputStorage][net_taskoutputstorage], и затем по завершении задачи вызовите метод [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync], чтобы сохранить выходные данные в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59c-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code to process data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="8f59c-155">Параметр `kind` метода [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) классифицирует сохраненные файлы.</span><span class="sxs-lookup"><span data-stu-id="8f59c-155">The `kind` parameter of the [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes the persisted files.</span></span> <span data-ttu-id="8f59c-156">Существует четыре стандартных типа [TaskOutputKind] [net_taskoutputkind]: `TaskOutput`, `TaskPreview`, `TaskLog` и `TaskIntermediate.`. Также можно определить пользовательские категории выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8f59c-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="8f59c-157">Эти типы позволяют указать тип выходных данных, отображаемых в списке, когда вы запрашиваете у пакетной службы сохраненные выходные данные какой-либо определенной задачи.</span><span class="sxs-lookup"><span data-stu-id="8f59c-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span></span> <span data-ttu-id="8f59c-158">Другими словами, при выводе списка выходных данных их можно отфильтровать по одному из типов выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8f59c-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span></span> <span data-ttu-id="8f59c-159">Например, "Выдайте мне версию *preview* выходных данных для задачи *109*".</span><span class="sxs-lookup"><span data-stu-id="8f59c-159">For example, "Give me the *preview* output for task *109*."</span></span> <span data-ttu-id="8f59c-160">Дополнительные сведения о выводе списка и извлечении выходных данных приведены далее, в разделе [Извлечение выходных данных](#retrieve-output) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="8f59c-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span></span>

> [!TIP]
> <span data-ttu-id="8f59c-161">Тип выходных данных также определяет, где на портале Azure будет отображен каждый конкретный файл: файлы из категории *TaskOutput* — в разделе **Task output files** (Выходные файлы задач), а файлы из категории *TaskLog* — в разделе **Task logs** (Журналы задач).</span><span class="sxs-lookup"><span data-stu-id="8f59c-161">The output kind also determines where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="8f59c-162">Хранения выходных данных заданий</span><span class="sxs-lookup"><span data-stu-id="8f59c-162">Store job outputs</span></span>

<span data-ttu-id="8f59c-163">Помимо хранения выходных данных задач, можно сохранять выходные данные, связанные со всем заданием.</span><span class="sxs-lookup"><span data-stu-id="8f59c-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span></span> <span data-ttu-id="8f59c-164">Например, для задачи слияния в задании отрисовки фильма можно сохранить полностью отрисованный фильм в качестве выходных данных задания.</span><span class="sxs-lookup"><span data-stu-id="8f59c-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span></span> <span data-ttu-id="8f59c-165">По завершении задания клиентское приложение может получить список и извлечь выходные данные этого задания, не отправляя запросы к отдельным задачам.</span><span class="sxs-lookup"><span data-stu-id="8f59c-165">When your job is completed, your client application can list and retrieve the outputs for the job, and does not need to query the individual tasks.</span></span>

<span data-ttu-id="8f59c-166">Для сохранения выходных данных задания используйте вызов метода [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] и укажите [JobOutputKind][net_joboutputkind] и имя файла.</span><span class="sxs-lookup"><span data-stu-id="8f59c-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="8f59c-167">В качестве значения **TaskOutputKind** для выходных данных задачи используйте тип [JobOutputKind][net_joboutputkind], чтобы классифицировать сохраняемые файлы задания.</span><span class="sxs-lookup"><span data-stu-id="8f59c-167">As with the **TaskOutputKind** type for task outputs, you use the [JobOutputKind][net_joboutputkind] type to categorize a job's persisted files.</span></span> <span data-ttu-id="8f59c-168">Позже это позволит запросить (получить список) определенный тип выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8f59c-168">This parameter allows you to later query for (list) a specific type of output.</span></span> <span data-ttu-id="8f59c-169">Тип **JobOutputKind** включает в себя категории output и preview, а также позволяет создавать пользовательские категории.</span><span class="sxs-lookup"><span data-stu-id="8f59c-169">The **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="8f59c-170">Хранение журналов задач</span><span class="sxs-lookup"><span data-stu-id="8f59c-170">Store task logs</span></span>

<span data-ttu-id="8f59c-171">Помимо сохранения файла в долговременном хранилище при завершении задачи или задания, может возникнуть потребность сохранять файлы, которые обновляются во время выполнения задачи &mdash;, например файлы журнала или `stdout.txt` и `stderr.txt`.</span><span class="sxs-lookup"><span data-stu-id="8f59c-171">In addition to persisting a file to durable storage when a task or job completes, you may need to persist files that are updated during the execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="8f59c-172">Для этой цели библиотека Azure Batch File Conventions предоставляет метод [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="8f59c-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="8f59c-173">С помощью метода [SaveTrackedAsync][net_savetrackedasync] можно отслеживать обновления файла на узле (с указанным интервалом) и сохранять эти обновления в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="8f59c-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span></span>

<span data-ttu-id="8f59c-174">В приведенном ниже фрагменте кода [SaveTrackedAsync][net_savetrackedasync] используется для обновления `stdout.txt` в службе хранилища Azure во время выполнения задачи через каждые 15 секунд.</span><span class="sxs-lookup"><span data-stu-id="8f59c-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// The primary task logic is wrapped in a using statement that sends updates to
// the stdout.txt blob in Storage every 15 seconds while the task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code to process data and produce output file(s) */

    // We are tracking the disk file to save our standard output, but the
    // node agent may take up to 3 seconds to flush the stdout stream to
    // disk. So give the file a moment to catch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="8f59c-175">Раздел с комментариями `Code to process data and produce output file(s)` — это просто заполнитель для обычного кода задачи.</span><span class="sxs-lookup"><span data-stu-id="8f59c-175">The commented section `Code to process data and produce output file(s)` is a placeholder for the code that your task would normally perform.</span></span> <span data-ttu-id="8f59c-176">Например, вам может понадобиться код, который скачивает данные из службы хранилища Azure и выполняет с ними операцию преобразования или вычисления.</span><span class="sxs-lookup"><span data-stu-id="8f59c-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="8f59c-177">В данном фрагменте кода важно обратить внимание на то, как такой код был помещен в блок `using` для периодического обновления файла с помощью метода [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="8f59c-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="8f59c-178">Агент узла — это программа, которая выполняется на каждом узле в пуле и предоставляет интерфейс контроля и управления между узлом и пакетной службой.</span><span class="sxs-lookup"><span data-stu-id="8f59c-178">The node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="8f59c-179">Чтобы агент узла имел время для записи содержимого стандартного потока вывода в файл stdout.txt на узле, в конце этого блока `using` требуется вызов `Task.Delay`.</span><span class="sxs-lookup"><span data-stu-id="8f59c-179">The `Task.Delay` call is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node.</span></span> <span data-ttu-id="8f59c-180">Без этой задержки вывод данных завершится на несколько секунд быстрее и, как результат, будет неполным.</span><span class="sxs-lookup"><span data-stu-id="8f59c-180">Without this delay, it is possible to miss the last few seconds of output.</span></span> <span data-ttu-id="8f59c-181">Задержка может не потребоваться для всех файлов.</span><span class="sxs-lookup"><span data-stu-id="8f59c-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="8f59c-182">При включении отслеживания файла с помощью метода **SaveTrackedAsync** в службе хранилища Azure будут сохраняться только данные, *добавляемые* в отслеживаемый файл.</span><span class="sxs-lookup"><span data-stu-id="8f59c-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* to the tracked file are persisted to Azure Storage.</span></span> <span data-ttu-id="8f59c-183">Этот метод следует использовать только для отслеживания не участвующих в ротации файлов журнала или других файлов, в конец которых с помощью операций добавления записываются данные.</span><span class="sxs-lookup"><span data-stu-id="8f59c-183">Use this method only for tracking non-rotating log files or other files that are written to with append operations to the end of the file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="8f59c-184">Извлечение выходных данных</span><span class="sxs-lookup"><span data-stu-id="8f59c-184">Retrieve output data</span></span>

<span data-ttu-id="8f59c-185">Извлечь сохраненные выходные данные с помощью библиотеки Azure Batch File Conventions можно в контексте задачи и задания.</span><span class="sxs-lookup"><span data-stu-id="8f59c-185">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="8f59c-186">Можно запросить выходные данные определенной задачи или задания без необходимости знать ни путь к ним в службе хранилища Azure, ни даже имя файла.</span><span class="sxs-lookup"><span data-stu-id="8f59c-186">You can request the output for given task or job without needing to know its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="8f59c-187">Вместо этого выходные файлы можно запрашивать по идентификатору задачи или задания.</span><span class="sxs-lookup"><span data-stu-id="8f59c-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="8f59c-188">Приведенный ниже фрагмент кода перебирает задачи в задании, выводит некоторые сведения о выходных файлах для задачи, а затем скачивает их из службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="8f59c-188">The following code snippet iterates through a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span></span>

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

## <a name="view-output-files-in-the-azure-portal"></a><span data-ttu-id="8f59c-189">Просмотр выходных файлов на портале Azure</span><span class="sxs-lookup"><span data-stu-id="8f59c-189">View output files in the Azure portal</span></span>

<span data-ttu-id="8f59c-190">Портал Azure будет отображать выходные данные и журналы задачи, сохраненные в связанной учетной записи службы хранилища Azure с использованием [стандарта соглашений об именовании пакетных файлов](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="8f59c-190">The Azure portal displays task output files and logs that are persisted to a linked Azure Storage account using the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="8f59c-191">Вы можете самостоятельно реализовать эти соглашения на выбранном языке или использовать библиотеку соглашений об именовании файлов в приложениях .NET.</span><span class="sxs-lookup"><span data-stu-id="8f59c-191">You can implement these conventions yourself in the a language of your choice, or you can use the File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="8f59c-192">Чтобы выходные файлы отображались на портале, необходимо выполнить следующие требования:</span><span class="sxs-lookup"><span data-stu-id="8f59c-192">To enable the display of your output files in the portal, you must satisfy the following requirements:</span></span>

1. <span data-ttu-id="8f59c-193">[Свяжите учетную запись хранения Azure](#requirement-linked-storage-account) со своей учетной записью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="8f59c-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span></span>
2. <span data-ttu-id="8f59c-194">При сохранении выходных данных нужно соблюдать предварительно определенные соглашения об именовании контейнеров хранилища и файлов.</span><span class="sxs-lookup"><span data-stu-id="8f59c-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="8f59c-195">Определение этих соглашений можно найти в [файле сведений][github_file_conventions_readme] о библиотеке соглашений об именовании файлов.</span><span class="sxs-lookup"><span data-stu-id="8f59c-195">You can find the definition of these conventions in the File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="8f59c-196">Если для сохранения выходных данных используется библиотека [соглашений об именовании пакетных файлов Azure][nuget_package], файлы сохраняются в соответствии со стандартом соглашений об именовании файлов.</span><span class="sxs-lookup"><span data-stu-id="8f59c-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, your files are persisted according to the File Conventions standard.</span></span>

<span data-ttu-id="8f59c-197">Чтобы просмотреть выходные файлы и журналы задачи на портале Azure, перейдите к задаче, выходные данные которой вас интересуют, затем щелкните **Сохраненные выходные файлы** или **Сохраненные журналы**.</span><span class="sxs-lookup"><span data-stu-id="8f59c-197">To view task output files and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="8f59c-198">На приведенном рисунке показан раздел **Saved output files** (Сохраненные выходные файлы) для задачи с идентификатором 007.</span><span class="sxs-lookup"><span data-stu-id="8f59c-198">This image shows the **Saved output files** for the task with ID "007":</span></span>

<span data-ttu-id="8f59c-199">![Колонка выходных данных задачи на портале Azure][2]</span><span class="sxs-lookup"><span data-stu-id="8f59c-199">![Task outputs blade in the Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="8f59c-200">Пример кода</span><span class="sxs-lookup"><span data-stu-id="8f59c-200">Code sample</span></span>

<span data-ttu-id="8f59c-201">Пример проекта [PersistOutputs][github_persistoutputs] — это один из [примеров кода пакетной службы Azure][github_samples] на портале GitHub.</span><span class="sxs-lookup"><span data-stu-id="8f59c-201">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="8f59c-202">Это решение Visual Studio демонстрирует использование библиотеки Azure Batch File Conventions для сохранения выходных данных задачи в долговременном хранилище.</span><span class="sxs-lookup"><span data-stu-id="8f59c-202">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span></span> <span data-ttu-id="8f59c-203">Чтобы запустить пример приложения, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="8f59c-203">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="8f59c-204">Откройте проект в **Visual Studio 2015 или более поздней версии**.</span><span class="sxs-lookup"><span data-stu-id="8f59c-204">Open the project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="8f59c-205">Добавьте свои **данные** учетной записи пакетной службы и учетной записи хранения в **AccountSettings.settings** в проекте Microsoft.Azure.Batch.Samples.Common.</span><span class="sxs-lookup"><span data-stu-id="8f59c-205">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="8f59c-206">**сборку** решения (но не запускайте его).</span><span class="sxs-lookup"><span data-stu-id="8f59c-206">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="8f59c-207">Восстановите необходимые пакеты NuGet в случае появления соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="8f59c-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="8f59c-208">С помощью портала Azure передайте [пакет приложения](batch-application-packages.md) для **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="8f59c-208">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="8f59c-209">Добавьте в ZIP-файл пакета `PersistOutputsTask.exe` и его зависимые сборки , задайте для приложения идентификатор PersistOutputsTask, а для версии пакета приложения — значение "1.0".</span><span class="sxs-lookup"><span data-stu-id="8f59c-209">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="8f59c-210">**Запустите** (выполните) проект **PersistOutputs**.</span><span class="sxs-lookup"><span data-stu-id="8f59c-210">**Start** (run) the **PersistOutputs** project.</span></span>
6. <span data-ttu-id="8f59c-211">Когда появится запрос на выбор технологии постоянного хранения для выполнения образца, введите **1** для запуска образца с помощью библиотеки соглашений об именовании файлов для сохранения выходных данных задачи.</span><span class="sxs-lookup"><span data-stu-id="8f59c-211">When prompted to choose the persistence technology to use for running the sample, enter **1** to run the sample using the File Conventions library to persist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8f59c-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8f59c-212">Next steps</span></span>

### <a name="get-the-batch-file-conventions-library-for-net"></a><span data-ttu-id="8f59c-213">Получение библиотеки соглашений об именовании пакетных файлов для .NET</span><span class="sxs-lookup"><span data-stu-id="8f59c-213">Get the Batch File Conventions library for .NET</span></span>

<span data-ttu-id="8f59c-214">Библиотека соглашений об именовании пакетных файлов для .NET доступна в [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="8f59c-214">The Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="8f59c-215">Библиотека расширяет классы [CloudJob][net_cloudjob] и [CloudTask][net_cloudtask] за счет новых методов.</span><span class="sxs-lookup"><span data-stu-id="8f59c-215">The library extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="8f59c-216">Сведения о библиотеке соглашений о наименовании файлов см. также в [справочной документации](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files).</span><span class="sxs-lookup"><span data-stu-id="8f59c-216">Also see the [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for the File Conventions library.</span></span>

<span data-ttu-id="8f59c-217">[Исходный код][github_file_conventions] библиотеки соглашений об именовании файлов Azure доступен на сайте GitHub в репозитории пакетов SDK Microsoft Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="8f59c-217">The [source code][github_file_conventions] for the File Conventions library is available on GitHub in the Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="8f59c-218">Другие методы сохранения выходных данных</span><span class="sxs-lookup"><span data-stu-id="8f59c-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="8f59c-219">Обзор методов сохранения данных задач и заданий см. в разделе [Сохранение выходных данных заданий и задач в службе хранилища Azure](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="8f59c-219">See [Persist job and task output to Azure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="8f59c-220">Сведения о том, как использовать API пакетной службы для сохранения выходных данных, см. в разделе [Сохранение данных задачи в службе хранилища Azure с помощью API пакетной службы](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="8f59c-220">See [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md) to learn how to use the Batch service API to persist output data.</span></span>

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
[2]: ./media/batch-task-output/task-output-02.png "Колонка выходных данных задачи на портале Azure"
