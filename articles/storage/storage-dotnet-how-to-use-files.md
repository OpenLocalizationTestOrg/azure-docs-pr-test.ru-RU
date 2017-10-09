---
title: "aaaDevelop для хранилища Azure File с помощью .NET | Документы Microsoft"
description: "Узнайте, как данные файлов toodevelop приложений и служб .NET, использующих toostore хранилище файлов Azure."
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: aa8f84f1c93249055370e2a2cb33d7118b972be1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a>Разработка для хранилища файлов Azure с помощью .NET 
> [!NOTE]
> В этой статье показано, как toomanage хранилища Azure File с кодом .NET. toolearn Дополнительные сведения о хранилище файлов Azure см. в разделе hello [tooAzure введение хранения файлов](storage-files-introduction.md).
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>О данном учебнике
Этот учебник продемонстрируют hello основные принципы использования toodevelop приложения или службы .NET, использующих данные файла toostore хранилище файлов Azure. В этом учебнике мы создайте простое консольное приложение и Показать как tooperform базовые действия с хранилищем .NET и файлов Azure:

* Получение содержимого файла hello
* Задать квоты hello (максимальный размер) для общей папки hello.
* Создание подписанного URL-адреса (ключ SAS) для файла, который использует политику общего доступа, определенные в общей папке hello.
* Скопируйте файл tooanother в hello учетную запись хранения.
* Копирование большого двоичного объекта файла tooa в hello учетную запись хранения.
* Используйте метрики службы хранилища Azure как средство устранения неполадок.

