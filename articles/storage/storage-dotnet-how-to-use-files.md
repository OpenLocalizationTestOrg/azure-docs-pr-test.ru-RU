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
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="406ba-103">Разработка для хранилища файлов Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="406ba-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="406ba-104">В этой статье показано, как toomanage хранилища Azure File с кодом .NET.</span><span class="sxs-lookup"><span data-stu-id="406ba-104">This article shows how toomanage Azure File storage with .NET code.</span></span> <span data-ttu-id="406ba-105">toolearn Дополнительные сведения о хранилище файлов Azure см. в разделе hello [tooAzure введение хранения файлов](storage-files-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="406ba-105">toolearn more about Azure File storage, please see hello [Introduction tooAzure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="406ba-106">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="406ba-106">About this tutorial</span></span>
<span data-ttu-id="406ba-107">Этот учебник продемонстрируют hello основные принципы использования toodevelop приложения или службы .NET, использующих данные файла toostore хранилище файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="406ba-107">This tutorial will demonstrate hello basics of using .NET toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="406ba-108">В этом учебнике мы создайте простое консольное приложение и Показать как tooperform базовые действия с хранилищем .NET и файлов Azure:</span><span class="sxs-lookup"><span data-stu-id="406ba-108">In this tutorial, we will create a simple console application and show how tooperform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="406ba-109">Получение содержимого файла hello</span><span class="sxs-lookup"><span data-stu-id="406ba-109">Get hello contents of a file</span></span>
* <span data-ttu-id="406ba-110">Задать квоты hello (максимальный размер) для общей папки hello.</span><span class="sxs-lookup"><span data-stu-id="406ba-110">Set hello quota (maximum size) for hello file share.</span></span>
* <span data-ttu-id="406ba-111">Создание подписанного URL-адреса (ключ SAS) для файла, который использует политику общего доступа, определенные в общей папке hello.</span><span class="sxs-lookup"><span data-stu-id="406ba-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>
* <span data-ttu-id="406ba-112">Скопируйте файл tooanother в hello учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="406ba-112">Copy a file tooanother file in hello same storage account.</span></span>
* <span data-ttu-id="406ba-113">Копирование большого двоичного объекта файла tooa в hello учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="406ba-113">Copy a file tooa blob in hello same storage account.</span></span>
* <span data-ttu-id="406ba-114">Используйте метрики службы хранилища Azure как средство устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="406ba-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="406ba-115">Поскольку хранилище файлов Azure может осуществляться по протоколу SMB, вполне возможно toowrite простых приложений, получающих доступ к папке файлов Azure hello, с помощью стандартных классов System.IO hello для файлового ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="406ba-115">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard System.IO classes for File I/O.</span></span> <span data-ttu-id="406ba-116">В этой статье описывается, как toowrite приложения, использующие hello пакет SDK .NET хранилища Azure, которая использует hello [хранилища Azure File API-интерфейса REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure хранилища файлов.</span><span class="sxs-lookup"><span data-stu-id="406ba-116">This article will describe how toowrite applications that use hello Azure Storage .NET SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span> 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a><span data-ttu-id="406ba-117">Создайте консольное приложение hello и получить сборку hello</span><span class="sxs-lookup"><span data-stu-id="406ba-117">Create hello console application and obtain hello assembly</span></span>
<span data-ttu-id="406ba-118">В Visual Studio создайте новое консольное приложение Windows.</span><span class="sxs-lookup"><span data-stu-id="406ba-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="406ba-119">следующие шаги Hello Показать чем toocreate консольное приложение в Visual Studio 2017 г., однако hello действия схожи в других версиях Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="406ba-119">hello following steps show you how toocreate a console application in Visual Studio 2017, however, hello steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="406ba-120">Выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="406ba-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="406ba-121">Выберите **Установлено** > **Шаблоны** > **Visual C#** > **Классический рабочий стол Windows**.</span><span class="sxs-lookup"><span data-stu-id="406ba-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="406ba-122">Выберите **Консольное приложение (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="406ba-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="406ba-123">Введите имя для вашего приложения в hello **имя:** поля</span><span class="sxs-lookup"><span data-stu-id="406ba-123">Enter a name for your application in hello **Name:** field</span></span>
5. <span data-ttu-id="406ba-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="406ba-124">Select **OK**</span></span>

