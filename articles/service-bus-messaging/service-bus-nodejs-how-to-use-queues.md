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
# <a name="how-toouse-service-bus-queues-with-nodejs"></a>Как очереди toouse Service Bus с Node.js

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

В этой статье описывается, как очереди toouse Service Bus с и Node.js. Hello примеры на языке JavaScript и использовать hello модуля Azure для Node.js. Hello сценарии включают **создание очередей**, **отправки и получения сообщений**, и **удаление очередей**. Дополнительные сведения об очередях см. в разделе hello [дальнейшие действия](#next-steps) раздела.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a>Создание приложения Node.js
Создайте пустое приложение Node.js. Инструкции по toocreate приложении Node.js. в разделе [создать и развернуть tooan приложений Node.js веб-сайта Azure][Create and deploy a Node.js application tooan Azure Website], или [Node.js облачной службы] [ Node.js Cloud Service] с помощью Windows PowerShell.

## <a name="configure-your-application-toouse-service-bus"></a>Настройка вашего приложения toouse Service Bus
toouse Azure Service Bus, загрузите и используйте hello Node.js Azure пакета. Этот пакет содержит набор библиотек, взаимодействующих со службами Service Bus REST hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>С помощью диспетчера пакетов узла (NPM) tooobtain hello пакета
1. Используйте hello **Windows PowerShell для Node.js** toohello toonavigate окно команд **c:\\узел\\sbqueues\\WebRole1** папку, в которой создан вашей Образец приложения.
2. Тип **npm Установка azure** в командном окне hello, что следует привести к аналогичные toohello следующие выходные данные:

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
3. Вы можете вручную запустить hello **ls** tooverify команды, **node_modules** папка была создана. Внутри этой папки поиска hello **azure** пакет, который содержит hello библиотеки tooaccess очереди Service Bus.

### <a name="import-hello-module"></a>Импорт модуля hello
С помощью блокнота или другого текстового редактора, добавьте следующие toohello вверху hello hello **server.js** файл приложения hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a>Настройка подключения к служебной шине Azure
Hello Azure модуль считывает переменной среды hello `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain сведения, необходимые tooconnect tooService шины. Если эта переменная среды не задано, необходимо указать сведения об учетной записи hello при вызове `createServiceBusService`.

Пример настройки переменных среды hello в файле конфигурации для облачной службы Azure см. в разделе [Node.js облачной службы с хранилищем][Node.js Cloud Service with Storage].

Пример настройки переменных среды hello в hello [портал Azure] [ Azure portal] на веб-сайт Azure в разделе [Node.js веб-приложение с хранилищем] [ Node.js Web Application with Storage].

## <a name="create-a-queue"></a>Создание очереди
Hello **ServiceBusService** позволяет toowork с очередями Service Bus. Hello следующий код создает **ServiceBusService** объекта. Добавьте его вверху hello hello **server.js** файла после hello инструкции tooimport hello модуль Azure:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Путем вызова `createQueueIfNotExists` на hello **ServiceBusService** объекта hello указано очереди возвращается (если он существует), или создать новую очередь с указанным именем hello. Hello следующий код использует `createQueueIfNotExists` toocreate или подключите toohello очередь с именем `myqueue`:

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

Hello `createServiceBusService` метод также поддерживает дополнительные параметры, позволяющие toooverride исходные очереди параметры, такие как очереди toolive или максимальный размер сообщения времени. Hello следующий пример устанавливает hello максимальный размер too5 ГБ и значение времени toolive (TTL) — 1 минута.

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

### <a name="filters"></a>Фильтры
Необязательный операции фильтрации может быть применен toooperations, выполняемые с помощью **ServiceBusService**. К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, которые реализуют метод с сигнатурой hello:

```javascript
function handle (requestOptions, next)
```

После выполнения предварительной обработки на hello параметры запроса, необходимо вызвать метод hello `next`, передача обратный вызов с hello следующие подписи:

```javascript
function (returnObject, finalCallback, next)
```

В этот обратный вызов и после обработки hello `returnObject` (hello ответа от сервера toohello hello запроса), hello обратного вызова должен либо вызвать `next` если он существует toocontinue обработки других фильтров, или просто вызвав `finalCallback`, которая заканчивается вызов службы Hello.

Два фильтра, которые реализовать логику повторных попыток входят в состав hello Azure SDK для Node.js `ExponentialRetryPolicyFilter` и `LinearRetryPolicyFilter`. Hello следующий код создает `ServiceBusService` объект, который использует hello `ExponentialRetryPolicyFilter`:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a>Отправка сообщений в очереди tooa
toosend очередью сообщений tooa Service Bus, приложение вызывает hello `sendQueueMessage` метод hello **ServiceBusService** объекта. Сообщений, отправленных слишком (и, полученных от) служебной шины, очереди являются **BrokeredMessage** объектов и иметь набор стандартных свойств (такие как **метка** и **TimeToLive**), словарь, который используется toohold пользовательские свойства для конкретного приложения, и тело произвольных данных приложения. Приложение может установить текст hello приветственное сообщение, передав строку как сообщение hello. Все необходимые стандартные свойства будут заполнены значениями по умолчанию.

Hello следующем примере показано, как toosend toohello очереди сообщений теста именоваться `myqueue` с помощью `sendQueueMessage`:

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

Очереди шины обслуживания поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md). Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ. Нет ограничений на число hello сообщения помещаются в очередь, но отсутствует ограничение на общий размер сообщений hello, хранящиеся в очереди hello. Этот размер очереди, определяемый в момент ее создания, не должен превышать 5 ГБ. Дополнительные сведения о квотах см. в статье [Квоты на служебную шину][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Получение сообщений из очереди
Сообщения принимаются из очереди с помощью hello `receiveQueueMessage` метод hello **ServiceBusService** объекта. По умолчанию сообщения удаляются из очереди hello, как они доступны для чтения; Однако можно считать (Просмотр) и заблокировать приветственное сообщение, не удаляя его из очереди hello параметр необязательным параметром hello `isPeekLock` слишком**true**.

Здравствуйте, поведение по умолчанию чтение и удаление приветственное сообщение, как часть hello операции получения hello самая простая модель и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя. toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки. Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.

Если hello `isPeekLock` параметра установлено слишком**true**, получать hello становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения. Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения. После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова `deleteMessage` метод и предоставляя toobe сообщение hello удален в качестве параметра. Hello `deleteMessage` метод помечает приветственное сообщение как полученное и удаляет его из очереди hello.

Hello следующий пример демонстрирует способ tooreceive и процесс сообщений с помощью `receiveQueueMessage`. Hello пример получает и удаляет сообщение и получает сообщения с помощью `isPeekLock` значение слишком**true**, а затем удаляет hello сообщения с помощью `deleteMessage`:

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Как происходит сбой toohandle приложения и может быть прочитан сообщений
Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения. Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlockMessage` метод hello **ServiceBusService** объекта. Это будет вызвать toounlock Service Bus сообщения в очереди hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.

Также существует время ожидания, связанные с сообщением, заблокировать в течение hello очереди, и при сбое приложения hello tooprocess hello сообщение перед hello срок блокировки (например, если приложение hello терпит сбой), то служебной шины будет автоматическую разблокировку приветственное сообщение и сделать ее доступной toobe получили еще раз.

В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `deleteMessage` вызывается метод, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения. Это часто называется *по крайней мере после обработки*, то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений. Это можно сделать с помощью hello **MessageId** свойство сообщения hello, который остается постоянным протяжении всех попыток доставки.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения об очередях см. следующие ресурсы hello.

* [Очереди, разделы и подписки служебной шины][Queues, topics, and subscriptions]
* Репозиторий [пакетов Azure SDK для Node][Azure SDK for Node] на сайте GitHub
* [центре разработчиков Node.js](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
