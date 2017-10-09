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
ms.openlocfilehash: 5034faf3b5f28f72d5b56ac1ce7a5723be697ce6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a><span data-ttu-id="65240-104">Как toouse хранилища очередей из PHP</span><span class="sxs-lookup"><span data-stu-id="65240-104">How toouse Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="65240-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="65240-105">Overview</span></span>
<span data-ttu-id="65240-106">В этом руководстве будет показано, как tooperform распространенных сценариев с помощью hello службы хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="65240-106">This guide will show you how tooperform common scenarios by using hello Azure Queue storage service.</span></span> <span data-ttu-id="65240-107">образцы Hello записываются через классы из пакета SDK для Windows hello для PHP.</span><span class="sxs-lookup"><span data-stu-id="65240-107">hello samples are written via classes from hello Windows SDK for PHP.</span></span> <span data-ttu-id="65240-108">Hello охватываемые сценарии включают Вставка, просмотр, получение и удаление сообщений очереди, а также создание и удаление очередей.</span><span class="sxs-lookup"><span data-stu-id="65240-108">hello covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="65240-109">Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="65240-109">Create a PHP application</span></span>
<span data-ttu-id="65240-110">Здравствуйте только требования для создания приложения PHP, которое обращается к хранилища очередей Azure — hello ссылки на классы из hello Azure SDK для PHP из кода.</span><span class="sxs-lookup"><span data-stu-id="65240-110">hello only requirement for creating a PHP application that accesses Azure Queue storage is hello referencing of classes from hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="65240-111">Можно использовать любой toocreate средства разработки приложения, включая «Блокнот».</span><span class="sxs-lookup"><span data-stu-id="65240-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="65240-112">В этом руководстве будут использоваться компоненты хранилища очередей, которые могут быть вызваны локально в приложении PHP или в коде, работающем в веб-роли, рабочей роли или на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="65240-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="65240-113">Получить клиентские библиотеки Azure hello</span><span class="sxs-lookup"><span data-stu-id="65240-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="65240-114">Настройка вашего приложения tooaccess хранилища очередей</span><span class="sxs-lookup"><span data-stu-id="65240-114">Configure your application tooaccess Queue storage</span></span>
<span data-ttu-id="65240-115">hello toouse API-интерфейсы для хранилища очередей Azure, необходимо:</span><span class="sxs-lookup"><span data-stu-id="65240-115">toouse hello APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="65240-116">Файл автозагрузчика hello ссылок с помощью hello [require_once] инструкции.</span><span class="sxs-lookup"><span data-stu-id="65240-116">Reference hello autoloader file by using hello [require_once] statement.</span></span>
2. <span data-ttu-id="65240-117">Ссылка на любые классы, которые могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="65240-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="65240-118">Hello следующем примере показано, как tooinclude hello автозагрузчика файла и ссылку hello **ServicesBuilder** класса.</span><span class="sxs-lookup"><span data-stu-id="65240-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="65240-119">В этом примере (и другие примеры в этой статье) предполагается, что вы установили hello PHP клиентские библиотеки для Azure через редактор.</span><span class="sxs-lookup"><span data-stu-id="65240-119">This example (and other examples in this article) assumes that you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="65240-120">Если вы установили hello библиотеки вручную, необходимо будет tooreference hello `WindowsAzure.php` автозагрузчика файла.</span><span class="sxs-lookup"><span data-stu-id="65240-120">If you installed hello libraries manually, you will need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="65240-121">В ниже примерах hello, hello `require_once` инструкции всегда будет отображаться, но будет ссылаться только hello классы, необходимые для tooexecute пример hello.</span><span class="sxs-lookup"><span data-stu-id="65240-121">In hello examples below, hello `require_once` statement will be shown always, but only hello classes that are necessary for hello example tooexecute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="65240-122">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="65240-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="65240-123">tooinstantiate клиент хранилища очередей Azure, сначала нужно допустимую строку соединения.</span><span class="sxs-lookup"><span data-stu-id="65240-123">tooinstantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="65240-124">Hello для строки подключения службы hello очереди имеет следующий формат.</span><span class="sxs-lookup"><span data-stu-id="65240-124">hello format for hello queue service connection string is as follows.</span></span>

<span data-ttu-id="65240-125">Для доступа к службе в режиме реального времени:</span><span class="sxs-lookup"><span data-stu-id="65240-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="65240-126">Для доступа к хранилищу эмулятор hello:</span><span class="sxs-lookup"><span data-stu-id="65240-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="65240-127">toocreate любого клиента службы Azure необходимо toouse hello **ServicesBuilder** класса.</span><span class="sxs-lookup"><span data-stu-id="65240-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="65240-128">Можно использовать либо hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="65240-128">You can use either of hello following techniques:</span></span>

