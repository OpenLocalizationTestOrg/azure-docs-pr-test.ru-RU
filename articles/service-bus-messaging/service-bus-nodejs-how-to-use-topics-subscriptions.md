---
title: "aaaHow toouse Azure Service Bus разделов и подписок с Node.js | Документы Microsoft"
description: "Узнайте, как toouse Service Bus разделы и подписки в Azure из приложения Node.js."
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
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="56f00-103">Как tooUse Service Bus разделов и подписок с Node.js</span><span class="sxs-lookup"><span data-stu-id="56f00-103">How tooUse Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="56f00-104">В этом руководстве описаны как toouse Service Bus разделов и подписок из приложений Node.js.</span><span class="sxs-lookup"><span data-stu-id="56f00-104">This guide describes how toouse Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="56f00-105">Hello сценарии включают **создания разделов и подписок**, **создание фильтров подписок**, **отправки сообщений** разделе tooa **получения сообщения из подписки**, и **удаление разделов и подписок**.</span><span class="sxs-lookup"><span data-stu-id="56f00-105">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="56f00-106">Дополнительные сведения о разделах и подписках см. в разделе hello [дальнейшие действия](#next-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="56f00-106">For more information about topics and subscriptions, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="56f00-107">Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="56f00-107">Create a Node.js application</span></span>
<span data-ttu-id="56f00-108">Создайте пустое приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="56f00-108">Create a blank Node.js application.</span></span> <span data-ttu-id="56f00-109">Инструкции по созданию приложений Node.js см. в разделе [создать и развернуть tooan приложений Node.js веб-сайта Azure], [Node.js облачной службы] [ Node.js Cloud Service] с помощью Windows PowerShell или веб-сайт в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="56f00-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooan Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="56f00-110">Настройка вашего приложения toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="56f00-110">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="56f00-111">toouse Service Bus, загрузите hello Node.js Azure пакета.</span><span class="sxs-lookup"><span data-stu-id="56f00-111">toouse Service Bus, download hello Node.js Azure package.</span></span> <span data-ttu-id="56f00-112">Этот пакет содержит набор библиотек, взаимодействующих со службами Service Bus REST hello.</span><span class="sxs-lookup"><span data-stu-id="56f00-112">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="56f00-113">С помощью диспетчера пакетов узла (NPM) tooobtain hello пакета</span><span class="sxs-lookup"><span data-stu-id="56f00-113">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="56f00-114">Использовать интерфейс командной строки, такие как **PowerShell** (Windows), **терминалов** (Mac), или **Bash** (Unix), перейдите в папку toohello, где создан пример приложения.</span><span class="sxs-lookup"><span data-stu-id="56f00-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="56f00-115">Тип **npm Установка azure** в командном окне приветствия, что должно привести к hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="56f00-115">Type **npm install azure** in hello command window, which should result in hello following output:</span></span>

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
3. <span data-ttu-id="56f00-116">Вы можете вручную запустить hello **ls** tooverify команды, **узел\_модули** папка была создана.</span><span class="sxs-lookup"><span data-stu-id="56f00-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="56f00-117">В этой папке можно найти **azure** пакет, который содержит hello библиотеки tooaccess разделы служебной шины.</span><span class="sxs-lookup"><span data-stu-id="56f00-117">Inside that folder find the **azure** package, which contains hello libraries you need tooaccess Service Bus topics.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="56f00-118">Импорт модуля hello</span><span class="sxs-lookup"><span data-stu-id="56f00-118">Import hello module</span></span>
<span data-ttu-id="56f00-119">С помощью блокнота или другого текстового редактора, добавьте следующие toohello вверху hello hello **server.js** файл приложения hello:</span><span class="sxs-lookup"><span data-stu-id="56f00-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="56f00-120">Настройка подключения к Service Bus</span><span class="sxs-lookup"><span data-stu-id="56f00-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="56f00-121">Hello Azure модуль считывает переменные среды hello `AZURE_SERVICEBUS_NAMESPACE` и `AZURE_SERVICEBUS_ACCESS_KEY` сведения необходимые tooconnect tooService шины.</span><span class="sxs-lookup"><span data-stu-id="56f00-121">hello Azure module reads hello environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required tooconnect tooService Bus.</span></span> <span data-ttu-id="56f00-122">Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello при вызове `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="56f00-122">If these environment variables are not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="56f00-123">Пример настройки переменных среды hello для облачной службы Azure см. в разделе [Node.js облачной службы с хранилищем][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="56f00-123">For an example of setting hello environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="56f00-124">Пример настройки hello переменных среды для веб-сайта Azure, в разделе [Node.js веб-приложение с хранилищем][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="56f00-124">For an example of setting hello environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="56f00-125">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="56f00-125">Create a topic</span></span>
<span data-ttu-id="56f00-126">Hello **ServiceBusService** позволяет toowork с разделами.</span><span class="sxs-lookup"><span data-stu-id="56f00-126">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="56f00-127">Следующий код создает объект **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="56f00-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="56f00-128">Добавьте его в верхней части hello **server.js** файла после tooimport hello azure hello инструкции модуля:</span><span class="sxs-lookup"><span data-stu-id="56f00-128">Add it near the top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="56f00-129">Путем вызова `createTopicIfNotExists` на hello **ServiceBusService** объекта hello указано, раздел возвращается (если он существует), или создается новый раздел с указанным именем hello.</span><span class="sxs-lookup"><span data-stu-id="56f00-129">By calling `createTopicIfNotExists` on hello **ServiceBusService** object, hello specified topic will be returned (if it exists,) or a new topic with hello specified name will be created.</span></span> <span data-ttu-id="56f00-130">Hello следующий код использует `createTopicIfNotExists` toocreate или подключения с именем раздела toohello `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="56f00-130">hello following code uses `createTopicIfNotExists` toocreate or connect toohello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="56f00-131">Hello `createServiceBusService` метод также поддерживает дополнительные параметры, позволяющие toooverride параметры раздела по умолчанию срок жизни сообщения или максимальный размер раздела.</span><span class="sxs-lookup"><span data-stu-id="56f00-131">hello `createServiceBusService` method also supports additional options, which enable you toooverride default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="56f00-132">Hello следующий пример задает hello максимальное число разделов размер too5GB со временем toolive 1 минута:</span><span class="sxs-lookup"><span data-stu-id="56f00-132">hello following example sets hello maximum topic size too5GB with a time toolive of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="56f00-133">Фильтры</span><span class="sxs-lookup"><span data-stu-id="56f00-133">Filters</span></span>
<span data-ttu-id="56f00-134">Необязательный операции фильтрации может быть применен toooperations, выполняемые с помощью **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="56f00-134">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="56f00-135">К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, которые реализуют метод с сигнатурой hello:</span><span class="sxs-lookup"><span data-stu-id="56f00-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="56f00-136">После выполнения предварительной обработки на параметры запроса hello, hello вызовов метода `next`, передача обратный вызов с hello следующие подписи:</span><span class="sxs-lookup"><span data-stu-id="56f00-136">After performing preprocessing on hello request options, hello method calls `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="56f00-137">В этот обратный вызов и после обработки hello `returnObject` (hello ответа от сервера toohello hello запроса), обратного вызова hello необходимы tooeither вызова рядом, если он существует toocontinue обработки других фильтров или вызвать `finalCallback` в противном случае — tooend hello вызов службы.</span><span class="sxs-lookup"><span data-stu-id="56f00-137">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or invoke `finalCallback` otherwise, tooend hello service invocation.</span></span>

<span data-ttu-id="56f00-138">Два фильтра, которые реализовать логику повторных попыток входят в состав hello Azure SDK для Node.js **ExponentialRetryPolicyFilter** и **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="56f00-138">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="56f00-139">Hello следующий код создает **ServiceBusService** объект, который использует hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="56f00-139">hello following creates a **ServiceBusService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="56f00-140">Создание подписок</span><span class="sxs-lookup"><span data-stu-id="56f00-140">Create subscriptions</span></span>
<span data-ttu-id="56f00-141">Подписок раздела также создаются с hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="56f00-141">Topic subscriptions are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="56f00-142">Подписки представляют собой именованные и может иметь дополнительный фильтр, ограничивающий набор hello сообщения, доставленные toohello в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="56f00-142">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="56f00-143">Подписки являются постоянными и продолжится до либо они tooexist или hello раздел они связаны, будут удалены.</span><span class="sxs-lookup"><span data-stu-id="56f00-143">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="56f00-144">Если приложение содержит логику toocreate подписки, он сначала проверить Если hello подписка уже существует, с помощью `getSubscription` метод.</span><span class="sxs-lookup"><span data-stu-id="56f00-144">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="56f00-145">Создайте подписку с фильтром (MatchAll) по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="56f00-145">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="56f00-146">Hello **MatchAll** фильтром является фильтр по умолчанию hello, который используется, если не указан фильтр при создании новой подписки.</span><span class="sxs-lookup"><span data-stu-id="56f00-146">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="56f00-147">Здравствуйте, когда **MatchAll** используется фильтр, раздел опубликованного toohello все сообщения помещаются в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="56f00-147">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="56f00-148">Hello следующем примере создается подписка с именем «AllMessages» и по умолчанию hello использует **MatchAll** фильтра.</span><span class="sxs-lookup"><span data-stu-id="56f00-148">hello following example creates a subscription named 'AllMessages' and uses hello default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="56f00-149">Создание подписок с фильтрами</span><span class="sxs-lookup"><span data-stu-id="56f00-149">Create subscriptions with filters</span></span>
<span data-ttu-id="56f00-150">Можно также создать фильтры, позволяющие tooscope сообщений отправила разделе tooa должно отображаться в рамках подписки определенный раздел.</span><span class="sxs-lookup"><span data-stu-id="56f00-150">You can also create filters that allow you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="56f00-151">Hello самый гибкий тип фильтра, поддерживаемых подписок — **SqlFilter**, который реализует подмножество SQL92.</span><span class="sxs-lookup"><span data-stu-id="56f00-151">hello most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="56f00-152">Фильтры SQL работают с свойств сообщений hello, раздел опубликованного toohello hello.</span><span class="sxs-lookup"><span data-stu-id="56f00-152">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="56f00-153">Дополнительные сведения о выражениях hello, которые могут использоваться с фильтром SQL просмотрите hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="56f00-153">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="56f00-154">Фильтры можно добавлять tooa подписки с помощью hello `createRule` метод hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="56f00-154">Filters can be added tooa subscription by using hello `createRule` method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="56f00-155">Этот метод позволяет добавить новую подписку tooan существующие фильтры.</span><span class="sxs-lookup"><span data-stu-id="56f00-155">This method allows you to add new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="56f00-156">Так как автоматически применяется фильтр по умолчанию hello tooall новых подписок, необходимо сначала удалить фильтр по умолчанию hello или **MatchAll** переопределит все фильтры, можно указать.</span><span class="sxs-lookup"><span data-stu-id="56f00-156">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="56f00-157">Правило по умолчанию hello можно удалить с помощью hello `deleteRule` метод **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="56f00-157">You can remove hello default rule by using hello `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="56f00-158">Hello следующий пример создает подписку с именем `HighMessages` с **SqlFilter** , выбирает только сообщения, которые содержат пользовательского `messagenumber` свойство больше 3:</span><span class="sxs-lookup"><span data-stu-id="56f00-158">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="56f00-159">Аналогичным образом hello следующий пример создает подписку с именем `LowMessages` с **SqlFilter** , выбирает только сообщения, которые содержат `messagenumber` свойства меньше или равно too3:</span><span class="sxs-lookup"><span data-stu-id="56f00-159">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

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

<span data-ttu-id="56f00-160">Если теперь отправляется сообщение слишком`MyTopic`, всегда будут предоставляться для приемников подписана toohello `AllMessages` подписки раздела и выборочно доставленный tooreceivers подписка toohello `HighMessages` и `LowMessages` подписок раздела (зависимости от содержимого сообщения hello).</span><span class="sxs-lookup"><span data-stu-id="56f00-160">When a message is now sent too`MyTopic`, it will always be delivered to receivers subscribed toohello `AllMessages` topic subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="how-toosend-messages-tooa-topic"></a><span data-ttu-id="56f00-161">Способ toosend сообщений tooa раздела</span><span class="sxs-lookup"><span data-stu-id="56f00-161">How toosend messages tooa topic</span></span>
<span data-ttu-id="56f00-162">toosend раздела Service Bus tooa сообщения, приложение должно использовать `sendTopicMessage` метод hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="56f00-162">toosend a message tooa Service Bus topic, your application must use the `sendTopicMessage` method of hello **ServiceBusService** object.</span></span>
<span data-ttu-id="56f00-163">Отправлять сообщения, разделы шины tooService **BrokeredMessage** объектов.</span><span class="sxs-lookup"><span data-stu-id="56f00-163">Messages sent tooService Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="56f00-164">**BrokeredMessage** объекты имеют набор стандартных свойств (например, `Label` и `TimeToLive`), словаря, используемые toohold пользовательские свойства для конкретного приложения и текст строки данных.</span><span class="sxs-lookup"><span data-stu-id="56f00-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="56f00-165">Приложение может установить текст hello приветственное сообщение, передав значение строки hello `sendTopicMessage` и любые необходимые стандартные свойства заполняются значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="56f00-165">An application can set hello body of hello message by passing a string value to hello `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="56f00-166">Hello следующем примере показано, как toosend пять тестовых сообщений для `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="56f00-166">hello following example demonstrates how toosend five test messages to `MyTopic`.</span></span> <span data-ttu-id="56f00-167">Обратите внимание, что hello `messagenumber` зависит от значения свойства каждого сообщения hello итерацию цикла hello (Это определяет, какие подписки получают его):</span><span class="sxs-lookup"><span data-stu-id="56f00-167">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="56f00-168">Темы Service Bus поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="56f00-168">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="56f00-169">Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="56f00-169">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="56f00-170">Нет ограничений на hello количество сообщений, которые содержатся в разделе, но отсутствует ограничение на общий размер сообщений hello, удерживаемые раздела hello.</span><span class="sxs-lookup"><span data-stu-id="56f00-170">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="56f00-171">Этот размер раздела определяется при создании с верхним пределом 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="56f00-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="56f00-172">Получение сообщений из подписки</span><span class="sxs-lookup"><span data-stu-id="56f00-172">Receive messages from a subscription</span></span>
<span data-ttu-id="56f00-173">Сообщения принимаются из подписки с помощью `receiveSubscriptionMessage` метод hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="56f00-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="56f00-174">По умолчанию сообщения удаляются из подписки hello, как они доступны для чтения; Однако можно считать (Просмотр) и заблокировать приветственное сообщение, не удаляя ее из подписки hello параметр необязательным параметром hello `isPeekLock` слишком**true**.</span><span class="sxs-lookup"><span data-stu-id="56f00-174">By default, messages are deleted from hello subscription as they are read; however, you can read (peek) and lock hello message without deleting it from hello subscription by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="56f00-175">поведение по умолчанию Hello чтение и удаление приветственное сообщение, как часть операции receive — самая простая модель hello и работает лучше для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="56f00-175">hello default behavior of reading and deleting hello message as part of the receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="56f00-176">toounderstand это, рассмотрим сценарий, в котором hello проблемы потребителя получают запрос и затем ломается до его обработки.</span><span class="sxs-lookup"><span data-stu-id="56f00-176">toounderstand this, consider a scenario in which the consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="56f00-177">Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="56f00-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="56f00-178">Если hello `isPeekLock` параметра установлено слишком**true**, получать hello становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="56f00-178">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="56f00-179">Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="56f00-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span>
<span data-ttu-id="56f00-180">После приложения hello завершает обработку сообщения hello (или хранит его для будущей обработки), он завершается hello второй этап процесса получения путем вызова **deleteMessage** метод и предоставляя toobe сообщения удален в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="56f00-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of the receive process by calling **deleteMessage** method and providing the message toobe deleted as a parameter.</span></span> <span data-ttu-id="56f00-181">Hello **deleteMessage** метод будет пометить приветственное сообщение как полученное и удалите его из подписки hello.</span><span class="sxs-lookup"><span data-stu-id="56f00-181">hello **deleteMessage** method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="56f00-182">Hello следующем примере показано, как можно получать сообщения и обработанные с помощью `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="56f00-182">hello following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="56f00-183">Hello примере впервые получает и удаляет сообщение из подписки «LowMessages» hello и затем получает сообщение из подписки «HighMessages» hello с помощью `isPeekLock` задать tootrue.</span><span class="sxs-lookup"><span data-stu-id="56f00-183">hello example first receives and deletes a message from hello 'LowMessages' subscription, and then receives a message from hello 'HighMessages' subscription using `isPeekLock` set tootrue.</span></span> <span data-ttu-id="56f00-184">Затем удаляет сообщение hello с помощью `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="56f00-184">It then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="56f00-185">Как происходит сбой toohandle приложения и может быть прочитан сообщений</span><span class="sxs-lookup"><span data-stu-id="56f00-185">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="56f00-186">Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="56f00-186">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="56f00-187">Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlockMessage` метод **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="56f00-187">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="56f00-188">Это будет вызвать toounlock Service Bus сообщение в рамках подписки hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.</span><span class="sxs-lookup"><span data-stu-id="56f00-188">This will cause Service Bus toounlock the message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="56f00-189">Также существует время ожидания, связанные с сообщением, заблокирован в подписке, и при сбое приложения hello tooprocess приветственное сообщение, прежде чем hello срок блокировки (например, если приложение hello терпит сбой), а затем Service Bus разблокирует сообщение hello автоматически и делает ее доступной toobe получили еще раз.</span><span class="sxs-lookup"><span data-stu-id="56f00-189">There is also a timeout associated with a message locked within the subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="56f00-190">В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `deleteMessage` вызывается метод, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="56f00-190">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="56f00-191">Это часто называется *по крайней мере после обработки*, то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться.</span><span class="sxs-lookup"><span data-stu-id="56f00-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="56f00-192">Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений.</span><span class="sxs-lookup"><span data-stu-id="56f00-192">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="56f00-193">Это можно сделать с помощью **MessageId** свойство сообщения hello, который остается постоянным протяжении всех попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="56f00-193">This is often achieved using the **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="56f00-194">Удаление разделов и подписок</span><span class="sxs-lookup"><span data-stu-id="56f00-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="56f00-195">Разделы и подписки являются постоянными, а должен быть явно удалены, либо через hello [портал Azure] [ Azure portal] или программными средствами.</span><span class="sxs-lookup"><span data-stu-id="56f00-195">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="56f00-196">Hello следующем примере показано, как toodelete hello раздел с именем `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="56f00-196">hello following example demonstrates how toodelete hello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="56f00-197">Удаление раздела приведет к удалению всех подписок, зарегистрированных в разделе hello.</span><span class="sxs-lookup"><span data-stu-id="56f00-197">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="56f00-198">Подписки также можно удалять по отдельности.</span><span class="sxs-lookup"><span data-stu-id="56f00-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="56f00-199">В следующем примере показано, как toodelete подписки именоваться `HighMessages` из hello `MyTopic` раздела:</span><span class="sxs-lookup"><span data-stu-id="56f00-199">The following example shows how toodelete a subscription named `HighMessages` from hello `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="56f00-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="56f00-200">Next Steps</span></span>
<span data-ttu-id="56f00-201">Теперь, когда вы узнали основы hello разделов Service Bus, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="56f00-201">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="56f00-202">Дополнительные сведения см. в статье [Очереди, разделы и подписки служебной шины][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="56f00-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="56f00-203">Справочник API для [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="56f00-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="56f00-204">Посетите hello [Azure SDK для узла] [ Azure SDK for Node] репозитория в GitHub.</span><span class="sxs-lookup"><span data-stu-id="56f00-204">Visit hello [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[создать и развернуть tooan приложений Node.js веб-сайта Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
