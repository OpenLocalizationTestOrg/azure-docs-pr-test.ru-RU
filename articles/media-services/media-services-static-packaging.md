---
title: "задачи статической упаковки tooaccomplish Azure Media Packager aaaUsing | Документы Microsoft"
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
ms.openlocfilehash: 64e8ba217bcd3074f5819ac3b74d2969432db5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-media-packager-tooaccomplish-static-packaging-tasks"></a><span data-ttu-id="053f7-103">С помощью Azure Media Packager tooaccomplish статической упаковки задач</span><span class="sxs-lookup"><span data-stu-id="053f7-103">Using Azure Media Packager tooaccomplish static packaging tasks</span></span>
> [!NOTE]
> <span data-ttu-id="053f7-104">Hello Дата окончания жизненного цикла для Microsoft Azure Media Packager и Microsoft Azure Media Encryptor была расширена tooMarch 1, 2017 г.</span><span class="sxs-lookup"><span data-stu-id="053f7-104">hello end of life date for Microsoft Azure Media Packager and Microsoft Azure Media Encryptor has been extended tooMarch 1, 2017.</span></span> <span data-ttu-id="053f7-105">До этой даты функциональные возможности hello эти процессоры будут добавлены tooMedia стандартный кодировщик (MES).</span><span class="sxs-lookup"><span data-stu-id="053f7-105">Before that date, hello functionalities of these processors will be added tooMedia Encoder Standard (MES).</span></span> <span data-ttu-id="053f7-106">Клиенты будут предоставлены инструкции о том, как toomigrate tooMES заданий toosend их рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="053f7-106">Customers will be provided with instructions on how toomigrate their workflows toosend Jobs tooMES.</span></span> <span data-ttu-id="053f7-107">Функциями преобразования формата и шифрования можно также пользоваться посредством динамической упаковки и динамического шифрования.</span><span class="sxs-lookup"><span data-stu-id="053f7-107">Format conversion and encryption capabilities may also be available through dynamic packaging and dynamic encryption.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="053f7-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="053f7-108">Overview</span></span>
<span data-ttu-id="053f7-109">В порядок toodeliver цифрового видео по hello hello Интернету необходимо сжать мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="053f7-109">In order toodeliver digital video over hello internet you must compress hello media.</span></span> <span data-ttu-id="053f7-110">Цифровые видеофайлы довольно велики и может быть слишком большой toodeliver hello Интернет или для клиентов устройств toodisplay должным образом.</span><span class="sxs-lookup"><span data-stu-id="053f7-110">Digital video files are quite large and may be too big toodeliver over hello internet or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="053f7-111">Кодирование-это процесс сжатия видео и аудио, чтобы ваши клиенты могли просмотреть мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="053f7-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span> <span data-ttu-id="053f7-112">После кодирования видео его можно поместить в различные контейнеры.</span><span class="sxs-lookup"><span data-stu-id="053f7-112">Once a video has been encoded it can be placed into different file containers.</span></span> <span data-ttu-id="053f7-113">Процесс помещения кодированных мультимедийных данных в контейнер Hello называется упаковкой.</span><span class="sxs-lookup"><span data-stu-id="053f7-113">hello process of placing encoded media into a container is called packaging.</span></span> <span data-ttu-id="053f7-114">Например можно взять MP4-файл и преобразовать его в содержимое Smooth Streaming или HLS с помощью hello Azure Media Packager.</span><span class="sxs-lookup"><span data-stu-id="053f7-114">For example, you can take an MP4 file and convert it into Smooth Streaming or HLS content by using hello Azure Media Packager.</span></span> 

<span data-ttu-id="053f7-115">Службы мультимедиа поддерживают динамическую и статическую упаковку.</span><span class="sxs-lookup"><span data-stu-id="053f7-115">Media Services supports dynamic and static packaging.</span></span> <span data-ttu-id="053f7-116">При использовании статической упаковки необходимо toocreate копию содержимого в каждом формате, который необходим клиентам.</span><span class="sxs-lookup"><span data-stu-id="053f7-116">When using static packaging you need toocreate a copy of your content in each format required by your customers.</span></span> <span data-ttu-id="053f7-117">При динамической упаковки достаточно будет toocreate актив, содержащий набор файлов MP4 или Smooth Streaming с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="053f7-117">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 or Smooth Streaming files.</span></span> <span data-ttu-id="053f7-118">Затем, на основании hello формата, указанного в манифесте hello или фрагмента запроса, hello сервер проверит получение вашими пользователями потока hello в протоколе hello выбранный потоковой передачи по требованию.</span><span class="sxs-lookup"><span data-stu-id="053f7-118">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that your users receive hello stream in hello protocol they have chosen.</span></span> <span data-ttu-id="053f7-119">В результате достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа будут создавать и обслуживать соответствующий ответ hello на основе запросов клиента.</span><span class="sxs-lookup"><span data-stu-id="053f7-119">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

