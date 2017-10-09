---
title: "aaaAdvanced кодирование с помощью расширенного рабочего процесса кодировщика мультимедиа | Документы Microsoft"
description: "Узнайте, как tooencode с расширенного рабочего процесса кодировщика мультимедиа. Примеры кода на языке C# и используйте hello пакета SDK служб мультимедиа для .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="14f69-104">Дополнительное кодирование с помощью рабочего процесса Premium кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="14f69-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="14f69-105">Обработчик мультимедиа расширенного рабочего процесса кодировщика мультимедиа, рассматриваемый в этом разделе, недоступен в Китае.</span><span class="sxs-lookup"><span data-stu-id="14f69-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="14f69-106">Вопросы о кодировщике Premium направляйте по адресу mepd@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="14f69-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="14f69-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="14f69-107">Overview</span></span>
<span data-ttu-id="14f69-108">Службы мультимедиа Microsoft Azure введение hello **расширенного рабочего процесса кодировщика мультимедиа** обработчика мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="14f69-108">Microsoft Azure Media Services is introducing hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="14f69-109">Данный обработчик предоставляет расширенные возможности кодирования для рабочих процессов уровня premium по требованию.</span><span class="sxs-lookup"><span data-stu-id="14f69-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="14f69-110">Hello ниже описаны сведения, связанные с слишком**расширенного рабочего процесса кодировщика мультимедиа**:</span><span class="sxs-lookup"><span data-stu-id="14f69-110">hello following topics outline details related too**Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="14f69-111">[Форматирует поддерживаемые с hello расширенного рабочего процесса кодировщика мультимедиа](media-services-premium-workflow-encoder-formats.md) — описание hello форматы и кодеки, поддерживаемые **расширенного рабочего процесса кодировщика мультимедиа**.</span><span class="sxs-lookup"><span data-stu-id="14f69-111">[Formats Supported by hello Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses hello file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="14f69-112">[Обзор и сравнение Azure по запросу мультимедиа кодировщики](media-services-encode-asset.md) сравнивает hello кодирования возможности **расширенного рабочего процесса кодировщика мультимедиа** и **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="14f69-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares hello encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="14f69-113">В этом разделе показано, как tooencode с **расширенного рабочего процесса кодировщика мультимедиа** с использованием .NET.</span><span class="sxs-lookup"><span data-stu-id="14f69-113">This topic demonstrates how tooencode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="14f69-114">Кодирование задачи для hello **расширенного рабочего процесса кодировщика мультимедиа** требуется отдельный файл конфигурации, называемый файлом рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="14f69-114">Encoding tasks for hello **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="14f69-115">Эти файлы имеют расширение цифры и создаются с помощью hello [конструктора рабочих процессов](media-services-workflow-designer.md) средства.</span><span class="sxs-lookup"><span data-stu-id="14f69-115">These files have a .workflow extension and are created using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="14f69-116">Можно также получить по умолчанию hello файлы рабочего процесса [здесь](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="14f69-116">You can also get hello default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="14f69-117">Hello папка также содержит описание hello этих файлов.</span><span class="sxs-lookup"><span data-stu-id="14f69-117">hello folder also contains hello description of these files.</span></span>

<span data-ttu-id="14f69-118">файлы рабочего процесса Hello необходима учетная запись служб мультимедиа tooyour toobe загружен как основное средство и необходимо передать этот ресурс toohello кодирование задачи.</span><span class="sxs-lookup"><span data-stu-id="14f69-118">hello workflow files need toobe uploaded tooyour Media Services account as an Asset, and this Asset should be passed in toohello encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="14f69-119">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="14f69-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="14f69-120">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="14f69-120">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="14f69-121">Пример кодирования</span><span class="sxs-lookup"><span data-stu-id="14f69-121">Encoding example</span></span>

<span data-ttu-id="14f69-122">Hello следующем примере показано, как tooencode с **расширенного рабочего процесса кодировщика мультимедиа**.</span><span class="sxs-lookup"><span data-stu-id="14f69-122">hello following example demonstrates how tooencode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="14f69-123">выполняются следующие шаги Hello.</span><span class="sxs-lookup"><span data-stu-id="14f69-123">hello following steps are performed:</span></span>

1. <span data-ttu-id="14f69-124">Создание ресурса и отправка файла рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="14f69-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="14f69-125">Создание ресурса и отправка исходного файла мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="14f69-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="14f69-126">Получите обработчик мультимедиа «Media расширенного рабочего процесса кодировщика» hello.</span><span class="sxs-lookup"><span data-stu-id="14f69-126">Get hello "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="14f69-127">Создание задания и задачи.</span><span class="sxs-lookup"><span data-stu-id="14f69-127">Create a job and a task.</span></span>

    <span data-ttu-id="14f69-128">В большинстве случаев строка hello конфигурации для задачи «hello» пуста (например, в следующий пример hello).</span><span class="sxs-lookup"><span data-stu-id="14f69-128">In most cases, hello configuration string for hello task is empty (like in hello following example).</span></span> <span data-ttu-id="14f69-129">Существуют некоторых сложных сценариев (которые требуют динамически свойствам среды выполнения tootooset) в этом случае будет предоставлен кодирования задачу toohello строку XML.</span><span class="sxs-lookup"><span data-stu-id="14f69-129">There are some advanced scenarios (that require you tootooset runtime properties dynamically) in which case you would provide an XML string toohello encoding task.</span></span> <span data-ttu-id="14f69-130">Примеры таких сценариев: создание наложения, параллельное или последовательное совмещение мультимедиа, субтитры.</span><span class="sxs-lookup"><span data-stu-id="14f69-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="14f69-131">Добавьте две задачи toohello входные активы.</span><span class="sxs-lookup"><span data-stu-id="14f69-131">Add two input assets toohello task.</span></span>

    1. <span data-ttu-id="14f69-132">1-го — активов hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="14f69-132">1st – hello workflow asset.</span></span>
    2. <span data-ttu-id="14f69-133">2 — видео активов hello.</span><span class="sxs-lookup"><span data-stu-id="14f69-133">2nd – hello video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="14f69-134">Hello активов рабочего процесса должны быть добавлены toohello задач перед hello актив мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="14f69-134">hello workflow asset must be added toohello task before hello media asset.</span></span>
   <span data-ttu-id="14f69-135">Строка Hello конфигурации для этой задачи должно быть пустым.</span><span class="sxs-lookup"><span data-stu-id="14f69-135">hello configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="14f69-136">Отправка задания кодирования hello.</span><span class="sxs-lookup"><span data-stu-id="14f69-136">Submit hello encoding job.</span></span>

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
                    }

                    return job.OutputMediaAssets[0];
                }

                static private void StateChanged(object sender, JobStateChangedEventArgs e)
                {
                    Console.WriteLine("Job state changed event:");
                    Console.WriteLine("  Previous state: " + e.PreviousState);
                    Console.WriteLine("  Current state: " + e.CurrentState);

                    switch (e.CurrentState)
                    {
                        case JobState.Finished:
                            Console.WriteLine();
                            Console.WriteLine("Job is finished.");
                            Console.WriteLine();
                            break;
                        case JobState.Canceling:
                        case JobState.Queued:
                        case JobState.Scheduled:
                        case JobState.Processing:
                            Console.WriteLine("Please wait...\n");
                            break;
                        case JobState.Canceled:
                        case JobState.Error:
                            // Cast sender as a job.
                            IJob job = (IJob)sender;
                            // Display or log error details as needed.
                            // LogJobStop(job.Id);
                            break;
                        default:
                            break;
                    }
                }
                private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
                {
                    var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                    ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                    if (processor == null)
                        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                    return processor;
                }
            }
        }

<span data-ttu-id="14f69-137">Вопросы о кодировщике Premium направляйте по адресу mepd@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="14f69-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="14f69-138">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="14f69-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="14f69-139">Отзывы</span><span class="sxs-lookup"><span data-stu-id="14f69-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
