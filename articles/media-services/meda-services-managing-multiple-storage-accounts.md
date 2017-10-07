---
title: "aaaManaging активы служб мультимедиа для нескольких учетных записей хранилища | Документы Microsoft"
description: "Этой статьи дают рекомендации по как службы мультимедиа toomanage средств для нескольких учетных записей хранилища."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4e4a9ec3-8ddb-4938-aec1-d7172d3db858
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 812f290d91f8d739be1c88db2b612767fda96220
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-media-services-assets-across-multiple-storage-accounts"></a><span data-ttu-id="9a272-103">Управление активами служб мультимедиа в нескольких учетных записях хранения</span><span class="sxs-lookup"><span data-stu-id="9a272-103">Managing Media Services Assets across Multiple Storage Accounts</span></span>
<span data-ttu-id="9a272-104">Начиная с Microsoft Azure Media Services 2.2, можно добавить несколько учетных записей tooa одной службы мультимедиа учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="9a272-104">Starting with Microsoft Azure Media Services 2.2, you can attach multiple storage accounts tooa single Media Services account.</span></span> <span data-ttu-id="9a272-105">Возможность tooattach нескольких tooa учетных записей хранилища учетной записи служб мультимедиа предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9a272-105">Ability tooattach multiple storage accounts tooa Media Services account provides hello following benefits:</span></span>

* <span data-ttu-id="9a272-106">балансирование нагрузки ваших ресурсов-контейнеров между несколькими учетными записями хранения;</span><span class="sxs-lookup"><span data-stu-id="9a272-106">Load balancing your assets across multiple storage accounts.</span></span>
* <span data-ttu-id="9a272-107">масштабирование служб мультимедиа для больших объемов обработки содержимого (сейчас действует ограничение в 500 ТБ на одну учетную запись хранения).</span><span class="sxs-lookup"><span data-stu-id="9a272-107">Scaling Media Services for large amounts of content processing (as currently a single storage account has a max limit of 500 TB).</span></span> 

