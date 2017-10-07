---
title: "отработка отказа aaaImplement потоковой передачи с помощью служб мультимедиа Azure | Документы Microsoft"
description: "В этом разделе показано, как tooimplement отказоустойчивого потоковой передачи."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fc45d849-eb0d-4739-ae91-0ff648113445
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako
ms.openlocfilehash: ade0bace57f35ab3ed855d3a98f743e08da4f324
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="implement-failover-streaming-with-azure-media-services"></a><span data-ttu-id="3a775-103">Реализация потоковой передачи отработки отказа с помощью служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="3a775-103">Implement failover streaming with Azure Media Services</span></span>

<span data-ttu-id="3a775-104">В этом пошаговом руководстве показано, как содержимое toocopy (BLOB) из одного актива в другую в порядке toohandle избыточность для потоковой передачи по требованию.</span><span class="sxs-lookup"><span data-stu-id="3a775-104">This walkthrough demonstrates how toocopy content (blobs) from one asset into another in order toohandle redundancy for on-demand streaming.</span></span> <span data-ttu-id="3a775-105">Этот сценарий полезен, если требуется tooset вверх сеть доставки содержимого Azure toofail к между двумя центрами обработки данных, в случае сбоя в одном центре данных.</span><span class="sxs-lookup"><span data-stu-id="3a775-105">This scenario is useful if you want tooset up Azure Content Delivery Network toofail over between two datacenters, in case of an outage in one datacenter.</span></span> <span data-ttu-id="3a775-106">В этом пошаговом руководстве используется hello Azure Media Services SDK, API REST служб мультимедиа Azure hello и hello пакет SDK хранилища Azure toodemonstrate hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="3a775-106">This walkthrough uses hello Azure Media Services SDK, hello Azure Media Services REST API, and hello Azure Storage SDK toodemonstrate hello following tasks:</span></span>

1. <span data-ttu-id="3a775-107">Настройка учетной записи для служб мультимедиа в "Центре обработки данных A".</span><span class="sxs-lookup"><span data-stu-id="3a775-107">Set up a Media Services account in "Data Center A."</span></span>
2. <span data-ttu-id="3a775-108">отправка мезонинного файла в исходный ресурс;</span><span class="sxs-lookup"><span data-stu-id="3a775-108">Upload a mezzanine file into a source asset.</span></span>
3. <span data-ttu-id="3a775-109">Кодирование активов hello в нескольких битах скорость MP4-файлов.</span><span class="sxs-lookup"><span data-stu-id="3a775-109">Encode hello asset into multi-bit rate MP4 files.</span></span> 
4. <span data-ttu-id="3a775-110">Создание доступного только для чтения указателя подписанного URL-адреса,</span><span class="sxs-lookup"><span data-stu-id="3a775-110">Create a read-only shared access signature locator.</span></span> <span data-ttu-id="3a775-111">Это необходимо для hello исходный активов toohave доступ для чтения toohello контейнер в учетной записи хранения hello, связанный с активом источника hello.</span><span class="sxs-lookup"><span data-stu-id="3a775-111">This is for hello source asset toohave read access toohello container in hello storage account that is associated with hello source asset.</span></span>
5. <span data-ttu-id="3a775-112">Получите имя контейнера hello hello исходный ресурс из локатора подписи общего доступа только для чтения hello, на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="3a775-112">Get hello container name of hello source asset from hello read-only shared access signature locator created in hello previous step.</span></span> <span data-ttu-id="3a775-113">Это необходимо для копирования больших двоичных объектов между учетными записями хранения (описано ниже в разделе hello).</span><span class="sxs-lookup"><span data-stu-id="3a775-113">This is necessary for copying blobs between storage accounts (explained later in hello topic.)</span></span>
6. <span data-ttu-id="3a775-114">Создание указателя origin для hello актива, который был создан путем кодирования задача hello.</span><span class="sxs-lookup"><span data-stu-id="3a775-114">Create an origin locator for hello asset that was created by hello encoding task.</span></span> 

<span data-ttu-id="3a775-115">Затем toohandle hello отработки отказа:</span><span class="sxs-lookup"><span data-stu-id="3a775-115">Then, toohandle hello failover:</span></span>

1. <span data-ttu-id="3a775-116">Настройка учетной записи для служб мультимедиа в "Центре обработки данных B".</span><span class="sxs-lookup"><span data-stu-id="3a775-116">Set up a Media Services account in "Data Center B."</span></span>
2. <span data-ttu-id="3a775-117">Создайте пустой актив целевой в целевом hello учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="3a775-117">Create a target empty asset in hello target Media Services account.</span></span>
3. <span data-ttu-id="3a775-118">Создание доступного для записи указателя подписанного URL-адреса,</span><span class="sxs-lookup"><span data-stu-id="3a775-118">Create a write shared access signature locator.</span></span> <span data-ttu-id="3a775-119">Это необходимо для hello целевой пустой актив toohave доступ на запись toohello контейнер в hello целевой учетной записи хранения, связанный с hello целевого ресурса.</span><span class="sxs-lookup"><span data-stu-id="3a775-119">This is for hello target empty asset toohave write access toohello container in hello target storage account that is associated with hello target asset.</span></span>
4. <span data-ttu-id="3a775-120">Используйте hello пакет SDK хранилища Azure toocopy BLOB-объектов (файлов ресурсов) между учетную запись хранилища источника hello в «Центре обработки данных A» и hello целевой учетной записи хранения в «B. центра данных»</span><span class="sxs-lookup"><span data-stu-id="3a775-120">Use hello Azure Storage SDK toocopy blobs (asset files) between hello source storage account in "Data Center A" and hello target storage account in "Data Center B."</span></span> <span data-ttu-id="3a775-121">Эти учетные записи хранения связаны с активы hello интерес.</span><span class="sxs-lookup"><span data-stu-id="3a775-121">These storage accounts are associated with hello assets of interest.</span></span>
5. <span data-ttu-id="3a775-122">Свяжите BLOB-объектов (файлов ресурсов), скопированный toohello целевой контейнер больших двоичных объектов с hello целевого ресурса.</span><span class="sxs-lookup"><span data-stu-id="3a775-122">Associate blobs (asset files) that were copied toohello target blob container with hello target asset.</span></span> 
6. <span data-ttu-id="3a775-123">Создание указателя origin для средства hello в «B центра данных» и укажите идентификатор локатора hello, созданный для средства hello в «Центре обработки данных а.»</span><span class="sxs-lookup"><span data-stu-id="3a775-123">Create an origin locator for hello asset in "Data Center B", and specify hello locator ID that was generated for hello asset in "Data Center A."</span></span>

