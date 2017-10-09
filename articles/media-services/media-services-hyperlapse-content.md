---
title: "aaaHyperlapse файлов мультимедиа с помощью Azure Media Hyperlapse | Документы Microsoft"
description: "Azure Media Hyperlapse создает плавное замедленное видео от первого лица или содержимое, характерное для экшн-камер. В этом разделе показано, как toouse индексатора мультимедиа."
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="c564a-104">Файлы мультимедиа Hyperlapse с Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c564a-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="c564a-105">Azure Media Hyperlapse представляет собой обработчик мультимедиа, создающий плавное замедленное видео от первого лица или содержимое, характерное для экшн-камер.</span><span class="sxs-lookup"><span data-stu-id="c564a-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="c564a-106">Здравствуйте того же уровня на основе облака, слишком[Microsoft Research рабочего стола Hyperlapse Pro и телефону Hyperlapse Mobile](http://aka.ms/hyperlapse), Hyperlapse Microsoft для служб мультимедиа Azure использует hello массовым масштабированием hello служб мультимедиа Azure Media Обработка toohorizontally платформы масштабировать и параллельного выполнения массового обработка Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="c564a-106">hello cloud-based sibling too[Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes hello massive scale of hello Azure Media Services Media Processing platform toohorizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c564a-107">Microsoft Hyperlapse — спроектированный toowork наиболее содержимое первого лица с помощью перемещения камеры.</span><span class="sxs-lookup"><span data-stu-id="c564a-107">Microsoft Hyperlapse is designed toowork best on first-person content with a moving camera.</span></span>  <span data-ttu-id="c564a-108">Несмотря на то, что по-прежнему могут работать по-прежнему видеокамер, hello производительность и качество hello обработчика мультимедиа Azure Media Hyperlapse не может быть гарантирована для других типов содержимого.</span><span class="sxs-lookup"><span data-stu-id="c564a-108">Although still-camera footage can still work, hello performance and quality of hello Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="c564a-109">toolearn Дополнительные сведения о Hyperlapse Microsoft для служб мультимедиа Azure и разделе некоторые видео с примерами, ознакомьтесь с hello [вводные блога](http://aka.ms/azurehyperlapseblog) из общедоступной предварительной версии hello.</span><span class="sxs-lookup"><span data-stu-id="c564a-109">toolearn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out hello [introductory blog post](http://aka.ms/azurehyperlapseblog) from hello public preview.</span></span>
> 
> 

<span data-ttu-id="c564a-110">Azure Media Hyperlapse задания принимает в качестве входных данных файла ресурса MP4, MOV или WMV вместе с файл конфигурации, который определяет, какие кадры видео должно быть промежуток времени и скорость toowhat (например первый 10 000 кадры 2 x).</span><span class="sxs-lookup"><span data-stu-id="c564a-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and toowhat speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="c564a-111">Hello выводится представление hello входное видео в стабилизации и промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="c564a-111">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

<span data-ttu-id="c564a-112">Последние обновления Azure Media Hyperlapse hello, в разделе [блоги служб мультимедиа](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="c564a-112">For hello latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="c564a-113">Использование Hyperlapse для обработки ресурса-контейнера</span><span class="sxs-lookup"><span data-stu-id="c564a-113">Hyperlapse an asset</span></span>
<span data-ttu-id="c564a-114">Сначала необходимо будет tooupload вашей tooAzure входной файл служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="c564a-114">First you will need tooupload your desired input file tooAzure Media Services.</span></span>  <span data-ttu-id="c564a-115">Дополнительные сведения о toolearn hello понятиями, связанными с отправка и управление содержимым, чтение hello [управления содержимым статьи](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c564a-115">toolearn more about hello concepts involved with uploading and managing content, read hello [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="c564a-116"><a id="configuration"></a>Предустановка конфигурации для Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c564a-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="c564a-117">Как только контента в учетную запись служб мультимедиа, необходимо будет tooconstruct предварительно заданную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="c564a-117">Once your content is in your Media Services account, you will need tooconstruct your configuration preset.</span></span>  <span data-ttu-id="c564a-118">Hello в следующей таблице описываются hello определяемые пользователем поля:</span><span class="sxs-lookup"><span data-stu-id="c564a-118">hello following table explains hello user-specified fields:</span></span>

| <span data-ttu-id="c564a-119">Поле</span><span class="sxs-lookup"><span data-stu-id="c564a-119">Field</span></span> | <span data-ttu-id="c564a-120">Описание</span><span class="sxs-lookup"><span data-stu-id="c564a-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c564a-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="c564a-121">StartFrame</span></span> |<span data-ttu-id="c564a-122">кадр Hello, после которого hello Microsoft Hyperlapse должна начинаться обработка.</span><span class="sxs-lookup"><span data-stu-id="c564a-122">hello frame upon which hello Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="c564a-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="c564a-123">NumFrames</span></span> |<span data-ttu-id="c564a-124">Hello число кадров tooprocess</span><span class="sxs-lookup"><span data-stu-id="c564a-124">hello number of frames tooprocess</span></span> |
| <span data-ttu-id="c564a-125">Speed</span><span class="sxs-lookup"><span data-stu-id="c564a-125">Speed</span></span> |<span data-ttu-id="c564a-126">Коэффициент Hello какие toospeed hello входного видео.</span><span class="sxs-lookup"><span data-stu-id="c564a-126">hello factor with which toospeed up hello input video.</span></span> |

<span data-ttu-id="c564a-127">Hello ниже приведен пример файла конфигурации соответствует стандартам XML и JSON:</span><span class="sxs-lookup"><span data-stu-id="c564a-127">hello following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="c564a-128">**Предустановка XML:**</span><span class="sxs-lookup"><span data-stu-id="c564a-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="c564a-129">**Предустановка JSON:**</span><span class="sxs-lookup"><span data-stu-id="c564a-129">**JSON preset:**</span></span>

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <span data-ttu-id="c564a-130"><a id="sample_code"></a>Microsoft Hyperlapse с hello AMS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c564a-130"><a id="sample_code"></a> Microsoft Hyperlapse with hello AMS .NET SDK</span></span>
<span data-ttu-id="c564a-131">Hello следующий метод отправляет файл мультимедиа в виде актива и создает задание с hello обработчика мультимедиа Azure Media Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="c564a-131">hello following method uploads a media file as an asset and creates a job with hello Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="c564a-132">В области с именем hello «контекст» для этого кода toowork необходимо иметь CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="c564a-132">You should already have a CloudMediaContext in scope with hello name "context" for this code toowork.</span></span>  <span data-ttu-id="c564a-133">Дополнительные сведения об этом, чтения hello toolearn [управления содержимым статьи](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c564a-133">toolearn more about this, read hello [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="c564a-134">Hello строковый аргумент «hyperConfig» является ожидаемым toobe конфигурации согласованность конфигурации в JSON или XML, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="c564a-134">hello string argument "hyperConfig" is expected toobe a conformant configuration preset in either JSON or XML as described above.</span></span>
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
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
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <span data-ttu-id="c564a-135"><a id="file_types"></a>Поддерживаемые типы файлов</span><span class="sxs-lookup"><span data-stu-id="c564a-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="c564a-136">MP4</span><span class="sxs-lookup"><span data-stu-id="c564a-136">MP4</span></span>
* <span data-ttu-id="c564a-137">MOV</span><span class="sxs-lookup"><span data-stu-id="c564a-137">MOV</span></span>
* <span data-ttu-id="c564a-138">WMV</span><span class="sxs-lookup"><span data-stu-id="c564a-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c564a-139">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="c564a-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c564a-140">Отзывы</span><span class="sxs-lookup"><span data-stu-id="c564a-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="c564a-141">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="c564a-141">Related links</span></span>
[<span data-ttu-id="c564a-142">Общие сведения об аналитике служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="c564a-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="c564a-143">Демонстрационные материалы для медиааналитики Azure</span><span class="sxs-lookup"><span data-stu-id="c564a-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

