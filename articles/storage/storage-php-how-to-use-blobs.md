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
# <a name="how-toouse-blob-storage-from-php"></a>Как toouse хранилище больших двоичных объектов из PHP
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Обзор
Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты. В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений. Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.

В этом руководстве показано, как tooperform распространенные сценарии, с помощью hello Azure служба BLOB-объектов. Hello примеры написаны на PHP и использовать hello [пакет Azure SDK для PHP][download]. Hello сценарии включают **передачи**, **вывод**, **Загрузка**, и **удаление** больших двоичных объектов. Дополнительные сведения о больших двоичных объектов см. в разделе hello [дальнейшие действия](#next-steps) раздела.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Создание приложения PHP
Здравствуйте, используется только для создания приложения PHP, которое обращается к службе BLOB-объектов Azure hello hello ссылки на классы в hello Azure SDK для PHP из кода. Можно использовать любой toocreate средства разработки приложения, включая «Блокнот».

В этом руководстве используются компоненты службы, которые могут быть вызваны локально в приложении PHP или в коде, работающем в веб-роли, рабочей роли или на веб-сайте Azure.

## <a name="get-hello-azure-client-libraries"></a>Получить клиентские библиотеки Azure hello
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a>Для настройки приложения tooaccess hello больших двоичных объектов
toouse hello BLOB-объектов Azure API службы, необходимо:

1. Файл автозагрузчика hello ссылка, с помощью hello [require_once] инструкции, и
2. Ссылка на любые классы, которые могут использоваться.

Hello следующем примере показано, как tooinclude hello автозагрузчика файла и ссылку hello **ServicesBuilder** класса.

> [!NOTE]
> Примеры Hello в этой статье предполагается, что вы установили hello клиентские библиотеки PHP для Azure через редактор. При установке библиотеки hello вручную необходимо tooreference hello `WindowsAzure.php` автозагрузчика файла.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

В ниже примерах hello, hello `require_once` всегда отображаются инструкции, но указываются только классы hello, необходимые для tooexecute пример hello.

## <a name="set-up-an-azure-storage-connection"></a>Настройка подключения к службе хранилища Azure
tooinstantiate клиента службы BLOB-объектов Azure, сначала нужно допустимую строку соединения. Hello для строки подключения для службы BLOB-объектов hello выглядит следующим образом:

Для доступа к службе в режиме реального времени:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Для доступа к hello эмулятор хранилища:

```php
UseDevelopmentStorage=true
```

toocreate любого клиента службы Azure необходимо toouse hello **ServicesBuilder** класса. Вы можете:

* Передайте hello подключения напрямую строка tooit или
* использовать hello **CloudConfigurationManager (CCM)** toocheck нескольких внешних источников для hello строки подключения:
  * по умолчанию предоставляется поддержка одного внешнего источника — переменных среды;
  * Можно добавлять новые источники, расширяя hello **ConnectionStringSource** класса.

Приведенные ниже примеры hello hello строки подключения будут передаваться напрямую.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a>Создание контейнера
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Объект **BlobRestProxy** объектов позволяет создавать контейнер больших двоичных объектов с hello **createContainer** метод. При создании контейнера, можно задать параметры для hello контейнера, но это не требуется. (hello приведенном ниже примере показано, как доступ к tooset hello контейнера списка управления Доступом, а также метаданные контейнера).

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

Вызов **setPublicAccess (PublicAccessType::CONTAINER\_AND\_больших двоичных ОБЪЕКТОВ)** делает hello контейнерах и больших двоичных данных, доступные через анонимные запросы. Вызов **setPublicAccess(PublicAccessType::BLOBS_ONLY)** делает доступными через анонимные запросы только данные BLOB-объектов. Дополнительные сведения о списках управления доступом контейнеров см. в статье [Set Container ACL][container-acl] (Задание списка управления доступом для контейнера).

Дополнительные сведения о кодах ошибок службы BLOB-объектов см. в разделе [Blob Service Error Codes][error-codes] (Коды ошибок службы BLOB-объектов).

## <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
файл в качестве большого двоичного объекта используйте hello tooupload **BlobRestProxy -> createBlockBlob** метод. Эта операция создает hello большого двоичного объекта, если он не существует, или перезаписывает его, если это так. Hello в следующем примере предполагается, этот контейнер hello уже создан и использует [fopen] [ fopen] tooopen hello файл как поток.

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

Обратите внимание, что предыдущий образец hello загружает большой двоичный объект в виде потока. Тем не менее, большой двоичный объект можно также передать в строку, используя, например, hello [файл\_получить\_содержимого] [ file_get_contents] функции. toodo этого с помощью предыдущего образца hello, изменить `$content = fopen("c:\myfile.txt", "r");` слишком`$content = file_get_contents("c:\myfile.txt");`.

## <a name="list-hello-blobs-in-a-container"></a>Перечисление hello больших двоичных объектов в контейнере
toolist hello BLOB-объектов в контейнере, используйте hello **BlobRestProxy -> listBlobs** метод с **foreach** цикл tooloop из результатов hello. Hello следующий код отображает hello имени каждого BLOB-объекта в качестве выходных данных в контейнере и toohello его URI браузера.

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

## <a name="download-a-blob"></a>Загрузка BLOB-объектов
toodownload большой двоичный объект hello вызовов **BlobRestProxy -> getBlob** метод, то вызов hello **getContentStream** метод на возникающие hello **GetBlobResult** объекта.

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

Обратите внимание, что приведенном выше примере hello возвращает большой двоичный объект как ресурс потока (поведение по умолчанию hello). Тем не менее, можно использовать hello [поток\_получить\_содержимого] [ stream-get-contents] hello tooconvert функция возвращена строка tooa потока.

## <a name="delete-a-blob"></a>Удаление большого двоичного объекта
toodelete большого двоичного объекта, передать имя контейнера hello и имя большого двоичного объекта слишком**BlobRestProxy -> deleteBlob**.

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

## <a name="delete-a-blob-container"></a>Удаление контейнера blob-объектов
Наконец, toodelete контейнер больших двоичных объектов, передайте имя контейнера hello слишком**BlobRestProxy -> deleteContainer**.

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

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello hello службы BLOB-объектов Azure, выполните эти ссылки toolearn о более сложных задач хранилища.

* Посетите hello [блог группы разработчиков хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* В разделе hello [пример большого двоичного объекта блока PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).
* В разделе hello [пример большой двоичный объект страницы PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).
* [Перенесите данные с помощью служебной программы командной строки AzCopy hello](storage-use-azcopy.md)

Дополнительные сведения см. также: hello [Центр разработчика PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