> [!Note]  
> Поскольку хранилище файлов Azure может осуществляться по протоколу SMB, вполне возможно toowrite простых приложений, получающих доступ к папке файлов Azure hello, с помощью стандартных классов System.IO hello для файлового ввода-вывода. В этой статье описывается, как toowrite приложения, использующие hello пакет SDK .NET хранилища Azure, которая использует hello [хранилища Azure File API-интерфейса REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure хранилища файлов. 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a>Создайте консольное приложение hello и получить сборку hello
В Visual Studio создайте новое консольное приложение Windows. следующие шаги Hello Показать чем toocreate консольное приложение в Visual Studio 2017 г., однако hello действия схожи в других версиях Visual Studio.

1. Выберите **Файл** > **Создать** > **Проект**.
2. Выберите **Установлено** > **Шаблоны** > **Visual C#** > **Классический рабочий стол Windows**.
3. Выберите **Консольное приложение (.NET Framework)**.
4. Введите имя для вашего приложения в hello **имя:** поля
5. Нажмите кнопку **ОК**.

Все примеры кода в этом учебнике можно добавить toohello `Main()` метода приложения командной `Program.cs` файла.

Hello клиентская библиотека хранилища Azure можно использовать в любом приложении .NET, включая Azure облачной службы или веб-приложение и приложений для настольных компьютеров и мобильных устройств. Для упрощения в этом руководстве мы будем использовать консольное приложение.

## <a name="use-nuget-tooinstall-hello-required-packages"></a>Использовать hello необходимые пакеты NuGet tooinstall
Существует два пакета, необходимо использовать tooreference в ваш проект toocomplete этого учебника:

* [Клиентская библиотека хранилища Microsoft Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): данный пакет обеспечивает программный доступ toodata ресурсы в вашей учетной записи хранилища.
* [Библиотека Microsoft Azure Configuration Manager для .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) — этот пакет предоставляет класс для анализа строки подключения в файле конфигурации независимо от среды выполнения приложения.

Можно использовать оба пакета NuGet tooobtain. Выполните следующие действия.

1. Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Управление пакетами NuGet**.
2. Найдите в Интернете «WindowsAzure.Storage» и нажмите кнопку **установить** tooinstall hello клиентской библиотеки хранилища и его зависимости.
3. Найдите в Интернете «WindowsAzure.ConfigurationManager» и нажмите кнопку **установить** tooinstall hello Azure Configuration Manager.

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a>Сохраните файл app.config toohello учетные данные учетной записи хранилища
Затем сохраните данные учетной записи хранения в файле app.config вашего проекта. Изменить файл app.config hello, чтобы он отображался как toohello следующий пример, заменив `myaccount` имя вашей учетной записи хранилища и `mykey` с помощью ключа учетной записи хранилища.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> Последняя версия эмулятора хранилища Azure hello Hello не поддерживает хранилище файлов Azure. Учетная запись хранения Azure в облаке toowork hello с хранилищем файлов Azure должны предназначаться для строки подключения.

## <a name="add-using-directives"></a>Добавление директив using
Откройте hello `Program.cs` файл из обозревателя решений и добавьте следующее hello с помощью директивы toohello вверху файла hello.

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a>Доступ hello общая папка программным способом
Добавьте следующий код toohello hello `Main()` строка подключения hello tooretrieve метод (после приведенного выше кода hello). Этот код возвращает файла toohello ссылок, созданную ранее и выводит в окно консоли toohello его содержимое.

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

Запустите выходных данных hello toosee hello консольного приложения.

## <a name="set-hello-maximum-size-for-a-file-share"></a>Установить максимальный размер hello для общей папки
Начиная с версии 5.x hello клиентская библиотека хранилища Azure, можно задать набор hello квоты (или максимальный размер) для общей папки в гигабайтах. Можно также проверить, какой объем данных в настоящее время хранится в папке hello toosee.

В параметр квоты hello для общей папки можно ограничить общий размер hello hello файлы, хранящиеся в папке hello. Если общий размер файлов в общей папке hello hello превышает квоту hello задать для общей папки hello, а затем клиентов будет невозможно tooincrease hello размера существующих файлов или создания новых файлов, если эти файлы являются пустыми.

Hello приведенном ниже примере показано, как toocheck hello текущего использования для общей папки и как tooset hello квоты для общей папки hello.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Создание подписи общего доступа для файла или файлового ресурса
Начиная с версии 5.x Здравствуйте клиентская библиотека хранилища Azure, можно создать подпись коллективного доступа (SAS) для общей папки или отдельного файла. Можно также создать политики общего доступа на общих toomanage общий доступ к файлам подписи. Создание политики общего доступа рекомендуется, так как она предоставляет средства отзыва hello SAS, если он должен быть скомпрометирован.

Следующий пример Hello создает политику общего доступа в общей папке, а затем использует ограничения hello tooprovide политика для SAS для файла в hello совместного использования.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

Дополнительные сведения см. в статьях [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md) и [Подписанные URL-адреса. Часть 2: создание и использование подписанного URL-адреса в службе BLOB-объектов](storage-dotnet-shared-access-signature-part-2.md).

## <a name="copy-files"></a>Копирование файлов
Начиная с версии 5.x hello клиентская библиотека хранилища Azure, можно скопировать файл tooanother, большой двоичный объект файла tooa или tooa файла большого двоичного объекта. В следующих разделах hello показывается как tooperform их копирование операций программными средствами.

Также можно использовать один файл tooanother AzCopy toocopy или toocopy большого двоичного объекта tooa файла, и наоборот. В разделе [перенесите данные с помощью служебной программы командной строки AzCopy hello](storage-use-azcopy.md).

> [!NOTE]
> При копировании файла tooa большого двоичного объекта или большой двоичный объект tooa файла необходимо использовать общего доступа (SAS) tooauthenticate hello исходного объекта сигнатуры, даже если копирование производится внутри hello же учетной записи хранилища.
> 
> 

**Скопируйте файл tooanother** hello следующий пример копирует файл tooanother в hello одной общей папке. Так как эта операция копирования копирует между Здравствуйте, файлы в учетную запись хранения, можно использовать копию hello tooperform проверки подлинности Shared Key.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

**Копирование большого двоичного объекта файла tooa** hello следующий пример создает файл и копирует его tooa BLOB-объектов в пределах hello учетную запись хранения. пример Hello создает SAS для hello исходного файла, службу hello, которая использует tooauthenticate доступа toohello исходный файл во время операции копирования hello.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

Можно скопировать tooa файла большого двоичного объекта в hello таким же образом. Если hello объекта источника является большой двоичный объект, необходимо создайте большой двоичный объект toothat SAS tooauthenticate доступ во время операции копирования hello.

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>Устранение неполадок хранилища файлов Azure с помощью метрик
Аналитика службы хранилища Azure теперь поддерживает метрики для хранилища файлов Azure. Данные метрик позволяют отслеживать запросы и диагностировать проблемы.


Можно включить метрики для хранилища Azure File с hello [портала Azure](https://portal.azure.com). Можно также включить метрики программным образом с вызывающему Привет операции установки свойств службы файлов с помощью API-интерфейса REST hello, или один из его аналоги в hello клиентской библиотеки хранилища.


Hello в следующем примере кода показано, как toouse hello клиентской библиотеки хранилища для .NET tooenable метрики для хранения файлов Azure.

Во-первых, добавьте следующее hello `using` tooyour директивы `Program.cs` файлов, кроме toothose добавленных выше:

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

Обратите внимание, что при больших двоичных объектов Azure, таблицы Azure и очереди Azure hello совместно использовать `ServiceProperties` типа в hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` имен хранилища Azure File использует собственный тип hello `FileServiceProperties` типа в hello `Microsoft.WindowsAzure.Storage.File.Protocol` пространства имен. Оба пространства имен должен ссылаться в коде, однако для следующих toocompile кода hello.

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read hello metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

Кроме того, можно ссылаться слишком[хранилища Azure File статьи по устранению неполадок](storage-troubleshoot-file-connection-problems.md) для начала до конца рекомендации по устранению неполадок.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.

### <a name="conceptual-articles-and-videos"></a>Тематические статьи и видео
* [Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Хранилище файлов Azure: удобная облачная файловая система SMB для Windows и Linux)
* [Как toouse хранилища Azure File с Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Средства для работы с хранилищем файлов
* [Использование Azure PowerShell со службой хранилища Azure](storage-powershell-guide-full.md)
* [Как toouse AzCopy с хранилищем Microsoft Azure](storage-use-azcopy.md)
* [С помощью hello Azure CLI со службой хранилища Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Устранение неполадок хранилища файлов Azure](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>Справочные материалы
* [Справочник по клиентской библиотеке хранилища для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Справочник по REST API службы файлов](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>Записи блога
* [Хранилище файлов Azure стало общедоступным](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Хранилище файлов Azure: взгляд изнутри)
* [Введение в службы файлов Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Сохранение соединений tooMicrosoft хранилища Azure File](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
