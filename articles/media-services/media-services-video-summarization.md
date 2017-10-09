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
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a>Использование Azure Media Video эскизы tooCreate сводку видео
## <a name="overview"></a>Обзор
Hello **Azure Media видео эскизы** обработчик мультимедиа (MP) позволяет toocreate Сводка видео, полезно toocustomers, просто нужно toopreview Сводка длинного видео. Например, клиентам может потребоваться toosee короткий «Сводка видео» Если задержать указатель мыши над эскиз. Изменив параметры hello **Azure Media Video эскизы** набора конфигурации, позволяет использовать мощные однократного обнаружения hello точки Управления и объединения tooalgorithmically технологии создания описательные subclip.  

Hello **Azure Media Video эскиз** MP в настоящее время находится в предварительной версии.

В этом разделе приведены подробные сведения о **Azure Media Video эскиз** и показано, как toouse с помощью пакета SDK служб мультимедиа для .NET.

## <a name="limitations"></a>Ограничения

В некоторых случаях если видео не состоит из различных сцен hello выходных данных будет только один снимок.

## <a name="video-summary-example"></a>Пример сводки видео
Ниже приведены некоторые примеры того, какой обработчик мультимедиа Azure Media Video эскизы hello можно сделать.

### <a name="original-video"></a>Исходное видео
[Исходное видео](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a>Результат — эскиз видео
[Результат — эскиз видео](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a>Конфигурация задачи (предустановка)
При создании эскиза видео с помощью **Azure Media Video Thumbnails**необходимо указать предустановку конфигурации. Hello эскиза примера выше создавался hello, следуя базовой конфигурации JSON:

    {"version":"1.0"}

В настоящее время можно изменить hello следующие параметры:

| Параметр | Описание |
| --- | --- |
| outputAudio |Указывает, содержит ли результирующий видео hello звуковых. <br/>Допустимые значения: True или False. Значение по умолчанию — True. |
| fadeInFadeOut |Указывает ли исчезания переходы используются для взаимодействия между hello отдельные движения эскизы.  <br/>Допустимые значения: True или False.  Значение по умолчанию — True. |
| maxMotionThumbnailDurationInSecs |Целое число, указывающее видео целиком результирующая длительность hello должны совпадать.  По умолчанию зависит от продолжительности исходного видео. |

Hello следующей таблице описаны длительность по умолчанию hello, когда **maxMotionThumbnailInSecs** не используется.

|  |  |  |
| --- | --- | --- | --- | --- |
| Продолжительность видео |видео < 3 мин |3 мин < видео < 15 мин |
| Продолжительность эскиза |15 с (2–3 сцены) |30 с (3–5 сцен) |

Hello следующий JSON задает доступных параметров.

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a>Пример кода .NET

Hello следующей программе показано как:

1. Создание актива и отправка файла мультимедиа в актив hello.
2. Создает задание с видео эскиза задачу на основе файла конфигурации, содержащий hello, следующая Предустановка json. 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. Загружает hello выходные файлы. 

#### <a name="create-and-configure-a-visual-studio-project"></a>Создание и настройка проекта Visual Studio

Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Пример

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

### <a name="video-thumbnail-output"></a>Результат — эскиз видео
[Результат — эскиз видео](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Связанные ссылки
[Общие сведения об аналитике служб мультимедиа Azure](media-services-analytics-overview.md)

[Демонстрационные материалы для медиааналитики Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

