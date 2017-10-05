---
title: "Использование Azure Media Packager для выполнения задач статической упаковки | Документация Майкрософт"
description: "В этом разделе показаны различные задачи, которые выполняются с помощью Azure Media Packager."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0582628e-a525-4a78-90ac-9f7fc1cd909f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: cd36e46821eb85db523a5c84ec44895f68cc60e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="using-azure-media-packager-to-accomplish-static-packaging-tasks"></a><span data-ttu-id="10b28-103">Использование Azure Media Packager для выполнения задач статической упаковки</span><span class="sxs-lookup"><span data-stu-id="10b28-103">Using Azure Media Packager to accomplish static packaging tasks</span></span>
> [!NOTE]
> <span data-ttu-id="10b28-104">Поддержка Microsoft Azure Media Packager и Microsoft Azure Media Encryptor продлена до 1 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="10b28-104">The end of life date for Microsoft Azure Media Packager and Microsoft Azure Media Encryptor has been extended to March 1, 2017.</span></span> <span data-ttu-id="10b28-105">За это время функциональные возможности данных процессоров будут добавлены в стандартный кодировщик служб мультимедиа (MES).</span><span class="sxs-lookup"><span data-stu-id="10b28-105">Before that date, the functionalities of these processors will be added to Media Encoder Standard (MES).</span></span> <span data-ttu-id="10b28-106">Клиенты получат инструкции по переводу рабочих процессов на отправку заданий в MES.</span><span class="sxs-lookup"><span data-stu-id="10b28-106">Customers will be provided with instructions on how to migrate their workflows to send Jobs to MES.</span></span> <span data-ttu-id="10b28-107">Функциями преобразования формата и шифрования можно также пользоваться посредством динамической упаковки и динамического шифрования.</span><span class="sxs-lookup"><span data-stu-id="10b28-107">Format conversion and encryption capabilities may also be available through dynamic packaging and dynamic encryption.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="10b28-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="10b28-108">Overview</span></span>
<span data-ttu-id="10b28-109">Для поставки цифрового видео по Интернету необходимо сжать мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="10b28-109">In order to deliver digital video over the internet you must compress the media.</span></span> <span data-ttu-id="10b28-110">Цифровые видеофайлы довольно объемные. Это затрудняет их доставку через Интернет и влияет на качество их отображения на устройствах клиентов.</span><span class="sxs-lookup"><span data-stu-id="10b28-110">Digital video files are quite large and may be too big to deliver over the internet or for your customers’ devices to display properly.</span></span> <span data-ttu-id="10b28-111">Кодирование — это процесс сжатия аудио- и видеофайлов, чтобы их могли просматривать клиенты.</span><span class="sxs-lookup"><span data-stu-id="10b28-111">Encoding is the process of compressing video and audio so your customers can view your media.</span></span> <span data-ttu-id="10b28-112">После кодирования видео его можно поместить в различные контейнеры.</span><span class="sxs-lookup"><span data-stu-id="10b28-112">Once a video has been encoded it can be placed into different file containers.</span></span> <span data-ttu-id="10b28-113">Процесс помещения кодированных мультимедийных данных в контейнер называется упаковкой.</span><span class="sxs-lookup"><span data-stu-id="10b28-113">The process of placing encoded media into a container is called packaging.</span></span> <span data-ttu-id="10b28-114">Например, с помощью Azure Media Packager можно взять файл MP4 и преобразовать его в формат Smooth Streaming или HLS.</span><span class="sxs-lookup"><span data-stu-id="10b28-114">For example, you can take an MP4 file and convert it into Smooth Streaming or HLS content by using the Azure Media Packager.</span></span> 

<span data-ttu-id="10b28-115">Службы мультимедиа поддерживают динамическую и статическую упаковку.</span><span class="sxs-lookup"><span data-stu-id="10b28-115">Media Services supports dynamic and static packaging.</span></span> <span data-ttu-id="10b28-116">При использовании статической упаковки необходимо создать копию содержимого в каждом формате, который необходим вашим клиентам.</span><span class="sxs-lookup"><span data-stu-id="10b28-116">When using static packaging you need to create a copy of your content in each format required by your customers.</span></span> <span data-ttu-id="10b28-117">При использовании динамической упаковки достаточно создать ресурс, содержащий набор файлов MP4 с переменной скоростью или файлов Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="10b28-117">With dynamic packaging all you need is to create an asset that contains a set of adaptive bitrate MP4 or Smooth Streaming files.</span></span> <span data-ttu-id="10b28-118">Затем на основе формата, указанного в манифесте или запросе фрагмента, сервер потокового воспроизведения по запросу обеспечит передачу содержимого по протоколу, выбранному пользователями.</span><span class="sxs-lookup"><span data-stu-id="10b28-118">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that your users receive the stream in the protocol they have chosen.</span></span> <span data-ttu-id="10b28-119">В результате вы сможете хранить и оплачивать файлы только в одном формате, а службы мультимедиа выполнят сборку и будут обслуживать соответствующий ответ на основе запросов клиента.</span><span class="sxs-lookup"><span data-stu-id="10b28-119">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

