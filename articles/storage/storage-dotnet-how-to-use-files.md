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
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="48d93-103">Разработка для хранилища файлов Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="48d93-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="48d93-104">В этой статье описывается управление хранилищем файлов Azure с помощью кода .NET.</span><span class="sxs-lookup"><span data-stu-id="48d93-104">This article shows how to manage Azure File storage with .NET code.</span></span> <span data-ttu-id="48d93-105">Дополнительные сведения о хранилище файлов Azure см. в статье [Introduction to Azure File storage](storage-files-introduction.md) (Знакомство с хранилищем файлов Azure).</span><span class="sxs-lookup"><span data-stu-id="48d93-105">To learn more about Azure File storage, please see the [Introduction to Azure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="48d93-106">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="48d93-106">About this tutorial</span></span>
<span data-ttu-id="48d93-107">В этом руководстве мы рассмотрим основы использования .NET для разработки приложений и служб, использующих хранилище файлов Azure для хранения файлов данных.</span><span class="sxs-lookup"><span data-stu-id="48d93-107">This tutorial will demonstrate the basics of using .NET to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="48d93-108">В рамках этого руководства мы создадим простое консольное приложение, а также покажем, как выполнять базовые действия с .NET и хранилищем файлов Azure:</span><span class="sxs-lookup"><span data-stu-id="48d93-108">In this tutorial, we will create a simple console application and show how to perform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="48d93-109">Получите содержимое файла.</span><span class="sxs-lookup"><span data-stu-id="48d93-109">Get the contents of a file</span></span>
* <span data-ttu-id="48d93-110">Задайте квоту (максимальный размер) для общей папки</span><span class="sxs-lookup"><span data-stu-id="48d93-110">Set the quota (maximum size) for the file share.</span></span>
* <span data-ttu-id="48d93-111">Создайте подпись общего доступа (ключ SAS) для файла, который использует политику общего доступа, определенную в общей папке.</span><span class="sxs-lookup"><span data-stu-id="48d93-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>
* <span data-ttu-id="48d93-112">Скопируйте файл в другой файл в той же учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="48d93-112">Copy a file to another file in the same storage account.</span></span>
* <span data-ttu-id="48d93-113">Скопируйте файл в BLOB-объект в той же учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="48d93-113">Copy a file to a blob in the same storage account.</span></span>
* <span data-ttu-id="48d93-114">Используйте метрики службы хранилища Azure как средство устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="48d93-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="48d93-115">Так как доступ к хранилищу файлов Azure можно получить с помощью SMB, можно написать простые приложения, которые получают доступ к общей папке Azure, используя стандартные классы System.IO для файлового ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="48d93-115">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard System.IO classes for File I/O.</span></span> <span data-ttu-id="48d93-116">Из этой статьи вы узнаете, как написать приложения, использующие пакет SDK .NET для службы хранилища Azure, который использует [REST API хранилища файлов Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) для взаимодействия с этим хранилищем.</span><span class="sxs-lookup"><span data-stu-id="48d93-116">This article will describe how to write applications that use the Azure Storage .NET SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span> 


## <a name="create-the-console-application-and-obtain-the-assembly"></a><span data-ttu-id="48d93-117">Создание консольного приложения и получение сборки</span><span class="sxs-lookup"><span data-stu-id="48d93-117">Create the console application and obtain the assembly</span></span>
<span data-ttu-id="48d93-118">В Visual Studio создайте новое консольное приложение Windows.</span><span class="sxs-lookup"><span data-stu-id="48d93-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="48d93-119">Ниже показано, как создать консольное приложение в Visual Studio 2017. Эти инструкции применимы и в других версиях Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="48d93-119">The following steps show you how to create a console application in Visual Studio 2017, however, the steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="48d93-120">Выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="48d93-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="48d93-121">Выберите **Установлено** > **Шаблоны** > **Visual C#** > **Классический рабочий стол Windows**.</span><span class="sxs-lookup"><span data-stu-id="48d93-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="48d93-122">Выберите **Консольное приложение (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="48d93-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="48d93-123">Введите имя приложения в поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="48d93-123">Enter a name for your application in the **Name:** field</span></span>
5. <span data-ttu-id="48d93-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="48d93-124">Select **OK**</span></span>

