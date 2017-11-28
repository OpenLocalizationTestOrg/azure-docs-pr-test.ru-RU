---
title: "хранилище больших двоичных объектов toouse aaaHow (объект хранилища) из PHP | Документы Microsoft"
description: "Храните неструктурированные данные в облаке hello с хранилищем больших двоичных объектов Azure (хранилище объектов)."
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
ms.openlocfilehash: 331405e583c17c4f71acacdc0078b2bc71efbef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a><span data-ttu-id="c25ba-103">Как toouse хранилище больших двоичных объектов из PHP</span><span class="sxs-lookup"><span data-stu-id="c25ba-103">How toouse blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="c25ba-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c25ba-104">Overview</span></span>
<span data-ttu-id="c25ba-105">Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты.</span><span class="sxs-lookup"><span data-stu-id="c25ba-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="c25ba-106">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="c25ba-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="c25ba-107">Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="c25ba-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="c25ba-108">В этом руководстве показано, как tooperform распространенные сценарии, с помощью hello Azure служба BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="c25ba-108">This guide shows you how tooperform common scenarios using hello Azure blob service.</span></span> <span data-ttu-id="c25ba-109">Hello примеры написаны на PHP и использовать hello [пакет Azure SDK для PHP][download].</span><span class="sxs-lookup"><span data-stu-id="c25ba-109">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="c25ba-110">Hello сценарии включают **передачи**, **вывод**, **Загрузка**, и **удаление** больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c25ba-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="c25ba-111">Дополнительные сведения о больших двоичных объектов см. в разделе hello [дальнейшие действия](#next-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="c25ba-111">For more information on blobs, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="c25ba-112">Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="c25ba-112">Create a PHP application</span></span>
<span data-ttu-id="c25ba-113">Здравствуйте, используется только для создания приложения PHP, которое обращается к службе BLOB-объектов Azure hello hello ссылки на классы в hello Azure SDK для PHP из кода.</span><span class="sxs-lookup"><span data-stu-id="c25ba-113">hello only requirement for creating a PHP application that accesses hello Azure blob service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="c25ba-114">Можно использовать любой toocreate средства разработки приложения, включая «Блокнот».</span><span class="sxs-lookup"><span data-stu-id="c25ba-114">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="c25ba-115">В этом руководстве используются компоненты службы, которые могут быть вызваны локально в приложении PHP или в коде, работающем в веб-роли, рабочей роли или на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="c25ba-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="c25ba-116">Получить клиентские библиотеки Azure hello</span><span class="sxs-lookup"><span data-stu-id="c25ba-116">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a><span data-ttu-id="c25ba-117">Для настройки приложения tooaccess hello больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="c25ba-117">Configure your application tooaccess hello blob service</span></span>
<span data-ttu-id="c25ba-118">toouse hello BLOB-объектов Azure API службы, необходимо:</span><span class="sxs-lookup"><span data-stu-id="c25ba-118">toouse hello Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="c25ba-119">Файл автозагрузчика hello ссылка, с помощью hello [require_once] инструкции, и</span><span class="sxs-lookup"><span data-stu-id="c25ba-119">Reference hello autoloader file using hello [require_once] statement, and</span></span>
2. <span data-ttu-id="c25ba-120">Ссылка на любые классы, которые могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="c25ba-120">Reference any classes you might use.</span></span>

<span data-ttu-id="c25ba-121">Hello следующем примере показано, как tooinclude hello автозагрузчика файла и ссылку hello **ServicesBuilder** класса.</span><span class="sxs-lookup"><span data-stu-id="c25ba-121">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="c25ba-122">Примеры Hello в этой статье предполагается, что вы установили hello клиентские библиотеки PHP для Azure через редактор.</span><span class="sxs-lookup"><span data-stu-id="c25ba-122">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="c25ba-123">При установке библиотеки hello вручную необходимо tooreference hello `WindowsAzure.php` автозагрузчика файла.</span><span class="sxs-lookup"><span data-stu-id="c25ba-123">If you installed hello libraries manually, you need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="c25ba-124">В ниже примерах hello, hello `require_once` всегда отображаются инструкции, но указываются только классы hello, необходимые для tooexecute пример hello.</span><span class="sxs-lookup"><span data-stu-id="c25ba-124">In hello examples below, hello `require_once` statement will be shown always, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="c25ba-125">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c25ba-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="c25ba-126">tooinstantiate клиента службы BLOB-объектов Azure, сначала нужно допустимую строку соединения.</span><span class="sxs-lookup"><span data-stu-id="c25ba-126">tooinstantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="c25ba-127">Hello для строки подключения для службы BLOB-объектов hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c25ba-127">hello format for hello blob service connection string is:</span></span>

