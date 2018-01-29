---
title: "Разработка Функций Azure с помощью служб мультимедиа"
description: "В этой статье описывается разработка Функций Azure с помощью служб мультимедиа на портале Azure."
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
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: f99fe340b6cfebaafb04af9dba8abf9cb0f09a2b
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="develop-azure-functions-with-media-services"></a>Разработка Функций Azure с помощью служб мультимедиа

В этой статье показано, как приступить к работе с созданием функции Azure, использование служб мультимедиа. Функция Azure, определенные в этой статье отслеживает контейнер учетной записи хранилища с именем **ввода** для новых файлов MP4. После удаления файла в контейнер хранилища больших двоичных объектов триггер выполняет функцию. **Обзор функций Azure** см. в разделах статьи [Общие сведения о Функциях Azure](../azure-functions/functions-overview.md).

Если вы хотите изучить и развернуть существующие службы "Функции Azure", использующие службы мультимедиа Azure, ознакомьтесь с [функциями Azure для служб мультимедиа](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). Этот репозиторий содержит примеры, которые используют службы мультимедиа, чтобы показать рабочие процессы, связанные с приемом содержимого напрямую от хранилища BLOB-объектов, шифрованием и записью содержимого обратно в хранилище BLOB-объектов. В нем также содержатся примеры отслеживания уведомлений заданий через объекты webhook и очереди Azure. Можно также разработать свои функции на основе примеров из репозитория [Функций Azure для служб мультимедиа](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). Для развертывания функций нажмите кнопку **Развертывание в Azure**.

## <a name="prerequisites"></a>Технические условия

