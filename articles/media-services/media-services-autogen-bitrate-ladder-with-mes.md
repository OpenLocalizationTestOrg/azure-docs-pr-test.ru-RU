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
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a><span data-ttu-id="4c48d-105">Используйте стандартный кодировщик мультимедиа Azure tooauto-формирования лестницу скоростью</span><span class="sxs-lookup"><span data-stu-id="4c48d-105">Use Azure Media Encoder Standard tooauto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="4c48d-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="4c48d-106">Overview</span></span>

<span data-ttu-id="4c48d-107">В этом разделе показано, как tooauto Media Encoder стандартных (MES) toouse-формирования лестницу скоростью (разрешение bitrate пары), на основе входных разрешения hello и скоростью.</span><span class="sxs-lookup"><span data-stu-id="4c48d-107">This topic shows how toouse Media Encoder Standard (MES) tooauto-generate a bitrate ladder (bitrate-resolution pairs) based on hello input resolution and bitrate.</span></span> <span data-ttu-id="4c48d-108">Hello автоматически созданный стиль никогда не превысит hello ввода разрешения и скорости.</span><span class="sxs-lookup"><span data-stu-id="4c48d-108">hello auto-generated preset will never exceed hello input resolution and bitrate.</span></span> <span data-ttu-id="4c48d-109">Например если входные данные hello 720p по адресу 3 Мбит/с, выходные данные будут остаются в лучшем 720p и начнется с частотой меньше 3 Мбит/с.</span><span class="sxs-lookup"><span data-stu-id="4c48d-109">For example, if hello input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="4c48d-110">Кодирование только для потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="4c48d-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="4c48d-111">Если вашей целью является tooencode источника видео только для потоковой передачи, то необходимо выполнить все использовать «Адаптивной потоковой передачи» hello стиль при создании задания кодирования.</span><span class="sxs-lookup"><span data-stu-id="4c48d-111">If your intent is tooencode your source video only for streaming, then you shoud use hello "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="4c48d-112">При использовании hello **адаптивной потоковой передачи** , то по умолчанию hello MES кодировщик будет интеллектуально ограничения максимального лестницу скоростью.</span><span class="sxs-lookup"><span data-stu-id="4c48d-112">When using hello **Adaptive Streaming** preset, hello MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="4c48d-113">Однако нельзя hello может toocontrol кодирование затраты, так как служба hello определяет, сколько уровней toouse и при каком разрешении.</span><span class="sxs-lookup"><span data-stu-id="4c48d-113">However, you will not be able toocontrol hello encoding costs, since hello service determines how many layers toouse and at what resolution.</span></span> <span data-ttu-id="4c48d-114">Можно просмотреть примеры слоев выходные данные, созданные MES в результате кодирования с hello **адаптивной потоковой передачи** предустановленный набор в конце hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="4c48d-114">You can see examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset at hello end of this topic.</span></span> <span data-ttu-id="4c48d-115">Hello выходных активов будет содержать MP4-файлов, где аудио и видео не чередуются.</span><span class="sxs-lookup"><span data-stu-id="4c48d-115">hello output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="4c48d-116">Кодирование для потоковой передачи и прогрессивного скачивания</span><span class="sxs-lookup"><span data-stu-id="4c48d-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="4c48d-117">Если планируется tooencode источник видео для потоковой передачи и tooproduce MP4-файлов для последовательной загрузки, а затем hello «Содержимого адаптивной несколько Bitrate MP4» необходимо выполнить все конфигурации при создании задания кодирования.</span><span class="sxs-lookup"><span data-stu-id="4c48d-117">If your intent is tooencode your source video for streaming as well as tooproduce MP4 files for progressive download, then you shoud use hello "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="4c48d-118">При использовании hello **содержимого адаптивной несколько Bitrate MP4** заданы, кодировщик MES hello применит hello же логика кодирования, как описано выше, но теперь hello выходного актива будет содержать MP4-файлов где аудио и видео с чередованием.</span><span class="sxs-lookup"><span data-stu-id="4c48d-118">When using hello **Content Adaptive Multiple Bitrate MP4** preset, hello MES encoder will apply hello same encoding logic as above, but now hello output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="4c48d-119">Можно использовать один из этих MP4-файлов (например, hello высокий битрейт версия) как файл последовательную загрузку.</span><span class="sxs-lookup"><span data-stu-id="4c48d-119">You can use one of these MP4 files (for example, hello highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="4c48d-120"><a id="encoding_with_dotnet"></a>Кодирование с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="4c48d-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="4c48d-121">Следующий пример кода Hello использует hello tooperform Media Services .NET SDK следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="4c48d-121">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="4c48d-122">Создание задания кодирования.</span><span class="sxs-lookup"><span data-stu-id="4c48d-122">Create an encoding job.</span></span>
- <span data-ttu-id="4c48d-123">Получите кодировщик Media Encoder Стандартная toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="4c48d-123">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="4c48d-124">Добавить задание кодирования toohello задач и указать toouse hello **адаптивной потоковой передачи** предустановки.</span><span class="sxs-lookup"><span data-stu-id="4c48d-124">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="4c48d-125">Создание выходного актива, который будет содержать активов hello в кодировке.</span><span class="sxs-lookup"><span data-stu-id="4c48d-125">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="4c48d-126">Добавьте событие обработчика toocheck hello ход выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="4c48d-126">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="4c48d-127">Отправка задания hello.</span><span class="sxs-lookup"><span data-stu-id="4c48d-127">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4c48d-128">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4c48d-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="4c48d-129">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4c48d-129">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="4c48d-130">Пример</span><span class="sxs-lookup"><span data-stu-id="4c48d-130">Example</span></span>

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

## <span data-ttu-id="4c48d-131"><a id="output"></a>Выходные данные</span><span class="sxs-lookup"><span data-stu-id="4c48d-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="4c48d-132">В этом разделе приведены три примера слоев выходные данные, созданные MES в результате кодирования с hello **адаптивной потоковой передачи** предустановки.</span><span class="sxs-lookup"><span data-stu-id="4c48d-132">This section shows three examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="4c48d-133">Пример 1</span><span class="sxs-lookup"><span data-stu-id="4c48d-133">Example 1</span></span>
<span data-ttu-id="4c48d-134">При исходной высоте 1080 и частоте кадров 29,970 создается 6 слоев видео.</span><span class="sxs-lookup"><span data-stu-id="4c48d-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="4c48d-135">Слой</span><span class="sxs-lookup"><span data-stu-id="4c48d-135">Layer</span></span>|<span data-ttu-id="4c48d-136">Высота:</span><span class="sxs-lookup"><span data-stu-id="4c48d-136">Height</span></span>|<span data-ttu-id="4c48d-137">Ширина</span><span class="sxs-lookup"><span data-stu-id="4c48d-137">Width</span></span>|<span data-ttu-id="4c48d-138">Скорость (кбит/с)</span><span class="sxs-lookup"><span data-stu-id="4c48d-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="4c48d-139">1</span><span class="sxs-lookup"><span data-stu-id="4c48d-139">1</span></span>|<span data-ttu-id="4c48d-140">1080</span><span class="sxs-lookup"><span data-stu-id="4c48d-140">1080</span></span>|<span data-ttu-id="4c48d-141">1920</span><span class="sxs-lookup"><span data-stu-id="4c48d-141">1920</span></span>|<span data-ttu-id="4c48d-142">6780</span><span class="sxs-lookup"><span data-stu-id="4c48d-142">6780</span></span>|
|<span data-ttu-id="4c48d-143">2</span><span class="sxs-lookup"><span data-stu-id="4c48d-143">2</span></span>|<span data-ttu-id="4c48d-144">720</span><span class="sxs-lookup"><span data-stu-id="4c48d-144">720</span></span>|<span data-ttu-id="4c48d-145">1280</span><span class="sxs-lookup"><span data-stu-id="4c48d-145">1280</span></span>|<span data-ttu-id="4c48d-146">3520</span><span class="sxs-lookup"><span data-stu-id="4c48d-146">3520</span></span>|
|<span data-ttu-id="4c48d-147">3</span><span class="sxs-lookup"><span data-stu-id="4c48d-147">3</span></span>|<span data-ttu-id="4c48d-148">540</span><span class="sxs-lookup"><span data-stu-id="4c48d-148">540</span></span>|<span data-ttu-id="4c48d-149">960</span><span class="sxs-lookup"><span data-stu-id="4c48d-149">960</span></span>|<span data-ttu-id="4c48d-150">2210</span><span class="sxs-lookup"><span data-stu-id="4c48d-150">2210</span></span>|
|<span data-ttu-id="4c48d-151">4.</span><span class="sxs-lookup"><span data-stu-id="4c48d-151">4</span></span>|<span data-ttu-id="4c48d-152">360</span><span class="sxs-lookup"><span data-stu-id="4c48d-152">360</span></span>|<span data-ttu-id="4c48d-153">640</span><span class="sxs-lookup"><span data-stu-id="4c48d-153">640</span></span>|<span data-ttu-id="4c48d-154">1150</span><span class="sxs-lookup"><span data-stu-id="4c48d-154">1150</span></span>|
|<span data-ttu-id="4c48d-155">5</span><span class="sxs-lookup"><span data-stu-id="4c48d-155">5</span></span>|<span data-ttu-id="4c48d-156">270</span><span class="sxs-lookup"><span data-stu-id="4c48d-156">270</span></span>|<span data-ttu-id="4c48d-157">480</span><span class="sxs-lookup"><span data-stu-id="4c48d-157">480</span></span>|<span data-ttu-id="4c48d-158">720</span><span class="sxs-lookup"><span data-stu-id="4c48d-158">720</span></span>|
|<span data-ttu-id="4c48d-159">6</span><span class="sxs-lookup"><span data-stu-id="4c48d-159">6</span></span>|<span data-ttu-id="4c48d-160">180</span><span class="sxs-lookup"><span data-stu-id="4c48d-160">180</span></span>|<span data-ttu-id="4c48d-161">320</span><span class="sxs-lookup"><span data-stu-id="4c48d-161">320</span></span>|<span data-ttu-id="4c48d-162">380</span><span class="sxs-lookup"><span data-stu-id="4c48d-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="4c48d-163">Пример 2</span><span class="sxs-lookup"><span data-stu-id="4c48d-163">Example 2</span></span>
<span data-ttu-id="4c48d-164">При исходной высоте 720 и частоте кадров 23,970 создается 5 слоев видео.</span><span class="sxs-lookup"><span data-stu-id="4c48d-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="4c48d-165">Слой</span><span class="sxs-lookup"><span data-stu-id="4c48d-165">Layer</span></span>|<span data-ttu-id="4c48d-166">Высота:</span><span class="sxs-lookup"><span data-stu-id="4c48d-166">Height</span></span>|<span data-ttu-id="4c48d-167">Ширина</span><span class="sxs-lookup"><span data-stu-id="4c48d-167">Width</span></span>|<span data-ttu-id="4c48d-168">Скорость (кбит/с)</span><span class="sxs-lookup"><span data-stu-id="4c48d-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="4c48d-169">1</span><span class="sxs-lookup"><span data-stu-id="4c48d-169">1</span></span>|<span data-ttu-id="4c48d-170">720</span><span class="sxs-lookup"><span data-stu-id="4c48d-170">720</span></span>|<span data-ttu-id="4c48d-171">1280</span><span class="sxs-lookup"><span data-stu-id="4c48d-171">1280</span></span>|<span data-ttu-id="4c48d-172">2940</span><span class="sxs-lookup"><span data-stu-id="4c48d-172">2940</span></span>|
|<span data-ttu-id="4c48d-173">2</span><span class="sxs-lookup"><span data-stu-id="4c48d-173">2</span></span>|<span data-ttu-id="4c48d-174">540</span><span class="sxs-lookup"><span data-stu-id="4c48d-174">540</span></span>|<span data-ttu-id="4c48d-175">960</span><span class="sxs-lookup"><span data-stu-id="4c48d-175">960</span></span>|<span data-ttu-id="4c48d-176">1850</span><span class="sxs-lookup"><span data-stu-id="4c48d-176">1850</span></span>|
|<span data-ttu-id="4c48d-177">3</span><span class="sxs-lookup"><span data-stu-id="4c48d-177">3</span></span>|<span data-ttu-id="4c48d-178">360</span><span class="sxs-lookup"><span data-stu-id="4c48d-178">360</span></span>|<span data-ttu-id="4c48d-179">640</span><span class="sxs-lookup"><span data-stu-id="4c48d-179">640</span></span>|<span data-ttu-id="4c48d-180">960</span><span class="sxs-lookup"><span data-stu-id="4c48d-180">960</span></span>|
|<span data-ttu-id="4c48d-181">4.</span><span class="sxs-lookup"><span data-stu-id="4c48d-181">4</span></span>|<span data-ttu-id="4c48d-182">270</span><span class="sxs-lookup"><span data-stu-id="4c48d-182">270</span></span>|<span data-ttu-id="4c48d-183">480</span><span class="sxs-lookup"><span data-stu-id="4c48d-183">480</span></span>|<span data-ttu-id="4c48d-184">600</span><span class="sxs-lookup"><span data-stu-id="4c48d-184">600</span></span>|
|<span data-ttu-id="4c48d-185">5</span><span class="sxs-lookup"><span data-stu-id="4c48d-185">5</span></span>|<span data-ttu-id="4c48d-186">180</span><span class="sxs-lookup"><span data-stu-id="4c48d-186">180</span></span>|<span data-ttu-id="4c48d-187">320</span><span class="sxs-lookup"><span data-stu-id="4c48d-187">320</span></span>|<span data-ttu-id="4c48d-188">320</span><span class="sxs-lookup"><span data-stu-id="4c48d-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="4c48d-189">Пример 3</span><span class="sxs-lookup"><span data-stu-id="4c48d-189">Example 3</span></span>
<span data-ttu-id="4c48d-190">При исходной высоте 360 и частоте кадров 29,970 создается 3 слоя видео.</span><span class="sxs-lookup"><span data-stu-id="4c48d-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="4c48d-191">Слой</span><span class="sxs-lookup"><span data-stu-id="4c48d-191">Layer</span></span>|<span data-ttu-id="4c48d-192">Высота:</span><span class="sxs-lookup"><span data-stu-id="4c48d-192">Height</span></span>|<span data-ttu-id="4c48d-193">Ширина</span><span class="sxs-lookup"><span data-stu-id="4c48d-193">Width</span></span>|<span data-ttu-id="4c48d-194">Скорость (кбит/с)</span><span class="sxs-lookup"><span data-stu-id="4c48d-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="4c48d-195">1</span><span class="sxs-lookup"><span data-stu-id="4c48d-195">1</span></span>|<span data-ttu-id="4c48d-196">360</span><span class="sxs-lookup"><span data-stu-id="4c48d-196">360</span></span>|<span data-ttu-id="4c48d-197">640</span><span class="sxs-lookup"><span data-stu-id="4c48d-197">640</span></span>|<span data-ttu-id="4c48d-198">700</span><span class="sxs-lookup"><span data-stu-id="4c48d-198">700</span></span>|
|<span data-ttu-id="4c48d-199">2</span><span class="sxs-lookup"><span data-stu-id="4c48d-199">2</span></span>|<span data-ttu-id="4c48d-200">270</span><span class="sxs-lookup"><span data-stu-id="4c48d-200">270</span></span>|<span data-ttu-id="4c48d-201">480</span><span class="sxs-lookup"><span data-stu-id="4c48d-201">480</span></span>|<span data-ttu-id="4c48d-202">440</span><span class="sxs-lookup"><span data-stu-id="4c48d-202">440</span></span>|
|<span data-ttu-id="4c48d-203">3</span><span class="sxs-lookup"><span data-stu-id="4c48d-203">3</span></span>|<span data-ttu-id="4c48d-204">180</span><span class="sxs-lookup"><span data-stu-id="4c48d-204">180</span></span>|<span data-ttu-id="4c48d-205">320</span><span class="sxs-lookup"><span data-stu-id="4c48d-205">320</span></span>|<span data-ttu-id="4c48d-206">230</span><span class="sxs-lookup"><span data-stu-id="4c48d-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="4c48d-207">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="4c48d-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4c48d-208">Отзывы</span><span class="sxs-lookup"><span data-stu-id="4c48d-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="4c48d-209">См. также</span><span class="sxs-lookup"><span data-stu-id="4c48d-209">See Also</span></span>
[<span data-ttu-id="4c48d-210">Обзор кодирования с помощью служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="4c48d-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

