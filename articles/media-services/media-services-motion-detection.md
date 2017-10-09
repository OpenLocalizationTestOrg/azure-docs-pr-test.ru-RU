---
title: "aaaDetect движения с медиа-аналитика Azure | Документы Microsoft"
description: "Здравствуйте Детектор движения мультимедиа Azure media процессора (MP) позволяет вам tooefficiently указывают разделы интерес в видео, в противном случае длинные и процедура."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a>Обнаружение движения с помощью медиа-аналитики Azure
## <a name="overview"></a>Обзор
Hello **Детектор движения Azure Media** media процессора (MP) позволяет вам tooefficiently указывают разделы интерес в видео, в противном случае длинные и процедура. Обнаружение движения может использоваться с камеры статических материал tooidentify разделами видео hello которой происходит движения. Он создает JSON-файл, содержащий метаданные с метки времени и hello, ограничивающий область, где произошло событие hello.

Ориентирован видео безопасности веб-каналы, эта технология является движения может toocategorize в соответствующие события и ложных положительных результатов, такие как изменение освещения и тени. Это позволяет toogenerate оповещений системы безопасности из каналов камеры без личного веб-узла с событиями бесконечные значения, не может tooextract моменты процент от видео с очень длинными наблюдения.

Hello **Детектор движения Azure Media** MP в настоящее время находится в предварительной версии.

В этом разделе приведены подробные сведения о **Детектор движения Azure Media** и показано, как toouse с помощью пакета SDK служб мультимедиа для .NET

## <a name="motion-detector-input-files"></a>Входные файлы детектора движения
Видеофайлы. В настоящее время поддерживаются следующие форматы hello: MP4, MOV и WMV.

## <a name="task-configuration-preset"></a>Конфигурация задачи (предустановка)
При создании задачи с использованием **Azure Media Motion Detector**необходимо задать предустановку конфигурации. 

### <a name="parameters"></a>Параметры
Можно использовать следующие параметры hello.

| Имя | Параметры | Описание | значение по умолчанию |
| --- | --- | --- | --- |
| sensitivityLevel |Строка: low, medium, high |Задает уровень чувствительности hello в какой движения сообщается. Измените эту сумму tooadjust ложных положительных результатов. |medium |
| frameSamplingValue |Положительное целое число |Задает частоту hello, в которой работает алгоритм. 1 соответствует каждому кадру, 2 — каждому второму кадру и т. д. |1 |
| detectLightChange |Логическое значение: true или false |Задает признак светлой изменения отображаются в результатах hello |False |
| mergeTimeThreshold |xs-time: "ЧЧ:ММ:СС", <br/>например 00:00:03 |Указывает hello интервал времени между событиями движения, где объединяются и возвращаются с 1 2 события. |00:00:00 |
| detectionZones |Массив зон обнаружения: <br/>зона обнаружения представляет собой массив из трех или более точек 3;<br/>-Точка — x и y из 0 too1 координат. |Описание обнаружения многоугольных зон toobe используется список hello.<br/>Результаты будут считаться с зонами hello идентификатора, первый из них выполняется «id» hello: 0 |Одной зоне, который охватывает всю рамку hello. |

### <a name="json-example"></a>Пример JSON-файла
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a>Выходные файлы детектора движения
Обнаружение движения задания будет возвращать JSON-файла в hello выходной актив, который описывает предупреждения движения hello и их категорий, в пределах hello видео. Hello файл будет содержать сведения о времени и длительности перемещений в видео hello hello.

API обнаружения движения Hello предоставляет индикаторы после движущихся объектов в основных фоновое видео (например наблюдения видео). Hello Детектор движения является обученной tooreduce ложные сигналы, такие как изменение тени и освещение. Текущие ограничения алгоритмов hello включают ночь концепции видео, прозрачные объекты и небольших объектов.