<span data-ttu-id="406ba-125">Все примеры кода в этом учебнике можно добавить toohello `Main()` метода приложения командной `Program.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="406ba-125">All code examples in this tutorial can be added toohello `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="406ba-126">Hello клиентская библиотека хранилища Azure можно использовать в любом приложении .NET, включая Azure облачной службы или веб-приложение и приложений для настольных компьютеров и мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="406ba-126">You can use hello Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="406ba-127">Для упрощения в этом руководстве мы будем использовать консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="406ba-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-tooinstall-hello-required-packages"></a><span data-ttu-id="406ba-128">Использовать hello необходимые пакеты NuGet tooinstall</span><span class="sxs-lookup"><span data-stu-id="406ba-128">Use NuGet tooinstall hello required packages</span></span>
<span data-ttu-id="406ba-129">Существует два пакета, необходимо использовать tooreference в ваш проект toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="406ba-129">There are two packages you need tooreference in your project toocomplete this tutorial:</span></span>

* <span data-ttu-id="406ba-130">[Клиентская библиотека хранилища Microsoft Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): данный пакет обеспечивает программный доступ toodata ресурсы в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="406ba-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access toodata resources in your storage account.</span></span>
* <span data-ttu-id="406ba-131">[Библиотека Microsoft Azure Configuration Manager для .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) — этот пакет предоставляет класс для анализа строки подключения в файле конфигурации независимо от среды выполнения приложения.</span><span class="sxs-lookup"><span data-stu-id="406ba-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="406ba-132">Можно использовать оба пакета NuGet tooobtain.</span><span class="sxs-lookup"><span data-stu-id="406ba-132">You can use NuGet tooobtain both packages.</span></span> <span data-ttu-id="406ba-133">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="406ba-133">Follow these steps:</span></span>

1. <span data-ttu-id="406ba-134">Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="406ba-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="406ba-135">Найдите в Интернете «WindowsAzure.Storage» и нажмите кнопку **установить** tooinstall hello клиентской библиотеки хранилища и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="406ba-135">Search online for "WindowsAzure.Storage" and click **Install** tooinstall hello Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="406ba-136">Найдите в Интернете «WindowsAzure.ConfigurationManager» и нажмите кнопку **установить** tooinstall hello Azure Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="406ba-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** tooinstall hello Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a><span data-ttu-id="406ba-137">Сохраните файл app.config toohello учетные данные учетной записи хранилища</span><span class="sxs-lookup"><span data-stu-id="406ba-137">Save your storage account credentials toohello app.config file</span></span>
<span data-ttu-id="406ba-138">Затем сохраните данные учетной записи хранения в файле app.config вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="406ba-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="406ba-139">Изменить файл app.config hello, чтобы он отображался как toohello следующий пример, заменив `myaccount` имя вашей учетной записи хранилища и `mykey` с помощью ключа учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="406ba-139">Edit hello app.config file so that it appears similar toohello following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> Последняя версия эмулятора хранилища Azure hello Hello не поддерживает хранилище файлов Azure. <span data-ttu-id="406ba-141">Учетная запись хранения Azure в облаке toowork hello с хранилищем файлов Azure должны предназначаться для строки подключения.</span><span class="sxs-lookup"><span data-stu-id="406ba-141">Your connection string must target an Azure Storage Account in hello cloud toowork with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="406ba-142">Добавление директив using</span><span class="sxs-lookup"><span data-stu-id="406ba-142">Add using directives</span></span>
<span data-ttu-id="406ba-143">Откройте hello `Program.cs` файл из обозревателя решений и добавьте следующее hello с помощью директивы toohello вверху файла hello.</span><span class="sxs-lookup"><span data-stu-id="406ba-143">Open hello `Program.cs` file from Solution Explorer, and add hello following using directives toohello top of hello file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a><span data-ttu-id="406ba-144">Доступ hello общая папка программным способом</span><span class="sxs-lookup"><span data-stu-id="406ba-144">Access hello file share programmatically</span></span>
<span data-ttu-id="406ba-145">Добавьте следующий код toohello hello `Main()` строка подключения hello tooretrieve метод (после приведенного выше кода hello).</span><span class="sxs-lookup"><span data-stu-id="406ba-145">Next, add hello following code toohello `Main()` method (after hello code shown above) tooretrieve hello connection string.</span></span> <span data-ttu-id="406ba-146">Этот код возвращает файла toohello ссылок, созданную ранее и выводит в окно консоли toohello его содержимое.</span><span class="sxs-lookup"><span data-stu-id="406ba-146">This code gets a reference toohello file we created earlier and outputs its contents toohello console window.</span></span>

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

