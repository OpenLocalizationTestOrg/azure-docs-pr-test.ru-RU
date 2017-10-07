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
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a>Приступая к работе с доставкой содержимого по запросу с помощью пакета SDK для .NET
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Этот учебник поможет выполнить шаги hello реализации базовой службы доставки содержимого видео по запросу (VoD) с приложением служб мультимедиа Azure (AMS), с помощью hello Azure Media Services .NET SDK.

## <a name="prerequisites"></a>Предварительные требования

Здесь представлены Hello необходимые toocomplete hello учебника:

* Учетная запись Azure. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).
* Учетная запись служб мультимедиа. toocreate учетную запись служб носителей в разделе [как учетную запись служб мультимедиа tooCreate](media-services-portal-create-account.md).
* .NET Framework 4.0 или более поздней версии.
* приведенному.

Этот учебник включает hello следующие задачи:

1. Запустите (с помощью портала Azure hello) конечной точки потоковой передачи.
2. Создание и настройка проекта Visual Studio.
3. Подключение toohello учетная запись служб мультимедиа.
2. Загрузка видеофайла.
3. Кодирование hello исходный файл в набор файлов MP4 с адаптивной скоростью.
4. Публикация активов hello и get потоковой передачи и URL-адресов прогрессивной загрузки.  
5. Воспроизведение содержимого.

## <a name="overview"></a>Обзор
Этот учебник поможет выполнить шаги hello реализации приложения доставки содержимого видео по запросу (VoD), с помощью служб мультимедиа Azure (AMS) пакета SDK для .NET.

Hello учебнике рассказывается hello базовый рабочий процесс служб мультимедиа и hello распространенных объектов и задач, необходимых для разработки служб мультимедиа. По завершении hello учебника hello будет toostream может быть или постепенно загрузить образец файла мультимедиа, отправки, закодированные и загружены.

### <a name="ams-model"></a>Модель AMS

Hello рисунке показаны некоторые из наиболее часто используемых hello объектов при разработке приложений VoD к модели hello OData служб мультимедиа.

Щелкните tooview изображение hello его полный размер.  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