> [!NOTE]
> <span data-ttu-id="053f7-120">Рекомендуется toouse [динамической упаковки](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="053f7-120">It is recommended toouse [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>
> 
> 

<span data-ttu-id="053f7-121">Однако существуют некоторые сценарии, в которых требуется использовать статическую упаковку.</span><span class="sxs-lookup"><span data-stu-id="053f7-121">However, there are some scenarios that require static packaging:</span></span> 

* <span data-ttu-id="053f7-122">Проверка MP4-файлов с переменной скоростью, закодированных с помощью внешних кодировщиков (например, кодировщиков сторонних поставщиков).</span><span class="sxs-lookup"><span data-stu-id="053f7-122">Validating adaptive bitrate MP4s encoded with external encoders (for example, using third party encoders).</span></span>

<span data-ttu-id="053f7-123">Также можно использовать статическую упаковку tooperform hello следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="053f7-123">You can also use static packaging tooperform hello following tasks.</span></span> <span data-ttu-id="053f7-124">Тем не менее рекомендуется toouse динамического шифрования.</span><span class="sxs-lookup"><span data-stu-id="053f7-124">However it is recommended toouse dynamic encryption.</span></span>

* <span data-ttu-id="053f7-125">Использование статического шифрования tooprotect Smooth и MPEG DASH с помощью PlayReady</span><span class="sxs-lookup"><span data-stu-id="053f7-125">Using static encryption tooprotect your Smooth and MPEG DASH with PlayReady</span></span>
* <span data-ttu-id="053f7-126">Использование статического шифрования tooprotect HLSv3 с помощью AES-128</span><span class="sxs-lookup"><span data-stu-id="053f7-126">Using static encryption tooprotect HLSv3 with AES-128</span></span>
* <span data-ttu-id="053f7-127">Использование статического шифрования tooprotect HLSv3 с помощью PlayReady</span><span class="sxs-lookup"><span data-stu-id="053f7-127">Using static encryption tooprotect HLSv3 with PlayReady</span></span>

## <a name="validating-adaptive-bitrate-mp4s-encoded-with-external-encoders"></a><span data-ttu-id="053f7-128">Проверка MP4-файлов с переменной скоростью, закодированных с помощью внешних кодировщиков</span><span class="sxs-lookup"><span data-stu-id="053f7-128">Validating Adaptive Bitrate MP4s Encoded with External Encoders</span></span>
<span data-ttu-id="053f7-129">Если вы хотите toouse набор файлов MP4 с адаптивной скоростью (с несколькими скоростями), не закодированных с помощью кодировщика служб мультимедиа, следует проверить файлы перед дальнейшей обработкой.</span><span class="sxs-lookup"><span data-stu-id="053f7-129">If you want toouse a set of adaptive bitrate (multi-bitrate) MP4 files that were not encoded with Media Services' encoders, you should validate your files before further processing.</span></span> <span data-ttu-id="053f7-130">Hello Media Services Packager можно проверить ресурс, содержащий набор MP4-файлов и проверьте, можно ли активов hello упакованных tooSmooth Streaming или HLS.</span><span class="sxs-lookup"><span data-stu-id="053f7-130">hello Media Services Packager can validate an asset that contains a set of MP4 files and check whether hello asset can be packaged tooSmooth Streaming or HLS.</span></span> <span data-ttu-id="053f7-131">В случае сбоя задачи проверки hello задания hello, обрабатывающее задачу hello завершается с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="053f7-131">If hello validation task fails, hello job that was processing hello task will complete with an error.</span></span> <span data-ttu-id="053f7-132">Hello XML, определяющий стиль для задачи проверки hello можно найти в hello hello [предустановки задачи для Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="053f7-132">hello XML that defines hello preset for hello validation task can be found in hello [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

> [!NOTE]
> <span data-ttu-id="053f7-133">Используйте стандартный кодировщик мультимедиа tooproduce hello или toovalidate Media Services Packager hello содержимого в порядке tooavoid проблемам.</span><span class="sxs-lookup"><span data-stu-id="053f7-133">Use hello Media Encoder Standard tooproduce or hello Media Services Packager toovalidate your content in order tooavoid runtime issues.</span></span> <span data-ttu-id="053f7-134">Если сервер потоковой передачи по требованию hello не может tooparse к исходным файлам во время выполнения, появится сообщение об ошибке HTTP 1.1 «415 неподдерживаемый тип носителя».</span><span class="sxs-lookup"><span data-stu-id="053f7-134">If hello On-Demand Streaming server is not able tooparse your source files at runtime, you will receive HTTP 1.1 error “415 Unsupported Media Type”.</span></span> <span data-ttu-id="053f7-135">Исходные файлы многократно вызывая hello server toofail tooparse влияет на производительность сервера потоковой передачи по требованию hello и может привести к снижению tooserving доступной пропускной способности hello других запросов.</span><span class="sxs-lookup"><span data-stu-id="053f7-135">Repeatedly causing hello server toofail tooparse your source files affects performance of hello On-Demand Streaming server and may reduce hello bandwidth available tooserving other requests.</span></span> <span data-ttu-id="053f7-136">Службы мультимедиа Azure предлагают соглашение уровень службы (SLA) на его службы потоковой передачи по требованию; Однако это соглашение не применяется, если сервер hello используется неправильно hello как описано выше.</span><span class="sxs-lookup"><span data-stu-id="053f7-136">Azure Media Services offers a Service Level Agreement (SLA) on its On-Demand Streaming services; however, this SLA cannot be honored if hello server is misused in hello fashion described above.</span></span>
> 
> 

<span data-ttu-id="053f7-137">В этом разделе показано, как tooprocess hello проверки задачи.</span><span class="sxs-lookup"><span data-stu-id="053f7-137">This section shows how tooprocess hello validation task.</span></span> <span data-ttu-id="053f7-138">Здесь также показано, как toosee hello состояние и hello сообщение об ошибке hello задания, завершенного с JobStatus.Error.</span><span class="sxs-lookup"><span data-stu-id="053f7-138">It also shows how toosee hello status and hello error message of hello job that completes with JobStatus.Error.</span></span>

<span data-ttu-id="053f7-139">toovalidate вашей MP4 файлы в Media Services Packager, необходимо создать собственный файл манифеста (.ism) и передать его вместе с hello исходные файлы в hello учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="053f7-139">toovalidate your MP4 files with Media Services Packager, you must create your own manifest (.ism) file and upload it together with hello source files into hello Media Services account.</span></span> <span data-ttu-id="053f7-140">Ниже приведен образец hello ISM-файла созданного hello стандартный кодировщик мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="053f7-140">Below is a sample of hello .ism file produced by hello Media Encoder Standard.</span></span> <span data-ttu-id="053f7-141">Hello имена файлов чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="053f7-141">hello file names are case sensitive.</span></span> <span data-ttu-id="053f7-142">Кроме того убедитесь, что текст hello в hello ISM-файле представлен в кодировке UTF-8.</span><span class="sxs-lookup"><span data-stu-id="053f7-142">Also, make sure hello text in hello .ism file is encoded with UTF-8.</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
    <!-- Tells hello server that these input files are MP4s – specific tooDynamic Packaging -->
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

<span data-ttu-id="053f7-143">После получения hello адаптивного битрейта MP4 в набор, который можно воспользоваться преимуществами динамической упаковки.</span><span class="sxs-lookup"><span data-stu-id="053f7-143">Once you have hello adaptive bitrate MP4 set you can take advantage of Dynamic Packaging.</span></span> <span data-ttu-id="053f7-144">Динамическая упаковка позволяет toodeliver потоков в hello указан протокол без дальнейшей упаковки.</span><span class="sxs-lookup"><span data-stu-id="053f7-144">Dynamic Packaging allows you toodeliver streams in hello specified protocol without further packaging.</span></span> <span data-ttu-id="053f7-145">Дополнительные сведения см. в статье [Динамическая упаковка](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="053f7-145">For more information, see [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="053f7-146">Следующий пример кода использует расширения SDK .NET служб мультимедиа Azure Hello.</span><span class="sxs-lookup"><span data-stu-id="053f7-146">hello following code sample uses Azure Media Services .NET SDK Extensions.</span></span>  <span data-ttu-id="053f7-147">Убедитесь, что tooupdate hello кода toopoint toohello каталогу где расположены входные MP4-файлы и файл .ism.</span><span class="sxs-lookup"><span data-stu-id="053f7-147">Make sure tooupdate hello code toopoint toohello folder where your input MP4 files and .ism file are located.</span></span> <span data-ttu-id="053f7-148">А также toowhere MediaPackager_ValidateTask.xml расположен файл.</span><span class="sxs-lookup"><span data-stu-id="053f7-148">And also toowhere your MediaPackager_ValidateTask.xml file is located.</span></span> <span data-ttu-id="053f7-149">Этот XML-файл определяется в разделе [Предустановка задачи для Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) .</span><span class="sxs-lookup"><span data-stu-id="053f7-149">This XML file is defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

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

            // hello MultibitrateMP4Files folder should also
            // contain hello .ism manifest file.
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
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Ingest a set of multibitrate MP4s.
                //
                // Use hello SDK extension method toocreate a new asset by 
                // uploading files from a local directory.
                IAsset multibitrateMP4sAsset = _context.Assets.CreateFromFolder(
                    _multibitrateMP4s,
                    AssetCreationOptions.None,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                // Use Azure Media Packager toovalidate hello files.
                IAsset validatedMP4s =
                    ValidateMultibitrateMP4s(multibitrateMP4sAsset);

                // Publish hello asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    validatedMP4s,
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                                     // Get hello streaming URLs.
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
                IJob job = _context.Jobs.Create("MP4 validation and converstion tooSmooth Stream job.");

                // Read hello task configuration data into a string. 
                string configMp4Validation = File.ReadAllText(Path.Combine(
                        _configurationXMLFiles,
                        "MediaPackager_ValidateTask.xml"));

                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Create a task with hello conversion details, using hello configuration data. 
                ITask task = job.Tasks.AddNew("Mp4 Validation Task",
                    processor,
                    configMp4Validation,
                    TaskOptions.None);

                // Specify hello input asset toobe validated.
                task.InputAssets.Add(multibitrateMP4sAsset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted). 
                task.OutputAssets.AddNew("Validated output asset",
                        AssetCreationOptions.None);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // If hello validation task fails and job completes with JobState.Error,
                // display hello error message and throw an exception.
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
                    throw new Exception("hello specified multi-bitrate MP4 set is not valid.");
                }


                return job.OutputMediaAssets[0];
            }

            static void SetISMFileAsPrimary(IAsset asset)
            {
                var ismAssetFiles = asset.AssetFiles.ToList().
                    Where(f => f.Name.EndsWith(".ism", StringComparison.OrdinalIgnoreCase)).ToArray();

                // hello following code assigns hello first .ism file as hello primary file in hello asset.
                // An asset should have one .ism file.  
                ismAssetFiles.First().IsPrimary = true;
                ismAssetFiles.First().Update();
            }
        }
    }

## <a name="using-static-encryption-tooprotect-your-smooth-and-mpeg-dash-with-playready"></a><span data-ttu-id="053f7-150">Использование статического шифрования tooProtect Smooth и MPEG DASH с помощью PlayReady</span><span class="sxs-lookup"><span data-stu-id="053f7-150">Using Static Encryption tooProtect your Smooth and MPEG DASH with PlayReady</span></span>
<span data-ttu-id="053f7-151">Если вы хотите tooprotect контента с помощью PlayReady, у вас есть выбрать использование [динамического шифрования](media-services-protect-with-drm.md) (hello рекомендуемый параметр) и статическим шифрованием (как описано в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="053f7-151">If you want tooprotect your content with PlayReady, you have a choice of using [dynamic encryption](media-services-protect-with-drm.md) (hello recommended option) or static encryption (as described in this section).</span></span>

<span data-ttu-id="053f7-152">пример Hello в этом разделе кодирует мезонинный файл (в данном случае MP4) в файлы MP4 с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="053f7-152">hello example in this section encodes a mezzanine file (in this case MP4) into adaptive bitrate MP4 files.</span></span> <span data-ttu-id="053f7-153">Затем файлы MP4 упаковываются в Smooth Streaming и шифруются с помощью PlayReady.</span><span class="sxs-lookup"><span data-stu-id="053f7-153">It then packages MP4s into Smooth Streaming and then encrypts Smooth Streaming with PlayReady.</span></span> <span data-ttu-id="053f7-154">В результате не может toostream Smooth Streaming или MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="053f7-154">As a result you are able toostream Smooth Streaming or MPEG DASH.</span></span>

<span data-ttu-id="053f7-155">Службы мультимедиа теперь обеспечивают доставку лицензий Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="053f7-155">Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="053f7-156">Hello пример в этой статье показано, каким образом службы доставки лицензий tooconfigure hello PlayReady служб мультимедиа (см. метод ConfigureLicenseDeliveryService hello, определенный в следующем примере кода hello).</span><span class="sxs-lookup"><span data-stu-id="053f7-156">hello example in this article shows how tooconfigure hello Media Services PlayReady license delivery service (see hello ConfigureLicenseDeliveryService method defined in hello code below).</span></span> <span data-ttu-id="053f7-157">Дополнительные сведения о службе доставки лицензий PlayReady служб мультимедиа см. в статье [Использование общего динамического шифрования PlayReady и (или) Widevine DRM](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="053f7-157">For more information about Media Services PlayReady license delivery service, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="053f7-158">toodeliver MPEG DASH с шифрованием PlayReady, убедитесь, что toouse параметры CENC путем задания свойств useSencBox и adjustSubSamples hello (описано в hello [предустановки задачи для Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) раздела) tootrue.</span><span class="sxs-lookup"><span data-stu-id="053f7-158">toodeliver MPEG DASH encrypted with PlayReady, make sure toouse CENC options by setting hello useSencBox and adjustSubSamples properties (described in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic) tootrue.</span></span>  
> 
> 

<span data-ttu-id="053f7-159">Убедитесь, что hello tooupdate следующая папка toohello toopoint кода, где расположен входной MP4-файл.</span><span class="sxs-lookup"><span data-stu-id="053f7-159">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span>

<span data-ttu-id="053f7-160">Пользователи, а также toowhere файлы MediaPackager_MP4ToSmooth.xml и MediaEncryptor_PlayReadyProtection.xml.</span><span class="sxs-lookup"><span data-stu-id="053f7-160">And also toowhere your MediaPackager_MP4ToSmooth.xml and MediaEncryptor_PlayReadyProtection.xml files are located.</span></span> <span data-ttu-id="053f7-161">MediaPackager_MP4ToSmooth.xml определяется в [предустановки задачи для Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) и MediaEncryptor_PlayReadyProtection.xml определяется в hello [предустановки задачи для Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="053f7-161">MediaPackager_MP4ToSmooth.xml is defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) and MediaEncryptor_PlayReadyProtection.xml is defined in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic.</span></span> 

<span data-ttu-id="053f7-162">пример Hello определяет метод UpdatePlayReadyConfigurationXMLFile hello, можно использовать файл MediaEncryptor_PlayReadyProtection.xml toodynamically обновления hello.</span><span class="sxs-lookup"><span data-stu-id="053f7-162">hello example defines hello UpdatePlayReadyConfigurationXMLFile method that you can use toodynamically update hello MediaEncryptor_PlayReadyProtection.xml file.</span></span> <span data-ttu-id="053f7-163">Если у вас есть hello доступное начальное значение ключа, можно использовать hello CommonEncryption.GeneratePlayReadyContentKey метод toogenerate hello ключ контента на основе значений hello keySeedValue и KeyId.</span><span class="sxs-lookup"><span data-stu-id="053f7-163">If you have hello key seed available, you can use hello CommonEncryption.GeneratePlayReadyContentKey method toogenerate hello content key based on hello keySeedValue and KeyId values.</span></span>

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
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Encoding and encrypting assets //////////////////////
                // Load a single MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset =
                    ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create a common encryption content key that is used 
                // a) tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
                //    that is used for encryption.
                // b) tooconfigure hello license delivery service and 
                //
                Guid keyId;
                byte[] contentKey;

                IContentKey key = CreateCommonEncryptionKey(out keyId, out contentKey);

                // hello content key authorization policy must be configured by you 
                // and met by hello client in order for hello PlayReady license
                // toobe delivered toohello client. 
                // In this example hello Media Services PlayReady license delivery service is used.
                ConfigureLicenseDeliveryService(key);

                // Get hello Media Services PlayReady license delivery URL.
                // This URL will be assigned toohello licenseAcquisitionUrl property 
                // of hello MediaEncryptor_PlayReadyProtection.xml file.
                Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

                // Update hello MediaEncryptor_PlayReadyProtection.xml file with hello key and URL info.
                UpdatePlayReadyConfigurationXMLFile(keyId, contentKey, acquisitionUrl);


                // Encrypt your clear Smooth Streaming tooSmooth Streaming with PlayReady.
                IAsset outputAsset = CreateSmoothStreamEncryptedWithPlayReady(clearSmoothStreamAsset);


                // You can use hello http://smf.cloudapp.net/healthmonitor player 
                // tootest hello smoothStreamURL URL.
                string smoothStreamURL = outputAsset.GetSmoothStreamingUri().ToString();
                Console.WriteLine("Smooth Streaming URL:");
                Console.WriteLine(smoothStreamURL);

                // You can use hello http://dashif.org/reference/players/javascript/ player 
                // tootest hello dashURL URL.
                string dashURL = outputAsset.GetMpegDashUri().ToString();
                Console.WriteLine("MPEG DASH URL:");
                Console.WriteLine(dashURL);
            }

            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Stream.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains hello Smooth Streaming asset.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Encrypts Smooth Stream with PlayReady.
            /// Then creates a Smooth Streaming Url.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateSmoothStreamEncryptedWithPlayReady(IAsset clearSmoothStreamAsset)
            {
                // Create a job.
                IJob job = _context.Jobs.Create("Encrypt tooPlayReady Smooth Streaming.");

                // Add task 1 - Encrypt Smooth Streaming with PlayReady 
                IAsset encryptedSmoothAsset =
                    EncryptSmoothStreamWithPlayReadyTask(job, clearSmoothStreamAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // hello OutputMediaAssets[0] contains hello desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[0],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[0];
            }

            /// <summary>
            /// Create a common encryption content key that is used 
            /// tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
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

                // Prepare hello encryption task template
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

                // Update hello "value" property.
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
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
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
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s",
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles,
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset =
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Stream",
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }


            /// <summary>
            /// Creates a task tooencrypt Smooth Streaming with PlayReady.
            /// Note: toodeliver DASH, make sure tooset hello useSencBox and adjustSubSamples 
            /// configuration properties tootrue. 
            /// In this example, MediaEncryptor_PlayReadyProtection.xml contains configuration.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncryptSmoothStreamWithPlayReadyTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Encryptor.
                IMediaProcessor playreadyProcessor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaEncryptor);

                // Read hello configuration XML.
                //
                // Note that hello configuration defined in MediaEncryptor_PlayReadyProtection.xml
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

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.CommonEncryptionProtected.
                IAsset playreadyAsset = playreadyTask.OutputAssets.AddNew(
                                                "PlayReady Smooth Streaming",
                                                AssetCreationOptions.CommonEncryptionProtected);

                return playreadyAsset;
            }

            /// <summary>
            /// Configures authorization policy for hello content key. 
            /// </summary>
            /// <param name="contentKey">hello content key.</param>
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

                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            static private string ConfigurePlayReadyLicenseTemplate()
            {
                // hello following code configures PlayReady License Template using .NET classes
                // and returns hello XML string.

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

## <a name="using-static-encryption-tooprotect-hlsv3-with-aes-128"></a><span data-ttu-id="053f7-164">Использование статического шифрования tooProtect HLSv3 с помощью AES-128</span><span class="sxs-lookup"><span data-stu-id="053f7-164">Using Static Encryption tooProtect HLSv3 with AES-128</span></span>
<span data-ttu-id="053f7-165">Если вы хотите tooencrypt контента HLS с помощью AES-128, у вас есть выбрать использование динамического шифрования (hello рекомендуемый параметр) и статическим шифрованием (как показано в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="053f7-165">If you want tooencrypt your HLS with AES-128, you have a choice of using dynamic encryption (hello recommended option) or static encryption (as shown in this section).</span></span> <span data-ttu-id="053f7-166">Если вы решите toouse динамического шифрования, см. раздел [с помощью динамического шифрования AES-128 и службы доставки ключей](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="053f7-166">If you decide toouse dynamic encryption, see [Using AES-128 Dynamic Encryption and Key Delivery Service](media-services-protect-with-aes128.md).</span></span>

> [!NOTE]
> <span data-ttu-id="053f7-167">Чтобы tooconvert контент в HLS, вам необходимо сначала преобразовать или закодировать контент в Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="053f7-167">In order tooconvert your content into HLS, you must first convert/encode your content into Smooth Streaming.</span></span>
> <span data-ttu-id="053f7-168">Убедитесь также, для hello HLS с шифрованием AES tooget hello tooset убедиться, что следующие свойства в файле MediaPackager_SmoothToHLS.xml: hello набора шифрования tootrue свойства, значение ключа набора hello и hello keyuri значение toopoint tooyour authentication\ сервер авторизации.</span><span class="sxs-lookup"><span data-stu-id="053f7-168">Also, for hello HLS tooget encrypted with AES make sure tooset hello following properties in your MediaPackager_SmoothToHLS.xml file: set hello encrypt property tootrue, set hello key value, and hello keyuri value toopoint tooyour authentication\authorization server.</span></span>
> <span data-ttu-id="053f7-169">Создайте файл ключа и поместить его в контейнер ресурса hello служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="053f7-169">Media Services will create a key file and place it in hello asset container.</span></span> <span data-ttu-id="053f7-170">Необходимо скопировать файл tooyour hello /asset-containerguid/*.key сервера (или создать свой собственный файл ключа) и удалите hello Key-файл из контейнера актива hello.</span><span class="sxs-lookup"><span data-stu-id="053f7-170">You should copy hello /asset-containerguid/*.key file tooyour server (or create your own key file) and then delete hello *.key file from hello asset container.</span></span>
> 
> 

<span data-ttu-id="053f7-171">Hello пример в этом разделе кодирует мезонинный файл (в данном случае MP4) в Многоскоростные MP4, файлы, а затем упаковывает MP4-файлов в Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="053f7-171">hello example in this section encodes a mezzanine file (in this case MP4) into multibitrate MP4 files and then packages MP4s into Smooth Streaming.</span></span> <span data-ttu-id="053f7-172">После этого он упаковывает содержимое в формате Smooth Streaming в формат HTTP Live Streaming (HLS), зашифрованный с помощью 128-разрядного шифрования потока AES.</span><span class="sxs-lookup"><span data-stu-id="053f7-172">It then packages Smooth Streaming into HTTP Live Streaming (HLS) encrypted with Advanced Encryption Standard (AES) 128-bit stream encryption.</span></span> <span data-ttu-id="053f7-173">Убедитесь, что hello tooupdate следующая папка toohello toopoint кода, где расположен входной MP4-файл.</span><span class="sxs-lookup"><span data-stu-id="053f7-173">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span> <span data-ttu-id="053f7-174">Пользователи, а также toowhere MediaPackager_MP4ToSmooth.xml и MediaPackager_SmoothToHLS.xml файлов конфигурации.</span><span class="sxs-lookup"><span data-stu-id="053f7-174">And also toowhere your MediaPackager_MP4ToSmooth.xml and MediaPackager_SmoothToHLS.xml configuration files are located.</span></span> <span data-ttu-id="053f7-175">Определение hello для этих файлов можно найти в hello [предустановки задачи для Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="053f7-175">You can find hello definition for these files in hello [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

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
            // Paths toosupport files (within hello above base path). You can use 
            // hello provided sample media files from hello "SupportFiles" folder, or 
            // provide paths tooyour own media files below toorun these samples.

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
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName, 
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Encoding and encrypting assets //////////////////////

                // Load an MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset = ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create HLS encrypted with AES.
                IAsset HLSEncryptedWithAESAsset = CreateHLSEncryptedWithAES(clearSmoothStreamAsset);

                // You can use hello following player tootest hello HLS with AES stream.
                // http://apps.microsoft.com/windows/app/3ivx-hls-player/f79ce7d0-2993-4658-bc4e-83dc182a0614 
                string hlsWithAESURL = HLSEncryptedWithAESAsset.GetHlsUri().ToString();
                Console.WriteLine("HLS with AES URL:");
                Console.WriteLine(hlsWithAESURL);
            }


            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeSingleMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Streaming.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains Smooth Streaming.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Encrypts an HLS with AES-128.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateHLSEncryptedWithAES(IAsset clearSmoothStreamAsset)
            {
                IJob job = _context.Jobs.Create("Encrypt tooHLS with AES.");

                // Add task 1 - Package clear Smooth Streaming tooHLS with AES.
                PackageSmoothStreamToHLS(job, clearSmoothStreamAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // hello OutputMediaAssets[0] contains hello desired asset.
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
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
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
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeSingleMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s", 
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles, 
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset = 
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Streaming", 
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }

            /// <summary>
            /// Converts Smooth Streaming tooHLS.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello Smooth Streaming asset.</param>
            /// <returns>hello asset that was packaged tooHLS.</returns>
            private static IAsset PackageSmoothStreamToHLS(IJob job, IAsset smoothStreamAsset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Read hello configuration data into a string. 
                // For hello HLS tooget encrypted with AES make sure tooset the
                // encrypt configuration property tootrue.
                //
                // In production, it is recommended toodo hello following:
                //    Set a Key url for your authn/authz server.
                //    Copy hello /asset-containerguid/*.key file tooyour server (or craft a key file for yourself).
                //    Delete *.key from hello asset container.
                //
                string configuration = File.ReadAllText(Path.Combine(_configurationXMLFiles, @"MediaPackager_SmoothToHLS.xml"));

                // Create a task with hello encoding details, using a configuration file.
                ITask task = job.Tasks.AddNew("My Smooth Streaming tooHLS Task",
                   processor,
                   configuration,
                   TaskOptions.ProtectedConfiguration);

                // Specify hello input asset toobe encoded.
                task.InputAssets.Add(smoothStreamAsset);

                // Add an output asset toocontain hello results of hello job. 
                IAsset outputAsset = 
                    task.OutputAssets.AddNew("HLS asset", AssetCreationOptions.None);


                return outputAsset;
            }
        }
    }

## <a name="using-static-encryption-tooprotect-hlsv3-with-playready"></a><span data-ttu-id="053f7-176">Использование статического шифрования tooProtect HLSv3 с помощью PlayReady</span><span class="sxs-lookup"><span data-stu-id="053f7-176">Using Static Encryption tooProtect HLSv3 with PlayReady</span></span>
<span data-ttu-id="053f7-177">Если вы хотите tooprotect контента с помощью PlayReady, у вас есть выбрать использование [динамического шифрования](media-services-protect-with-drm.md) (hello рекомендуемый параметр) и статическим шифрованием (как описано в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="053f7-177">If you want tooprotect your content with PlayReady, you have a choice of using [dynamic encryption](media-services-protect-with-drm.md) (hello recommended option) or static encryption (as described in this section).</span></span>

> [!NOTE]
> <span data-ttu-id="053f7-178">В порядке tooprotect контент с помощью PlayReady вам необходимо сначала преобразовать или закодировать контент в формат Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="053f7-178">In order tooprotect your content using PlayReady you must first convert/encode your content into a Smooth Streaming format.</span></span>
> 
> 

<span data-ttu-id="053f7-179">пример Hello в этом разделе кодирует мезонинный файл (в данном случае MP4) в Многоскоростные MP4-файлы.</span><span class="sxs-lookup"><span data-stu-id="053f7-179">hello example in this section encodes a mezzanine file (in this case MP4) into multibitrate MP4 files.</span></span> <span data-ttu-id="053f7-180">Затем файлы MP4 упаковываются в Smooth Streaming и шифруются с помощью PlayReady.</span><span class="sxs-lookup"><span data-stu-id="053f7-180">It then packages MP4s into Smooth Streaming and encrypts Smooth Streaming with PlayReady.</span></span> <span data-ttu-id="053f7-181">tooproduce HTTP Live Streaming (HLS) с шифрованием PlayReady, актив PlayReady Smooth Streaming hello должен toobe запаковать в HLS.</span><span class="sxs-lookup"><span data-stu-id="053f7-181">tooproduce HTTP Live Streaming (HLS) encrypted with PlayReady, hello PlayReady Smooth Streaming asset needs toobe packaged into HLS.</span></span> <span data-ttu-id="053f7-182">В этом разделе показано, как tooperform описанных действий.</span><span class="sxs-lookup"><span data-stu-id="053f7-182">This topic demonstrates how tooperform all these steps.</span></span>

<span data-ttu-id="053f7-183">Службы мультимедиа теперь обеспечивают доставку лицензий Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="053f7-183">Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="053f7-184">Hello пример в этой статье показано, каким образом службы доставки лицензий hello tooconfigure Media Services PlayReady (в разделе hello **ConfigureLicenseDeliveryService** метод, определенный в следующем примере кода hello).</span><span class="sxs-lookup"><span data-stu-id="053f7-184">hello example in this article shows how tooconfigure hello Media Services PlayReady license delivery service (see hello **ConfigureLicenseDeliveryService** method defined in hello code below).</span></span> 

<span data-ttu-id="053f7-185">Убедитесь, что hello tooupdate следующая папка toohello toopoint кода, где расположен входной MP4-файл.</span><span class="sxs-lookup"><span data-stu-id="053f7-185">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span> <span data-ttu-id="053f7-186">Пользователи, а также toowhere MediaPackager_MP4ToSmooth.xml, MediaPackager_SmoothToHLS.xml и MediaEncryptor_PlayReadyProtection.xml файлов.</span><span class="sxs-lookup"><span data-stu-id="053f7-186">And also toowhere your MediaPackager_MP4ToSmooth.xml, MediaPackager_SmoothToHLS.xml, and MediaEncryptor_PlayReadyProtection.xml files are located.</span></span> <span data-ttu-id="053f7-187">MediaPackager_MP4ToSmooth.xml и MediaPackager_SmoothToHLS.xml определяются в [предустановки задачи для Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) и MediaEncryptor_PlayReadyProtection.xml определяется в hello [предустановки задачи для Azure Шифратор мультимедиа](http://msdn.microsoft.com/library/azure/hh973610.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="053f7-187">MediaPackager_MP4ToSmooth.xml and MediaPackager_SmoothToHLS.xml are defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) and MediaEncryptor_PlayReadyProtection.xml is defined in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic.</span></span>

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
            // Paths toosupport files (within hello above base path). You can use 
            // hello provided sample media files from hello "SupportFiles" folder, or 
            // provide paths tooyour own media files below toorun these samples.

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
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Used hello chached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Load an MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset = ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create a common encryption content key that is used 
                // a) tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
                //    that is used for encryption.
                // b) tooconfigure hello license delivery service and 
                //
                Guid keyId;
                byte[] contentKey;

                IContentKey key = CreateCommonEncryptionKey(out keyId, out contentKey);

                // hello content key authorization policy must be configured by you 
                // and met by hello client in order for hello PlayReady license
                // toobe delivered toohello client. 
                // In this example hello Media Services PlayReady license delivery service is used.
                ConfigureLicenseDeliveryService(key);

                // Get hello Media Services PlayReady license delivery URL.
                // This URL will be assigned toohello licenseAcquisitionUrl property 
                // of hello MediaEncryptor_PlayReadyProtection.xml file.
                Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

                // Update hello MediaEncryptor_PlayReadyProtection.xml file with hello key and URL info.
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
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeSingleMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Streaming.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains Smooth Streaming.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Create a common encryption content key that is used 
            /// tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
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

                // Prepare hello encryption task template
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

                // Update hello "value" property.
                if (licenseAcquisitionUrlEl != null)
                    licenseAcquisitionUrlEl.Attribute("value").SetValue(licenseAcquisitionUrl.ToString());

                if (contentKeyEl != null)
                    contentKeyEl.Attribute("value").SetValue(Convert.ToBase64String(keyValue));

                if (keyIdEl != null)
                    keyIdEl.Attribute("value").SetValue(keyId);

                doc.Save(xmlFileName);
            }

            /// <summary>
            // Encrypts clear Smooth Streaming tooSmooth Streaming with PlayReady.
            // Then, packages hello PlayReady Smooth Streaming tooHLS with PlayReady.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateHLSEncryptedWithPlayReady(IAsset clearSmoothStreamAsset)
            {
                IJob job = _context.Jobs.Create("Encrypt tooHLS with PlayReady.");

                // Add task 1 - Encrypt Smooth Streaming with PlayReady 
                IAsset encryptedSmoothAsset =
                    EncryptSmoothStreamWithPlayReadyTask(job, clearSmoothStreamAsset);

                // Add task 2 - Package tooHLS with PlayReady.
                PackageSmoothStreamToHLS(job, encryptedSmoothAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Since we had two tasks, hello OutputMediaAssets[1]
                // contains hello desired asset.
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
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
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
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeSingleMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s",
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles,
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset =
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Streaming",
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }


            /// <summary>
            /// Converts Smooth Stream tooHLS.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello Smooth Stream asset.</param>
            /// <returns>hello asset that was packaged tooHLS.</returns>
            private static IAsset PackageSmoothStreamToHLS(IJob job, IAsset smoothStreamAsset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Read hello configuration data into a string. 
                //
                string configuration = File.ReadAllText(
                            Path.Combine(_configurationXMLFiles,
                                        @"MediaPackager_SmoothToHLS.xml"));

                // Create a task with hello encoding details, using a configuration file.
                ITask task = job.Tasks.AddNew("My Smooth tooHLS Task",
                   processor,
                   configuration,
                   TaskOptions.ProtectedConfiguration);

                // Specify hello input asset toobe encoded.
                task.InputAssets.Add(smoothStreamAsset);

                // Add an output asset toocontain hello results of hello job. 
                IAsset outputAsset =
                    task.OutputAssets.AddNew("HLS asset", AssetCreationOptions.None);


                return outputAsset;
            }

            /// <summary>
            /// Creates a task tooencrypt Smooth Streaming with PlayReady.
            /// Note: Do deliver DASH, make sure tooset hello useSencBox and adjustSubSamples 
            /// configuration properties tootrue.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncryptSmoothStreamWithPlayReadyTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Encryptor.
                IMediaProcessor playreadyProcessor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaEncryptor);

                // Read hello configuration XML.
                //
                // Note that hello configuration defined in MediaEncryptor_PlayReadyProtection.xml
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

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.CommonEncryptionProtected.
                IAsset playreadyAsset = playreadyTask.OutputAssets.AddNew(
                                                "PlayReady Smooth Streaming",
                                                AssetCreationOptions.CommonEncryptionProtected);


                return playreadyAsset;
            }


            /// <summary>
            /// Configures authorization policy for hello content key. 
            /// </summary>
            /// <param name="contentKey">hello content key.</param>
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

                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            static private string ConfigurePlayReadyLicenseTemplate()
            {
                // hello following code configures PlayReady License Template using .NET classes
                // and returns hello XML string.

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="053f7-188">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="053f7-188">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="053f7-189">Отзывы</span><span class="sxs-lookup"><span data-stu-id="053f7-189">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

