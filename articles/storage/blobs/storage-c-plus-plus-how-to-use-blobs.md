---
title: "хранилище больших двоичных объектов toouse aaaHow (объект хранилища) из C++ | Документы Microsoft"
description: "Храните неструктурированные данные в облаке hello с хранилищем больших двоичных объектов Azure (хранилище объектов)."
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
ms.openlocfilehash: e63df4683e5c10c9f8fbe4106c655df61be0e1a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a><span data-ttu-id="9928c-103">Как toouse хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="9928c-103">How toouse Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="9928c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9928c-104">Overview</span></span>
<span data-ttu-id="9928c-105">Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты.</span><span class="sxs-lookup"><span data-stu-id="9928c-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="9928c-106">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="9928c-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="9928c-107">Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="9928c-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="9928c-108">В этом руководстве показано, как с помощью распространенных сценариев tooperform hello службы хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="9928c-108">This guide will demonstrate how tooperform common scenarios using hello Azure Blob storage service.</span></span> <span data-ttu-id="9928c-109">Примеры Hello на языке C++ и использовать hello [клиентская библиотека хранилища Azure для C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="9928c-109">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="9928c-110">Hello сценарии включают **передачи**, **вывод**, **Загрузка**, и **удаление** больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="9928c-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="9928c-111">Это руководство по цели hello клиентская библиотека хранилища Azure для C++ версии 1.0.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="9928c-111">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="9928c-112">Hello рекомендуемое версии клиентской библиотеки хранилища 2.2.0, которая доступна через [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="9928c-112">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="9928c-113">Создание приложения на C++</span><span class="sxs-lookup"><span data-stu-id="9928c-113">Create a C++ application</span></span>
<span data-ttu-id="9928c-114">В этом руководстве будут использоваться компоненты хранилища, которые могут выполняться в приложениях C++.</span><span class="sxs-lookup"><span data-stu-id="9928c-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="9928c-115">toodo таким образом, вам потребуется tooinstall hello клиентская библиотека хранилища Azure для C++ и создать учетную запись хранилища Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="9928c-115">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="9928c-116">hello tooinstall клиентская библиотека хранилища Azure для C++, можно использовать следующие методы hello:</span><span class="sxs-lookup"><span data-stu-id="9928c-116">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="9928c-117">**Linux —** выполните hello инструкциями, приведенными в hello [клиентская библиотека хранилища Azure для C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) страницы.</span><span class="sxs-lookup"><span data-stu-id="9928c-117">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="9928c-118">**Windows:** в Visual Studio нажмите **Инструменты > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="9928c-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="9928c-119">Команда hello введите следующее в hello [консоль диспетчера пакетов NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="9928c-119">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="9928c-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="9928c-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="9928c-121">Настройка вашего приложения tooaccess хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="9928c-121">Configure your application tooaccess Blob Storage</span></span>
<span data-ttu-id="9928c-122">Добавьте следующие hello включать инструкции toohello вверху файла C++ hello место toouse hello Azure API-интерфейсы tooaccess BLOB-объектов хранилища:</span><span class="sxs-lookup"><span data-stu-id="9928c-122">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="9928c-123">Настройка строки подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="9928c-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="9928c-124">Клиент хранилища Azure использует хранилища конечные точки toostore соединения строки и учетные данные для доступа к службам данных управления.</span><span class="sxs-lookup"><span data-stu-id="9928c-124">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="9928c-125">При работе в клиентском приложении, необходимо указать строку соединения хранения hello в hello следующая формата, с помощью hello имя учетной записи и hello хранилища ключи доступа к хранилищу для учетной записи хранения hello, перечисленные в hello [портала Azure](https://portal.azure.com)для hello *AccountName* и *AccountKey* значения.</span><span class="sxs-lookup"><span data-stu-id="9928c-125">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="9928c-126">Сведения об учетных записях хранения и ключах доступа см. в статье[Об учетных записях хранения Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9928c-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="9928c-127">В этом примере показано, как объявить строки подключения hello toohold статического поля:</span><span class="sxs-lookup"><span data-stu-id="9928c-127">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="9928c-128">tootest приложения на локальном компьютере Windows, можно использовать hello Microsoft Azure [эмулятор хранилища](../storage-use-emulator.md) , установленная с hello [пакета Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9928c-128">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="9928c-129">Эмулятор хранилища Hello — это программа, которая имитирует hello больших двоичных объектов, очередей и таблиц служб, доступных в Azure на локальном компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="9928c-129">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="9928c-130">Hello следующем примере показано, как объявить статическое поле toohold hello соединения строки tooyour эмулятора локального хранилища:</span><span class="sxs-lookup"><span data-stu-id="9928c-130">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="9928c-131">Эмулятор хранилища Azure hello toostart, выберите hello **запустить** или клавишу hello **Windows** ключа.</span><span class="sxs-lookup"><span data-stu-id="9928c-131">toostart hello Azure storage emulator, Select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="9928c-132">Начните вводить **эмулятор хранилища Azure**и выберите **эмулятор хранилища Microsoft Azure** hello списке приложений.</span><span class="sxs-lookup"><span data-stu-id="9928c-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="9928c-133">Hello следующие образцы предполагается, что используется один из этих двух методов tooget hello строки подключения к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="9928c-133">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="9928c-134">Получить строку подключения</span><span class="sxs-lookup"><span data-stu-id="9928c-134">Retrieve your connection string</span></span>
<span data-ttu-id="9928c-135">Можно использовать hello **cloud_storage_account** класса toorepresent сведений учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="9928c-135">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="9928c-136">tooretrieve данные из строки подключения к хранилищу hello учетной записи хранилища, вы можете использовать hello **проанализировать** метод.</span><span class="sxs-lookup"><span data-stu-id="9928c-136">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="9928c-137">Затем следует получить tooa ссылку **cloud_blob_client** класса позволяет tooretrieve объектов, представляющих контейнеры и большие двоичные объекты, хранящиеся в hello службы хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="9928c-137">Next, get a reference tooa **cloud_blob_client** class as it allows you tooretrieve objects that represent containers and blobs stored within hello Blob Storage Service.</span></span> <span data-ttu-id="9928c-138">Hello следующий код создает **cloud_blob_client** объекта с помощью объекта учетной записи хранилища hello, мы получить выше:</span><span class="sxs-lookup"><span data-stu-id="9928c-138">hello following code creates a **cloud_blob_client** object using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="9928c-139">Практическое руководство. Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="9928c-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="9928c-140">В этом примере показано, как toocreate контейнера, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="9928c-140">This example shows how toocreate a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="9928c-141">По умолчанию hello новый контейнер является закрытым и необходимо указать хранилища доступа ключа toodownload BLOB-объектов из этого контейнера.</span><span class="sxs-lookup"><span data-stu-id="9928c-141">By default, hello new container is private and you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="9928c-142">Следует toomake hello файлов больших двоичных объектов в пределах доступных tooeveryone hello контейнера можно задать toobe контейнера hello общим с помощью hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="9928c-142">If you want toomake hello files (blobs) within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="9928c-143">Всем пользователям в Интернете hello можно увидеть в открытый контейнер BLOB-объектов, но можно изменить или удалить их только в том случае, если у вас есть ключ hello соответствующие права доступа.</span><span class="sxs-lookup"><span data-stu-id="9928c-143">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="9928c-144">Практическое руководство. Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="9928c-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="9928c-145">Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="9928c-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="9928c-146">В большинстве случаев hello блочного BLOB-объекта — hello, рекомендуется toouse типа.</span><span class="sxs-lookup"><span data-stu-id="9928c-146">In hello majority of cases, block blob is hello recommended type toouse.</span></span>  

<span data-ttu-id="9928c-147">большой двоичный объект блока файла tooa tooupload получить ссылку на контейнер и использовать его tooget ссылку на большой двоичный объект блока.</span><span class="sxs-lookup"><span data-stu-id="9928c-147">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="9928c-148">Получив ссылку на большой двоичный объект можно передать любой поток данных tooit с вызывающему Привет **upload_from_stream** метод.</span><span class="sxs-lookup"><span data-stu-id="9928c-148">Once you have a blob reference, you can upload any stream of data tooit by calling hello **upload_from_stream** method.</span></span> <span data-ttu-id="9928c-149">Эта операция создаст hello большого двоичного объекта, если он не существует, или ранее перезаписать его, если он существует.</span><span class="sxs-lookup"><span data-stu-id="9928c-149">This operation will create hello blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="9928c-150">Следующий пример показывает как Hello tooupload большого двоичного объекта в контейнер и предполагается hello контейнера уже был создан.</span><span class="sxs-lookup"><span data-stu-id="9928c-150">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="9928c-151">Кроме того, можно использовать hello **upload_from_file** tooupload метод файл tooa большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="9928c-151">Alternatively, you can use hello **upload_from_file** method tooupload a file tooa block blob.</span></span>

## <a name="how-to-list-hello-blobs-in-a-container"></a><span data-ttu-id="9928c-152">Как: hello двоичные объекты перечислены в контейнер</span><span class="sxs-lookup"><span data-stu-id="9928c-152">How to: List hello blobs in a container</span></span>
<span data-ttu-id="9928c-153">toolist hello BLOB-объектов в контейнере, сначала нужно получить ссылку на контейнер.</span><span class="sxs-lookup"><span data-stu-id="9928c-153">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="9928c-154">Затем можно использовать контейнер hello **list_blobs** метод tooretrieve hello BLOB-объектов и/или каталогов в ней.</span><span class="sxs-lookup"><span data-stu-id="9928c-154">You can then use hello container's **list_blobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="9928c-155">широкий набор свойств и методов для возвращенной hello tooaccess **list_blob_item**, необходимо вызвать hello **list_blob_item.as_blob** tooget метод **cloud_blob** объекта, или hello **list_blob.as_directory** tooget метод объекта cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="9928c-155">tooaccess hello rich set of properties and methods for a returned **list_blob_item**, you must call hello **list_blob_item.as_blob** method tooget a  **cloud_blob** object, or hello **list_blob.as_directory** method tooget a  cloud_blob_directory object.</span></span> <span data-ttu-id="9928c-156">Hello следующий код демонстрирует, как tooretrieve и вывод hello URI каждого элемента в hello **мой пример контейнера** контейнера:</span><span class="sxs-lookup"><span data-stu-id="9928c-156">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
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

<span data-ttu-id="9928c-157">Дополнительные сведения об операциях перечисления см. в разделе [Перечисление ресурсов хранилища Azure в C++](../storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="9928c-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="9928c-158">Практическое руководство. Загрузка BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="9928c-158">How to: Download blobs</span></span>
<span data-ttu-id="9928c-159">toodownload больших двоичных объектов, сначала получить ссылку на большой двоичный объект, а затем вызвать hello **download_to_stream** метод.</span><span class="sxs-lookup"><span data-stu-id="9928c-159">toodownload blobs, first retrieve a blob reference and then call hello **download_to_stream** method.</span></span> <span data-ttu-id="9928c-160">Hello следующий пример использует hello **download_to_stream** метод tootransfer hello blob содержимое tooa объекта потока могут затем сохраняться tooa локального файла.</span><span class="sxs-lookup"><span data-stu-id="9928c-160">hello following example uses hello **download_to_stream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="9928c-161">Кроме того, можно использовать hello **download_to_file** метод toodownload hello содержимое файла tooa большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="9928c-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a blob tooa file.</span></span>
<span data-ttu-id="9928c-162">Кроме того, можно также использовать hello **download_text** метод toodownload hello содержимое большого двоичного объекта в виде строки текста.</span><span class="sxs-lookup"><span data-stu-id="9928c-162">In addition, you can also use hello **download_text** method toodownload hello contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="9928c-163">Практическое руководство. Удаление BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="9928c-163">How to: Delete blobs</span></span>
<span data-ttu-id="9928c-164">toodelete большого двоичного объекта сначала получить ссылку на большой двоичный объект, а затем вызвать hello **delete_blob** метода.</span><span class="sxs-lookup"><span data-stu-id="9928c-164">toodelete a blob, first get a blob reference and then call hello **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="9928c-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9928c-165">Next steps</span></span>
<span data-ttu-id="9928c-166">Теперь, когда вы узнали основы hello хранилища больших двоичных объектов, выполните следующие дополнительные сведения о хранилище Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="9928c-166">Now that you've learned hello basics of blob storage, follow these links toolearn more about Azure Storage.</span></span>  

* [<span data-ttu-id="9928c-167">Как toouse хранилища очередей из C++</span><span class="sxs-lookup"><span data-stu-id="9928c-167">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="9928c-168">Как toouse хранилище таблиц из C++</span><span class="sxs-lookup"><span data-stu-id="9928c-168">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="9928c-169">Перечисление ресурсов хранилища Azure в C++</span><span class="sxs-lookup"><span data-stu-id="9928c-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="9928c-170">Справочник по клиентской библиотеке хранилища для C++</span><span class="sxs-lookup"><span data-stu-id="9928c-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="9928c-171">Документация по хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="9928c-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="9928c-172">Перенесите данные с помощью командной строки программу AzCopy hello</span><span class="sxs-lookup"><span data-stu-id="9928c-172">Transfer data with hello AzCopy command-line utility</span></span>](../storage-use-azcopy.md)

