---
title: "aaaAdvanced кодирование с помощью расширенного рабочего процесса кодировщика мультимедиа | Документы Microsoft"
description: "Узнайте, как tooencode с расширенного рабочего процесса кодировщика мультимедиа. Примеры кода на языке C# и используйте hello пакета SDK служб мультимедиа для .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a>Дополнительное кодирование с помощью рабочего процесса Premium кодировщика мультимедиа
> [!NOTE]
> Обработчик мультимедиа расширенного рабочего процесса кодировщика мультимедиа, рассматриваемый в этом разделе, недоступен в Китае.
>
>

Вопросы о кодировщике Premium направляйте по адресу mepd@microsoft.com.

## <a name="overview"></a>Обзор
Службы мультимедиа Microsoft Azure введение hello **расширенного рабочего процесса кодировщика мультимедиа** обработчика мультимедиа. Данный обработчик предоставляет расширенные возможности кодирования для рабочих процессов уровня premium по требованию.

Hello ниже описаны сведения, связанные с слишком**расширенного рабочего процесса кодировщика мультимедиа**:

* [Форматирует поддерживаемые с hello расширенного рабочего процесса кодировщика мультимедиа](media-services-premium-workflow-encoder-formats.md) — описание hello форматы и кодеки, поддерживаемые **расширенного рабочего процесса кодировщика мультимедиа**.
* [Обзор и сравнение Azure по запросу мультимедиа кодировщики](media-services-encode-asset.md) сравнивает hello кодирования возможности **расширенного рабочего процесса кодировщика мультимедиа** и **Media Encoder Standard**.

В этом разделе показано, как tooencode с **расширенного рабочего процесса кодировщика мультимедиа** с использованием .NET.

Кодирование задачи для hello **расширенного рабочего процесса кодировщика мультимедиа** требуется отдельный файл конфигурации, называемый файлом рабочего процесса. Эти файлы имеют расширение цифры и создаются с помощью hello [конструктора рабочих процессов](media-services-workflow-designer.md) средства.

Можно также получить по умолчанию hello файлы рабочего процесса [здесь](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). Hello папка также содержит описание hello этих файлов.

файлы рабочего процесса Hello необходима учетная запись служб мультимедиа tooyour toobe загружен как основное средство и необходимо передать этот ресурс toohello кодирование задачи.

## <a name="create-and-configure-a-visual-studio-project"></a>Создание и настройка проекта Visual Studio

Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md). 

## <a name="encoding-example"></a>Пример кодирования

Hello следующем примере показано, как tooencode с **расширенного рабочего процесса кодировщика мультимедиа**.

выполняются следующие шаги Hello.

1. Создание ресурса и отправка файла рабочего процесса.
2. Создание ресурса и отправка исходного файла мультимедиа.
3. Получите обработчик мультимедиа «Media расширенного рабочего процесса кодировщика» hello.
4. Создание задания и задачи.

    В большинстве случаев строка hello конфигурации для задачи «hello» пуста (например, в следующий пример hello). Существуют некоторых сложных сценариев (которые требуют динамически свойствам среды выполнения tootooset) в этом случае будет предоставлен кодирования задачу toohello строку XML. Примеры таких сценариев: создание наложения, параллельное или последовательное совмещение мультимедиа, субтитры.
5. Добавьте две задачи toohello входные активы.

    1. 1-го — активов hello рабочего процесса.
    2. 2 — видео активов hello.

    >[!NOTE]
    >Hello активов рабочего процесса должны быть добавлены toohello задач перед hello актив мультимедиа.
   Строка Hello конфигурации для этой задачи должно быть пустым.
   
6. Отправка задания кодирования hello.

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
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

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
                    }

                    return job.OutputMediaAssets[0];
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

Вопросы о кодировщике Premium направляйте по адресу mepd@microsoft.com.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
