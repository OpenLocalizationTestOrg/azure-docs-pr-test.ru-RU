---
title: "Использование разделов и подписок служебной шины Azure с Node.js | Документация Майкрософт"
description: "Узнайте, как использовать разделы и подписки служебной шины в Azure в приложении Node.js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 24ae9b80f75531c5e4a84c3b4a6666a6f8a83d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="4e7b8-103">Как использовать разделы и подписки служебной шины с Node.js</span><span class="sxs-lookup"><span data-stu-id="4e7b8-103">How to Use Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="4e7b8-104">В этом руководстве показано, как использовать разделы и подписки служебной шины в приложениях Node.js.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-104">This guide describes how to use Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="4e7b8-105">В этой статье описаны такие сценарии, как **создание разделов и подписок**, **создание фильтров подписок**, **отправка сообщений в раздел**, **получение сообщений из подписки** и **удаление разделов и подписок**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-105">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="4e7b8-106">Дополнительные сведения о разделах и подписках см. в разделе [Дальнейшие действия](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="4e7b8-106">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="4e7b8-107">Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="4e7b8-107">Create a Node.js application</span></span>
<span data-ttu-id="4e7b8-108">Создайте пустое приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-108">Create a blank Node.js application.</span></span> <span data-ttu-id="4e7b8-109">Указания по созданию приложения Node.js см. в статьях [Создание и развертывание веб-приложения Node.js в службе приложений Azure], [Построение и развертывание приложения Node.js в облачной службе Azure][Node.js Cloud Service] (с помощью Windows PowerShell) или "Создание и развертывание веб-приложения Node.js в Azure с использованием WebMatrix".</span><span class="sxs-lookup"><span data-stu-id="4e7b8-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to an Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="4e7b8-110">Настройка приложения для использования служебной шины</span><span class="sxs-lookup"><span data-stu-id="4e7b8-110">Configure your application to use Service Bus</span></span>
<span data-ttu-id="4e7b8-111">Для использования служебной шины скачайте пакет Node.js для Azure.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-111">To use Service Bus, download the Node.js Azure package.</span></span> <span data-ttu-id="4e7b8-112">Пакет содержит набор библиотек, взаимодействующих со службами REST Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-112">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="4e7b8-113">Использование диспетчера пакета Node (NPM) для получения пакета</span><span class="sxs-lookup"><span data-stu-id="4e7b8-113">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="4e7b8-114">Используя интерфейс командной строки, такой как **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix), перейдите в папку, в которой создан пример приложения.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="4e7b8-115">В командной строке введите команду **npm install azure**. Должен получиться вот такой результат:</span><span class="sxs-lookup"><span data-stu-id="4e7b8-115">Type **npm install azure** in the command window, which should result in the following output:</span></span>

   ```
       azure@0.7.5 node_modules\azure
   ├── dateformat@1.0.2-1.2.3
   ├── xmlbuilder@0.4.2
   ├── node-uuid@1.2.0
   ├── mime@1.2.9
   ├── underscore@1.4.4
   ├── validator@1.1.1
   ├── tunnel@0.0.2
   ├── wns@0.5.3
   ├── xml2js@0.2.7 (sax@0.5.2)
   └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
   ```
