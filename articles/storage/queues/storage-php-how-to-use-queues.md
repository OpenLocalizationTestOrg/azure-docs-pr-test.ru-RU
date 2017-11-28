---
title: "Как использовать хранилище очередей из PHP | Документация Майкрософт"
description: "Узнайте, как создавать и удалять очереди, а также вставлять, получать и удалять сообщения с помощью службы хранилища очередей Azure. Примеры написаны на PHP."
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
ms.openlocfilehash: 12ebb905184e74da534cd44e8314335145f7042d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-php"></a><span data-ttu-id="fcdbe-104">Использование хранилища очередей из PHP</span><span class="sxs-lookup"><span data-stu-id="fcdbe-104">How to use Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="fcdbe-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="fcdbe-105">Overview</span></span>
<span data-ttu-id="fcdbe-106">В этом руководстве показано, как реализовать типичные сценарии с использованием службы хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span></span> <span data-ttu-id="fcdbe-107">Примеры написаны с использованием классов из пакета SDK для Windows для PHP.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-107">The samples are written via classes from the Windows SDK for PHP.</span></span> <span data-ttu-id="fcdbe-108">Здесь описаны такие сценарии, как вставка, просмотр, получение и удаление сообщений очереди, а также создание и удаление очередей.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="fcdbe-109">Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="fcdbe-109">Create a PHP application</span></span>
<span data-ttu-id="fcdbe-110">Единственным требованием для создания приложения PHP, которое получает доступ к хранилищу очередей Azure, является ссылка на классы в пакете SDK для Azure для PHP непосредственно из кода.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="fcdbe-111">Можно использовать любые средства разработки для создания приложения, включая программу "Блокнот".</span><span class="sxs-lookup"><span data-stu-id="fcdbe-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="fcdbe-112">В этом руководстве будут использоваться компоненты хранилища очередей, которые могут быть вызваны локально в приложении PHP или в коде, работающем в веб-роли, рабочей роли или на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="fcdbe-113">Получение клиентских библиотек Azure</span><span class="sxs-lookup"><span data-stu-id="fcdbe-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="fcdbe-114">Настройка приложения для доступа к хранилищу очередей</span><span class="sxs-lookup"><span data-stu-id="fcdbe-114">Configure your application to access Queue storage</span></span>
<span data-ttu-id="fcdbe-115">Чтобы использовать интерфейсы API для хранилища очередей Azure, требуется:</span><span class="sxs-lookup"><span data-stu-id="fcdbe-115">To use the APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="fcdbe-116">Ссылка на файл автозагрузчика с использованием оператора [require_once].</span><span class="sxs-lookup"><span data-stu-id="fcdbe-116">Reference the autoloader file by using the [require_once] statement.</span></span>
2. <span data-ttu-id="fcdbe-117">Ссылка на любые классы, которые могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="fcdbe-118">В следующем примере показано, как включить файл автозагрузчика и сослаться на класс **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="fcdbe-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="fcdbe-119">В этом примере (и других примерах в этой статье) предполагается, что установлены клиентские библиотеки PHP для Azure с помощью Composer.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="fcdbe-120">Если вы установили эти библиотеки вручную, то потребуется добавить ссылку на файл автозагрузчика `WindowsAzure.php` .</span><span class="sxs-lookup"><span data-stu-id="fcdbe-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="fcdbe-121">В приведенных ниже примерах всегда будет отображаться оператор `require_once` , но ссылки будут приводиться только на классы, которые необходимы для выполнения этого примера.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="fcdbe-122">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="fcdbe-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="fcdbe-123">Чтобы создать экземпляр клиента хранилища очередей Azure, сначала необходимо сформировать правильную строку подключения.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="fcdbe-124">Формат строки подключения к службе очередей:</span><span class="sxs-lookup"><span data-stu-id="fcdbe-124">The format for the queue service connection string is as follows.</span></span>

