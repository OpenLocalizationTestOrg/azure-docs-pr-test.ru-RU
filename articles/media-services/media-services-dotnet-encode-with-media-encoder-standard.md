---
title: "aaaEncode актива стандарту Media Encoder с помощью .NET | Документы Microsoft"
description: "В этом разделе показано, как .NET toouse tooencode ресурс с помощью Media Encoder Стандартная."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a>Кодирование ресурса-контейнера с помощью Media Encoder Standard и .NET
Задания кодирования — это один из самых распространенных операций обработки hello в службах мультимедиа. Создать кодирования файлов мультимедиа tooconvert заданий из одной кодировки tooanother. При кодировании можно использовать hello встроенных Media Encoder служб мультимедиа. Также можно использовать кодировщик, предоставленный партнером Media Services; сторонние кодировщики можно найти hello Azure Marketplace. 

В этом разделе показано, как toouse .NET tooencode активов с Media Encoder Standard (MES). Стандартный кодировщик мультимедиа настраивается с помощью одного из описанных предустановки кодировщика hello [здесь](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

Рекомендуется tooalways кодируют исходные файлы в набор MP4 с адаптивной скоростью, а затем преобразовать hello набор toohello нужный формат с помощью hello [динамической упаковки](media-services-dynamic-packaging-overview.md). 

Если выходящий ресурс зашифрован в хранилище, необходимо настроить политику доставки ресурсов. Дополнительные сведения см. в статье [Настройка политик доставки ресурсов-контейнеров](media-services-dotnet-configure-asset-delivery-policy.md).

> [!NOTE]
> MES создает выходной файл с именем, содержащим hello первые 32 символа hello имя входного файла. Имя Hello основано на, заданных в файле предустановки hello. Например, "FileName": "{Basename}_{Index}{Extension}". {Базовое имя} заменяется hello первые 32 символа имени входного файла hello.
> 
> 

### <a name="mes-formats"></a>Форматы стандартного кодировщика мультимедиа
[Форматы и кодеки](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a>Предустановки стандартного кодировщика мультимедиа
Стандартный кодировщик мультимедиа настраивается с помощью одного из описанных предустановки кодировщика hello [здесь](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Входные и выходные метаданные
При кодировании входным активом (или активами), с помощью MES вы получаете выходного актива в hello успешное завершение, кодирования задач. Hello выходной актив содержит видеофайлы, аудиофайлы, эскизы, манифест, т. д., основании предустановку hello, используемого.

Hello также включает файл метаданных входного актива hello. Hello hello метаданных XML-файлу имеет hello следующий формат: < идентификатор_актива > _metadata.xml (например, 41114ad3-eb5e - 4c 57 8d 92-5354e2b7d4a4_metadata.xml), где < идентификатор_актива > — hello значение AssetId входного актива hello. Hello схем входных метаданных XML описывается [здесь](media-services-input-metadata-schema.md).

Hello также включает файл метаданных выходного актива hello. Hello hello метаданных XML-файлу имеет hello следующий формат: < имя_исходного_файла > _manifest.xml (например, BigBuckBunny_manifest.xml). Схема Hello этих метаданных выходного XML описана [здесь](media-services-output-metadata-schema.md).

Следует tooexamine либо hello двух файлов метаданных можно создать указатель SAS и загрузки hello файл tooyour локального компьютера. Пример как toocreate указателя SAS и загрузки файла с помощью hello служб мультимедиа можно найти расширения SDK .NET.

## <a name="download-sample"></a>Скачивание образца
Можно получить и выполнить пример, в котором показано, как tooencode с MES из [здесь](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="net-sample-code"></a>Пример кода .NET

Следующий пример кода Hello использует hello tooperform Media Services .NET SDK следующие задачи:

* Создание задания кодирования.
* Получите кодировщик Media Encoder Стандартная toohello ссылки.
* Укажите toouse hello [адаптивной потоковой передачи](media-services-autogen-bitrate-ladder-with-mes.md) предустановки. 
* Добавьте одно задание toohello задач кодирования. 
* Укажите входной hello toobe активов кодировке.
* Создание выходного актива, который будет содержать активов hello в кодировке.
* Добавьте событие обработчика toocheck hello ход выполнения задания.
* Отправка задания hello.

#### <a name="create-and-configure-a-visual-studio-project"></a>Создание и настройка проекта Visual Studio

Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Пример 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    // Get an uploaded asset.
                    var asset = _context.Assets.FirstOrDefault();

                    // Encode and generate hello output using hello "Adaptive Streaming" preset.
                    EncodeToAdaptiveBitrateMP4Set(asset);

                    Console.ReadLine();
                }

                static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Media Encoder Standard Job");
                    // Get a media processor reference, and pass tooit hello name of hello 
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
                        processor,
                        "Adaptive Streaming",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(asset);
                    // Add an output asset toocontain hello results of hello job. 
                    // This output is specified as AssetCreationOptions.None, which 
                    // means hello output asset is not encrypted. 
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
                    job.Submit();
                    job.GetExecutionProgressTask(CancellationToken.None).Wait();

                    return job.OutputMediaAssets[0];
                }

                private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
                {
                    Console.WriteLine("Job state changed event:");
                    Console.WriteLine("  Previous state: " + e.PreviousState);
                    Console.WriteLine("  Current state: " + e.CurrentState);
                    switch (e.CurrentState)
                    {
                        case JobState.Finished:
                            Console.WriteLine();
                            Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
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
                            break;
                        default:
                            break;
                    }
                }

                private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
                {
                    var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                    ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                    if (processor == null)
                        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                    return processor;
                }
            }
        }

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Дальнейшие действия
[Как toogenerate эскиз в .NET Framework с помощью Media Encoder Стандартная](media-services-dotnet-generate-thumbnail-with-mes.md)
[Обзор кодирования службами мультимедиа](media-services-encode-asset.md)

