---
title: "Дополнительное кодирование с помощью расширенного рабочего процесса кодировщика мультимедиа | Документация Майкрософт"
description: "Узнайте, как выполнять дополнительное кодирование с помощью рабочего процесса Premium кодировщика мультимедиа. Примеры кода написаны на языке C# и используют пакет SDK служб мультимедиа для .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: 0cb7c7c33866ea078ab597e71cb56a601929f8f5
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a>Дополнительное кодирование с помощью рабочего процесса Premium кодировщика мультимедиа
> [!NOTE]
> Обработчик мультимедиа расширенного рабочего процесса кодировщика мультимедиа, рассматриваемые в данной статье не доступные в Китае.
>
>

Вопросы о кодировщике Premium направляйте по адресу mepd@microsoft.com.

## <a name="overview"></a>Обзор
Службы мультимедиа Microsoft Azure представляют обработчик мультимедиа **Media Encoder Premium Workflow**. Данный обработчик предоставляет расширенные возможности кодирования для рабочих процессов уровня premium по требованию.

В следующих разделах приводятся подробные сведения o **расширенном рабочем процессе кодировщика мультимедиа**:

* [Форматы, которые поддерживаются рабочим процессом Premium кодировщика мультимедиа](media-services-premium-workflow-encoder-formats.md) — описание файла форматирования и поддерживаемые кодеки **рабочего процесса Premium кодировщика мультимедиа**.
* [Обзор и сравнение кодировщика мультимедиа Azure по требованию](media-services-encode-asset.md) сравнивает кодирования возможности **расширенного рабочего процесса кодировщика мультимедиа** и **Media Encoder Standard**.

В этой статье показано, как для кодирования с **расширенного рабочего процесса кодировщика мультимедиа** с использованием .NET.

Задачи кодирования для обработчика мультимедиа **Media Encoder Premium Workflow** требуют наличия отдельного файла конфигурации, который называется файлом Workflow). Эти файл имеют расширение .workflow и создаются с помощью [Конструктора рабочих процессов](media-services-workflow-designer.md) .

Также можно получить файлы рабочего процесса с настройками по умолчанию [отсюда](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). Папка также содержит описание этих файлов.

Файлы рабочего процесса должны быть отправлены в учетную запись служб мультимедиа в виде ресурса, и этот ресурс нужно передать в задачу кодирования.

## <a name="create-and-configure-a-visual-studio-project"></a>Создание и настройка проекта Visual Studio

Настройте среду разработки и укажите в файле app.config сведения о подключении, как описано в статье [Разработка служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md). 

## <a name="encoding-example"></a>Пример кодирования

В следующем примере показано, как кодировать с помощью обработчика мультимедиа **Media Encoder Premium Workflow**.

Выполняются следующие шаги.

1. Создание ресурса и отправка файла рабочего процесса.
2. Создание ресурса и отправка исходного файла мультимедиа.
3. Получение обработчика мультимедиа "Расширенный рабочий процесс кодировщика мультимедиа".
4. Создание задания и задачи.

    В большинстве случаев строка конфигурации задачи будет пуста (как в следующем примере). Существуют некоторых сложных сценариев (которых необходимо задать свойства среды выполнения динамически) в этом случае будет предоставлен для задачи кодирования XML-строку. Примеры таких сценариев: создание наложения, параллельное или последовательное совмещение мультимедиа, субтитры.
5. Добавление двух входных ресурсов в задачу.

    1. Первый – ресурс рабочего процесса.
    2. Второй – ресурс видео.

    >[!NOTE]
    >Ресурс рабочего процесса необходимо добавить в задачу до того, как в нее будет добавлен ресурс мультимедиа.
   Строка конфигурации для этой задачи должна быть пуста.
   
6. Отправка задания кодирования.

```
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
            ConfigurationManager.AppSettings["AMSAADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["AMSRESTAPIEndpoint"];
        private static readonly string _AMSClientId =
            ConfigurationManager.AppSettings["AMSClientId"];
        private static readonly string _AMSClientSecret =
            ConfigurationManager.AppSettings["AMSClientSecret"];

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

            AzureAdTokenCredentials tokenCredentials =
                new AzureAdTokenCredentials(_AADTenantDomain,
                    new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                    AzureEnvironments.AzureCloudEnvironment);

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
            // Get a media processor reference, and pass to it the name of the
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                processor,
                "",
                TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(workflow);
            task.InputAssets.Add(video); // we add one asset
                                         // Add an output asset to contain the results of the job.
                                         // This output is specified as AssetCreationOptions.None, which
                                         // means the output asset is not encrypted.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Use the following event handler to check job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch the job.
            job.Submit();

            // Check job execution and wait for job to finish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();

            // If job state is Error the event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                throw new Exception("\nExiting method due to job error.");
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
```

Вопросы о кодировщике Premium направляйте по адресу mepd@microsoft.com.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