3. <span data-ttu-id="4e7b8-116">Выполнив команду **ls** вручную, можно убедиться, что папка **node\_modules** создана.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="4e7b8-117">Найдите в папке пакет **azure**, который содержит библиотеки, необходимые для доступа к разделам служебной шины.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-117">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus topics.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="4e7b8-118">Импорт модуля</span><span class="sxs-lookup"><span data-stu-id="4e7b8-118">Import the module</span></span>
<span data-ttu-id="4e7b8-119">С помощью Блокнота или другого текстового редактора добавьте в начало файла **server.js** приложения следующее:</span><span class="sxs-lookup"><span data-stu-id="4e7b8-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="4e7b8-120">Настройка подключения к Service Bus</span><span class="sxs-lookup"><span data-stu-id="4e7b8-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="4e7b8-121">Модуль Azure считывает переменные среды `AZURE_SERVICEBUS_NAMESPACE` и `AZURE_SERVICEBUS_ACCESS_KEY`, чтобы получить сведения, необходимые для подключения к служебной шине.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-121">The Azure module reads the environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required to connect to Service Bus.</span></span> <span data-ttu-id="4e7b8-122">Если эти переменные среды не заданы, при вызове `createServiceBusService` необходимо указать сведения об учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-122">If these environment variables are not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="4e7b8-123">Пример настройки переменных среды для облачной службы Azure см. в статье [Облачная служба Node.js с хранилищем][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="4e7b8-123">For an example of setting the environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="4e7b8-124">Пример настройки переменных среды для веб-сайта Azure см. в статье [Веб-приложение Node.js с хранилищем][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="4e7b8-124">For an example of setting the environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="4e7b8-125">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="4e7b8-125">Create a topic</span></span>
<span data-ttu-id="4e7b8-126">Объект **ServiceBusService** позволяет работать с разделами.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-126">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="4e7b8-127">Следующий код создает объект **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="4e7b8-128">Добавьте его в начало файла **server.js** после оператора импорта модуля Аzure.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-128">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="4e7b8-129">Вызов `createTopicIfNotExists` для объекта **ServiceBusService** возвратит указанный раздел (при его наличии) или создаст новый раздел с указанным именем.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-129">By calling `createTopicIfNotExists` on the **ServiceBusService** object, the specified topic will be returned (if it exists,) or a new topic with the specified name will be created.</span></span> <span data-ttu-id="4e7b8-130">В следующем коде используется метод `createTopicIfNotExists`, чтобы создать раздел `MyTopic` или подключиться к нему.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-130">The following code uses `createTopicIfNotExists` to create or connect to the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="4e7b8-131">Метод `createServiceBusService` также поддерживает дополнительные параметры, позволяющие переопределить настройки раздела по умолчанию, такие как срок жизни сообщения или максимальный размер раздела.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-131">The `createServiceBusService` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="4e7b8-132">В следующем примере показано, как установить максимальный размер раздела 5 ГБ и значение срока жизни в 1 минуту.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-132">The following example sets the maximum topic size to 5GB with a time to live of 1 minute:</span></span>

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="4e7b8-133">Фильтры</span><span class="sxs-lookup"><span data-stu-id="4e7b8-133">Filters</span></span>
<span data-ttu-id="4e7b8-134">Используя **ServiceBusService**, к выполняемым операциям можно применить дополнительные операции фильтрации.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-134">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="4e7b8-135">К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, реализующими метод со следующей сигнатурой:</span><span class="sxs-lookup"><span data-stu-id="4e7b8-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="4e7b8-136">Выполнив предварительную обработку параметров запроса, метод вызывает `next`, передавая обратный вызов со следующей сигнатурой:</span><span class="sxs-lookup"><span data-stu-id="4e7b8-136">After performing preprocessing on the request options, the method calls `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="4e7b8-137">В этом примере, а также после обработки `returnObject` (ответа на запрос к серверу) функция обратного вызова должна вызвать функцию next (если она существует), чтобы продолжить обработку других фильтров, или же вызвать `finalCallback`, чтобы завершить вызов службы.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-137">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or invoke `finalCallback` otherwise, to end the service invocation.</span></span>

<span data-ttu-id="4e7b8-138">В пакет SDK Azure для Node.js включены два фильтра, реализующие логику повторных попыток: **ExponentialRetryPolicyFilter** и **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="4e7b8-139">Следующий код создает объект **ServiceBusService**, использующий **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="4e7b8-139">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="4e7b8-140">Создание подписок</span><span class="sxs-lookup"><span data-stu-id="4e7b8-140">Create subscriptions</span></span>
<span data-ttu-id="4e7b8-141">Подписки на разделы также создаются с помощью объекта **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-141">Topic subscriptions are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="4e7b8-142">Подписки имеют имена и могут использовать дополнительный фильтр, который ограничивает набор сообщений, доставляемых в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-142">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="4e7b8-143">Подписки являются постоянными и продолжают существовать либо до их удаления, либо до удаления раздела, с которым они связаны.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-143">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="4e7b8-144">Если приложение содержит логику для создания подписки, оно сначала должно проверить, существует ли подписка, используя метод `getSubscription`.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-144">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="4e7b8-145">Создание подписки с фильтром по умолчанию (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="4e7b8-145">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="4e7b8-146">Фильтр **MatchAll** является фильтром по умолчанию, используемым, если при создании новой подписки не указан фильтр.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-146">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="4e7b8-147">Если используется фильтр **MatchAll**, то все сообщения, опубликованные в разделе, помещаются в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-147">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="4e7b8-148">В следующем примере создается подписка AllMessages и используется фильтр по умолчанию **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-148">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="4e7b8-149">Создание подписок с фильтрами</span><span class="sxs-lookup"><span data-stu-id="4e7b8-149">Create subscriptions with filters</span></span>
<span data-ttu-id="4e7b8-150">Вы также можете создать фильтры, позволяющие определять, какие сообщения, отправленные в раздел, будут отображаться в той или иной подписке раздела.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-150">You can also create filters that allow you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="4e7b8-151">Самый гибкий тип фильтра, который поддерживается подписками, — это **SqlFilter**, реализующий подмножество SQL92.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-151">The most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="4e7b8-152">Фильтры SQL работают со свойствами сообщений, которые опубликованы в разделе.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-152">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="4e7b8-153">Дополнительные сведения о выражениях, которые можно использовать с фильтром SQL, см. в описании синтаксиса [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="4e7b8-153">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="4e7b8-154">Добавить фильтры в подписку можно с помощью метода `createRule` объекта **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-154">Filters can be added to a subscription by using the `createRule` method of the **ServiceBusService** object.</span></span> <span data-ttu-id="4e7b8-155">Этот метод позволяет добавлять новые фильтры в существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-155">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4e7b8-156">Так как ко всем новым подпискам автоматически применяется фильтр по умолчанию, сначала необходимо удалить фильтр по умолчанию, иначе фильтр **MatchAll** переопределит поведение всех остальных заданных фильтров.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-156">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="4e7b8-157">Вы можете удалить правило по умолчанию с помощью метода `deleteRule` объекта **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-157">You can remove the default rule by using the `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="4e7b8-158">В следующем примере создается подписка `HighMessages`, содержащая фильтр **SqlFilter**, который выбирает только те сообщения, значение настраиваемого свойства `messagenumber` которых больше 3.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-158">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="4e7b8-159">Аналогичным образом в следующем примере создается подписка `LowMessages` с фильтром **SqlFilter**, который выбирает только те сообщения, значение настраиваемого свойства `messagenumber` которых меньше или равно 3.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-159">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="4e7b8-160">Если сообщение отправляется в раздел `MyTopic`, оно всегда будет доставляться в приемники, подписанные на подписку раздела `AllMessages`, и в отдельные приемники, подписанные на подписки разделов `HighMessages` и `LowMessages` (в зависимости от содержимого сообщения).</span><span class="sxs-lookup"><span data-stu-id="4e7b8-160">When a message is now sent to `MyTopic`, it will always be delivered to receivers subscribed to the `AllMessages` topic subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` topic subscriptions (depending upon the message content).</span></span>

## <a name="how-to-send-messages-to-a-topic"></a><span data-ttu-id="4e7b8-161">Как отправлять сообщения в раздел</span><span class="sxs-lookup"><span data-stu-id="4e7b8-161">How to send messages to a topic</span></span>
<span data-ttu-id="4e7b8-162">Чтобы отправить сообщение в раздел служебной шины, приложение должно использовать метод `sendTopicMessage` объекта **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-162">To send a message to a Service Bus topic, your application must use the `sendTopicMessage` method of the **ServiceBusService** object.</span></span>
<span data-ttu-id="4e7b8-163">Сообщения, отправленные в разделы служебной шины, являются объектами **BrokeredMessage**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-163">Messages sent to Service Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="4e7b8-164">Объекты **BrokeredMessage** содержат набор стандартных свойств (например, `Label` и `TimeToLive`), словарь, используемый для хранения настраиваемых свойств приложения, и текст из строковых данных.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="4e7b8-165">Приложение может задавать текст сообщения, передавая строковое значение в `sendTopicMessage`, и все обязательные стандартные свойства будут заполнены значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-165">An application can set the body of the message by passing a string value to the `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="4e7b8-166">В следующем примере показано, как отправить пять тестовых сообщений в `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-166">The following example demonstrates how to send five test messages to `MyTopic`.</span></span> <span data-ttu-id="4e7b8-167">Обратите внимание, что значение свойства `messagenumber` каждого сообщения зависит от итерации цикла (определяет, какие подписки его получают).</span><span class="sxs-lookup"><span data-stu-id="4e7b8-167">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

<span data-ttu-id="4e7b8-168">Разделы служебной шины поддерживают максимальный размер сообщения 256 КБ для [уровня "Стандартный"](service-bus-premium-messaging.md) и 1 МБ для [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="4e7b8-168">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="4e7b8-169">Максимальный размер заголовка, который содержит стандартные и настраиваемые свойства приложения, — 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-169">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="4e7b8-170">Ограничения на количество сообщений в разделе нет, но есть максимальный общий размер сообщений, содержащихся в разделе.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-170">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="4e7b8-171">Этот размер раздела определяется при создании с верхним пределом 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="4e7b8-172">Получение сообщений из подписки</span><span class="sxs-lookup"><span data-stu-id="4e7b8-172">Receive messages from a subscription</span></span>
<span data-ttu-id="4e7b8-173">Сообщения извлекаются из подписки с помощью метода `receiveSubscriptionMessage` для объекта **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="4e7b8-174">По умолчанию прочитанные сообщения удаляются из подписки. Но сообщение можно прочитать (просмотреть) и заблокировать, не удаляя его из подписки. Для этого следует задать для необязательного параметра `isPeekLock` значение **true**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-174">By default, messages are deleted from the subscription as they are read; however, you can read (peek) and lock the message without deleting it from the subscription by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="4e7b8-175">Поведение по умолчанию — чтение и удаление сообщения как часть операции получения — это простейшая модель, оптимальная для сценариев, в которых приложение может не обрабатывать сообщение в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-175">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="4e7b8-176">Чтобы это понять, рассмотрим сценарий, в котором объект-получатель выдает запрос на получение и выходит из строя до его обработки.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="4e7b8-177">Поскольку служебная шина помечает сообщение как использованное, то когда после своего перезапуска приложение снова начнет обрабатывать сообщения, оно пропустит сообщение, использованное до сбоя.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="4e7b8-178">Если параметр `isPeekLock` имеет значение **true**, получение становится операцией из двух этапов, что позволяет поддерживать приложения, неустойчивые к пропуску сообщений.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-178">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="4e7b8-179">Получив запрос, служебная шина находит следующее сообщение, блокирует его, чтобы предотвратить его получение другими получателями, и возвращает его приложению.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span>
<span data-ttu-id="4e7b8-180">Обработав сообщение (или сохранив его в надежном месте для последующей обработки), приложение вызывает метод **deleteMessage** и указывает сообщение, которое будет удалено как параметр, таким образом завершая второй этап процесса получения.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="4e7b8-181">Метод **deleteMessage** помечает сообщение как использованное и удаляет его из подписки.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-181">The **deleteMessage** method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="4e7b8-182">В следующем примере показано, как получать и обрабатывать сообщения с помощью метода `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-182">The following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="4e7b8-183">В этом примере сначала поступает и удаляется сообщение из подписки LowMessages, затем поступает сообщение из подписки HighMessages при значении true, заданном для параметра `isPeekLock`.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-183">The example first receives and deletes a message from the 'LowMessages' subscription, and then receives a message from the 'HighMessages' subscription using `isPeekLock` set to true.</span></span> <span data-ttu-id="4e7b8-184">Затем сообщение удаляется с помощью метода `deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-184">It then deletes the message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="4e7b8-185">Как обрабатывать сбои приложения и нечитаемые сообщения</span><span class="sxs-lookup"><span data-stu-id="4e7b8-185">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="4e7b8-186">служебная шина предоставляет функции, помогающие корректно выполнить восстановление после ошибок в приложении или трудностей, возникших при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-186">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="4e7b8-187">Если по какой-либо причине приложению-получателю не удается обработать сообщение, оно вызывает метод `unlockMessage` для объекта **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-187">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="4e7b8-188">После этого служебная шина разблокирует сообщение в подписке и сделает его доступным для приема тем же приложением или другим приложением.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-188">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="4e7b8-189">Кроме того, при блокировке сообщения в подписке предусмотрено определенное время ожидания. Если приложение не может обработать сообщение до истечения времени блокировки (например, аварийно завершит работу), то служебная шина автоматически разблокирует сообщение и оно станет доступным для повторного получения.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-189">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="4e7b8-190">Если в приложении происходит сбой после обработки сообщения, но перед вызовом метода `deleteMessage`, сообщение будет повторно доставлено в приложение после его перезапуска.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-190">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="4e7b8-191">Часто этот подход называют *обработать хотя бы один раз*, т. е. каждое сообщение будет обрабатываться по крайней мере один раз, но в некоторых случаях это же сообщение может быть доставлено повторно.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="4e7b8-192">Если повторная обработка недопустима, разработчики приложения должны добавить дополнительную логику для обработки повторной доставки сообщений.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-192">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="4e7b8-193">Часто это достигается с помощью свойства **MessageId** сообщения, которое остается постоянным для различных попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-193">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="4e7b8-194">Удаление разделов и подписок</span><span class="sxs-lookup"><span data-stu-id="4e7b8-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="4e7b8-195">Разделы и подписки хранятся постоянно, и их нужно удалять явным образом на [портале Azure][Azure portal] или с помощью программных средств.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-195">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="4e7b8-196">В следующем примере показано, как удалить раздел с именем `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-196">The following example demonstrates how to delete the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="4e7b8-197">При удалении раздела также удаляются все подписки, зарегистрированные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-197">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="4e7b8-198">Подписки также можно удалять по отдельности.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="4e7b8-199">В следующем примере показано, как удалить подписку с именем `HighMessages` из раздела `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-199">The following example shows how to delete a subscription named `HighMessages` from the `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="4e7b8-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e7b8-200">Next Steps</span></span>
<span data-ttu-id="4e7b8-201">Вы узнали основные сведения о разделах служебной шины. Для получения дополнительных сведений используйте следующие ссылки.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-201">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="4e7b8-202">Дополнительные сведения см. в статье [Очереди, разделы и подписки служебной шины][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="4e7b8-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="4e7b8-203">Справочник API для [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="4e7b8-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="4e7b8-204">Посетите репозиторий [пакет Azure SDK для Node][Azure SDK for Node] на веб-сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="4e7b8-204">Visit the [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Создание и развертывание веб-приложения Node.js в службе приложений Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