* <span data-ttu-id="65240-129">Передайте hello подключения tooit строки напрямую.</span><span class="sxs-lookup"><span data-stu-id="65240-129">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="65240-130">Используйте **CloudConfigurationManager (CCM)** toocheck нескольких внешних источников для hello строки подключения:</span><span class="sxs-lookup"><span data-stu-id="65240-130">Use **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="65240-131">По умолчанию предоставляется поддержка одного внешнего источника — переменных среды.</span><span class="sxs-lookup"><span data-stu-id="65240-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="65240-132">Можно добавлять новые источники, расширяя hello **ConnectionStringSource** класса.</span><span class="sxs-lookup"><span data-stu-id="65240-132">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="65240-133">Приведенные ниже примеры hello hello строки подключения будут передаваться напрямую.</span><span class="sxs-lookup"><span data-stu-id="65240-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="65240-134">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="65240-134">Create a queue</span></span>
<span data-ttu-id="65240-135">Объект **QueueRestProxy** объектов позволяет создать очередь с помощью hello **createQueue** метод.</span><span class="sxs-lookup"><span data-stu-id="65240-135">A **QueueRestProxy** object lets you create a queue by using hello **createQueue** method.</span></span> <span data-ttu-id="65240-136">При создании очереди, можно задать параметры hello очереди, но это не требуется.</span><span class="sxs-lookup"><span data-stu-id="65240-136">When creating a queue, you can set options on hello queue, but doing so is not required.</span></span> <span data-ttu-id="65240-137">(hello в следующем примере показано, как tooset метаданные для очереди.)</span><span class="sxs-lookup"><span data-stu-id="65240-137">(hello example below shows how tooset metadata on a queue.)</span></span>

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
> <span data-ttu-id="65240-138">Не следует полагаться на учет регистра для ключей метаданных.</span><span class="sxs-lookup"><span data-stu-id="65240-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="65240-139">Все ключи считываются из службы hello в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="65240-139">All keys are read from hello service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="65240-140">Добавить tooa очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="65240-140">Add a message tooa queue</span></span>
<span data-ttu-id="65240-141">Используйте tooadd tooa очередью сообщений **QueueRestProxy -> createMessage**.</span><span class="sxs-lookup"><span data-stu-id="65240-141">tooadd a message tooa queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="65240-142">метод Hello принимает имя очереди hello, текст сообщения hello и параметры сообщения (которые не являются обязательными).</span><span class="sxs-lookup"><span data-stu-id="65240-142">hello method takes hello queue name, hello message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="65240-143">Просмотр следующего сообщения hello</span><span class="sxs-lookup"><span data-stu-id="65240-143">Peek at hello next message</span></span>
<span data-ttu-id="65240-144">Можно читать сообщения (или сообщения) в начале очереди hello не удаляет его из очереди hello путем вызова **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="65240-144">You can peek at a message (or messages) at hello front of a queue without removing it from hello queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="65240-145">По умолчанию hello **peekMessage** метод возвращает одно сообщение, но это значение можно изменить с помощью hello **PeekMessagesOptions -> setNumberOfMessages** метод.</span><span class="sxs-lookup"><span data-stu-id="65240-145">By default, hello **peekMessage** method returns a single message, but you can change that value by using hello **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="65240-146">Отмена очередь следующего сообщения hello</span><span class="sxs-lookup"><span data-stu-id="65240-146">De-queue hello next message</span></span>
<span data-ttu-id="65240-147">Ваш код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="65240-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="65240-148">Во-первых, можно вызвать **QueueRestProxy -> listMessages**, что делает невидимыми tooany сообщение hello другой код, который выполняет чтение из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="65240-148">First, you call **QueueRestProxy->listMessages**, which makes hello message invisible tooany other code that's reading from hello queue.</span></span> <span data-ttu-id="65240-149">По умолчанию это сообщение будет оставаться невидимым в течение 30 секунд</span><span class="sxs-lookup"><span data-stu-id="65240-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="65240-150">(Если приветственное сообщение не будет удалена в этот период времени, он будет видимым в очереди hello еще раз.) toofinish удаление приветственное сообщение из очереди hello, необходимо вызвать **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="65240-150">(If hello message is not deleted in this time period, it will become visible on hello queue again.) toofinish removing hello message from hello queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="65240-151">Это двухэтапный процесс удаления сообщения гарантирует, что при tooprocess завершается с ошибкой вашего кода, получит сообщение из-за toohardware или ошибок программного обеспечения, другой экземпляр кода hello же сообщение и повторите.</span><span class="sxs-lookup"><span data-stu-id="65240-151">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="65240-152">Вызовы кода **deleteMessage** сразу после обработки сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="65240-152">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="65240-153">Изменить содержимое hello сообщение из очереди</span><span class="sxs-lookup"><span data-stu-id="65240-153">Change hello contents of a queued message</span></span>
<span data-ttu-id="65240-154">Можно изменить содержимое сообщений на месте в очереди hello hello путем вызова **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="65240-154">You can change hello contents of a message in-place in hello queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="65240-155">Если сообщение hello представляет рабочей задачи, можно использовать этот компонент tooupdate hello состояние задачи рабочего hello.</span><span class="sxs-lookup"><span data-stu-id="65240-155">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="65240-156">После кода Hello обновляет приветственное сообщение очереди новое содержимое, и задает tooextend время ожидания видимости hello другой 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="65240-156">hello following code updates hello queue message with new contents, and it sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="65240-157">Это сохраняет состояние hello работы, связанной с приветственное сообщение, а также клиент hello другой минуты toocontinue работа на приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="65240-157">This saves hello state of work that's associated with hello message, and it gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="65240-158">Можно использовать этот рабочих процессов способ tootrack многоэтапной для очереди сообщений без необходимости toostart через от начала hello при неудачном завершении шага обработки из-за toohardware или ошибок программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="65240-158">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="65240-159">Как правило, будет хранить значение числа повторов, и если hello сообщение повторяется более  *n*  раз, следует удалить его.</span><span class="sxs-lookup"><span data-stu-id="65240-159">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="65240-160">Это обеспечивает защиту от сообщений, которые инициируют ошибку приложения при каждой попытке обработки.</span><span class="sxs-lookup"><span data-stu-id="65240-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="65240-161">Дополнительные параметры для удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="65240-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="65240-162">Существует два способа настройки извлечения сообщения из очереди.</span><span class="sxs-lookup"><span data-stu-id="65240-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="65240-163">Во-первых можно получить пакет сообщений (вверх too32).</span><span class="sxs-lookup"><span data-stu-id="65240-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="65240-164">Во-вторых можно задать время ожидания видимости длинный или короткий, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="65240-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="65240-165">Hello следующий пример кода использует hello **getMessages** метод tooget 16 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="65240-165">hello following code example uses hello **getMessages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="65240-166">Затем он обрабатывает каждое сообщение с помощью цикла **for** .</span><span class="sxs-lookup"><span data-stu-id="65240-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="65240-167">Он также устанавливает минут toofive hello невидимости время ожидания для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="65240-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="65240-168">Получение длины очереди</span><span class="sxs-lookup"><span data-stu-id="65240-168">Get queue length</span></span>
<span data-ttu-id="65240-169">Можно получить оценку hello количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="65240-169">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="65240-170">Hello **QueueRestProxy -> getQueueMetadata** метод запрашивает hello очереди службы tooreturn метаданные о hello очереди.</span><span class="sxs-lookup"><span data-stu-id="65240-170">hello **QueueRestProxy->getQueueMetadata** method asks hello queue service tooreturn metadata about hello queue.</span></span> <span data-ttu-id="65240-171">Вызов hello **getApproximateMessageCount** метода в hello возвращен объект предоставляет количество количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="65240-171">Calling hello **getApproximateMessageCount** method on hello returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="65240-172">число Hello приблизительное только в том случае, поскольку сообщения можно добавить или удалить после запроса tooyour отвечает hello службы очередей.</span><span class="sxs-lookup"><span data-stu-id="65240-172">hello count is only approximate because messages can be added or removed after hello queue service responds tooyour request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="65240-173">Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="65240-173">Delete a queue</span></span>
<span data-ttu-id="65240-174">toodelete очереди и все сообщения hello, вызовите hello **QueueRestProxy -> deleteQueue** метод.</span><span class="sxs-lookup"><span data-stu-id="65240-174">toodelete a queue and all hello messages in it, call hello **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="65240-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65240-175">Next steps</span></span>
<span data-ttu-id="65240-176">Теперь, когда вы узнали основы hello хранилища очередей Azure, выполните эти ссылки toolearn о более сложных задач хранилища.</span><span class="sxs-lookup"><span data-stu-id="65240-176">Now that you've learned hello basics of Azure Queue storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="65240-177">Посетите hello [блога группы разработчиков хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="65240-177">Visit hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="65240-178">Дополнительные сведения см. также: hello [Центр разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="65240-178">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

