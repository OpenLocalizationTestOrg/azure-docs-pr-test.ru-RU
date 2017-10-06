---
title: "темы Service Bus toouse aaaHow с PHP | Документы Microsoft"
description: "Узнайте, как toouse разделы служебной шины с PHP в Azure."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: 0ca8625fa3edc5854c0d6c1c2f6adab6a2d42f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a>Как toouse Service Bus разделов и подписок с PHP

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

В этой статье показано, как toouse Service Bus разделы и подписки. Hello примеры написаны на PHP и использовать hello [пакет Azure SDK для PHP](../php-download-sdk.md). Hello сценарии включают **создания разделов и подписок**, **создание фильтров подписок**, **отправки темы о сообщениях tooa**, **получения сообщения из подписки**, и **удаление разделов и подписок**.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a>Создание приложения PHP
Здравствуйте, только классы tooreference hello является обязательным условием для создания приложения PHP, которое обращается к службе BLOB-объектов Azure hello [пакет Azure SDK для PHP](../php-download-sdk.md) из кода. Можно использовать любой toocreate средства разработки приложения или «Блокнот».

> [!NOTE]
> Установку PHP также должен иметь hello [OpenSSL расширения](http://php.net/openssl) установлен и включен.
> 
> 

В этой статье описывается, как toouse службы компонентов, которые могут быть вызваны в рамках приложения PHP локально или в код, выполняющийся в Azure веб-роли, рабочей роли или веб-сайта.

## <a name="get-hello-azure-client-libraries"></a>Получить hello клиентских библиотек Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Настройка вашего приложения toouse Service Bus
hello toouse интерфейсов API служебной шины:

1. Файл автозагрузчика hello ссылка, с помощью hello [require_once] [ require-once] инструкции.
2. Ссылка на любые классы, которые могут использоваться.

Hello следующем примере показано, как tooinclude hello автозагрузчика файла и ссылку hello **ServiceBusService** класса.

> [!NOTE]
> В этом примере (и другие примеры в этой статье) предполагается, что вы установили hello PHP клиентские библиотеки для Azure через редактор. При установке библиотеки hello вручную или в виде пакета ГРУШИ необходимо сослаться на hello **WindowsAzure.php** автозагрузчика файла.
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

В следующих примерах hello, hello `require_once` всегда будут отображаться инструкции, но указываются только классы hello, необходимые для tooexecute пример hello.

## <a name="set-up-a-service-bus-connection"></a>Настройка подключения к Service Bus
tooinstantiate клиента Service Bus, необходимо сначала иметь допустимую строку соединения в следующем формате:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Где `Endpoint` обычно имеет формат hello `https://[yourNamespace].servicebus.windows.net`.

toocreate любого клиента службы Azure, необходимо использовать hello `ServicesBuilder` класса. Вы можете:

* Передайте hello подключения tooit строки напрямую.
* использовать hello **CloudConfigurationManager (CCM)** toocheck нескольких внешних источников для hello строки подключения:
  * По умолчанию предоставляется поддержка одного внешнего источника — переменных среды.
  * Можно добавлять новые источники, расширяя hello `ConnectionStringSource` класса.

Приведенные ниже примеры hello hello строка подключения передается напрямую.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a>Создание раздела
Вы можете выполнять операции управления для разделов Service Bus через hello `ServiceBusRestProxy` класса. Объект `ServiceBusRestProxy` через hello создается объект `ServicesBuilder::createServiceBusService` фабричный метод со строкой соединения, соответствующую, инкапсулирующий hello маркера разрешения toomanage его.

Следующий пример показывает как Hello tooinstantiate `ServiceBusRestProxy` и вызвать `ServiceBusRestProxy->createTopic` toocreate распределитель с именем `mytopic` в `MySBNamespace` пространство имен:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
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
> Можно использовать hello `listTopics` метод `ServiceBusRestProxy` объектов toocheck, если раздел с указанным именем уже существует в пространстве имен службы.
> 
> 

## <a name="create-a-subscription"></a>Создание подписки
Подписок раздела также создаются с hello `ServiceBusRestProxy->createSubscription` метод. Подписки представляют собой именованные и может иметь дополнительный фильтр, ограничивающий hello набор сообщений, передаваемых toohello в виртуальную очередь подписки.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Создайте подписку с фильтром (MatchAll) по умолчанию hello
Hello **MatchAll** фильтром является фильтр по умолчанию hello, который используется, если не указан фильтр при создании новой подписки. Здравствуйте, когда **MatchAll** используется фильтр, раздел опубликованного toohello все сообщения помещаются в виртуальную очередь подписки hello. Hello следующем примере создается подписка с именем «mysubscription» и по умолчанию hello использует **MatchAll** фильтра.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
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

### <a name="create-subscriptions-with-filters"></a>Создание подписок с фильтрами
Также можно настроить фильтры, позволяющие toospecify сообщений отправила разделе tooa должны появиться в подписку определенного раздела. Hello самый гибкий тип фильтра, поддерживаемых подписок — hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), который реализует подмножество SQL92. Фильтры SQL работают с свойств сообщений hello, раздел опубликованного toohello hello. Дополнительные сведения о фильтрах SqlFilter см. в описании [свойства SqlFilter.SqlExpression][sqlfilter].

