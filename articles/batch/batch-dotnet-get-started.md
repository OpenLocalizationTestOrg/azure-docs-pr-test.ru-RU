---
title: "aaaTutorial - используется клиентская библиотека hello пакетной службы Azure для .NET | Документы Microsoft"
description: "Изучите основные понятия hello пакетной службы Azure и создайте простое решение, с помощью .NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a><span data-ttu-id="f8e96-103">Приступить к созданию решения с hello пакета клиентской библиотеки для .NET</span><span class="sxs-lookup"><span data-stu-id="f8e96-103">Get started building solutions with hello Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8e96-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f8e96-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="f8e96-105">Python</span><span class="sxs-lookup"><span data-stu-id="f8e96-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="f8e96-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="f8e96-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="f8e96-107">Основы hello объекта [пакетной службы Azure] [ azure_batch] и hello [пакета .NET] [ net_api] библиотеки в этой статье в обсуждении C# образца приложения шаг по шаг.</span><span class="sxs-lookup"><span data-stu-id="f8e96-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="f8e96-108">Мы рассмотрим как пример приложения hello использует hello пакетной службы tooprocess параллельной рабочей нагрузки в облаке hello, а также их взаимодействие с [хранилища Azure](../storage/common/storage-introduction.md) для файла промежуточного хранения и извлечения.</span><span class="sxs-lookup"><span data-stu-id="f8e96-108">We look at how hello sample application leverages hello Batch service tooprocess a parallel workload in hello cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="f8e96-109">Будет узнать общий рабочий процесс приложения пакета и получить представление о базовых hello основных компонентов пакета, например заданий, задач, пулы и вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="f8e96-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="f8e96-110">![Рабочий процесс решения пакетной службы (основной)][11]</span><span class="sxs-lookup"><span data-stu-id="f8e96-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="f8e96-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f8e96-111">Prerequisites</span></span>
<span data-ttu-id="f8e96-112">В этой статье предполагается, что вы уже работали с C# и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f8e96-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="f8e96-113">Также предполагается, что вы будете требования к создания может toosatisfy hello учетной записи, указанные ниже для Azure и пакета hello и служб хранилища.</span><span class="sxs-lookup"><span data-stu-id="f8e96-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="f8e96-114">Учетные записи</span><span class="sxs-lookup"><span data-stu-id="f8e96-114">Accounts</span></span>
* <span data-ttu-id="f8e96-115">**Учетная запись Azure.** Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="f8e96-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="f8e96-116">**Учетная запись пакетной службы**. Если у вас есть подписка Azure, [создайте учетную запись пакетной службы Azure](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f8e96-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="f8e96-117">**Учетная запись хранения**. См. раздел [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account) в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f8e96-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8e96-118">Пакетов в настоящее время поддерживает *только* hello **общего назначения** тип учетной записи хранения, как описано в шаге #5 [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) в [о Azure учетные записи хранения](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f8e96-118">Batch currently supports *only* hello **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="f8e96-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f8e96-119">Visual Studio</span></span>
<span data-ttu-id="f8e96-120">Необходимо иметь **Visual Studio 2015 или более новой** toobuild hello образца проекта.</span><span class="sxs-lookup"><span data-stu-id="f8e96-120">You must have **Visual Studio 2015 or newer** toobuild hello sample project.</span></span> <span data-ttu-id="f8e96-121">Бесплатные и пробные версии Visual Studio можно найти в hello [Общие сведения о продуктах Visual Studio][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="f8e96-121">You can find free and trial versions of Visual Studio in hello [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="f8e96-122">*DotNetTutorial* </span><span class="sxs-lookup"><span data-stu-id="f8e96-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="f8e96-123">Hello [DotNetTutorial] [ github_dotnettutorial] образца является одним из hello найти множество образцов кода пакета в hello [образцы azure пакета] [ github_samples] репозитория на GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8e96-123">hello [DotNetTutorial][github_dotnettutorial] sample is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="f8e96-124">Можно загрузить все образцы hello, щелкнув **клон или загрузки > загрузить ZIP** на домашней странице hello репозитория или щелкнув hello [azure пакета образцы master.zip] [ github_samples_zip]прямой ссылкой скачивания.</span><span class="sxs-lookup"><span data-stu-id="f8e96-124">You can download all hello samples by clicking  **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="f8e96-125">Как только вы извлекли содержимое hello hello ZIP-файл, hello решения можно найти в hello следующие папки:</span><span class="sxs-lookup"><span data-stu-id="f8e96-125">Once you've extracted hello contents of hello ZIP file, you can find hello solution in hello following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="f8e96-126">Обозреватель пакетной службы Azure (необязательно)</span><span class="sxs-lookup"><span data-stu-id="f8e96-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="f8e96-127">Hello [обозреватель пакета Azure] [ github_batchexplorer] является бесплатное средство, которое включено в hello [образцы azure пакета] [ github_samples] репозитория в GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8e96-127">hello [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="f8e96-128">При toocomplete не требуется этого учебника, его можно использовать при разработке и отладке пакета решения.</span><span class="sxs-lookup"><span data-stu-id="f8e96-128">While not required toocomplete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="f8e96-129">Общие сведения о примере проекта DotNetTutorial</span><span class="sxs-lookup"><span data-stu-id="f8e96-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="f8e96-130">Hello *DotNetTutorial* образец кода представляет собой решение Visual Studio, которое состоит из двух проектов: **DotNetTutorial** и **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="f8e96-130">hello *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="f8e96-131">**DotNetTutorial** представляет hello клиентское приложение, которое взаимодействует с tooexecute hello пакета и хранилище служб параллельной рабочей нагрузки на вычислительных узлов (виртуальных машин).</span><span class="sxs-lookup"><span data-stu-id="f8e96-131">**DotNetTutorial** is hello client application that interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="f8e96-132">DotNetTutorial работает на локальной рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="f8e96-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="f8e96-133">**TaskApplication** — hello программы, которая выполняется на вычислительных узлах в Azure tooperform hello фактическую работу.</span><span class="sxs-lookup"><span data-stu-id="f8e96-133">**TaskApplication** is hello program that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="f8e96-134">В образце hello `TaskApplication.exe` анализирует hello текст в файл, загруженный из хранилища Azure (hello входного файла).</span><span class="sxs-lookup"><span data-stu-id="f8e96-134">In hello sample, `TaskApplication.exe` parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="f8e96-135">Затем он создает текстовый файл (hello выходной файл), содержащий список hello первых трех слов, которые содержатся во входном файле hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-135">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="f8e96-136">После создания выходного файла hello, TaskApplication передает tooAzure hello файла хранилища.</span><span class="sxs-lookup"><span data-stu-id="f8e96-136">After it creates hello output file, TaskApplication uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="f8e96-137">Это делает доступными toohello клиентского приложения для загрузки.</span><span class="sxs-lookup"><span data-stu-id="f8e96-137">This makes it available toohello client application for download.</span></span> <span data-ttu-id="f8e96-138">TaskApplication выполняется параллельно на нескольких вычислительных узлах hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="f8e96-138">TaskApplication runs in parallel on multiple compute nodes in hello Batch service.</span></span>

<span data-ttu-id="f8e96-139">Hello следующей схеме показана hello основных операций, выполняемых клиентским приложением hello *DotNetTutorial*и приложение hello, выполняемое задачи hello *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="f8e96-139">hello following diagram illustrates hello primary operations that are performed by hello client application, *DotNetTutorial*, and hello application that is executed by hello tasks, *TaskApplication*.</span></span> <span data-ttu-id="f8e96-140">Этот основной рабочий процесс является типичным для многих вычислительных решений, созданных с помощью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="f8e96-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="f8e96-141">Хотя здесь не показаны каждый компонент, доступный в hello пакетная служба, практически все пакета сценарий включает некоторые части этого рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="f8e96-141">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="f8e96-142">![Пример рабочего процесса пакетной службы][8]</span><span class="sxs-lookup"><span data-stu-id="f8e96-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="f8e96-143">**Шаг 1.**</span><span class="sxs-lookup"><span data-stu-id="f8e96-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="f8e96-144">Создайте **контейнеры** в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e96-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="f8e96-145">
[**Шаг 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="f8e96-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="f8e96-146">Отправка файлов приложения задач и toocontainers входные файлы.</span><span class="sxs-lookup"><span data-stu-id="f8e96-146">Upload task application files and input files toocontainers.</span></span><br/><span data-ttu-id="f8e96-147">
[**Шаг 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="f8e96-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="f8e96-148">Создайте **пул** пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="f8e96-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="f8e96-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="f8e96-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="f8e96-150">Здравствуйте, пул **StartTask** загрузки hello toonodes двоичные файлы (TaskApplication) задачи, которые они присоединиться к пулу hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-150">hello pool **StartTask** downloads hello task binary files (TaskApplication) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="f8e96-151">
[**Шаг 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="f8e96-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="f8e96-152">Создайте **задание** пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="f8e96-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="f8e96-153">
[**Шаг 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="f8e96-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="f8e96-154">Добавить **задачи** toohello задания.</span><span class="sxs-lookup"><span data-stu-id="f8e96-154">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="f8e96-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="f8e96-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="f8e96-156">Hello задачи, запланированные tooexecute на узлах.</span><span class="sxs-lookup"><span data-stu-id="f8e96-156">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="f8e96-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="f8e96-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="f8e96-158">Каждая задача скачивает свои входные данные из службы хранилища Azure, а затем начинает выполнение.</span><span class="sxs-lookup"><span data-stu-id="f8e96-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="f8e96-159">
[**Шаг 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="f8e96-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="f8e96-160">Мониторинг задач.</span><span class="sxs-lookup"><span data-stu-id="f8e96-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="f8e96-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="f8e96-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="f8e96-162">Как выполнить действия, они отправляют их вывода данных tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="f8e96-162">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="f8e96-163">
[**Шаг 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="f8e96-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="f8e96-164">Скачайте выходные данные задачи из службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="f8e96-164">Download task output from Storage.</span></span>

<span data-ttu-id="f8e96-165">Как уже упоминалось, решение не каждый пакет выполняет эти конкретные шаги и может включать другие, но hello *DotNetTutorial* образце приложения показано общих процессов найден в решении пакета.</span><span class="sxs-lookup"><span data-stu-id="f8e96-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but hello *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-hello-dotnettutorial-sample-project"></a><span data-ttu-id="f8e96-166">Построение hello *DotNetTutorial* образца проекта</span><span class="sxs-lookup"><span data-stu-id="f8e96-166">Build hello *DotNetTutorial* sample project</span></span>
<span data-ttu-id="f8e96-167">Перед запуском образца hello, необходимо указать пакет и хранения учетных данных учетной записи в hello *DotNetTutorial* проекта `Program.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="f8e96-167">Before you can successfully run hello sample, you must specify both Batch and Storage account credentials in hello *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="f8e96-168">Если вы еще не сделали этого, откройте hello решений в Visual Studio, дважды щелкнув hello `DotNetTutorial.sln` файл решения.</span><span class="sxs-lookup"><span data-stu-id="f8e96-168">If you have not done so already, open hello solution in Visual Studio by double-clicking hello `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="f8e96-169">Или откройте его из среды Visual Studio с помощью hello **файл > Открыть > проект или решение** меню.</span><span class="sxs-lookup"><span data-stu-id="f8e96-169">Or open it from within Visual Studio by using hello **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="f8e96-170">Откройте `Program.cs` внутри hello *DotNetTutorial* проекта.</span><span class="sxs-lookup"><span data-stu-id="f8e96-170">Open `Program.cs` within hello *DotNetTutorial* project.</span></span> <span data-ttu-id="f8e96-171">Затем добавьте учетные данные в качестве указанной верхней hello hello файла:</span><span class="sxs-lookup"><span data-stu-id="f8e96-171">Then add your credentials as specified near hello top of hello file:</span></span>

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="f8e96-172">Как упоминалось выше, в настоящее время необходимо указать учетные данные hello для **общего назначения** учетной записи хранения в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e96-172">As mentioned above, you must currently specify hello credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="f8e96-173">Пакет приложения используют хранилище больших двоичных объектов в пределах hello **общего назначения** учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="f8e96-173">Your Batch applications use blob storage within hello **general-purpose** storage account.</span></span> <span data-ttu-id="f8e96-174">Не указан hello учетные данные для учетной записи хранилища, который был создан, выбрав hello *хранилище больших двоичных объектов* тип учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f8e96-174">Do not specify hello credentials for a Storage account that was created by selecting hello *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="f8e96-175">Пакет и хранения учетные данные учетной записи в колонке hello учетной записи каждой службы можно найти в hello [портал Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="f8e96-175">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="f8e96-176">![Пакетное учетные данные на портале hello][9]
![учетные данные хранилища на портале hello][10]</span><span class="sxs-lookup"><span data-stu-id="f8e96-176">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="f8e96-177">Теперь, когда вы обновили hello проекта с помощью учетных данных, щелкните правой кнопкой мыши решение hello в обозревателе решений и выберите **построить решение**.</span><span class="sxs-lookup"><span data-stu-id="f8e96-177">Now that you've updated hello project with your credentials, right-click hello solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="f8e96-178">Подтверждение восстановления hello любых пакетов NuGet при появлении.</span><span class="sxs-lookup"><span data-stu-id="f8e96-178">Confirm hello restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="f8e96-179">Если пакеты NuGet hello не восстанавливаются автоматически или при обнаружении ошибок, о пакетах hello toorestore сбоя, обеспечьте hello [диспетчера пакетов NuGet] [ nuget_packagemgr] установлен.</span><span class="sxs-lookup"><span data-stu-id="f8e96-179">If hello NuGet packages are not automatically restored, or if you see errors about a failure toorestore hello packages, ensure that you have hello [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="f8e96-180">Затем включите hello загрузки отсутствующих пакетов.</span><span class="sxs-lookup"><span data-stu-id="f8e96-180">Then enable hello download of missing packages.</span></span> <span data-ttu-id="f8e96-181">В разделе [Включение пакета восстановления во время построения] [ nuget_restore] tooenable загрузки пакета.</span><span class="sxs-lookup"><span data-stu-id="f8e96-181">See [Enabling Package Restore During Build][nuget_restore] tooenable package download.</span></span>
>
>

<span data-ttu-id="f8e96-182">В следующих разделах hello мы подразделяется на несколько hello пример приложения hello шагов, что оно работает tooprocess рабочую нагрузку в hello пакетная служба и обсудить эти шаги подробно.</span><span class="sxs-lookup"><span data-stu-id="f8e96-182">In hello following sections, we break down hello sample application into hello steps that it performs tooprocess a workload in hello Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="f8e96-183">Мы рекомендуем вам toorefer toohello откройте решение в Visual Studio во время работы по hello оставшейся части этой статьи, так как не все строки кода в образце hello рассматривается.</span><span class="sxs-lookup"><span data-stu-id="f8e96-183">We encourage you toorefer toohello open solution in Visual Studio while you work your way through hello rest of this article, since not every line of code in hello sample is discussed.</span></span>

<span data-ttu-id="f8e96-184">Перейдите toohello вверху hello `MainAsync` метод в hello *DotNetTutorial* проекта `Program.cs` файл toostart с шага 1.</span><span class="sxs-lookup"><span data-stu-id="f8e96-184">Navigate toohello top of hello `MainAsync` method in hello *DotNetTutorial* project's `Program.cs` file toostart with Step 1.</span></span> <span data-ttu-id="f8e96-185">Каждый шаг ниже примерно следующим hello продвижения метода вызывает `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="f8e96-185">Each step below then roughly follows hello progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="f8e96-186">Шаг 1. Создание контейнеров службы хранилища</span><span class="sxs-lookup"><span data-stu-id="f8e96-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="f8e96-187">![Создание контейнеров в службе хранилища Azure][1]
</span><span class="sxs-lookup"><span data-stu-id="f8e96-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="f8e96-188">Пакетная служба включает встроенную поддержку для взаимодействия со службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e96-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="f8e96-189">Контейнеры в учетной записи хранилища обеспечивают hello файлов, необходимых hello задач, которые выполняются в вашей учетной записи пакета.</span><span class="sxs-lookup"><span data-stu-id="f8e96-189">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="f8e96-190">контейнеры Hello также обеспечивают месте toostore hello выходные данные задачи hello выдавать.</span><span class="sxs-lookup"><span data-stu-id="f8e96-190">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="f8e96-191">Здравствуйте, первое, что hello *DotNetTutorial* клиентского приложения является создание трех контейнеров в [хранилища больших двоичных объектов](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="f8e96-191">hello first thing hello *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="f8e96-192">**приложение**: этот контейнер будет хранить выполнения задачи hello, а также любой из его зависимостей, таких как библиотеки DLL приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-192">**application**: This container will store hello application run by hello tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="f8e96-193">**входной**: задачи будут загружены файлы tooprocess hello данных с hello *ввода* контейнера.</span><span class="sxs-lookup"><span data-stu-id="f8e96-193">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="f8e96-194">**выходные данные**: после завершения выполнения задач обработки входных файлов они загрузит hello результаты toohello *вывода* контейнера.</span><span class="sxs-lookup"><span data-stu-id="f8e96-194">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="f8e96-195">В порядке toointeract с хранилищем учетной записи и создавать контейнеры, мы используем hello [клиентская библиотека хранилища Azure для .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="f8e96-195">In order toointeract with a Storage account and create containers, we use hello [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="f8e96-196">Мы создадим ссылку toohello учетную запись с [CloudStorageAccount][net_cloudstorageaccount]и, создайте [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="f8e96-196">We create a reference toohello account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="f8e96-197">Мы используем hello `blobClient` ссылаться на протяжении приложения hello и передайте его в качестве параметра tooseveral методы.</span><span class="sxs-lookup"><span data-stu-id="f8e96-197">We use hello `blobClient` reference throughout hello application and pass it as a parameter tooseveral methods.</span></span> <span data-ttu-id="f8e96-198">Примером этого является в блоке кода hello, стоящего выше hello, где мы называем `CreateContainerIfNotExistAsync` tooactually создавать контейнеры hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-198">An example of this is in hello code block that immediately follows hello above, where we call `CreateContainerIfNotExistAsync` tooactually create hello containers.</span></span>

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

<span data-ttu-id="f8e96-199">После создания контейнеров hello приложения hello, теперь можно отправить hello файлы, которые будут использоваться задачами hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="f8e96-200">[Как toouse хранилища BLOB-объектов из .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) хороший Обзор работы с контейнеров хранилища Azure и больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="f8e96-200">[How toouse Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="f8e96-201">В начале работы с использованием пакета должно быть hello верхней части списка для чтения.</span><span class="sxs-lookup"><span data-stu-id="f8e96-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="f8e96-202">Шаг 2. Отправка приложения задач и файлов данных</span><span class="sxs-lookup"><span data-stu-id="f8e96-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="f8e96-203">![Задача передачи приложения и ввода (данных) файлы toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="f8e96-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="f8e96-204">В файле hello операции, передачи *DotNetTutorial* сначала определяет коллекции **приложения** и **ввода** пути к файлам, в котором они хранятся на локальном компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-204">In hello file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="f8e96-205">Затем он передает эти контейнеры toohello файлы, созданные на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="f8e96-206">Существует два метода в `Program.cs` , участвующие в процессе загрузки hello:</span><span class="sxs-lookup"><span data-stu-id="f8e96-206">There are two methods in `Program.cs` that are involved in hello upload process:</span></span>

* <span data-ttu-id="f8e96-207">`UploadFilesToContainerAsync`: Этот метод возвращает коллекцию [ResourceFile] [ net_resourcefile] объектов (как описано ниже) и внутренним образом вызывает метод `UploadFileToContainerAsync` tooupload каждый файл, который является переданный hello *filePaths* параметра.</span><span class="sxs-lookup"><span data-stu-id="f8e96-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` tooupload each file that is passed in hello *filePaths* parameter.</span></span>
* <span data-ttu-id="f8e96-208">`UploadFileToContainerAsync`: Этот метод называется методом hello, который фактически выполняет загрузку файла hello и создает hello [ResourceFile] [ net_resourcefile] объектов.</span><span class="sxs-lookup"><span data-stu-id="f8e96-208">`UploadFileToContainerAsync`: This is hello method that actually performs hello file upload and creates hello [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="f8e96-209">После отправки файла hello, он получает подпись общего доступа (SAS) для файла hello и возвращает объект ResourceFile, который ее представляет.</span><span class="sxs-lookup"><span data-stu-id="f8e96-209">After uploading hello file, it obtains a shared access signature (SAS) for hello file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="f8e96-210">Подписанные URL-адреса также рассматриваются ниже.</span><span class="sxs-lookup"><span data-stu-id="f8e96-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="f8e96-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="f8e96-211">ResourceFiles</span></span>
<span data-ttu-id="f8e96-212">Объект [ResourceFile] [ net_resourcefile] предоставляет задачи в пакете с файлом tooa hello URL-адрес в службе хранилища Azure, загруженные tooa вычислительный узел перед запуском этой задачи.</span><span class="sxs-lookup"><span data-stu-id="f8e96-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="f8e96-213">Hello [ResourceFile.BlobSource] [ net_resourcefile_blobsource] свойство указывает hello полный URL-адрес файла hello, которое существовало в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e96-213">hello [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="f8e96-214">Hello URL-адрес может также включать подписанного URL-адреса (SAS), предоставляющий безопасный доступ toohello файла.</span><span class="sxs-lookup"><span data-stu-id="f8e96-214">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="f8e96-215">Большинство типов задач в пакетной службе .NET, в том числе перечисленные ниже, содержат свойство *ResourceFiles* .</span><span class="sxs-lookup"><span data-stu-id="f8e96-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="f8e96-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="f8e96-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="f8e96-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="f8e96-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="f8e96-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="f8e96-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="f8e96-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="f8e96-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="f8e96-220">DotNetTutorial пример приложения Hello не использует hello JobPreparationTask или JobReleaseTask типы задач, но вы можете прочитать больше о них в [выполнения задания Подготовка и выполнение задач в пакете Azure вычислительные узлы](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="f8e96-220">hello DotNetTutorial sample application does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="f8e96-221">Подписанный URL-адрес (SAS)</span><span class="sxs-lookup"><span data-stu-id="f8e96-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="f8e96-222">Общего доступа, подписи, строки которого — Если включается как часть URL-адреса — предоставить безопасный доступ toocontainers и больших двоичных объектов в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e96-222">Shared access signatures are strings which—when included as part of a URL—provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="f8e96-223">Hello DotNetTutorial приложение использует оба большого двоичного объекта и контейнера общие URL-адреса подписи доступа и показано, как эти общие tooobtain доступ к строки подписи из hello службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="f8e96-223">hello DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="f8e96-224">**BLOB-объектов подписи коллективного доступа**: hello пула StartTask в DotNetTutorial использует URL-адреса большого двоичного объекта совместно при загрузке hello двоичные файлы приложения и файлы входных данных из хранилища (см. шаг #3 ниже).</span><span class="sxs-lookup"><span data-stu-id="f8e96-224">**Blob shared access signatures**: hello pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads hello application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="f8e96-225">Hello `UploadFileToContainerAsync` метода в его DotNetTutorial `Program.cs` содержит hello код, который получает подпись общего доступа для каждого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="f8e96-225">hello `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="f8e96-226">Для этого выполняется вызов [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="f8e96-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="f8e96-227">**Контейнер подписи коллективного доступа**: как каждая задача завершит свою работу на вычислительном узле hello, передает его выходной файл toohello *вывода* контейнера в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e96-227">**Container shared access signatures**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="f8e96-228">toodo этого TaskApplication использует контейнер подписанный URL-адрес, предоставляющий доступ на запись toohello контейнера как часть пути hello, когда он передает файл hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-228">toodo so, TaskApplication uses a container shared access signature that provides write access toohello container as part of hello path when it uploads hello file.</span></span> <span data-ttu-id="f8e96-229">Получение подписи общего доступа контейнера hello выполняется таким же образом, как при больших двоичных объектов для получения hello подписанном URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="f8e96-229">Obtaining hello container shared access signature is done in a similar fashion as when obtaining hello blob shared access signature.</span></span> <span data-ttu-id="f8e96-230">В DotNetTutorial, вы найдете, hello `GetContainerSasUrl` вызывает вспомогательный метод [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo так.</span><span class="sxs-lookup"><span data-stu-id="f8e96-230">In DotNetTutorial, you will find that hello `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] toodo so.</span></span> <span data-ttu-id="f8e96-231">Вам нужно прочитать больше об использовании контейнера hello TaskApplication подписанный URL-в «шаг 6: задачи монитора.»</span><span class="sxs-lookup"><span data-stu-id="f8e96-231">You'll read more about how TaskApplication uses hello container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="f8e96-232">Извлечение серии из двух частей hello подписей общего доступа [часть 1: hello понимание общая модель адреса (SAS) доступ](../storage/common/storage-dotnet-shared-access-signature-part-1.md) и [часть 2: Создание и использование подписи общего доступа (SAS) с помощью хранилища больших двоичных объектов](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn дополнительные о предоставлении toodata безопасного доступа к вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="f8e96-232">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="f8e96-233">Шаг 3. Создание пула пакетной службы</span><span class="sxs-lookup"><span data-stu-id="f8e96-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="f8e96-234">![Создание пула пакетной службы][3]
</span><span class="sxs-lookup"><span data-stu-id="f8e96-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="f8e96-235">**Пул** пакетной службы — это коллекция вычислительных узлов (виртуальных машин), на которых пакетная служба выполняет задачи задания.</span><span class="sxs-lookup"><span data-stu-id="f8e96-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="f8e96-236">После загрузки приложения hello и toohello файлы данных учетной записи хранилища с помощью API-интерфейсов хранилища Azure, *DotNetTutorial* начинает делать вызовы toohello пакетная служба с интерфейсами API, предоставляемые библиотекой .NET пакета hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-236">After uploading hello application and data files toohello Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls toohello Batch service with APIs provided by hello Batch .NET library.</span></span> <span data-ttu-id="f8e96-237">Hello код сначала создает [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="f8e96-237">hello code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="f8e96-238">Далее образец hello создает пул вычислительных узлов в hello пакетной учетной записи с помощью вызова слишком`CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="f8e96-238">Next, hello sample creates a pool of compute nodes in hello Batch account with a call too`CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="f8e96-239">`CreatePoolIfNotExistsAsync`использует hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create] toocreate метод пула в hello пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="f8e96-239">`CreatePoolIfNotExistsAsync` uses hello [BatchClient.PoolOperations.CreatePool][net_pool_create] method toocreate a new pool in hello Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="f8e96-240">При создании пула с [CreatePool][net_pool_create], можно указать несколько параметров, например hello количество вычислительных узлов hello [размер узлов hello](../cloud-services/cloud-services-sizes-specs.md), и hello операционной узлы система.</span><span class="sxs-lookup"><span data-stu-id="f8e96-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as hello number of compute nodes, hello [size of hello nodes](../cloud-services/cloud-services-sizes-specs.md), and hello nodes' operating system.</span></span> <span data-ttu-id="f8e96-241">В *DotNetTutorial*, мы используем [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 из [облачные службы](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="f8e96-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="f8e96-242">Также можно создать пулы вычислительных узлов, которые представляют собой виртуальные машины Azure (ВМ), указав hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] для пула.</span><span class="sxs-lookup"><span data-stu-id="f8e96-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying hello [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="f8e96-243">Пул вычислительных узлов виртуальных машин можно создать из образов Windows или [Linux](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="f8e96-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="f8e96-244">Источник Hello для образов виртуальной Машины может быть либо:</span><span class="sxs-lookup"><span data-stu-id="f8e96-244">hello source for your VM images can be either:</span></span>

- <span data-ttu-id="f8e96-245">Hello [виртуальных машин Azure Marketplace][vm_marketplace], который предоставляет образы Windows и Linux, готовые к использованию.</span><span class="sxs-lookup"><span data-stu-id="f8e96-245">hello [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="f8e96-246">Настраиваемый образ, подготавливаемый и предоставляемый пользователем.</span><span class="sxs-lookup"><span data-stu-id="f8e96-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="f8e96-247">Дополнительные сведения о пользовательских образах см. в руководстве по [разработке решений для крупномасштабных параллельных вычислений с помощью пакетной службы](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="f8e96-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8e96-248">В пакетной службе за использование вычислительных ресурсов взимается плата.</span><span class="sxs-lookup"><span data-stu-id="f8e96-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="f8e96-249">toominimize затраты, можно понизить `targetDedicatedComputeNodes` too1 перед запуском образца hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-249">toominimize costs, you can lower `targetDedicatedComputeNodes` too1 before you run hello sample.</span></span>
>
>

<span data-ttu-id="f8e96-250">Вместе с этим свойствам физического узла, можно также указать [StartTask] [ net_pool_starttask] hello в пуле.</span><span class="sxs-lookup"><span data-stu-id="f8e96-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for hello pool.</span></span> <span data-ttu-id="f8e96-251">Hello StartTask выполняет на каждом узле, как этот узел соединяет hello пул, и каждый раз при перезапуске узла.</span><span class="sxs-lookup"><span data-stu-id="f8e96-251">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="f8e96-252">Hello StartTask особенно полезен для установки приложений на вычислительных узлах предыдущих toohello выполнения задач.</span><span class="sxs-lookup"><span data-stu-id="f8e96-252">hello StartTask is especially useful for installing applications on compute nodes prior toohello execution of tasks.</span></span> <span data-ttu-id="f8e96-253">Например если задач обработки данных с помощью сценариев Python, можно использовать на вычислительных узлах hello StartTask tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="f8e96-253">For example, if your tasks process data by using Python scripts, you could use a StartTask tooinstall Python on hello compute nodes.</span></span>

<span data-ttu-id="f8e96-254">В этом образце приложения hello StartTask копирует hello файлы, загружаемые из хранилища (которые указываются с помощью hello [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] свойство) из общего каталога hello StartTask рабочий каталог toohello, *все* доступны задачи, выполняемые на узле hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-254">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from hello StartTask working directory toohello shared directory that *all* tasks running on hello node can access.</span></span> <span data-ttu-id="f8e96-255">По сути, это копирует `TaskApplication.exe` и его toohello зависимости общих каталогов на каждом узле при присоединении узла hello пула hello доступа к ней все задачи, выполняемых в узле hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-255">Essentially, this copies `TaskApplication.exe` and its dependencies toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="f8e96-256">Hello **пакетов приложений** компонент пакетной службы Azure предоставляет другим способом tooget приложения в hello вычислительных узлов в пуле.</span><span class="sxs-lookup"><span data-stu-id="f8e96-256">hello **application packages** feature of Azure Batch provides another way tooget your application onto hello compute nodes in a pool.</span></span> <span data-ttu-id="f8e96-257">В разделе [развертывания приложений toocompute узлов с пакетами приложения пакета](batch-application-packages.md) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="f8e96-257">See [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="f8e96-258">Также значительным в приведенном выше фрагменте кода hello используется hello двух переменных среды в hello *CommandLine* свойство hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` и `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="f8e96-258">Also notable in hello code snippet above is hello use of two environment variables in hello *CommandLine* property of hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="f8e96-259">Несколько переменных среды, которые являются определенной tooBatch автоматически настраивается каждом вычислительном узле в пуле пакета.</span><span class="sxs-lookup"><span data-stu-id="f8e96-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="f8e96-260">Любой процесс, выполняемый задачей имеет доступ к переменным среды toothese.</span><span class="sxs-lookup"><span data-stu-id="f8e96-260">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="f8e96-261">toofind Дополнительные сведения о переменных среды hello, доступные на вычислительных узлах пула и сведения о задаче рабочие каталоги, в разделе hello [параметры среды для задачи](batch-api-basics.md#environment-settings-for-tasks) и [файлов и каталогов ](batch-api-basics.md#files-and-directories) подразделы hello [пакета Обзор возможностей для разработчиков](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="f8e96-261">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see hello [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in hello [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="f8e96-262">Шаг 4. Создание задания пакетной службы</span><span class="sxs-lookup"><span data-stu-id="f8e96-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="f8e96-263">![Создание задания пакетной службы][4]</span><span class="sxs-lookup"><span data-stu-id="f8e96-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="f8e96-264">**Задание** пакетной службы — это коллекция задач, связанных с пулом вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="f8e96-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="f8e96-265">Hello задачи в задании, выполняются в hello связанный пул вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="f8e96-265">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="f8e96-266">Задания можно использовать не только для упорядочивания и отслеживания задач в связанных рабочих нагрузок, но также и для налагающий определенные ограничения, например hello максимального времени для задания hello (и по расширению, его задачи), а также приоритет задания в заданиях tooother отношений в пакете hello Учетная запись.</span><span class="sxs-lookup"><span data-stu-id="f8e96-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) as well as job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="f8e96-267">В этом примере задание hello связаны только с пулом hello, который был создан на шаге #3.</span><span class="sxs-lookup"><span data-stu-id="f8e96-267">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="f8e96-268">Дополнительные свойства не настроены.</span><span class="sxs-lookup"><span data-stu-id="f8e96-268">No additional properties are configured.</span></span>

<span data-ttu-id="f8e96-269">Все задания пакетной службы связаны с конкретным пулом.</span><span class="sxs-lookup"><span data-stu-id="f8e96-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="f8e96-270">Эта связь указывает, какие узлы будут выполняться задачи hello задания.</span><span class="sxs-lookup"><span data-stu-id="f8e96-270">This association indicates which nodes hello job's tasks will execute on.</span></span> <span data-ttu-id="f8e96-271">Можно указать это, используя hello [CloudJob.PoolInformation] [ net_job_poolinfo] свойства, как показано в приведенном ниже фрагменте кода hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-271">You specify this by using hello [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in hello code snippet below.</span></span>

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

<span data-ttu-id="f8e96-272">После создания задания задачи добавляются рабочие tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-272">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="f8e96-273">Шаг 5: Добавление toojob задачи</span><span class="sxs-lookup"><span data-stu-id="f8e96-273">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="f8e96-274">![Добавление задачи toojob][5]</span><span class="sxs-lookup"><span data-stu-id="f8e96-274">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="f8e96-275">
*(1) задачи добавляются toohello задания, (2) hello задачи, запланированные toorun на узлах и (3) hello задачи загрузки tooprocess файлы данных hello*</span><span class="sxs-lookup"><span data-stu-id="f8e96-275">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="f8e96-276">Пакет **задачи** являются hello отдельных рабочих элементов, выполните на hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="f8e96-276">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="f8e96-277">Задача имеет командную строку и выполняется hello сценарии или исполняемые файлы, укажите в этой командной строке.</span><span class="sxs-lookup"><span data-stu-id="f8e96-277">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="f8e96-278">tooactually выполнения работы, задачи должны быть добавлены tooa задания.</span><span class="sxs-lookup"><span data-stu-id="f8e96-278">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="f8e96-279">Каждый [CloudTask] [ net_task] настраивается с помощью свойства командной строки и [ResourceFiles] [ net_task_resourcefiles] (как в случае с StartTask hello пула), Задача Hello загружает toohello узла перед его командной строки выполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="f8e96-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="f8e96-280">В hello *DotNetTutorial* образец проекта, каждая задача обрабатывает только один файл.</span><span class="sxs-lookup"><span data-stu-id="f8e96-280">In hello *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="f8e96-281">Поэтому его коллекция ResourceFiles содержит один элемент.</span><span class="sxs-lookup"><span data-stu-id="f8e96-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="f8e96-282">При доступе переменные среды, такие как `%AZ_BATCH_NODE_SHARED_DIR%` или выполнить приложение не найдено в узле hello `PATH`, командные строки задача должна начинаться с префикса `cmd /c`.</span><span class="sxs-lookup"><span data-stu-id="f8e96-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in hello node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="f8e96-283">Будет явно выполнение интерпретатор команд hello и задать для него tooterminate после выполнения команду.</span><span class="sxs-lookup"><span data-stu-id="f8e96-283">This will explicitly execute hello command interpreter and instruct it tooterminate after carrying out your command.</span></span> <span data-ttu-id="f8e96-284">Это требование не требуется, если задачи Выполнение приложения в узле hello `PATH` (такие как *robocopy.exe* или *powershell.exe*) и используются переменные среды.</span><span class="sxs-lookup"><span data-stu-id="f8e96-284">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="f8e96-285">В рамках hello `foreach` цикла в приведенном выше фрагменте кода hello, можно увидеть, что hello командной строки для задачи «hello» создается таким образом, что слишком передаются три аргумента командной строки*TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="f8e96-285">Within hello `foreach` loop in hello code snippet above, you can see that hello command line for hello task is constructed such that three command-line arguments are passed too*TaskApplication.exe*:</span></span>

1. <span data-ttu-id="f8e96-286">Hello **первый аргумент** hello путь файла tooprocess hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-286">hello **first argument** is hello path of hello file tooprocess.</span></span> <span data-ttu-id="f8e96-287">Это файл toohello hello локальный путь, как она находится на узле hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-287">This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="f8e96-288">Когда hello объекта ResourceFile в `UploadFileToContainerAsync` была создана более поздней версии, имя файла hello использовался для этого свойства (как параметр конструктора ResourceFile toohello).</span><span class="sxs-lookup"><span data-stu-id="f8e96-288">When hello ResourceFile object in `UploadFileToContainerAsync` was first created above, hello file name was used for this property (as a parameter toohello ResourceFile constructor).</span></span> <span data-ttu-id="f8e96-289">Это означает, что этот файл hello можно найти в hello же каталоге, что и *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="f8e96-289">This indicates that hello file can be found in hello same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="f8e96-290">Hello **второй аргумент** указывает, что верхней hello *N* слова должны быть написаны toohello выходного файла.</span><span class="sxs-lookup"><span data-stu-id="f8e96-290">hello **second argument** specifies that hello top *N* words should be written toohello output file.</span></span> <span data-ttu-id="f8e96-291">В образце hello это будет жестко, чтобы верхний три слова hello записываются toohello выходного файла.</span><span class="sxs-lookup"><span data-stu-id="f8e96-291">In hello sample, this is hard-coded so that hello top three words are written toohello output file.</span></span>
3. <span data-ttu-id="f8e96-292">Hello **третий аргумент** — hello подписанного URL-адреса (SAS), предоставляющий доступ на запись toohello **вывода** контейнера в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e96-292">hello **third argument** is hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="f8e96-293">*TaskApplication.exe* использует этот общий доступ к URL-адрес подписи при его передаче hello выходной файл tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="f8e96-293">*TaskApplication.exe* uses this shared access signature URL when it uploads hello output file tooAzure Storage.</span></span> <span data-ttu-id="f8e96-294">Для этого можно найти кода hello в hello `UploadFileToContainer` метода в проекте TaskApplication hello `Program.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="f8e96-294">You can find hello code for this in hello `UploadFileToContainer` method in hello TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="f8e96-295">Шаг 6. Мониторинг задач</span><span class="sxs-lookup"><span data-stu-id="f8e96-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="f8e96-296">![Мониторинг задач][6]</span><span class="sxs-lookup"><span data-stu-id="f8e96-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="f8e96-297">
*Hello клиентского приложения (1) мониторы hello задачи для завершения и состояние успеха и (2) hello данных результата tooAzure хранилища для задачи передачи*</span><span class="sxs-lookup"><span data-stu-id="f8e96-297">
*hello client application (1) monitors hello tasks for completion and success status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="f8e96-298">При добавлении задачи задания tooa они автоматически в очередь и запланировать выполнение на вычислительных узлах пула hello, связанный с заданием hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-298">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="f8e96-299">В зависимости от настройки hello пакета обрабатывает все очереди задач, планирования, повтор и другие задачи администрирования обязанностей.</span><span class="sxs-lookup"><span data-stu-id="f8e96-299">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="f8e96-300">Существует множество подходов toomonitoring выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="f8e96-300">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="f8e96-301">Приложение DotNetTutorial — это простой пример, который сообщает только о трех состояниях: завершение, сбой задачи и успешное завершение.</span><span class="sxs-lookup"><span data-stu-id="f8e96-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="f8e96-302">В рамках hello `MonitorTasks` метода в его DotNetTutorial `Program.cs`, есть три пакета .NET понятия, которые служат основанием для обсуждения.</span><span class="sxs-lookup"><span data-stu-id="f8e96-302">Within hello `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="f8e96-303">Они перечислены ниже в порядке появления.</span><span class="sxs-lookup"><span data-stu-id="f8e96-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="f8e96-304">**ODATADetailLevel.** Чтобы обеспечить выполнение приложения пакетной службы, необходимо указать класс [ODATADetailLevel][net_odatadetaillevel] в операциях получения списков (таких как получение списка задач задания).</span><span class="sxs-lookup"><span data-stu-id="f8e96-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="f8e96-305">Добавить [эффективно запрашивать hello пакетной службы Azure](batch-efficient-list-queries.md) tooyour при чтении списка, если вы планируете выполнять каких-либо мониторинга состояния пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="f8e96-305">Add [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md) tooyour reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="f8e96-306">**TaskStateMonitor.** Класс [TaskStateMonitor][net_taskstatemonitor] предоставляет приложениям .NET пакетной службы вспомогательные служебные программы для мониторинга состояния задач.</span><span class="sxs-lookup"><span data-stu-id="f8e96-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="f8e96-307">В `MonitorTasks`, *DotNetTutorial* ожидает, пока все задачи tooreach [TaskState.Completed] [ net_taskstate] за отведенное время.</span><span class="sxs-lookup"><span data-stu-id="f8e96-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks tooreach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="f8e96-308">Затем он завершает задание hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-308">Then it terminates hello job.</span></span>
3. <span data-ttu-id="f8e96-309">**TerminateJobAsync**: завершение задания с помощью [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (или hello блокировки JobOperations.TerminateJob) помечает задание как завершенное.</span><span class="sxs-lookup"><span data-stu-id="f8e96-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or hello blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="f8e96-310">Это основные toodo таким образом, если решение пакет использует [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="f8e96-310">It is essential toodo so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="f8e96-311">Это особый тип задачи, который описан в статье о [задачах подготовки и завершения заданий](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="f8e96-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="f8e96-312">Hello `MonitorTasks` метод *DotNetTutorial* `Program.cs` показан ниже:</span><span class="sxs-lookup"><span data-stu-id="f8e96-312">hello `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="f8e96-313">Шаг 7. Загрузка выходных данных задачи</span><span class="sxs-lookup"><span data-stu-id="f8e96-313">Step 7: Download task output</span></span>
<span data-ttu-id="f8e96-314">![Загрузка выходных данных задачи из службы хранилища][7]</span><span class="sxs-lookup"><span data-stu-id="f8e96-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="f8e96-315">Теперь, когда hello работа завершена, hello выходные данные задач hello можно загрузить из хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e96-315">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="f8e96-316">Это делается с помощью вызова слишком`DownloadBlobsFromContainerAsync` в *DotNetTutorial* `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="f8e96-316">This is done with a call too`DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="f8e96-317">Здравствуйте вызов слишком`DownloadBlobsFromContainerAsync` в hello *DotNetTutorial* приложение указывает, hello файлы должны быть загруженного tooyour `%TEMP%` папки.</span><span class="sxs-lookup"><span data-stu-id="f8e96-317">hello call too`DownloadBlobsFromContainerAsync` in hello *DotNetTutorial* application specifies that hello files should be downloaded tooyour `%TEMP%` folder.</span></span> <span data-ttu-id="f8e96-318">Свободное toomodify считаете это расположение выходных данных.</span><span class="sxs-lookup"><span data-stu-id="f8e96-318">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="f8e96-319">Шаг 8. Удаление контейнеров</span><span class="sxs-lookup"><span data-stu-id="f8e96-319">Step 8: Delete containers</span></span>
<span data-ttu-id="f8e96-320">Поскольку плата взимается для данных, которые хранятся в хранилище Azure, всегда является хорошей идеей tooremove больших двоичных объектов, больше не нужны для пакетных заданий.</span><span class="sxs-lookup"><span data-stu-id="f8e96-320">Because you are charged for data that resides in Azure Storage, it's always a good idea tooremove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="f8e96-321">В его DotNetTutorial `Program.cs`, это делается с помощью трех вызовов toohello вспомогательный метод `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="f8e96-321">In DotNetTutorial's `Program.cs`, this is done with three calls toohello helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="f8e96-322">сам метод Hello просто Получает контейнер toohello ссылку, а затем вызывает [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="f8e96-322">hello method itself merely obtains a reference toohello container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="f8e96-323">Шаг 9: Удалить задание hello и hello пула</span><span class="sxs-lookup"><span data-stu-id="f8e96-323">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="f8e96-324">На заключительном этапе hello все запрашиваемые toodelete hello задания и hello пул, созданные приложением DotNetTutorial hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-324">In hello final step, you're prompted toodelete hello job and hello pool that were created by hello DotNetTutorial application.</span></span> <span data-ttu-id="f8e96-325">Вы не оплачиваете задания и задачи, но *платите* за используемые вычислительные узлы.</span><span class="sxs-lookup"><span data-stu-id="f8e96-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="f8e96-326">Поэтому рекомендуется выделять узлы только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="f8e96-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="f8e96-327">Удаление неиспользуемых пулов может быть частью процесса обслуживания.</span><span class="sxs-lookup"><span data-stu-id="f8e96-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="f8e96-328">Hello BatchClient [JobOperations] [ net_joboperations] и [PoolOperations] [ net_pooloperations] имеют соответствующие методы удаления, которые вызываются, если Удаление подтверждения пользователем Hello:</span><span class="sxs-lookup"><span data-stu-id="f8e96-328">hello BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if hello user confirms deletion:</span></span>

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> <span data-ttu-id="f8e96-329">Помните, что вы платите за использование вычислительных ресурсов, поэтому удаление неиспользуемых пулов позволит сократить затраты.</span><span class="sxs-lookup"><span data-stu-id="f8e96-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="f8e96-330">Кроме того помните, что при удалении пула удаляются все вычислительные узлы этого пула, и все данные на узлах hello будет неустранимой после удаления пула hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-dotnettutorial-sample"></a><span data-ttu-id="f8e96-331">Запустите hello *DotNetTutorial* образца</span><span class="sxs-lookup"><span data-stu-id="f8e96-331">Run hello *DotNetTutorial* sample</span></span>
<span data-ttu-id="f8e96-332">При запуске образца приложения hello, вывод на консоль hello будет примерно следующее toohello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-332">When you run hello sample application, hello console output will be similar toohello following.</span></span> <span data-ttu-id="f8e96-333">Во время выполнения, могут возникнуть приостановит `Awaiting task completion, timeout in 00:30:00...` во время запуска hello пул вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="f8e96-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while hello pool's compute nodes are started.</span></span> <span data-ttu-id="f8e96-334">Используйте hello [портал Azure] [ azure_portal] toomonitor пула, вычислительные узлы, заданий и задач во время и после выполнения.</span><span class="sxs-lookup"><span data-stu-id="f8e96-334">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="f8e96-335">Используйте hello [портал Azure] [ azure_portal] или hello [обозреватель хранилищ Azure] [ storage_explorers] tooview hello ресурсов хранилища (контейнеры и большие двоичные объекты), создается приложение hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-335">Use hello [Azure portal][azure_portal] or hello [Azure Storage Explorer][storage_explorers] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

<span data-ttu-id="f8e96-336">Обычно время выполнения равно **около 5 минут** при запуске приложения hello в конфигурации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f8e96-336">Typical execution time is **approximately 5 minutes** when you run hello application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="f8e96-337">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f8e96-337">Next steps</span></span>
<span data-ttu-id="f8e96-338">Чувствовать себя свободного toomake изменения слишком*DotNetTutorial* и *TaskApplication* tooexperiment с различными вычислений сценариев.</span><span class="sxs-lookup"><span data-stu-id="f8e96-338">Feel free toomake changes too*DotNetTutorial* and *TaskApplication* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="f8e96-339">Например, попробуйте добавить задержки выполнения слишком*TaskApplication*, такие как в случае с [Thread.Sleep][net_thread_sleep], toosimulate длительные задачи, а также отслеживать их на портале hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-339">For example, try adding an execution delay too*TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="f8e96-340">Попробуйте установить дополнительные задачи или изменить hello количество вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="f8e96-340">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="f8e96-341">Добавление toocheck логику для и разрешить использование hello существующих времени выполнения toospeed пула (*указание*: извлечение `ArticleHelpers.cs` в hello [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] проекта в [образцы azure пакета][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="f8e96-341">Add logic toocheck for and allow hello use of an existing pool toospeed execution time (*hint*: check out `ArticleHelpers.cs` in hello [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="f8e96-342">Теперь, когда вы знакомы с hello базовый рабочий процесс пакета решения, это время toodig в дополнительные возможности toohello hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="f8e96-342">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="f8e96-343">Просмотрите hello [возможности пакетной обработки Обзор Azure](batch-api-basics.md) статьи, которая рекомендуется, если вы новую службу toohello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-343">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="f8e96-344">Здравствуйте, запуска на другие статьи по разработке пакета в списке **разработки подробные** в hello [план обучения пакета][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="f8e96-344">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="f8e96-345">Извлечение другой реализации обработки рабочей нагрузки hello «N основных слова» с помощью пакета в hello [TopNWords] [ github_topnwords] образца.</span><span class="sxs-lookup"><span data-stu-id="f8e96-345">Check out a different implementation of processing hello "top N words" workload by using Batch in hello [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="f8e96-346">Просмотрите hello пакета .NET [заметки о выпуске](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) для hello последние изменения в библиотеке hello.</span><span class="sxs-lookup"><span data-stu-id="f8e96-346">Review hello Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for hello latest changes in hello library.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Создание контейнеров в службе хранилища Azure"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Задача передачи приложения и ввода (данных) файлы toocontainers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Создание пула пакетной службы"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Создание задания пакетной службы"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Добавление задачи toojob"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Мониторинг задач"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Скачивание выходных данных задачи из службы хранилища"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Рабочий процесс решения пакетной службы (полная схема)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Учетные данные пакетной службы на портале"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Учетные данные службы хранилища на портале"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Рабочий процесс решения пакетной службы (сокращенная схема)"