<span data-ttu-id="c25ba-128">Для доступа к службе в режиме реального времени:</span><span class="sxs-lookup"><span data-stu-id="c25ba-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="c25ba-129">Для доступа к hello эмулятор хранилища:</span><span class="sxs-lookup"><span data-stu-id="c25ba-129">For accessing hello storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="c25ba-130">toocreate любого клиента службы Azure необходимо toouse hello **ServicesBuilder** класса.</span><span class="sxs-lookup"><span data-stu-id="c25ba-130">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="c25ba-131">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="c25ba-131">You can:</span></span>

* <span data-ttu-id="c25ba-132">Передайте hello подключения напрямую строка tooit или</span><span class="sxs-lookup"><span data-stu-id="c25ba-132">Pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="c25ba-133">использовать hello **CloudConfigurationManager (CCM)** toocheck нескольких внешних источников для hello строки подключения:</span><span class="sxs-lookup"><span data-stu-id="c25ba-133">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="c25ba-134">по умолчанию предоставляется поддержка одного внешнего источника — переменных среды;</span><span class="sxs-lookup"><span data-stu-id="c25ba-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="c25ba-135">Можно добавлять новые источники, расширяя hello **ConnectionStringSource** класса.</span><span class="sxs-lookup"><span data-stu-id="c25ba-135">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="c25ba-136">Приведенные ниже примеры hello hello строки подключения будут передаваться напрямую.</span><span class="sxs-lookup"><span data-stu-id="c25ba-136">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="c25ba-137">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="c25ba-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="c25ba-138">Объект **BlobRestProxy** объектов позволяет создавать контейнер больших двоичных объектов с hello **createContainer** метод.</span><span class="sxs-lookup"><span data-stu-id="c25ba-138">A **BlobRestProxy** object lets you create a blob container with hello **createContainer** method.</span></span> <span data-ttu-id="c25ba-139">При создании контейнера, можно задать параметры для hello контейнера, но это не требуется.</span><span class="sxs-lookup"><span data-stu-id="c25ba-139">When creating a container, you can set options on hello container, but doing so is not required.</span></span> <span data-ttu-id="c25ba-140">(hello приведенном ниже примере показано, как доступ к tooset hello контейнера списка управления Доступом, а также метаданные контейнера).</span><span class="sxs-lookup"><span data-stu-id="c25ba-140">(hello example below shows how tooset hello container access control list (ACL) and container metadata.)</span></span>

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
// proxys can enumerate blobs within hello container via anonymous
// request, but cannot enumerate containers within hello storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within hello container via
// anonymous request.
// If this value is not specified in hello request, container data is
// private toohello account owner.
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

<span data-ttu-id="c25ba-141">Вызов **setPublicAccess (PublicAccessType::CONTAINER\_AND\_больших двоичных ОБЪЕКТОВ)** делает hello контейнерах и больших двоичных данных, доступные через анонимные запросы.</span><span class="sxs-lookup"><span data-stu-id="c25ba-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes hello container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="c25ba-142">Вызов **setPublicAccess(PublicAccessType::BLOBS_ONLY)** делает доступными через анонимные запросы только данные BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="c25ba-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="c25ba-143">Дополнительные сведения о списках управления доступом контейнеров см. в статье [Set Container ACL][container-acl] (Задание списка управления доступом для контейнера).</span><span class="sxs-lookup"><span data-stu-id="c25ba-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="c25ba-144">Дополнительные сведения о кодах ошибок службы BLOB-объектов см. в разделе [Blob Service Error Codes][error-codes] (Коды ошибок службы BLOB-объектов).</span><span class="sxs-lookup"><span data-stu-id="c25ba-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="c25ba-145">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="c25ba-145">Upload a blob into a container</span></span>
<span data-ttu-id="c25ba-146">файл в качестве большого двоичного объекта используйте hello tooupload **BlobRestProxy -> createBlockBlob** метод.</span><span class="sxs-lookup"><span data-stu-id="c25ba-146">tooupload a file as a blob, use hello **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="c25ba-147">Эта операция создает hello большого двоичного объекта, если он не существует, или перезаписывает его, если это так.</span><span class="sxs-lookup"><span data-stu-id="c25ba-147">This operation creates hello blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="c25ba-148">Hello в следующем примере предполагается, этот контейнер hello уже создан и использует [fopen] [ fopen] tooopen hello файл как поток.</span><span class="sxs-lookup"><span data-stu-id="c25ba-148">hello code example below assumes that hello container has already been created and uses [fopen][fopen] tooopen hello file as a stream.</span></span>

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

