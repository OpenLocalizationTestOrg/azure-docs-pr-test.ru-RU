---
title: "Стандартный кодировщик мультимедиа Azure tooauto aaaUse-формирования лестницу bitrate | Документы Microsoft"
description: "В этом разделе показано, как tooauto Media Encoder стандартных (MES) toouse-формирования лестницу скоростью, на основе входных разрешения hello и скоростью. Hello входной разрешения и скорости, никогда не превышено. Например если входные данные hello 720p по адресу 3 Мбит/с, выходные данные будут остаются в лучшем 720p и начнется с частотой меньше 3 Мбит/с."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a>Используйте стандартный кодировщик мультимедиа Azure tooauto-формирования лестницу скоростью

## <a name="overview"></a>Обзор

В этом разделе показано, как tooauto Media Encoder стандартных (MES) toouse-формирования лестницу скоростью (разрешение bitrate пары), на основе входных разрешения hello и скоростью. Hello автоматически созданный стиль никогда не превысит hello ввода разрешения и скорости. Например если входные данные hello 720p по адресу 3 Мбит/с, выходные данные будут остаются в лучшем 720p и начнется с частотой меньше 3 Мбит/с.

### <a name="encoding-for-streaming-only"></a>Кодирование только для потоковой передачи

Если вашей целью является tooencode источника видео только для потоковой передачи, то необходимо выполнить все использовать «Адаптивной потоковой передачи» hello стиль при создании задания кодирования. При использовании hello **адаптивной потоковой передачи** , то по умолчанию hello MES кодировщик будет интеллектуально ограничения максимального лестницу скоростью. Однако нельзя hello может toocontrol кодирование затраты, так как служба hello определяет, сколько уровней toouse и при каком разрешении. Можно просмотреть примеры слоев выходные данные, созданные MES в результате кодирования с hello **адаптивной потоковой передачи** предустановленный набор в конце hello в этом разделе. Hello выходных активов будет содержать MP4-файлов, где аудио и видео не чередуются.

### <a name="encoding-for-streaming-and-progressive-download"></a>Кодирование для потоковой передачи и прогрессивного скачивания

Если планируется tooencode источник видео для потоковой передачи и tooproduce MP4-файлов для последовательной загрузки, а затем hello «Содержимого адаптивной несколько Bitrate MP4» необходимо выполнить все конфигурации при создании задания кодирования. При использовании hello **содержимого адаптивной несколько Bitrate MP4** заданы, кодировщик MES hello применит hello же логика кодирования, как описано выше, но теперь hello выходного актива будет содержать MP4-файлов где аудио и видео с чередованием. Можно использовать один из этих MP4-файлов (например, hello высокий битрейт версия) как файл последовательную загрузку.

## <a id="encoding_with_dotnet"></a>Кодирование с помощью пакета SDK служб мультимедиа для .NET

Следующий пример кода Hello использует hello tooperform Media Services .NET SDK следующие задачи:

- Создание задания кодирования.
- Получите кодировщик Media Encoder Стандартная toohello ссылки.
- Добавить задание кодирования toohello задач и указать toouse hello **адаптивной потоковой передачи** предустановки. 
- Создание выходного актива, который будет содержать активов hello в кодировке.
- Добавьте событие обработчика toocheck hello ход выполнения задания.
- Отправка задания hello.

#### <a name="create-and-configure-a-visual-studio-project"></a>Создание и настройка проекта Visual Studio

Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Пример

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
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

## <a id="output"></a>Выходные данные

В этом разделе приведены три примера слоев выходные данные, созданные MES в результате кодирования с hello **адаптивной потоковой передачи** предустановки. 

### <a name="example-1"></a>Пример 1
При исходной высоте 1080 и частоте кадров 29,970 создается 6 слоев видео.

|Слой|Высота:|Ширина|Скорость (кбит/с)|
|---|---|---|---|
|1|1080|1920|6780|
|2|720|1280|3520|
|3|540|960|2210|
|4.|360|640|1150|
|5|270|480|720|
|6|180|320|380|

### <a name="example-2"></a>Пример 2
При исходной высоте 720 и частоте кадров 23,970 создается 5 слоев видео.

|Слой|Высота:|Ширина|Скорость (кбит/с)|
|---|---|---|---|
|1|720|1280|2940|
|2|540|960|1850|
|3|360|640|960|
|4.|270|480|600|
|5|180|320|320|

### <a name="example-3"></a>Пример 3
При исходной высоте 360 и частоте кадров 29,970 создается 3 слоя видео.

|Слой|Высота:|Ширина|Скорость (кбит/с)|
|---|---|---|---|
|1|360|640|700|
|2|270|480|440|
|3|180|320|230|
## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>См. также
[Обзор кодирования с помощью служб мультимедиа](media-services-encode-asset.md)

