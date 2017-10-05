---
title: "Передача файлов в учетную запись служб мультимедиа с помощью .NET | Документация Майкрософт"
description: "Узнайте, как включить мультимедийное содержимое в службы мультимедиа, создав и отправив ресурс."
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
ms.openlocfilehash: ec8c1da633374ba684f6a0a895c542ee76ef73b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="9d05b-103">Передача файлов в учетную запись служб мультимедиа с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="9d05b-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d05b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="9d05b-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="9d05b-105">REST</span><span class="sxs-lookup"><span data-stu-id="9d05b-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="9d05b-106">Портал</span><span class="sxs-lookup"><span data-stu-id="9d05b-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="9d05b-107">В службах мультимедиа цифровые файлы отправляются (или принимаются) в актив.</span><span class="sxs-lookup"><span data-stu-id="9d05b-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="9d05b-108">Сущность **Asset** может содержать видео, аудио, изображения, коллекции эскизов, текстовые дорожки и файлы скрытых субтитров (а также метаданные этих файлов).  После отправки этих файлов содержимое сохраняется в безопасном расположении в облаке для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="9d05b-108">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="9d05b-109">Файлы в ресурсе называются **файлами ресурса**.</span><span class="sxs-lookup"><span data-stu-id="9d05b-109">The files in the asset are called **Asset Files**.</span></span> <span data-ttu-id="9d05b-110">Экземпляр **AssetFile** и фактический файл мультимедиа — это два разных объекта.</span><span class="sxs-lookup"><span data-stu-id="9d05b-110">The **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="9d05b-111">Экземпляр AssetFile содержит метаданные о файле мультимедиа, а сам файл мультимедиа — фактическое мультимедийное содержимое.</span><span class="sxs-lookup"><span data-stu-id="9d05b-111">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="9d05b-112">Действительны следующие условия.</span><span class="sxs-lookup"><span data-stu-id="9d05b-112">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="9d05b-113">Службы мультимедиа используют значение свойства IAssetFile.Name при создании URL-адресов для потоковой передачи содержимого (например, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) По этой причине кодирование с помощью знака процента не допускается.</span><span class="sxs-lookup"><span data-stu-id="9d05b-113">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="9d05b-114">Значение свойства **Name** не может содержать такие [зарезервированные знаки, используемые для кодировки URL-адресов](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="9d05b-114">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="9d05b-115">Кроме того, может использоваться только один знак "." для расширения имени файла.</span><span class="sxs-lookup"><span data-stu-id="9d05b-115">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="9d05b-116">Длина имени не должна превышать 260 знаков.</span><span class="sxs-lookup"><span data-stu-id="9d05b-116">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="9d05b-117">Существует ограничение на максимальный размер файла, который могут обработать службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="9d05b-117">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="9d05b-118">Подробные сведения об этом см. [здесь](media-services-quotas-and-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="9d05b-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> * <span data-ttu-id="9d05b-119">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="9d05b-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="9d05b-120">Следует указывать один и тот же идентификатор политики, если вы используете те же дни, разрешения доступа и т. д. Например, политики для указателей, которые должны оставаться на месте в течение длительного времени (не политики передачи).</span><span class="sxs-lookup"><span data-stu-id="9d05b-120">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="9d05b-121">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="9d05b-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="9d05b-122">При создании ресурсов можно указать следующие параметры шифрования.</span><span class="sxs-lookup"><span data-stu-id="9d05b-122">When you create assets, you can specify the following encryption options.</span></span> 