<span data-ttu-id="3a775-124">Это дает hello потоковой передачи URL-адреса которых hello относительные пути URL-адреса hello hello же (только hello базовый URL-адреса отличаются).</span><span class="sxs-lookup"><span data-stu-id="3a775-124">This gives you hello streaming URLs where hello relative paths of hello URLs are hello same (only hello base URLs are different).</span></span> 

<span data-ttu-id="3a775-125">Затем toohandle любые сбои в работе, можно создать сеть доставки содержимого на основе этих локаторы источника.</span><span class="sxs-lookup"><span data-stu-id="3a775-125">Then, toohandle any outages, you can create a Content Delivery Network on top of these origin locators.</span></span> 

<span data-ttu-id="3a775-126">применить Hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="3a775-126">hello following considerations apply:</span></span>

* <span data-ttu-id="3a775-127">Текущая версия пакета SDK служб мультимедиа Hello не поддерживает программным путем создания IAssetFile сведения, будет воспринимать актива с помощью файлов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3a775-127">hello current version of Media Services SDK does not support programmatically generating IAssetFile information that would associate an asset with asset files.</span></span> <span data-ttu-id="3a775-128">Вместо этого используйте API REST служб мультимедиа CreateFileInfos toodo hello это.</span><span class="sxs-lookup"><span data-stu-id="3a775-128">Instead, use hello CreateFileInfos Media Services REST API toodo this.</span></span> 
* <span data-ttu-id="3a775-129">Зашифрованные активы хранилища (AssetCreationOptions.StorageEncrypted) не поддерживаются для репликации (так как ключ шифрования hello отличается в обе учетные записи служб мультимедиа).</span><span class="sxs-lookup"><span data-stu-id="3a775-129">Storage encrypted assets (AssetCreationOptions.StorageEncrypted) are not supported for replication (because hello encryption key is different in both Media Services accounts).</span></span> 
* <span data-ttu-id="3a775-130">Если вы хотите tootake преимуществами динамической упаковки, убедитесь, что hello потоковой передачи конечной точки, из которого нужно toostream содержимого находится в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="3a775-130">If you want tootake advantage of dynamic packaging, make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>

