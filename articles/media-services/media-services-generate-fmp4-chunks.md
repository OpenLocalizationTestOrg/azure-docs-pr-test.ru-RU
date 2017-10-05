---
title: "Создание задачи кодирования служб мультимедиа Azure, которая создает блоки fMP4 | Документация Майкрософт"
description: "В этом разделе показано, как создать задачу кодирования, которая создает блоки fMP4. При использовании этой задачи в кодировщике Media Encoder Standard или Media Encoder Premium Workflow выходной ресурс будет содержать блоки fMP4 вместо MP4-файлов (ISO)."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b7029ac5-eadd-4a2f-8111-1fc460828981
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 55dca4bcb80e8daab2b4d293a9cc85a087055110
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
#  <a name="create-an-encoding-task-that-generates-fmp4-chunks"></a><span data-ttu-id="d56a0-104">Создание задачи кодирования, создающей блоки fMP4</span><span class="sxs-lookup"><span data-stu-id="d56a0-104">Create an encoding task that generates fMP4 chunks</span></span>

## <a name="overview"></a><span data-ttu-id="d56a0-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="d56a0-105">Overview</span></span>

<span data-ttu-id="d56a0-106">В этом разделе показано, как создать задачу кодирования, которая создает фрагментированные блоки MP4 (fMP4) вместо MP4-файлов (ISO).</span><span class="sxs-lookup"><span data-stu-id="d56a0-106">This topic shows how to create an encoding task that generates fragmented MP4 (fMP4) chunks instead of ISO MP4 files.</span></span> <span data-ttu-id="d56a0-107">Чтобы создать блоки fMP4, используйте кодировщик **Media Encoder Standard** или **Media Encoder Premium Workflow** для создания задачи кодирования и укажите параметр **AssetFormatOption.AdaptiveStreaming**, как показано в приведенном фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="d56a0-107">To generate fMP4 chunks, use the **Media Encoder Standard** or **Media Encoder Premium Workflow** encoder to create an encoding task and also specify **AssetFormatOption.AdaptiveStreaming** option, as shown in this code snippet:</span></span>  
    
    task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks", 
            options: AssetCreationOptions.None, 
            formatOption: AssetFormatOption.AdaptiveStreaming);


## <span data-ttu-id="d56a0-108"><a id="encoding_with_dotnet"></a>Кодирование с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="d56a0-108"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="d56a0-109">В следующем примере кода пакет SDK служб мультимедиа используется для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="d56a0-109">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="d56a0-110">Создание задания кодирования.</span><span class="sxs-lookup"><span data-stu-id="d56a0-110">Create an encoding job.</span></span>
- <span data-ttu-id="d56a0-111">Получите ссылку на кодировщик **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="d56a0-111">Get a reference to the **Media Encoder Standard** encoder.</span></span>
- <span data-ttu-id="d56a0-112">Добавьте задачу кодирования в задание и укажите предустановку **Adaptive Streaming**.</span><span class="sxs-lookup"><span data-stu-id="d56a0-112">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="d56a0-113">Создайте выходной ресурс, который будет содержать блоки fMP4 и ISM-файл.</span><span class="sxs-lookup"><span data-stu-id="d56a0-113">Create an output asset that will contain fMP4 chunks and an .ism file.</span></span>
- <span data-ttu-id="d56a0-114">Добавление обработчика событий для проверки хода выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="d56a0-114">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="d56a0-115">Отправка задания.</span><span class="sxs-lookup"><span data-stu-id="d56a0-115">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d56a0-116">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d56a0-116">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="d56a0-117">Настройте среду разработки и укажите в файле app.config сведения о подключении, как описано в статье [Разработка служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d56a0-117">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="d56a0-118">Пример</span><span class="sxs-lookup"><span data-stu-id="d56a0-118">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreaming
    {
        class Program
        {
        // Read values from the App.config file.
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

            // Encode and generate the output using the "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }
        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job. 

            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            // It is also specified to use AssetFormatOption.AdaptiveStreaming, 
            // which means the output asset will contain fMP4 chunks.

            task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks",
            options: AssetCreationOptions.None,
            formatOption: AssetFormatOption.AdaptiveStreaming);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="d56a0-119">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d56a0-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d56a0-120">Отзывы</span><span class="sxs-lookup"><span data-stu-id="d56a0-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d56a0-121">См. также</span><span class="sxs-lookup"><span data-stu-id="d56a0-121">See Also</span></span>
[<span data-ttu-id="d56a0-122">Обзор кодирования с помощью служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d56a0-122">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

