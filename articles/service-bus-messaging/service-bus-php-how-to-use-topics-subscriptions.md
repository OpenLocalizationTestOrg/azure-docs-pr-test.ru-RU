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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="5f4ca-103">Как toouse Service Bus разделов и подписок с PHP</span><span class="sxs-lookup"><span data-stu-id="5f4ca-103">How toouse Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="5f4ca-104">В этой статье показано, как toouse Service Bus разделы и подписки.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-104">This article shows you how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="5f4ca-105">Hello примеры написаны на PHP и использовать hello [пакет Azure SDK для PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5f4ca-105">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="5f4ca-106">Hello сценарии включают **создания разделов и подписок**, **создание фильтров подписок**, **отправки темы о сообщениях tooa**, **получения сообщения из подписки**, и **удаление разделов и подписок**.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="5f4ca-107">Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="5f4ca-107">Create a PHP application</span></span>
<span data-ttu-id="5f4ca-108">Здравствуйте, только классы tooreference hello является обязательным условием для создания приложения PHP, которое обращается к службе BLOB-объектов Azure hello [пакет Azure SDK для PHP](../php-download-sdk.md) из кода.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-108">hello only requirement for creating a PHP application that accesses hello Azure Blob service is tooreference classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="5f4ca-109">Можно использовать любой toocreate средства разработки приложения или «Блокнот».</span><span class="sxs-lookup"><span data-stu-id="5f4ca-109">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="5f4ca-110">Установку PHP также должен иметь hello [OpenSSL расширения](http://php.net/openssl) установлен и включен.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-110">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="5f4ca-111">В этой статье описывается, как toouse службы компонентов, которые могут быть вызваны в рамках приложения PHP локально или в код, выполняющийся в Azure веб-роли, рабочей роли или веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-111">This article describes how toouse service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="5f4ca-112">Получить hello клиентских библиотек Azure</span><span class="sxs-lookup"><span data-stu-id="5f4ca-112">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="5f4ca-113">Настройка вашего приложения toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="5f4ca-113">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="5f4ca-114">hello toouse интерфейсов API служебной шины:</span><span class="sxs-lookup"><span data-stu-id="5f4ca-114">toouse hello Service Bus APIs:</span></span>

1. <span data-ttu-id="5f4ca-115">Файл автозагрузчика hello ссылка, с помощью hello [require_once] [ require-once] инструкции.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-115">Reference hello autoloader file using hello [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="5f4ca-116">Ссылка на любые классы, которые могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-116">Reference any classes you might use.</span></span>

<span data-ttu-id="5f4ca-117">Hello следующем примере показано, как tooinclude hello автозагрузчика файла и ссылку hello **ServiceBusService** класса.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-117">hello following example shows how tooinclude hello autoloader file and reference hello **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="5f4ca-118">В этом примере (и другие примеры в этой статье) предполагается, что вы установили hello PHP клиентские библиотеки для Azure через редактор.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-118">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="5f4ca-119">При установке библиотеки hello вручную или в виде пакета ГРУШИ необходимо сослаться на hello **WindowsAzure.php** автозагрузчика файла.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-119">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="5f4ca-120">В следующих примерах hello, hello `require_once` всегда будут отображаться инструкции, но указываются только классы hello, необходимые для tooexecute пример hello.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-120">In hello following examples, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="5f4ca-121">Настройка подключения к Service Bus</span><span class="sxs-lookup"><span data-stu-id="5f4ca-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="5f4ca-122">tooinstantiate клиента Service Bus, необходимо сначала иметь допустимую строку соединения в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="5f4ca-122">tooinstantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="5f4ca-123">Где `Endpoint` обычно имеет формат hello `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-123">Where `Endpoint` is typically of hello format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="5f4ca-124">toocreate любого клиента службы Azure, необходимо использовать hello `ServicesBuilder` класса.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-124">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="5f4ca-125">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="5f4ca-125">You can:</span></span>

* <span data-ttu-id="5f4ca-126">Передайте hello подключения tooit строки напрямую.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-126">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="5f4ca-127">использовать hello **CloudConfigurationManager (CCM)** toocheck нескольких внешних источников для hello строки подключения:</span><span class="sxs-lookup"><span data-stu-id="5f4ca-127">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="5f4ca-128">По умолчанию предоставляется поддержка одного внешнего источника — переменных среды.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="5f4ca-129">Можно добавлять новые источники, расширяя hello `ConnectionStringSource` класса.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-129">You can add new sources by extending hello `ConnectionStringSource` class.</span></span>