> [!NOTE]
> <span data-ttu-id="10b28-120">Рекомендуется использовать [динамическую упаковку](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10b28-120">It is recommended to use [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>
> 
> 

<span data-ttu-id="10b28-121">Однако существуют некоторые сценарии, в которых требуется использовать статическую упаковку.</span><span class="sxs-lookup"><span data-stu-id="10b28-121">However, there are some scenarios that require static packaging:</span></span> 

* <span data-ttu-id="10b28-122">Проверка MP4-файлов с переменной скоростью, закодированных с помощью внешних кодировщиков (например, кодировщиков сторонних поставщиков).</span><span class="sxs-lookup"><span data-stu-id="10b28-122">Validating adaptive bitrate MP4s encoded with external encoders (for example, using third party encoders).</span></span>

<span data-ttu-id="10b28-123">Статическую упаковку также можно использовать для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="10b28-123">You can also use static packaging to perform the following tasks.</span></span> <span data-ttu-id="10b28-124">Однако рекомендуется использовать динамическое шифрование.</span><span class="sxs-lookup"><span data-stu-id="10b28-124">However it is recommended to use dynamic encryption.</span></span>

* <span data-ttu-id="10b28-125">Использование статического шифрования для защиты данных в формате Smooth и MPEG DASH с использованием PlayReady</span><span class="sxs-lookup"><span data-stu-id="10b28-125">Using static encryption to protect your Smooth and MPEG DASH with PlayReady</span></span>
* <span data-ttu-id="10b28-126">Использование статического шифрования для защиты HLSv3 с использованием AES-128</span><span class="sxs-lookup"><span data-stu-id="10b28-126">Using static encryption to protect HLSv3 with AES-128</span></span>
* <span data-ttu-id="10b28-127">Использование статического шифрования для защиты HLSv3 с использованием PlayReady</span><span class="sxs-lookup"><span data-stu-id="10b28-127">Using static encryption to protect HLSv3 with PlayReady</span></span>

## <a name="validating-adaptive-bitrate-mp4s-encoded-with-external-encoders"></a><span data-ttu-id="10b28-128">Проверка MP4-файлов с переменной скоростью, закодированных с помощью внешних кодировщиков</span><span class="sxs-lookup"><span data-stu-id="10b28-128">Validating Adaptive Bitrate MP4s Encoded with External Encoders</span></span>
<span data-ttu-id="10b28-129">Если вы хотите использовать набор MP4-файлов с адаптивной скоростью (с несколькими скоростями), которые не были закодированы с помощью кодировщиков служб мультимедиа, эти файлы следует проверить перед дальнейшей обработкой.</span><span class="sxs-lookup"><span data-stu-id="10b28-129">If you want to use a set of adaptive bitrate (multi-bitrate) MP4 files that were not encoded with Media Services' encoders, you should validate your files before further processing.</span></span> <span data-ttu-id="10b28-130">Media Services Packager может проверить ресурс, содержащий набор MP4-файлов, и определить, можно ли упаковать ресурс в формат Smooth Streaming или HLS.</span><span class="sxs-lookup"><span data-stu-id="10b28-130">The Media Services Packager can validate an asset that contains a set of MP4 files and check whether the asset can be packaged to Smooth Streaming or HLS.</span></span> <span data-ttu-id="10b28-131">Если проверка завершается неудачно, задача обработки также завершится с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="10b28-131">If the validation task fails, the job that was processing the task will complete with an error.</span></span> <span data-ttu-id="10b28-132">Файл XML, определяющий предустановку для задачи проверки, можно найти в разделе [Предустановка задачи для Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) .</span><span class="sxs-lookup"><span data-stu-id="10b28-132">The XML that defines the preset for the validation task can be found in the [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

> [!NOTE]
> <span data-ttu-id="10b28-133">Во избежание проблем во время выполнения используйте стандартный кодировщик мультимедиа для создания содержимого, а упаковщик служб мультимедиа — для проверки содержимого.</span><span class="sxs-lookup"><span data-stu-id="10b28-133">Use the Media Encoder Standard to produce or the Media Services Packager to validate your content in order to avoid runtime issues.</span></span> <span data-ttu-id="10b28-134">Если сервер потокового воспроизведения по запросу не может выполнить синтаксический анализ исходных файлов во время выполнения, вы получите ошибку HTTP 1.1 "415 Тип содержимого не поддерживается".</span><span class="sxs-lookup"><span data-stu-id="10b28-134">If the On-Demand Streaming server is not able to parse your source files at runtime, you will receive HTTP 1.1 error “415 Unsupported Media Type”.</span></span> <span data-ttu-id="10b28-135">Несколько неудачных попыток анализа исходных файлов влияют на производительность сервера потокового воспроизведения по запросу и могут снизить пропускную способность, доступную для обработки других запросов.</span><span class="sxs-lookup"><span data-stu-id="10b28-135">Repeatedly causing the server to fail to parse your source files affects performance of the On-Demand Streaming server and may reduce the bandwidth available to serving other requests.</span></span> <span data-ttu-id="10b28-136">Службы мультимедиа Azure предлагают Соглашение об уровне обслуживания (SLA) для служб потокового воспроизведения по запросу; тем не менее, если сервер используется неправильно описанным выше образом, это соглашение не учитывается.</span><span class="sxs-lookup"><span data-stu-id="10b28-136">Azure Media Services offers a Service Level Agreement (SLA) on its On-Demand Streaming services; however, this SLA cannot be honored if the server is misused in the fashion described above.</span></span>
> 
> 

<span data-ttu-id="10b28-137">В этом разделе показано, как выполнить задачу проверки.</span><span class="sxs-lookup"><span data-stu-id="10b28-137">This section shows how to process the validation task.</span></span> <span data-ttu-id="10b28-138">В нем также показано, как просмотреть состояние и сообщение об ошибке для задания, которое завершилось с состоянием ошибки JobStatus.Error.</span><span class="sxs-lookup"><span data-stu-id="10b28-138">It also shows how to see the status and the error message of the job that completes with JobStatus.Error.</span></span>

<span data-ttu-id="10b28-139">Чтобы проверить файлы MP4 с помощью Media Services Packager, необходимо создать собственный файл манифеста (ISM) и загрузить его вместе с исходными файлами в учетную запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="10b28-139">To validate your MP4 files with Media Services Packager, you must create your own manifest (.ism) file and upload it together with the source files into the Media Services account.</span></span> <span data-ttu-id="10b28-140">Ниже приведен пример ISM-файла, созданного стандартным кодировщиком мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="10b28-140">Below is a sample of the .ism file produced by the Media Encoder Standard.</span></span> <span data-ttu-id="10b28-141">Имена файлов чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="10b28-141">The file names are case sensitive.</span></span> <span data-ttu-id="10b28-142">Также убедитесь, что текст в ISM-файле представлен в кодировке UTF-8.</span><span class="sxs-lookup"><span data-stu-id="10b28-142">Also, make sure the text in the .ism file is encoded with UTF-8.</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
    <!-- Tells the server that these input files are MP4s – specific to Dynamic Packaging -->
        <meta name="formats" content="mp4" /> 
      </head>
      <body>
        <switch>
          <video src="BigBuckBunny_1000.mp4" />
          <video src="BigBuckBunny_1500.mp4" />
          <video src="BigBuckBunny_2250.mp4" />
          <video src="BigBuckBunny_3400.mp4" />
          <video src="BigBuckBunny_400.mp4" />
          <video src="BigBuckBunny_650.mp4" />
          <audio src="BigBuckBunny_400.mp4" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="10b28-143">После того как у вас появится набор файлов MP4 с переменной скоростью, вы сможете воспользоваться преимуществами динамической упаковки.</span><span class="sxs-lookup"><span data-stu-id="10b28-143">Once you have the adaptive bitrate MP4 set you can take advantage of Dynamic Packaging.</span></span> <span data-ttu-id="10b28-144">Динамическая упаковка позволяет доставлять потоковое содержимое с помощью указанного протокола без дальнейшей упаковки.</span><span class="sxs-lookup"><span data-stu-id="10b28-144">Dynamic Packaging allows you to deliver streams in the specified protocol without further packaging.</span></span> <span data-ttu-id="10b28-145">Дополнительные сведения см. в статье [Динамическая упаковка](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10b28-145">For more information, see [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="10b28-146">В следующем примере кода используются расширения пакета SDK служб мультимедиа Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="10b28-146">The following code sample uses Azure Media Services .NET SDK Extensions.</span></span>  <span data-ttu-id="10b28-147">Обязательно измените код, указав каталог, в котором расположены исходные MP4-файлы и ISM-файл.</span><span class="sxs-lookup"><span data-stu-id="10b28-147">Make sure to update the code to point to the folder where your input MP4 files and .ism file are located.</span></span> <span data-ttu-id="10b28-148">Также укажите расположение файла MediaPackager_ValidateTask.xml.</span><span class="sxs-lookup"><span data-stu-id="10b28-148">And also to where your MediaPackager_ValidateTask.xml file is located.</span></span> <span data-ttu-id="10b28-149">Этот XML-файл определяется в разделе [Предустановка задачи для Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) .</span><span class="sxs-lookup"><span data-stu-id="10b28-149">This XML file is defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Xml.Linq;

    namespace MediaServicesStaticPackaging
    {
        class Program
        {
            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            // The MultibitrateMP4Files folder should also
            // contain the .ism manifest file.
            private static readonly string _multibitrateMP4s =
                Path.Combine(_mediaFiles, @"MultibitrateMP4Files");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations";

            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServicesAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServicesAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache the Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Use the cached credentials to create CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Ingest a set of multibitrate MP4s.
                //
                // Use the SDK extension method to create a new asset by 
                // uploading files from a local directory.
                IAsset multibitrateMP4sAsset = _context.Assets.CreateFromFolder(
                    _multibitrateMP4s,
                    AssetCreationOptions.None,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                // Use Azure Media Packager to validate the files.
                IAsset validatedMP4s =
                    ValidateMultibitrateMP4s(multibitrateMP4sAsset);

                // Publish the asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    validatedMP4s,
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                                     // Get the streaming URLs.
                Console.WriteLine("Smooth Streaming URL:");
                Console.WriteLine(validatedMP4s.GetSmoothStreamingUri().ToString());
                Console.WriteLine("MPEG DASH URL:");
                Console.WriteLine(validatedMP4s.GetMpegDashUri().ToString());
                Console.WriteLine("HLS URL:");
                Console.WriteLine(validatedMP4s.GetHlsUri().ToString());
            }

            public static IAsset ValidateMultibitrateMP4s(IAsset multibitrateMP4sAsset)
            {
                // Set .ism as a primary file 
                // in a multibitrate MP4 set.
                SetISMFileAsPrimary(multibitrateMP4sAsset);

                // Create a new job.
                IJob job = _context.Jobs.Create("MP4 validation and converstion to Smooth Stream job.");

                // Read the task configuration data into a string. 
                string configMp4Validation = File.ReadAllText(Path.Combine(
                        _configurationXMLFiles,
                        "MediaPackager_ValidateTask.xml"));

                // Get the SDK extension method to  get a reference to the Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Create a task with the conversion details, using the configuration data. 
                ITask task = job.Tasks.AddNew("Mp4 Validation Task",
                    processor,
                    configMp4Validation,
                    TaskOptions.None);

                // Specify the input asset to be validated.
                task.InputAssets.Add(multibitrateMP4sAsset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means the output asset is in the clear (unencrypted). 
                task.OutputAssets.AddNew("Validated output asset",
                        AssetCreationOptions.None);

                // Submit the job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // If the validation task fails and job completes with JobState.Error,
                // display the error message and throw an exception.
                if (job.State == JobState.Error)
                {
                    Console.WriteLine("  Job ID: " + job.Id);
                    Console.WriteLine("  Name: " + job.Name);
                    Console.WriteLine("  State: " + job.State);

                    foreach (var jobTask in job.Tasks)
                    {
                        Console.WriteLine("  Task Id: " + jobTask.Id);
                        Console.WriteLine("  Name: " + jobTask.Name);
                        Console.WriteLine("  Progress: " + jobTask.Progress);
                        Console.WriteLine("  Configuration: " + jobTask.Configuration);
                        Console.WriteLine("  Running time: " + jobTask.RunningDuration);
                        if (jobTask.ErrorDetails != null)
                        {
                            foreach (var errordetail in jobTask.ErrorDetails)
                            {

                                Console.WriteLine("  Error Message:" + errordetail.Message);
                                Console.WriteLine("  Error Code:" + errordetail.Code);
                            }
                        }
                    }
                    throw new Exception("The specified multi-bitrate MP4 set is not valid.");
                }


                return job.OutputMediaAssets[0];
            }

            static void SetISMFileAsPrimary(IAsset asset)
            {
                var ismAssetFiles = asset.AssetFiles.ToList().
                    Where(f => f.Name.EndsWith(".ism", StringComparison.OrdinalIgnoreCase)).ToArray();

                // The following code assigns the first .ism file as the primary file in the asset.
                // An asset should have one .ism file.  
                ismAssetFiles.First().IsPrimary = true;
                ismAssetFiles.First().Update();
            }
        }
    }

## <a name="using-static-encryption-to-protect-your-smooth-and-mpeg-dash-with-playready"></a><span data-ttu-id="10b28-150">Использование статического шифрования для защиты данных в формате Smooth и MPEG DASH с использованием PlayReady</span><span class="sxs-lookup"><span data-stu-id="10b28-150">Using Static Encryption to Protect your Smooth and MPEG DASH with PlayReady</span></span>
<span data-ttu-id="10b28-151">Если вы хотите защитить содержимое с помощью PlayReady, можно выполнить [динамическое шифрование](media-services-protect-with-drm.md) (рекомендуемый вариант) или статическое шифрование (как описано в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="10b28-151">If you want to protect your content with PlayReady, you have a choice of using [dynamic encryption](media-services-protect-with-drm.md) (the recommended option) or static encryption (as described in this section).</span></span>

<span data-ttu-id="10b28-152">В примере, приведенном в этом разделе, мезонинный файл (в данном случае, формата MP4) кодируется в файлы MP4 с переменной скоростью.</span><span class="sxs-lookup"><span data-stu-id="10b28-152">The example in this section encodes a mezzanine file (in this case MP4) into adaptive bitrate MP4 files.</span></span> <span data-ttu-id="10b28-153">Затем файлы MP4 упаковываются в Smooth Streaming и шифруются с помощью PlayReady.</span><span class="sxs-lookup"><span data-stu-id="10b28-153">It then packages MP4s into Smooth Streaming and then encrypts Smooth Streaming with PlayReady.</span></span> <span data-ttu-id="10b28-154">В результате вы можете выполнять потоковую передачу содержимого с помощью Smooth Streaming или MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="10b28-154">As a result you are able to stream Smooth Streaming or MPEG DASH.</span></span>

<span data-ttu-id="10b28-155">Службы мультимедиа теперь обеспечивают доставку лицензий Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="10b28-155">Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="10b28-156">Пример в этой статье показывает, как настроить службу доставки лицензий PlayReady служб мультимедиа (см. метод ConfigureLicenseDeliveryService, определенный в приведенном ниже коде).</span><span class="sxs-lookup"><span data-stu-id="10b28-156">The example in this article shows how to configure the Media Services PlayReady license delivery service (see the ConfigureLicenseDeliveryService method defined in the code below).</span></span> <span data-ttu-id="10b28-157">Дополнительные сведения о службе доставки лицензий PlayReady служб мультимедиа см. в статье [Использование общего динамического шифрования PlayReady и (или) Widevine DRM](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="10b28-157">For more information about Media Services PlayReady license delivery service, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="10b28-158">Для доставки содержимого MPEG DASH, зашифрованного с помощью PlayReady, обязательно использовать параметры CENC, установив свойства useSencBox и adjustSubSamples (описанные в разделе [Предустановка задачи для Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) ) в значение true.</span><span class="sxs-lookup"><span data-stu-id="10b28-158">To deliver MPEG DASH encrypted with PlayReady, make sure to use CENC options by setting the useSencBox and adjustSubSamples properties (described in the [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic) to true.</span></span>  
> 
> 

<span data-ttu-id="10b28-159">Обязательно измените следующий код, указав каталог, в котором расположен исходный файл MP4.</span><span class="sxs-lookup"><span data-stu-id="10b28-159">Make sure to update the following code to point to the folder where your input MP4 file is located.</span></span>

<span data-ttu-id="10b28-160">Также укажите расположение файлов MediaPackager_MP4ToSmooth.xml и MediaEncryptor_PlayReadyProtection.xml.</span><span class="sxs-lookup"><span data-stu-id="10b28-160">And also to where your MediaPackager_MP4ToSmooth.xml and MediaEncryptor_PlayReadyProtection.xml files are located.</span></span> <span data-ttu-id="10b28-161">Файл MediaPackager_MP4ToSmooth.xml описан [здесь](http://msdn.microsoft.com/library/azure/hh973635.aspx), а MediaEncryptor_PlayReadyProtection.xml — [здесь](http://msdn.microsoft.com/library/azure/hh973610.aspx).</span><span class="sxs-lookup"><span data-stu-id="10b28-161">MediaPackager_MP4ToSmooth.xml is defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) and MediaEncryptor_PlayReadyProtection.xml is defined in the [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic.</span></span> 

<span data-ttu-id="10b28-162">В примере определяется метод UpdatePlayReadyConfigurationXMLFile, который можно использовать для динамического обновления файла MediaEncryptor_PlayReadyProtection.xml.</span><span class="sxs-lookup"><span data-stu-id="10b28-162">The example defines the UpdatePlayReadyConfigurationXMLFile method that you can use to dynamically update the MediaEncryptor_PlayReadyProtection.xml file.</span></span> <span data-ttu-id="10b28-163">Если начальное значение ключа доступно, можно использовать метод CommonEncryption.GeneratePlayReadyContentKey для создания ключа содержимого на основе значений keySeedValue и KeyId.</span><span class="sxs-lookup"><span data-stu-id="10b28-163">If you have the key seed available, you can use the CommonEncryption.GeneratePlayReadyContentKey method to generate the content key based on the keySeedValue and KeyId values.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace PlayReadyStaticEncryptAndKeyDeliverySvc
    {
        class Program
        {

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";


            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache the Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Use the cached credentials to create CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Encoding and encrypting assets //////////////////////
                // Load a single MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file to a set of multibitrate MP4s.
                // Then, package a set of MP4s to clear Smooth Streaming.
                IAsset clearSmoothStreamAsset =
                    ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create a common encryption content key that is used 
                // a) to set the key values in the MediaEncryptor_PlayReadyProtection.xml file
                //    that is used for encryption.
                // b) to configure the license delivery service and 
                //
                Guid keyId;
                byte[] contentKey;

                IContentKey key = CreateCommonEncryptionKey(out keyId, out contentKey);

                // The content key authorization policy must be configured by you 
                // and met by the client in order for the PlayReady license
                // to be delivered to the client. 
                // In this example the Media Services PlayReady license delivery service is used.
                ConfigureLicenseDeliveryService(key);

                // Get the Media Services PlayReady license delivery URL.
                // This URL will be assigned to the licenseAcquisitionUrl property 
                // of the MediaEncryptor_PlayReadyProtection.xml file.
                Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

                // Update the MediaEncryptor_PlayReadyProtection.xml file with the key and URL info.
                UpdatePlayReadyConfigurationXMLFile(keyId, contentKey, acquisitionUrl);


                // Encrypt your clear Smooth Streaming to Smooth Streaming with PlayReady.
                IAsset outputAsset = CreateSmoothStreamEncryptedWithPlayReady(clearSmoothStreamAsset);


                // You can use the http://smf.cloudapp.net/healthmonitor player 
                // to test the smoothStreamURL URL.
                string smoothStreamURL = outputAsset.GetSmoothStreamingUri().ToString();
                Console.WriteLine("Smooth Streaming URL:");
                Console.WriteLine(smoothStreamURL);

                // You can use the http://dashif.org/reference/players/javascript/ player 
                // to test the dashURL URL.
                string dashURL = outputAsset.GetMpegDashUri().ToString();
                Console.WriteLine("MPEG DASH URL:");
                Console.WriteLine(dashURL);
            }

            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 to multibitrate MP4s,
            /// 2 task - packages MP4s to Smooth Streaming.
            /// </summary>
            /// <returns>The output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 to Smooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set to Clear Smooth Stream.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit the job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get the output asset that contains the Smooth Streaming asset.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Encrypts Smooth Stream with PlayReady.
            /// Then creates a Smooth Streaming Url.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>The output asset.</returns>
            public static IAsset CreateSmoothStreamEncryptedWithPlayReady(IAsset clearSmoothStreamAsset)
            {
                // Create a job.
                IJob job = _context.Jobs.Create("Encrypt to PlayReady Smooth Streaming.");

                // Add task 1 - Encrypt Smooth Streaming with PlayReady 
                IAsset encryptedSmoothAsset =
                    EncryptSmoothStreamWithPlayReadyTask(job, clearSmoothStreamAsset);

                // Submit the job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // The OutputMediaAssets[0] contains the desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[0],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[0];
            }

            /// <summary>
            /// Create a common encryption content key that is used 
            /// to set the key values in the MediaEncryptor_PlayReadyProtection.xml file
            /// that is used for encryption.
            /// </summary>
            /// <param name="keyId"></param>
            /// <param name="contentKey"></param>
            /// <returns></returns>
            public static IContentKey CreateCommonEncryptionKey(out Guid keyId, out byte[] contentKey)
            {
                keyId = Guid.NewGuid();
                contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            /// <summary>
            /// Update your configuration .xml file dynamically.
            /// </summary>
            public static void UpdatePlayReadyConfigurationXMLFile(Guid keyId, byte[] keyValue, Uri licenseAcquisitionUrl)
            {
                string xmlFileName = Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml");

                XNamespace xmlns = "http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#";

                // Prepare the encryption task template
                XDocument doc = XDocument.Load(xmlFileName);

                var licenseAcquisitionUrlEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "licenseAcquisitionUrl")
                        .FirstOrDefault();
                var contentKeyEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "contentKey")
                        .FirstOrDefault();
                var keyIdEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "keyId")
                        .FirstOrDefault();

                // Update the "value" property.
                if (licenseAcquisitionUrlEl != null)
                    licenseAcquisitionUrlEl.Attribute("value").SetValue(licenseAcquisitionUrl.ToString());

                if (contentKeyEl != null)
                    contentKeyEl.Attribute("value").SetValue(Convert.ToBase64String(keyValue));

                if (keyIdEl != null)
                    keyIdEl.Attribute("value").SetValue(keyId);

                doc.Save(xmlFileName);
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">The location of the files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify the following encryption options for the AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded to Azure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: The files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use the SDK extension method to create a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                return asset;
            }

            /// <summary>
            /// Creates a task to encode to Adaptive Bitrate. 
            /// Adds the new task to a job.
            /// </summary>
            /// <param name="job">The job to which to add the new task.</param>
            /// <param name="asset">The input asset.</param>
            /// <returns>The output asset.</returns>
            private static IAsset EncodeMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get the SDK extension method to  get a reference to the Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 to Adaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify the input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means the output asset is in the clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s",
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task to convert the MP4 file(s) to a Smooth Streaming asset.
            /// Adds the new task to a job.
            /// </summary>
            /// <param name="job">The job to which to add the new task.</param>
            /// <param name="asset">The input asset.</param>
            /// <returns>The output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get the SDK extension method to  get a reference to the Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles,
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task to convert adaptive bitrate to Smooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 to Smooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify the input Asset, which is the output Asset from the first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means the output asset is in the clear (unencrypted).
                IAsset smoothOutputAsset =
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Stream",
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }


            /// <summary>
            /// Creates a task to encrypt Smooth Streaming with PlayReady.
            /// Note: To deliver DASH, make sure to set the useSencBox and adjustSubSamples 
            /// configuration properties to true. 
            /// In this example, MediaEncryptor_PlayReadyProtection.xml contains configuration.
            /// </summary>
            /// <param name="job">The job to which to add the new task.</param>
            /// <param name="asset">The input asset.</param>
            /// <returns>The output asset.</returns>
            private static IAsset EncryptSmoothStreamWithPlayReadyTask(IJob job, IAsset asset)
            {
                // Get the SDK extension method to  get a reference to the Azure Media Encryptor.
                IMediaProcessor playreadyProcessor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaEncryptor);

                // Read the configuration XML.
                //
                // Note that the configuration defined in MediaEncryptor_PlayReadyProtection.xml
                // is using keySeedValue. It is recommended that you do this only for testing 
                // and not in production. For more information, see 
                // http://msdn.microsoft.com/library/windowsazure/dn189154.aspx.
                //
                string configPlayReady = File.ReadAllText(Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml"));

                ITask playreadyTask = job.Tasks.AddNew("My PlayReady Task",
                   playreadyProcessor,
                   configPlayReady,
                   TaskOptions.ProtectedConfiguration);

                playreadyTask.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.CommonEncryptionProtected.
                IAsset playreadyAsset = playreadyTask.OutputAssets.AddNew(
                                                "PlayReady Smooth Streaming",
                                                AssetCreationOptions.CommonEncryptionProtected);

                return playreadyAsset;
            }

            /// <summary>
            /// Configures authorization policy for the content key. 
            /// </summary>
            /// <param name="contentKey">The content key.</param>
            static public void ConfigureLicenseDeliveryService(IContentKey contentKey)
            {
                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                    new ContentKeyAuthorizationPolicyRestriction 
                    { 
                        Name = "Open", 
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                        Requirements = null
                    }
                };

                // Configure PlayReady license template.
                string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                IContentKeyAuthorizationPolicyOption policyOption =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, newLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(policyOption);

                // Associate the content key authorization policy with the content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            static private string ConfigurePlayReadyLicenseTemplate()
            {
                // The following code configures PlayReady License Template using .NET classes
                // and returns the XML string.

                PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }

            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }
        }
    }

## <a name="using-static-encryption-to-protect-hlsv3-with-aes-128"></a><span data-ttu-id="10b28-164">Использование статического шифрования для защиты HLSv3 с использованием AES-128</span><span class="sxs-lookup"><span data-stu-id="10b28-164">Using Static Encryption to Protect HLSv3 with AES-128</span></span>
<span data-ttu-id="10b28-165">Если вы хотите зашифровать содержимое HLS с AES-128, можно выполнить динамическое шифрование (рекомендуемый вариант) или статическое шифрование (как описано в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="10b28-165">If you want to encrypt your HLS with AES-128, you have a choice of using dynamic encryption (the recommended option) or static encryption (as shown in this section).</span></span> <span data-ttu-id="10b28-166">Если вы решили воспользоваться динамическим шифрованием, обратитесь к разделу [Использование динамического шифрования AES-128 и службы доставки ключей](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="10b28-166">If you decide to use dynamic encryption, see [Using AES-128 Dynamic Encryption and Key Delivery Service](media-services-protect-with-aes128.md).</span></span>

> [!NOTE]
> <span data-ttu-id="10b28-167">Чтобы преобразовать содержимое в формат HLS, необходимо сначала преобразовать или закодировать содержимое в формат Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="10b28-167">In order to convert your content into HLS, you must first convert/encode your content into Smooth Streaming.</span></span>
> <span data-ttu-id="10b28-168">Кроме того, чтобы зашифровать содержимое HLS с AES, обязательно установите следующие свойства в файле MediaPackager_SmoothToHLS.xml: установите свойство encrypt в true и установите значение ключа и значение keyuri, так чтобы они указывали на ваш сервер проверки подлинности или авторизации.</span><span class="sxs-lookup"><span data-stu-id="10b28-168">Also, for the HLS to get encrypted with AES make sure to set the following properties in your MediaPackager_SmoothToHLS.xml file: set the encrypt property to true, set the key value, and the keyuri value to point to your authentication\authorization server.</span></span>
> <span data-ttu-id="10b28-169">Службы мультимедиа создадут файл ключа и поместят его в контейнер ресурса.</span><span class="sxs-lookup"><span data-stu-id="10b28-169">Media Services will create a key file and place it in the asset container.</span></span> <span data-ttu-id="10b28-170">Необходимо скопировать файл /asset-containerguid/*.key на сервер (или создать свой собственный файл ключа) и затем удалите Key-файл из контейнера актива.</span><span class="sxs-lookup"><span data-stu-id="10b28-170">You should copy the /asset-containerguid/*.key file to your server (or create your own key file) and then delete the *.key file from the asset container.</span></span>
> 
> 

<span data-ttu-id="10b28-171">Пример в этом разделе кодирует мезонинный файл (в данном случае MP4) в файлы MP4 с несколькими скоростями, а затем упаковывает файлы MP4 в формат Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="10b28-171">The example in this section encodes a mezzanine file (in this case MP4) into multibitrate MP4 files and then packages MP4s into Smooth Streaming.</span></span> <span data-ttu-id="10b28-172">После этого он упаковывает содержимое в формате Smooth Streaming в формат HTTP Live Streaming (HLS), зашифрованный с помощью 128-разрядного шифрования потока AES.</span><span class="sxs-lookup"><span data-stu-id="10b28-172">It then packages Smooth Streaming into HTTP Live Streaming (HLS) encrypted with Advanced Encryption Standard (AES) 128-bit stream encryption.</span></span> <span data-ttu-id="10b28-173">Обязательно измените следующий код, указав каталог, в котором расположен исходный файл MP4.</span><span class="sxs-lookup"><span data-stu-id="10b28-173">Make sure to update the following code to point to the folder where your input MP4 file is located.</span></span> <span data-ttu-id="10b28-174">Также укажите расположение файлов MediaPackager_MP4ToSmooth.xml и MediaPackager_SmoothToHLS.xml.</span><span class="sxs-lookup"><span data-stu-id="10b28-174">And also to where your MediaPackager_MP4ToSmooth.xml and MediaPackager_SmoothToHLS.xml configuration files are located.</span></span> <span data-ttu-id="10b28-175">Определение этих файлов можно найти в разделе [Предустановка задачи для Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) .</span><span class="sxs-lookup"><span data-stu-id="10b28-175">You can find the definition for these files in the [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;

    namespace MediaServicesContentProtection
    {
        class Program
        {
            // Paths to support files (within the above base path). You can use 
            // the provided sample media files from the "SupportFiles" folder, or 
            // provide paths to your own media files below to run these samples.

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"SingleMP4\BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";

            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName = 
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey = 
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache the Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName, 
                                _mediaServicesAccountKey);
                // Use the cached credentials to create CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Encoding and encrypting assets //////////////////////

                // Load an MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file to a set of multibitrate MP4s.
                // Then, package a set of MP4s to clear Smooth Streaming.
                IAsset clearSmoothStreamAsset = ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create HLS encrypted with AES.
                IAsset HLSEncryptedWithAESAsset = CreateHLSEncryptedWithAES(clearSmoothStreamAsset);

                // You can use the following player to test the HLS with AES stream.
                // http://apps.microsoft.com/windows/app/3ivx-hls-player/f79ce7d0-2993-4658-bc4e-83dc182a0614 
                string hlsWithAESURL = HLSEncryptedWithAESAsset.GetHlsUri().ToString();
                Console.WriteLine("HLS with AES URL:");
                Console.WriteLine(hlsWithAESURL);
            }


            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 to multibitrate MP4s,
            /// 2 task - packages MP4s to Smooth Streaming.
            /// </summary>
            /// <returns>The output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 to Smooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeSingleMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set to Clear Smooth Streaming.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit the job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get the output asset that contains Smooth Streaming.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Encrypts an HLS with AES-128.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>The output asset.</returns>
            public static IAsset CreateHLSEncryptedWithAES(IAsset clearSmoothStreamAsset)
            {
                IJob job = _context.Jobs.Create("Encrypt to HLS with AES.");

                // Add task 1 - Package clear Smooth Streaming to HLS with AES.
                PackageSmoothStreamToHLS(job, clearSmoothStreamAsset);

                // Submit the job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // The OutputMediaAssets[0] contains the desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[0],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[0];
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">The location of the files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify the following encryption options for the AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded to Azure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: The files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use the SDK extension method to create a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                return asset;
            }

            /// <summary>
            /// Creates a task to encode to Adaptive Bitrate. 
            /// Adds the new task to a job.
            /// </summary>
            /// <param name="job">The job to which to add the new task.</param>
            /// <param name="asset">The input asset.</param>
            /// <returns>The output asset.</returns>
            private static IAsset EncodeSingleMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get the SDK extension method to  get a reference to the Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 to Adaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify the input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means the output asset is in the clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s", 
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task to convert the MP4 file(s) to a Smooth Streaming asset.
            /// Adds the new task to a job.
            /// </summary>
            /// <param name="job">The job to which to add the new task.</param>
            /// <param name="asset">The input asset.</param>
            /// <returns>The output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get the SDK extension method to  get a reference to the Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles, 
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task to convert adaptive bitrate to Smooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 to Smooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify the input Asset, which is the output Asset from the first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means the output asset is in the clear (unencrypted).
                IAsset smoothOutputAsset = 
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Streaming", 
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }

            /// <summary>
            /// Converts Smooth Streaming to HLS.
            /// </summary>
            /// <param name="job">The job to which to add the new task.</param>
            /// <param name="asset">The Smooth Streaming asset.</param>
            /// <returns>The asset that was packaged to HLS.</returns>
            private static IAsset PackageSmoothStreamToHLS(IJob job, IAsset smoothStreamAsset)
            {
                // Get the SDK extension method to  get a reference to the Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Read the configuration data into a string. 
                // For the HLS to get encrypted with AES make sure to set the
                // encrypt configuration property to true.
                //
                // In production, it is recommended to do the following:
                //    Set a Key url for your authn/authz server.
                //    Copy the /asset-containerguid/*.key file to your server (or craft a key file for yourself).
                //    Delete *.key from the asset container.
                //
                string configuration = File.ReadAllText(Path.Combine(_configurationXMLFiles, @"MediaPackager_SmoothToHLS.xml"));

                // Create a task with the encoding details, using a configuration file.
                ITask task = job.Tasks.AddNew("My Smooth Streaming to HLS Task",
                   processor,
                   configuration,
                   TaskOptions.ProtectedConfiguration);

                // Specify the input asset to be encoded.
                task.InputAssets.Add(smoothStreamAsset);

                // Add an output asset to contain the results of the job. 
                IAsset outputAsset = 
                    task.OutputAssets.AddNew("HLS asset", AssetCreationOptions.None);


                return outputAsset;
            }
        }
    }

## <a name="using-static-encryption-to-protect-hlsv3-with-playready"></a><span data-ttu-id="10b28-176">Использование статического шифрования для защиты HLSv3 с использованием PlayReady</span><span class="sxs-lookup"><span data-stu-id="10b28-176">Using Static Encryption to Protect HLSv3 with PlayReady</span></span>
<span data-ttu-id="10b28-177">Если вы хотите защитить содержимое с помощью PlayReady, можно выполнить [динамическое шифрование](media-services-protect-with-drm.md) (рекомендуемый вариант) или статическое шифрование (как описано в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="10b28-177">If you want to protect your content with PlayReady, you have a choice of using [dynamic encryption](media-services-protect-with-drm.md) (the recommended option) or static encryption (as described in this section).</span></span>

> [!NOTE]
> <span data-ttu-id="10b28-178">Чтобы защитить ваше содержимое с помощью PlayReady, необходимо сначала преобразовать или закодировать содержимое в формат Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="10b28-178">In order to protect your content using PlayReady you must first convert/encode your content into a Smooth Streaming format.</span></span>
> 
> 

<span data-ttu-id="10b28-179">В примере, приведенном в этом разделе, мезонинный файл (в данном случае, файл формата MP4) кодируется в файлы MP4 с переменной скоростью.</span><span class="sxs-lookup"><span data-stu-id="10b28-179">The example in this section encodes a mezzanine file (in this case MP4) into multibitrate MP4 files.</span></span> <span data-ttu-id="10b28-180">Затем файлы MP4 упаковываются в Smooth Streaming и шифруются с помощью PlayReady.</span><span class="sxs-lookup"><span data-stu-id="10b28-180">It then packages MP4s into Smooth Streaming and encrypts Smooth Streaming with PlayReady.</span></span> <span data-ttu-id="10b28-181">Для шифрования формата HTTP Live Streaming (HLS) с помощью PlayReady, ресурс PlayReady Smooth Streaming необходимо упаковать в формат HLS.</span><span class="sxs-lookup"><span data-stu-id="10b28-181">To produce HTTP Live Streaming (HLS) encrypted with PlayReady, the PlayReady Smooth Streaming asset needs to be packaged into HLS.</span></span> <span data-ttu-id="10b28-182">В этом разделе показано, как выполнить все эти действия.</span><span class="sxs-lookup"><span data-stu-id="10b28-182">This topic demonstrates how to perform all these steps.</span></span>

<span data-ttu-id="10b28-183">Службы мультимедиа теперь обеспечивают доставку лицензий Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="10b28-183">Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="10b28-184">В примере из этой статьи показывается, как настроить службу доставки лицензий PlayReady служб мультимедиа (см. метод **ConfigureLicenseDeliveryService**, определенный в коде ниже).</span><span class="sxs-lookup"><span data-stu-id="10b28-184">The example in this article shows how to configure the Media Services PlayReady license delivery service (see the **ConfigureLicenseDeliveryService** method defined in the code below).</span></span> 

<span data-ttu-id="10b28-185">Обязательно измените следующий код, указав каталог, в котором расположен исходный файл MP4.</span><span class="sxs-lookup"><span data-stu-id="10b28-185">Make sure to update the following code to point to the folder where your input MP4 file is located.</span></span> <span data-ttu-id="10b28-186">Также укажите расположение файлов MediaPackager_MP4ToSmooth.xml, MediaPackager_SmoothToHLS.xml и MediaEncryptor_PlayReadyProtection.xml.</span><span class="sxs-lookup"><span data-stu-id="10b28-186">And also to where your MediaPackager_MP4ToSmooth.xml, MediaPackager_SmoothToHLS.xml, and MediaEncryptor_PlayReadyProtection.xml files are located.</span></span> <span data-ttu-id="10b28-187">Файлы MediaPackager_MP4ToSmooth.xml и MediaPackager_SmoothToHLS.xml описаны [здесь](http://msdn.microsoft.com/library/azure/hh973635.aspx), а MediaEncryptor_PlayReadyProtection.xml — [здесь](http://msdn.microsoft.com/library/azure/hh973610.aspx).</span><span class="sxs-lookup"><span data-stu-id="10b28-187">MediaPackager_MP4ToSmooth.xml and MediaPackager_SmoothToHLS.xml are defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) and MediaEncryptor_PlayReadyProtection.xml is defined in the [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace MediaServicesContentProtection
    {
        class Program
        {
            // Paths to support files (within the above base path). You can use 
            // the provided sample media files from the "SupportFiles" folder, or 
            // provide paths to your own media files below to run these samples.

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"SingleMP4\BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";


            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache the Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Used the chached credentials to create CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Load an MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file to a set of multibitrate MP4s.
                // Then, package a set of MP4s to clear Smooth Streaming.
                IAsset clearSmoothStreamAsset = ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create a common encryption content key that is used 
                // a) to set the key values in the MediaEncryptor_PlayReadyProtection.xml file
                //    that is used for encryption.
                // b) to configure the license delivery service and 
                //
                Guid keyId;
                byte[] contentKey;

                IContentKey key = CreateCommonEncryptionKey(out keyId, out contentKey);

                // The content key authorization policy must be configured by you 
                // and met by the client in order for the PlayReady license
                // to be delivered to the client. 
                // In this example the Media Services PlayReady license delivery service is used.
                ConfigureLicenseDeliveryService(key);

                // Get the Media Services PlayReady license delivery URL.
                // This URL will be assigned to the licenseAcquisitionUrl property 
                // of the MediaEncryptor_PlayReadyProtection.xml file.
                Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

                // Update the MediaEncryptor_PlayReadyProtection.xml file with the key and URL info.
                UpdatePlayReadyConfigurationXMLFile(keyId, contentKey, acquisitionUrl);

                // Create HLS encrypted with PlayReady.
                IAsset playReadyHLSAsset = CreateHLSEncryptedWithPlayReady(clearSmoothStreamAsset);
                //
                string hlsWithPlayReadyURL = playReadyHLSAsset.GetHlsUri().ToString();
                Console.WriteLine("HLS with PlayReady URL:");
                Console.WriteLine(hlsWithPlayReadyURL);
            }

            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 to multibitrate MP4s,
            /// 2 task - packages MP4s to Smooth Streaming.
            /// </summary>
            /// <returns>The output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 to Smooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeSingleMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set to Clear Smooth Streaming.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit the job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get the output asset that contains Smooth Streaming.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Create a common encryption content key that is used 
            /// to set the key values in the MediaEncryptor_PlayReadyProtection.xml file
            /// that is used for encryption.
            /// </summary>
            /// <param name="keyId"></param>
            /// <param name="contentKey"></param>
            /// <returns></returns>
            public static IContentKey CreateCommonEncryptionKey(out Guid keyId, out byte[] contentKey)
            {
                keyId = Guid.NewGuid();
                contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            /// <summary>
            /// Update your configuration .xml file dynamically.
            /// </summary>
            public static void UpdatePlayReadyConfigurationXMLFile(Guid keyId, byte[] keyValue, Uri licenseAcquisitionUrl)
            {
                string xmlFileName = Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml");

                XNamespace xmlns = "http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#";

                // Prepare the encryption task template
                XDocument doc = XDocument.Load(xmlFileName);

                var licenseAcquisitionUrlEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "licenseAcquisitionUrl")
                        .FirstOrDefault();
                var contentKeyEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "contentKey")
                        .FirstOrDefault();
                var keyIdEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "keyId")
                        .FirstOrDefault();

                // Update the "value" property.
                if (licenseAcquisitionUrlEl != null)
                    licenseAcquisitionUrlEl.Attribute("value").SetValue(licenseAcquisitionUrl.ToString());

                if (contentKeyEl != null)
                    contentKeyEl.Attribute("value").SetValue(Convert.ToBase64String(keyValue));

                if (keyIdEl != null)
                    keyIdEl.Attribute("value").SetValue(keyId);

                doc.Save(xmlFileName);
            }

            /// <summary>
            // Encrypts clear Smooth Streaming to Smooth Streaming with PlayReady.
            // Then, packages the PlayReady Smooth Streaming to HLS with PlayReady.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>The output asset.</returns>
            public static IAsset CreateHLSEncryptedWithPlayReady(IAsset clearSmoothStreamAsset)
            {
                IJob job = _context.Jobs.Create("Encrypt to HLS with PlayReady.");

                // Add task 1 - Encrypt Smooth Streaming with PlayReady 
                IAsset encryptedSmoothAsset =
                    EncryptSmoothStreamWithPlayReadyTask(job, clearSmoothStreamAsset);

                // Add task 2 - Package to HLS with PlayReady.
                PackageSmoothStreamToHLS(job, encryptedSmoothAsset);

                // Submit the job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Since we had two tasks, the OutputMediaAssets[1]
                // contains the desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[1],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">The location of the files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify the following encryption options for the AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded to Azure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: The files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use the SDK extension method to create a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });


                return asset;

            }
            /// <summary>
            /// Creates a task to encode to Adaptive Bitrate. 
            /// Adds the new task to a job.
            /// </summary>
            /// <param name="job">The job to which to add the new task.</param>
            /// <param name="asset">The input asset.</param>
            /// <returns>The output asset.</returns>
            private static IAsset EncodeSingleMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get the SDK extension method to  get a reference to the Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 to Adaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify the input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means the output asset is in the clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s",
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task to convert the MP4 file(s) to a Smooth Streaming asset.
            /// Adds the new task to a job.
            /// </summary>
            /// <param name="job">The job to which to add the new task.</param>
            /// <param name="asset">The input asset.</param>
            /// <returns>The output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get the SDK extension method to  get a reference to the Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles,
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task to convert adaptive bitrate to Smooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 to Smooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify the input Asset, which is the output Asset from the first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means the output asset is in the clear (unencrypted).
                IAsset smoothOutputAsset =
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Streaming",
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }


            /// <summary>
            /// Converts Smooth Stream to HLS.
            /// </summary>
            /// <param name="job">The job to which to add the new task.</param>
            /// <param name="asset">The Smooth Stream asset.</param>
            /// <returns>The asset that was packaged to HLS.</returns>
            private static IAsset PackageSmoothStreamToHLS(IJob job, IAsset smoothStreamAsset)
            {
                // Get the SDK extension method to  get a reference to the Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Read the configuration data into a string. 
                //
                string configuration = File.ReadAllText(
                            Path.Combine(_configurationXMLFiles,
                                        @"MediaPackager_SmoothToHLS.xml"));

                // Create a task with the encoding details, using a configuration file.
                ITask task = job.Tasks.AddNew("My Smooth to HLS Task",
                   processor,
                   configuration,
                   TaskOptions.ProtectedConfiguration);

                // Specify the input asset to be encoded.
                task.InputAssets.Add(smoothStreamAsset);

                // Add an output asset to contain the results of the job. 
                IAsset outputAsset =
                    task.OutputAssets.AddNew("HLS asset", AssetCreationOptions.None);


                return outputAsset;
            }

            /// <summary>
            /// Creates a task to encrypt Smooth Streaming with PlayReady.
            /// Note: Do deliver DASH, make sure to set the useSencBox and adjustSubSamples 
            /// configuration properties to true.
            /// </summary>
            /// <param name="job">The job to which to add the new task.</param>
            /// <param name="asset">The input asset.</param>
            /// <returns>The output asset.</returns>
            private static IAsset EncryptSmoothStreamWithPlayReadyTask(IJob job, IAsset asset)
            {
                // Get the SDK extension method to  get a reference to the Azure Media Encryptor.
                IMediaProcessor playreadyProcessor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaEncryptor);

                // Read the configuration XML.
                //
                // Note that the configuration defined in MediaEncryptor_PlayReadyProtection.xml
                // is using keySeedValue. It is recommended that you do this only for testing 
                // and not in production. For more information, see 
                // http://msdn.microsoft.com/library/windowsazure/dn189154.aspx.
                //
                string configPlayReady = File.ReadAllText(Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml"));

                ITask playreadyTask = job.Tasks.AddNew("My PlayReady Task",
                   playreadyProcessor,
                   configPlayReady,
                   TaskOptions.ProtectedConfiguration);

                playreadyTask.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.CommonEncryptionProtected.
                IAsset playreadyAsset = playreadyTask.OutputAssets.AddNew(
                                                "PlayReady Smooth Streaming",
                                                AssetCreationOptions.CommonEncryptionProtected);


                return playreadyAsset;
            }


            /// <summary>
            /// Configures authorization policy for the content key. 
            /// </summary>
            /// <param name="contentKey">The content key.</param>
            static public void ConfigureLicenseDeliveryService(IContentKey contentKey)
            {
                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                    new ContentKeyAuthorizationPolicyRestriction 
                    { 
                        Name = "Open", 
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                        Requirements = null
                    }
                };

                // Configure PlayReady license template.
                string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                IContentKeyAuthorizationPolicyOption policyOption =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, newLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(policyOption);

                // Associate the content key authorization policy with the content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            static private string ConfigurePlayReadyLicenseTemplate()
            {
                // The following code configures PlayReady License Template using .NET classes
                // and returns the XML string.

                PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }
            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }

        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="10b28-188">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="10b28-188">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="10b28-189">Отзывы</span><span class="sxs-lookup"><span data-stu-id="10b28-189">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

