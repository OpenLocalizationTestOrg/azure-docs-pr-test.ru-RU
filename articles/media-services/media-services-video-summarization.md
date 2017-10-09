---
title: "Azure Media Video эскизы aaaUse tooCreate сводку видео | Документы Microsoft"
description: "Видео формирования сводных данных поможет вам создать сводные видеофайлов большого размера, выбрав интересные фрагменты автоматически из источника видео hello. Это полезно при необходимости tooprovide краткий обзор какие tooexpect в длинного видео."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 0a8f0bba6c12a948b940114fe4937e675688a8c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a><span data-ttu-id="d8a42-104">Использование Azure Media Video эскизы tooCreate сводку видео</span><span class="sxs-lookup"><span data-stu-id="d8a42-104">Use Azure Media Video Thumbnails tooCreate a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="d8a42-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="d8a42-105">Overview</span></span>
<span data-ttu-id="d8a42-106">Hello **Azure Media видео эскизы** обработчик мультимедиа (MP) позволяет toocreate Сводка видео, полезно toocustomers, просто нужно toopreview Сводка длинного видео.</span><span class="sxs-lookup"><span data-stu-id="d8a42-106">hello **Azure Media Video Thumbnails** media processor (MP) enables you toocreate a summary of a video that is useful toocustomers who just want toopreview a summary of a long video.</span></span> <span data-ttu-id="d8a42-107">Например, клиентам может потребоваться toosee короткий «Сводка видео» Если задержать указатель мыши над эскиз.</span><span class="sxs-lookup"><span data-stu-id="d8a42-107">For example, customers might want toosee a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="d8a42-108">Изменив параметры hello **Azure Media Video эскизы** набора конфигурации, позволяет использовать мощные однократного обнаружения hello точки Управления и объединения tooalgorithmically технологии создания описательные subclip.</span><span class="sxs-lookup"><span data-stu-id="d8a42-108">By tweaking hello parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use hello MP's powerful shot detection and concatenation technology tooalgorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="d8a42-109">Hello **Azure Media Video эскиз** MP в настоящее время находится в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="d8a42-109">hello **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="d8a42-110">В этом разделе приведены подробные сведения о **Azure Media Video эскиз** и показано, как toouse с помощью пакета SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="d8a42-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="d8a42-111">Ограничения</span><span class="sxs-lookup"><span data-stu-id="d8a42-111">Limitations</span></span>