<span data-ttu-id="5f4ca-130">Приведенные ниже примеры hello hello строка подключения передается напрямую.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-130">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="5f4ca-131">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="5f4ca-131">Create a topic</span></span>
<span data-ttu-id="5f4ca-132">Вы можете выполнять операции управления для разделов Service Bus через hello `ServiceBusRestProxy` класса.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-132">You can perform management operations for Service Bus topics via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="5f4ca-133">Объект `ServiceBusRestProxy` через hello создается объект `ServicesBuilder::createServiceBusService` фабричный метод со строкой соединения, соответствующую, инкапсулирующий hello маркера разрешения toomanage его.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-133">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="5f4ca-134">Следующий пример показывает как Hello tooinstantiate `ServiceBusRestProxy` и вызвать `ServiceBusRestProxy->createTopic` toocreate распределитель с именем `mytopic` в `MySBNamespace` пространство имен:</span><span class="sxs-lookup"><span data-stu-id="5f4ca-134">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` toocreate a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

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
> <span data-ttu-id="5f4ca-135">Можно использовать hello `listTopics` метод `ServiceBusRestProxy` объектов toocheck, если раздел с указанным именем уже существует в пространстве имен службы.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-135">You can use hello `listTopics` method on `ServiceBusRestProxy` objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="5f4ca-136">Создание подписки</span><span class="sxs-lookup"><span data-stu-id="5f4ca-136">Create a subscription</span></span>
<span data-ttu-id="5f4ca-137">Подписок раздела также создаются с hello `ServiceBusRestProxy->createSubscription` метод.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-137">Topic subscriptions are also created with hello `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="5f4ca-138">Подписки представляют собой именованные и может иметь дополнительный фильтр, ограничивающий hello набор сообщений, передаваемых toohello в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-138">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="5f4ca-139">Создайте подписку с фильтром (MatchAll) по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="5f4ca-139">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="5f4ca-140">Hello **MatchAll** фильтром является фильтр по умолчанию hello, который используется, если не указан фильтр при создании новой подписки.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-140">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="5f4ca-141">Здравствуйте, когда **MatchAll** используется фильтр, раздел опубликованного toohello все сообщения помещаются в виртуальную очередь подписки hello.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-141">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="5f4ca-142">Hello следующем примере создается подписка с именем «mysubscription» и по умолчанию hello использует **MatchAll** фильтра.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-142">hello following example creates a subscription named 'mysubscription' and uses hello default **MatchAll** filter.</span></span>

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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="5f4ca-143">Создание подписок с фильтрами</span><span class="sxs-lookup"><span data-stu-id="5f4ca-143">Create subscriptions with filters</span></span>
<span data-ttu-id="5f4ca-144">Также можно настроить фильтры, позволяющие toospecify сообщений отправила разделе tooa должны появиться в подписку определенного раздела.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-144">You can also set up filters that enable you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="5f4ca-145">Hello самый гибкий тип фильтра, поддерживаемых подписок — hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), который реализует подмножество SQL92.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-145">hello most flexible type of filter supported by subscriptions is hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="5f4ca-146">Фильтры SQL работают с свойств сообщений hello, раздел опубликованного toohello hello.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-146">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="5f4ca-147">Дополнительные сведения о фильтрах SqlFilter см. в описании [свойства SqlFilter.SqlExpression][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="5f4ca-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="5f4ca-148">Каждое правило в подписке обрабатывает входящие сообщения независимо друг от друга, добавление их результат сообщения toohello подписки.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-148">Each rule on a subscription processes incoming messages independently, adding their result messages toohello subscription.</span></span> <span data-ttu-id="5f4ca-149">Кроме того, каждой новой подписки имеет значение по умолчанию **правило** объекта с фильтром, который добавляет все сообщения из подписки toohello раздела hello.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from hello topic toohello subscription.</span></span> <span data-ttu-id="5f4ca-150">tooreceive только сообщения, соответствующие фильтру, необходимо удалить правило по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-150">tooreceive only messages matching your filter, you must remove hello default rule.</span></span> <span data-ttu-id="5f4ca-151">Правило по умолчанию hello можно удалить с помощью hello `ServiceBusRestProxy->deleteRule` метод.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-151">You can remove hello default rule by using hello `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="5f4ca-152">Hello следующий пример создает подписку с именем `HighMessages` с **SqlFilter** , выбирает только сообщения, которые содержат пользовательского `MessageNumber` свойство больше 3.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-152">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="5f4ca-153">В разделе [tooa темы о сообщениях отправки](#send-messages-to-a-topic) сведения о добавлении пользовательских свойств toomessages.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-153">See [Send messages tooa topic](#send-messages-to-a-topic) for information about adding custom properties toomessages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="5f4ca-154">Обратите внимание, что этот код требует использования hello дополнительное пространство имен: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-154">Note that this code requires hello use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="5f4ca-155">Аналогичным образом hello следующий пример создает подписку с именем `LowMessages` с `SqlFilter` , выбирает только сообщения, которые содержат `MessageNumber` свойства меньше или равно too3.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-155">Similarly, hello following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal too3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="5f4ca-156">Теперь, когда сообщение отправляется toohello `mytopic` раздела, он всегда доставляется toohello tooreceivers подписка `mysubscription` подписки и выборочно доставленный tooreceivers подписка toohello `HighMessages` и `LowMessages` подписок () зависимости от содержимого сообщения hello).</span><span class="sxs-lookup"><span data-stu-id="5f4ca-156">Now, when a message is sent toohello `mytopic` topic, it is always delivered tooreceivers subscribed toohello `mysubscription` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="5f4ca-157">Отправить tooa темы о сообщениях</span><span class="sxs-lookup"><span data-stu-id="5f4ca-157">Send messages tooa topic</span></span>
<span data-ttu-id="5f4ca-158">toosend раздела Service Bus tooa сообщения, приложение вызывает hello `ServiceBusRestProxy->sendTopicMessage` метод.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-158">toosend a message tooa Service Bus topic, your application calls hello `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="5f4ca-159">Здравствуйте, как следующий код показывает toosend toohello сообщение `mytopic` ранее созданных в разделе `MySBNamespace` пространства имен службы.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-159">hello following code shows how toosend a message toohello `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="5f4ca-160">Сообщения отправляются разделы шины tooService являются экземплярами hello [BrokeredMessage] [ BrokeredMessage] класса.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-160">Messages sent tooService Bus topics are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="5f4ca-161">[BrokeredMessage] [ BrokeredMessage] объекты имеют ряд стандартных свойств и методов, а также свойства, которые могут быть используется toohold пользовательские свойства для конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used toohold custom application-specific properties.</span></span> <span data-ttu-id="5f4ca-162">Hello примере показан способ тестирования toosend 5 сообщений toohello `mytopic` раздел создан ранее.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-162">hello following example shows how toosend 5 test messages toohello `mytopic` topic previously created.</span></span> <span data-ttu-id="5f4ca-163">Hello `setProperty` tooadd используется пользовательское свойство имеет метод (`MessageNumber`) tooeach сообщения.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-163">hello `setProperty` method is used tooadd a custom property (`MessageNumber`) tooeach message.</span></span> <span data-ttu-id="5f4ca-164">Обратите внимание, что hello `MessageNumber` зависит от значения свойства для каждого сообщения (это значение toodetermine, его получении подписки, которые можно использовать, как показано в hello [создать подписку](#create-a-subscription) раздел):</span><span class="sxs-lookup"><span data-stu-id="5f4ca-164">Note that hello `MessageNumber` property value varies on each message (you can use this value toodetermine which subscriptions receive it, as shown in hello [Create a subscription](#create-a-subscription) section):</span></span>

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

<span data-ttu-id="5f4ca-165">Темы Service Bus поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="5f4ca-165">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="5f4ca-166">Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-166">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="5f4ca-167">Нет ограничений на hello количество сообщений, которые содержатся в разделе, но отсутствует ограничение на общий размер сообщений hello, удерживаемые раздела hello.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-167">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="5f4ca-168">Максимальный размер раздела ограничен 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="5f4ca-169">Дополнительные сведения о квотах см. в статье [Квоты на служебную шину][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="5f4ca-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="5f4ca-170">Получение сообщений из подписки</span><span class="sxs-lookup"><span data-stu-id="5f4ca-170">Receive messages from a subscription</span></span>
<span data-ttu-id="5f4ca-171">Hello лучшим способом tooreceive сообщений из подписки — toouse `ServiceBusRestProxy->receiveSubscriptionMessage` метод.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-171">hello best way tooreceive messages from a subscription is toouse a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="5f4ca-172">Сообщения можно получать в двух различных режимах: [*ReceiveAndDelete* и *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="5f4ca-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="5f4ca-173">**PeekLock** по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-173">**PeekLock** is hello default.</span></span>

<span data-ttu-id="5f4ca-174">При использовании hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) режиме получение является единовременной операцией; то есть когда Service Bus получает запросы на чтение для сообщения в подписке, она помечает приветственное сообщение как полученное и возвращает его toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-174">When using hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="5f4ca-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * режим — самая простая модель hello и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="5f4ca-176">toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-176">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="5f4ca-177">Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="5f4ca-178">По умолчанию hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) режим, получает сообщение становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-178">In hello default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="5f4ca-179">Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="5f4ca-180">После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения, передавая сообщение hello получено слишком`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="5f4ca-181">Когда Service Bus обнаруживает hello `deleteMessage` вызов, он пометить приветственное сообщение как полученное и удалите его из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-181">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="5f4ca-182">Следующий пример показывает как Hello tooreceive и обрабатывать сообщения с помощью [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) режиме (режим по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="5f4ca-182">hello following example shows how tooreceive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (hello default mode).</span></span> 

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="5f4ca-183">Практическое руководство. Обработка сбоев приложения и нечитаемых сообщений</span><span class="sxs-lookup"><span data-stu-id="5f4ca-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="5f4ca-184">Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-184">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="5f4ca-185">Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlockMessage` метод для получения приветственное сообщение (вместо hello `deleteMessage` метода).</span><span class="sxs-lookup"><span data-stu-id="5f4ca-185">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="5f4ca-186">Это будет вызвать Service Bus toounlock приветственное сообщение в очередь hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-186">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="5f4ca-187">Также существует время ожидания, связанные с сообщением, заблокировать в течение hello очереди, и при сбое приложения hello tooprocess приветственное сообщение, прежде чем hello срок блокировки (например, если приложение hello терпит сбой), разблокируйте Service Bus приветственное сообщение автоматически и сделать ее доступной toobe получили еще раз.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-187">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="5f4ca-188">В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `deleteMessage` выдается запрос, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-188">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="5f4ca-189">Это часто называется *как минимум один раз* обработки; то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="5f4ca-190">Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tooapplications toohandle повторной доставке сообщений.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-190">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tooapplications toohandle duplicate message delivery.</span></span> <span data-ttu-id="5f4ca-191">Это можно сделать с помощью hello `getMessageId` метод приветственное сообщение, остается постоянным на протяжении всех попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-191">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="5f4ca-192">Удаление разделов и подписок</span><span class="sxs-lookup"><span data-stu-id="5f4ca-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="5f4ca-193">toodelete раздела или подписки, используйте hello `ServiceBusRestProxy->deleteTopic` или hello `ServiceBusRestProxy->deleteSubscripton` методы, соответственно.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-193">toodelete a topic or a subscription, use hello `ServiceBusRestProxy->deleteTopic` or hello `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="5f4ca-194">Обратите внимание, что при удалении раздела также удаляются все подписки, которые зарегистрированы в разделе hello.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-194">Note that deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span>

<span data-ttu-id="5f4ca-195">Hello следующем примере показано как toodelete раздел с именем `mytopic` и его зарегистрированным подпискам.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-195">hello following example shows how toodelete a topic named `mytopic` and its registered subscriptions.</span></span>

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

<span data-ttu-id="5f4ca-196">С помощью hello `deleteSubscription` метод, можно удалить подписку независимо друг от друга:</span><span class="sxs-lookup"><span data-stu-id="5f4ca-196">By using hello `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="5f4ca-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f4ca-197">Next steps</span></span>
<span data-ttu-id="5f4ca-198">Теперь, когда вы узнали основы hello очереди шины обслуживания, в разделе [очереди, разделы и подписки] [ Queues, topics, and subscriptions] для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="5f4ca-198">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
