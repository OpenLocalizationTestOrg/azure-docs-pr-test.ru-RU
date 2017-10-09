---
title: "Помещает в очередь aaaHow toouse служебной шины с PHP | Документы Microsoft"
description: "Узнайте, как очереди toouse Service Bus в Azure. Примеры кода написаны на PHP."
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
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a><span data-ttu-id="ce0fc-104">Как очереди toouse служебной шины с PHP</span><span class="sxs-lookup"><span data-stu-id="ce0fc-104">How toouse Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="ce0fc-105">В этом руководстве показано, как toouse очереди Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-105">This guide shows you how toouse Service Bus queues.</span></span> <span data-ttu-id="ce0fc-106">Hello примеры написаны на PHP и использовать hello [пакет Azure SDK для PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="ce0fc-106">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="ce0fc-107">Hello сценарии включают **создание очередей**, **отправки и получения сообщений**, и **удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="ce0fc-108">Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="ce0fc-108">Create a PHP application</span></span>
<span data-ttu-id="ce0fc-109">Здравствуйте, используется только для создания приложения PHP, которое обращается к службе BLOB-объектов Azure hello hello ссылки на классы в hello [пакет Azure SDK для PHP](../php-download-sdk.md) из кода.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-109">hello only requirement for creating a PHP application that accesses hello Azure Blob service is hello referencing of classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="ce0fc-110">Можно использовать любой toocreate средства разработки приложения или «Блокнот».</span><span class="sxs-lookup"><span data-stu-id="ce0fc-110">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="ce0fc-111">Установку PHP также должен иметь hello [OpenSSL расширения](http://php.net/openssl) установлен и включен.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-111">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="ce0fc-112">В этом руководстве будут использоваться компоненты службы, которые могут быть вызваны локально или в коде из приложения PHP, работающем в веб-роли Azure, рабочей роли или на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="ce0fc-113">Получить hello клиентских библиотек Azure</span><span class="sxs-lookup"><span data-stu-id="ce0fc-113">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="ce0fc-114">Настройка вашего приложения toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="ce0fc-114">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="ce0fc-115">очередь Service Bus hello toouse API-интерфейсы, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="ce0fc-115">toouse hello Service Bus queue APIs, do hello following:</span></span>

1. <span data-ttu-id="ce0fc-116">Файл автозагрузчика hello ссылка, с помощью hello [require_once] [ require_once] инструкции.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-116">Reference hello autoloader file using hello [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="ce0fc-117">Ссылка на любые классы, которые могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-117">Reference any classes you might use.</span></span>

<span data-ttu-id="ce0fc-118">Hello следующем примере показано, как tooinclude hello автозагрузчика файла и ссылку hello `ServicesBuilder` класса.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-118">hello following example shows how tooinclude hello autoloader file and reference hello `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="ce0fc-119">В этом примере (и другие примеры в этой статье) предполагается, что вы установили hello PHP клиентские библиотеки для Azure через редактор.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-119">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="ce0fc-120">При установке библиотеки hello вручную или в виде пакета ГРУШИ необходимо сослаться на hello **WindowsAzure.php** автозагрузчика файла.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-120">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="ce0fc-121">В ниже примерах hello, hello `require_once` всегда будут отображаться инструкции, но указываются только классы hello, необходимые для tooexecute пример hello.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-121">In hello examples below, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="ce0fc-122">Настройка подключения к Service Bus</span><span class="sxs-lookup"><span data-stu-id="ce0fc-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="ce0fc-123">tooinstantiate клиента служебной шины, сначала нужно допустимую строку соединения в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="ce0fc-123">tooinstantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="ce0fc-124">Где `Endpoint` обычно имеет формат hello `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-124">Where `Endpoint` is typically of hello format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="ce0fc-125">toocreate любого клиента службы Azure, необходимо использовать hello `ServicesBuilder` класса.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-125">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="ce0fc-126">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="ce0fc-126">You can:</span></span>

* <span data-ttu-id="ce0fc-127">Передайте hello подключения tooit строки напрямую.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-127">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="ce0fc-128">использовать hello **CloudConfigurationManager (CCM)** toocheck нескольких внешних источников для hello строки подключения:</span><span class="sxs-lookup"><span data-stu-id="ce0fc-128">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="ce0fc-129">По умолчанию предоставляется поддержка одного внешнего источника — переменных среды.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="ce0fc-130">Можно добавлять новые источники, расширяя hello `ConnectionStringSource` класса</span><span class="sxs-lookup"><span data-stu-id="ce0fc-130">You can add new sources by extending hello `ConnectionStringSource` class</span></span>

