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
# <a name="how-toouse-service-bus-queues-with-php"></a>Как очереди toouse служебной шины с PHP
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

В этом руководстве показано, как toouse очереди Service Bus. Hello примеры написаны на PHP и использовать hello [пакет Azure SDK для PHP](../php-download-sdk.md). Hello сценарии включают **создание очередей**, **отправки и получения сообщений**, и **удаление очередей**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a>Создание приложения PHP
Здравствуйте, используется только для создания приложения PHP, которое обращается к службе BLOB-объектов Azure hello hello ссылки на классы в hello [пакет Azure SDK для PHP](../php-download-sdk.md) из кода. Можно использовать любой toocreate средства разработки приложения или «Блокнот».

> [!NOTE]
> Установку PHP также должен иметь hello [OpenSSL расширения](http://php.net/openssl) установлен и включен.
> 
> 

В этом руководстве будут использоваться компоненты службы, которые могут быть вызваны локально или в коде из приложения PHP, работающем в веб-роли Azure, рабочей роли или на веб-сайте Azure.

## <a name="get-hello-azure-client-libraries"></a>Получить hello клиентских библиотек Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Настройка вашего приложения toouse Service Bus
очередь Service Bus hello toouse API-интерфейсы, hello следующие:

1. Файл автозагрузчика hello ссылка, с помощью hello [require_once] [ require_once] инструкции.
2. Ссылка на любые классы, которые могут использоваться.

Hello следующем примере показано, как tooinclude hello автозагрузчика файла и ссылку hello `ServicesBuilder` класса.

> [!NOTE]
> В этом примере (и другие примеры в этой статье) предполагается, что вы установили hello PHP клиентские библиотеки для Azure через редактор. При установке библиотеки hello вручную или в виде пакета ГРУШИ необходимо сослаться на hello **WindowsAzure.php** автозагрузчика файла.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

В ниже примерах hello, hello `require_once` всегда будут отображаться инструкции, но указываются только классы hello, необходимые для tooexecute пример hello.

## <a name="set-up-a-service-bus-connection"></a>Настройка подключения к Service Bus
tooinstantiate клиента служебной шины, сначала нужно допустимую строку соединения в следующем формате:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Где `Endpoint` обычно имеет формат hello `[yourNamespace].servicebus.windows.net`.

toocreate любого клиента службы Azure, необходимо использовать hello `ServicesBuilder` класса. Вы можете:

* Передайте hello подключения tooit строки напрямую.
* использовать hello **CloudConfigurationManager (CCM)** toocheck нескольких внешних источников для hello строки подключения:
  * По умолчанию предоставляется поддержка одного внешнего источника — переменных среды.
  * Можно добавлять новые источники, расширяя hello `ConnectionStringSource` класса

Приведенные ниже примеры hello hello строка подключения передается напрямую.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a>Создание очереди
Вы можете выполнять операции управления для очереди Service Bus через hello `ServiceBusRestProxy` класса. Объект `ServiceBusRestProxy` через hello создается объект `ServicesBuilder::createServiceBusService` фабричный метод со строкой соединения, соответствующую, инкапсулирующий hello маркера разрешения toomanage его.

Следующий пример показывает как Hello tooinstantiate `ServiceBusRestProxy` и вызвать `ServiceBusRestProxy->createQueue` toocreate очередь с именем `myqueue` в `MySBNamespace` пространства имен службы:

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
> Можно использовать hello `listQueues` метод `ServiceBusRestProxy` объектов toocheck, если очередь с указанным именем уже существует в пространстве имен.
> 
> 

## <a name="send-messages-tooa-queue"></a>Отправка сообщений в очереди tooa
toosend очередью сообщений tooa Service Bus, приложение вызывает hello `ServiceBusRestProxy->sendQueueMessage` метод. Здравствуйте, как следующий код показывает toosend toohello сообщение `myqueue` очереди, созданной ранее в `MySBNamespace` пространства имен службы.

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

Сообщения, отправленного слишком (и, полученных от) очереди шины обслуживания являются экземплярами hello [BrokeredMessage] [ BrokeredMessage] класса. [BrokeredMessage] [ BrokeredMessage] объекты имеют ряд стандартных методов и свойств, используемых toohold пользовательские свойства для конкретного приложения и текст из произвольных данных приложения.

Очереди шины обслуживания поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md). Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ. Нет ограничений на число hello сообщения помещаются в очередь, но отсутствует ограничение на общий размер сообщений hello, хранящиеся в очереди hello. Максимальный размер очереди ограничен 5 ГБ.

## <a name="receive-messages-from-a-queue"></a>Получение сообщений из очереди

Hello лучшим способом tooreceive сообщений из очереди — toouse `ServiceBusRestProxy->receiveQueueMessage` метод. Сообщения можно получать в двух различных режимах: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) и [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock). **PeekLock** по умолчанию hello.

При использовании [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) режиме получение является единовременной операцией; то есть, когда Service Bus получает запросы на чтение для сообщения в очереди, он помечает приветственное сообщение как полученное и возвращает его toohello приложения. [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) режим — самая простая модель hello и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя. toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки. Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.

По умолчанию hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) режим, получает сообщение становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения. Service Bus, получив запрос, он выполняет поиск следующего сообщения toobe hello потребляет, блокирует его tooprevent других потребителей получать и возвращает его toohello приложения. После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения, передавая сообщение hello получено слишком`ServiceBusRestProxy->deleteMessage`. Когда Service Bus обнаруживает hello `deleteMessage` вызов, он пометить приветственное сообщение как полученное и удалите его из очереди hello.

Следующий пример показывает как Hello tooreceive и обрабатывать сообщения с помощью [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) режиме (режим по умолчанию hello).

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Как происходит сбой toohandle приложения и может быть прочитан сообщений

Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения. Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlockMessage` метод для получения приветственное сообщение (вместо hello `deleteMessage` метода). Это будет вызвать Service Bus toounlock приветственное сообщение в очередь hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.

Также существует время ожидания, связанные с сообщением, заблокировать в течение hello очереди, и при сбое приложения hello tooprocess приветственное сообщение, прежде чем hello срок блокировки (например, если приложение hello терпит сбой), разблокируйте Service Bus приветственное сообщение автоматически и сделать ее доступной toobe получили еще раз.

В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `deleteMessage` выдается запрос, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения. Это часто называется *как минимум один раз* обработки; то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, а затем добавление дополнительного рекомендуется логика tooapplications toohandle повторной доставке сообщений. Это можно сделать с помощью hello `getMessageId` метод приветственное сообщение, остается постоянным на протяжении всех попыток доставки.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello очереди шины обслуживания, в разделе [очереди, разделы и подписки] [ Queues, topics, and subscriptions] для получения дополнительной информации.

Для получения дополнительной информации посетите также hello [Центр разработчика PHP](https://azure.microsoft.com/develop/php/).

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


