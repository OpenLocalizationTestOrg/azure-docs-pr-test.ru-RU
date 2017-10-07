---
title: "aaaDevelop функции Azure с помощью служб мультимедиа"
description: "В этом разделе показано, как toostart разработки Azure работают с помощью служб мультимедиа hello портал Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a>Разработка Функций Azure с помощью служб мультимедиа

В этом разделе показано, как tooget работу с создания функций Azure, использование служб мультимедиа. Hello Azure функцию, определенную в этом разделе отслеживает контейнер учетной записи хранилища с именем **ввода** для новых файлов MP4. После удаления файла в контейнер хранилища hello hello больших двоичных объектов будет выполняться триггер функции hello.

Извлечение tooexplore и развернуть существующих функций Azure, использование служб мультимедиа Azure, [функции Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). Этот репозиторий содержит примеры использования служб мультимедиа tooshow рабочие процессы связанных tooingesting содержимого непосредственно из хранилища больших двоичных объектов, кодирования и записи содержимого резервное хранилище tooblob. Он также включает примеры как toomonitor задания уведомления через веб-перехватчиков и очереди Azure. Предусмотрена также возможность разрабатывать в виде примеров hello в hello функций [функции Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) репозитория. функции hello toodeploy, нажмите клавишу hello **развертывание tooAzure** кнопки.

## <a name="prerequisites"></a>Предварительные требования

- Перед созданием первой функции, необходимо toohave активную учетную запись Azure. Если у вас ее нет, воспользуйтесь [бесплатной учетной записью Azure](https://azure.microsoft.com/free/).
- Если вы собираетесь функции toocreate Azure, выполнять действия в вашей учетной записи служб мультимедиа Azure (AMS) или прослушивания tooevents, отправленные службами мультимедиа, следует создать учетную запись AMS, как описано [здесь](media-services-portal-create-account.md).
- Понимание [как toouse Azure функции](../azure-functions/functions-overview.md). Кроме того, ознакомьтесь со следующими разделами:
    - [Привязки HTTP и webhook в функциях Azure](../azure-functions/functions-triggers-bindings.md)
    - [Как параметры приложения Azure функция tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>Рекомендации

-  Функции Azure, выполняемых в рамках плана потребления hello имеют ограничения времени ожидания 5 минут.

## <a name="create-a-function-app"></a>Создание приложения-функции

1. Go toohello [портал Azure](http://portal.azure.com) и войдите с учетной записью Azure.
2. Создайте приложение-функцию, как описано [здесь](../azure-functions/functions-create-function-app-portal.md).

>[!NOTE]
> Учетная запись хранения, указанной в hello **StorageConnection** переменной среды (см. следующий шаг hello) должны находиться в hello же регионе, что ваше приложение.

## <a name="configure-function-app-settings"></a>Настройка параметров приложения-функции

При разработке функций служб мультимедиа, бывает удобно tooadd переменные среды, которые будут использоваться во всей функции. Параметры приложения tooconfigure, щелкните ссылку настроить параметры приложения hello. Дополнительные сведения см. в разделе [как параметры приложения Azure функция tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

Например:

![данных](./media/media-services-azure-functions/media-services-azure-functions001.png)

функции Hello, определенные в этой статье предполагается, что у вас есть следующие переменные среды в параметрах приложения hello.

**AMSAccount**: *имя учетной записи AMS* (например, testams).

**AMSKey**: *ключ учетной записи AMS* (например, IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=).

**MediaServicesStorageAccountName**: *имя учетной записи хранения* (например, testamsstorage).

**MediaServicesStorageAccountKey**: *ключ учетной записи хранения* (например, xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ или awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==).

**StorageConnection**: *подключения к хранилищу* (например, DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==).

## <a name="create-a-function"></a>Создание функции

После развертывания приложения-функции его можно найти в Функциях Azure **службы приложений**.

1. Выберите свое приложение-функцию и щелкните **Новая функция**.
2. Выберите hello **C#** языка и **обработки данных** сценария.
3. Выберите шаблон **BlobTrigger**. Эта функция будет применяться всякий раз, когда большой двоичный объект загружается в hello **ввода** контейнера. Hello **ввода** имя задается в hello **путь**, в следующем шаге hello.

    ![файлов](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. После выбора **BlobTrigger**, некоторые дополнительные элементы управления будут отображаться на странице приветствия.

    ![файлов](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. Щелкните **Создать**. 


## <a name="files"></a>Файлы

Функция Azure связана с файлами кода и другими файлами, описание которых представлено в данной статье. По умолчанию она связана с файлами **function.json** и **run.csx** (C#). Вам потребуется tooadd **project.json** файла. Hello оставшейся части этого раздела показаны hello определения для этих файлов.

![файлов](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>function.json

файл function.json Hello определяет привязки функций hello и других параметров конфигурации. Hello среды выполнения использует этот файл toodetermine hello события toomonitor и функционировать как toopass и возврат данных из выполнения. Дополнительные сведения см. в статье [Привязки HTTP и webhook в функциях Azure](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Набор hello **отключено** свойство слишком**true** функции hello tooprevent выполнение. 


Ниже приведен пример файла **function.json**.

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a>project.json

файл project.json Hello содержит зависимости. Ниже приведен пример **project.json** файл, который включает службы мультимедиа Azure .NET hello необходимые пакеты из Nuget. Обратите внимание, что номера версий hello изменится с последними обновлениями toohello пакетов, таким образом следует проверить hello самых последних версий. 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a>run.csx

Это hello C# кода для функции.  функции Hello указанных ниже мониторы контейнер учетной записи хранилища с именем **ввода** (это то, что был указан в пути hello) для новых файлов MP4. После удаления файла в контейнер хранилища hello hello больших двоичных объектов будет выполняться триггер функции hello.
    
демонстрирует пример Hello, заданные в этом разделе 

1. учетной записи tooingest актива в службы мультимедиа (например, копирование большого двоичного объекта в актив AMS) и 
2. как toosubmit предварительно задание кодирования, использующего носителя кодировщика Standard «адаптивной потоковой передачи».

В сценарии реальной жизни hello скорее всего, вы хотите tootrack ход выполнения задания, а затем опубликовать кодировке актива. Дополнительные сведения см. в разделе [служб мультимедиа Azure использование веб-перехватчиков toomonitor задания уведомления](media-services-dotnet-check-job-progress-with-webhooks.md). Дополнительные примеры приведены в разделе [функций Azure для служб мультимедиа](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

После определения функции щелкните **Сохранить и запустить**.

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
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


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get hello destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of hello destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a>Тестирование функции

tootest функции, необходимые MP4-файл в hello tooupload **ввода** контейнера hello учетной записи хранения, указанной в строке подключения hello.  

## <a name="next-step"></a>Дальнейшие действия

На этом этапе вы являются готов toostart разработки приложений служб мультимедиа. 
 
Дополнительные сведения и полный образцы и решений с помощью функции Azure и логика приложений с рабочими процессами создания пользовательского содержимого toocreate служб мультимедиа Azure см. в разделе hello [пример интеграции функций .NET служб мультимедиа на GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)

Кроме того, в разделе [служб мультимедиа Azure использование веб-перехватчиков toomonitor задания уведомления с помощью .NET](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

