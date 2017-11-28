---
title: "aaaUpload файлы в учетную запись служб мультимедиа с помощью .NET | Документы Microsoft"
description: "Узнайте, как носитель tooget содержимого в службы мультимедиа, создав и загрузив активы."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="a4c02-103">Передача файлов в учетную запись служб мультимедиа с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="a4c02-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4c02-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a4c02-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="a4c02-105">REST</span><span class="sxs-lookup"><span data-stu-id="a4c02-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="a4c02-106">Портал</span><span class="sxs-lookup"><span data-stu-id="a4c02-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="a4c02-107">В службах мультимедиа цифровые файлы отправляются (или принимаются) в актив.</span><span class="sxs-lookup"><span data-stu-id="a4c02-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="a4c02-108">Hello **активов** может содержать сущности, видео, аудио, изображения, коллекции эскизов, текст отслеживает и титров файлов (и hello метаданные об этих файлах.)  После загрузки файлов hello контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="a4c02-108">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="a4c02-109">Hello в ресурсе hello, называются **файлов активов**.</span><span class="sxs-lookup"><span data-stu-id="a4c02-109">hello files in hello asset are called **Asset Files**.</span></span> <span data-ttu-id="a4c02-110">Hello **AssetFile** экземпляра и hello фактический файл мультимедиа являются двумя отдельными объектами.</span><span class="sxs-lookup"><span data-stu-id="a4c02-110">hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="a4c02-111">экземпляр AssetFile Hello содержит метаданные о файле мультимедиа hello, а файл мультимедиа hello hello фактический контент мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="a4c02-111">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="a4c02-112">применить Hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="a4c02-112">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="a4c02-113">Службы мультимедиа используют значение hello hello свойство IAssetFile.Name при построении URL-адреса для hello, потоковая передача содержимого (например, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) По этой причине кодирование с помощью знака процента не допускается.</span><span class="sxs-lookup"><span data-stu-id="a4c02-113">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="a4c02-114">Здравствуйте, значение hello **имя** свойство не может иметь любой из следующих hello [процентов зарезервированные символы](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? % # []».</span><span class="sxs-lookup"><span data-stu-id="a4c02-114">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="a4c02-115">Кроме того, может существовать только один "." для расширения имени файла hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-115">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="a4c02-116">Длина Hello hello имени не должна быть более 260 знаков.</span><span class="sxs-lookup"><span data-stu-id="a4c02-116">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="a4c02-117">Имеется ограничение toohello максимальный размер файла поддерживается для обработки в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="a4c02-117">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="a4c02-118">См. в разделе [это](media-services-quotas-and-limitations.md) сведения о hello ограничения размера файла.</span><span class="sxs-lookup"><span data-stu-id="a4c02-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> * <span data-ttu-id="a4c02-119">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a4c02-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a4c02-120">Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="a4c02-120">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="a4c02-121">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="a4c02-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="a4c02-122">При создании активов можно указать следующие параметры шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-122">When you create assets, you can specify hello following encryption options.</span></span> 

* <span data-ttu-id="a4c02-123">**None** — шифрование не используется.</span><span class="sxs-lookup"><span data-stu-id="a4c02-123">**None** - No encryption is used.</span></span> <span data-ttu-id="a4c02-124">Это значение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-124">This is hello default value.</span></span> <span data-ttu-id="a4c02-125">Обратите внимание, что при использовании этого параметра содержимое не защищено при передаче или в хранилище.</span><span class="sxs-lookup"><span data-stu-id="a4c02-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="a4c02-126">Если планируется toodeliver MP4-файл с помощью прогрессивной загрузки, используйте этот параметр.</span><span class="sxs-lookup"><span data-stu-id="a4c02-126">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="a4c02-127">**CommonEncryption** — используйте этот параметр при отправке содержимого, которое уже зашифровано и защищено с помощью стандартного шифрования или PlayReady DRM (например, Smooth Streaming с защитой PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="a4c02-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="a4c02-128">**EnvelopeEncrypted** — используйте этот параметр при отправке HLS с шифрованием AES.</span><span class="sxs-lookup"><span data-stu-id="a4c02-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="a4c02-129">Обратите внимание, что hello файлы необходимо были закодированы и зашифрованы диспетчером преобразования.</span><span class="sxs-lookup"><span data-stu-id="a4c02-129">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="a4c02-130">**StorageEncrypted** — шифрование незащищенного содержимого локально с помощью AES-256-разрядного шифрования, а затем передает его tooAzure хранилища, где она хранится в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="a4c02-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="a4c02-131">Активы, защищенные с помощью шифрования хранилища, автоматически дешифруются и помещаются в предыдущих tooencoding зашифрованный файл системы и при необходимости повторно зашифрован предыдущих toouploading возвращены в виде нового выходного актива.</span><span class="sxs-lookup"><span data-stu-id="a4c02-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="a4c02-132">Hello основным случаем использования шифрования хранилища удобно, если нужно toosecure rest вашей высококачественных входных файлов мультимедиа с помощью строгого шифрования на диске.</span><span class="sxs-lookup"><span data-stu-id="a4c02-132">hello primary use case for Storage Encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="a4c02-133">Службы мультимедиа обеспечивают шифрование ресурсов на диске в хранилище, а не по сети, как технология управления цифровыми правами (DRM).</span><span class="sxs-lookup"><span data-stu-id="a4c02-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="a4c02-134">Если ресурс зашифрован в хранилище, необходимо настроить политику доставки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a4c02-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="a4c02-135">Дополнительные сведения см. в статье [Настройка политик доставки ресурсов-контейнеров](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a4c02-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="a4c02-136">При указании для вашего toobe активов зашифрованы с **CommonEncrypted** параметр, или **EnvelopeEncypted** параметр, необходимо будет tooassociate актива с **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="a4c02-136">If you specify for your asset toobe encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need tooassociate your asset with a **ContentKey**.</span></span> <span data-ttu-id="a4c02-137">Дополнительные сведения см. в разделе [как toocreate ContentKey](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="a4c02-137">For more information, see [How toocreate a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="a4c02-138">При указании для вашего toobe активов зашифрованы с **StorageEncrypted** , то hello пакета SDK служб мультимедиа для .NET создаст **StorateEncrypted** **ContentKey** для вашей активов.</span><span class="sxs-lookup"><span data-stu-id="a4c02-138">If you specify for your asset toobe encrypted with a **StorageEncrypted** option, hello Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="a4c02-139">В этом разделе показано, как toouse Media Services .NET SDK, а также файлы tooupload Media Services .NET SDK расширения в актив служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="a4c02-139">This topic shows how toouse Media Services .NET SDK as well as Media Services .NET SDK extensions tooupload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="a4c02-140">Передача одного файла с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="a4c02-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="a4c02-141">Hello в образце кода ниже использует .NET SDK tooupload один файл.</span><span class="sxs-lookup"><span data-stu-id="a4c02-141">hello sample code below uses .NET SDK tooupload a single file.</span></span> <span data-ttu-id="a4c02-142">создании и удалении функцией передачи hello Hello AccessPolicy и указателя.</span><span class="sxs-lookup"><span data-stu-id="a4c02-142">hello AccessPolicy and Locator are created and destroyed by hello Upload function.</span></span> 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="a4c02-143">Передача нескольких файлов с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="a4c02-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="a4c02-144">Здравствуйте, как следующий код показывает toocreate актива и отправка нескольких файлов.</span><span class="sxs-lookup"><span data-stu-id="a4c02-144">hello following code shows how toocreate an asset and upload multiple files.</span></span>

<span data-ttu-id="a4c02-145">Hello кода hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a4c02-145">hello code does hello following:</span></span>

* <span data-ttu-id="a4c02-146">Создает пустой актив с помощью метода CreateEmptyAsset hello, определенный в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-146">Creates an empty asset using hello CreateEmptyAsset method defined in hello previous step.</span></span>
* <span data-ttu-id="a4c02-147">Создает **AccessPolicy** экземпляр, который определяет hello разрешения и длительность доступа toohello активов.</span><span class="sxs-lookup"><span data-stu-id="a4c02-147">Creates an **AccessPolicy** instance that defines hello permissions and duration of access toohello asset.</span></span>
* <span data-ttu-id="a4c02-148">Создает **локатора** экземпляр, который предоставляет доступ toohello активов.</span><span class="sxs-lookup"><span data-stu-id="a4c02-148">Creates a **Locator** instance that provides access toohello asset.</span></span>
* <span data-ttu-id="a4c02-149">Создает экземпляр **BlobTransferClient** .</span><span class="sxs-lookup"><span data-stu-id="a4c02-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="a4c02-150">Этот тип представляет клиент, работающий на приветствия больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c02-150">This type represents a client that operates on hello Azure blobs.</span></span> <span data-ttu-id="a4c02-151">В этом примере мы используем прогресса отправки hello toomonitor клиента hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-151">In this example we use hello client toomonitor hello upload progress.</span></span> 
* <span data-ttu-id="a4c02-152">Перечисляет файлы в указанном каталоге hello и создает **AssetFile** экземпляра для каждого файла.</span><span class="sxs-lookup"><span data-stu-id="a4c02-152">Enumerates through files in hello specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="a4c02-153">Передачи файлов hello в службы мультимедиа с помощью hello **UploadAsync** метод.</span><span class="sxs-lookup"><span data-stu-id="a4c02-153">Uploads hello files into Media Services using hello **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="a4c02-154">Используйте tooensure метод UploadAsync hello, hello вызовы не блокируются и hello файлы отправляются параллельно.</span><span class="sxs-lookup"><span data-stu-id="a4c02-154">Use hello UploadAsync method tooensure that hello calls are not blocking and hello files are uploaded in parallel.</span></span>
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="a4c02-155">При передаче большего количества активов, рассмотрим следующие hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-155">When uploading a large number of assets, consider hello following.</span></span>

* <span data-ttu-id="a4c02-156">Создайте новый объект **CloudMediaContext** в каждом потоке.</span><span class="sxs-lookup"><span data-stu-id="a4c02-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="a4c02-157">Hello **CloudMediaContext** класс не является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="a4c02-157">hello **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="a4c02-158">Увеличьте NumberOfConcurrentTransfers со значения по умолчанию hello 2 tooa высокого значения, например 5.</span><span class="sxs-lookup"><span data-stu-id="a4c02-158">Increase NumberOfConcurrentTransfers from hello default value of 2 tooa higher value like 5.</span></span> <span data-ttu-id="a4c02-159">Задание этого свойства влияет на все экземпляры **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="a4c02-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="a4c02-160">Сохраните ParallelTransferThreadCount на значение по умолчанию hello 10.</span><span class="sxs-lookup"><span data-stu-id="a4c02-160">Keep ParallelTransferThreadCount at hello default value of 10.</span></span>

## <span data-ttu-id="a4c02-161"><a id="ingest_in_bulk"></a>Массовый прием ресурсов с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="a4c02-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="a4c02-162">Передача больших файлов ресурсов может оказаться узким местом при создании ресурса.</span><span class="sxs-lookup"><span data-stu-id="a4c02-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="a4c02-163">Массовое получение активов массового или «Массовой передаче», связана с разделением создания ресурсов от процесса отправки hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from hello upload process.</span></span> <span data-ttu-id="a4c02-164">toouse массовое получение подход более bulk, создайте манифест (IngestManifest), описывающий активов hello и связанные с ней файлы.</span><span class="sxs-lookup"><span data-stu-id="a4c02-164">toouse a bulk ingesting approach, create a manifest (IngestManifest) that describes hello asset and its associated files.</span></span> <span data-ttu-id="a4c02-165">Затем используйте метод отправки hello ваш выбор tooupload hello связанные файлы toohello манифеста контейнера BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="a4c02-165">Then use hello upload method of your choice tooupload hello associated files toohello manifest’s blob container.</span></span> <span data-ttu-id="a4c02-166">Службы мультимедиа Microsoft Azure отслеживает hello контейнер больших двоичных объектов, связанных с манифестом hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-166">Microsoft Azure Media Services watches hello blob container associated with hello manifest.</span></span> <span data-ttu-id="a4c02-167">Как только файл отправленного toohello контейнер больших двоичных объектов, службы мультимедиа Microsoft Azure завершает hello создания ресурса, на основе конфигурации hello средства hello в манифесте hello (IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="a4c02-167">Once a file is uploaded toohello blob container, Microsoft Azure Media Services completes hello asset creation based on hello configuration of hello asset in hello manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="a4c02-168">toocreate нового объекта IngestManifest вызвать метод Create hello, предоставляемые hello коллекции hello CloudMediaContext объекты Ingestmanifest.</span><span class="sxs-lookup"><span data-stu-id="a4c02-168">toocreate a new IngestManifest call hello Create method exposed by hello IngestManifests collection on hello CloudMediaContext.</span></span> <span data-ttu-id="a4c02-169">Этот метод создаст новый IngestManifest с именем манифеста hello вами.</span><span class="sxs-lookup"><span data-stu-id="a4c02-169">This method will create a new IngestManifest with hello manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="a4c02-170">Создайте hello активы, которые будут связаны с неполным hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="a4c02-170">Create hello assets that will be associated with hello bulk IngestManifest.</span></span> <span data-ttu-id="a4c02-171">Настройте параметры шифрования hello требуемого hello активе для массового получения.</span><span class="sxs-lookup"><span data-stu-id="a4c02-171">Configure hello desired encryption options on hello asset for bulk ingesting.</span></span>

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="a4c02-172">Сущность IngestManifestAsset связывает ресурс с массовой сущностью IngestManifest для массового приема.</span><span class="sxs-lookup"><span data-stu-id="a4c02-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="a4c02-173">Он также связывает hello AssetFiles, составляющих каждого средства.</span><span class="sxs-lookup"><span data-stu-id="a4c02-173">It also associates hello AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="a4c02-174">toocreate IngestManifestAsset, используйте метод Create hello на контекст сервера hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-174">toocreate an IngestManifestAsset, use hello Create method on hello server context.</span></span>

<span data-ttu-id="a4c02-175">Hello следующий пример демонстрирует добавление двух новых IngestManifestAssets, которые связывают два актива hello ранее созданные toohello массового манифеста получения.</span><span class="sxs-lookup"><span data-stu-id="a4c02-175">hello following example demonstrates adding two new IngestManifestAssets that associate hello two assets previously created toohello bulk ingest manifest.</span></span> <span data-ttu-id="a4c02-176">Каждая сущность IngestManifestAsset связывает также набор файлов, которые передаются для каждого ресурса во время массового приема.</span><span class="sxs-lookup"><span data-stu-id="a4c02-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="a4c02-177">Можно использовать любое высокоскоростное клиентское приложение может загрузить контейнер больших двоичных объектов хранилища для активов файлы hello toohello URI, предоставляемые hello **IIngestManifest.BlobStorageUriForUpload** свойство hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="a4c02-177">You can use any high speed client application capable of uploading hello asset files toohello blob storage container URI provided by hello **IIngestManifest.BlobStorageUriForUpload** property of hello IngestManifest.</span></span> <span data-ttu-id="a4c02-178">[Приложение Aspera On Demand for Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6)— одна из наиболее примечательных служб высокоскоростной передачи.</span><span class="sxs-lookup"><span data-stu-id="a4c02-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="a4c02-179">Можно также написать код tooupload hello ресурсных файлов как показано в следующем примере кода hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-179">You can also write code tooupload hello assets files as shown in hello following code example.</span></span>

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

<span data-ttu-id="a4c02-180">Hello код для отправки файлов активов hello для образца hello, используемый в этом разделе показан в следующем примере кода hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-180">hello code for uploading hello asset files for hello sample used in this topic is shown in hello following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="a4c02-181">Можно определить ход выполнения hello hello массового добавления для всех ресурсов, связанных с **IngestManifest** путем опроса свойства статистики hello hello **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="a4c02-181">You can determine hello progress of hello bulk ingesting for all assets associated with an **IngestManifest** by polling hello Statistics property of hello **IngestManifest**.</span></span> <span data-ttu-id="a4c02-182">В сведения о заказе tooupdate хода выполнения, необходимо использовать новый **CloudMediaContext** каждый раз опроса свойства Statistics hello.</span><span class="sxs-lookup"><span data-stu-id="a4c02-182">In order tooupdate progress information, you must use a new **CloudMediaContext** each time you poll hello Statistics property.</span></span>

<span data-ttu-id="a4c02-183">Hello следующий пример демонстрирует опрос в IngestManifest, его **идентификатор**.</span><span class="sxs-lookup"><span data-stu-id="a4c02-183">hello following example demonstrates polling an IngestManifest by its **Id**.</span></span>

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="a4c02-184">Передача файлов с помощью расширений пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="a4c02-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="a4c02-185">Hello приведенном ниже примере показано, как tooupload один файл с помощью расширений SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="a4c02-185">hello example below shows how tooupload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="a4c02-186">В этом случае hello **CreateFromFile** метод используется, но также доступна асинхронная версия hello (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="a4c02-186">In this case hello **CreateFromFile** method is used, but hello asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="a4c02-187">Hello **CreateFromFile** метод позволяет указать имя файла hello, шифрование и обратный вызов в порядке tooreport hello ход hello файла отправки.</span><span class="sxs-lookup"><span data-stu-id="a4c02-187">hello **CreateFromFile** method lets you specify hello file name, encryption option, and a callback in order tooreport hello upload progress of hello file.</span></span>

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }

<span data-ttu-id="a4c02-188">Hello следующий пример вызывает функцию UploadFile и задает в качестве параметра создания активов hello шифрование хранилища.</span><span class="sxs-lookup"><span data-stu-id="a4c02-188">hello following example calls UploadFile function and specifies storage encryption as hello asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="a4c02-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a4c02-189">Next steps</span></span>

<span data-ttu-id="a4c02-190">Теперь можно закодировать отправленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a4c02-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="a4c02-191">Дополнительную информацию см. в статье, посвященной [кодированию ресурсов](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="a4c02-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="a4c02-192">Также можно использовать функции Azure tootrigger задание кодирования на основе файла, поступающих в контейнере hello настроен.</span><span class="sxs-lookup"><span data-stu-id="a4c02-192">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="a4c02-193">Дополнительные сведения см. в [этом примере](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="a4c02-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a4c02-194">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a4c02-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a4c02-195">Отзывы</span><span class="sxs-lookup"><span data-stu-id="a4c02-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="a4c02-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a4c02-196">Next step</span></span>
<span data-ttu-id="a4c02-197">Теперь, когда вы отправили актива служб tooMedia go toohello [как обработчик мультимедиа tooGet] [ How tooGet a Media Processor] раздела.</span><span class="sxs-lookup"><span data-stu-id="a4c02-197">Now that you have uploaded an asset tooMedia Services, go toohello [How tooGet a Media Processor][How tooGet a Media Processor] topic.</span></span>

[How tooGet a Media Processor]: media-services-get-media-processor.md

