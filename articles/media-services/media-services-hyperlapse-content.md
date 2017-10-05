---
title: "Обработка файлов мультимедиа с помощью технологии Hyperlapse служб мультимедиа Azure | Документация Майкрософт"
description: "Azure Media Hyperlapse создает плавное замедленное видео от первого лица или содержимое, характерное для экшн-камер. В этом разделе показано, как использовать индексатор мультимедийных данных."
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
ms.openlocfilehash: 02f634c2af04b6b372642ab0e6a17a5d29f16450
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="58ef8-104">Файлы мультимедиа Hyperlapse с Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="58ef8-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="58ef8-105">Azure Media Hyperlapse представляет собой обработчик мультимедиа, создающий плавное замедленное видео от первого лица или содержимое, характерное для экшн-камер.</span><span class="sxs-lookup"><span data-stu-id="58ef8-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="58ef8-106">Microsoft Hyperlapse для служб мультимедиа Azure, облачный аналог [настольной системы Hyperlapse Pro и телефонной системы Hyperlapse Mobile от Microsoft Research](http://aka.ms/hyperlapse), использует обширные возможности масштабирования платформы обработки мультимедиа служб мультимедиа Azure, чтобы реализовать горизонтальное масштабирование и параллелизовать массовую обработку Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="58ef8-106">The cloud-based sibling to [Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes the massive scale of the Azure Media Services Media Processing platform to horizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58ef8-107">Продукт Microsoft Hyperlapse оптимально подходит для работы с содержимым от первого лица с перемещающейся камерой.</span><span class="sxs-lookup"><span data-stu-id="58ef8-107">Microsoft Hyperlapse is designed to work best on first-person content with a moving camera.</span></span>  <span data-ttu-id="58ef8-108">Хотя материал с неподвижной камеры может обрабатываться, производительность и качество обработчика мультимедиа Azure Media Hyperlapse не позволяет гарантировать работу с другими типами содержимого.</span><span class="sxs-lookup"><span data-stu-id="58ef8-108">Although still-camera footage can still work, the performance and quality of the Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="58ef8-109">Чтобы получить дополнительные сведения о Microsoft Hyperlapse для служб мультимедиа Azure и увидеть некоторые видеоматериалы с примерами, ознакомьтесь с [вводной записью блога](http://aka.ms/azurehyperlapseblog) из общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="58ef8-109">To learn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out the [introductory blog post](http://aka.ms/azurehyperlapseblog) from the public preview.</span></span>
> 
> 

<span data-ttu-id="58ef8-110">Задание Azure Media Hyperlapse принимает в качестве входных данных файлы ресурсов MP4, MOV или WMV вместе с файлом конфигурации, который определяет, какие кадры видео должны быть замедлены и на какой скорости (например, первые 10 000 кадров на скорости 2x).</span><span class="sxs-lookup"><span data-stu-id="58ef8-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and to what speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="58ef8-111">Результатом является стабилизированное и замедленное представление входного видео.</span><span class="sxs-lookup"><span data-stu-id="58ef8-111">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

<span data-ttu-id="58ef8-112">Последние новости о Azure Media Hyperlapse см. в [блогах служб мультимедиа](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="58ef8-112">For the latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="58ef8-113">Использование Hyperlapse для обработки ресурса-контейнера</span><span class="sxs-lookup"><span data-stu-id="58ef8-113">Hyperlapse an asset</span></span>
<span data-ttu-id="58ef8-114">Сначала необходимо загрузить требуемый входной файл для служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="58ef8-114">First you will need to upload your desired input file to Azure Media Services.</span></span>  <span data-ttu-id="58ef8-115">Дополнительные сведения об основных понятиях, связанных с загрузкой содержимого и управлением им, см. в статье [об управлении содержимым](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="58ef8-115">To learn more about the concepts involved with uploading and managing content, read the [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="58ef8-116"><a id="configuration"></a>Предустановка конфигурации для Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="58ef8-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="58ef8-117">После помещения содержимого в учетную запись служб мультимедиа необходимо создать предустановку вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="58ef8-117">Once your content is in your Media Services account, you will need to construct your configuration preset.</span></span>  <span data-ttu-id="58ef8-118">В следующей таблице описаны поля, задаваемые пользователем:</span><span class="sxs-lookup"><span data-stu-id="58ef8-118">The following table explains the user-specified fields:</span></span>

| <span data-ttu-id="58ef8-119">Поле</span><span class="sxs-lookup"><span data-stu-id="58ef8-119">Field</span></span> | <span data-ttu-id="58ef8-120">Описание</span><span class="sxs-lookup"><span data-stu-id="58ef8-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="58ef8-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="58ef8-121">StartFrame</span></span> |<span data-ttu-id="58ef8-122">Кадр, с которого должна начинаться обработка Microsoft Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="58ef8-122">The frame upon which the Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="58ef8-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="58ef8-123">NumFrames</span></span> |<span data-ttu-id="58ef8-124">Число обрабатываемых кадров.</span><span class="sxs-lookup"><span data-stu-id="58ef8-124">The number of frames to process</span></span> |
| <span data-ttu-id="58ef8-125">Speed</span><span class="sxs-lookup"><span data-stu-id="58ef8-125">Speed</span></span> |<span data-ttu-id="58ef8-126">Коэффициент ускорения входного видео.</span><span class="sxs-lookup"><span data-stu-id="58ef8-126">The factor with which to speed up the input video.</span></span> |

<span data-ttu-id="58ef8-127">Ниже приведен пример соответствующего файла конфигурации для XML и JSON:</span><span class="sxs-lookup"><span data-stu-id="58ef8-127">The following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="58ef8-128">**Предустановка XML:**</span><span class="sxs-lookup"><span data-stu-id="58ef8-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="58ef8-129">**Предустановка JSON:**</span><span class="sxs-lookup"><span data-stu-id="58ef8-129">**JSON preset:**</span></span>

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

### <span data-ttu-id="58ef8-130"><a id="sample_code"></a> Microsoft Hyperlapse с пакетом AMS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="58ef8-130"><a id="sample_code"></a> Microsoft Hyperlapse with the AMS .NET SDK</span></span>
<span data-ttu-id="58ef8-131">Следующий метод передает файл мультимедиа как ресурс и создает задание с помощью обработчика мультимедиа Azure Media Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="58ef8-131">The following method uploads a media file as an asset and creates a job with the Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="58ef8-132">Для работы этого кода в области с именем "context" уже должен находиться CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="58ef8-132">You should already have a CloudMediaContext in scope with the name "context" for this code to work.</span></span>  <span data-ttu-id="58ef8-133">Дополнительные сведения об этом см. в [статье об управлении содержимым](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="58ef8-133">To learn more about this, read the [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="58ef8-134">Строковый аргумент "hyperConfig" должен быть соответствующей предустановкой конфигурации для JSON или XML, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="58ef8-134">The string argument "hyperConfig" is expected to be a conformant configuration preset in either JSON or XML as described above.</span></span>
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

            // If job state is Error, the event handling
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

### <span data-ttu-id="58ef8-135"><a id="file_types"></a>Поддерживаемые типы файлов</span><span class="sxs-lookup"><span data-stu-id="58ef8-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="58ef8-136">MP4</span><span class="sxs-lookup"><span data-stu-id="58ef8-136">MP4</span></span>
* <span data-ttu-id="58ef8-137">MOV</span><span class="sxs-lookup"><span data-stu-id="58ef8-137">MOV</span></span>
* <span data-ttu-id="58ef8-138">WMV</span><span class="sxs-lookup"><span data-stu-id="58ef8-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="58ef8-139">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="58ef8-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="58ef8-140">Отзывы</span><span class="sxs-lookup"><span data-stu-id="58ef8-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="58ef8-141">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="58ef8-141">Related links</span></span>
[<span data-ttu-id="58ef8-142">Общие сведения об аналитике служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="58ef8-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="58ef8-143">Демонстрационные материалы для медиааналитики Azure</span><span class="sxs-lookup"><span data-stu-id="58ef8-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

