---
title: "Как использовать хранилище BLOB-объектов (хранилище объектов) из PHP | Документация Майкрософт"
description: "Хранение неструктурированных данных в облаке в хранилище BLOB-объектов Azure."
documentationcenter: php
services: storage
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1af56b59-b3f0-4b46-8441-aab463ae088e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 2c356d7faafa8ef4591087b5b1f949b9374732be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-php"></a><span data-ttu-id="0991b-103">Использование хранилища больших двоичных объектов из PHP</span><span class="sxs-lookup"><span data-stu-id="0991b-103">How to use blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="0991b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="0991b-104">Overview</span></span>
<span data-ttu-id="0991b-105">Хранилище BLOB-объектов Azure — это служба, которая хранит неструктурированные данные в облаке в качестве объектов или больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="0991b-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="0991b-106">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="0991b-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="0991b-107">Хранилище BLOB-объектов иногда также называют хранилищем объектов.</span><span class="sxs-lookup"><span data-stu-id="0991b-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="0991b-108">В этом руководстве показано, как реализовать типичные сценарии с использованием службы BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0991b-108">This guide shows you how to perform common scenarios using the Azure blob service.</span></span> <span data-ttu-id="0991b-109">Примеры написаны на PHP и используют [пакет SDK Azure для PHP][download].</span><span class="sxs-lookup"><span data-stu-id="0991b-109">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="0991b-110">Здесь описаны такие сценарии, как **отправка**, **перечисление**, **скачивание** и **удаление** BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="0991b-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="0991b-111">Дополнительные сведения о больших двоичных объектах см. в разделе [Дальнейшие действия](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="0991b-111">For more information on blobs, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="0991b-112">Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="0991b-112">Create a PHP application</span></span>
<span data-ttu-id="0991b-113">Единственным требованием для создания приложения PHP, которое получает доступ к службе BLOB-объектов Azure, является ссылка на классы в пакете SDK для Azure для PHP непосредственно из кода.</span><span class="sxs-lookup"><span data-stu-id="0991b-113">The only requirement for creating a PHP application that accesses the Azure blob service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="0991b-114">Можно использовать любые средства разработки для создания приложения, включая программу "Блокнот".</span><span class="sxs-lookup"><span data-stu-id="0991b-114">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="0991b-115">В этом руководстве используются компоненты службы, которые могут быть вызваны локально в приложении PHP или в коде, работающем в веб-роли, рабочей роли или на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="0991b-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="0991b-116">Получение клиентских библиотек Azure</span><span class="sxs-lookup"><span data-stu-id="0991b-116">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-blob-service"></a><span data-ttu-id="0991b-117">Настройка приложения для доступа к службе BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="0991b-117">Configure your application to access the blob service</span></span>
<span data-ttu-id="0991b-118">Чтобы использовать интерфейсы API службы BLOB-объектов Azure, требуется:</span><span class="sxs-lookup"><span data-stu-id="0991b-118">To use the Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="0991b-119">Ссылка на файл автозагрузчика с использованием инструкции [require_once] и</span><span class="sxs-lookup"><span data-stu-id="0991b-119">Reference the autoloader file using the [require_once] statement, and</span></span>
2. <span data-ttu-id="0991b-120">Ссылка на любые классы, которые могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="0991b-120">Reference any classes you might use.</span></span>