<span data-ttu-id="406ba-147">Запустите выходных данных hello toosee hello консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="406ba-147">Run hello console application toosee hello output.</span></span>

## <a name="set-hello-maximum-size-for-a-file-share"></a><span data-ttu-id="406ba-148">Установить максимальный размер hello для общей папки</span><span class="sxs-lookup"><span data-stu-id="406ba-148">Set hello maximum size for a file share</span></span>
<span data-ttu-id="406ba-149">Начиная с версии 5.x hello клиентская библиотека хранилища Azure, можно задать набор hello квоты (или максимальный размер) для общей папки в гигабайтах.</span><span class="sxs-lookup"><span data-stu-id="406ba-149">Beginning with version 5.x of hello Azure Storage Client Library, you can set set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="406ba-150">Можно также проверить, какой объем данных в настоящее время хранится в папке hello toosee.</span><span class="sxs-lookup"><span data-stu-id="406ba-150">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="406ba-151">В параметр квоты hello для общей папки можно ограничить общий размер hello hello файлы, хранящиеся в папке hello.</span><span class="sxs-lookup"><span data-stu-id="406ba-151">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="406ba-152">Если общий размер файлов в общей папке hello hello превышает квоту hello задать для общей папки hello, а затем клиентов будет невозможно tooincrease hello размера существующих файлов или создания новых файлов, если эти файлы являются пустыми.</span><span class="sxs-lookup"><span data-stu-id="406ba-152">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="406ba-153">Hello приведенном ниже примере показано, как toocheck hello текущего использования для общей папки и как tooset hello квоты для общей папки hello.</span><span class="sxs-lookup"><span data-stu-id="406ba-153">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

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

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="406ba-154">Создание подписи общего доступа для файла или файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="406ba-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="406ba-155">Начиная с версии 5.x Здравствуйте клиентская библиотека хранилища Azure, можно создать подпись коллективного доступа (SAS) для общей папки или отдельного файла.</span><span class="sxs-lookup"><span data-stu-id="406ba-155">Beginning with version 5.x of hello Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="406ba-156">Можно также создать политики общего доступа на общих toomanage общий доступ к файлам подписи.</span><span class="sxs-lookup"><span data-stu-id="406ba-156">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="406ba-157">Создание политики общего доступа рекомендуется, так как она предоставляет средства отзыва hello SAS, если он должен быть скомпрометирован.</span><span class="sxs-lookup"><span data-stu-id="406ba-157">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="406ba-158">Следующий пример Hello создает политику общего доступа в общей папке, а затем использует ограничения hello tooprovide политика для SAS для файла в hello совместного использования.</span><span class="sxs-lookup"><span data-stu-id="406ba-158">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

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