<span data-ttu-id="ce0fc-131">Приведенные ниже примеры hello hello строка подключения передается напрямую.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-131">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="ce0fc-132">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="ce0fc-132">Create a queue</span></span>
<span data-ttu-id="ce0fc-133">Вы можете выполнять операции управления для очереди Service Bus через hello `ServiceBusRestProxy` класса.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-133">You can perform management operations for Service Bus queues via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="ce0fc-134">Объект `ServiceBusRestProxy` через hello создается объект `ServicesBuilder::createServiceBusService` фабричный метод со строкой соединения, соответствующую, инкапсулирующий hello маркера разрешения toomanage его.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-134">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="ce0fc-135">Следующий пример показывает как Hello tooinstantiate `ServiceBusRestProxy` и вызвать `ServiceBusRestProxy->createQueue` toocreate очередь с именем `myqueue` в `MySBNamespace` пространства имен службы:</span><span class="sxs-lookup"><span data-stu-id="ce0fc-135">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` toocreate a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

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
> <span data-ttu-id="ce0fc-136">Можно использовать hello `listQueues` метод `ServiceBusRestProxy` объектов toocheck, если очередь с указанным именем уже существует в пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-136">You can use hello `listQueues` method on `ServiceBusRestProxy` objects toocheck if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="ce0fc-137">Отправка сообщений в очереди tooa</span><span class="sxs-lookup"><span data-stu-id="ce0fc-137">Send messages tooa queue</span></span>
<span data-ttu-id="ce0fc-138">toosend очередью сообщений tooa Service Bus, приложение вызывает hello `ServiceBusRestProxy->sendQueueMessage` метод.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-138">toosend a message tooa Service Bus queue, your application calls hello `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="ce0fc-139">Здравствуйте, как следующий код показывает toosend toohello сообщение `myqueue` очереди, созданной ранее в `MySBNamespace` пространства имен службы.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-139">hello following code shows how toosend a message toohello `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="ce0fc-140">Сообщения, отправленного слишком (и, полученных от) очереди шины обслуживания являются экземплярами hello [BrokeredMessage] [ BrokeredMessage] класса.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-140">Messages sent too(and received from ) Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="ce0fc-141">[BrokeredMessage] [ BrokeredMessage] объекты имеют ряд стандартных методов и свойств, используемых toohold пользовательские свойства для конкретного приложения и текст из произвольных данных приложения.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used toohold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="ce0fc-142">Очереди шины обслуживания поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="ce0fc-142">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="ce0fc-143">Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-143">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="ce0fc-144">Нет ограничений на число hello сообщения помещаются в очередь, но отсутствует ограничение на общий размер сообщений hello, хранящиеся в очереди hello.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-144">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="ce0fc-145">Максимальный размер очереди ограничен 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="ce0fc-146">Получение сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="ce0fc-146">Receive messages from a queue</span></span>

<span data-ttu-id="ce0fc-147">Hello лучшим способом tooreceive сообщений из очереди — toouse `ServiceBusRestProxy->receiveQueueMessage` метод.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-147">hello best way tooreceive messages from a queue is toouse a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="ce0fc-148">Сообщения можно получать в двух различных режимах: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) и [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="ce0fc-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="ce0fc-149">**PeekLock** по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-149">**PeekLock** is hello default.</span></span>

<span data-ttu-id="ce0fc-150">При использовании [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) режиме получение является единовременной операцией; то есть, когда Service Bus получает запросы на чтение для сообщения в очереди, он помечает приветственное сообщение как полученное и возвращает его toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="ce0fc-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) режим — самая простая модель hello и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="ce0fc-152">toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-152">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="ce0fc-153">Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-153">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="ce0fc-154">По умолчанию hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) режим, получает сообщение становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-154">In hello default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="ce0fc-155">Service Bus, получив запрос, он выполняет поиск следующего сообщения toobe hello потребляет, блокирует его tooprevent других потребителей получать и возвращает его toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-155">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="ce0fc-156">После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения, передавая сообщение hello получено слишком`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-156">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="ce0fc-157">Когда Service Bus обнаруживает hello `deleteMessage` вызов, он пометить приветственное сообщение как полученное и удалите его из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-157">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="ce0fc-158">Следующий пример показывает как Hello tooreceive и обрабатывать сообщения с помощью [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) режиме (режим по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="ce0fc-158">hello following example shows how tooreceive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (hello default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="ce0fc-159">Как происходит сбой toohandle приложения и может быть прочитан сообщений</span><span class="sxs-lookup"><span data-stu-id="ce0fc-159">How toohandle application crashes and unreadable messages</span></span>

<span data-ttu-id="ce0fc-160">Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-160">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="ce0fc-161">Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlockMessage` метод для получения приветственное сообщение (вместо hello `deleteMessage` метода).</span><span class="sxs-lookup"><span data-stu-id="ce0fc-161">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="ce0fc-162">Это будет вызвать Service Bus toounlock приветственное сообщение в очередь hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-162">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="ce0fc-163">Также существует время ожидания, связанные с сообщением, заблокировать в течение hello очереди, и при сбое приложения hello tooprocess приветственное сообщение, прежде чем hello срок блокировки (например, если приложение hello терпит сбой), разблокируйте Service Bus приветственное сообщение автоматически и сделать ее доступной toobe получили еще раз.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-163">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="ce0fc-164">В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `deleteMessage` выдается запрос, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-164">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="ce0fc-165">Это часто называется *как минимум один раз* обработки; то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="ce0fc-166">Если сценарий hello не допускает обработку дубликатов, а затем добавление дополнительного рекомендуется логика tooapplications toohandle повторной доставке сообщений.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-166">If hello scenario cannot tolerate duplicate processing, then adding additional logic tooapplications toohandle duplicate message delivery is recommended.</span></span> <span data-ttu-id="ce0fc-167">Это можно сделать с помощью hello `getMessageId` метод приветственное сообщение, остается постоянным на протяжении всех попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-167">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce0fc-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ce0fc-168">Next steps</span></span>
<span data-ttu-id="ce0fc-169">Теперь, когда вы узнали основы hello очереди шины обслуживания, в разделе [очереди, разделы и подписки] [ Queues, topics, and subscriptions] для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="ce0fc-169">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="ce0fc-170">Для получения дополнительной информации посетите также hello [Центр разработчика PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="ce0fc-170">For more information, also visit hello [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