> [!NOTE]
> <span data-ttu-id="3a775-131">Рассмотрите возможность использования служб мультимедиа hello [средство Replicator](http://replicator.codeplex.com/) как альтернативный tooimplementing a отработки отказа, сценарий потоковой передачи вручную.</span><span class="sxs-lookup"><span data-stu-id="3a775-131">Consider using hello Media Services [Replicator Tool](http://replicator.codeplex.com/) as an alternative tooimplementing a failover streaming scenario manually.</span></span> <span data-ttu-id="3a775-132">Это средство позволяет tooreplicate активы по две учетные записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="3a775-132">This tool allows you tooreplicate assets across two Media Services accounts.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3a775-133">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3a775-133">Prerequisites</span></span>
* <span data-ttu-id="3a775-134">Две учетные записи служб мультимедиа в новой или существующей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="3a775-134">Two Media Services accounts in a new or existing Azure subscription.</span></span> <span data-ttu-id="3a775-135">В разделе [как учетную запись служб мультимедиа tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="3a775-135">See [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="3a775-136">Операционные системы: Windows 7, Windows 2008 R2 или Windows 8.</span><span class="sxs-lookup"><span data-stu-id="3a775-136">Operating system: Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="3a775-137">.NET Framework 4.5 или .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="3a775-137">.NET Framework 4.5 or .NET Framework 4.</span></span>
* <span data-ttu-id="3a775-138">Visual Studio 2010 с пакетом обновления 1 или более поздней версии (Professional, Premium, Ultimate или Express).</span><span class="sxs-lookup"><span data-stu-id="3a775-138">Visual Studio 2010 SP1 or later version (Professional, Premium, Ultimate, or Express).</span></span>

## <a name="set-up-your-project"></a><span data-ttu-id="3a775-139">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="3a775-139">Set up your project</span></span>
<span data-ttu-id="3a775-140">В этом разделе вы создадите и настроите проект консольного приложения на C#.</span><span class="sxs-lookup"><span data-stu-id="3a775-140">In this section, you create and set up a C# Console Application project.</span></span>

1. <span data-ttu-id="3a775-141">С помощью Visual Studio toocreate новое решение, содержащее проект консольного приложения C# hello.</span><span class="sxs-lookup"><span data-stu-id="3a775-141">Use Visual Studio toocreate a new solution that contains hello C# Console Application project.</span></span> <span data-ttu-id="3a775-142">Введите **HandleRedundancyForOnDemandStreaming** hello имя, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3a775-142">Enter **HandleRedundancyForOnDemandStreaming** for hello name, and then click **OK**.</span></span>
2. <span data-ttu-id="3a775-143">Создать hello **SupportFiles** папку на hello же уровня как hello **HandleRedundancyForOnDemandStreaming.csproj** файл проекта.</span><span class="sxs-lookup"><span data-stu-id="3a775-143">Create hello **SupportFiles** folder on hello same level as hello **HandleRedundancyForOnDemandStreaming.csproj** project file.</span></span> <span data-ttu-id="3a775-144">В разделе hello **SupportFiles** папки, создать hello **OutputFiles** и **MP4Files** папки.</span><span class="sxs-lookup"><span data-stu-id="3a775-144">Under hello **SupportFiles** folder, create hello **OutputFiles** and **MP4Files** folders.</span></span> <span data-ttu-id="3a775-145">Скопируйте MP4-файл в hello **MP4Files** папки.</span><span class="sxs-lookup"><span data-stu-id="3a775-145">Copy an .mp4 file into hello **MP4Files** folder.</span></span> <span data-ttu-id="3a775-146">(В этом примере hello **BigBuckBunny.mp4** файл используется.)</span><span class="sxs-lookup"><span data-stu-id="3a775-146">(In this example, hello **BigBuckBunny.mp4** file is used.)</span></span> 
3. <span data-ttu-id="3a775-147">Используйте **Nuget** tooMedia служб, связанных с tooDLLs tooadd ссылки.</span><span class="sxs-lookup"><span data-stu-id="3a775-147">Use **Nuget** tooadd references tooDLLs related tooMedia Services.</span></span> <span data-ttu-id="3a775-148">В **главном меню Visual Studio** выберите **Инструменты** > **Library Package Manager** (Диспетчер пакетов библиотеки) > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="3a775-148">In **Visual Studio Main Menu**, select **TOOLS** > **Library Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="3a775-149">В окне консоли hello, введите **windowsazure.mediaservices Install-Package**, и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="3a775-149">In hello console window, type **Install-Package windowsazure.mediaservices**, and press Enter.</span></span>
4. <span data-ttu-id="3a775-150">Добавьте другие ссылки, необходимые для этого проекта: System.Configuration, System.Runtime.Serialization и System.Web.</span><span class="sxs-lookup"><span data-stu-id="3a775-150">Add other references that are required for this project: System.Configuration, System.Runtime.Serialization, and System.Web.</span></span>
5. <span data-ttu-id="3a775-151">Замените **с помощью** инструкций, которые были добавлены toohello **Programs.cs** файла по умолчанию hello следующие объекты:</span><span class="sxs-lookup"><span data-stu-id="3a775-151">Replace **using** statements that were added toohello **Programs.cs** file by default with hello following ones:</span></span>
   
        using System;
        using System.Configuration;
        using System.Globalization;
        using System.IO;
        using System.Net;
        using System.Runtime.Serialization.Json;
        using System.Text;
        using System.Threading;
        using System.Threading.Tasks;
        using System.Web;
        using System.Xml;
        using System.Linq;
        using Microsoft.WindowsAzure;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using Microsoft.WindowsAzure.Storage.Auth;
6. <span data-ttu-id="3a775-152">Добавить hello **appSettings** toohello раздел **.config** файла и обновлять значения hello на основе Media Services и хранилища ключей и имя значения.</span><span class="sxs-lookup"><span data-stu-id="3a775-152">Add hello **appSettings** section toohello **.config** file, and update hello values based on your Media Services and Storage key and name values.</span></span> 
   
        <appSettings>
          <add key="MediaServicesAccountNameSource" value="Media-Services-Account-Name-Source"/>
          <add key="MediaServicesAccountKeySource" value="Media-Services-Account-Key-Source"/>
          <add key="MediaServicesStorageAccountNameSource" value="Media-Services-Storage-Account-Name-Source"/>
          <add key="MediaServicesStorageAccountKeySource" value="Media-Services-Storage-Account-Key-Source"/>
          <add key="MediaServicesAccountNameTarget" value="Media-Services-Account-Name-Target" />
          <add key="MediaServicesAccountKeyTarget" value=" Media-Services-Account-Key-Target" />
          <add key="MediaServicesStorageAccountNameTarget" value=" Media-Services-Storage-Account-Name-Target" />
          <add key="MediaServicesStorageAccountKeyTarget" value=" Media-Services-Storage-Account-Key-Target" />
        </appSettings>

## <a name="add-code-that-handles-redundancy-for-on-demand-streaming"></a><span data-ttu-id="3a775-153">Добавление кода, обрабатывающего избыточность потокового воспроизведения по запросу</span><span class="sxs-lookup"><span data-stu-id="3a775-153">Add code that handles redundancy for on-demand streaming</span></span>
<span data-ttu-id="3a775-154">В этом разделе создайте hello возможность toohandle избыточности.</span><span class="sxs-lookup"><span data-stu-id="3a775-154">In this section, you create hello ability toohandle redundancy.</span></span>

1. <span data-ttu-id="3a775-155">Добавьте следующий класс Program toohello поля уровня класса hello.</span><span class="sxs-lookup"><span data-stu-id="3a775-155">Add hello following class-level fields toohello Program class.</span></span>
       
        // Read values from hello App.config file.
        private static readonly string MediaServicesAccountNameSource = ConfigurationManager.AppSettings["MediaServicesAccountNameSource"];
        private static readonly string MediaServicesAccountKeySource = ConfigurationManager.AppSettings["MediaServicesAccountKeySource"];
        private static readonly string StorageNameSource = ConfigurationManager.AppSettings["MediaServicesStorageAccountNameSource"];
        private static readonly string StorageKeySource = ConfigurationManager.AppSettings["MediaServicesStorageAccountKeySource"];
        
        private static readonly string MediaServicesAccountNameTarget = ConfigurationManager.AppSettings["MediaServicesAccountNameTarget"];
        private static readonly string MediaServicesAccountKeyTarget = ConfigurationManager.AppSettings["MediaServicesAccountKeyTarget"];
        private static readonly string StorageNameTarget = ConfigurationManager.AppSettings["MediaServicesStorageAccountNameTarget"];
        private static readonly string StorageKeyTarget = ConfigurationManager.AppSettings["MediaServicesStorageAccountKeyTarget"];
        
        // Base support files path.  Update this field toopoint toohello base path  
        // for hello local support files folder that you create. 
        private static readonly string SupportFiles = Path.GetFullPath(@"../..\SupportFiles");
        
        // Paths toosupport files (within hello above base path). 
        private static readonly string SingleInputMp4Path = Path.GetFullPath(SupportFiles + @"\MP4Files\BigBuckBunny.mp4");
        private static readonly string OutputFilesFolder = Path.GetFullPath(SupportFiles + @"\OutputFiles");
        
        // Class-level field used tookeep a reference toohello service context.
        static private CloudMediaContext _contextSource = null;
        static private CloudMediaContext _contextTarget = null;
        static private MediaServicesCredentials _cachedCredentialsSource = null;
        static private MediaServicesCredentials _cachedCredentialsTarget = null;

2. <span data-ttu-id="3a775-156">Замените определение метода Main по умолчанию hello одном hello.</span><span class="sxs-lookup"><span data-stu-id="3a775-156">Replace hello default Main method definition with hello following one.</span></span> <span data-ttu-id="3a775-157">Определения методов, вызываемых из метода Main, описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="3a775-157">Method definitions that are called from Main are defined below.</span></span>
        
        static void Main(string[] args)
        {
            _cachedCredentialsSource = new MediaServicesCredentials(
                            MediaServicesAccountNameSource,
                            MediaServicesAccountKeySource);
        
            _cachedCredentialsTarget = new MediaServicesCredentials(
                            MediaServicesAccountNameTarget,
                            MediaServicesAccountKeyTarget);
        
            // Get server context.    
            _contextSource = new CloudMediaContext(_cachedCredentialsSource);
            _contextTarget = new CloudMediaContext(_cachedCredentialsTarget);
        
            IAsset assetSingleFile = CreateAssetAndUploadSingleFile(_contextSource,
                                        AssetCreationOptions.None,
                                        SingleInputMp4Path);
        
            IJob job = CreateEncodingJob(_contextSource, assetSingleFile);
        
            if (job.State != JobState.Error)
            {
                IAsset sourceOutputAsset = job.OutputMediaAssets[0];
                // Get hello locator for Smooth Streaming
                var sourceOriginLocator = GetStreamingOriginLocator(_contextSource, sourceOutputAsset);
        
                Console.WriteLine("Locator Id: {0}", sourceOriginLocator.Id);
                
                // 1.Create a read-only SAS locator for hello source asset toohave read access toohello container in hello source Storage account (associated with hello source Media Services account)
                var readSasLocator = GetSasReadLocator(_contextSource, sourceOutputAsset);
        
                // 2.Get hello container name of hello source asset from hello read-only SAS locator created in hello previous step
                string containerName = (new Uri(readSasLocator.Path)).Segments[1];
        
                // 3.Create a target empty asset in hello target Media Services account
                var targetAsset = CreateTargetEmptyAsset(_contextTarget, containerName);
        
                // 4.Create a write SAS locator for hello target empty asset toohave write access toohello container in hello target Storage account (associated with hello target Media Services account)
                ILocator writeSasLocator = CreateSasWriteLocator(_contextTarget, targetAsset);
        
                // Get asset container name.
                string targetContainerName = (new Uri(writeSasLocator.Path)).Segments[1];
        
                // 5.Copy hello blobs in hello source container (source asset) toohello target container (target empty asset)
                CopyBlobsFromDifferentStorage(containerName, targetContainerName, StorageNameSource, StorageKeySource, StorageNameTarget, StorageKeyTarget);
        
                // 6.Use hello CreateFileInfos Media Services REST API tooautomatically generate all hello IAssetFile’s for hello target asset. 
                //      This API call is not supported in hello current Media Services SDK for .NET. 
                CreateFileInfosForAssetWithRest(_contextTarget, targetAsset, MediaServicesAccountNameTarget, MediaServicesAccountKeyTarget);
        
                // Check if hello AssetFiles are now  associated with hello asset.
                Console.WriteLine("Asset files assocated with hello {0} asset:", targetAsset.Name);
                foreach (var af in targetAsset.AssetFiles)
                {
                    Console.WriteLine(af.Name);
                }
        
                // 7.Copy hello Origin locator of hello source asset toohello target asset by using hello same Id
                var replicatedLocatorPath = CreateOriginLocatorWithRest(_contextTarget,
                            MediaServicesAccountNameTarget, MediaServicesAccountKeyTarget,
                            sourceOriginLocator.Id, targetAsset.Id);
        
                // Create a full URL toohello manifest file. Use this for playback
                // in streaming media clients. 
                string originalUrlForClientStreaming = sourceOriginLocator.Path + GetPrimaryFile(sourceOutputAsset).Name + "/manifest";
        
                Console.WriteLine("Original Locator Path: {0}\n", originalUrlForClientStreaming);
        
                string replicatedUrlForClientStreaming = replicatedLocatorPath + GetPrimaryFile(sourceOutputAsset).Name + "/manifest";
        
                Console.WriteLine("Replicated Locator Path: {0}", replicatedUrlForClientStreaming);
        
                readSasLocator.Delete();
                writeSasLocator.Delete();
        }

3. <span data-ttu-id="3a775-158">Hello после определения метода вызываются из метода Main.</span><span class="sxs-lookup"><span data-stu-id="3a775-158">hello following method definitions are called from Main.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3a775-159">Действует ограничение в 1 000 000 записей для разных политик служб мультимедиа (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="3a775-159">There is a limit of 1,000,000 policies for different Media Services policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="3a775-160">Следует использовать hello же идентификатор политики, если вы используете всегда hello же дней и доступа разрешения.</span><span class="sxs-lookup"><span data-stu-id="3a775-160">You should use hello same policy ID if you are always using hello same days and access permissions.</span></span> <span data-ttu-id="3a775-161">Например используйте hello таким же ИДЕНТИФИКАТОРОМ для политик указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="3a775-161">For example, use hello same ID for policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="3a775-162">Дополнительные сведения см. в [этом разделе](media-services-dotnet-manage-entities.md#limit-access-policies).</span><span class="sxs-lookup"><span data-stu-id="3a775-162">For more information, see [this topic](media-services-dotnet-manage-entities.md#limit-access-policies).</span></span>

        public static IAsset CreateAssetAndUploadSingleFile(CloudMediaContext context,
                                                        AssetCreationOptions assetCreationOptions,
                                                        string singleFilePath)
        {
            var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
   
            var asset = context.Assets.Create(assetName, assetCreationOptions);
   
            Console.WriteLine("Asset name: " + asset.Name);
   
            var fileName = Path.GetFileName(singleFilePath);
   
            var assetFile = asset.AssetFiles.Create(fileName);
   
            Console.WriteLine("Created assetFile {0}", assetFile.Name);
   
            Console.WriteLine("Upload {0}", assetFile.Name);
   
            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);
   
            return asset;
        }
   
        public static IJob CreateEncodingJob(CloudMediaContext context, IAsset asset)
        {
            // Declare a new job.
            IJob job = context.Jobs.Create("My encoding job");
   
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName(context,
                                                    "Media Encoder Standard");
   
            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.ProtectedConfiguration);
   
            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
   
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is in hello clear (unencrypted). 
            var outputAssetName = "OutputAsset_" + Guid.NewGuid();
            task.OutputAssets.AddNew(outputAssetName,
                AssetCreationOptions.None);
   
            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);
   
            // Launch hello job.
            job.Submit();
   
            // Optionally log job details. This displays basic job details
            // toohello console and saves them tooa JobDetails-{JobId}.txt file 
            // in your output folder.
            LogJobDetails(context, job.Id);
   
            // Check job execution and wait for job toofinish. 
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();
   
            // Get an updated job reference.
            job = GetJob(context, job.Id);
   
            // Since we hello output asset contains a set of Smooth Streaming files,
            // set hello .ism file toobe hello primary file
            if (job.State != JobState.Error)
                SetPrimaryFile(job.OutputMediaAssets[0]);
   
            return job;
        }
   
        public static ILocator GetStreamingOriginLocator(CloudMediaContext context, IAsset assetToStream)
        {
            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 
            IAssetFile manifestFile = GetPrimaryFile(assetToStream);
   
            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
   
            IAccessPolicy policy = context.AccessPolicies.Create("Streaming policy",
                TimeSpan.FromDays(30),
                AccessPermissions.Read);
   
            // Create a locator toohello streaming content on an origin. 
            ILocator originLocator = context.Locators.CreateLocator(LocatorType.OnDemandOrigin,
                assetToStream,
                policy,
                DateTime.UtcNow.AddMinutes(-5));
   
            // Return hello locator. 
            return originLocator;
        }
   
        public static ILocator GetSasReadLocator(CloudMediaContext context, IAsset asset)
        {
            IAccessPolicy accessPolicy = context.AccessPolicies.Create("File Download Policy",
                TimeSpan.FromDays(30), AccessPermissions.Read);
   
            ILocator sasLocator = context.Locators.CreateLocator(LocatorType.Sas,
                asset, accessPolicy);
   
            return sasLocator;
        }
   
        public static ILocator CreateSasWriteLocator(CloudMediaContext context, IAsset asset)
        {
   
            IAccessPolicy writePolicy = context.AccessPolicies.Create("Write Policy",
                TimeSpan.FromDays(30), AccessPermissions.Write);
   
            ILocator sasLocator = context.Locators.CreateLocator(LocatorType.Sas,
                asset, writePolicy);
   
            return sasLocator;
        }
   
        public static IAsset CreateTargetEmptyAsset(CloudMediaContext context, string containerName)
        {
            // Create a new asset.
            IAsset assetToBeProcessed = context.Assets.Create(containerName,
                AssetCreationOptions.None);
   
            return assetToBeProcessed;
        }
   
        public static void CreateFileInfosForAssetWithRest(CloudMediaContext context, IAsset asset, string mediaServicesAccountNameTarget,
            string mediaServicesAccountKeyTarget)
        {
            string apiServer = "";
            string scope = "";
            string acsBaseAddress = "";
   
            string acsToken = GetAcsBearerToken(mediaServicesAccountNameTarget,
                                    mediaServicesAccountKeyTarget, scope, acsBaseAddress);
   
            if (!string.IsNullOrEmpty(acsToken))
            {
                CreateFileInfos(apiServer, acsToken, asset.Id);
            }
        }
   
        public static string CreateOriginLocatorWithRest(CloudMediaContext context, string mediaServicesAccountNameTarget,
            string mediaServicesAccountKeyTarget, string locatorIdToReplicate, string targetAssetId)
        {
            //Make sure we are not asking for a duplicate:
            var locator = context.Locators.Where(l => l.Id == locatorIdToReplicate).FirstOrDefault();
            if (locator != null)
                return "";
   
            string locatorNewPath = "";
            string apiServer = "";
            string scope = "";
            string acsBaseAddress = "";
   
            string acsToken = GetAcsBearerToken(mediaServicesAccountNameTarget,
                                    mediaServicesAccountKeyTarget, scope, acsBaseAddress);
   
            if (!string.IsNullOrEmpty(acsToken))
            {
                var asset = context.Assets.Where(a => a.Id == targetAssetId).FirstOrDefault();
   
                // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
                var accessPolicy = context.AccessPolicies.Create("RestTest", TimeSpan.FromDays(100),
                                                                    AccessPermissions.Read);
                if (asset != null)
                {
                    string redirectedServiceUri = null;
   
                    var xmlResponse = CreateLocator(apiServer, out redirectedServiceUri, acsToken,
                                                                asset.Id, accessPolicy.Id,
                                                                (int)LocatorType.OnDemandOrigin,
                                                                DateTime.UtcNow.AddMinutes(-10), locatorIdToReplicate);
   
                    Console.WriteLine("Redirected to: " + redirectedServiceUri);
                    if (xmlResponse != null)
                    {
                        Console.WriteLine(String.Format("Locator Id: {0}",
                                                        xmlResponse.GetElementsByTagName("Id")[0].InnerText));
                        Console.WriteLine(String.Format("Locator Path: {0}",
                                xmlResponse.GetElementsByTagName("Path")[0].InnerText));

                        locatorNewPath = xmlResponse.GetElementsByTagName("Path")[0].InnerText;
                    }
                }
            }

            return locatorNewPath;
        }

        public static void SetPrimaryFile(IAsset asset)
        {

            var ismAssetFiles = asset.AssetFiles.ToList().
                        Where(f => f.Name.EndsWith(".ism", StringComparison.OrdinalIgnoreCase))
                        .ToArray();

            if (ismAssetFiles.Count() != 1)
                throw new ArgumentException("hello asset should have only one, .ism file");

            ismAssetFiles.First().IsPrimary = true;
            ismAssetFiles.First().Update();
        }

        public static IAssetFile GetPrimaryFile(IAsset asset)
        {
            var theManifest =
                    from f in asset.AssetFiles
                    where f.Name.EndsWith(".ism")
                    select f;

            // Cast hello reference tooa true IAssetFile type. 
            IAssetFile manifestFile = theManifest.First();

            return manifestFile;
        }

        public static IAsset RefreshAsset(CloudMediaContext context, IAsset asset)
        {
            asset = context.Assets.Where(a => a.Id == asset.Id).FirstOrDefault();
            return asset;
        }

        public static void CopyBlobsFromDifferentStorage(string sourceContainerName, string targetContainerName,
                                            string srcAccountName, string srcAccountKey,
                                            string destAccountName, string destAccountKey)
        {
            var srcAccount = new CloudStorageAccount(new StorageCredentials(srcAccountName, srcAccountKey), true);
            var destAccount = new CloudStorageAccount(new StorageCredentials(destAccountName, destAccountKey), true);

            var cloudBlobClient = srcAccount.CreateCloudBlobClient();
            var targetBlobClient = destAccount.CreateCloudBlobClient();

            var sourceContainer = cloudBlobClient.GetContainerReference(sourceContainerName);
            var targetContainer = targetBlobClient.GetContainerReference(targetContainerName);
            targetContainer.CreateIfNotExists();

            string blobToken = sourceContainer.GetSharedAccessSignature(new SharedAccessBlobPolicy()
            {
                // Specify hello expiration time for hello signature.
                SharedAccessExpiryTime = DateTime.Now.AddDays(1),
                // Specify hello permissions granted by hello signature.
                Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read
            });

            foreach (var sourceBlob in sourceContainer.ListBlobs())
            {
                string fileName = (sourceBlob as ICloudBlob).Name;
                var sourceCloudBlob = sourceContainer.GetBlockBlobReference(fileName);
                sourceCloudBlob.FetchAttributes();

                if (sourceCloudBlob.Properties.Length > 0)
                {
                    // In Azure Media Services, hello files are stored as block blobs. 
                    // Page blobs are not supported by Azure Media Services.  
                    var destinationBlob = targetContainer.GetBlockBlobReference(fileName);
                    destinationBlob.StartCopyFromBlob(new Uri(sourceBlob.Uri.AbsoluteUri + blobToken));

                    while (true)
                    {
                        // hello StartCopyFromBlob is an async operation, 
                        // so we want toocheck if hello copy operation is completed before proceeding. 
                        // toodo that, we call FetchAttributes on hello blob and check hello CopyStatus. 
                        destinationBlob.FetchAttributes();
                        if (destinationBlob.CopyState.Status != CopyStatus.Pending)
                        {
                            break;
                        }
                        //It's still not completed. So wait for some time.
                        System.Threading.Thread.Sleep(1000);
                    }
                }

                Console.WriteLine(fileName);
            }

            Console.WriteLine("Done copying.");
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(CloudMediaContext context, string mediaProcessorName)
        {

            var processor = context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        // This method is a handler for events that track job progress.   
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
                    LogJobStop(null, job.Id);
                    break;
                default:
                    break;
            }
        }

        private static void LogJobStop(CloudMediaContext context, string jobId)
        {
            StringBuilder builder = new StringBuilder();
            IJob job = GetJob(context, jobId);

            builder.AppendLine("\nThe job stopped due toocancellation or an error.");
            builder.AppendLine("***************************");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Job Name: " + job.Name);
            builder.AppendLine("Job State: " + job.State.ToString());
            builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
            // Log job errors if they exist.  
            if (job.State == JobState.Error)
            {
                builder.Append("Error Details: \n");
                foreach (ITask task in job.Tasks)
                {
                    foreach (ErrorDetail detail in task.ErrorDetails)
                    {
                        builder.AppendLine("  Task Id: " + task.Id);
                        builder.AppendLine("    Error Code: " + detail.Code);
                        builder.AppendLine("    Error Message: " + detail.Message + "\n");
                    }
                }
            }
            builder.AppendLine("***************************\n");
            // Write hello output tooa local file and toohello console. hello template 
            // for an error output file is:  JobStop-{JobId}.txt
            string outputFile = OutputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
            WriteToFile(outputFile, builder.ToString());
            Console.Write(builder.ToString());
        }

        private static void LogJobDetails(CloudMediaContext context, string jobId)
        {
            StringBuilder builder = new StringBuilder();
            IJob job = GetJob(context, jobId);

            builder.AppendLine("\nJob ID: " + job.Id);
            builder.AppendLine("Job Name: " + job.Name);
            builder.AppendLine("Job submitted (client UTC time): " + DateTime.UtcNow.ToString());

            // Write hello output tooa local file and toohello console. hello template 
            // for an error output file is:  JobDetails-{JobId}.txt
            string outputFile = OutputFilesFolder + @"\JobDetails-" + JobIdAsFileName(job.Id) + ".txt";
            WriteToFile(outputFile, builder.ToString());
            Console.Write(builder.ToString());
        }

        // Replace ":" with "_" in Job id values so they can 
        // be used as log file names.  
        private static string JobIdAsFileName(string jobID)
        {
            return jobID.Replace(":", "_");
        }

        // Write method output toohello output files folder.
        private static void WriteToFile(string outFilePath, string fileContent)
        {
            StreamWriter sr = File.CreateText(outFilePath);
            sr.WriteLine(fileContent);
            sr.Close();
        }

        private static IJob GetJob(CloudMediaContext context, string jobId)
        {
            // Use a Linq select query tooget an updated 
            // reference by Id. 
            var jobInstance =
                from j in context.Jobs
                where j.Id == jobId
                select j;

            // Return hello job reference as an Ijob. 
            IJob job = jobInstance.FirstOrDefault();

            return job;
        }

        private static IAsset GetAsset(CloudMediaContext context, string assetId)
        {
            // Use a LINQ Select query tooget an asset.
            var assetInstance =
                from a in context.Assets
                where a.Id == assetId
                select a;

            // Reference hello asset as an IAsset.
            IAsset asset = assetInstance.FirstOrDefault();

            return asset;
        }

        public static void DeleteAllAssets(CloudMediaContext context)
        {
            // Loop through and delete all assets.
            foreach (IAsset asset in context.Assets)
            {
                DeleteLocatorsForAsset(context, asset);

                asset.Delete();
            }
        }

        public static void DeleteLocatorsForAsset(CloudMediaContext context, IAsset asset)
        {
            string assetId = asset.Id;
            var locators = from a in context.Locators
                            where a.AssetId == assetId
                            select a;
            foreach (var locator in locators)
            {
                Console.WriteLine("Deleting locator {0} for asset {1}", locator.Path, assetId);

                locator.Delete();
            }
        }

        public static void DeleteAccessPolicy(CloudMediaContext context, string existingPolicyId)
        {
            // toodelete a specific access policy, get a reference toohello policy.  
            // based on hello policy Id passed toohello method.
            var policyInstance =
                    from p in context.AccessPolicies
                    where p.Id == existingPolicyId
                    select p;

            IAccessPolicy policy = policyInstance.FirstOrDefault();

            policy.Delete();

        }

        //////////////////////////////////////////////////////
        /// hello following methods use REST calls.
        //////////////////////////////////////////////////////

        public static string GetAcsBearerToken(string clientId, string clientSecret, string scope, string accessControlServiceUri)
        {
            if (string.IsNullOrEmpty(clientId))
                throw new ArgumentNullException("clientId");

            if (string.IsNullOrEmpty(clientSecret))
                throw new ArgumentNullException("clientSecret");

            if (string.IsNullOrEmpty(scope))
            {
                scope = "urn:WindowsAzureMediaServices";
            }
            else if (!scope.ToLower().StartsWith("urn:"))
            {
                scope = "urn:" + scope;
            }

            if (string.IsNullOrEmpty(accessControlServiceUri))
            {
                accessControlServiceUri = "https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13";
            }
            else if (!accessControlServiceUri.ToLower().EndsWith("/v2/oauth2-13"))
            {
                accessControlServiceUri = accessControlServiceUri.TrimEnd('/') + "/v2/OAuth2-13";
            }

            HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(accessControlServiceUri);
            request.Method = "POST";
            request.ContentType = "application/x-www-form-urlencoded";
            request.KeepAlive = true;
            string acsBearerToken = null;

            var requestBytes = Encoding.ASCII.GetBytes("grant_type=client_credentials&client_id=" +
                clientId + "&client_secret=" + HttpUtility.UrlEncode(clientSecret) +
                "&scope=" + HttpUtility.UrlEncode(scope));
            request.ContentLength = requestBytes.Length;

            var requestStream = request.GetRequestStream();
            requestStream.Write(requestBytes, 0, requestBytes.Length);
            requestStream.Close();

            var response = (HttpWebResponse)request.GetResponse();

            if (response.StatusCode == HttpStatusCode.OK)
            {
                using (Stream responseStream = response.GetResponseStream())
                {
                    using (StreamReader stream = new StreamReader(responseStream))
                    {
                        string responseString = stream.ReadToEnd();
                        var reader = JsonReaderWriterFactory.CreateJsonReader(Encoding.UTF8.GetBytes(responseString),
                            new XmlDictionaryReaderQuotas());

                        while (reader.Read())
                        {
                            if ((reader.Name == "access_token") && (reader.NodeType == XmlNodeType.Element))
                            {
                                if (reader.Read())
                                {
                                    acsBearerToken = reader.Value;
                                    break;
                                }
                            }
                        }
                    }
                }
            }

            return acsBearerToken;
        }

        public static XmlDocument CreateLocator(string mediaServicesApiServerUri,
                                                out string redirectedMediaServicesApiServerUri,
                                                string acsBearerToken, string assetId,
                                                string accessPolicyId, int locatorType,
                                                DateTime startTime, string locatorIdToReplicate = null,
                                                bool autoRedirect = true)
        {
            if (string.IsNullOrEmpty(mediaServicesApiServerUri))
            {
                mediaServicesApiServerUri = "https://media.windows.net/api/";
            }
            if (!mediaServicesApiServerUri.EndsWith("/"))
                mediaServicesApiServerUri = mediaServicesApiServerUri + "/";

            if (string.IsNullOrEmpty(acsBearerToken)) throw new ArgumentNullException("acsBearerToken");
            if (string.IsNullOrEmpty(assetId)) throw new ArgumentNullException("assetId");
            if (string.IsNullOrEmpty(accessPolicyId)) throw new ArgumentNullException("accessPolicyId");

            redirectedMediaServicesApiServerUri = null;
            XmlDocument xmlResponse = null;

            StringBuilder sb = new StringBuilder();
            sb.Append("{ \"AssetId\" : \"" + assetId + "\"");
            sb.Append(", \"AccessPolicyId\" : \"" + accessPolicyId + "\"");
            sb.Append(", \"Type\" : \"" + locatorType + "\"");
            if (startTime != DateTime.MinValue)
                sb.Append(", \"StartTime\" : \"" + startTime.ToString("G", CultureInfo.CreateSpecificCulture("en-us")) + "\"");
            if (!string.IsNullOrEmpty(locatorIdToReplicate))
                sb.Append(", \"Id\" : \"" + locatorIdToReplicate + "\"");
            sb.Append("}");

            string requestbody = sb.ToString();

            try
            {
                var request = GenerateRequest("POST", mediaServicesApiServerUri, "Locators",
                    null, acsBearerToken, requestbody);
                var response = (HttpWebResponse)request.GetResponse();

                switch (response.StatusCode)
                {
                    case HttpStatusCode.MovedPermanently:
                        //Recurse once with hello mediaServicesApiServerUri redirect Location:
                        if (autoRedirect)
                        {
                            redirectedMediaServicesApiServerUri = response.Headers["Location"];
                            string secondRedirection = null;
                            xmlResponse = CreateLocator(redirectedMediaServicesApiServerUri,
                                                        out secondRedirection, acsBearerToken,
                                                        assetId, accessPolicyId, locatorType,
                                                        startTime, locatorIdToReplicate, false);
                        }
                        else
                        {
                            Console.WriteLine("Redirection too{0} failed.",
                                mediaServicesApiServerUri);
                            return null;
                        }
                        break;
                    case HttpStatusCode.Created:
                        using (Stream responseStream = response.GetResponseStream())
                        {
                            using (StreamReader stream = new StreamReader(responseStream))
                            {
                                string responseString = stream.ReadToEnd();
                                var reader = JsonReaderWriterFactory.
                                    CreateJsonReader(Encoding.UTF8.GetBytes(responseString),
                                        new XmlDictionaryReaderQuotas());

                                xmlResponse = new XmlDocument();
                                reader.Read();
                                xmlResponse.LoadXml(reader.ReadInnerXml());
                            }
                        }
                        break;

                    default:
                        Console.WriteLine(response.StatusDescription);
                        break;
                }
            }
            catch (WebException ex)
            {
                Console.WriteLine(ex.Message);
            }

            return xmlResponse;
        }

        public static void CreateFileInfos(string mediaServicesApiServerUri,
                                    string acsBearerToken,
                                    string assetId
                                    )
        {
            if (String.IsNullOrEmpty(mediaServicesApiServerUri))
            {
                mediaServicesApiServerUri = "https://media.windows.net/api/";
            }
            if (!mediaServicesApiServerUri.EndsWith("/"))
                mediaServicesApiServerUri = mediaServicesApiServerUri + "/";

            if (String.IsNullOrEmpty(acsBearerToken)) throw new ArgumentNullException("acsBearerToken");
            if (String.IsNullOrEmpty(assetId)) throw new ArgumentNullException("assetId");


            string id = assetId.Replace(":", "%");

            UriBuilder builder = new UriBuilder(mediaServicesApiServerUri);
            builder.Path = Path.Combine(builder.Path, "CreateFileInfos");
            builder.Query = String.Format(CultureInfo.InvariantCulture, "assetid='{0}'", assetId);

            try
            {
                var request = GenerateRequest("GET", mediaServicesApiServerUri, "CreateFileInfos",
                    String.Format(CultureInfo.InvariantCulture, "assetid='{0}'", assetId), acsBearerToken, null);

                using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                {
                    if (response.StatusCode == HttpStatusCode.MovedPermanently)
                    {
                        string redirectedMediaServicesApiUrl = response.Headers["Location"];

                        CreateFileInfos(redirectedMediaServicesApiUrl, acsBearerToken, assetId);
                    }
                    else if ((response.StatusCode != HttpStatusCode.OK) &&
                        (response.StatusCode != HttpStatusCode.Accepted) &&
                        (response.StatusCode != HttpStatusCode.Created) &&
                        (response.StatusCode != HttpStatusCode.NoContent))
                    {
                        // TODO: Throw a more specific exception.
                        throw new Exception("Invalid response received ");
                    }
                }
            }
            catch (WebException ex)
            {
                Console.WriteLine(ex.Message);
            }
        }

        private static HttpWebRequest GenerateRequest(string verb,
                                                        string mediaServicesApiServerUri,
                                                        string resourcePath, string query,
                                                        string acsBearerToken, string requestbody)
        {
            var uriBuilder = new UriBuilder(mediaServicesApiServerUri);
            uriBuilder.Path += resourcePath;
            if (query != null)
            {
                uriBuilder.Query = query;
            }
            HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(uriBuilder.Uri);
            request.AllowAutoRedirect = false; //We manage our own redirects.
            request.Method = verb;

            if (resourcePath == "$metadata")
                request.MediaType = "application/xml";
            else
            {
                request.ContentType = "application/json;odata=verbose";
                request.Accept = "application/json;odata=verbose";
            }

            request.Headers.Add("DataServiceVersion", "3.0");
            request.Headers.Add("MaxDataServiceVersion", "3.0");
            request.Headers.Add("x-ms-version", "2.1");
            request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + acsBearerToken);

            if (requestbody != null)
            {
                var requestBytes = Encoding.ASCII.GetBytes(requestbody);
                request.ContentLength = requestBytes.Length;

                var requestStream = request.GetRequestStream();
                requestStream.Write(requestBytes, 0, requestBytes.Length);
                requestStream.Close();
            }
            else
            {
                request.ContentLength = 0;
            }
            return request;
        }

## <a name="next-steps"></a><span data-ttu-id="3a775-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3a775-163">Next steps</span></span>
<span data-ttu-id="3a775-164">Теперь использовать запросов tooroute диспетчера трафика, между двумя центрами обработки данных hello и таким образом отработки отказа в случае любой сбоев.</span><span class="sxs-lookup"><span data-stu-id="3a775-164">You can now use a traffic manager tooroute requests between hello two datacenters, and thus fail over in case of any outages.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="3a775-165">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3a775-165">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3a775-166">Отзывы</span><span class="sxs-lookup"><span data-stu-id="3a775-166">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