<span data-ttu-id="0991b-121">В следующем примере показано, как включить файл автозагрузчика и сослаться на класс **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="0991b-121">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="0991b-122">В примере этой статьи предполагается, что установлены клиентские библиотеки PHP для Azure с помощью Composer.</span><span class="sxs-lookup"><span data-stu-id="0991b-122">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="0991b-123">Если вы установили эти библиотеки вручную, то необходимо добавить ссылку на файл автозагрузчика `WindowsAzure.php` .</span><span class="sxs-lookup"><span data-stu-id="0991b-123">If you installed the libraries manually, you need to reference the `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="0991b-124">В приведенных ниже примерах всегда будет отображаться оператор `require_once` , однако ссылки будут приводиться только на классы, которые необходимы для выполнения этого примера.</span><span class="sxs-lookup"><span data-stu-id="0991b-124">In the examples below, the `require_once` statement will be shown always, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="0991b-125">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="0991b-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="0991b-126">Чтобы создать экземпляр клиента службы BLOB-объектов Azure, сначала необходимо сформировать правильную строку подключения.</span><span class="sxs-lookup"><span data-stu-id="0991b-126">To instantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="0991b-127">Формат строки подключения к службе BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="0991b-127">The format for the blob service connection string is:</span></span>

<span data-ttu-id="0991b-128">Для доступа к службе в режиме реального времени:</span><span class="sxs-lookup"><span data-stu-id="0991b-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="0991b-129">Для доступа к эмулятору хранения:</span><span class="sxs-lookup"><span data-stu-id="0991b-129">For accessing the storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="0991b-130">Чтобы создать клиент любой службы Azure, необходимо использовать класс **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="0991b-130">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="0991b-131">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="0991b-131">You can:</span></span>

* <span data-ttu-id="0991b-132">передать строку подключения напрямую или</span><span class="sxs-lookup"><span data-stu-id="0991b-132">Pass the connection string directly to it or</span></span>
* <span data-ttu-id="0991b-133">использовать **CloudConfigurationManager (CCM)** для проверки нескольких внешних источников на наличие строки подключения:</span><span class="sxs-lookup"><span data-stu-id="0991b-133">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="0991b-134">по умолчанию предоставляется поддержка одного внешнего источника — переменных среды;</span><span class="sxs-lookup"><span data-stu-id="0991b-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="0991b-135">можно добавить новые источники, расширив класс **ConnectionStringSource** .</span><span class="sxs-lookup"><span data-stu-id="0991b-135">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="0991b-136">В приведенных здесь примерах строка подключения передается напрямую.</span><span class="sxs-lookup"><span data-stu-id="0991b-136">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="0991b-137">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="0991b-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="0991b-138">Объект **BlobRestProxy** позволяет создать контейнер BLOB-объектов с помощью метода **createContainer**.</span><span class="sxs-lookup"><span data-stu-id="0991b-138">A **BlobRestProxy** object lets you create a blob container with the **createContainer** method.</span></span> <span data-ttu-id="0991b-139">При создании контейнера можно задать параметры контейнера, однако это не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="0991b-139">When creating a container, you can set options on the container, but doing so is not required.</span></span> <span data-ttu-id="0991b-140">(В приведенном ниже примере показано, как задать список управления доступом (ACL) и метаданные контейнера.)</span><span class="sxs-lookup"><span data-stu-id="0991b-140">(The example below shows how to set the container access control list (ACL) and container metadata.)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Blob\Models\CreateContainerOptions;
use MicrosoftAzure\Storage\Blob\Models\PublicAccessType;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


// OPTIONAL: Set public access policy and metadata.
// Create container options object.
$createContainerOptions = new CreateContainerOptions();

// Set public access policy. Possible values are
// PublicAccessType::CONTAINER_AND_BLOBS and PublicAccessType::BLOBS_ONLY.
// CONTAINER_AND_BLOBS:
// Specifies full public read access for container and blob data.
// proxys can enumerate blobs within the container via anonymous
// request, but cannot enumerate containers within the storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within the container via
// anonymous request.
// If this value is not specified in the request, container data is
// private to the account owner.
$createContainerOptions->setPublicAccess(PublicAccessType::CONTAINER_AND_BLOBS);

// Set container metadata.
$createContainerOptions->addMetaData("key1", "value1");
$createContainerOptions->addMetaData("key2", "value2");

try    {
    // Create container.
    $blobRestProxy->createContainer("mycontainer", $createContainerOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="0991b-141">Вызов **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** делает контейнер и данные BLOB-объектов доступными через анонимные запросы.</span><span class="sxs-lookup"><span data-stu-id="0991b-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes the container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="0991b-142">Вызов **setPublicAccess(PublicAccessType::BLOBS_ONLY)** делает доступными через анонимные запросы только данные BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="0991b-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="0991b-143">Дополнительные сведения о списках управления доступом контейнеров см. в статье [Set Container ACL][container-acl] (Задание списка управления доступом для контейнера).</span><span class="sxs-lookup"><span data-stu-id="0991b-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="0991b-144">Дополнительные сведения о кодах ошибок службы BLOB-объектов см. в разделе [Blob Service Error Codes][error-codes] (Коды ошибок службы BLOB-объектов).</span><span class="sxs-lookup"><span data-stu-id="0991b-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="0991b-145">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="0991b-145">Upload a blob into a container</span></span>
<span data-ttu-id="0991b-146">Чтобы передать файл в виде BLOB-объекта, используйте метод **BlobRestProxy->createBlockBlob**.</span><span class="sxs-lookup"><span data-stu-id="0991b-146">To upload a file as a blob, use the **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="0991b-147">Эта операция создает большой двоичный объект, если он еще не существует, или заменяет его, если он существует.</span><span class="sxs-lookup"><span data-stu-id="0991b-147">This operation creates the blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="0991b-148">В примере кода предполагается, что контейнер уже был создан и использует [fopen][fopen] для открытия файла в виде потока.</span><span class="sxs-lookup"><span data-stu-id="0991b-148">The code example below assumes that the container has already been created and uses [fopen][fopen] to open the file as a stream.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


$content = fopen("c:\myfile.txt", "r");
$blob_name = "myblob";

try    {
    //Upload blob
    $blobRestProxy->createBlockBlob("mycontainer", $blob_name, $content);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="0991b-149">Обратите внимание, что в предыдущем примере большой двоичный объект передается в виде потока.</span><span class="sxs-lookup"><span data-stu-id="0991b-149">Note that the previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="0991b-150">Однако BLOB-объект можно передать в качестве строки с помощью, к примеру, функции [file\_get\_contents][file_get_contents].</span><span class="sxs-lookup"><span data-stu-id="0991b-150">However, a blob can also be uploaded as a string using, for example, the [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="0991b-151">Чтобы сделать это, используя предыдущий пример, измените `$content = fopen("c:\myfile.txt", "r");` на `$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="0991b-151">To do this using the previous sample, change `$content = fopen("c:\myfile.txt", "r");` to `$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="0991b-152">Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="0991b-152">List the blobs in a container</span></span>
<span data-ttu-id="0991b-153">Чтобы получить список BLOB-объектов в контейнере, используйте метод **BlobRestProxy->listBlobs** с циклом **foreach** для перебора результатов.</span><span class="sxs-lookup"><span data-stu-id="0991b-153">To list the blobs in a container, use the **BlobRestProxy->listBlobs** method with a **foreach** loop to loop through the result.</span></span> <span data-ttu-id="0991b-154">Следующий код выводит имя каждого большого двоичного объекта в контейнере и соответствующий URI в браузере.</span><span class="sxs-lookup"><span data-stu-id="0991b-154">The following code displays the name of each blob as output in a container and displays its URI to the browser.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // List blobs.
    $blob_list = $blobRestProxy->listBlobs("mycontainer");
    $blobs = $blob_list->getBlobs();

    foreach($blobs as $blob)
    {
        echo $blob->getName().": ".$blob->getUrl()."<br />";
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="download-a-blob"></a><span data-ttu-id="0991b-155">Загрузка BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="0991b-155">Download a blob</span></span>
<span data-ttu-id="0991b-156">Чтобы загрузить BLOB-объект, вызовите метод **BlobRestProxy->getBlob**, затем вызовите метод **getContentStream** для результирующего объекта **GetBlobResult**.</span><span class="sxs-lookup"><span data-stu-id="0991b-156">To download a blob, call the **BlobRestProxy->getBlob** method, then call the **getContentStream** method on the resulting **GetBlobResult** object.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Get blob.
    $blob = $blobRestProxy->getBlob("mycontainer", "myblob");
    fpassthru($blob->getContentStream());
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="0991b-157">Обратите внимание, что приведенный выше пример получает BLOB-объект как ресурс потока (поведение по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="0991b-157">Note that the example above gets a blob as a stream resource (the default behavior).</span></span> <span data-ttu-id="0991b-158">Однако можно использовать функцию [stream\_get\_contents][stream-get-contents] для преобразования возвращенного потока в строку.</span><span class="sxs-lookup"><span data-stu-id="0991b-158">However, you can use the [stream\_get\_contents][stream-get-contents] function to convert the returned stream to a string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="0991b-159">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="0991b-159">Delete a blob</span></span>
<span data-ttu-id="0991b-160">Чтобы удалить BLOB-объект, передайте имя контейнера и имя BLOB-объекта в **BlobRestProxy->deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="0991b-160">To delete a blob, pass the container name and blob name to **BlobRestProxy->deleteBlob**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Delete blob.
    $blobRestProxy->deleteBlob("mycontainer", "myblob");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="0991b-161">Удаление контейнера blob-объектов</span><span class="sxs-lookup"><span data-stu-id="0991b-161">Delete a blob container</span></span>
<span data-ttu-id="0991b-162">Наконец, чтобы удалить контейнер BLOB-объектов, передайте имя контейнера в **BlobRestProxy->deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="0991b-162">Finally, to delete a blob container, pass the container name to **BlobRestProxy->deleteContainer**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);

try    {
    // Delete container.
    $blobRestProxy->deleteContainer("mycontainer");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="0991b-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0991b-163">Next steps</span></span>
<span data-ttu-id="0991b-164">Вы изучили основную информацию о службе BLOB-объектов Azure. Дополнительную информацию о более сложных задачах по использованию хранилища можно найти по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="0991b-164">Now that you've learned the basics of the Azure blob service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="0991b-165">Посетите [блог команды разработчиков службы хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="0991b-165">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="0991b-166">Ознакомьтесь с [примером блочного BLOB-объекта РНР](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="0991b-166">See the [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="0991b-167">Ознакомьтесь с [примером страничного BLOB-объекта PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="0991b-167">See the [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="0991b-168">Приступая к работе со служебной программой командной строки AzCopy</span><span class="sxs-lookup"><span data-stu-id="0991b-168">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

<span data-ttu-id="0991b-169">Дополнительную информацию можно найти также в [Центре разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="0991b-169">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
<span data-ttu-id="0991b-170">[require_once]: http://php.net/require_once</span><span class="sxs-lookup"><span data-stu-id="0991b-170">[require_once]: http://php.net/require_once</span></span>
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