<span data-ttu-id="48d93-125">Все примеры кода из этого руководства можно добавить в метод `Main()` в файле `Program.cs` консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="48d93-125">All code examples in this tutorial can be added to the `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="48d93-126">Вы можете использовать клиентскую библиотеку службы хранилища Azure в любом приложении .NET, в том числе в облачной службе Azure, веб-приложении Azure, классическом или мобильном приложении.</span><span class="sxs-lookup"><span data-stu-id="48d93-126">You can use the Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="48d93-127">Для упрощения в этом руководстве мы будем использовать консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="48d93-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-to-install-the-required-packages"></a><span data-ttu-id="48d93-128">Установка необходимых пакетов с помощью NuGet</span><span class="sxs-lookup"><span data-stu-id="48d93-128">Use NuGet to install the required packages</span></span>
<span data-ttu-id="48d93-129">Для работы с этим руководством вам нужно указать в проекте два пакета:</span><span class="sxs-lookup"><span data-stu-id="48d93-129">There are two packages you need to reference in your project to complete this tutorial:</span></span>

* <span data-ttu-id="48d93-130">[Клиентская библиотека службы хранилища Microsoft Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)— этот пакет предоставляет программный доступ к ресурсам данных в вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="48d93-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access to data resources in your storage account.</span></span>
* <span data-ttu-id="48d93-131">[Библиотека Microsoft Azure Configuration Manager для .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) — этот пакет предоставляет класс для анализа строки подключения в файле конфигурации независимо от среды выполнения приложения.</span><span class="sxs-lookup"><span data-stu-id="48d93-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="48d93-132">Вы можете использовать NuGet для установки обоих пакетов.</span><span class="sxs-lookup"><span data-stu-id="48d93-132">You can use NuGet to obtain both packages.</span></span> <span data-ttu-id="48d93-133">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="48d93-133">Follow these steps:</span></span>

1. <span data-ttu-id="48d93-134">Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="48d93-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="48d93-135">Выполните в Интернете поиск по запросу "WindowsAzure.Storage" и нажмите кнопку **Установить** , чтобы установить клиентскую библиотеку службы хранилища и зависимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="48d93-135">Search online for "WindowsAzure.Storage" and click **Install** to install the Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="48d93-136">Выполните поиск в Интернете по запросу WindowsAzure.ConfigurationManager и нажмите кнопку **Установить**, чтобы установить Azure Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="48d93-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** to install the Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-to-the-appconfig-file"></a><span data-ttu-id="48d93-137">Сохранение данных учетной записи хранения в файле app.config.</span><span class="sxs-lookup"><span data-stu-id="48d93-137">Save your storage account credentials to the app.config file</span></span>
<span data-ttu-id="48d93-138">Затем сохраните данные учетной записи хранения в файле app.config вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="48d93-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="48d93-139">Замените содержимое файла app.config текстом из следующего примера: введите вместо `myaccount` имя учетной записи хранения, а вместо `mykey` — ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="48d93-139">Edit the app.config file so that it appears similar to the following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> Последняя версия эмулятора хранения Azure не поддерживает хранилище файлов Azure. <span data-ttu-id="48d93-141">Для работы с хранилищем файлов Azure необходимо, чтобы строка подключения указывала на учетную запись хранения Azure в облаке.</span><span class="sxs-lookup"><span data-stu-id="48d93-141">Your connection string must target an Azure Storage Account in the cloud to work with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="48d93-142">Добавление директив using</span><span class="sxs-lookup"><span data-stu-id="48d93-142">Add using directives</span></span>
<span data-ttu-id="48d93-143">В обозревателе решений откройте файл `Program.cs` и добавьте следующие директивы using в начало файла.</span><span class="sxs-lookup"><span data-stu-id="48d93-143">Open the `Program.cs` file from Solution Explorer, and add the following using directives to the top of the file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-the-file-share-programmatically"></a><span data-ttu-id="48d93-144">Доступ к общей папке программным путем</span><span class="sxs-lookup"><span data-stu-id="48d93-144">Access the file share programmatically</span></span>
<span data-ttu-id="48d93-145">Затем, чтобы получить строку подключения, добавьте в метод `Main()` после указанного выше кода приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="48d93-145">Next, add the following code to the `Main()` method (after the code shown above) to retrieve the connection string.</span></span> <span data-ttu-id="48d93-146">Этот код получает ссылку на ранее созданный файл и выводит его содержимое в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="48d93-146">This code gets a reference to the file we created earlier and outputs its contents to the console window.</span></span>

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

<span data-ttu-id="48d93-147">Запустите консольное приложение и получите вывод.</span><span class="sxs-lookup"><span data-stu-id="48d93-147">Run the console application to see the output.</span></span>

## <a name="set-the-maximum-size-for-a-file-share"></a><span data-ttu-id="48d93-148">Установка максимального размера для файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="48d93-148">Set the maximum size for a file share</span></span>
<span data-ttu-id="48d93-149">Клиентская библиотека хранилища Azure версии 5.x и выше позволяет задавать квоту (или максимальный размер) в файловом ресурсе в гигабайтах.</span><span class="sxs-lookup"><span data-stu-id="48d93-149">Beginning with version 5.x of the Azure Storage Client Library, you can set set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="48d93-150">Можно также проверить, какой объем данных хранится в настоящее время в общей папке.</span><span class="sxs-lookup"><span data-stu-id="48d93-150">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="48d93-151">Задав квоту для файлового ресурса, можно ограничить общий размер файлов, хранящихся в общей папке.</span><span class="sxs-lookup"><span data-stu-id="48d93-151">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="48d93-152">Если общий размер файлов в файловом ресурсе превышает установленную квоту, клиенты не смогут увеличить размер существующих файлов или создать новые файлы, только если они не являются пустыми.</span><span class="sxs-lookup"><span data-stu-id="48d93-152">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="48d93-153">В приведенном ниже примере показано, как проверить текущее использование данных в файловом ресурсе, а также задать для него квоту.</span><span class="sxs-lookup"><span data-stu-id="48d93-153">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

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

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="48d93-154">Создание подписи общего доступа для файла или файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="48d93-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="48d93-155">Начиная с версии 5.x клиентской библиотеки хранилища Azure можно создать подпись общего доступа (SAS) для файлового ресурса или отдельного файла.</span><span class="sxs-lookup"><span data-stu-id="48d93-155">Beginning with version 5.x of the Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="48d93-156">Также можно создать политики общего доступа на файловом ресурсе, чтобы управлять подписями общего доступа.</span><span class="sxs-lookup"><span data-stu-id="48d93-156">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="48d93-157">Создание политики общего доступа рекомендуется, так как она позволяет отменить SAS, если она скомпрометирована.</span><span class="sxs-lookup"><span data-stu-id="48d93-157">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="48d93-158">В приведенном ниже примере создаются политики общего доступа в общей папке, а затем используются для обеспечения ограничения SAS для файла в общей папке.</span><span class="sxs-lookup"><span data-stu-id="48d93-158">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

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

<span data-ttu-id="48d93-159">Дополнительные сведения см. в статьях [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md) и [Подписанные URL-адреса. Часть 2: создание и использование подписанного URL-адреса в службе BLOB-объектов](storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="48d93-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="48d93-160">Копирование файлов</span><span class="sxs-lookup"><span data-stu-id="48d93-160">Copy files</span></span>
<span data-ttu-id="48d93-161">Начиная с версии 5.x клиентской библиотеки хранилища Azure можно скопировать файл в другой файл, файл в большой двоичный объект или BLOB-объект в файл.</span><span class="sxs-lookup"><span data-stu-id="48d93-161">Beginning with version 5.x of the Azure Storage Client Library, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="48d93-162">В следующих разделах демонстрируется выполнение этих операций копирования программными средствами.</span><span class="sxs-lookup"><span data-stu-id="48d93-162">In the next sections, we demonstrate how to perform these copy operations programmatically.</span></span>

<span data-ttu-id="48d93-163">AzCopy можно использовать для копирования одного файла в другой, а также копирования большого двоичного объекта в файл или наоборот.</span><span class="sxs-lookup"><span data-stu-id="48d93-163">You can also use AzCopy to copy one file to another or to copy a blob to a file or vice versa.</span></span> <span data-ttu-id="48d93-164">См. статью [Приступая к работе со служебной программой командной строки AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="48d93-164">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="48d93-165">При копировании большого двоичного объекта в файл или файла в большой двоичный объект необходимо использовать подпись общего доступа (SAS) для проверки подлинности исходного объекта, даже если копирование производится внутри одной и той же учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="48d93-165">If you are copying a blob to a file, or a file to a blob, you must use a shared access signature (SAS) to authenticate the source object, even if you are copying within the same storage account.</span></span>
> 
> 

<span data-ttu-id="48d93-166">**Скопируйте файл в другой файл**. В приведенном ниже примере файл копируется в другой файл в той же общей папке.</span><span class="sxs-lookup"><span data-stu-id="48d93-166">**Copy a file to another file** The following example copies a file to another file in the same share.</span></span> <span data-ttu-id="48d93-167">Так как эта операция копирования осуществляет копирование между файлами в одной учетной записи хранения, для выполнения копирования можно использовать проверку подлинности Shared Key.</span><span class="sxs-lookup"><span data-stu-id="48d93-167">Because this copy operation copies between files in the same storage account, you can use Shared Key authentication to perform the copy.</span></span>

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

<span data-ttu-id="48d93-168">**Скопируйте файл в большой двоичный объект**. В приведенном ниже примере файл создается и копируется в большой двоичный объект в пределах одной и той же учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="48d93-168">**Copy a file to a blob** The following example creates a file and copies it to a blob within the same storage account.</span></span> <span data-ttu-id="48d93-169">В примере для исходного файла создается SAS, которую служба использует для проверки подлинности при доступе к исходному файлу во время операции копирования.</span><span class="sxs-lookup"><span data-stu-id="48d93-169">The example creates a SAS for the source file, which the service uses to authenticate access to the source file during the copy operation.</span></span>

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

<span data-ttu-id="48d93-170">Таким же образом можно скопировать BLOB-объект в файл.</span><span class="sxs-lookup"><span data-stu-id="48d93-170">You can copy a blob to a file in the same way.</span></span> <span data-ttu-id="48d93-171">Если исходным объектом является BLOB-объект, создайте SAS для проверки подлинности доступа к BLOB-объекту во время операции копирования.</span><span class="sxs-lookup"><span data-stu-id="48d93-171">If the source object is a blob, then create a SAS to authenticate access to that blob during the copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="48d93-172">Устранение неполадок хранилища файлов Azure с помощью метрик</span><span class="sxs-lookup"><span data-stu-id="48d93-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="48d93-173">Аналитика службы хранилища Azure теперь поддерживает метрики для хранилища файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="48d93-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="48d93-174">Данные метрик позволяют отслеживать запросы и диагностировать проблемы.</span><span class="sxs-lookup"><span data-stu-id="48d93-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="48d93-175">Вы можете включить метрики для файлового хранилища Azure с помощью [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="48d93-175">You can enable metrics for Azure File storage from the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="48d93-176">Кроме того, вы можете включить метрики программным путем. Для этого используйте операцию Set File Service Properties через интерфейс REST API или любой ее аналог из имеющихся в клиентской библиотеке хранилища.</span><span class="sxs-lookup"><span data-stu-id="48d93-176">You can also enable metrics programmatically by calling the Set File Service Properties operation via the REST API, or one of its analogues in the Storage Client Library.</span></span>


<span data-ttu-id="48d93-177">В следующем примере кода показано, как использовать клиентскую библиотеку хранилища для .NET, чтобы включить метрики для хранилища файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="48d93-177">The following code example shows how to use the Storage Client Library for .NET to enable metrics for Azure File storage.</span></span>

<span data-ttu-id="48d93-178">Сначала добавьте в файл `Program.cs` следующие директивы `using` в дополнение к указанным выше.</span><span class="sxs-lookup"><span data-stu-id="48d93-178">First, add the following `using` directives to your `Program.cs` file, in addition to those you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="48d93-179">Обратите внимание, что в то время, как большие двоичные объекты, таблицы и очереди Azure используют общий тип `ServiceProperties` в пространстве имен `Microsoft.WindowsAzure.Storage.Shared.Protocol`, хранилище файлов Azure использует собственный тип `FileServiceProperties` в пространстве имен `Microsoft.WindowsAzure.Storage.File.Protocol`.</span><span class="sxs-lookup"><span data-stu-id="48d93-179">Note that while Azure Blobs, Azure Table, and Azure Queues use the shared `ServiceProperties` type in the `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, the `FileServiceProperties` type in the `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="48d93-180">Однако для обеспечения компиляции приведенного ниже кода ваш код должен ссылаться на оба этих пространства имен.</span><span class="sxs-lookup"><span data-stu-id="48d93-180">Both namespaces must be referenced from your code, however, for the following code to compile.</span></span>

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

<span data-ttu-id="48d93-181">Кроме того, вы можете найти подробное руководство по устранению неполадок в статье [Troubleshoot Azure File storage problems in Windows](storage-troubleshoot-file-connection-problems.md) (Устранение неполадок в хранилище файлов Azure).</span><span class="sxs-lookup"><span data-stu-id="48d93-181">Also, you can refer to [Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48d93-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48d93-182">Next steps</span></span>
<span data-ttu-id="48d93-183">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="48d93-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="48d93-184">Тематические статьи и видео</span><span class="sxs-lookup"><span data-stu-id="48d93-184">Conceptual articles and videos</span></span>
* <span data-ttu-id="48d93-185">[Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Хранилище файлов Azure: удобная облачная файловая система SMB для Windows и Linux)</span><span class="sxs-lookup"><span data-stu-id="48d93-185">[Azure File storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)</span></span>
* [<span data-ttu-id="48d93-186">Использование хранилища файлов Azure в Linux</span><span class="sxs-lookup"><span data-stu-id="48d93-186">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="48d93-187">Средства для работы с хранилищем файлов</span><span class="sxs-lookup"><span data-stu-id="48d93-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="48d93-188">Использование Azure PowerShell со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="48d93-188">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="48d93-189">Использование AzCopy со службой хранилища Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="48d93-189">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="48d93-190">Использование интерфейса командной строки (CLI) Azure со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="48d93-190">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="48d93-191">Устранение неполадок хранилища файлов Azure</span><span class="sxs-lookup"><span data-stu-id="48d93-191">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="48d93-192">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="48d93-192">Reference</span></span>
* [<span data-ttu-id="48d93-193">Справочник по клиентской библиотеке хранилища для .NET</span><span class="sxs-lookup"><span data-stu-id="48d93-193">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="48d93-194">Справочник по REST API службы файлов</span><span class="sxs-lookup"><span data-stu-id="48d93-194">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="48d93-195">Записи блога</span><span class="sxs-lookup"><span data-stu-id="48d93-195">Blog posts</span></span>
* [<span data-ttu-id="48d93-196">Хранилище файлов Azure стало общедоступным</span><span class="sxs-lookup"><span data-stu-id="48d93-196">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* <span data-ttu-id="48d93-197">[Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Хранилище файлов Azure: взгляд изнутри)</span><span class="sxs-lookup"><span data-stu-id="48d93-197">[Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)</span></span>
* [<span data-ttu-id="48d93-198">Введение в службы файлов Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="48d93-198">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* <span data-ttu-id="48d93-199">[Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx) (Сохраняемые подключения к файлам Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="48d93-199">[Persisting connections to Microsoft Azure File storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)</span></span>