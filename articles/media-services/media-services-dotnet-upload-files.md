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
# <a name="upload-files-into-a-media-services-account-using-net"></a>Передача файлов в учетную запись служб мультимедиа с помощью .NET
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Портал](media-services-portal-upload-files.md)
> 
> 

В службах мультимедиа цифровые файлы отправляются (или принимаются) в актив. Hello **активов** может содержать сущности, видео, аудио, изображения, коллекции эскизов, текст отслеживает и титров файлов (и hello метаданные об этих файлах.)  После загрузки файлов hello контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.

Hello в ресурсе hello, называются **файлов активов**. Hello **AssetFile** экземпляра и hello фактический файл мультимедиа являются двумя отдельными объектами. экземпляр AssetFile Hello содержит метаданные о файле мультимедиа hello, а файл мультимедиа hello hello фактический контент мультимедиа.

> [!NOTE]
> применить Hello следующие вопросы:
> 
> * Службы мультимедиа используют значение hello hello свойство IAssetFile.Name при построении URL-адреса для hello, потоковая передача содержимого (например, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) По этой причине кодирование с помощью знака процента не допускается. Здравствуйте, значение hello **имя** свойство не может иметь любой из следующих hello [процентов зарезервированные символы](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? % # []». Кроме того, может существовать только один "." для расширения имени файла hello.
> * Длина Hello hello имени не должна быть более 260 знаков.
> * Имеется ограничение toohello максимальный размер файла поддерживается для обработки в службах мультимедиа. См. в разделе [это](media-services-quotas-and-limitations.md) сведения о hello ограничения размера файла.
> * Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy). Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики). Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.
> 

При создании активов можно указать следующие параметры шифрования hello. 

* **None** — шифрование не используется. Это значение по умолчанию hello. Обратите внимание, что при использовании этого параметра содержимое не защищено при передаче или в хранилище.
  Если планируется toodeliver MP4-файл с помощью прогрессивной загрузки, используйте этот параметр. 
* **CommonEncryption** — используйте этот параметр при отправке содержимого, которое уже зашифровано и защищено с помощью стандартного шифрования или PlayReady DRM (например, Smooth Streaming с защитой PlayReady DRM).
* **EnvelopeEncrypted** — используйте этот параметр при отправке HLS с шифрованием AES. Обратите внимание, что hello файлы необходимо были закодированы и зашифрованы диспетчером преобразования.
* **StorageEncrypted** — шифрование незащищенного содержимого локально с помощью AES-256-разрядного шифрования, а затем передает его tooAzure хранилища, где она хранится в зашифрованном виде. Активы, защищенные с помощью шифрования хранилища, автоматически дешифруются и помещаются в предыдущих tooencoding зашифрованный файл системы и при необходимости повторно зашифрован предыдущих toouploading возвращены в виде нового выходного актива. Hello основным случаем использования шифрования хранилища удобно, если нужно toosecure rest вашей высококачественных входных файлов мультимедиа с помощью строгого шифрования на диске.
  
    Службы мультимедиа обеспечивают шифрование ресурсов на диске в хранилище, а не по сети, как технология управления цифровыми правами (DRM).
  
    Если ресурс зашифрован в хранилище, необходимо настроить политику доставки ресурсов. Дополнительные сведения см. в статье [Настройка политик доставки ресурсов-контейнеров](media-services-dotnet-configure-asset-delivery-policy.md).

При указании для вашего toobe активов зашифрованы с **CommonEncrypted** параметр, или **EnvelopeEncypted** параметр, необходимо будет tooassociate актива с **ContentKey**. Дополнительные сведения см. в разделе [как toocreate ContentKey](media-services-dotnet-create-contentkey.md). 

При указании для вашего toobe активов зашифрованы с **StorageEncrypted** , то hello пакета SDK служб мультимедиа для .NET создаст **StorateEncrypted** **ContentKey** для вашей активов.

В этом разделе показано, как toouse Media Services .NET SDK, а также файлы tooupload Media Services .NET SDK расширения в актив служб мультимедиа.

## <a name="upload-a-single-file-with-media-services-net-sdk"></a>Передача одного файла с помощью пакета SDK служб мультимедиа для .NET
Hello в образце кода ниже использует .NET SDK tooupload один файл. создании и удалении функцией передачи hello Hello AccessPolicy и указателя. 


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


## <a name="upload-multiple-files-with-media-services-net-sdk"></a>Передача нескольких файлов с помощью пакета SDK служб мультимедиа для .NET
Здравствуйте, как следующий код показывает toocreate актива и отправка нескольких файлов.

Hello кода hello следующие:

* Создает пустой актив с помощью метода CreateEmptyAsset hello, определенный в предыдущем шаге hello.
* Создает **AccessPolicy** экземпляр, который определяет hello разрешения и длительность доступа toohello активов.
* Создает **локатора** экземпляр, который предоставляет доступ toohello активов.
* Создает экземпляр **BlobTransferClient** . Этот тип представляет клиент, работающий на приветствия больших двоичных объектов Azure. В этом примере мы используем прогресса отправки hello toomonitor клиента hello. 
* Перечисляет файлы в указанном каталоге hello и создает **AssetFile** экземпляра для каждого файла.
* Передачи файлов hello в службы мультимедиа с помощью hello **UploadAsync** метод. 

