---
title: "грани aaaRedact с медиа-аналитика Azure | Документы Microsoft"
description: "В этом разделе показано, как tooredact сталкивается с мультимедиа Azure analytics."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a>Скрытие лиц с помощью аналитики мультимедиа Azure
## <a name="overview"></a>Обзор
**Azure Media Redactor** — [медиа-аналитика Azure](media-services-analytics-overview.md) обработчик мультимедиа (MP), который предлагает исправления масштабируемой лицевой стороны в облаке hello. Исправления лицевой стороны позволяет вам toomodify видео в гранях tooblur порядок выбранных сотрудников. Вы можете toouse hello начертания исправления службы в общих сценариях безопасности и новости мультимедиа. Через несколько минут, содержащий несколько начертаний материал может занять tooredact часы вручную, но с этой службы hello начертания процесс исправления потребуется всего несколько простых шагов. Дополнительные сведения см. в [этом блоге](https://azure.microsoft.com/blog/azure-media-redactor/).

В этом разделе приведены подробные сведения о **Redactor мультимедиа Azure** и показано, как toouse с помощью пакета SDK служб мультимедиа для .NET.

Hello **Redactor мультимедиа Azure** MP в настоящее время находится в предварительной версии. Он доступен во всех общедоступных регионах Azure, а также в центрах обработки данных для государственных организаций США и для Китая. В настоящее время эта предварительная версия предоставляется бесплатно. 

## <a name="face-redaction-modes"></a>Режимы скрытия лиц
Лица исправления работает путем обнаружения лиц в каждом кадре видео и отслеживания начертания hello объекта оба вперед и назад по времени, чтобы hello же человек может быть размытое из других углы наклона. Hello автоматические исправления процесс очень сложный и не всегда выдает 100% нужного выходных данных, поэтому медиа-аналитика обеспечивает несколько способов toomodify hello конечного результата.

В полностью автоматическом режиме Добавление tooa нет двухпроходный рабочий процесс, который позволяет hello выбора или деактивировать-selection найден сторон через список идентификаторов. Кроме того произвольный каждого кадра корректировки hello MP toomake использует файл метаданных в формате JSON. Этот рабочий процесс разделен на два режима: **анализ** и **скрытие**. Можно объединить два режима hello за один проход, выполняет обе задачи в одно задание; Этот режим называется **объединенное**.

### <a name="combined-mode"></a>Объединенный режим
В результате вы получите MP4-файл с автоматическим скрытием, который не нужно править вручную.

| Этап | Имя файла | Примечания |
| --- | --- | --- |
| Входной ресурс-контейнер |foo.bar |Видео в формате WMV, MOV или MP4 |
| Входная конфигурация |Конфигурация задания (предустановка) |{'version':'1.0', 'options': {'mode':'combined'}} |
| Выходной ресурс-контейнер |foo_redacted.mp4 |Видео с размытием |

#### <a name="input-example"></a>Пример входных данных
[См. видео](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a>Пример выходных данных
[См. видео](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a>Режим анализа
Hello **анализ** этап рабочего процесса двухпроходный hello входные видео и создает файл JSON расположений лицевой стороны, а изображений jpg каждого обнаруженного начертания.

| Этап | Имя файла | Примечания |
| --- | --- | --- |
| Входной ресурс-контейнер |foo.bar |Видео в формате WMV, MPV или MP4 |
| Входная конфигурация |Конфигурация задания (предустановка) |{'version':'1.0', 'options': {'mode':'analyze'}} |
| Выходной ресурс-контейнер |foo_annotations.json |Аннотация с данными о расположении лиц в формате JSON. Это можно изменить путем hello пользователя toomodify hello стирают ограничительные рамки. См. пример ниже. |
| Выходной ресурс-контейнер |foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg] |Обрезанное jpg каждого обнаружил лицо, где число hello указывает labelId hello гарнитур hello |

#### <a name="output-example"></a>Пример выходных данных

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a>Режим скрытия
Hello второго этапа hello рабочего процесса имеет большее количество входных данных, которые должны быть объединены в один ресурс.

Они включают список идентификаторов tooblur исходного видео hello и заметок hello JSON. Этот режим использует стирают tooapply hello заметок на входное видео hello.

Hello выходные данные этапа анализ hello не включает hello исходного видео. Hello видео должен toobe отправлен в hello входного актива для задачи в режиме Redact hello и выбран в качестве первичного файла hello.

| Этап | Имя файла | Примечания |
| --- | --- | --- |
| Входной ресурс-контейнер |foo.bar |Видео в формате WMV, MPV или MP4. То же видео, что и на этапе 1. |
| Входной ресурс-контейнер |foo_annotations.json |Файл аннотации с метаданными, полученными на этапе 1, с необязательными изменениями. |
| Входной ресурс-контейнер |foo_IDList.txt (необязательный) |Необязательный новую строку запятыми список идентификаторов tooredact лицевой стороны. Если оставить его пустым, будут размыты все лица. |
| Входная конфигурация |Конфигурация задания (предустановка) |{'version':'1.0', 'options': {'mode':'redact'}} |
| Выходной ресурс-контейнер |foo_redacted.mp4 |Видео с размытием, примененным на основе аннотаций |

#### <a name="example-output"></a>Пример выходных данных
Это hello вывод Список_идентификаторов с выбран один идентификатор.

[См. видео](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

Пример foo_IDList.txt
 
     1
     2
     3

## <a name="blur-types"></a>Типы размытия

В hello **объединенное** или **Redact** режиме существует 5 режима разных размытия, можно выбрать через входной конфигурации JSON hello: **Low**, **Med**, **Высокой**, **отладки**, и **черный**. По умолчанию используется режим **Med** (Средний).

Можно найти примеры hello Размытие ниже типы.

### <a name="example-json"></a>Пример JSON:

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a>Низкий

![Низкий](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a>Средний

![Средний](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a>Высокий

![Высокий](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a>Отладка

![Отладка](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a>Черный

![Черный](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a>Элементы hello выходных данных JSON-файла

Hello MP исправления предоставляет высокой точности начертания расположение обнаружения и отслеживания для определения вверх too64 человека граней в кадров видео. Распознавания фронтальных видов лица предоставляют hello лучшей при боковые и небольшие фрагменты (меньше или равно too24x24 пикселей) требуют.

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a>Пример кода .NET

Hello следующей программе показано как:

1. Создание актива и отправка файла мультимедиа в актив hello.
2. Создание задания с задачей «исправление» начертания на основе файла конфигурации, содержащий hello, следующая Предустановка json. 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. Загрузка файлов JSON hello выходных данных. 

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

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Связанные ссылки
[Общие сведения об аналитике служб мультимедиа Azure](media-services-analytics-overview.md)

[Демонстрационные материалы для медиааналитики Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

