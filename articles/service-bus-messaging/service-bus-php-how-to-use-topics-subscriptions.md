---
title: "Использование разделов служебной шины в PHP | Документация Майкрософт"
description: "Узнайте, как использовать разделы служебной шины с PHP в Azure."
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
ms.openlocfilehash: afa9efcb6335786198021ec81dd087287c39bda9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="256d4-103">Как использовать разделы и подписки служебной шины с PHP</span><span class="sxs-lookup"><span data-stu-id="256d4-103">How to use Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="256d4-104">Из этой статьи вы узнаете, как использовать разделы и подписки служебной шины.</span><span class="sxs-lookup"><span data-stu-id="256d4-104">This article shows you how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="256d4-105">Примеры написаны на PHP и используют [пакет Azure SDK для PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="256d4-105">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="256d4-106">В этой статье описаны такие сценарии, как **создание разделов и подписок**, **создание фильтров подписок**, **отправка сообщений в раздел**, **получение сообщений из подписки** и **удаление разделов и подписок**.</span><span class="sxs-lookup"><span data-stu-id="256d4-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="256d4-107">Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="256d4-107">Create a PHP application</span></span>
<span data-ttu-id="256d4-108">Единственным требованием для создания приложения PHP, которое получает доступ к службе BLOB-объектов Azure, является наличие ссылки на классы в [пакете SDK для Azure для PHP](../php-download-sdk.md) непосредственно из кода.</span><span class="sxs-lookup"><span data-stu-id="256d4-108">The only requirement for creating a PHP application that accesses the Azure Blob service is to reference classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="256d4-109">Для создания приложения можно использовать любые средства разработки или Блокнот.</span><span class="sxs-lookup"><span data-stu-id="256d4-109">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="256d4-110">В установленном пакете PHP должно быть установлено и включено [расширение OpenSSL](http://php.net/openssl).</span><span class="sxs-lookup"><span data-stu-id="256d4-110">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="256d4-111">В этой статье рассказывается, как использовать компоненты службы, которые могут быть вызваны локально в приложении PHP или в коде, работающем в веб-роли, рабочей роли или на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="256d4-111">This article describes how to use service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="256d4-112">Получение клиентских библиотек Azure</span><span class="sxs-lookup"><span data-stu-id="256d4-112">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="256d4-113">Настройка приложения для использования служебной шины</span><span class="sxs-lookup"><span data-stu-id="256d4-113">Configure your application to use Service Bus</span></span>
<span data-ttu-id="256d4-114">Чтобы использовать интерфейсы API служебной шины, требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="256d4-114">To use the Service Bus APIs:</span></span>

1. <span data-ttu-id="256d4-115">Ссылка на файл автозагрузчика с использованием оператора [require_once][require-once].</span><span class="sxs-lookup"><span data-stu-id="256d4-115">Reference the autoloader file using the [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="256d4-116">Ссылка на любые классы, которые могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="256d4-116">Reference any classes you might use.</span></span>

<span data-ttu-id="256d4-117">В следующем примере показано, как включить файл автозагрузчика и сослаться на класс **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="256d4-117">The following example shows how to include the autoloader file and reference the **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="256d4-118">В этом примере (и других примерах в этой статье) предполагается, что установлены клиентские библиотеки PHP для Azure с помощью Composer.</span><span class="sxs-lookup"><span data-stu-id="256d4-118">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="256d4-119">При установке библиотек вручную или в качестве пакета PEAR необходимо использовать ссылку на файл автозагрузчика **WindowsAzure.php**.</span><span class="sxs-lookup"><span data-stu-id="256d4-119">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="256d4-120">В приведенных ниже примерах всегда будет отображаться оператор `require_once`, однако ссылки будут приводиться только на классы, которые необходимы для выполнения этого примера.</span><span class="sxs-lookup"><span data-stu-id="256d4-120">In the following examples, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="256d4-121">Настройка подключения к Service Bus</span><span class="sxs-lookup"><span data-stu-id="256d4-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="256d4-122">Для создания клиента служебной шины необходимо сначала сформировать правильную строку подключения в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="256d4-122">To instantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="256d4-123">где `Endpoint` обычно имеет формат `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="256d4-123">Where `Endpoint` is typically of the format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="256d4-124">Для создания клиента службы Azure необходимо использовать класс `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="256d4-124">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="256d4-125">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="256d4-125">You can:</span></span>

* <span data-ttu-id="256d4-126">Передать строку подключения напрямую или</span><span class="sxs-lookup"><span data-stu-id="256d4-126">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="256d4-127">использовать **CloudConfigurationManager (CCM)** для проверки нескольких внешних источников на наличие строки подключения:</span><span class="sxs-lookup"><span data-stu-id="256d4-127">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="256d4-128">По умолчанию предоставляется поддержка одного внешнего источника — переменных среды.</span><span class="sxs-lookup"><span data-stu-id="256d4-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="256d4-129">Можно добавить новые источники, расширив класс `ConnectionStringSource`.</span><span class="sxs-lookup"><span data-stu-id="256d4-129">You can add new sources by extending the `ConnectionStringSource` class.</span></span>

<span data-ttu-id="256d4-130">В приведенных здесь примерах строка подключения передается напрямую.</span><span class="sxs-lookup"><span data-stu-id="256d4-130">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="256d4-131">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="256d4-131">Create a topic</span></span>
<span data-ttu-id="256d4-132">Операции управления разделами служебной шины можно выполнять с помощью класса `ServiceBusRestProxy`.</span><span class="sxs-lookup"><span data-stu-id="256d4-132">You can perform management operations for Service Bus topics via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="256d4-133">Объект `ServiceBusRestProxy` создается посредством фабричного метода `ServicesBuilder::createServiceBusService` с соответствующей строкой подключения, инкапсулирующей в себе разрешения маркера на управление им.</span><span class="sxs-lookup"><span data-stu-id="256d4-133">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="256d4-134">В приведенном ниже примере показано, как создать экземпляр `ServiceBusRestProxy` и вызвать метод `ServiceBusRestProxy->createTopic` для создания раздела `mytopic` в пространстве имен `MySBNamespace`.</span><span class="sxs-lookup"><span data-stu-id="256d4-134">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` to create a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

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
> <span data-ttu-id="256d4-135">Можно использовать метод `listTopics` для объектов `ServiceBusRestProxy`, чтобы проверить, существует ли уже раздел с указанным именем в пространстве имен службы.</span><span class="sxs-lookup"><span data-stu-id="256d4-135">You can use the `listTopics` method on `ServiceBusRestProxy` objects to check if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="256d4-136">Создание подписки</span><span class="sxs-lookup"><span data-stu-id="256d4-136">Create a subscription</span></span>
<span data-ttu-id="256d4-137">Подписки на разделы также создаются с помощью метода `ServiceBusRestProxy->createSubscription`.</span><span class="sxs-lookup"><span data-stu-id="256d4-137">Topic subscriptions are also created with the `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="256d4-138">Подписки имеют имена и могут использовать дополнительный фильтр, ограничивающий набор сообщений, доставляемых в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="256d4-138">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="256d4-139">Создание подписки с фильтром по умолчанию (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="256d4-139">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="256d4-140">Фильтр **MatchAll** является фильтром по умолчанию, используемым, если при создании новой подписки не указан фильтр.</span><span class="sxs-lookup"><span data-stu-id="256d4-140">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="256d4-141">Если используется фильтр **MatchAll**, то все сообщения, опубликованные в разделе, помещаются в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="256d4-141">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="256d4-142">В следующем примере создается подписка с именем mysubscription и используется фильтр по умолчанию **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="256d4-142">The following example creates a subscription named 'mysubscription' and uses the default **MatchAll** filter.</span></span>

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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="256d4-143">Создание подписок с фильтрами</span><span class="sxs-lookup"><span data-stu-id="256d4-143">Create subscriptions with filters</span></span>
<span data-ttu-id="256d4-144">Кроме того, можно настраивать фильтры, позволяющие определять, какие посылаемые в раздел сообщения должны появляться в рамках конкретной подписки.</span><span class="sxs-lookup"><span data-stu-id="256d4-144">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="256d4-145">Самый гибкий тип фильтра, который поддерживается подписками, — это [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), реализующий подмножество SQL92.</span><span class="sxs-lookup"><span data-stu-id="256d4-145">The most flexible type of filter supported by subscriptions is the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="256d4-146">Фильтры SQL работают со свойствами сообщений, которые опубликованы в разделе.</span><span class="sxs-lookup"><span data-stu-id="256d4-146">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="256d4-147">Дополнительные сведения о фильтрах SqlFilter см. в описании [свойства SqlFilter.SqlExpression][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="256d4-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="256d4-148">Каждое правило в подписке обрабатывает входящие сообщения независимо, добавляя к подписке свои сообщения о результате.</span><span class="sxs-lookup"><span data-stu-id="256d4-148">Each rule on a subscription processes incoming messages independently, adding their result messages to the subscription.</span></span> <span data-ttu-id="256d4-149">Кроме того, в состав каждой новой подписки по умолчанию входит объект **Правило** с фильтром, который добавляет все сообщения из раздела в подписку.</span><span class="sxs-lookup"><span data-stu-id="256d4-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from the topic to the subscription.</span></span> <span data-ttu-id="256d4-150">Чтобы получать только сообщения, соответствующие условиям фильтра, необходимо удалить это правило по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="256d4-150">To receive only messages matching your filter, you must remove the default rule.</span></span> <span data-ttu-id="256d4-151">Правило по умолчанию можно удалить с помощью метода `ServiceBusRestProxy->deleteRule`.</span><span class="sxs-lookup"><span data-stu-id="256d4-151">You can remove the default rule by using the `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="256d4-152">В следующем примере создается подписка `HighMessages`, содержащая фильтр **SqlFilter**, который выбирает только те сообщения, значение настраиваемого свойства `MessageNumber` которых больше 3.</span><span class="sxs-lookup"><span data-stu-id="256d4-152">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="256d4-153">Чтобы получить информацию о добавлении пользовательских свойств в сообщения, изучите раздел [Отправка сообщений в раздел](#send-messages-to-a-topic).</span><span class="sxs-lookup"><span data-stu-id="256d4-153">See [Send messages to a topic](#send-messages-to-a-topic) for information about adding custom properties to messages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="256d4-154">Обратите внимание, что этот код требует использования дополнительного пространства имен: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="256d4-154">Note that this code requires the use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="256d4-155">Аналогичным образом в следующем примере создается подписка `LowMessages` с фильтром `SqlFilter`, который выбирает только те сообщения, у которых значение свойства `MessageNumber` меньше или равно 3.</span><span class="sxs-lookup"><span data-stu-id="256d4-155">Similarly, the following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal to 3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="256d4-156">Теперь, если сообщение отправляется в раздел `mytopic`, оно всегда будет доставляться получателям, подписанным на подписку раздела `mysubscription`, и выборочно доставляться получателям, подписанным на подписки разделов `HighMessages` и `LowMessages` (в зависимости от содержания сообщения).</span><span class="sxs-lookup"><span data-stu-id="256d4-156">Now, when a message is sent to the `mytopic` topic, it is always delivered to receivers subscribed to the `mysubscription` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="256d4-157">Отправка сообщений в раздел</span><span class="sxs-lookup"><span data-stu-id="256d4-157">Send messages to a topic</span></span>
<span data-ttu-id="256d4-158">Чтобы отправить сообщение в раздел служебной шины, в приложении вызывается метод `ServiceBusRestProxy->sendTopicMessage`.</span><span class="sxs-lookup"><span data-stu-id="256d4-158">To send a message to a Service Bus topic, your application calls the `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="256d4-159">В следующем примере кода показано, как отправить сообщение в раздел `mytopic`, созданный ранее в пространстве имен службы `MySBNamespace`.</span><span class="sxs-lookup"><span data-stu-id="256d4-159">The following code shows how to send a message to the `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="256d4-160">Сообщения, отправляемые в разделы служебной шины и получаемые из них, — это экземпляры класса [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="256d4-160">Messages sent to Service Bus topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="256d4-161">У объектов [BrokeredMessage][BrokeredMessage] есть набор стандартных свойств и методов, а также свойства, которые можно использовать для хранения настраиваемых свойств приложения.</span><span class="sxs-lookup"><span data-stu-id="256d4-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used to hold custom application-specific properties.</span></span> <span data-ttu-id="256d4-162">В следующем примере показано, как отправить 5 тестовых сообщений в созданный ранее раздел `mytopic`.</span><span class="sxs-lookup"><span data-stu-id="256d4-162">The following example shows how to send 5 test messages to the `mytopic` topic previously created.</span></span> <span data-ttu-id="256d4-163">Метод `setProperty` используется для добавления настраиваемого свойства (`MessageNumber`) в каждое сообщение.</span><span class="sxs-lookup"><span data-stu-id="256d4-163">The `setProperty` method is used to add a custom property (`MessageNumber`) to each message.</span></span> <span data-ttu-id="256d4-164">Обратите внимание, что значение свойства `MessageNumber` меняется в каждом сообщении (с помощью этого можно определить, какие подписки его получают, как показано в разделе [Создание подписки](#create-a-subscription)).</span><span class="sxs-lookup"><span data-stu-id="256d4-164">Note that the `MessageNumber` property value varies on each message (you can use this value to determine which subscriptions receive it, as shown in the [Create a subscription](#create-a-subscription) section):</span></span>

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

<span data-ttu-id="256d4-165">Разделы служебной шины поддерживают максимальный размер сообщения 256 КБ для [уровня "Стандартный"](service-bus-premium-messaging.md) и 1 МБ для [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="256d4-165">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="256d4-166">Максимальный размер заголовка, который содержит стандартные и настраиваемые свойства приложения, — 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="256d4-166">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="256d4-167">Ограничения на количество сообщений в разделе нет, но есть максимальный общий размер сообщений, содержащихся в разделе.</span><span class="sxs-lookup"><span data-stu-id="256d4-167">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="256d4-168">Максимальный размер раздела ограничен 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="256d4-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="256d4-169">Дополнительные сведения о квотах см. в статье [Квоты на служебную шину][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="256d4-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="256d4-170">Получение сообщений из подписки</span><span class="sxs-lookup"><span data-stu-id="256d4-170">Receive messages from a subscription</span></span>
<span data-ttu-id="256d4-171">Самым простым способом получать сообщения от подписки является использование метода `ServiceBusRestProxy->receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="256d4-171">The best way to receive messages from a subscription is to use a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="256d4-172">Сообщения можно получать в двух различных режимах: [*ReceiveAndDelete* и *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="256d4-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="256d4-173">По умолчанию используется **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="256d4-173">**PeekLock** is the default.</span></span>

<span data-ttu-id="256d4-174">В режиме [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) получение — это одиночная операция. Когда служебная шина получает запрос на чтение для сообщения в подписке, сообщение помечается как использованное и возвращается в приложение.</span><span class="sxs-lookup"><span data-stu-id="256d4-174">When using the [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="256d4-175">Режим [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)* представляет собой самую простую модель, которая лучше всего работает в ситуациях, когда приложение может не обрабатывать сообщение при сбое.</span><span class="sxs-lookup"><span data-stu-id="256d4-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="256d4-176">Чтобы это понять, рассмотрим сценарий, в котором объект-получатель выдает запрос на получение и выходит из строя до его обработки.</span><span class="sxs-lookup"><span data-stu-id="256d4-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="256d4-177">Поскольку служебная шина помечает сообщение как использованное, то когда после своего перезапуска приложение снова начнет обрабатывать сообщения, оно пропустит сообщение, использованное до сбоя.</span><span class="sxs-lookup"><span data-stu-id="256d4-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="256d4-178">В используемом по умолчанию режиме [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) процесс получения становится двухэтапной операцией, что позволяет поддерживать приложения, не устойчивые к пропуску сообщений.</span><span class="sxs-lookup"><span data-stu-id="256d4-178">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="256d4-179">Получив запрос, служебная шина находит следующее сообщение, блокирует его, чтобы предотвратить его получение другими получателями, и возвращает его приложению.</span><span class="sxs-lookup"><span data-stu-id="256d4-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="256d4-180">Когда приложение завершает обработку сообщения (или сохраняет его для будущей обработки), оно завершает второй этап процесса получения, вызывая метод `ServiceBusRestProxy->deleteMessage` для полученного сообщения.</span><span class="sxs-lookup"><span data-stu-id="256d4-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="256d4-181">Когда служебная шина обнаруживает вызов метода `deleteMessage`, она помечает сообщение как использованное и удаляет его из очереди.</span><span class="sxs-lookup"><span data-stu-id="256d4-181">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="256d4-182">В следующем примере показывается, как получать и обрабатывать сообщения с помощью режима [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) (используется по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="256d4-182">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode to PeekLock (default is ReceiveAndDelete)
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="256d4-183">Практическое руководство. Обработка сбоев приложения и нечитаемых сообщений</span><span class="sxs-lookup"><span data-stu-id="256d4-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="256d4-184">служебная шина предоставляет функции, помогающие корректно выполнить восстановление после ошибок в приложении или трудностей, возникших при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="256d4-184">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="256d4-185">Если приложение-получатель по каким-либо причинам не может обработать сообщение, то оно может вызвать метод `unlockMessage` для полученного сообщения (вместо метода `deleteMessage`).</span><span class="sxs-lookup"><span data-stu-id="256d4-185">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="256d4-186">После этого служебная шина разблокирует сообщение в очереди и сделает его доступным для приема тем же приложением или другим приложением.</span><span class="sxs-lookup"><span data-stu-id="256d4-186">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="256d4-187">Кроме того, с сообщением, заблокированным в очереди, связано время ожидания. Если приложение не сможет обработать сообщение в течение времени ожидания (например, при сбое приложения), служебная шина разблокирует сообщение автоматически и сделает его доступным для приема.</span><span class="sxs-lookup"><span data-stu-id="256d4-187">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="256d4-188">Если сбой приложения происходит после обработки сообщения, но перед отправкой запроса `deleteMessage`, то это сообщение повторно доставляется в приложение после его перезапуска.</span><span class="sxs-lookup"><span data-stu-id="256d4-188">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="256d4-189">Часто такой подход называют *Обработать хотя бы один раз*, т. е. каждое сообщение будет обрабатываться по крайней мере один раз, но в некоторых случаях это же сообщение может быть доставлено повторно.</span><span class="sxs-lookup"><span data-stu-id="256d4-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="256d4-190">Если повторная обработка недопустима, разработчики приложения должны добавить дополнительную логику для обработки повторной доставки сообщений.</span><span class="sxs-lookup"><span data-stu-id="256d4-190">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to applications to handle duplicate message delivery.</span></span> <span data-ttu-id="256d4-191">Часто это достигается с помощью метода `getMessageId` сообщения, который остается постоянным для различных попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="256d4-191">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="256d4-192">Удаление разделов и подписок</span><span class="sxs-lookup"><span data-stu-id="256d4-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="256d4-193">Чтобы удалить раздел или подписку, используйте методы `ServiceBusRestProxy->deleteTopic` или `ServiceBusRestProxy->deleteSubscripton` соответственно.</span><span class="sxs-lookup"><span data-stu-id="256d4-193">To delete a topic or a subscription, use the `ServiceBusRestProxy->deleteTopic` or the `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="256d4-194">Обратите внимание, что при удалении раздела также удаляются все подписки, зарегистрированные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="256d4-194">Note that deleting a topic also deletes any subscriptions that are registered with the topic.</span></span>

<span data-ttu-id="256d4-195">Следующий пример показывает, как удалить раздел `mytopic` и зарегистрированные в нем подписки.</span><span class="sxs-lookup"><span data-stu-id="256d4-195">The following example shows how to delete a topic named `mytopic` and its registered subscriptions.</span></span>

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

<span data-ttu-id="256d4-196">С помощью метода `deleteSubscription` можно удалить подписку независимо.</span><span class="sxs-lookup"><span data-stu-id="256d4-196">By using the `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="256d4-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="256d4-197">Next steps</span></span>
<span data-ttu-id="256d4-198">Вы ознакомились с основами использования очередей служебной шины. Дополнительные сведения см. в статье [Очереди, разделы и подписки служебной шины][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="256d4-198">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
