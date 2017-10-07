---
title: "aaaDetect начертания и эмоций с медиа-аналитика Azure | Документы Microsoft"
description: "В этом разделе показано, как грани toodetect и эмоций с медиа-аналитика Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a>Обнаружение лиц и определение эмоций с помощью медиа-аналитики Azure
## <a name="overview"></a>Обзор
Hello **детектор лицевой стороны Azure Media** обработчик мультимедиа (MP) позволяет toocount, перемещений отслеживания и даже участие аудитории датчика и реакция через выражения лица. В этой службе реализованы две функции: 

* **Обнаружение лиц**
  
    Функция обнаружения лиц используется для обнаружения и отслеживания человеческих лиц на видео. Несколько фрагментов могут быть обнаружены и впоследствии отслеживаются перемещения, с hello времени и расположение метаданных, возвращаемых в файле JSON. Во время отслеживания, он попытается toogive согласованного toohello идентификатор же сталкиваются при hello пользователь перемещается на экране, даже в том случае, если они являются действия или кратко оставьте hello кадра.
  
  > [!NOTE]
  > Эта служба не поддерживает распознавание лиц. Лицо, которое отправляется hello кадра или становится действия для слишком долго получает новый идентификатор при подключении.
  > 
  > 
* **Определение эмоций**
  
    Обнаружение эмоций — это необязательный компонент hello обработчик мультимедиа обнаружения начертания, возвращающий анализа на несколько атрибутов этому из hello гарнитуры обнаружено, включая счастье, sadness, опасаясь, anger и многое другое. 

Hello **детектор лицевой стороны Azure Media** MP в настоящее время находится в предварительной версии.

В этом разделе приведены подробные сведения о **детектор лицевой стороны Azure Media** и показано, как toouse с помощью пакета SDK служб мультимедиа для .NET.

## <a name="face-detector-input-files"></a>Входные файлы детектора лиц
Видеофайлы. В настоящее время поддерживаются следующие форматы hello: MP4, MOV и WMV.

## <a name="face-detector-output-files"></a>Выходные файлы детектора лиц
API обнаружения и отслеживания начертания Hello предоставляет высокой точности начертания расположение обнаружения и отслеживания для определения вверх too64 человека фрагменты в видео. Распознавания фронтальных видов лица предоставляют hello лучшей при боковые и небольшие фрагменты (меньше или равно too24x24 пикселей) не может быть точным.

Hello обнаружены и отслеживаемых гарнитуры возвращаются с координатами (left, top, ширину и высоту), указывающий положение hello граней в hello изображения в пикселях, а также начертания идентификатор число, указывающее, hello, отдельные отслеживание. Идентификаторы начертания, имеют ошибкам tooreset обстоятельствах при утере или перекрываются в кадре hello фронтального лица hello в результате некоторых пользователей, назначении нескольких идентификаторов.

## <a id="output_elements"></a>Элементы hello выходных данных JSON-файла

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

Детектор начертания использует методы фрагментации (где hello метаданные могут быть классифицированы фрагментами синхронизированного и можно загрузить только необходимые) и сегментации (где hello события сгруппированы в случае, если они получают слишком большое). Несколько простых вычислений поможет вам преобразовывать данные hello. Например, если событие началось в 6 300 (тактов) с шкалой времени 2 997 (тактов в секунду) и частотой кадров 29,97 (кадров в секунду), то:

* начало/шкала времени = 2,1 секунды
* Время (с) x частота кадров = 63 кадра

## <a name="face-detection-input-and-output-example"></a>Пример входных и выходных данных обнаружения лиц
### <a name="input-video"></a>Входные видеоданные
[Входные видеоданные](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Конфигурация задачи (предустановка)
При создании задачи с помощью **Azure Media Face Detector**необходимо указать предустановку конфигурации. Привет, следующая Предустановка конфигурации необходимо только для обнаружения лицевой стороны.

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a>Описания атрибутов
| Имя атрибута | Описание |
| --- | --- |
| Режим |Fast: быстрая скорость обработки, но с меньшей точностью (по умолчанию).|

### <a name="json-output"></a>Выходные данные JSON
Следующий пример выходных данных JSON Hello был усечен.

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a>Пример входных и выходных данных определения эмоций
### <a name="input-video"></a>Входные видеоданные
[Входные видеоданные](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Конфигурация задачи (предустановка)
При создании задачи с помощью **Azure Media Face Detector**необходимо указать предустановку конфигурации. следующие конфигурации Предустановка Hello указывает toocreate JSON на основании обнаружения эмоций hello.

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a>Описания атрибутов
| Имя атрибута | Описание |
| --- | --- |
| Режим |Faces: только обнаружение лиц.<br/>PerFaceEmotion: эмоции возвращаются отдельно для каждого обнаружения лиц.<br/>AggregateEmotion. Возвращаются средние значения эмоций для всех лиц в кадре. |
| AggregateEmotionWindowMs |Используется, если выбран режим AggregateEmotion. Указывает длину hello видео используется tooproduce каждого итоговый результат, в миллисекундах. |
| AggregateEmotionIntervalMs |Используется, если выбран режим AggregateEmotion. Указывает агрегат tooproduce какие частоты приводит. |

#### <a name="aggregate-defaults"></a>Совокупные значения по умолчанию
Ниже, рекомендуется использовать значения статистической оконной hello и параметры интервала. Значение AggregateEmotionWindowMs должно быть больше значения AggregateEmotionIntervalMs.

|| Значения по умолчанию | Минимальные | Максимальные |
|--- | --- | --- | --- |
| AggregateEmotionWindowMs |0,5 |2 |0,25|
| AggregateEmotionIntervalMs |0,5 |1 |0,25|

### <a name="json-output"></a>Выходные данные JSON
Выходные данные JSON для совокупных эмоций (сокращенные).

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a>Ограничения
* формат ввода видео Hello поддерживается включают MP4, MOV и WMV.
* размер диапазона Hello выявляемых лицевой стороны — too2048x2048 24 x 24 пикселя. не будет обнаружен гарнитуры Hello за пределами этого диапазона.
* Для каждого видео hello гарнитуры возвращается не более 64.
* Некоторые лица могут не обнаруживаться из-за проблем tootechnical; Например очень больших углы лицевой стороны (head позы) и больших перекрытия. Фрагменты фронтальных и около фронтальных имеют hello наилучших результатов.

## <a name="net-sample-code"></a>Пример кода .NET

Hello следующей программе показано как:

1. Создание актива и отправка файла мультимедиа в актив hello.
2. Создание задания с задачу обнаружения лиц на основе файла конфигурации, содержащий hello, следующая Предустановка json. 
   
        {
            "version": "1.0"
        }
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

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

[Демонстрационные материалы для медиааналитики Azure](http://amslabs.azurewebsites.net/demos/Analytics.html)

