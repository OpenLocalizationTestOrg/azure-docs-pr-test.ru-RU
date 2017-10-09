---
title: "aaaDigitize текста с помощью Azure Media Analytics OCR | Документы Microsoft"
description: "Аналитика OCR Azure Media (распознавания) позволяет tooconvert текстовое содержимое в файлы видео в цифровой текст редактируемый, с возможностью поиска.  Это позволяет tooautomate извлечение метаданных может применяться hello из hello видеосигнала мультимедиа."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a>Используйте Azure медиа-аналитика tooconvert текстовое содержимое в файлы видео в цифровой текст
## <a name="overview"></a>Обзор
Если нужно tooextract текстового содержимого из видеофайлы и создание цифрового текста для редактирования, с возможностью поиска, следует использовать Azure Media Analytics OCR (распознавание символов). Этот обработчик мультимедиа Azure обнаруживает текстовое содержимое в видеофайлах и создает текстовые файлы, готовые к использованию. OCR позволяет вам tooautomate hello извлечение значимых метаданных из hello видеосигнала мультимедиа.

При использовании в сочетании с помощью поисковой системы, можно легко проиндексировать мультимедиа, текст и повышения возможности обнаружения hello содержимого. Это очень полезно, если видео содержит много текста, например, если это видеозапись или снимки экрана какой-либо презентации в режиме слайд-шоу. Hello обработчика мультимедиа Azure OCR оптимизирован для цифровых текста.

Hello **Azure Media OCR** обработчик мультимедиа в данный момент находится в предварительной версии.

В этом разделе приведены подробные сведения о **Azure Media OCR** и показано, как toouse с помощью пакета SDK служб мультимедиа для .NET. Дополнительные сведения и примеры см. в [этом блоге](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).

## <a name="ocr-input-files"></a>Входные файлы OCR
Видеофайлы. В настоящее время поддерживаются следующие форматы hello: MP4, MOV и WMV.

## <a name="task-configuration"></a>Конфигурация задачи
Конфигурация задачи (предустановка). При создании задачи с помощью **Azure Media OCR** необходимо указать предустановку конфигурации, используя JSON- или XML-файл. 

>[!NOTE]
>механизм распознавания текста Hello занимает область изображения с минимальным 40 пикселей toomaximum 32000 как допустимые входные данные в обоих высоты и ширины.
>

### <a name="attribute-descriptions"></a>Описания атрибутов
| Имя атрибута | Описание |
| --- | --- |
|AdvancedOutput| Если задать AdvancedOutput tootrue hello JSON выход будет содержать позиционные данные для каждого отдельного слова (в дополнение toophrases и регионы). Если вы не хотите toosee эти сведения, установите флаг toofalse hello. значение по умолчанию Hello имеет значение false. Дополнительную информацию см. в [этом блоге](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).|
| Язык |(необязательно) описание языка hello какие toolook текста. Одно из следующих hello: автообнаружение (по умолчанию), арабский, китайского, вместе, чешский датский, голландский, английский, финский, французский, немецкий, греческий, венгерский, итальянский, японский, корейский, норвежский, польский, португальский, румынский, русский, SerbianCyrillic, SerbianLatin, словацкий, испанский, шведский, турецкий. |
| TextOrientation |(необязательно) описание hello ориентацию текста для какой toolook.  «Левый» означает, что hello вверху все буквы указывают указатели по направлению к левому hello.  По умолчанию текст (как, например, в книге) имеет ориентацию "Up", то есть буквы направлены вверх.  Одно из следующих hello: автообнаружение (по умолчанию), до, правой, вниз, влево. |
| TimeInterval |(необязательно) описание hello частоту выборки.  Значение по умолчанию — каждые полсекунды.<br/>Формат JSON — ЧЧ:мм:сс.ССС (по умолчанию — 00:00:00.500)<br/>Формат XML: минимальная длительность W3C XSD (по умолчанию — PT0.5). |
| DetectRegions |(необязательно) Массив объектов DetectRegion указания областей в пределах кадра видео hello в какой toodetect текст.<br/>Объект DetectRegion состоит из hello следующие четыре целочисленных значений:<br/>Left — пикселей от левого поля hello<br/>Начало — пикселей верхнее hello<br/>Ширина: ширина области hello в пикселях<br/>Высота: высота области hello в пикселях |

#### <a name="json-preset-example"></a>Пример предустановки JSON

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a>Пример предустановки XML
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a>Выходные файлы OCR
выходные данные Hello обработчик мультимедиа OCR hello является файлом JSON.

### <a name="elements-of-hello-output-json-file"></a>Элементы hello выходных данных JSON-файла
Выход видео OCR Hello обеспечивает время сегментированных данных на hello символы, входящие в видео.  Можно использовать атрибуты, такие как язык или ориентацией toohone в точно hello слов, которые нужно в анализ. 

Hello выходные данные содержат hello следующие атрибуты:

| Элемент | Описание |
| --- | --- |
| Шкала времени |«тактах» в секунду hello видео |
| Offset |Смещение времени для отметки времени. В API видео версии 1.0 это значение всегда равно 0. |
| Framerate |Кадров в секунду hello видео |
| width |Ширина hello видео в пикселях |
| height |Высота изображения в пикселях hello |
| Fragments |Массив из фрагментов видео, в которой hello фрагментирован метаданных на основе времени |
| start |Время начала фрагмента в тактах |
| длительность |Продолжительность фрагмента в тактах |
| interval |Интервал каждого события в пределах заданного фрагмента hello |
| events |Массив, содержащий области |
| region |Объект, представляющий обнаруженные слова или фразы |
| Язык |язык обнаружена в области текста hello |
| orientation |ориентацию текста hello обнаружена в области |
| lines |Массив строк текста, обнаруженного в пределах области |
| text |Фактический текст Hello |

### <a name="json-output-example"></a>Пример выходных данных JSON
Hello следующий пример выходных данных содержит общие сведения видео hello и несколько фрагментов видео. В каждый фрагмент видео в нем каждого региона, в которой обнаружен OCR MP с языком hello и его ориентацию текста. Hello область также содержит каждой строки слова в этом регионе с текстом hello строки, положение строки hello и сведения каждого word (содержимого word, положение и достоверности) в этой строке. Hello ниже приведен пример и переводе некоторые встроенные комментарии.

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a>Пример кода .NET

Hello следующей программе показано как:

1. Создание актива и отправка файла мультимедиа в актив hello.
2. Создание задания с помощью файла конфигурации или файла предустановки OCR.
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

    namespace OCR
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

