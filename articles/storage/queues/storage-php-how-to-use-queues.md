---
title: "aaaHow toouse хранилища очередей из PHP | Документы Microsoft"
description: "Узнайте, как toouse hello Azure очереди хранилища службы toocreate и очереди delete и insert, получение и удаление сообщений. Примеры написаны на PHP."
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 8daabcc9b3b4de121a309f21bb3325242cff06f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a>Как toouse хранилища очередей из PHP
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Обзор
В этом руководстве будет показано, как tooperform распространенных сценариев с помощью hello службы хранилища очередей Azure. образцы Hello записываются через классы из пакета SDK для Windows hello для PHP. Hello охватываемые сценарии включают Вставка, просмотр, получение и удаление сообщений очереди, а также создание и удаление очередей.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Создание приложения PHP
Здравствуйте только требования для создания приложения PHP, которое обращается к хранилища очередей Azure — hello ссылки на классы из hello Azure SDK для PHP из кода. Можно использовать любой toocreate средства разработки приложения, включая «Блокнот».

В этом руководстве будут использоваться компоненты хранилища очередей, которые могут быть вызваны локально в приложении PHP или в коде, работающем в веб-роли, рабочей роли или на веб-сайте Azure.

## <a name="get-hello-azure-client-libraries"></a>Получить клиентские библиотеки Azure hello
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a>Настройка вашего приложения tooaccess хранилища очередей
hello toouse API-интерфейсы для хранилища очередей Azure, необходимо:

1. Файл автозагрузчика hello ссылок с помощью hello [require_once] инструкции.
2. Ссылка на любые классы, которые могут использоваться.

Hello следующем примере показано, как tooinclude hello автозагрузчика файла и ссылку hello **ServicesBuilder** класса.

> [!NOTE]
> В этом примере (и другие примеры в этой статье) предполагается, что вы установили hello PHP клиентские библиотеки для Azure через редактор. Если вы установили hello библиотеки вручную, необходимо будет tooreference hello `WindowsAzure.php` автозагрузчика файла.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

В ниже примерах hello, hello `require_once` инструкции всегда будет отображаться, но будет ссылаться только hello классы, необходимые для tooexecute пример hello.

## <a name="set-up-an-azure-storage-connection"></a>Настройка подключения к службе хранилища Azure
tooinstantiate клиент хранилища очередей Azure, сначала нужно допустимую строку соединения. Hello для строки подключения службы hello очереди имеет следующий формат.

Для доступа к службе в режиме реального времени:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Для доступа к хранилищу эмулятор hello:

```php
UseDevelopmentStorage=true
```

toocreate любого клиента службы Azure необходимо toouse hello **ServicesBuilder** класса. Можно использовать либо hello следующие методы:

* Передайте hello подключения tooit строки напрямую.
* Используйте **CloudConfigurationManager (CCM)** toocheck нескольких внешних источников для hello строки подключения:
  * По умолчанию предоставляется поддержка одного внешнего источника — переменных среды.
  * Можно добавлять новые источники, расширяя hello **ConnectionStringSource** класса.

Приведенные ниже примеры hello hello строки подключения будут передаваться напрямую.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Создание очереди
Объект **QueueRestProxy** объектов позволяет создать очередь с помощью hello **createQueue** метод. При создании очереди, можно задать параметры hello очереди, но это не требуется. (hello в следующем примере показано, как tooset метаданные для очереди.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> Не следует полагаться на учет регистра для ключей метаданных. Все ключи считываются из службы hello в нижнем регистре.
> 
> 

## <a name="add-a-message-tooa-queue"></a>Добавить tooa очереди сообщений
Используйте tooadd tooa очередью сообщений **QueueRestProxy -> createMessage**. метод Hello принимает имя очереди hello, текст сообщения hello и параметры сообщения (которые не являются обязательными).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-hello-next-message"></a>Просмотр следующего сообщения hello
Можно читать сообщения (или сообщения) в начале очереди hello не удаляет его из очереди hello путем вызова **QueueRestProxy -> peekMessages**. По умолчанию hello **peekMessage** метод возвращает одно сообщение, но это значение можно изменить с помощью hello **PeekMessagesOptions -> setNumberOfMessages** метод.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-hello-next-message"></a>Отмена очередь следующего сообщения hello
Ваш код удаляет сообщение из очереди в два этапа. Во-первых, можно вызвать **QueueRestProxy -> listMessages**, что делает невидимыми tooany сообщение hello другой код, который выполняет чтение из очереди hello. По умолчанию это сообщение будет оставаться невидимым в течение 30 секунд (Если приветственное сообщение не будет удалена в этот период времени, он будет видимым в очереди hello еще раз.) toofinish удаление приветственное сообщение из очереди hello, необходимо вызвать **QueueRestProxy -> deleteMessage**. Это двухэтапный процесс удаления сообщения гарантирует, что при tooprocess завершается с ошибкой вашего кода, получит сообщение из-за toohardware или ошибок программного обеспечения, другой экземпляр кода hello же сообщение и повторите. Вызовы кода **deleteMessage** сразу после обработки сообщения hello.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-hello-contents-of-a-queued-message"></a>Изменить содержимое hello сообщение из очереди
Можно изменить содержимое сообщений на месте в очереди hello hello путем вызова **QueueRestProxy -> updateMessage**. Если сообщение hello представляет рабочей задачи, можно использовать этот компонент tooupdate hello состояние задачи рабочего hello. После кода Hello обновляет приветственное сообщение очереди новое содержимое, и задает tooextend время ожидания видимости hello другой 60 секунд. Это сохраняет состояние hello работы, связанной с приветственное сообщение, а также клиент hello другой минуты toocontinue работа на приветственное сообщение. Можно использовать этот рабочих процессов способ tootrack многоэтапной для очереди сообщений без необходимости toostart через от начала hello при неудачном завершении шага обработки из-за toohardware или ошибок программного обеспечения. Как правило, будет хранить значение числа повторов, и если hello сообщение повторяется более  *n*  раз, следует удалить его. Это обеспечивает защиту от сообщений, которые инициируют ошибку приложения при каждой попытке обработки.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a>Дополнительные параметры для удаления сообщений из очереди
Существует два способа настройки извлечения сообщения из очереди. Во-первых можно получить пакет сообщений (вверх too32). Во-вторых можно задать время ожидания видимости длинный или короткий, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения. Hello следующий пример кода использует hello **getMessages** метод tooget 16 сообщений в одном вызове. Затем он обрабатывает каждое сообщение с помощью цикла **for** . Он также устанавливает минут toofive hello невидимости время ожидания для каждого сообщения.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a>Получение длины очереди
Можно получить оценку hello количество сообщений в очереди. Hello **QueueRestProxy -> getQueueMetadata** метод запрашивает hello очереди службы tooreturn метаданные о hello очереди. Вызов hello **getApproximateMessageCount** метода в hello возвращен объект предоставляет количество количество сообщений в очереди. число Hello приблизительное только в том случае, поскольку сообщения можно добавить или удалить после запроса tooyour отвечает hello службы очередей.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a>Удаление очереди
toodelete очереди и все сообщения hello, вызовите hello **QueueRestProxy -> deleteQueue** метод.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища очередей Azure, выполните эти ссылки toolearn о более сложных задач хранилища.

* Посетите hello [блога группы разработчиков хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/).

Дополнительные сведения см. также: hello [Центр разработчика PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