<span data-ttu-id="d8a42-112">В некоторых случаях если видео не состоит из различных сцен hello выходных данных будет только один снимок.</span><span class="sxs-lookup"><span data-stu-id="d8a42-112">In some cases, if your video is not comprised of different scenes, hello output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="d8a42-113">Пример сводки видео</span><span class="sxs-lookup"><span data-stu-id="d8a42-113">Video summary example</span></span>
<span data-ttu-id="d8a42-114">Ниже приведены некоторые примеры того, какой обработчик мультимедиа Azure Media Video эскизы hello можно сделать.</span><span class="sxs-lookup"><span data-stu-id="d8a42-114">Here are some examples of what hello Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="d8a42-115">Исходное видео</span><span class="sxs-lookup"><span data-stu-id="d8a42-115">Original video</span></span>
[<span data-ttu-id="d8a42-116">Исходное видео</span><span class="sxs-lookup"><span data-stu-id="d8a42-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="d8a42-117">Результат — эскиз видео</span><span class="sxs-lookup"><span data-stu-id="d8a42-117">Video thumbnail result</span></span>
[<span data-ttu-id="d8a42-118">Результат — эскиз видео</span><span class="sxs-lookup"><span data-stu-id="d8a42-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="d8a42-119">Конфигурация задачи (предустановка)</span><span class="sxs-lookup"><span data-stu-id="d8a42-119">Task configuration (preset)</span></span>
<span data-ttu-id="d8a42-120">При создании эскиза видео с помощью **Azure Media Video Thumbnails**необходимо указать предустановку конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d8a42-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="d8a42-121">Hello эскиза примера выше создавался hello, следуя базовой конфигурации JSON:</span><span class="sxs-lookup"><span data-stu-id="d8a42-121">hello above thumbnail sample was created with hello following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="d8a42-122">В настоящее время можно изменить hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="d8a42-122">Currently, you can change hello following parameters:</span></span>

| <span data-ttu-id="d8a42-123">Параметр</span><span class="sxs-lookup"><span data-stu-id="d8a42-123">Param</span></span> | <span data-ttu-id="d8a42-124">Описание</span><span class="sxs-lookup"><span data-stu-id="d8a42-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d8a42-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="d8a42-125">outputAudio</span></span> |<span data-ttu-id="d8a42-126">Указывает, содержит ли результирующий видео hello звуковых.</span><span class="sxs-lookup"><span data-stu-id="d8a42-126">Specifies whether or not hello resultant video contains any audio.</span></span> <br/><span data-ttu-id="d8a42-127">Допустимые значения: True или False.</span><span class="sxs-lookup"><span data-stu-id="d8a42-127">Allowed values are: True or False.</span></span> <span data-ttu-id="d8a42-128">Значение по умолчанию — True.</span><span class="sxs-lookup"><span data-stu-id="d8a42-128">Default is True.</span></span> |
| <span data-ttu-id="d8a42-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="d8a42-129">fadeInFadeOut</span></span> |<span data-ttu-id="d8a42-130">Указывает ли исчезания переходы используются для взаимодействия между hello отдельные движения эскизы.</span><span class="sxs-lookup"><span data-stu-id="d8a42-130">Specifies whether or not fade transitions are used between hello separate motion thumbnails.</span></span>  <br/><span data-ttu-id="d8a42-131">Допустимые значения: True или False.</span><span class="sxs-lookup"><span data-stu-id="d8a42-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="d8a42-132">Значение по умолчанию — True.</span><span class="sxs-lookup"><span data-stu-id="d8a42-132">Default is True.</span></span> |
| <span data-ttu-id="d8a42-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="d8a42-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="d8a42-134">Целое число, указывающее видео целиком результирующая длительность hello должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="d8a42-134">Integer that specifies how long hello entire resultant video shall be.</span></span>  <span data-ttu-id="d8a42-135">По умолчанию зависит от продолжительности исходного видео.</span><span class="sxs-lookup"><span data-stu-id="d8a42-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="d8a42-136">Hello следующей таблице описаны длительность по умолчанию hello, когда **maxMotionThumbnailInSecs** не используется.</span><span class="sxs-lookup"><span data-stu-id="d8a42-136">hello following table describes hello default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d8a42-137">Продолжительность видео</span><span class="sxs-lookup"><span data-stu-id="d8a42-137">Video duration</span></span> |<span data-ttu-id="d8a42-138">видео < 3 мин</span><span class="sxs-lookup"><span data-stu-id="d8a42-138">d < 3 min</span></span> |<span data-ttu-id="d8a42-139">3 мин < видео < 15 мин</span><span class="sxs-lookup"><span data-stu-id="d8a42-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="d8a42-140">Продолжительность эскиза</span><span class="sxs-lookup"><span data-stu-id="d8a42-140">Thumbnail duration</span></span> |<span data-ttu-id="d8a42-141">15 с (2–3 сцены)</span><span class="sxs-lookup"><span data-stu-id="d8a42-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="d8a42-142">30 с (3–5 сцен)</span><span class="sxs-lookup"><span data-stu-id="d8a42-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="d8a42-143">Hello следующий JSON задает доступных параметров.</span><span class="sxs-lookup"><span data-stu-id="d8a42-143">hello following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="d8a42-144">Пример кода .NET</span><span class="sxs-lookup"><span data-stu-id="d8a42-144">.NET sample code</span></span>

<span data-ttu-id="d8a42-145">Hello следующей программе показано как:</span><span class="sxs-lookup"><span data-stu-id="d8a42-145">hello following program shows how to:</span></span>

1. <span data-ttu-id="d8a42-146">Создание актива и отправка файла мультимедиа в актив hello.</span><span class="sxs-lookup"><span data-stu-id="d8a42-146">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="d8a42-147">Создает задание с видео эскиза задачу на основе файла конфигурации, содержащий hello, следующая Предустановка json.</span><span class="sxs-lookup"><span data-stu-id="d8a42-147">Creates a job with a video thumbnail task based on a configuration file that contains hello following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="d8a42-148">Загружает hello выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="d8a42-148">Downloads hello output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d8a42-149">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8a42-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="d8a42-150">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d8a42-150">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="d8a42-151">Пример</span><span class="sxs-lookup"><span data-stu-id="d8a42-151">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoSummarization
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);


                // Run hello thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference tooAzure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
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

        }
    }

### <a name="video-thumbnail-output"></a><span data-ttu-id="d8a42-152">Результат — эскиз видео</span><span class="sxs-lookup"><span data-stu-id="d8a42-152">Video thumbnail output</span></span>
[<span data-ttu-id="d8a42-153">Результат — эскиз видео</span><span class="sxs-lookup"><span data-stu-id="d8a42-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="d8a42-154">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d8a42-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d8a42-155">Отзывы</span><span class="sxs-lookup"><span data-stu-id="d8a42-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="d8a42-156">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="d8a42-156">Related links</span></span>
[<span data-ttu-id="d8a42-157">Общие сведения об аналитике служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="d8a42-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="d8a42-158">Демонстрационные материалы для медиааналитики Azure</span><span class="sxs-lookup"><span data-stu-id="d8a42-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

