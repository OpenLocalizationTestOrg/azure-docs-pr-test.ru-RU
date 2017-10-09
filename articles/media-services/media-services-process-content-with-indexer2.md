---
title: "aaaIndexing файлов мультимедиа с помощью предварительной версии 2 индексатора мультимедиа Azure | Документы Microsoft"
description: "Индексатор мультимедиа Azure позволяет toomake содержимого для поиска файлов мультимедиа и toogenerate полнотекстового сообщения для закрыто субтитров и ключевых слов. В этом разделе показано, как просмотреть toouse индексатора мультимедиа 2."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 85d25525-a498-44eb-ae3a-2ca5ceb8e53d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: f83fa0db58b828ffa29933d68ce108b4906dcd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a>Индексирование файлов мультимедиа с помощью индексатора мультимедийных данных Azure 2 (предварительная версия)
## <a name="overview"></a>Обзор
Hello **предварительной версии 2 индексатора мультимедиа Azure** обработчик мультимедиа (MP) позволяет toomake файлы и контент мультимедиа с возможностью поиска, а также создавать дорожек со скрытыми субтитрами. Сравниваемые toohello предыдущей версии [индексатора мультимедиа Azure](media-services-index-content.md), **предварительной версии 2 индексатора мультимедиа Azure** выполняет более быстрого индексирования и обеспечивает более широкую поддержку языка. В число поддерживаемых языков входят английский, испанский, французский, немецкий, итальянский, китайский (мандаринский диалект, упрощенное письмо), португальский, арабский и японский.

Hello **предварительной версии 2 индексатора мультимедиа Azure** MP в настоящее время находится в предварительной версии.

В этом разделе показано, как индексирование toocreate заданий с **предварительной версии 2 индексатора мультимедиа Azure**.

> [!NOTE]
> применить Hello следующие вопросы:
> 
> Индексатор 2 не поддерживается в Azure в Китае и Azure для государственных организаций.
> 
> Во время индексирования содержимого, убедитесь, что toouse файлы мультимедиа, которые максимально разборчивой речью (без фоновой музыки, шума, эффектов или шипения микрофона). Примерами подходящего содержимого могут служить записи собраний, лекций или презентаций. Hello следующее содержимое может не подходить для индексирования: фильмы, ТВ-передачи, что-либо со смешанными аудио- и звуковыми эффектами, некачественная запись содержимого с фоновым шумом (шипением).
> 
> 

В этом разделе приведены подробные сведения о **предварительной версии 2 индексатора мультимедиа Azure** и показано, как toouse с помощью пакета SDK служб мультимедиа для .NET

## <a name="input-and-output-files"></a>Входные и выходные файлы
### <a name="input-files"></a>Входные файлы
Аудио- или видеофайлы

### <a name="output-files"></a>Выходные файлы
Задание индексирования можно создать файлы титров hello следующие форматы:  

* **SAMI**
* **TTML**
* **WebVTT**

Закрытых субтитров (CC) файлов в этих форматах можно использовать toomake аудио и видео файлы доступны toopeople возможностями слуха.

## <a name="task-configuration-preset"></a>Конфигурация задачи (предустановка)
При создании задачи индексирования с помощью **предварительной версии индексатора мультимедийных данных Azure 2**необходимо указать предустановку конфигурации.

Hello следующий JSON задает доступных параметров.

    {
      "version":"1.0",
      "Features":
        [
           {
           "Options": {
                "Formats":["WebVtt","ttml"],
                "Language":"enUs",
                "Type":"RecoOptions"
           },
           "Type":"SpReco"
        }]
    }

## <a name="supported-languages"></a>Поддерживаемые языки
Предварительная версия 2 для Azure Media индексатор поддерживает речи в текст hello следующих языков (при указании имени языка hello в конфигурации задачи hello, используйте 4-значный код в квадратные скобки, как показано ниже).

* английский [EnUs];
* испанский [EsEs];
* китайский (мандаринский диалект, упрощенное письмо) [ZhCn];
* французский [FrFr];
* немецкий [DeDe];
* итальянский [ItIt];
* португальский [PtBr];
* арабский (Египет) [ArEg].
* японский [JaJp].
* русский [RuRu];
* британский английский [EnGb];
* испанский (Мексика) [EsMx]; 

## <a name="supported-file-types"></a>Поддерживаемые типы файлов

Сведения о типах файлов, поддерживаемых см. в разделе hello [поддерживаемые кодеки и форматы](media-services-media-encoder-standard-formats.md#input-containerfile-formats) раздела.

## <a name="net-sample-code"></a>Пример кода .NET

Hello следующей программе показано как:

1. Создание актива и отправка файла мультимедиа в актив hello.
2. Создание задания с задачи индексирования на основе файла конфигурации, содержащий hello, следующая Предустановка json.
   
        {
          "version":"1.0",
          "Features":
            [
               {
               "Options": {
                    "Formats":["WebVtt","ttml"],
                    "Language":"enUs",
                    "Type":"RecoOptions"
               },
               "Type":"SpReco"
            }]
        }
3. Загрузите hello выходные файлы. 
   
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

    namespace IndexContent
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

                // Run indexing job.
                var asset = RunIndexingJob(@"C:\supportFiles\Indexer\BigBuckBunny.mp4",
                                            @"C:\supportFiles\Indexer\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\Indexer\Output");
            }

            static IAsset RunIndexingJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Indexing Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Indexing Job");

                // Get a reference tooAzure Media Indexer 2 Preview.
                string MediaProcessorName = "Azure Media Indexer 2 Preview";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Indexing Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset toobe indexed.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Связанные ссылки
[Общие сведения об аналитике служб мультимедиа Azure](media-services-analytics-overview.md)

[Демонстрационные материалы для медиааналитики Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

