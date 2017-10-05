---
title: "Разработка для хранилища файлов Azure с помощью .NET | Документация Майкрософт"
description: "Узнайте, как разработать приложения и службы .NET, использующие хранилище файлов Azure для хранения файлов данных."
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
ms.openlocfilehash: e26da88ef1803d47d7286c5ae836ac9c041dadd1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a>Разработка для хранилища файлов Azure с помощью .NET 
> [!NOTE]
> В этой статье описывается управление хранилищем файлов Azure с помощью кода .NET. Дополнительные сведения о хранилище файлов Azure см. в статье [Introduction to Azure File storage](storage-files-introduction.md) (Знакомство с хранилищем файлов Azure).
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>О данном учебнике
В этом руководстве мы рассмотрим основы использования .NET для разработки приложений и служб, использующих хранилище файлов Azure для хранения файлов данных. В рамках этого руководства мы создадим простое консольное приложение, а также покажем, как выполнять базовые действия с .NET и хранилищем файлов Azure:

* Получите содержимое файла.
* Задайте квоту (максимальный размер) для общей папки
* Создайте подпись общего доступа (ключ SAS) для файла, который использует политику общего доступа, определенную в общей папке.
* Скопируйте файл в другой файл в той же учетной записи хранения
* Скопируйте файл в BLOB-объект в той же учетной записи хранения
* Используйте метрики службы хранилища Azure как средство устранения неполадок.

> [!Note]  
> Так как доступ к хранилищу файлов Azure можно получить с помощью SMB, можно написать простые приложения, которые получают доступ к общей папке Azure, используя стандартные классы System.IO для файлового ввода-вывода. Из этой статьи вы узнаете, как написать приложения, использующие пакет SDK .NET для службы хранилища Azure, который использует [REST API хранилища файлов Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) для взаимодействия с этим хранилищем. 


## <a name="create-the-console-application-and-obtain-the-assembly"></a>Создание консольного приложения и получение сборки
В Visual Studio создайте новое консольное приложение Windows. Ниже показано, как создать консольное приложение в Visual Studio 2017. Эти инструкции применимы и в других версиях Visual Studio.

1. Выберите **Файл** > **Создать** > **Проект**.
2. Выберите **Установлено** > **Шаблоны** > **Visual C#** > **Классический рабочий стол Windows**.
3. Выберите **Консольное приложение (.NET Framework)**.
4. Введите имя приложения в поле **Имя**.
5. Нажмите кнопку **ОК**.

Все примеры кода из этого руководства можно добавить в метод `Main()` в файле `Program.cs` консольного приложения.

Вы можете использовать клиентскую библиотеку службы хранилища Azure в любом приложении .NET, в том числе в облачной службе Azure, веб-приложении Azure, классическом или мобильном приложении. Для упрощения в этом руководстве мы будем использовать консольное приложение.

## <a name="use-nuget-to-install-the-required-packages"></a>Установка необходимых пакетов с помощью NuGet
Для работы с этим руководством вам нужно указать в проекте два пакета:

* [Клиентская библиотека службы хранилища Microsoft Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)— этот пакет предоставляет программный доступ к ресурсам данных в вашей учетной записи хранения.
* [Библиотека Microsoft Azure Configuration Manager для .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) — этот пакет предоставляет класс для анализа строки подключения в файле конфигурации независимо от среды выполнения приложения.

Вы можете использовать NuGet для установки обоих пакетов. Выполните следующие действия.

1. Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Управление пакетами NuGet**.
2. Выполните в Интернете поиск по запросу "WindowsAzure.Storage" и нажмите кнопку **Установить** , чтобы установить клиентскую библиотеку службы хранилища и зависимые компоненты.
3. Выполните поиск в Интернете по запросу WindowsAzure.ConfigurationManager и нажмите кнопку **Установить**, чтобы установить Azure Configuration Manager.

## <a name="save-your-storage-account-credentials-to-the-appconfig-file"></a>Сохранение данных учетной записи хранения в файле app.config.
Затем сохраните данные учетной записи хранения в файле app.config вашего проекта. Замените содержимое файла app.config текстом из следующего примера: введите вместо `myaccount` имя учетной записи хранения, а вместо `mykey` — ключ учетной записи хранения.

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
> Последняя версия эмулятора хранения Azure не поддерживает хранилище файлов Azure. Для работы с хранилищем файлов Azure необходимо, чтобы строка подключения указывала на учетную запись хранения Azure в облаке.

## <a name="add-using-directives"></a>Добавление директив using
В обозревателе решений откройте файл `Program.cs` и добавьте следующие директивы using в начало файла.

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-the-file-share-programmatically"></a>Доступ к общей папке программным путем
Затем, чтобы получить строку подключения, добавьте в метод `Main()` после указанного выше кода приведенный ниже код. Этот код получает ссылку на ранее созданный файл и выводит его содержимое в окне консоли.