> [!NOTE]
> Используйте tooensure метод UploadAsync hello, hello вызовы не блокируются и hello файлы отправляются параллельно.
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



При передаче большего количества активов, рассмотрим следующие hello.

* Создайте новый объект **CloudMediaContext** в каждом потоке. Hello **CloudMediaContext** класс не является потокобезопасным.
* Увеличьте NumberOfConcurrentTransfers со значения по умолчанию hello 2 tooa высокого значения, например 5. Задание этого свойства влияет на все экземпляры **CloudMediaContext**. 
* Сохраните ParallelTransferThreadCount на значение по умолчанию hello 10.

## <a id="ingest_in_bulk"></a>Массовый прием ресурсов с помощью пакета SDK служб мультимедиа для .NET
Передача больших файлов ресурсов может оказаться узким местом при создании ресурса. Массовое получение активов массового или «Массовой передаче», связана с разделением создания ресурсов от процесса отправки hello. toouse массовое получение подход более bulk, создайте манифест (IngestManifest), описывающий активов hello и связанные с ней файлы. Затем используйте метод отправки hello ваш выбор tooupload hello связанные файлы toohello манифеста контейнера BLOB-объектов. Службы мультимедиа Microsoft Azure отслеживает hello контейнер больших двоичных объектов, связанных с манифестом hello. Как только файл отправленного toohello контейнер больших двоичных объектов, службы мультимедиа Microsoft Azure завершает hello создания ресурса, на основе конфигурации hello средства hello в манифесте hello (IngestManifestAsset).

toocreate нового объекта IngestManifest вызвать метод Create hello, предоставляемые hello коллекции hello CloudMediaContext объекты Ingestmanifest. Этот метод создаст новый IngestManifest с именем манифеста hello вами.

    IIngestManifest manifest = context.IngestManifests.Create(name);

Создайте hello активы, которые будут связаны с неполным hello IngestManifest. Настройте параметры шифрования hello требуемого hello активе для массового получения.

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

Сущность IngestManifestAsset связывает ресурс с массовой сущностью IngestManifest для массового приема. Он также связывает hello AssetFiles, составляющих каждого средства. toocreate IngestManifestAsset, используйте метод Create hello на контекст сервера hello.

Hello следующий пример демонстрирует добавление двух новых IngestManifestAssets, которые связывают два актива hello ранее созданные toohello массового манифеста получения. Каждая сущность IngestManifestAsset связывает также набор файлов, которые передаются для каждого ресурса во время массового приема.  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

Можно использовать любое высокоскоростное клиентское приложение может загрузить контейнер больших двоичных объектов хранилища для активов файлы hello toohello URI, предоставляемые hello **IIngestManifest.BlobStorageUriForUpload** свойство hello IngestManifest. [Приложение Aspera On Demand for Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6)— одна из наиболее примечательных служб высокоскоростной передачи. Можно также написать код tooupload hello ресурсных файлов как показано в следующем примере кода hello.

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

Hello код для отправки файлов активов hello для образца hello, используемый в этом разделе показан в следующем примере кода hello.

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


Можно определить ход выполнения hello hello массового добавления для всех ресурсов, связанных с **IngestManifest** путем опроса свойства статистики hello hello **IngestManifest**. В сведения о заказе tooupdate хода выполнения, необходимо использовать новый **CloudMediaContext** каждый раз опроса свойства Statistics hello.

Hello следующий пример демонстрирует опрос в IngestManifest, его **идентификатор**.

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



## <a name="upload-files-using-net-sdk-extensions"></a>Передача файлов с помощью расширений пакета SDK для .NET
Hello приведенном ниже примере показано, как tooupload один файл с помощью расширений SDK .NET. В этом случае hello **CreateFromFile** метод используется, но также доступна асинхронная версия hello (**CreateFromFileAsync**). Hello **CreateFromFile** метод позволяет указать имя файла hello, шифрование и обратный вызов в порядке tooreport hello ход hello файла отправки.

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

Hello следующий пример вызывает функцию UploadFile и задает в качестве параметра создания активов hello шифрование хранилища.  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a>Дальнейшие действия

Теперь можно закодировать отправленные ресурсы. Дополнительную информацию см. в статье, посвященной [кодированию ресурсов](media-services-portal-encode.md).

Также можно использовать функции Azure tootrigger задание кодирования на основе файла, поступающих в контейнере hello настроен. Дополнительные сведения см. в [этом примере](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Дальнейшие действия
Теперь, когда вы отправили актива служб tooMedia go toohello [как обработчик мультимедиа tooGet] [ How tooGet a Media Processor] раздела.

[How tooGet a Media Processor]: media-services-get-media-processor.md