<span data-ttu-id="9a272-108">В этом разделе показано, как tooattach несколько учетных записей хранения учетной записи служб мультимедиа с помощью tooa [API диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/media/mediaservice) и [Powershell](/powershell/module/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="9a272-108">This topic demonstrates how tooattach multiple storage accounts tooa Media Services account using [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](/powershell/module/azurerm.media).</span></span> <span data-ttu-id="9a272-109">Здесь также показано, как при создании активов с помощью пакета SDK служб мультимедиа hello toospecify другое хранилище учетных записей.</span><span class="sxs-lookup"><span data-stu-id="9a272-109">It also shows how toospecify different storage accounts when creating assets using hello Media Services SDK.</span></span> 

## <a name="considerations"></a><span data-ttu-id="9a272-110">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="9a272-110">Considerations</span></span>
<span data-ttu-id="9a272-111">При добавлении нескольких tooyour учетных записей хранилища учетной записи служб мультимедиа, hello действуют следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="9a272-111">When attaching multiple storage accounts tooyour Media Services account, hello following considerations apply:</span></span>

* <span data-ttu-id="9a272-112">Все учетные записи хранения, вложенные tooa учетная запись служб мультимедиа должен находиться в hello одного центра обработки данных, как учетная запись служб мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="9a272-112">All storage accounts attached tooa Media Services account must be in hello same data center as hello Media Services account.</span></span>
* <span data-ttu-id="9a272-113">В настоящее время после присоединения учетной записи хранилища toohello указана учетная запись служб мультимедиа, не может быть отсоединен.</span><span class="sxs-lookup"><span data-stu-id="9a272-113">Currently, once a storage account is attached toohello specified Media Services account, it cannot be detached.</span></span>
* <span data-ttu-id="9a272-114">Учетной записи основного хранилища — hello, один указано во время создания учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="9a272-114">Primary storage account is hello one indicated during Media Services account creation time.</span></span> <span data-ttu-id="9a272-115">В настоящее время нельзя изменить учетную запись хранения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="9a272-115">Currently, you cannot change hello default storage account.</span></span> 
* <span data-ttu-id="9a272-116">В настоящее время tooadd учетную запись AMS toohello ожиданием хранилища учетной записи следует hello учетной записи хранилища должен быть тип большого двоичного объекта и задать первичный toonon.</span><span class="sxs-lookup"><span data-stu-id="9a272-116">Currently, if you want tooadd a Cool Storage account toohello AMS account, hello storage account must be a Blob type and set toonon-primary.</span></span>

<span data-ttu-id="9a272-117">Дополнительные рекомендации</span><span class="sxs-lookup"><span data-stu-id="9a272-117">Other considerations:</span></span>

<span data-ttu-id="9a272-118">Службы мультимедиа используют значение hello hello **IAssetFile.Name** свойства при формировании URL-адресов для потоковой передачи содержимого (например, http://{WAMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/ hello streamingParameters). По этой причине кодирование с помощью знака процента не допускается.</span><span class="sxs-lookup"><span data-stu-id="9a272-118">Media Services uses hello value of hello **IAssetFile.Name** property when building URLs for hello streaming content (for example, http://{WAMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="9a272-119">Hello hello имя свойства не может иметь любой из следующих hello [процентов зарезервированные символы](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? % # []».</span><span class="sxs-lookup"><span data-stu-id="9a272-119">hello value of hello Name property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="9a272-120">Кроме того, может использоваться только один знак ".".</span><span class="sxs-lookup"><span data-stu-id="9a272-120">Also, there can only be one ‘.’</span></span> <span data-ttu-id="9a272-121">для расширения имени файла hello.</span><span class="sxs-lookup"><span data-stu-id="9a272-121">for hello file name extension.</span></span>

## <a name="tooattach-storage-accounts"></a><span data-ttu-id="9a272-122">учетные записи хранения tooattach</span><span class="sxs-lookup"><span data-stu-id="9a272-122">tooattach storage accounts</span></span>  

<span data-ttu-id="9a272-123">tooattach хранилища учетных записей tooyour AMS учетной записи, используйте [API диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/media/mediaservice) и [Powershell](/powershell/module/azurerm.media), как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="9a272-123">tooattach storage accounts tooyour AMS account, use [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](/powershell/module/azurerm.media), as shown in hello following example.</span></span>

    $regionName = "West US"
    $subscriptionId = " xxxxxxxx-xxxx-xxxx-xxxx- xxxxxxxxxxxx "
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccount1Name = "skystorage1"
    $storageAccount2Name = "skystorage2"
    $storageAccount1Id = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccount1Name"
    $storageAccount2Id = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccount2Name"
    $storageAccount1 = New-AzureRmMediaServiceStorageConfig -StorageAccountId $storageAccount1Id -IsPrimary
    $storageAccount2 = New-AzureRmMediaServiceStorageConfig -StorageAccountId $storageAccount2Id
    $storageAccounts = @($storageAccount1, $storageAccount2)
    
    Set-AzureRmMediaService -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccounts $storageAccounts

### <a name="support-for-cool-storage"></a><span data-ttu-id="9a272-124">Поддержка "холодного" хранилища</span><span class="sxs-lookup"><span data-stu-id="9a272-124">Support for Cool Storage</span></span>

<span data-ttu-id="9a272-125">В настоящее время tooadd учетную запись AMS toohello ожиданием хранилища учетной записи следует hello учетной записи хранилища должен быть тип большого двоичного объекта и задать первичный toonon.</span><span class="sxs-lookup"><span data-stu-id="9a272-125">Currently, if you want tooadd a Cool Storage account toohello AMS account, hello storage account must be a Blob type and set toonon-primary.</span></span>

## <a name="toomanage-media-services-assets-across-multiple-storage-accounts"></a><span data-ttu-id="9a272-126">toomanage активы служб мультимедиа для нескольких учетных записей хранения</span><span class="sxs-lookup"><span data-stu-id="9a272-126">toomanage Media Services assets across multiple Storage Accounts</span></span>
<span data-ttu-id="9a272-127">Привет, следующий код использует hello пакета SDK служб мультимедиа tooperform hello для последней следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="9a272-127">hello following code uses hello latest Media Services SDK tooperform hello following tasks:</span></span>

1. <span data-ttu-id="9a272-128">Показать все учетные записи хранения hello, связанные с hello указана учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="9a272-128">Display all hello storage accounts associated with hello specified Media Services account.</span></span>
2. <span data-ttu-id="9a272-129">Получить имя учетной записи хранения по умолчанию hello hello.</span><span class="sxs-lookup"><span data-stu-id="9a272-129">Retrieve hello name of hello default storage account.</span></span>
3. <span data-ttu-id="9a272-130">Создание нового актива в учетной записи хранения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="9a272-130">Create a new asset in hello default storage account.</span></span>
4. <span data-ttu-id="9a272-131">Создание выходного актива кодирования hello задания в hello указано учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="9a272-131">Create an output asset of hello encoding job in hello specified storage account.</span></span>
   
```
using Microsoft.WindowsAzure.MediaServices.Client;
using System;
using System.Collections.Generic;
using System.Configuration;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace MultipleStorageAccounts
{
    class Program
    {
        // Location of hello media file that you want tooencode. 
        private static readonly string _singleInputFilePath =
            Path.GetFullPath(@"../..\supportFiles\multifile\interview2.wmv");

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Display hello storage accounts associated with 
            // hello specified Media Services account:
            foreach (var sa in _context.StorageAccounts)
                Console.WriteLine(sa.Name);

            // Retrieve hello name of hello default storage account.
            var defaultStorageName = _context.StorageAccounts.Where(s => s.IsDefault == true).FirstOrDefault();
            Console.WriteLine("Name: {0}", defaultStorageName.Name);
            Console.WriteLine("IsDefault: {0}", defaultStorageName.IsDefault);

            // Retrieve hello name of a storage account that is not hello default one.
            var notDefaultStroageName = _context.StorageAccounts.Where(s => s.IsDefault == false).FirstOrDefault();
            Console.WriteLine("Name: {0}", notDefaultStroageName.Name);
            Console.WriteLine("IsDefault: {0}", notDefaultStroageName.IsDefault);

            // Create hello original asset in hello default storage account.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.None,
                defaultStorageName.Name, _singleInputFilePath);
            Console.WriteLine("Created hello asset in hello {0} storage account", asset.StorageAccountName);

            // Create an output asset of hello encoding job in hello other storage account.
            IAsset outputAsset = CreateEncodingJob(asset, notDefaultStroageName.Name, _singleInputFilePath);
            if (outputAsset != null)
                Console.WriteLine("Created hello output asset in hello {0} storage account", outputAsset.StorageAccountName);

        }

        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string storageName, string singleFilePath)
        {
            var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();

            // If you are creating an asset in hello default storage account, you can omit hello StorageName parameter.
            var asset = _context.Assets.Create(assetName, storageName, assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);

            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return asset;
        }

        static IAsset CreateEncodingJob(IAsset asset, string storageName, string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My encoding job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.ProtectedConfiguration);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset", storageName,
                AssetCreationOptions.None);

            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch hello job.
            job.Submit();

            // Check job execution and wait for job toofinish. 
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();

            // Get an updated job reference.
            job = GetJob(job.Id);

            // If job state is Error hello event handling 
            // method for job progress should log errors.  Here we check 
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                Console.WriteLine("\nExiting method due toojob error.");
                return null;
            }

            // Get a reference toohello output asset from hello job.
            IAsset outputAsset = job.OutputMediaAssets[0];

            return outputAsset;
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        private static void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
                case JobState.Finished:
                    Console.WriteLine();
                    Console.WriteLine("********************");
                    Console.WriteLine("Job is finished.");
                    Console.WriteLine("Please wait while local tasks or downloads complete...");
                    Console.WriteLine("********************");
                    Console.WriteLine();
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
                    Console.WriteLine("An error occurred in {0}", job.Id);
                    break;
                default:
                    break;
            }
        }

        static IJob GetJob(string jobId)
        {
            // Use a Linq select query tooget an updated 
            // reference by Id. 
            var jobInstance =
                from j in _context.Jobs
                where j.Id == jobId
                select j;
            // Return hello job reference as an Ijob. 
            IJob job = jobInstance.FirstOrDefault();

            return job;
        }
    }
}
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="9a272-132">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="9a272-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9a272-133">Отзывы</span><span class="sxs-lookup"><span data-stu-id="9a272-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