Можно просмотреть всю модель hello [здесь](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Запустить с помощью портала Azure hello конечные точки потоковой передачи

При работе со службами мультимедиа Azure одним из наиболее распространенных сценариев hello разрабатывает видео через потоковой передачи с адаптивной скоростью. Служба Media Services предоставляет динамической упаковки, что позволяет вам toodeliver с адаптивным битрейтом MP4 кодируются содержимого в форматах, поддерживаемых служб мультимедиа (MPEG DASH, HLS, Smooth Streaming) just-in-time, без необходимости toostore упакована заранее потоковой передачи версии каждого из этих форматов потоковой передачи.

>[!NOTE]
>При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния.

toostart Здравствуйте конечной точки потоковой передачи, hello следующие:

1. Войдите на hello [портал Azure](https://portal.azure.com/).
2. В окне "Параметры" hello щелкните конечных точек потоковой передачи.
3. Щелкните конечную точку потоковой передачи по умолчанию hello.

    Появится окно Hello по умолчанию потоковая передача сведений о конечной ТОЧКЕ.

4. Щелкните значок запуска hello.
5. Щелкните toosave кнопку hello сохранить изменения.

## <a name="create-and-configure-a-visual-studio-project"></a>Создание и настройка проекта Visual Studio

1. Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md). 
2. Создайте новую папку (папку может быть в любом месте на локальном диске) и скопируйте MP4-файл, должны быть tooencode и потоком, или последовательная загрузка. В этом примере используется путь «C:\VideoFiles» hello.

## <a name="connect-toohello-media-services-account"></a>Учетная запись служб мультимедиа toohello подключения

При использовании служб мультимедиа с помощью .NET, необходимо использовать hello **CloudMediaContext** класс для большинства задач программирования служб Media Services: учетной записи службы tooMedia подключения; создание, обновление, доступ к и удаление следующих hello объекты: активы, файлы активов, заданий, политики доступа, указателей, и т. д.

Замените класс программы по умолчанию hello hello, следующий код. Hello кода показано, как значения tooread hello соединений из файла App.config hello и как toocreate hello **CloudMediaContext** объект в порядке tooconnect tooMedia служб. Дополнительные сведения см. в разделе [подключение toohello API служб мультимедиа](media-services-use-aad-auth-to-access-ams-api.md).

Убедитесь, что tooupdate hello файла имя и путь toowhere вами файл.

Hello **Main** функция вызывает методы, которые будут определены далее в этом разделе.

> [!NOTE]
> Будет использоваться для получения ошибки компиляции пока не будут добавлены определения всех функций hello.

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

## <a name="create-a-new-asset-and-upload-a-video-file"></a>Создание нового актива и отправка видеофайла

В службах мультимедиа цифровые файлы отправляются (или принимаются) в актив. Hello **активов** может содержать сущности, видео, аудио, изображения, коллекции эскизов, текст записи на диске и титров файлов (и hello метаданные об этих файлах.)  После загрузки файлов hello контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи. Hello в ресурсе hello, называются **файлов активов**.

Hello **UploadFile** ниже вызывает определенный метод **CreateFromFile** (определенная в расширения SDK .NET). **CreateFromFile** создает новый актив, в которой hello загружается указанный исходный файл.

Hello **CreateFromFile** принимает **AssetCreationOptions** которого вы можете задать один из следующих вариантов создания активов hello:

* **None** — шифрование не используется. Это значение по умолчанию hello. Обратите внимание, что при использовании этого параметра содержимое не защищено при передаче и хранении.
  Если планируется toodeliver MP4-файл с помощью прогрессивной загрузки, используйте этот параметр.
* **StorageEncrypted** -используйте этот параметр tooencrypt незащищенного содержимого локально с помощью Advanced Encryption Standard (AES)-256-разрядного шифрования, который затем передает его tooAzure хранилища, где она хранится в зашифрованном виде. Активы, защищенные с помощью шифрования хранилища, автоматически дешифруются и помещаются в предыдущих tooencoding зашифрованный файл системы и при необходимости повторно зашифрован предыдущих toouploading возвращены в виде нового выходного актива. Hello основным случаем использования шифрования хранилища при необходимости toosecure файлов входном файле мультимедиа высокого качества с помощью криптостойкого шифрования на диске.
* **CommonEncryptionProtected**. Используйте этот параметр при отправке содержимого, которое уже зашифровано и защищено с помощью стандартного шифрования или PlayReady DRM (например, Smooth Streaming с защитой PlayReady DRM).
* **EnvelopeEncryptionProtected**. Используйте этот параметр при отправке HLS с шифрованием AES. Обратите внимание, что hello файлы необходимо были закодированы и зашифрованы диспетчером преобразования.

Hello **CreateFromFile** метод также позволяет указать обратный вызов выполняется отправка заказа tooreport hello hello файла.

В следующем примере hello, мы указываем **нет** варианты активов hello.

Добавьте следующий класс Program toohello метод hello.

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


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a>Кодирование hello исходный файл в набор файлов MP4 с адаптивной скоростью
После передачи ресурсов в службы мультимедиа, носитель может быть закодированы в transmuxed, водяные знаки и т. д., прежде чем оно будет доставлено tooclients. Эти операции планируются и выполняются несколько фона роль экземпляров tooensure высокой производительности и доступности. Эти действия называются заданиями, и каждое задание состоит из атомарных задач, которые hello фактические трудозатраты на файл актива hello.

Как упоминалось ранее, при работе со службами мультимедиа Azure, одним из наиболее распространенных сценариев hello разрабатывает клиентов tooyour потоковой передачи с адаптивной скоростью. Службы мультимедиа можно динамически упаковать набор файлов MP4 с адаптивной скоростью в один из следующих форматов hello: HTTP Live Streaming (HLS), Smooth Streaming и MPEG DASH.

tootake преимущества динамической упаковки необходимо tooencode или перекодирования мезонинный (источник) в набор файлов MP4 с адаптивным битрейтом или файлов Smooth Streaming с адаптивной скоростью.  

Hello, следующий код показывает, как задание toosubmit кодировку. Hello задание содержит одну задачу, которая указывает tootranscode hello мезонинный файл в набор MP4-файлов с адаптивной скоростью, с помощью **Media Encoder Standard**. Код Hello отправляет задание hello и ожидает до его завершения.

После завершения задания hello бы быть актива может toostream или прогрессивное скачивание MP4-файлов, которые были созданы в результате перекодировки.

Добавьте следующий класс Program toohello метод hello.

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

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a>Публиковать hello активов, а URL-адресов для потоковой передачи и прогрессивной загрузки

toostream или загрузки актив, сначала требуется слишком «публикацией» путем создания локатора. Локаторы предоставляют доступ toofiles, содержащиеся в ресурсе hello. Службы мультимедиа поддерживают два типа локаторов: OnDemandOrigin указатели, используемые toostream мультимедиа (например, MPEG DASH, HLS или Smooth Streaming) и указатели подписи доступа (SAS), используемые файлы мультимедиа toodownload (Подробнее о SAS см. указатели [это](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) блога).

### <a name="some-details-about-url-formats"></a>Некоторые сведения о форматах URL-адреса

После создания hello указателей, можно построить hello URL-адреса, которые бы быть используется toostream или загружать файлы. Образец Hello в этом учебнике будет выдавать URL-адреса, которые можно вставить в соответствующий браузерах. В этом разделе представлены краткие примеры разных форматов.

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a>URL-адрес потоковой передачи для MPEG DASH имеет hello следующий формат:

{имя_конечной_точки_потоковой_передачи-имя_учетной_записи_служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор_указателя}/{имя_файла}.ism/Manifest**(format=mpd-time-csf)**

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a>URL-адрес потоковой передачи для HLS имеет hello следующий формат:

{имя_конечной_точки_потоковой_передачи-имя_учетной_записи_служб_мультимедиа}.streaming.mediaservices.windows.net/{идентификатор_указателя}/{имя_файла}.ism/Manifest**(format=m3u8-aapl)**

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a>URL-адрес потоковой передачи для Smooth Streaming имеет hello следующий формат:

{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a>URL-адрес SAS используется toodownload файлов имеет hello следующий формат:

{имя_контейнера_больших_двоичных_объектов}/{имя_ресурса-контейнера}/{имя_файла}/{подпись_SAS}

Расширения пакета SDK .NET служб мультимедиа предоставляет удобные вспомогательные методы, возвращаемое в формате URL-адреса для hello опубликованный актив.

Hello следующий код использует указатели toocreate расширения SDK .NET и потоковой передачи tooget и последовательной загрузки URL-адреса. Привет код также показывает, как toodownload файлы tooa локальную папку.

Добавьте следующий класс Program toohello метод hello.

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

## <a name="test-by-playing-your-content"></a>Проверка посредством воспроизведения содержимого

После запуска программы hello, определенный в предыдущем разделе hello hello URL-адреса, примерно следующее toohello будет отображаться в окне консоли hello.

URL-адреса адаптивной потоковой передачи:

Smooth Streaming

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

HLS

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

MPEG DASH

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

URL-адреса поэтапного скачивания (аудио и видео).

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


toostream видео, вставьте URL-адрес в текстовое поле URL-адрес hello в hello [проигрыватель служб мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest прогрессивной загрузки, вставьте URL-адрес в адресную строку браузера (например, Internet Explorer, Chrome или Safari).

Дополнительные сведения см. в разделе hello следующие вопросы:

- [Воспроизведение содержимого с помощью существующих проигрывателей](media-services-playback-content-with-existing-players.md)
- [Разработка приложений видеопроигрывателя](media-services-develop-video-players.md)
- [Встраивание адаптивного потокового видео MPEG-DASH в приложение HTML5 с помощью DASH.js](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a>Скачивание образца
Hello следующий образец кода содержит hello код, созданный в этом учебнике: [пример](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
