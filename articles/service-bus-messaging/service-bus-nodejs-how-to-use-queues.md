---
title: "aaaHow toouse Service Bus очереди в Node.js | Документы Microsoft"
description: "Узнайте, как очереди toouse Service Bus в Azure из приложения Node.js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a><span data-ttu-id="f1e33-103">Как очереди toouse Service Bus с Node.js</span><span class="sxs-lookup"><span data-stu-id="f1e33-103">How toouse Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="f1e33-104">В этой статье описывается, как очереди toouse Service Bus с и Node.js.</span><span class="sxs-lookup"><span data-stu-id="f1e33-104">This article describes how toouse Service Bus queues with Node.js.</span></span> <span data-ttu-id="f1e33-105">Hello примеры на языке JavaScript и использовать hello модуля Azure для Node.js.</span><span class="sxs-lookup"><span data-stu-id="f1e33-105">hello samples are written in JavaScript and use hello Node.js Azure module.</span></span> <span data-ttu-id="f1e33-106">Hello сценарии включают **создание очередей**, **отправки и получения сообщений**, и **удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="f1e33-106">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="f1e33-107">Дополнительные сведения об очередях см. в разделе hello [дальнейшие действия](#next-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="f1e33-107">For more information on queues, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="f1e33-108">Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="f1e33-108">Create a Node.js application</span></span>
<span data-ttu-id="f1e33-109">Создайте пустое приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="f1e33-109">Create a blank Node.js application.</span></span> <span data-ttu-id="f1e33-110">Инструкции по toocreate приложении Node.js. в разделе [создать и развернуть tooan приложений Node.js веб-сайта Azure][Create and deploy a Node.js application tooan Azure Website], или [Node.js облачной службы] [ Node.js Cloud Service] с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1e33-110">For instructions on how toocreate a Node.js application, see [Create and deploy a Node.js application tooan Azure Website][Create and deploy a Node.js application tooan Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="f1e33-111">Настройка вашего приложения toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="f1e33-111">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="f1e33-112">toouse Azure Service Bus, загрузите и используйте hello Node.js Azure пакета.</span><span class="sxs-lookup"><span data-stu-id="f1e33-112">toouse Azure Service Bus, download and use hello Node.js Azure package.</span></span> <span data-ttu-id="f1e33-113">Этот пакет содержит набор библиотек, взаимодействующих со службами Service Bus REST hello.</span><span class="sxs-lookup"><span data-stu-id="f1e33-113">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="f1e33-114">С помощью диспетчера пакетов узла (NPM) tooobtain hello пакета</span><span class="sxs-lookup"><span data-stu-id="f1e33-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="f1e33-115">Используйте hello **Windows PowerShell для Node.js** toohello toonavigate окно команд **c:\\узел\\sbqueues\\WebRole1** папку, в которой создан вашей Образец приложения.</span><span class="sxs-lookup"><span data-stu-id="f1e33-115">Use hello **Windows PowerShell for Node.js** command window toonavigate toohello **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="f1e33-116">Тип **npm Установка azure** в командном окне hello, что следует привести к аналогичные toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="f1e33-116">Type **npm install azure** in hello command window, which should result in output similar toohello following:</span></span>

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
3. <span data-ttu-id="f1e33-117">Вы можете вручную запустить hello **ls** tooverify команды, **node_modules** папка была создана.</span><span class="sxs-lookup"><span data-stu-id="f1e33-117">You can manually run hello **ls** command tooverify that a **node_modules** folder was created.</span></span> <span data-ttu-id="f1e33-118">Внутри этой папки поиска hello **azure** пакет, который содержит hello библиотеки tooaccess очереди Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f1e33-118">Inside that folder find hello **azure** package, which contains hello libraries you need tooaccess Service Bus queues.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="f1e33-119">Импорт модуля hello</span><span class="sxs-lookup"><span data-stu-id="f1e33-119">Import hello module</span></span>
<span data-ttu-id="f1e33-120">С помощью блокнота или другого текстового редактора, добавьте следующие toohello вверху hello hello **server.js** файл приложения hello:</span><span class="sxs-lookup"><span data-stu-id="f1e33-120">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="f1e33-121">Настройка подключения к служебной шине Azure</span><span class="sxs-lookup"><span data-stu-id="f1e33-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="f1e33-122">Hello Azure модуль считывает переменной среды hello `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain сведения, необходимые tooconnect tooService шины.</span><span class="sxs-lookup"><span data-stu-id="f1e33-122">hello Azure module reads hello environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain information required tooconnect tooService Bus.</span></span> <span data-ttu-id="f1e33-123">Если эта переменная среды не задано, необходимо указать сведения об учетной записи hello при вызове `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="f1e33-123">If this environment variable is not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="f1e33-124">Пример настройки переменных среды hello в файле конфигурации для облачной службы Azure см. в разделе [Node.js облачной службы с хранилищем][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="f1e33-124">For an example of setting hello environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="f1e33-125">Пример настройки переменных среды hello в hello [портал Azure] [ Azure portal] на веб-сайт Azure в разделе [Node.js веб-приложение с хранилищем] [ Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="f1e33-125">For an example of setting hello environment variables in hello [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="f1e33-126">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="f1e33-126">Create a queue</span></span>
<span data-ttu-id="f1e33-127">Hello **ServiceBusService** позволяет toowork с очередями Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f1e33-127">hello **ServiceBusService** object enables you toowork with Service Bus queues.</span></span> <span data-ttu-id="f1e33-128">Hello следующий код создает **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="f1e33-128">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="f1e33-129">Добавьте его вверху hello hello **server.js** файла после hello инструкции tooimport hello модуль Azure:</span><span class="sxs-lookup"><span data-stu-id="f1e33-129">Add it near hello top of hello **server.js** file, after hello statement tooimport hello Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="f1e33-130">Путем вызова `createQueueIfNotExists` на hello **ServiceBusService** объекта hello указано очереди возвращается (если он существует), или создать новую очередь с указанным именем hello.</span><span class="sxs-lookup"><span data-stu-id="f1e33-130">By calling `createQueueIfNotExists` on hello **ServiceBusService** object, hello specified queue is returned (if it exists), or a new queue with hello specified name is created.</span></span> <span data-ttu-id="f1e33-131">Hello следующий код использует `createQueueIfNotExists` toocreate или подключите toohello очередь с именем `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="f1e33-131">hello following code uses `createQueueIfNotExists` toocreate or connect toohello queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="f1e33-132">Hello `createServiceBusService` метод также поддерживает дополнительные параметры, позволяющие toooverride исходные очереди параметры, такие как очереди toolive или максимальный размер сообщения времени.</span><span class="sxs-lookup"><span data-stu-id="f1e33-132">hello `createServiceBusService` method also supports additional options, which enable you toooverride default queue settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="f1e33-133">Hello следующий пример устанавливает hello максимальный размер too5 ГБ и значение времени toolive (TTL) — 1 минута.</span><span class="sxs-lookup"><span data-stu-id="f1e33-133">hello following example sets hello maximum queue size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="f1e33-134">Фильтры</span><span class="sxs-lookup"><span data-stu-id="f1e33-134">Filters</span></span>
<span data-ttu-id="f1e33-135">Необязательный операции фильтрации может быть применен toooperations, выполняемые с помощью **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="f1e33-135">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="f1e33-136">К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, которые реализуют метод с сигнатурой hello:</span><span class="sxs-lookup"><span data-stu-id="f1e33-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="f1e33-137">После выполнения предварительной обработки на hello параметры запроса, необходимо вызвать метод hello `next`, передача обратный вызов с hello следующие подписи:</span><span class="sxs-lookup"><span data-stu-id="f1e33-137">After doing its pre-processing on hello request options, hello method must call `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="f1e33-138">В этот обратный вызов и после обработки hello `returnObject` (hello ответа от сервера toohello hello запроса), hello обратного вызова должен либо вызвать `next` если он существует toocontinue обработки других фильтров, или просто вызвав `finalCallback`, которая заканчивается вызов службы Hello.</span><span class="sxs-lookup"><span data-stu-id="f1e33-138">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback must either invoke `next` if it exists toocontinue processing other filters, or simply invoke `finalCallback`, which ends hello service invocation.</span></span>