- Чтобы создавать функции, вам нужна активная учетная запись Azure. Если у вас ее нет, воспользуйтесь [бесплатной учетной записью Azure](https://azure.microsoft.com/free/).
- Если вы хотите создать Функции Azure, которые выполняют определенные действия в учетной записи служб мультимедиа Azure (AMS) или прослушивают события, отправляемые службами мультимедиа, вам необходимо создать учетную запись AMS, следуя приведенным [здесь](media-services-portal-create-account.md) инструкциям.
    
## <a name="create-a-function-app"></a>Создание приложения-функции

1. Перейдите на [портал Azure](http://portal.azure.com) и войдите, используя свою учетную запись Azure.
2. Создайте приложение-функцию, как описано [здесь](../azure-functions/functions-create-function-app-portal.md).

>[!NOTE]
> Учетная запись хранения, указанная в переменной среды **StorageConnection** (см. следующий шаг), должна находиться в том же регионе, что и ваше приложение.

## <a name="configure-function-app-settings"></a>Настройка параметров приложения-функции

При разработке функций служб мультимедиа удобно добавить переменные среды, которые будут использоваться в функциях. Чтобы настроить параметры приложения, щелкните ссылку "Настроить параметры приложения". Дополнительную информацию см. в разделе [Настройка параметров приложения-функции Azure](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

В функции, определенной в этой статье, предполагается, что в параметрах приложения настроены следующие переменные среды.

**AMSAADTenantDomain**: конечная точка клиента Azure AD. Дополнительные сведения о подключении к AMS API см. в [этой статье](media-services-use-aad-auth-to-access-ams-api.md).

**AMSRESTAPIEndpoint**: URI, который соответствует конечной точке REST API. 

**AMSClientId**: идентификатор клиента приложения Azure AD

**AMSClientSecret** — секрет клиента приложения Azure AD.

**StorageConnection**: соединение хранилища учетной записи, связанной с учетной записью служб мультимедиа. Это значение используется в файлах **function.json** и **run.csx** (как описано ниже).

## <a name="create-a-function"></a>Создание функции

После развертывания приложения-функции его можно найти в Функциях Azure **службы приложений**.

1. Выберите свое приложение-функцию и щелкните **Новая функция**.
2. Выберите язык **C#** и сценарий **Обработка данных**.
3. Выберите шаблон **BlobTrigger**. Эта функция будет запускаться при каждом отправки большого двоичного объекта в **ввода** контейнера. На следующем шаге в **Path** указывается имя **input**.

    ![файлов](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. После выбора **BlobTrigger**, на этой странице отображаются некоторые дополнительные элементы управления.

    ![файлов](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. Нажмите кнопку **Создать**. 

## <a name="files"></a>Файлы

Функция Azure связана с файлами кода и другими файлами, описание которых представлено в данной статье. При создании функции с помощью портала Azure файлы **function.json** и **run.csx** создаются автоматически. Вам потребуется добавить или отправить файл **project.json**. В оставшейся части этого раздела содержится краткое описание и определение каждого из этих файлов.

![файлов](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>function.json

Файл function.json определяет привязки функций и другие параметры конфигурации. В среде выполнения этот файл используется для определения событий, которые необходимо отслеживать, и способа передачи данных в выполнение функции и возвращения данных из него. Дополнительные сведения см. в статье [Привязки HTTP и webhook в функциях Azure](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Чтобы функция не выполнялась, задайте для свойства **disabled** значение **true**. 

Замените содержимое существующего файла function.json следующим кодом:

```
{
  "bindings": [
    {
      "name": "myBlob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "input/{filename}.mp4",
      "connection": "ConnectionString"
    }
  ],
  "disabled": false
}
```

### <a name="projectjson"></a>project.json

Файл project.json содержит зависимости. Ниже приведен пример файла **project.json**, содержащего необходимые пакеты служб мультимедиа Azure для .NET из NuGet. Обратите внимание, что номера версий изменить с помощью последних обновлений для пакетов, таким образом, чтобы подтверждать самую новую версию. 

Добавьте следующее определение в файл project.json. 

```
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "windowsazure.mediaservices": "4.0.0.4",
        "windowsazure.mediaservices.extensions": "4.0.0.4",
        "Microsoft.IdentityModel.Clients.ActiveDirectory": "3.13.1",
        "Microsoft.IdentityModel.Protocol.Extensions": "1.0.2.206221351"
      }
    }
   }
}

```
    
### <a name="runcsx"></a>run.csx

Это код C# для функции.  Функция, определенная ниже, отслеживает контейнер учетной записи хранения **input** (который был указан в пути) на наличие новых MP4-файлов. После удаления файла в контейнер хранилища больших двоичных объектов триггер выполняет функцию.
    
В примере, определенном в этом разделе, демонстрируется, 

1. как принять ресурс в учетной записи служб мультимедиа (скопировать большой двоичный объект в ресурс AMS) и 
2. как отправить задание кодирования, использующее предустановку Adaptive Streaming из Media Encoder Standard.

В реальном сценарии скорее всего потребуется отслеживать ход выполнения задания, а затем опубликовать закодированный ресурс. Дополнительные сведения см. в статье [Использование объектов Webhook Azure для наблюдения за уведомлениями о заданиях служб мультимедиа с использованием .NET](media-services-dotnet-check-job-progress-with-webhooks.md). Дополнительные примеры приведены в разделе [функций Azure для служб мультимедиа](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

Замените содержимое существующего файла run.csx следующий код: после завершения определении функции щелкните **сохранить и запустить**.

```
#r "Microsoft.WindowsAzure.Storage"
#r "Newtonsoft.Json"
#r "System.Web"

using System;
using System.Net;
using System.Net.Http;
using Newtonsoft.Json;
using Microsoft.WindowsAzure.MediaServices.Client;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using System.IO;
using System.Web;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.Azure.WebJobs;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
  
// Read values from the App.config file.

static readonly string _AADTenantDomain = Environment.GetEnvironmentVariable("AMSAADTenantDomain");
static readonly string _RESTAPIEndpoint = Environment.GetEnvironmentVariable("AMSRESTAPIEndpoint");
 
static readonly string _mediaservicesClientId = Environment.GetEnvironmentVariable("AMSClientId");
static readonly string _mediaservicesClientSecret = Environment.GetEnvironmentVariable("AMSClientSecret");

static readonly string _connectionString = Environment.GetEnvironmentVariable("ConnectionString");  

private static CloudMediaContext _context = null;
private static CloudStorageAccount _destinationStorageAccount = null;

public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
{
    // NOTE that the variables {fileName} here come from the path setting in function.json
    // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
    // was dropped into the input container for the function. 

    // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
    // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

    log.Info($"C# Blob trigger function processed: {fileName}.mp4");
    log.Info($"Media Services REST endpoint : {_RESTAPIEndpoint}");

    try
    {
        AzureAdTokenCredentials tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain,
                            new AzureAdClientSymmetricKey(_mediaservicesClientId, _mediaservicesClientSecret),
                            AzureEnvironments.AzureCloudEnvironment);
 
        AzureAdTokenProvider tokenProvider = new AzureAdTokenProvider(tokenCredentials);
 
        _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
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
/// Creates a new asset and copies blobs from the specifed storage account.
/// </summary>
/// <param name="blob">The specified blob.</param>
/// <returns>The new asset.</returns>
public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
{
     //Get a reference to the storage account that is associated with the Media Services account. 
    _destinationStorageAccount = CloudStorageAccount.Parse(_connectionString);

    // Create a new asset. 
    var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
    log.Info($"Created new asset {asset.Name}");

    IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
    TimeSpan.FromHours(4), AccessPermissions.Write);
    ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
    CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

    // Get the destination asset container reference
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

    // Get hold of the destination blob
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
```

##<a name="test-your-function"></a>Тестирование функции

Чтобы протестировать функцию, необходимо передать MP4-файл в контейнер учетной записи хранения **input**, указанный в строке подключения.  

1. Выберите учетную запись хранилища, которую вы указали в переменной среды **StorageConnection**.
2. Щелкните **Большие двоичные объекты**.
3. Щелкните **+ Container** (+ Контейнер). Введите имя для **входных данных** контейнера.
4. Нажмите клавишу **отправить** и перейдите в MP4-файл, который требуется отправить.

>[!NOTE]
> Если используется триггер BLOB-объекта в плане потребления, то после того как приложение-функция стало неактивным, обработка новых BLOB-объектов может осуществляться с задержкой до 10 минут. После запуска приложения-функции большие двоичные объекты обрабатываются немедленно. Дополнительные сведения см. в статье о [привязках и триггерах хранилища BLOB-объектов](https://docs.microsoft.com/azure/azure-functions/functions-bindings-storage-blob#blob-storage-triggers-and-bindings).

## <a name="next-steps"></a>Дальнейшие действия

На этом этапе вы готовы начать разработку приложения служб мультимедиа. 
 
Дополнительные сведения и полные примеры и решения на основе служб "Функции Azure" и Logic Apps с использованием служб мультимедиа Azure, предназначенные для создания рабочих процессов, создающих пользовательское содержимое, можно изучить на [примере интеграции службы "Функции Azure" и служб мультимедиа с помощью .NET на сайте GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).

Кроме того, ознакомьтесь с разделом [Использование объектов Webhook Azure для наблюдения за уведомлениями о заданиях служб мультимедиа с использованием .NET](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