<span data-ttu-id="c25ba-149">Обратите внимание, что предыдущий образец hello загружает большой двоичный объект в виде потока.</span><span class="sxs-lookup"><span data-stu-id="c25ba-149">Note that hello previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="c25ba-150">Тем не менее, большой двоичный объект можно также передать в строку, используя, например, hello [файл\_получить\_содержимого] [ file_get_contents] функции.</span><span class="sxs-lookup"><span data-stu-id="c25ba-150">However, a blob can also be uploaded as a string using, for example, hello [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="c25ba-151">toodo этого с помощью предыдущего образца hello, изменить `$content = fopen("c:\myfile.txt", "r");` слишком`$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="c25ba-151">toodo this using hello previous sample, change `$content = fopen("c:\myfile.txt", "r");` too`$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="c25ba-152">Перечисление hello больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="c25ba-152">List hello blobs in a container</span></span>
<span data-ttu-id="c25ba-153">toolist hello BLOB-объектов в контейнере, используйте hello **BlobRestProxy -> listBlobs** метод с **foreach** цикл tooloop из результатов hello.</span><span class="sxs-lookup"><span data-stu-id="c25ba-153">toolist hello blobs in a container, use hello **BlobRestProxy->listBlobs** method with a **foreach** loop tooloop through hello result.</span></span> <span data-ttu-id="c25ba-154">Hello следующий код отображает hello имени каждого BLOB-объекта в качестве выходных данных в контейнере и toohello его URI браузера.</span><span class="sxs-lookup"><span data-stu-id="c25ba-154">hello following code displays hello name of each blob as output in a container and displays its URI toohello browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="c25ba-155">Загрузка BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="c25ba-155">Download a blob</span></span>
<span data-ttu-id="c25ba-156">toodownload большой двоичный объект hello вызовов **BlobRestProxy -> getBlob** метод, то вызов hello **getContentStream** метод на возникающие hello **GetBlobResult** объекта.</span><span class="sxs-lookup"><span data-stu-id="c25ba-156">toodownload a blob, call hello **BlobRestProxy->getBlob** method, then call hello **getContentStream** method on hello resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="c25ba-157">Обратите внимание, что приведенном выше примере hello возвращает большой двоичный объект как ресурс потока (поведение по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="c25ba-157">Note that hello example above gets a blob as a stream resource (hello default behavior).</span></span> <span data-ttu-id="c25ba-158">Тем не менее, можно использовать hello [поток\_получить\_содержимого] [ stream-get-contents] hello tooconvert функция возвращена строка tooa потока.</span><span class="sxs-lookup"><span data-stu-id="c25ba-158">However, you can use hello [stream\_get\_contents][stream-get-contents] function tooconvert hello returned stream tooa string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="c25ba-159">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="c25ba-159">Delete a blob</span></span>
<span data-ttu-id="c25ba-160">toodelete большого двоичного объекта, передать имя контейнера hello и имя большого двоичного объекта слишком**BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="c25ba-160">toodelete a blob, pass hello container name and blob name too**BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="c25ba-161">Удаление контейнера blob-объектов</span><span class="sxs-lookup"><span data-stu-id="c25ba-161">Delete a blob container</span></span>
<span data-ttu-id="c25ba-162">Наконец, toodelete контейнер больших двоичных объектов, передайте имя контейнера hello слишком**BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="c25ba-162">Finally, toodelete a blob container, pass hello container name too**BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c25ba-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c25ba-163">Next steps</span></span>
<span data-ttu-id="c25ba-164">Теперь, когда вы узнали основы hello hello службы BLOB-объектов Azure, выполните эти ссылки toolearn о более сложных задач хранилища.</span><span class="sxs-lookup"><span data-stu-id="c25ba-164">Now that you've learned hello basics of hello Azure blob service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="c25ba-165">Посетите hello [блог группы разработчиков хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="c25ba-165">Visit hello [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="c25ba-166">В разделе hello [пример большого двоичного объекта блока PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="c25ba-166">See hello [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="c25ba-167">В разделе hello [пример большой двоичный объект страницы PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="c25ba-167">See hello [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="c25ba-168">Перенесите данные с помощью служебной программы командной строки AzCopy hello</span><span class="sxs-lookup"><span data-stu-id="c25ba-168">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

<span data-ttu-id="c25ba-169">Дополнительные сведения см. также: hello [Центр разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="c25ba-169">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