* <span data-ttu-id="9d05b-123">**None** — шифрование не используется.</span><span class="sxs-lookup"><span data-stu-id="9d05b-123">**None** - No encryption is used.</span></span> <span data-ttu-id="9d05b-124">Это значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9d05b-124">This is the default value.</span></span> <span data-ttu-id="9d05b-125">Обратите внимание, что при использовании этого параметра содержимое не защищено при передаче или в хранилище.</span><span class="sxs-lookup"><span data-stu-id="9d05b-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="9d05b-126">Используйте этот параметр, если MP4-файл планируется доставить с помощью поэтапного скачивания.</span><span class="sxs-lookup"><span data-stu-id="9d05b-126">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="9d05b-127">**CommonEncryption** — используйте этот параметр при отправке содержимого, которое уже зашифровано и защищено с помощью стандартного шифрования или PlayReady DRM (например, Smooth Streaming с защитой PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="9d05b-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="9d05b-128">**EnvelopeEncrypted** — используйте этот параметр при отправке HLS с шифрованием AES.</span><span class="sxs-lookup"><span data-stu-id="9d05b-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="9d05b-129">Обратите внимание, что файлы должны быть закодированы и зашифрованы с помощью Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="9d05b-129">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="9d05b-130">**StorageEncrypted** — шифрует незашифрованное содержимое локально с помощью 256-разрядного алгоритма шифрования AES-256, а затем отправляет его в службу хранилища Azure, где оно хранится в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="9d05b-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="9d05b-131">Активы, защищенные с помощью шифрования хранилища, автоматически расшифровываются и помещаются в систему зашифрованных файлов до кодирования и при необходимости повторно кодируются до отправки в виде нового выходного актива.</span><span class="sxs-lookup"><span data-stu-id="9d05b-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="9d05b-132">Основная причина использования шифрования хранилища — если нужно защитить входные файлы мультимедиа высокого качества с помощью стойкого шифрования при хранении на диске.</span><span class="sxs-lookup"><span data-stu-id="9d05b-132">The primary use case for Storage Encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="9d05b-133">Службы мультимедиа обеспечивают шифрование ресурсов на диске в хранилище, а не по сети, как технология управления цифровыми правами (DRM).</span><span class="sxs-lookup"><span data-stu-id="9d05b-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="9d05b-134">Если ресурс зашифрован в хранилище, необходимо настроить политику доставки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9d05b-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="9d05b-135">Дополнительные сведения см. в статье [Настройка политик доставки ресурсов-контейнеров](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="9d05b-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="9d05b-136">Если для ресурса задано шифрование с использованием параметра **CommonEncrypted** или **EnvelopeEncypted**, этот ресурс необходимо связать с ключом содержимого **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="9d05b-136">If you specify for your asset to be encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need to associate your asset with a **ContentKey**.</span></span> <span data-ttu-id="9d05b-137">Дополнительные сведения см. в статье [Создание ContentKey с использованием .NET](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="9d05b-137">For more information, see [How to create a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="9d05b-138">Если для ресурса задано шифрование с использованием параметра **StorageEncrypted**, пакет SDK служб мультимедиа для .NET создаст для ресурса зашифрованный в хранилище ключ содержимого (**StorateEncrypted** **ContentKey**).</span><span class="sxs-lookup"><span data-stu-id="9d05b-138">If you specify for your asset to be encrypted with a **StorageEncrypted** option, the Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="9d05b-139">В этом разделе показано, как использовать пакет SDK служб мультимедиа для .NET, а также расширения пакета SDK служб мультимедиа для .NET для передачи файлов в ресурс-контейнер служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="9d05b-139">This topic shows how to use Media Services .NET SDK as well as Media Services .NET SDK extensions to upload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="9d05b-140">Передача одного файла с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="9d05b-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="9d05b-141">Следующий пример кода использует пакет SDK для .NET для отправки одного файла.</span><span class="sxs-lookup"><span data-stu-id="9d05b-141">The sample code below uses .NET SDK to upload a single file.</span></span> <span data-ttu-id="9d05b-142">Свойства AccessPolicy и Locator создаются и удаляются с помощью функции Upload.</span><span class="sxs-lookup"><span data-stu-id="9d05b-142">The AccessPolicy and Locator are created and destroyed by the Upload function.</span></span> 


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


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="9d05b-143">Передача нескольких файлов с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="9d05b-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="9d05b-144">В следующем примере кода показано, как создать актив и отправить несколько файлов.</span><span class="sxs-lookup"><span data-stu-id="9d05b-144">The following code shows how to create an asset and upload multiple files.</span></span>

<span data-ttu-id="9d05b-145">Код делает следующее:</span><span class="sxs-lookup"><span data-stu-id="9d05b-145">The code does the following:</span></span>

* <span data-ttu-id="9d05b-146">Создает пустой ресурс, используя метод CreateEmptyAsset, определенный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="9d05b-146">Creates an empty asset using the CreateEmptyAsset method defined in the previous step.</span></span>
* <span data-ttu-id="9d05b-147">Создает экземпляр **AccessPolicy** , определяющий разрешения и длительность доступа к ресурсу.</span><span class="sxs-lookup"><span data-stu-id="9d05b-147">Creates an **AccessPolicy** instance that defines the permissions and duration of access to the asset.</span></span>
* <span data-ttu-id="9d05b-148">Создает экземпляр **Locator** , который предоставляет доступ к ресурсу.</span><span class="sxs-lookup"><span data-stu-id="9d05b-148">Creates a **Locator** instance that provides access to the asset.</span></span>
* <span data-ttu-id="9d05b-149">Создает экземпляр **BlobTransferClient** .</span><span class="sxs-lookup"><span data-stu-id="9d05b-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="9d05b-150">Этот тип представляет клиент, работающий с большим двоичным объектом Azure.</span><span class="sxs-lookup"><span data-stu-id="9d05b-150">This type represents a client that operates on the Azure blobs.</span></span> <span data-ttu-id="9d05b-151">В этом примере используется клиент для отслеживания хода выполнения передачи.</span><span class="sxs-lookup"><span data-stu-id="9d05b-151">In this example we use the client to monitor the upload progress.</span></span> 
* <span data-ttu-id="9d05b-152">Перечисляет файлы в указанном каталоге и создает экземпляр **AssetFile** для каждого файла.</span><span class="sxs-lookup"><span data-stu-id="9d05b-152">Enumerates through files in the specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="9d05b-153">Передает файлы в службы мультимедиа с помощью метода **UploadAsync** .</span><span class="sxs-lookup"><span data-stu-id="9d05b-153">Uploads the files into Media Services using the **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="9d05b-154">Используйте метод UploadAsync, гарантирующий, что вызовы не будут блокироваться, а файлы будут загружаться в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="9d05b-154">Use the UploadAsync method to ensure that the calls are not blocking and the files are uploaded in parallel.</span></span>
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

                // It is recommended to validate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading the files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as the upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="9d05b-155">При передаче большого количества ресурсов необходимо учитывать следующее.</span><span class="sxs-lookup"><span data-stu-id="9d05b-155">When uploading a large number of assets, consider the following.</span></span>

* <span data-ttu-id="9d05b-156">Создайте новый объект **CloudMediaContext** в каждом потоке.</span><span class="sxs-lookup"><span data-stu-id="9d05b-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="9d05b-157">Класс **CloudMediaContext** не является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="9d05b-157">The **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="9d05b-158">Замените для NumberOfConcurrentTransfers значение по умолчанию (2) более высоким значением, например 5.</span><span class="sxs-lookup"><span data-stu-id="9d05b-158">Increase NumberOfConcurrentTransfers from the default value of 2 to a higher value like 5.</span></span> <span data-ttu-id="9d05b-159">Задание этого свойства влияет на все экземпляры **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="9d05b-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="9d05b-160">Оставьте для ParallelTransferThreadCount значение по умолчанию (10).</span><span class="sxs-lookup"><span data-stu-id="9d05b-160">Keep ParallelTransferThreadCount at the default value of 10.</span></span>

## <span data-ttu-id="9d05b-161"><a id="ingest_in_bulk"></a>Массовый прием ресурсов с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="9d05b-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="9d05b-162">Передача больших файлов ресурсов может оказаться узким местом при создании ресурса.</span><span class="sxs-lookup"><span data-stu-id="9d05b-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="9d05b-163">Массовый прием ресурсов предполагает отделение создания ресурса от процесса передачи.</span><span class="sxs-lookup"><span data-stu-id="9d05b-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from the upload process.</span></span> <span data-ttu-id="9d05b-164">Чтобы использовать массовый прием ресурсов, создайте манифест (IngestManifest), описывающий ресурс и связанные с ним файлы.</span><span class="sxs-lookup"><span data-stu-id="9d05b-164">To use a bulk ingesting approach, create a manifest (IngestManifest) that describes the asset and its associated files.</span></span> <span data-ttu-id="9d05b-165">Затем воспользуйтесь методом передачи по своему усмотрению, чтобы передать связанные файлы в контейнер больших двоичных объектов манифеста.</span><span class="sxs-lookup"><span data-stu-id="9d05b-165">Then use the upload method of your choice to upload the associated files to the manifest’s blob container.</span></span> <span data-ttu-id="9d05b-166">Службы мультимедиа Microsoft Azure отслеживают контейнер больших двоичных объектов, связанный с манифестом.</span><span class="sxs-lookup"><span data-stu-id="9d05b-166">Microsoft Azure Media Services watches the blob container associated with the manifest.</span></span> <span data-ttu-id="9d05b-167">После загрузки файла в контейнер больших двоичных объектов службы мультимедиа Microsoft Azure завершает создание ресурса на основе конфигурации ресурса в манифесте (IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="9d05b-167">Once a file is uploaded to the blob container, Microsoft Azure Media Services completes the asset creation based on the configuration of the asset in the manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="9d05b-168">Для создания новой сущности IngestManifest вызовите метод Create, предоставляемый коллекцией IngestManifests в классе CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="9d05b-168">To create a new IngestManifest call the Create method exposed by the IngestManifests collection on the CloudMediaContext.</span></span> <span data-ttu-id="9d05b-169">Этот метод создаст новую сущность IngestManifest с указанным именем манифеста.</span><span class="sxs-lookup"><span data-stu-id="9d05b-169">This method will create a new IngestManifest with the manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="9d05b-170">Создайте ресурсы, которые будут связаны с массовой сущностью IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="9d05b-170">Create the assets that will be associated with the bulk IngestManifest.</span></span> <span data-ttu-id="9d05b-171">Настройте необходимые параметры шифрования ресурса для массового приема.</span><span class="sxs-lookup"><span data-stu-id="9d05b-171">Configure the desired encryption options on the asset for bulk ingesting.</span></span>

    // Create the assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="9d05b-172">Сущность IngestManifestAsset связывает ресурс с массовой сущностью IngestManifest для массового приема.</span><span class="sxs-lookup"><span data-stu-id="9d05b-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="9d05b-173">Она также связывает сущности AssetFile, из которых состоит каждый ресурс.</span><span class="sxs-lookup"><span data-stu-id="9d05b-173">It also associates the AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="9d05b-174">Чтобы создать IngestManifestAsset, используйте метод Create в контексте сервера.</span><span class="sxs-lookup"><span data-stu-id="9d05b-174">To create an IngestManifestAsset, use the Create method on the server context.</span></span>

<span data-ttu-id="9d05b-175">В следующем примере показано добавление двух новых сущностей IngestManifestAsset, связывающих два созданных ранее ресурса с манифестом массового приема.</span><span class="sxs-lookup"><span data-stu-id="9d05b-175">The following example demonstrates adding two new IngestManifestAssets that associate the two assets previously created to the bulk ingest manifest.</span></span> <span data-ttu-id="9d05b-176">Каждая сущность IngestManifestAsset связывает также набор файлов, которые передаются для каждого ресурса во время массового приема.</span><span class="sxs-lookup"><span data-stu-id="9d05b-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="9d05b-177">При этом можно использовать любое высокоскоростное клиентское приложение, которое может передавать файлы ресурсов по универсальному коду ресурса (URI) контейнера хранилища больших двоичных объектов, предоставляемому свойством **IIngestManifest.BlobStorageUriForUpload** сущности IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="9d05b-177">You can use any high speed client application capable of uploading the asset files to the blob storage container URI provided by the **IIngestManifest.BlobStorageUriForUpload** property of the IngestManifest.</span></span> <span data-ttu-id="9d05b-178">[Приложение Aspera On Demand for Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6)— одна из наиболее примечательных служб высокоскоростной передачи.</span><span class="sxs-lookup"><span data-stu-id="9d05b-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="9d05b-179">Кроме того, можно написать код для передачи файлов ресурсов, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="9d05b-179">You can also write code to upload the assets files as shown in the following code example.</span></span>

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

<span data-ttu-id="9d05b-180">В следующем примере показан код для передачи файлов ресурса-контейнера для примера, используемого в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="9d05b-180">The code for uploading the asset files for the sample used in this topic is shown in the following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="9d05b-181">Ход выполнения массового приема для всех ресурсов, связанных с **IngestManifest**, можно определить с помощью опроса по свойству Statistics сущности **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="9d05b-181">You can determine the progress of the bulk ingesting for all assets associated with an **IngestManifest** by polling the Statistics property of the **IngestManifest**.</span></span> <span data-ttu-id="9d05b-182">Чтобы получать обновленную информацию о ходе выполнения, необходимо использовать новый класс **CloudMediaContext** при каждом опросе по свойству Statistics.</span><span class="sxs-lookup"><span data-stu-id="9d05b-182">In order to update progress information, you must use a new **CloudMediaContext** each time you poll the Statistics property.</span></span>

<span data-ttu-id="9d05b-183">В следующем примере демонстрируется опрос сущности IngestManifest по ее идентификатору **Id**.</span><span class="sxs-lookup"><span data-stu-id="9d05b-183">The following example demonstrates polling an IngestManifest by its **Id**.</span></span>

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



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="9d05b-184">Передача файлов с помощью расширений пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="9d05b-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="9d05b-185">В приведенном ниже примере показано, как передать один файл с помощью расширений пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="9d05b-185">The example below shows how to upload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="9d05b-186">В этом случае используется метод **CreateFromFile**, но доступна также и асинхронная версия (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="9d05b-186">In this case the **CreateFromFile** method is used, but the asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="9d05b-187">Метод **CreateFromFile** позволяет указать имя файла, параметр шифрования и обратный вызов, чтобы сообщать о ходе передачи файла.</span><span class="sxs-lookup"><span data-stu-id="9d05b-187">The **CreateFromFile** method lets you specify the file name, encryption option, and a callback in order to report the upload progress of the file.</span></span>

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

<span data-ttu-id="9d05b-188">В следующем примере вызывается функция UploadFile, а в качестве параметра создания ресурса указывается шифрование хранилища.</span><span class="sxs-lookup"><span data-stu-id="9d05b-188">The following example calls UploadFile function and specifies storage encryption as the asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="9d05b-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9d05b-189">Next steps</span></span>

<span data-ttu-id="9d05b-190">Теперь можно закодировать отправленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9d05b-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="9d05b-191">Дополнительную информацию см. в статье, посвященной [кодированию ресурсов](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="9d05b-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="9d05b-192">Можно также использовать функции Azure для запуска задания кодирования на основе файла, поступающего в настроенный контейнер.</span><span class="sxs-lookup"><span data-stu-id="9d05b-192">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="9d05b-193">Дополнительные сведения см. в [этом примере](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="9d05b-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="9d05b-194">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="9d05b-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9d05b-195">Отзывы</span><span class="sxs-lookup"><span data-stu-id="9d05b-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="9d05b-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9d05b-196">Next step</span></span>
<span data-ttu-id="9d05b-197">Передав ресурс в службы мультимедиа, перейдите к статье [Получение экземпляра процессора мультимедиа][How to Get a Media Processor].</span><span class="sxs-lookup"><span data-stu-id="9d05b-197">Now that you have uploaded an asset to Media Services, go to the [How to Get a Media Processor][How to Get a Media Processor] topic.</span></span>

[How to Get a Media Processor]: media-services-get-media-processor.md