### <a id="output_elements"></a>Элементы hello выходных данных JSON-файла
> [!NOTE]
> В последнем выпуске hello формат вывода JSON hello изменилась и может представлять является критическим изменением для некоторых клиентов.
> 
> 

Hello следующей таблице описываются элементы hello выходных данных JSON-файла.

| Элемент | Описание |
| --- | --- |
| Version (версия) |Это относится toohello версии hello API видео. Текущая версия Hello — 2. |
| Шкала времени |«Тактах» в секунду hello видео. |
| Offset |Смещение времени Hello для отметки времени в «тактах». В API видео версии 1.0 это значение всегда равно 0. В будущих поддерживаемых сценариях это значение может измениться. |
| Framerate |Кадров в секунду hello видео. |
| Width, Height |Ссылается toohello ширину и высоту изображения в пикселях hello. |
| Начало |Hello запустите метки времени «тикает». |
| Duration |Длина Hello события hello в «тактах». |
| Интервал |Интервал приветствия каждая запись в события hello в «тактах». |
| События |Каждый фрагмент событие содержит движения hello обнаружен в течение этого промежутка времени. |
| Тип |В текущей версии hello всегда является "2" для универсального движения. Эта метка предоставляет API-интерфейсы видео hello гибкость toocategorize движения в будущих версиях. |
| RegionID |Как упоминалось выше, в этой версии всегда будет использоваться значение 0. Эта метка дает движения toofind API видео hello гибкость в различных регионах в будущих версиях. |
| регионы |Указывает область toohello видео, где важна движения. <br/><br/>-«id» представляет hello области — в этой версии имеется только один, идентификатор 0. <br/>-«тип» представляет фигуры hello области hello важна для перемещения. Сейчас поддерживаются прямоугольник и многоугольник.<br/> Если вы указали «прямоугольник», hello области имеет измерений X, Y, ширину и высоту. Hello X и Y координаты представляют координатами x и y верхний левый hello области hello в нормализованной масштабом too1.0 0,0. Hello ширины и высоты представляют Привет размер области hello в масштабе нормализованный 0,0 too1.0. В текущей версии hello X, Y, ширина и высота всегда фиксируются в 0, 0 и 1, 1. <br/>Если вы указали «многоугольник», область hello имеет измерений в пунктах. <br/> |
| Fragments |метаданные Hello фрагментирован вверх в разных сегментах, называемые фрагментами. Каждый фрагмент имеет начало, длительность, номер интервала и события. Фрагмент без событий означает, что с момента начала и в течение продолжительности события движение обнаружено не было. |
| Квадратные скобки [] |Каждая скобка представляет один интервал в событии hello. Пустые скобки для этого интервала означают, что движение не обнаружено. |
| locations |Эту новую запись в списке событий перечислены hello расположение, где произошло hello движения. Это более точным определением, чем зоны обнаружения hello. |

Hello ниже приведен пример выходных данных JSON

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a>Ограничения
* формат ввода видео Hello поддерживается включают MP4, MOV и WMV.
* Функция обнаружения движения оптимизирована для видео с неподвижными фонами. алгоритм Hello основное внимание уделяется уменьшение ложные сигналы, такие как изменения освещения и тени.
* Некоторые движения могут не обнаруживаться из-за проблем tootechnical; Например ночь концепции видео, прозрачные объекты и небольшие объекты.

## <a name="net-sample-code"></a>Пример кода .NET

Hello следующей программе показано как:

1. Создание актива и отправка файла мультимедиа в актив hello.
2. Создание задания с задачу обнаружения движения видео на основе файла конфигурации, содержащий hello, следующая Предустановка json. 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
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

    namespace VideoMotionDetection
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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
[Блог по инструменту Motion Detector служб Azure Media Services](https://azure.microsoft.com/blog/motion-detector-update/)

[Общие сведения об аналитике служб мультимедиа Azure](media-services-analytics-overview.md)

[Демонстрационные материалы для медиааналитики Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

