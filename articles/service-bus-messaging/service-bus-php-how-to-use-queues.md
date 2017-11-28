---
title: "Как использовать очереди служебной шины с помощью PHP | Документация Майкрософт"
description: "Узнайте, как использовать очереди служебной шины в Azure. Примеры кода написаны на PHP."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3514812f7f087582035dad5d9a4d620652aa4da9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-php"></a><span data-ttu-id="1c48c-104">Как использовать очереди служебной шины с PHP</span><span class="sxs-lookup"><span data-stu-id="1c48c-104">How to use Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="1c48c-105">В этом руководстве показано, как использовать очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="1c48c-105">This guide shows you how to use Service Bus queues.</span></span> <span data-ttu-id="1c48c-106">Примеры написаны на PHP и используют [пакет Azure SDK для PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="1c48c-106">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="1c48c-107">Здесь описаны такие сценарии, как **создание очередей**, **отправка и получение сообщений**, а также **удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="1c48c-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="1c48c-108">Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="1c48c-108">Create a PHP application</span></span>
<span data-ttu-id="1c48c-109">Для создания приложения PHP, которое получает доступ к службе BLOB-объектов Azure, достаточно сослаться на классы в [пакете SDK Azure для PHP](../php-download-sdk.md) непосредственно из кода.</span><span class="sxs-lookup"><span data-stu-id="1c48c-109">The only requirement for creating a PHP application that accesses the Azure Blob service is the referencing of classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="1c48c-110">Для создания приложения можно использовать любые средства разработки или Блокнот.</span><span class="sxs-lookup"><span data-stu-id="1c48c-110">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="1c48c-111">В установленном пакете PHP должно быть установлено и включено [расширение OpenSSL](http://php.net/openssl).</span><span class="sxs-lookup"><span data-stu-id="1c48c-111">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="1c48c-112">В этом руководстве будут использоваться компоненты службы, которые могут быть вызваны локально или в коде из приложения PHP, работающем в веб-роли Azure, рабочей роли или на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="1c48c-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="1c48c-113">Получение клиентских библиотек Azure</span><span class="sxs-lookup"><span data-stu-id="1c48c-113">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="1c48c-114">Настройка приложения для использования служебной шины</span><span class="sxs-lookup"><span data-stu-id="1c48c-114">Configure your application to use Service Bus</span></span>
<span data-ttu-id="1c48c-115">Чтобы использовать интерфейсы API очередей служебной шины, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="1c48c-115">To use the Service Bus queue APIs, do the following:</span></span>

1. <span data-ttu-id="1c48c-116">Ссылка на файл автозагрузчика с использованием оператора [require_once][require_once].</span><span class="sxs-lookup"><span data-stu-id="1c48c-116">Reference the autoloader file using the [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="1c48c-117">Ссылка на любые классы, которые могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="1c48c-117">Reference any classes you might use.</span></span>

<span data-ttu-id="1c48c-118">В следующем примере показано, как включить файл автозагрузчика и добавить ссылку на класс `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="1c48c-118">The following example shows how to include the autoloader file and reference the `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="1c48c-119">В этом примере (и других примерах в этой статье) предполагается, что установлены клиентские библиотеки PHP для Azure с помощью Composer.</span><span class="sxs-lookup"><span data-stu-id="1c48c-119">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="1c48c-120">При установке библиотек вручную или в качестве пакета PEAR необходимо использовать ссылку на файл автозагрузчика **WindowsAzure.php**.</span><span class="sxs-lookup"><span data-stu-id="1c48c-120">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="1c48c-121">В приведенных ниже примерах всегда будет отображаться оператор `require_once`, однако ссылки будут приводиться только на классы, которые необходимы для выполнения этого примера.</span><span class="sxs-lookup"><span data-stu-id="1c48c-121">In the examples below, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="1c48c-122">Настройка подключения к Service Bus</span><span class="sxs-lookup"><span data-stu-id="1c48c-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="1c48c-123">Для создания клиента служебной шины необходимо сначала сформировать правильную строку подключения в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="1c48c-123">To instantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="1c48c-124">где `Endpoint` обычно имеет формат `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="1c48c-124">Where `Endpoint` is typically of the format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="1c48c-125">Для создания клиента службы Azure необходимо использовать класс `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="1c48c-125">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="1c48c-126">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="1c48c-126">You can:</span></span>

* <span data-ttu-id="1c48c-127">Передать строку подключения напрямую или</span><span class="sxs-lookup"><span data-stu-id="1c48c-127">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="1c48c-128">использовать **CloudConfigurationManager (CCM)** для проверки нескольких внешних источников на наличие строки подключения:</span><span class="sxs-lookup"><span data-stu-id="1c48c-128">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="1c48c-129">По умолчанию предоставляется поддержка одного внешнего источника — переменных среды.</span><span class="sxs-lookup"><span data-stu-id="1c48c-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="1c48c-130">Можно добавить новые источники, расширив класс `ConnectionStringSource`.</span><span class="sxs-lookup"><span data-stu-id="1c48c-130">You can add new sources by extending the `ConnectionStringSource` class</span></span>

<span data-ttu-id="1c48c-131">В приведенных здесь примерах строка подключения передается напрямую.</span><span class="sxs-lookup"><span data-stu-id="1c48c-131">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="1c48c-132">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="1c48c-132">Create a queue</span></span>
<span data-ttu-id="1c48c-133">Операции управления очередями служебной шины можно выполнять с помощью класса `ServiceBusRestProxy`.</span><span class="sxs-lookup"><span data-stu-id="1c48c-133">You can perform management operations for Service Bus queues via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="1c48c-134">Объект `ServiceBusRestProxy` создается посредством фабричного метода `ServicesBuilder::createServiceBusService` с соответствующей строкой подключения, инкапсулирующей в себе разрешения маркера на управление им.</span><span class="sxs-lookup"><span data-stu-id="1c48c-134">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="1c48c-135">В приведенном ниже примере показано, как создать экземпляр `ServiceBusRestProxy` и вызвать метод `ServiceBusRestProxy->createQueue` для создания очереди `myqueue` в пространстве имен службы `MySBNamespace`.</span><span class="sxs-lookup"><span data-stu-id="1c48c-135">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` to create a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="1c48c-136">Можно использовать метод `listQueues` для объектов `ServiceBusRestProxy`, чтобы проверить, существует ли уже очередь с указанным именем в пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="1c48c-136">You can use the `listQueues` method on `ServiceBusRestProxy` objects to check if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="1c48c-137">Отправка сообщений в очередь</span><span class="sxs-lookup"><span data-stu-id="1c48c-137">Send messages to a queue</span></span>
<span data-ttu-id="1c48c-138">Чтобы отправить сообщение в очередь служебной шины, в приложении вызывается метод `ServiceBusRestProxy->sendQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="1c48c-138">To send a message to a Service Bus queue, your application calls the `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="1c48c-139">В следующем примере кода показано, как отправить сообщение в очередь `myqueue`, созданную ранее в пространстве имен службы `MySBNamespace`.</span><span class="sxs-lookup"><span data-stu-id="1c48c-139">The following code shows how to send a message to the `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="1c48c-140">Сообщения, отправляемые в очереди служебной шины и получаемые из них, представляют собой экземпляры класса [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="1c48c-140">Messages sent to (and received from ) Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="1c48c-141">У объектов [BrokeredMessage][BrokeredMessage] есть набор стандартных методов и свойств, используемый для хранения настраиваемых свойств приложения, и текст из произвольных данных приложения.</span><span class="sxs-lookup"><span data-stu-id="1c48c-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used to hold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="1c48c-142">Очереди служебной шины поддерживают максимальный размер сообщения 256 КБ для [уровня "Стандартный"](service-bus-premium-messaging.md) и 1 МБ для [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="1c48c-142">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="1c48c-143">Максимальный размер заголовка, который содержит стандартные и настраиваемые свойства приложения, — 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="1c48c-143">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="1c48c-144">Ограничения на количество сообщений в очереди нет, но есть максимальный общий размер сообщений, содержащихся в очереди.</span><span class="sxs-lookup"><span data-stu-id="1c48c-144">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="1c48c-145">Максимальный размер очереди ограничен 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="1c48c-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="1c48c-146">Получение сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="1c48c-146">Receive messages from a queue</span></span>

<span data-ttu-id="1c48c-147">Наилучшим способом получать сообщения из очереди является использование метода `ServiceBusRestProxy->receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="1c48c-147">The best way to receive messages from a queue is to use a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="1c48c-148">Сообщения можно получать в двух различных режимах: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) и [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="1c48c-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="1c48c-149">Значение по умолчанию — **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="1c48c-149">**PeekLock** is the default.</span></span>

<span data-ttu-id="1c48c-150">В режиме [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) получение является одиночной операцией. Это значит, что когда служебная шина получает запрос на чтение для сообщения в очереди, это сообщение помечается как использованное и возвращается в приложение.</span><span class="sxs-lookup"><span data-stu-id="1c48c-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="1c48c-151">Режим [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) представляет собой самую простую модель, которая лучше всего работает в ситуациях, когда приложение может не обрабатывать сообщение при сбое.</span><span class="sxs-lookup"><span data-stu-id="1c48c-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="1c48c-152">Чтобы это понять, рассмотрим сценарий, в котором объект-получатель выдает запрос на получение и выходит из строя до его обработки.</span><span class="sxs-lookup"><span data-stu-id="1c48c-152">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="1c48c-153">Поскольку служебная шина помечает сообщение как использованное, то когда после своего перезапуска приложение снова начнет обрабатывать сообщения, оно пропустит сообщение, использованное до сбоя.</span><span class="sxs-lookup"><span data-stu-id="1c48c-153">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="1c48c-154">В используемом по умолчанию режиме [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) процесс получения становится двухэтапной операцией, что позволяет поддерживать приложения, не устойчивые к пропуску сообщений.</span><span class="sxs-lookup"><span data-stu-id="1c48c-154">In the default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="1c48c-155">Получив запрос, Service Bus находит следующее сообщение, блокирует его, чтобы другие получатели не могли его принять, а затем возвращает его приложению.</span><span class="sxs-lookup"><span data-stu-id="1c48c-155">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="1c48c-156">Когда приложение завершает обработку сообщения (или сохраняет его для будущей обработки), оно завершает второй этап процесса получения, вызывая метод `ServiceBusRestProxy->deleteMessage` для полученного сообщения.</span><span class="sxs-lookup"><span data-stu-id="1c48c-156">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="1c48c-157">Когда служебная шина обнаруживает вызов метода `deleteMessage`, она помечает сообщение как использованное и удаляет его из очереди.</span><span class="sxs-lookup"><span data-stu-id="1c48c-157">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="1c48c-158">В следующем примере показывается, как получать и обрабатывать сообщения с помощью режима [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) (используется по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="1c48c-158">The following example shows how to receive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (the default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set the receive mode to PeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="1c48c-159">Как обрабатывать сбои приложения и нечитаемые сообщения</span><span class="sxs-lookup"><span data-stu-id="1c48c-159">How to handle application crashes and unreadable messages</span></span>

<span data-ttu-id="1c48c-160">служебная шина предоставляет функции, помогающие корректно выполнить восстановление после ошибок в приложении или трудностей, возникших при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="1c48c-160">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="1c48c-161">Если приложение-получатель по каким-либо причинам не может обработать сообщение, то оно может вызвать метод `unlockMessage` для полученного сообщения (вместо метода `deleteMessage`).</span><span class="sxs-lookup"><span data-stu-id="1c48c-161">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="1c48c-162">После этого служебная шина разблокирует сообщение в очереди и сделает его доступным для приема тем же приложением или другим приложением.</span><span class="sxs-lookup"><span data-stu-id="1c48c-162">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="1c48c-163">Кроме того, с сообщением, заблокированным в очереди, связано время ожидания. Если приложение не сможет обработать сообщение в течение времени ожидания (например, при сбое приложения), служебная шина разблокирует сообщение автоматически и сделает его доступным для приема.</span><span class="sxs-lookup"><span data-stu-id="1c48c-163">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="1c48c-164">Если сбой приложения происходит после обработки сообщения, но перед отправкой запроса `deleteMessage`, то это сообщение повторно доставляется в приложение после его перезапуска.</span><span class="sxs-lookup"><span data-stu-id="1c48c-164">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="1c48c-165">Часто такой подход называют *Обработать хотя бы один раз*, т. е. каждое сообщение будет обрабатываться по крайней мере один раз, но в некоторых случаях это же сообщение может быть доставлено повторно.</span><span class="sxs-lookup"><span data-stu-id="1c48c-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="1c48c-166">Если повторная обработка недопустима, рекомендуется добавить в приложение дополнительную логику для обработки повторной доставки сообщений.</span><span class="sxs-lookup"><span data-stu-id="1c48c-166">If the scenario cannot tolerate duplicate processing, then adding additional logic to applications to handle duplicate message delivery is recommended.</span></span> <span data-ttu-id="1c48c-167">Часто это достигается с помощью метода `getMessageId` сообщения, который остается постоянным для различных попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="1c48c-167">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c48c-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c48c-168">Next steps</span></span>
<span data-ttu-id="1c48c-169">Вы ознакомились с основами использования очередей служебной шины. Дополнительные сведения см. в статье [Очереди, разделы и подписки служебной шины][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="1c48c-169">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="1c48c-170">Дополнительные сведения также доступны в [Центре разработчика PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="1c48c-170">For more information, also visit the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