```csharp
// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the file exists.
        if (file.Exists())
        {
            // Write the contents of the file to the console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

Запустите консольное приложение и получите вывод.

## <a name="set-the-maximum-size-for-a-file-share"></a>Установка максимального размера для файлового ресурса
Клиентская библиотека хранилища Azure версии 5.x и выше позволяет задавать квоту (или максимальный размер) в файловом ресурсе в гигабайтах. Можно также проверить, какой объем данных хранится в настоящее время в общей папке.

Задав квоту для файлового ресурса, можно ограничить общий размер файлов, хранящихся в общей папке. Если общий размер файлов в файловом ресурсе превышает установленную квоту, клиенты не смогут увеличить размер существующих файлов или создать новые файлы, только если они не являются пустыми.

В приведенном ниже примере показано, как проверить текущее использование данных в файловом ресурсе, а также задать для него квоту.

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Check current usage stats for the share.
    // Note that the ShareStats object is part of the protocol layer for the File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify the maximum size of the share, in GB.
    // This line sets the quota to be 10 GB greater than the current usage of the share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check the quota for the share. Call FetchAttributes() to populate the share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Создание подписи общего доступа для файла или файлового ресурса
Начиная с версии 5.x клиентской библиотеки хранилища Azure можно создать подпись общего доступа (SAS) для файлового ресурса или отдельного файла. Также можно создать политики общего доступа на файловом ресурсе, чтобы управлять подписями общего доступа. Создание политики общего доступа рекомендуется, так как она позволяет отменить SAS, если она скомпрометирована.

В приведенном ниже примере создаются политики общего доступа в общей папке, а затем используются для обеспечения ограничения SAS для файла в общей папке.

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for the share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add the shared access policy to the share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in the share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from the SAS, and write some text to the file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

Дополнительные сведения см. в статьях [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md) и [Подписанные URL-адреса. Часть 2: создание и использование подписанного URL-адреса в службе BLOB-объектов](storage-dotnet-shared-access-signature-part-2.md).

## <a name="copy-files"></a>Копирование файлов
Начиная с версии 5.x клиентской библиотеки хранилища Azure можно скопировать файл в другой файл, файл в большой двоичный объект или BLOB-объект в файл. В следующих разделах демонстрируется выполнение этих операций копирования программными средствами.

AzCopy можно использовать для копирования одного файла в другой, а также копирования большого двоичного объекта в файл или наоборот. См. статью [Приступая к работе со служебной программой командной строки AzCopy](storage-use-azcopy.md).

> [!NOTE]
> При копировании большого двоичного объекта в файл или файла в большой двоичный объект необходимо использовать подпись общего доступа (SAS) для проверки подлинности исходного объекта, даже если копирование производится внутри одной и той же учетной записи хранения.
> 
> 

**Скопируйте файл в другой файл**. В приведенном ниже примере файл копируется в другой файл в той же общей папке. Так как эта операция копирования осуществляет копирование между файлами в одной учетной записи хранения, для выполнения копирования можно использовать проверку подлинности Shared Key.

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference to the destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start the copy operation.
            destFile.StartCopy(sourceFile);

            // Write the contents of the destination file to the console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

**Скопируйте файл в большой двоичный объект**. В приведенном ниже примере файл создается и копируется в большой двоичный объект в пределах одной и той же учетной записи хранения. В примере для исходного файла создается SAS, которую служба использует для проверки подлинности при доступе к исходному файлу во время операции копирования.

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in the root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in the root directory.");

// Get a reference to the blob to which the file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for the file that's valid for 24 hours.
// Note that when you are copying a file to a blob, or a blob to a file, you must use a SAS
// to authenticate access to the source object, even if you are copying within the same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for the source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct the URI to the source file, including the SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy the file to the blob.
destBlob.StartCopy(fileSasUri);

// Write the contents of the file to the console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

Таким же образом можно скопировать BLOB-объект в файл. Если исходным объектом является BLOB-объект, создайте SAS для проверки подлинности доступа к BLOB-объекту во время операции копирования.

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>Устранение неполадок хранилища файлов Azure с помощью метрик
Аналитика службы хранилища Azure теперь поддерживает метрики для хранилища файлов Azure. Данные метрик позволяют отслеживать запросы и диагностировать проблемы.


Вы можете включить метрики для файлового хранилища Azure с помощью [портала Azure](https://portal.azure.com). Кроме того, вы можете включить метрики программным путем. Для этого используйте операцию Set File Service Properties через интерфейс REST API или любой ее аналог из имеющихся в клиентской библиотеке хранилища.


В следующем примере кода показано, как использовать клиентскую библиотеку хранилища для .NET, чтобы включить метрики для хранилища файлов Azure.

Сначала добавьте в файл `Program.cs` следующие директивы `using` в дополнение к указанным выше.

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

Обратите внимание, что в то время, как большие двоичные объекты, таблицы и очереди Azure используют общий тип `ServiceProperties` в пространстве имен `Microsoft.WindowsAzure.Storage.Shared.Protocol`, хранилище файлов Azure использует собственный тип `FileServiceProperties` в пространстве имен `Microsoft.WindowsAzure.Storage.File.Protocol`. Однако для обеспечения компиляции приведенного ниже кода ваш код должен ссылаться на оба этих пространства имен.

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create the File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that the File service currently uses its own service properties type,
// available in the Microsoft.WindowsAzure.Storage.File.Protocol namespace.
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

// Read the metrics properties we just set.
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

Кроме того, вы можете найти подробное руководство по устранению неполадок в статье [Troubleshoot Azure File storage problems in Windows](storage-troubleshoot-file-connection-problems.md) (Устранение неполадок в хранилище файлов Azure).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.

### <a name="conceptual-articles-and-videos"></a>Тематические статьи и видео
* [Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Хранилище файлов Azure: удобная облачная файловая система SMB для Windows и Linux)
* [Использование хранилища файлов Azure в Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Средства для работы с хранилищем файлов
* [Использование Azure PowerShell со службой хранилища Azure](storage-powershell-guide-full.md)
* [Использование AzCopy со службой хранилища Microsoft Azure](storage-use-azcopy.md)
* [Использование интерфейса командной строки (CLI) Azure со службой хранилища Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Устранение неполадок хранилища файлов Azure](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>Справочные материалы
* [Справочник по клиентской библиотеке хранилища для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Справочник по REST API службы файлов](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>Записи блога
* [Хранилище файлов Azure стало общедоступным](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Хранилище файлов Azure: взгляд изнутри)
* [Введение в службы файлов Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx) (Сохраняемые подключения к файлам Microsoft Azure)