<span data-ttu-id="406ba-159">Дополнительные сведения см. в статьях [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md) и [Подписанные URL-адреса. Часть 2: создание и использование подписанного URL-адреса в службе BLOB-объектов](storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="406ba-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="406ba-160">Копирование файлов</span><span class="sxs-lookup"><span data-stu-id="406ba-160">Copy files</span></span>
<span data-ttu-id="406ba-161">Начиная с версии 5.x hello клиентская библиотека хранилища Azure, можно скопировать файл tooanother, большой двоичный объект файла tooa или tooa файла большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="406ba-161">Beginning with version 5.x of hello Azure Storage Client Library, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="406ba-162">В следующих разделах hello показывается как tooperform их копирование операций программными средствами.</span><span class="sxs-lookup"><span data-stu-id="406ba-162">In hello next sections, we demonstrate how tooperform these copy operations programmatically.</span></span>

<span data-ttu-id="406ba-163">Также можно использовать один файл tooanother AzCopy toocopy или toocopy большого двоичного объекта tooa файла, и наоборот.</span><span class="sxs-lookup"><span data-stu-id="406ba-163">You can also use AzCopy toocopy one file tooanother or toocopy a blob tooa file or vice versa.</span></span> <span data-ttu-id="406ba-164">В разделе [перенесите данные с помощью служебной программы командной строки AzCopy hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="406ba-164">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="406ba-165">При копировании файла tooa большого двоичного объекта или большой двоичный объект tooa файла необходимо использовать общего доступа (SAS) tooauthenticate hello исходного объекта сигнатуры, даже если копирование производится внутри hello же учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="406ba-165">If you are copying a blob tooa file, or a file tooa blob, you must use a shared access signature (SAS) tooauthenticate hello source object, even if you are copying within hello same storage account.</span></span>
> 
> 

<span data-ttu-id="406ba-166">**Скопируйте файл tooanother** hello следующий пример копирует файл tooanother в hello одной общей папке.</span><span class="sxs-lookup"><span data-stu-id="406ba-166">**Copy a file tooanother file** hello following example copies a file tooanother file in hello same share.</span></span> <span data-ttu-id="406ba-167">Так как эта операция копирования копирует между Здравствуйте, файлы в учетную запись хранения, можно использовать копию hello tooperform проверки подлинности Shared Key.</span><span class="sxs-lookup"><span data-stu-id="406ba-167">Because this copy operation copies between files in hello same storage account, you can use Shared Key authentication tooperform hello copy.</span></span>

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

<span data-ttu-id="406ba-168">**Копирование большого двоичного объекта файла tooa** hello следующий пример создает файл и копирует его tooa BLOB-объектов в пределах hello учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="406ba-168">**Copy a file tooa blob** hello following example creates a file and copies it tooa blob within hello same storage account.</span></span> <span data-ttu-id="406ba-169">пример Hello создает SAS для hello исходного файла, службу hello, которая использует tooauthenticate доступа toohello исходный файл во время операции копирования hello.</span><span class="sxs-lookup"><span data-stu-id="406ba-169">hello example creates a SAS for hello source file, which hello service uses tooauthenticate access toohello source file during hello copy operation.</span></span>

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

<span data-ttu-id="406ba-170">Можно скопировать tooa файла большого двоичного объекта в hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="406ba-170">You can copy a blob tooa file in hello same way.</span></span> <span data-ttu-id="406ba-171">Если hello объекта источника является большой двоичный объект, необходимо создайте большой двоичный объект toothat SAS tooauthenticate доступ во время операции копирования hello.</span><span class="sxs-lookup"><span data-stu-id="406ba-171">If hello source object is a blob, then create a SAS tooauthenticate access toothat blob during hello copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="406ba-172">Устранение неполадок хранилища файлов Azure с помощью метрик</span><span class="sxs-lookup"><span data-stu-id="406ba-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="406ba-173">Аналитика службы хранилища Azure теперь поддерживает метрики для хранилища файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="406ba-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="406ba-174">Данные метрик позволяют отслеживать запросы и диагностировать проблемы.</span><span class="sxs-lookup"><span data-stu-id="406ba-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="406ba-175">Можно включить метрики для хранилища Azure File с hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="406ba-175">You can enable metrics for Azure File storage from hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="406ba-176">Можно также включить метрики программным образом с вызывающему Привет операции установки свойств службы файлов с помощью API-интерфейса REST hello, или один из его аналоги в hello клиентской библиотеки хранилища.</span><span class="sxs-lookup"><span data-stu-id="406ba-176">You can also enable metrics programmatically by calling hello Set File Service Properties operation via hello REST API, or one of its analogues in hello Storage Client Library.</span></span>


<span data-ttu-id="406ba-177">Hello в следующем примере кода показано, как toouse hello клиентской библиотеки хранилища для .NET tooenable метрики для хранения файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="406ba-177">hello following code example shows how toouse hello Storage Client Library for .NET tooenable metrics for Azure File storage.</span></span>

<span data-ttu-id="406ba-178">Во-первых, добавьте следующее hello `using` tooyour директивы `Program.cs` файлов, кроме toothose добавленных выше:</span><span class="sxs-lookup"><span data-stu-id="406ba-178">First, add hello following `using` directives tooyour `Program.cs` file, in addition toothose you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="406ba-179">Обратите внимание, что при больших двоичных объектов Azure, таблицы Azure и очереди Azure hello совместно использовать `ServiceProperties` типа в hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` имен хранилища Azure File использует собственный тип hello `FileServiceProperties` типа в hello `Microsoft.WindowsAzure.Storage.File.Protocol` пространства имен.</span><span class="sxs-lookup"><span data-stu-id="406ba-179">Note that while Azure Blobs, Azure Table, and Azure Queues use hello shared `ServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, hello `FileServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="406ba-180">Оба пространства имен должен ссылаться в коде, однако для следующих toocompile кода hello.</span><span class="sxs-lookup"><span data-stu-id="406ba-180">Both namespaces must be referenced from your code, however, for hello following code toocompile.</span></span>

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

<span data-ttu-id="406ba-181">Кроме того, можно ссылаться слишком[хранилища Azure File статьи по устранению неполадок](storage-troubleshoot-file-connection-problems.md) для начала до конца рекомендации по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="406ba-181">Also, you can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="406ba-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="406ba-182">Next steps</span></span>
<span data-ttu-id="406ba-183">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="406ba-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="406ba-184">Тематические статьи и видео</span><span class="sxs-lookup"><span data-stu-id="406ba-184">Conceptual articles and videos</span></span>
* <span data-ttu-id="406ba-185">[Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Хранилище файлов Azure: удобная облачная файловая система SMB для Windows и Linux)</span><span class="sxs-lookup"><span data-stu-id="406ba-185">[Azure File storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)</span></span>
* [<span data-ttu-id="406ba-186">Как toouse хранилища Azure File с Linux</span><span class="sxs-lookup"><span data-stu-id="406ba-186">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="406ba-187">Средства для работы с хранилищем файлов</span><span class="sxs-lookup"><span data-stu-id="406ba-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="406ba-188">Использование Azure PowerShell со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="406ba-188">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="406ba-189">Как toouse AzCopy с хранилищем Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="406ba-189">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="406ba-190">С помощью hello Azure CLI со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="406ba-190">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="406ba-191">Устранение неполадок хранилища файлов Azure</span><span class="sxs-lookup"><span data-stu-id="406ba-191">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="406ba-192">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="406ba-192">Reference</span></span>
* [<span data-ttu-id="406ba-193">Справочник по клиентской библиотеке хранилища для .NET</span><span class="sxs-lookup"><span data-stu-id="406ba-193">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="406ba-194">Справочник по REST API службы файлов</span><span class="sxs-lookup"><span data-stu-id="406ba-194">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="406ba-195">Записи блога</span><span class="sxs-lookup"><span data-stu-id="406ba-195">Blog posts</span></span>
* [<span data-ttu-id="406ba-196">Хранилище файлов Azure стало общедоступным</span><span class="sxs-lookup"><span data-stu-id="406ba-196">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* <span data-ttu-id="406ba-197">[Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Хранилище файлов Azure: взгляд изнутри)</span><span class="sxs-lookup"><span data-stu-id="406ba-197">[Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)</span></span>
* [<span data-ttu-id="406ba-198">Введение в службы файлов Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="406ba-198">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="406ba-199">Сохранение соединений tooMicrosoft хранилища Azure File</span><span class="sxs-lookup"><span data-stu-id="406ba-199">Persisting connections tooMicrosoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
