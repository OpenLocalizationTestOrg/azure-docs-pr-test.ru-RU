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
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a>Файлы мультимедиа Hyperlapse с Azure Media Hyperlapse
Azure Media Hyperlapse представляет собой обработчик мультимедиа, создающий плавное замедленное видео от первого лица или содержимое, характерное для экшн-камер.  Здравствуйте того же уровня на основе облака, слишком[Microsoft Research рабочего стола Hyperlapse Pro и телефону Hyperlapse Mobile](http://aka.ms/hyperlapse), Hyperlapse Microsoft для служб мультимедиа Azure использует hello массовым масштабированием hello служб мультимедиа Azure Media Обработка toohorizontally платформы масштабировать и параллельного выполнения массового обработка Hyperlapse.

> [!IMPORTANT]
> Microsoft Hyperlapse — спроектированный toowork наиболее содержимое первого лица с помощью перемещения камеры.  Несмотря на то, что по-прежнему могут работать по-прежнему видеокамер, hello производительность и качество hello обработчика мультимедиа Azure Media Hyperlapse не может быть гарантирована для других типов содержимого.  toolearn Дополнительные сведения о Hyperlapse Microsoft для служб мультимедиа Azure и разделе некоторые видео с примерами, ознакомьтесь с hello [вводные блога](http://aka.ms/azurehyperlapseblog) из общедоступной предварительной версии hello.
> 
> 

Azure Media Hyperlapse задания принимает в качестве входных данных файла ресурса MP4, MOV или WMV вместе с файл конфигурации, который определяет, какие кадры видео должно быть промежуток времени и скорость toowhat (например первый 10 000 кадры 2 x).  Hello выводится представление hello входное видео в стабилизации и промежуток времени.

Последние обновления Azure Media Hyperlapse hello, в разделе [блоги служб мультимедиа](https://azure.microsoft.com/blog/topics/media-services/).

## <a name="hyperlapse-an-asset"></a>Использование Hyperlapse для обработки ресурса-контейнера
Сначала необходимо будет tooupload вашей tooAzure входной файл служб мультимедиа.  Дополнительные сведения о toolearn hello понятиями, связанными с отправка и управление содержимым, чтение hello [управления содержимым статьи](media-services-portal-vod-get-started.md).

### <a id="configuration"></a>Предустановка конфигурации для Hyperlapse
Как только контента в учетную запись служб мультимедиа, необходимо будет tooconstruct предварительно заданную конфигурацию.  Hello в следующей таблице описываются hello определяемые пользователем поля:

| Поле | Описание |
| --- | --- |
| StartFrame |кадр Hello, после которого hello Microsoft Hyperlapse должна начинаться обработка. |
| NumFrames |Hello число кадров tooprocess |
| Speed |Коэффициент Hello какие toospeed hello входного видео. |

Hello ниже приведен пример файла конфигурации соответствует стандартам XML и JSON:

**Предустановка XML:**

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

**Предустановка JSON:**

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

### <a id="sample_code"></a>Microsoft Hyperlapse с hello AMS .NET SDK
Hello следующий метод отправляет файл мультимедиа в виде актива и создает задание с hello обработчика мультимедиа Azure Media Hyperlapse.

> [!NOTE]
> В области с именем hello «контекст» для этого кода toowork необходимо иметь CloudMediaContext.  Дополнительные сведения об этом, чтения hello toolearn [управления содержимым статьи](media-services-dotnet-get-started.md).
> 
> [!NOTE]
> Hello строковый аргумент «hyperConfig» является ожидаемым toobe конфигурации согласованность конфигурации в JSON или XML, как описано выше.
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

### <a id="file_types"></a>Поддерживаемые типы файлов
* MP4
* MOV
* WMV

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Связанные ссылки
[Общие сведения об аналитике служб мультимедиа Azure](media-services-analytics-overview.md)

[Демонстрационные материалы для медиааналитики Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