<span data-ttu-id="f1e33-139">Два фильтра, которые реализовать логику повторных попыток входят в состав hello Azure SDK для Node.js `ExponentialRetryPolicyFilter` и `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="f1e33-139">Two filters that implement retry logic are included with hello Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="f1e33-140">Hello следующий код создает `ServiceBusService` объект, который использует hello `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="f1e33-140">hello following code creates a `ServiceBusService` object that uses hello `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="f1e33-141">Отправка сообщений в очереди tooa</span><span class="sxs-lookup"><span data-stu-id="f1e33-141">Send messages tooa queue</span></span>
<span data-ttu-id="f1e33-142">toosend очередью сообщений tooa Service Bus, приложение вызывает hello `sendQueueMessage` метод hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="f1e33-142">toosend a message tooa Service Bus queue, your application calls hello `sendQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="f1e33-143">Сообщений, отправленных слишком (и, полученных от) служебной шины, очереди являются **BrokeredMessage** объектов и иметь набор стандартных свойств (такие как **метка** и **TimeToLive**), словарь, который используется toohold пользовательские свойства для конкретного приложения, и тело произвольных данных приложения.</span><span class="sxs-lookup"><span data-stu-id="f1e33-143">Messages sent too(and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="f1e33-144">Приложение может установить текст hello приветственное сообщение, передав строку как сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="f1e33-144">An application can set hello body of hello message by passing a string as hello message.</span></span> <span data-ttu-id="f1e33-145">Все необходимые стандартные свойства будут заполнены значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f1e33-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="f1e33-146">Hello следующем примере показано, как toosend toohello очереди сообщений теста именоваться `myqueue` с помощью `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="f1e33-146">hello following example demonstrates how toosend a test message toohello queue named `myqueue` using `sendQueueMessage`:</span></span>

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

<span data-ttu-id="f1e33-147">Очереди шины обслуживания поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="f1e33-147">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="f1e33-148">Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="f1e33-148">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="f1e33-149">Нет ограничений на число hello сообщения помещаются в очередь, но отсутствует ограничение на общий размер сообщений hello, хранящиеся в очереди hello.</span><span class="sxs-lookup"><span data-stu-id="f1e33-149">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="f1e33-150">Этот размер очереди, определяемый в момент ее создания, не должен превышать 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="f1e33-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="f1e33-151">Дополнительные сведения о квотах см. в статье [Квоты на служебную шину][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="f1e33-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="f1e33-152">Получение сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="f1e33-152">Receive messages from a queue</span></span>
<span data-ttu-id="f1e33-153">Сообщения принимаются из очереди с помощью hello `receiveQueueMessage` метод hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="f1e33-153">Messages are received from a queue using hello `receiveQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="f1e33-154">По умолчанию сообщения удаляются из очереди hello, как они доступны для чтения; Однако можно считать (Просмотр) и заблокировать приветственное сообщение, не удаляя его из очереди hello параметр необязательным параметром hello `isPeekLock` слишком**true**.</span><span class="sxs-lookup"><span data-stu-id="f1e33-154">By default, messages are deleted from hello queue as they are read; however, you can read (peek) and lock hello message without deleting it from hello queue by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="f1e33-155">Здравствуйте, поведение по умолчанию чтение и удаление приветственное сообщение, как часть hello операции получения hello самая простая модель и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="f1e33-155">hello default behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="f1e33-156">toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки.</span><span class="sxs-lookup"><span data-stu-id="f1e33-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="f1e33-157">Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="f1e33-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="f1e33-158">Если hello `isPeekLock` параметра установлено слишком**true**, получать hello становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="f1e33-158">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="f1e33-159">Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="f1e33-159">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="f1e33-160">После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова `deleteMessage` метод и предоставляя toobe сообщение hello удален в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="f1e33-160">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `deleteMessage` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="f1e33-161">Hello `deleteMessage` метод помечает приветственное сообщение как полученное и удаляет его из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="f1e33-161">hello `deleteMessage` method marks hello message as being consumed and removes it from hello queue.</span></span>

<span data-ttu-id="f1e33-162">Hello следующий пример демонстрирует способ tooreceive и процесс сообщений с помощью `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="f1e33-162">hello following example demonstrates how tooreceive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="f1e33-163">Hello пример получает и удаляет сообщение и получает сообщения с помощью `isPeekLock` значение слишком**true**, а затем удаляет hello сообщения с помощью `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="f1e33-163">hello example first receives and deletes a message, and then receives a message using `isPeekLock` set too**true**, then deletes hello message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="f1e33-164">Как происходит сбой toohandle приложения и может быть прочитан сообщений</span><span class="sxs-lookup"><span data-stu-id="f1e33-164">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="f1e33-165">Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="f1e33-165">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="f1e33-166">Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlockMessage` метод hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="f1e33-166">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="f1e33-167">Это будет вызвать toounlock Service Bus сообщения в очереди hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.</span><span class="sxs-lookup"><span data-stu-id="f1e33-167">This will cause Service Bus toounlock the message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="f1e33-168">Также существует время ожидания, связанные с сообщением, заблокировать в течение hello очереди, и при сбое приложения hello tooprocess hello сообщение перед hello срок блокировки (например, если приложение hello терпит сбой), то служебной шины будет автоматическую разблокировку приветственное сообщение и сделать ее доступной toobe получили еще раз.</span><span class="sxs-lookup"><span data-stu-id="f1e33-168">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="f1e33-169">В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `deleteMessage` вызывается метод, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="f1e33-169">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="f1e33-170">Это часто называется *по крайней мере после обработки*, то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться.</span><span class="sxs-lookup"><span data-stu-id="f1e33-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="f1e33-171">Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений.</span><span class="sxs-lookup"><span data-stu-id="f1e33-171">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="f1e33-172">Это можно сделать с помощью hello **MessageId** свойство сообщения hello, который остается постоянным протяжении всех попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="f1e33-172">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1e33-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f1e33-173">Next steps</span></span>
<span data-ttu-id="f1e33-174">toolearn Дополнительные сведения об очередях см. следующие ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="f1e33-174">toolearn more about queues, see hello following resources.</span></span>

* <span data-ttu-id="f1e33-175">[Очереди, разделы и подписки служебной шины][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="f1e33-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="f1e33-176">Репозиторий [пакетов Azure SDK для Node][Azure SDK for Node] на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="f1e33-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="f1e33-177">центре разработчиков Node.js</span><span class="sxs-lookup"><span data-stu-id="f1e33-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