> [!NOTE]
> Каждое правило в подписке обрабатывает входящие сообщения независимо друг от друга, добавление их результат сообщения toohello подписки. Кроме того, каждой новой подписки имеет значение по умолчанию **правило** объекта с фильтром, который добавляет все сообщения из подписки toohello раздела hello. tooreceive только сообщения, соответствующие фильтру, необходимо удалить правило по умолчанию hello. Правило по умолчанию hello можно удалить с помощью hello `ServiceBusRestProxy->deleteRule` метод.
> 
> 

Hello следующий пример создает подписку с именем `HighMessages` с **SqlFilter** , выбирает только сообщения, которые содержат пользовательского `MessageNumber` свойство больше 3. В разделе [tooa темы о сообщениях отправки](#send-messages-to-a-topic) сведения о добавлении пользовательских свойств toomessages.

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

Обратите внимание, что этот код требует использования hello дополнительное пространство имен: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.

Аналогичным образом hello следующий пример создает подписку с именем `LowMessages` с `SqlFilter` , выбирает только сообщения, которые содержат `MessageNumber` свойства меньше или равно too3.

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

Теперь, когда сообщение отправляется toohello `mytopic` раздела, он всегда доставляется toohello tooreceivers подписка `mysubscription` подписки и выборочно доставленный tooreceivers подписка toohello `HighMessages` и `LowMessages` подписок () зависимости от содержимого сообщения hello).

## <a name="send-messages-tooa-topic"></a>Отправить tooa темы о сообщениях
toosend раздела Service Bus tooa сообщения, приложение вызывает hello `ServiceBusRestProxy->sendTopicMessage` метод. Здравствуйте, как следующий код показывает toosend toohello сообщение `mytopic` ранее созданных в разделе `MySBNamespace` пространства имен службы.

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
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
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

Сообщения отправляются разделы шины tooService являются экземплярами hello [BrokeredMessage] [ BrokeredMessage] класса. [BrokeredMessage] [ BrokeredMessage] объекты имеют ряд стандартных свойств и методов, а также свойства, которые могут быть используется toohold пользовательские свойства для конкретного приложения. Hello примере показан способ тестирования toosend 5 сообщений toohello `mytopic` раздел создан ранее. Hello `setProperty` tooadd используется пользовательское свойство имеет метод (`MessageNumber`) tooeach сообщения. Обратите внимание, что hello `MessageNumber` зависит от значения свойства для каждого сообщения (это значение toodetermine, его получении подписки, которые можно использовать, как показано в hello [создать подписку](#create-a-subscription) раздел):

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

Темы Service Bus поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md). Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ. Нет ограничений на hello количество сообщений, которые содержатся в разделе, но отсутствует ограничение на общий размер сообщений hello, удерживаемые раздела hello. Максимальный размер раздела ограничен 5 ГБ. Дополнительные сведения о квотах см. в статье [Квоты на служебную шину][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Получение сообщений из подписки
Hello лучшим способом tooreceive сообщений из подписки — toouse `ServiceBusRestProxy->receiveSubscriptionMessage` метод. Сообщения можно получать в двух различных режимах: [*ReceiveAndDelete* и *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode). **PeekLock** по умолчанию hello.

При использовании hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) режиме получение является единовременной операцией; то есть когда Service Bus получает запросы на чтение для сообщения в подписке, она помечает приветственное сообщение как полученное и возвращает его toohello приложение. [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * режим — самая простая модель hello и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя. toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки. Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.

По умолчанию hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) режим, получает сообщение становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения. Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения. После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения, передавая сообщение hello получено слишком`ServiceBusRestProxy->deleteMessage`. Когда Service Bus обнаруживает hello `deleteMessage` вызов, он пометить приветственное сообщение как полученное и удалите его из очереди hello.

Следующий пример показывает как Hello tooreceive и обрабатывать сообщения с помощью [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) режиме (режим по умолчанию hello). 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode tooPeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>Практическое руководство. Обработка сбоев приложения и нечитаемых сообщений
Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения. Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlockMessage` метод для получения приветственное сообщение (вместо hello `deleteMessage` метода). Это будет вызвать Service Bus toounlock приветственное сообщение в очередь hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.

Также существует время ожидания, связанные с сообщением, заблокировать в течение hello очереди, и при сбое приложения hello tooprocess приветственное сообщение, прежде чем hello срок блокировки (например, если приложение hello терпит сбой), разблокируйте Service Bus приветственное сообщение автоматически и сделать ее доступной toobe получили еще раз.

В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `deleteMessage` выдается запрос, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения. Это часто называется *как минимум один раз* обработки; то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tooapplications toohandle повторной доставке сообщений. Это можно сделать с помощью hello `getMessageId` метод приветственное сообщение, остается постоянным на протяжении всех попыток доставки.

## <a name="delete-topics-and-subscriptions"></a>Удаление разделов и подписок
toodelete раздела или подписки, используйте hello `ServiceBusRestProxy->deleteTopic` или hello `ServiceBusRestProxy->deleteSubscripton` методы, соответственно. Обратите внимание, что при удалении раздела также удаляются все подписки, которые зарегистрированы в разделе hello.

Hello следующем примере показано как toodelete раздел с именем `mytopic` и его зарегистрированным подпискам.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
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

С помощью hello `deleteSubscription` метод, можно удалить подписку независимо друг от друга:

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello очереди шины обслуживания, в разделе [очереди, разделы и подписки] [ Queues, topics, and subscriptions] для получения дополнительной информации.

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
