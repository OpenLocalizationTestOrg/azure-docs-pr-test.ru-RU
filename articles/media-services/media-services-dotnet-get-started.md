---
title: "aaaGet работы с доставки содержимого по требованию с помощью .NET | Документы Microsoft"
description: "Этот учебник поможет выполнить шаги hello реализации приложения доставки содержимого по запросу с помощью служб мультимедиа Azure с помощью .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="44362-103">Приступая к работе с доставкой содержимого по запросу с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="44362-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="44362-104">Этот учебник поможет выполнить шаги hello реализации базовой службы доставки содержимого видео по запросу (VoD) с приложением служб мультимедиа Azure (AMS), с помощью hello Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="44362-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44362-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="44362-105">Prerequisites</span></span>

<span data-ttu-id="44362-106">Здесь представлены Hello необходимые toocomplete hello учебника:</span><span class="sxs-lookup"><span data-stu-id="44362-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="44362-107">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="44362-107">An Azure account.</span></span> <span data-ttu-id="44362-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44362-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="44362-109">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="44362-109">A Media Services account.</span></span> <span data-ttu-id="44362-110">toocreate учетную запись служб носителей в разделе [как учетную запись служб мультимедиа tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="44362-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="44362-111">.NET Framework 4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="44362-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="44362-112">приведенному.</span><span class="sxs-lookup"><span data-stu-id="44362-112">Visual Studio.</span></span>

<span data-ttu-id="44362-113">Этот учебник включает hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="44362-113">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="44362-114">Запустите (с помощью портала Azure hello) конечной точки потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="44362-114">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="44362-115">Создание и настройка проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44362-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="44362-116">Подключение toohello учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="44362-116">Connect toohello Media Services account.</span></span>
2. <span data-ttu-id="44362-117">Загрузка видеофайла.</span><span class="sxs-lookup"><span data-stu-id="44362-117">Upload a video file.</span></span>
3. <span data-ttu-id="44362-118">Кодирование hello исходный файл в набор файлов MP4 с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="44362-118">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="44362-119">Публикация активов hello и get потоковой передачи и URL-адресов прогрессивной загрузки.</span><span class="sxs-lookup"><span data-stu-id="44362-119">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="44362-120">Воспроизведение содержимого.</span><span class="sxs-lookup"><span data-stu-id="44362-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="44362-121">Обзор</span><span class="sxs-lookup"><span data-stu-id="44362-121">Overview</span></span>
<span data-ttu-id="44362-122">Этот учебник поможет выполнить шаги hello реализации приложения доставки содержимого видео по запросу (VoD), с помощью служб мультимедиа Azure (AMS) пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="44362-122">This tutorial walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="44362-123">Hello учебнике рассказывается hello базовый рабочий процесс служб мультимедиа и hello распространенных объектов и задач, необходимых для разработки служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="44362-123">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="44362-124">По завершении hello учебника hello будет toostream может быть или постепенно загрузить образец файла мультимедиа, отправки, закодированные и загружены.</span><span class="sxs-lookup"><span data-stu-id="44362-124">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="44362-125">Модель AMS</span><span class="sxs-lookup"><span data-stu-id="44362-125">AMS model</span></span>

<span data-ttu-id="44362-126">Hello рисунке показаны некоторые из наиболее часто используемых hello объектов при разработке приложений VoD к модели hello OData служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="44362-126">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="44362-127">Щелкните tooview изображение hello его полный размер.</span><span class="sxs-lookup"><span data-stu-id="44362-127">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="44362-128">Можно просмотреть всю модель hello [здесь](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="44362-128">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="44362-129">Запустить с помощью портала Azure hello конечные точки потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="44362-129">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="44362-130">При работе со службами мультимедиа Azure одним из наиболее распространенных сценариев hello разрабатывает видео через потоковой передачи с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="44362-130">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="44362-131">Служба Media Services предоставляет динамической упаковки, что позволяет вам toodeliver с адаптивным битрейтом MP4 кодируются содержимого в форматах, поддерживаемых служб мультимедиа (MPEG DASH, HLS, Smooth Streaming) just-in-time, без необходимости toostore упакована заранее потоковой передачи версии каждого из этих форматов потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="44362-131">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="44362-132">При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="44362-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="44362-133">Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="44362-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="44362-134">toostart Здравствуйте конечной точки потоковой передачи, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="44362-134">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="44362-135">Войдите на hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="44362-135">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="44362-136">В окне "Параметры" hello щелкните конечных точек потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="44362-136">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="44362-137">Щелкните конечную точку потоковой передачи по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="44362-137">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="44362-138">Появится окно Hello по умолчанию потоковая передача сведений о конечной ТОЧКЕ.</span><span class="sxs-lookup"><span data-stu-id="44362-138">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="44362-139">Щелкните значок запуска hello.</span><span class="sxs-lookup"><span data-stu-id="44362-139">Click hello Start icon.</span></span>
5. <span data-ttu-id="44362-140">Щелкните toosave кнопку hello сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="44362-140">Click hello Save button toosave your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="44362-141">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="44362-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="44362-142">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="44362-142">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="44362-143">Создайте новую папку (папку может быть в любом месте на локальном диске) и скопируйте MP4-файл, должны быть tooencode и потоком, или последовательная загрузка.</span><span class="sxs-lookup"><span data-stu-id="44362-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="44362-144">В этом примере используется путь «C:\VideoFiles» hello.</span><span class="sxs-lookup"><span data-stu-id="44362-144">In this example, hello "C:\VideoFiles" path is used.</span></span>

## <a name="connect-toohello-media-services-account"></a><span data-ttu-id="44362-145">Учетная запись служб мультимедиа toohello подключения</span><span class="sxs-lookup"><span data-stu-id="44362-145">Connect toohello Media Services account</span></span>

<span data-ttu-id="44362-146">При использовании служб мультимедиа с помощью .NET, необходимо использовать hello **CloudMediaContext** класс для большинства задач программирования служб Media Services: учетной записи службы tooMedia подключения; создание, обновление, доступ к и удаление следующих hello объекты: активы, файлы активов, заданий, политики доступа, указателей, и т. д.</span><span class="sxs-lookup"><span data-stu-id="44362-146">When using Media Services with .NET, you must use hello **CloudMediaContext** class for most Media Services programming tasks: connecting tooMedia Services account; creating, updating, accessing, and deleting hello following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="44362-147">Замените класс программы по умолчанию hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="44362-147">Overwrite hello default Program class with hello following code.</span></span> <span data-ttu-id="44362-148">Hello кода показано, как значения tooread hello соединений из файла App.config hello и как toocreate hello **CloudMediaContext** объект в порядке tooconnect tooMedia служб.</span><span class="sxs-lookup"><span data-stu-id="44362-148">hello code demonstrates how tooread hello connection values from hello App.config file and how toocreate hello **CloudMediaContext** object in order tooconnect tooMedia Services.</span></span> <span data-ttu-id="44362-149">Дополнительные сведения см. в разделе [подключение toohello API служб мультимедиа](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="44362-149">For more information, see [connecting toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="44362-150">Убедитесь, что tooupdate hello файла имя и путь toowhere вами файл.</span><span class="sxs-lookup"><span data-stu-id="44362-150">Make sure tooupdate hello file name and path toowhere you have your media file.</span></span>

<span data-ttu-id="44362-151">Hello **Main** функция вызывает методы, которые будут определены далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="44362-151">hello **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="44362-152">Будет использоваться для получения ошибки компиляции пока не будут добавлены определения всех функций hello.</span><span class="sxs-lookup"><span data-stu-id="44362-152">You will be getting compilation errors until you add definitions for all hello functions.</span></span>

    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="44362-153">Создание нового актива и отправка видеофайла</span><span class="sxs-lookup"><span data-stu-id="44362-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="44362-154">В службах мультимедиа цифровые файлы отправляются (или принимаются) в актив.</span><span class="sxs-lookup"><span data-stu-id="44362-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="44362-155">Hello **активов** может содержать сущности, видео, аудио, изображения, коллекции эскизов, текст записи на диске и титров файлов (и hello метаданные об этих файлах.)  После загрузки файлов hello контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="44362-155">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> <span data-ttu-id="44362-156">Hello в ресурсе hello, называются **файлов активов**.</span><span class="sxs-lookup"><span data-stu-id="44362-156">hello files in hello asset are called **Asset Files**.</span></span>

<span data-ttu-id="44362-157">Hello **UploadFile** ниже вызывает определенный метод **CreateFromFile** (определенная в расширения SDK .NET).</span><span class="sxs-lookup"><span data-stu-id="44362-157">hello **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="44362-158">**CreateFromFile** создает новый актив, в которой hello загружается указанный исходный файл.</span><span class="sxs-lookup"><span data-stu-id="44362-158">**CreateFromFile** creates a new asset into which hello specified source file is uploaded.</span></span>

<span data-ttu-id="44362-159">Hello **CreateFromFile** принимает **AssetCreationOptions** которого вы можете задать один из следующих вариантов создания активов hello:</span><span class="sxs-lookup"><span data-stu-id="44362-159">hello **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of hello following asset creation options:</span></span>

* <span data-ttu-id="44362-160">**None** — шифрование не используется.</span><span class="sxs-lookup"><span data-stu-id="44362-160">**None** - No encryption is used.</span></span> <span data-ttu-id="44362-161">Это значение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="44362-161">This is hello default value.</span></span> <span data-ttu-id="44362-162">Обратите внимание, что при использовании этого параметра содержимое не защищено при передаче и хранении.</span><span class="sxs-lookup"><span data-stu-id="44362-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="44362-163">Если планируется toodeliver MP4-файл с помощью прогрессивной загрузки, используйте этот параметр.</span><span class="sxs-lookup"><span data-stu-id="44362-163">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="44362-164">**StorageEncrypted** -используйте этот параметр tooencrypt незащищенного содержимого локально с помощью Advanced Encryption Standard (AES)-256-разрядного шифрования, который затем передает его tooAzure хранилища, где она хранится в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="44362-164">**StorageEncrypted** - Use this option tooencrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="44362-165">Активы, защищенные с помощью шифрования хранилища, автоматически дешифруются и помещаются в предыдущих tooencoding зашифрованный файл системы и при необходимости повторно зашифрован предыдущих toouploading возвращены в виде нового выходного актива.</span><span class="sxs-lookup"><span data-stu-id="44362-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="44362-166">Hello основным случаем использования шифрования хранилища при необходимости toosecure файлов входном файле мультимедиа высокого качества с помощью криптостойкого шифрования на диске.</span><span class="sxs-lookup"><span data-stu-id="44362-166">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="44362-167">**CommonEncryptionProtected**. Используйте этот параметр при отправке содержимого, которое уже зашифровано и защищено с помощью стандартного шифрования или PlayReady DRM (например, Smooth Streaming с защитой PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="44362-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="44362-168">**EnvelopeEncryptionProtected**. Используйте этот параметр при отправке HLS с шифрованием AES.</span><span class="sxs-lookup"><span data-stu-id="44362-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="44362-169">Обратите внимание, что hello файлы необходимо были закодированы и зашифрованы диспетчером преобразования.</span><span class="sxs-lookup"><span data-stu-id="44362-169">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="44362-170">Hello **CreateFromFile** метод также позволяет указать обратный вызов выполняется отправка заказа tooreport hello hello файла.</span><span class="sxs-lookup"><span data-stu-id="44362-170">hello **CreateFromFile** method also lets you specify a callback in order tooreport hello upload progress of hello file.</span></span>

<span data-ttu-id="44362-171">В следующем примере hello, мы указываем **нет** варианты активов hello.</span><span class="sxs-lookup"><span data-stu-id="44362-171">In hello following example, we specify **None** for hello asset options.</span></span>

<span data-ttu-id="44362-172">Добавьте следующий класс Program toohello метод hello.</span><span class="sxs-lookup"><span data-stu-id="44362-172">Add hello following method toohello Program class.</span></span>

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


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="44362-173">Кодирование hello исходный файл в набор файлов MP4 с адаптивной скоростью</span><span class="sxs-lookup"><span data-stu-id="44362-173">Encode hello source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="44362-174">После передачи ресурсов в службы мультимедиа, носитель может быть закодированы в transmuxed, водяные знаки и т. д., прежде чем оно будет доставлено tooclients.</span><span class="sxs-lookup"><span data-stu-id="44362-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="44362-175">Эти операции планируются и выполняются несколько фона роль экземпляров tooensure высокой производительности и доступности.</span><span class="sxs-lookup"><span data-stu-id="44362-175">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="44362-176">Эти действия называются заданиями, и каждое задание состоит из атомарных задач, которые hello фактические трудозатраты на файл актива hello.</span><span class="sxs-lookup"><span data-stu-id="44362-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do hello actual work on hello Asset file.</span></span>

<span data-ttu-id="44362-177">Как упоминалось ранее, при работе со службами мультимедиа Azure, одним из наиболее распространенных сценариев hello разрабатывает клиентов tooyour потоковой передачи с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="44362-177">As was mentioned earlier, when working with Azure Media Services, one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="44362-178">Службы мультимедиа можно динамически упаковать набор файлов MP4 с адаптивной скоростью в один из следующих форматов hello: HTTP Live Streaming (HLS), Smooth Streaming и MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="44362-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="44362-179">tootake преимущества динамической упаковки необходимо tooencode или перекодирования мезонинный (источник) в набор файлов MP4 с адаптивным битрейтом или файлов Smooth Streaming с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="44362-179">tootake advantage of dynamic packaging, you need tooencode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="44362-180">Hello, следующий код показывает, как задание toosubmit кодировку.</span><span class="sxs-lookup"><span data-stu-id="44362-180">hello following code shows how toosubmit an encoding job.</span></span> <span data-ttu-id="44362-181">Hello задание содержит одну задачу, которая указывает tootranscode hello мезонинный файл в набор MP4-файлов с адаптивной скоростью, с помощью **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="44362-181">hello job contains one task that specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="44362-182">Код Hello отправляет задание hello и ожидает до его завершения.</span><span class="sxs-lookup"><span data-stu-id="44362-182">hello code submits hello job and waits until it is completed.</span></span>

<span data-ttu-id="44362-183">После завершения задания hello бы быть актива может toostream или прогрессивное скачивание MP4-файлов, которые были созданы в результате перекодировки.</span><span class="sxs-lookup"><span data-stu-id="44362-183">Once hello job is completed, you would be able toostream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="44362-184">Добавьте следующий класс Program toohello метод hello.</span><span class="sxs-lookup"><span data-stu-id="44362-184">Add hello following method toohello Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="44362-185">Публиковать hello активов, а URL-адресов для потоковой передачи и прогрессивной загрузки</span><span class="sxs-lookup"><span data-stu-id="44362-185">Publish hello asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="44362-186">toostream или загрузки актив, сначала требуется слишком «публикацией» путем создания локатора.</span><span class="sxs-lookup"><span data-stu-id="44362-186">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="44362-187">Локаторы предоставляют доступ toofiles, содержащиеся в ресурсе hello.</span><span class="sxs-lookup"><span data-stu-id="44362-187">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="44362-188">Службы мультимедиа поддерживают два типа локаторов: OnDemandOrigin указатели, используемые toostream мультимедиа (например, MPEG DASH, HLS или Smooth Streaming) и указатели подписи доступа (SAS), используемые файлы мультимедиа toodownload (Подробнее о SAS см. указатели [это](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) блога).</span><span class="sxs-lookup"><span data-stu-id="44362-188">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="44362-189">Некоторые сведения о форматах URL-адреса</span><span class="sxs-lookup"><span data-stu-id="44362-189">Some details about URL formats</span></span>

<span data-ttu-id="44362-190">После создания hello указателей, можно построить hello URL-адреса, которые бы быть используется toostream или загружать файлы.</span><span class="sxs-lookup"><span data-stu-id="44362-190">After you create hello locators, you can build hello URLs that would be used toostream or download your files.</span></span> <span data-ttu-id="44362-191">Образец Hello в этом учебнике будет выдавать URL-адреса, которые можно вставить в соответствующий браузерах.</span><span class="sxs-lookup"><span data-stu-id="44362-191">hello sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="44362-192">В этом разделе представлены краткие примеры разных форматов.</span><span class="sxs-lookup"><span data-stu-id="44362-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a><span data-ttu-id="44362-193">URL-адрес потоковой передачи для MPEG DASH имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="44362-193">A streaming URL for MPEG DASH has hello following format:</span></span>

<span data-ttu-id="44362-194">{имя_конечной_точки_потоковой_передачи-имя_учетной_записи_служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор_указателя}/{имя_файла}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="44362-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a><span data-ttu-id="44362-195">URL-адрес потоковой передачи для HLS имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="44362-195">A streaming URL for HLS has hello following format:</span></span>

<span data-ttu-id="44362-196">{имя_конечной_точки_потоковой_передачи-имя_учетной_записи_служб_мультимедиа}.streaming.mediaservices.windows.net/{идентификатор_указателя}/{имя_файла}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="44362-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a><span data-ttu-id="44362-197">URL-адрес потоковой передачи для Smooth Streaming имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="44362-197">A streaming URL for Smooth Streaming has hello following format:</span></span>

<span data-ttu-id="44362-198">{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="44362-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a><span data-ttu-id="44362-199">URL-адрес SAS используется toodownload файлов имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="44362-199">A SAS URL used toodownload files has hello following format:</span></span>

<span data-ttu-id="44362-200">{имя_контейнера_больших_двоичных_объектов}/{имя_ресурса-контейнера}/{имя_файла}/{подпись_SAS}</span><span class="sxs-lookup"><span data-stu-id="44362-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="44362-201">Расширения пакета SDK .NET служб мультимедиа предоставляет удобные вспомогательные методы, возвращаемое в формате URL-адреса для hello опубликованный актив.</span><span class="sxs-lookup"><span data-stu-id="44362-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for hello published asset.</span></span>

<span data-ttu-id="44362-202">Hello следующий код использует указатели toocreate расширения SDK .NET и потоковой передачи tooget и последовательной загрузки URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="44362-202">hello following code uses .NET SDK Extensions toocreate locators and tooget streaming and progressive download URLs.</span></span> <span data-ttu-id="44362-203">Привет код также показывает, как toodownload файлы tooa локальную папку.</span><span class="sxs-lookup"><span data-stu-id="44362-203">hello code also shows how toodownload files tooa local folder.</span></span>

<span data-ttu-id="44362-204">Добавьте следующий класс Program toohello метод hello.</span><span class="sxs-lookup"><span data-stu-id="44362-204">Add hello following method toohello Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="44362-205">Проверка посредством воспроизведения содержимого</span><span class="sxs-lookup"><span data-stu-id="44362-205">Test by playing your content</span></span>

<span data-ttu-id="44362-206">После запуска программы hello, определенный в предыдущем разделе hello hello URL-адреса, примерно следующее toohello будет отображаться в окне консоли hello.</span><span class="sxs-lookup"><span data-stu-id="44362-206">Once you run hello program defined in hello previous section, hello URLs similar toohello following will be displayed in hello console window.</span></span>

<span data-ttu-id="44362-207">URL-адреса адаптивной потоковой передачи:</span><span class="sxs-lookup"><span data-stu-id="44362-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="44362-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="44362-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="44362-209">HLS</span><span class="sxs-lookup"><span data-stu-id="44362-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="44362-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="44362-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="44362-211">URL-адреса поэтапного скачивания (аудио и видео).</span><span class="sxs-lookup"><span data-stu-id="44362-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="44362-212">toostream видео, вставьте URL-адрес в текстовое поле URL-адрес hello в hello [проигрыватель служб мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="44362-212">toostream your video, paste your URL in hello URL textbox in hello [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="44362-213">tootest прогрессивной загрузки, вставьте URL-адрес в адресную строку браузера (например, Internet Explorer, Chrome или Safari).</span><span class="sxs-lookup"><span data-stu-id="44362-213">tootest progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="44362-214">Дополнительные сведения см. в разделе hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="44362-214">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="44362-215">Воспроизведение содержимого с помощью существующих проигрывателей</span><span class="sxs-lookup"><span data-stu-id="44362-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="44362-216">Разработка приложений видеопроигрывателя</span><span class="sxs-lookup"><span data-stu-id="44362-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="44362-217">Встраивание адаптивного потокового видео MPEG-DASH в приложение HTML5 с помощью DASH.js</span><span class="sxs-lookup"><span data-stu-id="44362-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="44362-218">Скачивание образца</span><span class="sxs-lookup"><span data-stu-id="44362-218">Download sample</span></span>
<span data-ttu-id="44362-219">Hello следующий образец кода содержит hello код, созданный в этом учебнике: [пример](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="44362-219">hello following code sample contains hello code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="44362-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44362-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="44362-221">Отзывы</span><span class="sxs-lookup"><span data-stu-id="44362-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
