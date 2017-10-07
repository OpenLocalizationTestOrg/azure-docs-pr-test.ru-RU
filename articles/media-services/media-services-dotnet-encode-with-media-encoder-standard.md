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
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="335e0-103">Кодирование ресурса-контейнера с помощью Media Encoder Standard и .NET</span><span class="sxs-lookup"><span data-stu-id="335e0-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="335e0-104">Задания кодирования — это один из самых распространенных операций обработки hello в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="335e0-104">Encoding jobs are one of hello most common processing operations in Media Services.</span></span> <span data-ttu-id="335e0-105">Создать кодирования файлов мультимедиа tooconvert заданий из одной кодировки tooanother.</span><span class="sxs-lookup"><span data-stu-id="335e0-105">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="335e0-106">При кодировании можно использовать hello встроенных Media Encoder служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="335e0-106">When you encode, you can use hello Media Services built-in Media Encoder.</span></span> <span data-ttu-id="335e0-107">Также можно использовать кодировщик, предоставленный партнером Media Services; сторонние кодировщики можно найти hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="335e0-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through hello Azure Marketplace.</span></span> 

<span data-ttu-id="335e0-108">В этом разделе показано, как toouse .NET tooencode активов с Media Encoder Standard (MES).</span><span class="sxs-lookup"><span data-stu-id="335e0-108">This topic shows how toouse .NET tooencode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="335e0-109">Стандартный кодировщик мультимедиа настраивается с помощью одного из описанных предустановки кодировщика hello [здесь](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="335e0-109">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="335e0-110">Рекомендуется tooalways кодируют исходные файлы в набор MP4 с адаптивной скоростью, а затем преобразовать hello набор toohello нужный формат с помощью hello [динамической упаковки](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="335e0-110">It is recommended tooalways encode your source files into an adaptive bitrate MP4 set and then convert hello set toohello desired format using hello [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="335e0-111">Если выходящий ресурс зашифрован в хранилище, необходимо настроить политику доставки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="335e0-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="335e0-112">Дополнительные сведения см. в статье [Настройка политик доставки ресурсов-контейнеров](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="335e0-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="335e0-113">MES создает выходной файл с именем, содержащим hello первые 32 символа hello имя входного файла.</span><span class="sxs-lookup"><span data-stu-id="335e0-113">MES produces an output file with a name that contains hello first 32 characters of hello input file name.</span></span> <span data-ttu-id="335e0-114">Имя Hello основано на, заданных в файле предустановки hello.</span><span class="sxs-lookup"><span data-stu-id="335e0-114">hello name is based on what is specified in hello preset file.</span></span> <span data-ttu-id="335e0-115">Например, "FileName": "{Basename}_{Index}{Extension}".</span><span class="sxs-lookup"><span data-stu-id="335e0-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="335e0-116">{Базовое имя} заменяется hello первые 32 символа имени входного файла hello.</span><span class="sxs-lookup"><span data-stu-id="335e0-116">{Basename} is replaced by hello first 32 characters of hello input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="335e0-117">Форматы стандартного кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="335e0-117">MES Formats</span></span>
[<span data-ttu-id="335e0-118">Форматы и кодеки</span><span class="sxs-lookup"><span data-stu-id="335e0-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="335e0-119">Предустановки стандартного кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="335e0-119">MES Presets</span></span>
<span data-ttu-id="335e0-120">Стандартный кодировщик мультимедиа настраивается с помощью одного из описанных предустановки кодировщика hello [здесь](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="335e0-120">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="335e0-121">Входные и выходные метаданные</span><span class="sxs-lookup"><span data-stu-id="335e0-121">Input and output metadata</span></span>
<span data-ttu-id="335e0-122">При кодировании входным активом (или активами), с помощью MES вы получаете выходного актива в hello успешное завершение, кодирования задач.</span><span class="sxs-lookup"><span data-stu-id="335e0-122">When you encode an input asset (or assets) using MES, you get an output asset at hello successful completion of that encode task.</span></span> <span data-ttu-id="335e0-123">Hello выходной актив содержит видеофайлы, аудиофайлы, эскизы, манифест, т. д., основании предустановку hello, используемого.</span><span class="sxs-lookup"><span data-stu-id="335e0-123">hello output asset contains video, audio, thumbnails, manifest, etc. based on hello encoding preset you use.</span></span>

<span data-ttu-id="335e0-124">Hello также включает файл метаданных входного актива hello.</span><span class="sxs-lookup"><span data-stu-id="335e0-124">hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="335e0-125">Hello hello метаданных XML-файлу имеет hello следующий формат: < идентификатор_актива > _metadata.xml (например, 41114ad3-eb5e - 4c 57 8d 92-5354e2b7d4a4_metadata.xml), где < идентификатор_актива > — hello значение AssetId входного актива hello.</span><span class="sxs-lookup"><span data-stu-id="335e0-125">hello name of hello metadata XML file has hello following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is hello AssetId value of hello input asset.</span></span> <span data-ttu-id="335e0-126">Hello схем входных метаданных XML описывается [здесь](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="335e0-126">hello schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="335e0-127">Hello также включает файл метаданных выходного актива hello.</span><span class="sxs-lookup"><span data-stu-id="335e0-127">hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="335e0-128">Hello hello метаданных XML-файлу имеет hello следующий формат: < имя_исходного_файла > _manifest.xml (например, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="335e0-128">hello name of hello metadata XML file has hello following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="335e0-129">Схема Hello этих метаданных выходного XML описана [здесь](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="335e0-129">hello schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="335e0-130">Следует tooexamine либо hello двух файлов метаданных можно создать указатель SAS и загрузки hello файл tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="335e0-130">If you want tooexamine either of hello two metadata files, you can create a SAS locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="335e0-131">Пример как toocreate указателя SAS и загрузки файла с помощью hello служб мультимедиа можно найти расширения SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="335e0-131">You can find an example on how toocreate a SAS locator and download a file Using hello Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="335e0-132">Скачивание образца</span><span class="sxs-lookup"><span data-stu-id="335e0-132">Download sample</span></span>
<span data-ttu-id="335e0-133">Можно получить и выполнить пример, в котором показано, как tooencode с MES из [здесь](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="335e0-133">You can get and run a sample that shows how tooencode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="335e0-134">Пример кода .NET</span><span class="sxs-lookup"><span data-stu-id="335e0-134">.NET sample code</span></span>

<span data-ttu-id="335e0-135">Следующий пример кода Hello использует hello tooperform Media Services .NET SDK следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="335e0-135">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="335e0-136">Создание задания кодирования.</span><span class="sxs-lookup"><span data-stu-id="335e0-136">Create an encoding job.</span></span>
* <span data-ttu-id="335e0-137">Получите кодировщик Media Encoder Стандартная toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="335e0-137">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="335e0-138">Укажите toouse hello [адаптивной потоковой передачи](media-services-autogen-bitrate-ladder-with-mes.md) предустановки.</span><span class="sxs-lookup"><span data-stu-id="335e0-138">Specify toouse hello [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="335e0-139">Добавьте одно задание toohello задач кодирования.</span><span class="sxs-lookup"><span data-stu-id="335e0-139">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="335e0-140">Укажите входной hello toobe активов кодировке.</span><span class="sxs-lookup"><span data-stu-id="335e0-140">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="335e0-141">Создание выходного актива, который будет содержать активов hello в кодировке.</span><span class="sxs-lookup"><span data-stu-id="335e0-141">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="335e0-142">Добавьте событие обработчика toocheck hello ход выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="335e0-142">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="335e0-143">Отправка задания hello.</span><span class="sxs-lookup"><span data-stu-id="335e0-143">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="335e0-144">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="335e0-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="335e0-145">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="335e0-145">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="335e0-146">Пример</span><span class="sxs-lookup"><span data-stu-id="335e0-146">Example</span></span> 

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="335e0-147">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="335e0-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="335e0-148">Отзывы</span><span class="sxs-lookup"><span data-stu-id="335e0-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="335e0-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="335e0-149">Next steps</span></span>
<span data-ttu-id="335e0-150">[Как toogenerate эскиз в .NET Framework с помощью Media Encoder Стандартная](media-services-dotnet-generate-thumbnail-with-mes.md)
[Обзор кодирования службами мультимедиа](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="335e0-150">[How toogenerate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

