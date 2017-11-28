---
title: "Использование хранилища BLOB-объектов (хранилища объектов) из C++ | Документация Майкрософт"
description: "Хранение неструктурированных данных в облаке в хранилище BLOB-объектов Azure."
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: daf480b7be78dc001712010eac6386d4744c3c1d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-c"></a><span data-ttu-id="67e5e-103">Использование хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="67e5e-103">How to use Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="67e5e-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="67e5e-104">Overview</span></span>
<span data-ttu-id="67e5e-105">Хранилище BLOB-объектов Azure — это служба, которая хранит неструктурированные данные в облаке в качестве объектов или больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="67e5e-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="67e5e-106">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="67e5e-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="67e5e-107">Хранилище BLOB-объектов иногда также называют хранилищем объектов.</span><span class="sxs-lookup"><span data-stu-id="67e5e-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="67e5e-108">В этом руководстве показано, как реализовать типичные сценарии с использованием службы хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="67e5e-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span></span> <span data-ttu-id="67e5e-109">Примеры написаны на C++ и используют [клиентскую библиотеку хранилища Azure для C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="67e5e-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="67e5e-110">Здесь описаны такие сценарии, как **отправка**, **перечисление**, **скачивание** и **удаление** BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="67e5e-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="67e5e-111">Данное руководство предназначено для клиентской библиотеки хранилища Azure для С++ версии 1.0.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="67e5e-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="67e5e-112">Рекомендуемая версия клиентской библиотеки хранилища — 2.2.0. Она доступна на сайте [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="67e5e-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="67e5e-113">Создание приложения на C++</span><span class="sxs-lookup"><span data-stu-id="67e5e-113">Create a C++ application</span></span>
<span data-ttu-id="67e5e-114">В этом руководстве будут использоваться компоненты хранилища, которые могут выполняться в приложениях C++.</span><span class="sxs-lookup"><span data-stu-id="67e5e-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="67e5e-115">Для этого необходимо установить клиентскую библиотеку хранилища Azure для C++ и создать учетную запись хранения Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="67e5e-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="67e5e-116">Чтобы установить клиентскую библиотеку хранилища для C++, можно использовать следующие методы.</span><span class="sxs-lookup"><span data-stu-id="67e5e-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="67e5e-117">**Linux:** следуйте инструкциям, указанным в файле README [клиентской библиотеки хранилища Azure для C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="67e5e-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="67e5e-118">**Windows:** в Visual Studio нажмите **Инструменты > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="67e5e-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="67e5e-119">Введите следующую команду в [консоли диспетчера пакетов NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="67e5e-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="67e5e-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="67e5e-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="67e5e-121">Настройка приложения для доступа к хранилищу BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="67e5e-121">Configure your application to access Blob Storage</span></span>
<span data-ttu-id="67e5e-122">Добавьте следующие инструкции в начало файла C++, где требуется использовать API-интерфейсы Azure для доступа к BLOB-объектам.</span><span class="sxs-lookup"><span data-stu-id="67e5e-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="67e5e-123">Настройка строки подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="67e5e-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="67e5e-124">Клиент хранилища Azure использует строку подключения с целью хранения конечных точек и учетных данных для доступа к службам управления данными.</span><span class="sxs-lookup"><span data-stu-id="67e5e-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="67e5e-125">При запуске в клиентском приложении необходимо указать строку подключения для хранилища в следующем формате (в качестве параметров *AccountName* и *AccountKey* укажите имя и ключ доступа своей учетной записи хранения, их можно получить на [портале Azure](https://portal.azure.com)).</span><span class="sxs-lookup"><span data-stu-id="67e5e-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="67e5e-126">Сведения об учетных записях хранения и ключах доступа см. в статье[Об учетных записях хранения Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67e5e-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="67e5e-127">В этом примере показано, как объявить статическое поле для размещения строки подключения:</span><span class="sxs-lookup"><span data-stu-id="67e5e-127">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="67e5e-128">Чтобы протестировать приложение на локальном компьютере Windows, можно использовать [эмулятор хранения](../storage-use-emulator.md) Microsoft Azure, установленный вместе с [пакетом SDK Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="67e5e-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="67e5e-129">Эмулятор хранения — это программа, моделирующая службы больших двоичных объектов, очередей и таблиц, доступных в Azure на локальном компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="67e5e-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="67e5e-130">В следующем примере показано, как объявить статическое поле для размещения строки подключения для эмулятора локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="67e5e-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="67e5e-131">Чтобы запустить эмулятор хранения Azure, нажмите кнопку **Пуск** или клавишу **Windows**.</span><span class="sxs-lookup"><span data-stu-id="67e5e-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="67e5e-132">Начните набирать **эмулятор хранения Azure** и выберите **эмулятор хранения Microsoft Azure** из списка приложений.</span><span class="sxs-lookup"><span data-stu-id="67e5e-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="67e5e-133">В приведенных ниже примерах предполагается, что вы использовали одно из этих двух определений для получения строки подключения к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="67e5e-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="67e5e-134">Получить строку подключения</span><span class="sxs-lookup"><span data-stu-id="67e5e-134">Retrieve your connection string</span></span>
<span data-ttu-id="67e5e-135">Информацию о своей учетной записи хранения можно представить с помощью класса **cloud_storage_account**.</span><span class="sxs-lookup"><span data-stu-id="67e5e-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="67e5e-136">Чтобы получить данные учетной записи хранения из строки подключения хранилища, можно использовать метод **синтаксического анализа** .</span><span class="sxs-lookup"><span data-stu-id="67e5e-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="67e5e-137">Затем получите ссылку на класс **cloud_blob_client**, позволяющий извлекать объекты, представляющие контейнеры и BLOB-объекты, которые хранятся в службе хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="67e5e-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span></span> <span data-ttu-id="67e5e-138">Следующий код создает объект **cloud_blob_client** с помощью объекта учетной записи хранения, полученной выше:</span><span class="sxs-lookup"><span data-stu-id="67e5e-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span></span>  

```cpp
// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="67e5e-139">Практическое руководство. Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="67e5e-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="67e5e-140">В этом примере показано, как создать контейнер:</span><span class="sxs-lookup"><span data-stu-id="67e5e-140">This example shows how to create a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create the blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference to a container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create the container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="67e5e-141">По умолчанию новый контейнер закрытый, и вам необходимо указать ключ доступа к хранилищу, чтобы загрузить BLOB-объекты из этого контейнера.</span><span class="sxs-lookup"><span data-stu-id="67e5e-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="67e5e-142">Чтобы сделать файлы (BLOB) в этом контейнере доступными для всех пользователей, сделайте контейнер открытым, используя следующий код.</span><span class="sxs-lookup"><span data-stu-id="67e5e-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span></span>  

```cpp
// Make the blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="67e5e-143">Любой пользователь в Интернете может видеть большие двоичные объекты в открытом контейнере, но изменить или удалить их можно только при наличии ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="67e5e-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="67e5e-144">Практическое руководство. Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="67e5e-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="67e5e-145">Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="67e5e-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="67e5e-146">В большинстве случаев рекомендуется использовать блочные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="67e5e-146">In the majority of cases, block blob is the recommended type to use.</span></span>  

<span data-ttu-id="67e5e-147">Для передачи файла в блочный BLOB-объект получите ссылку на контейнер и используйте ее для получения ссылки на блочный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="67e5e-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="67e5e-148">Получив ссылку на BLOB-объект, можно отправить любой поток данных в этот объект с помощью метода **upload_from_stream**.</span><span class="sxs-lookup"><span data-stu-id="67e5e-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span></span> <span data-ttu-id="67e5e-149">Эта операция создает большой двоичный объект, если он не существует, или заменяет его, если он существует.</span><span class="sxs-lookup"><span data-stu-id="67e5e-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="67e5e-150">В следующем примере показано, как отправить BLOB-объект в контейнер. Предполагается, что контейнер уже был создан.</span><span class="sxs-lookup"><span data-stu-id="67e5e-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite the "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite the "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference to a blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="67e5e-151">Кроме того, можно использовать метод **upload_from_file** для отправки файла в блочный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="67e5e-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span></span>

## <a name="how-to-list-the-blobs-in-a-container"></a><span data-ttu-id="67e5e-152">Практическое руководство. Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="67e5e-152">How to: List the blobs in a container</span></span>
<span data-ttu-id="67e5e-153">Для перечисления BLOB-объектов в контейнере сначала необходимо получить ссылку на контейнер.</span><span class="sxs-lookup"><span data-stu-id="67e5e-153">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="67e5e-154">Затем вы можете использовать метод контейнера **list_blobs** для получения BLOB-объектов или их каталогов.</span><span class="sxs-lookup"><span data-stu-id="67e5e-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="67e5e-155">Для доступа к широкому набору свойств и методов возвращаемого объекта **list_blob_item** необходимо вызвать метод **list_blob_item.as_blob**, чтобы получить объект **cloud_blob**, или метод **list_blob.as_directory**, чтобы получить объект cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="67e5e-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span></span> <span data-ttu-id="67e5e-156">В следующем коде показано, как получить и вывести URI каждого элемента в контейнере **my-sample-container** .</span><span class="sxs-lookup"><span data-stu-id="67e5e-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

<span data-ttu-id="67e5e-157">Дополнительные сведения об операциях перечисления см. в разделе [Перечисление ресурсов хранилища Azure в C++](../storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="67e5e-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="67e5e-158">Практическое руководство. Загрузка BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="67e5e-158">How to: Download blobs</span></span>
<span data-ttu-id="67e5e-159">Для загрузки BLOB-объектов сначала нужно получить ссылку на BLOB-объект и затем вызвать метод **download_to_stream**.</span><span class="sxs-lookup"><span data-stu-id="67e5e-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span></span> <span data-ttu-id="67e5e-160">В следующем примере используется метод **download_to_stream** для переноса содержимого BLOB-объекта в объект потока, который затем можно сохранить в локальном файле.</span><span class="sxs-lookup"><span data-stu-id="67e5e-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents to a file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="67e5e-161">Кроме того, можно использовать метод **download_to_file**, чтобы загрузить содержимое BLOB-объекта в файл.</span><span class="sxs-lookup"><span data-stu-id="67e5e-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span></span>
<span data-ttu-id="67e5e-162">Также можно использовать метод **download_text**, чтобы загрузить содержимое BLOB-объекта в виде текстовой строки.</span><span class="sxs-lookup"><span data-stu-id="67e5e-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download the contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="67e5e-163">Практическое руководство. Удаление BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="67e5e-163">How to: Delete blobs</span></span>
<span data-ttu-id="67e5e-164">Чтобы удалить BLOB-объект, сначала нужно получить ссылку на него, а затем вызвать для него метод **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="67e5e-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete the blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="67e5e-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="67e5e-165">Next steps</span></span>
<span data-ttu-id="67e5e-166">Теперь, когда вы ознакомились с основными сведениями о хранилище BLOB-объектов, используйте следующие ссылки для получения дополнительных сведений о хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="67e5e-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span></span>  

* [<span data-ttu-id="67e5e-167">Использование хранилища очередей из C++</span><span class="sxs-lookup"><span data-stu-id="67e5e-167">How to use Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="67e5e-168">Использование табличного хранилища из C++</span><span class="sxs-lookup"><span data-stu-id="67e5e-168">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="67e5e-169">Перечисление ресурсов хранилища Azure в C++</span><span class="sxs-lookup"><span data-stu-id="67e5e-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="67e5e-170">Справочник по клиентской библиотеке хранилища для C++</span><span class="sxs-lookup"><span data-stu-id="67e5e-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="67e5e-171">Документация по хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="67e5e-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="67e5e-172">Приступая к работе со служебной программой командной строки AzCopy</span><span class="sxs-lookup"><span data-stu-id="67e5e-172">Transfer data with the AzCopy command-line utility</span></span>](../storage-use-azcopy.md)