<span data-ttu-id="fcdbe-125">Для доступа к службе в режиме реального времени:</span><span class="sxs-lookup"><span data-stu-id="fcdbe-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="fcdbe-126">Для доступа к хранилищу эмулятора:</span><span class="sxs-lookup"><span data-stu-id="fcdbe-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="fcdbe-127">Чтобы создать клиент службы Azure, необходимо использовать класс **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="fcdbe-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="fcdbe-128">Для этого можно использовать один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-128">You can use either of the following techniques:</span></span>

* <span data-ttu-id="fcdbe-129">Передать строку подключения напрямую или</span><span class="sxs-lookup"><span data-stu-id="fcdbe-129">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="fcdbe-130">Использовать **CloudConfigurationManager (CCM)** для проверки нескольких внешних источников на наличие строки подключения.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="fcdbe-131">По умолчанию предоставляется поддержка одного внешнего источника — переменных среды.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="fcdbe-132">Можно добавить новые источники, расширив класс **ConnectionStringSource** .</span><span class="sxs-lookup"><span data-stu-id="fcdbe-132">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="fcdbe-133">В приведенных здесь примерах строка подключения передается напрямую.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="fcdbe-134">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="fcdbe-134">Create a queue</span></span>
<span data-ttu-id="fcdbe-135">Объект **QueueRestProxy** позволяет создать очередь с помощью метода **createQueue**.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span></span> <span data-ttu-id="fcdbe-136">При создании очереди можно задать ее параметры, однако это не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-136">When creating a queue, you can set options on the queue, but doing so is not required.</span></span> <span data-ttu-id="fcdbe-137">(В приведенном ниже примере показано, как задать метаданные в очереди.)</span><span class="sxs-lookup"><span data-stu-id="fcdbe-137">(The example below shows how to set metadata on a queue.)</span></span>

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
> <span data-ttu-id="fcdbe-138">Не следует полагаться на учет регистра для ключей метаданных.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="fcdbe-139">Все параметры считываются из службы в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-139">All keys are read from the service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="fcdbe-140">Добавление сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="fcdbe-140">Add a message to a queue</span></span>
<span data-ttu-id="fcdbe-141">Чтобы добавить сообщение в очередь, используйте **QueueRestProxy->createMessage**.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="fcdbe-142">Этот метод принимает имя очереди, текст сообщения и параметры сообщения (которые не являются обязательными).</span><span class="sxs-lookup"><span data-stu-id="fcdbe-142">The method takes the queue name, the message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-the-next-message"></a><span data-ttu-id="fcdbe-143">Просмотр следующего сообщения</span><span class="sxs-lookup"><span data-stu-id="fcdbe-143">Peek at the next message</span></span>
<span data-ttu-id="fcdbe-144">Вы можете просмотреть сообщение (или сообщения) в начале очереди, не удаляя его из очереди, вызвав метод **QueueRestProxy->peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="fcdbe-145">По умолчанию метод **peekMessage** возвращает одно сообщение, но это значение можно изменить с помощью метода **PeekMessagesOptions->setNumberOfMessages**.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-the-next-message"></a><span data-ttu-id="fcdbe-146">Удаление следующего сообщения из очереди</span><span class="sxs-lookup"><span data-stu-id="fcdbe-146">De-queue the next message</span></span>
<span data-ttu-id="fcdbe-147">Ваш код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="fcdbe-148">Во-первых, вызовите метод **QueueRestProxy->listMessages**, который делает сообщение невидимым для любого другого кода, который считывает данные из очереди.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span></span> <span data-ttu-id="fcdbe-149">По умолчанию это сообщение будет оставаться невидимым в течение 30 секунд</span><span class="sxs-lookup"><span data-stu-id="fcdbe-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="fcdbe-150">(если за это время сообщение не будет удалено, оно снова станет видимым в очереди). Чтобы завершить удаление сообщения из очереди, необходимо вызвать **QueueRestProxy->deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="fcdbe-151">Этот двухэтапный процесс удаления сообщения позволяет удостовериться, что если коду не удастся обработать сообщение из-за сбоя оборудования или программного обеспечения, другой экземпляр кода сможет получить то же сообщение и повторить попытку.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="fcdbe-152">Код вызывает метод **deleteMessage** сразу после обработки сообщения.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-152">Your code calls **deleteMessage** right after the message has been processed.</span></span>

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

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="fcdbe-153">Изменение содержимого сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="fcdbe-153">Change the contents of a queued message</span></span>
<span data-ttu-id="fcdbe-154">Вы можете изменить содержимое сообщения непосредственно в очереди, вызвав **QueueRestProxy->updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="fcdbe-155">Если сообщение представляет собой рабочую задачу, можно использовать эту функцию для обновления состояния рабочей задачи.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-155">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="fcdbe-156">Следующий код добавляет новое содержимое в сообщение очереди и продлевает время ожидания видимости еще на 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="fcdbe-157">Это сохраняет состояние работы, связанной с данным сообщением, и позволяет клиенту продолжить работу с сообщением на протяжении еще одной минуты.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="fcdbe-158">Этот метод можно использовать для отслеживания многошаговых рабочих процессов по сообщениям в очереди без необходимости начинать с самого начала в случае сбоя шага обработки в связи с ошибкой аппаратного или программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="fcdbe-159">Обычно также сохраняется счетчик повторов. Если количество повторов сообщения превысит *n* раз, его нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="fcdbe-160">Это обеспечивает защиту от сообщений, которые инициируют ошибку приложения при каждой попытке обработки.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="fcdbe-161">Дополнительные параметры для удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="fcdbe-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="fcdbe-162">Существует два способа настройки извлечения сообщения из очереди.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="fcdbe-163">Во-первых, можно получить пакет сообщений (до 32 сообщений).</span><span class="sxs-lookup"><span data-stu-id="fcdbe-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="fcdbe-164">Во-вторых, можно задать более длительное или короткое время ожидания видимости, чтобы предоставить коду больше или меньше времени на полную обработку каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="fcdbe-165">В следующем примере кода метод **getMessages** используется для получения 16 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span></span> <span data-ttu-id="fcdbe-166">Затем он обрабатывает каждое сообщение с помощью цикла **for** .</span><span class="sxs-lookup"><span data-stu-id="fcdbe-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="fcdbe-167">Он также задает время ожидания невидимости 5 минут для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-167">It also sets the invisibility timeout to five minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="fcdbe-168">Получение длины очереди</span><span class="sxs-lookup"><span data-stu-id="fcdbe-168">Get queue length</span></span>
<span data-ttu-id="fcdbe-169">Вы можете узнать приблизительное количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-169">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="fcdbe-170">Метод **QueueRestProxy->getQueueMetadata** запрашивает у службы очередей метаданные очереди.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span></span> <span data-ttu-id="fcdbe-171">Вызов метода **getApproximateMessageCount** для возвращенного объекта позволяет получить количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="fcdbe-172">Счетчик указывает число лишь приблизительно, так как сообщения могут добавляться или удаляться после ответа службы очередей на ваш запрос.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="fcdbe-173">Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="fcdbe-173">Delete a queue</span></span>
<span data-ttu-id="fcdbe-174">Чтобы удалить очередь и все сообщения в ней, вызовите метод **QueueRestProxy->deleteQueue**.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fcdbe-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fcdbe-175">Next steps</span></span>
<span data-ttu-id="fcdbe-176">Вы изучили основную информацию о хранилище очередей Azure. Дополнительную информацию о более сложных задачах по использованию хранилища можно найти по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="fcdbe-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="fcdbe-177">Посетите [блог команды разработчиков службы хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="fcdbe-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="fcdbe-178">Дополнительную информацию можно найти также в [Центре разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="fcdbe-178">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

