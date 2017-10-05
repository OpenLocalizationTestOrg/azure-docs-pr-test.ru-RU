---
title: "Настройка предустановок Media Encoder Standard | Документация Майкрософт"
description: "В этом разделе показано, как выполнять расширенные задачи кодирования, настраивая предустановки задач Media Encoder Standard. В этом разделе показано, как использовать пакет SDK служб мультимедиа для .NET для создания задания и задачи кодирования. В нем также показано, как предоставить пользовательские предустановки для задания кодирования."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec95392f-d34a-4c22-a6df-5274eaac445b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: b4d25f07349043da8cb745930fde3371c98f9960
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="customizing-media-encoder-standard-presets"></a><span data-ttu-id="73a8e-105">Настройка предустановок Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="73a8e-105">Customizing Media Encoder Standard presets</span></span>

## <a name="overview"></a><span data-ttu-id="73a8e-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="73a8e-106">Overview</span></span>

<span data-ttu-id="73a8e-107">В этом разделе показано, как выполнять расширенные задачи кодирования с помощью Media Encoder Standard (MES) и пользовательской предустановки.</span><span class="sxs-lookup"><span data-stu-id="73a8e-107">This topic shows how to perform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span></span> <span data-ttu-id="73a8e-108">В этом разделе с помощью .NET создаются задача кодирования и задание, которое выполняет эту задачу.</span><span class="sxs-lookup"><span data-stu-id="73a8e-108">The topic uses .NET to create an encoding task and a job that executes this task.</span></span>  

<span data-ttu-id="73a8e-109">В данном разделе показано, как настроить предустановку. Для примера взята предустановка [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md), в которой уменьшается количество уровней.</span><span class="sxs-lookup"><span data-stu-id="73a8e-109">In this topic you will see how to customize a preset by taking the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing the number of layers.</span></span> <span data-ttu-id="73a8e-110">В разделе [Настройка предустановок Media Encoder Standard](media-services-advanced-encoding-with-mes.md) показаны пользовательские предустановки, которые могут использоваться для выполнения расширенных задач кодирования.</span><span class="sxs-lookup"><span data-stu-id="73a8e-110">The [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) topic demonstrates custom presets that can be used to perform advanced encoding tasks.</span></span>

## <span data-ttu-id="73a8e-111"><a id="customizing_presets"></a> Настройка предустановки MES</span><span class="sxs-lookup"><span data-stu-id="73a8e-111"><a id="customizing_presets"></a> Customizing a MES preset</span></span>

### <a name="original-preset"></a><span data-ttu-id="73a8e-112">Первоначальная предустановка</span><span class="sxs-lookup"><span data-stu-id="73a8e-112">Original preset</span></span>

<span data-ttu-id="73a8e-113">Сохраните код JSON, определенный в разделе [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md), в отдельный JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="73a8e-113">Save the JSON defined in the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) topic in some file with .json extension.</span></span> <span data-ttu-id="73a8e-114">Например, **CustomPreset_JSON.json**.</span><span class="sxs-lookup"><span data-stu-id="73a8e-114">For example, **CustomPreset_JSON.json**.</span></span>

### <a name="customized-preset"></a><span data-ttu-id="73a8e-115">Настроенная предустановка</span><span class="sxs-lookup"><span data-stu-id="73a8e-115">Customized preset</span></span>

<span data-ttu-id="73a8e-116">Откройте файл **CustomPreset_JSON.json** и удалите первые три слоя из **H264Layers**, чтобы файл выглядел, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="73a8e-116">Open the **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span></span>

    
    {  
      "Version": 1.0,  
      "Codecs": [  
        {  
          "KeyFrameInterval": "00:00:02",  
          "H264Layers": [  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 1000,  
              "MaxBitrate": 1000,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 650,  
              "MaxBitrate": 650,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 400,  
              "MaxBitrate": 400,  
              "BufferWindow": "00:00:05",  
              "Width": 320,  
              "Height": 180,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            }  
          ],  
          "Type": "H264Video"  
        },  
        {  
          "Profile": "AACLC",  
          "Channels": 2,  
          "SamplingRate": 48000,  
          "Bitrate": 128,  
          "Type": "AACAudio"  
        }  
      ],  
      "Outputs": [  
        {  
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",  
          "Format": {  
            "Type": "MP4Format"  
          }  
        }  
      ]  
    }  
    

## <span data-ttu-id="73a8e-117"><a id="encoding_with_dotnet"></a>Кодирование с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="73a8e-117"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="73a8e-118">В следующем примере кода пакет SDK служб мультимедиа используется для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="73a8e-118">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="73a8e-119">Создание задания кодирования.</span><span class="sxs-lookup"><span data-stu-id="73a8e-119">Create an encoding job.</span></span>
- <span data-ttu-id="73a8e-120">Получение ссылки на стандартный кодировщик мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="73a8e-120">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="73a8e-121">Загрузите пользовательскую предустановку JSON, созданную в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="73a8e-121">Load the custom JSON preset that you created in the previous section.</span></span> 
  
        // Load the JSON from the local file.
        string configuration = File.ReadAllText(fileName);  

- <span data-ttu-id="73a8e-122">Добавление задачи кодирования в задание.</span><span class="sxs-lookup"><span data-stu-id="73a8e-122">Add an encoding task to the job.</span></span> 
- <span data-ttu-id="73a8e-123">Указание входного ресурса-контейнера для кодирования.</span><span class="sxs-lookup"><span data-stu-id="73a8e-123">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="73a8e-124">Создание выходного ресурса-контейнера, который будет содержать закодированный ресурс-контейнер.</span><span class="sxs-lookup"><span data-stu-id="73a8e-124">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="73a8e-125">Добавление обработчика событий для проверки хода выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="73a8e-125">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="73a8e-126">Отправка задания.</span><span class="sxs-lookup"><span data-stu-id="73a8e-126">Submit the job.</span></span>
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="73a8e-127">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73a8e-127">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="73a8e-128">Настройте среду разработки и укажите в файле app.config сведения о подключении, как описано в статье [Разработка служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="73a8e-128">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="73a8e-129">Пример</span><span class="sxs-lookup"><span data-stu-id="73a8e-129">Example</span></span>   

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace CustomizeMESPresests
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

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate the output using custom presets.
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

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("CustomPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="73a8e-130">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="73a8e-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="73a8e-131">Отзывы</span><span class="sxs-lookup"><span data-stu-id="73a8e-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="73a8e-132">См. также</span><span class="sxs-lookup"><span data-stu-id="73a8e-132">See Also</span></span>
[<span data-ttu-id="73a8e-133">Обзор кодирования с помощью служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="73a8e-133">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

