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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a>Как tooUse Service Bus разделов и подписок с Node.js

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

В этом руководстве описаны как toouse Service Bus разделов и подписок из приложений Node.js. Hello сценарии включают **создания разделов и подписок**, **создание фильтров подписок**, **отправки сообщений** разделе tooa **получения сообщения из подписки**, и **удаление разделов и подписок**. Дополнительные сведения о разделах и подписках см. в разделе hello [дальнейшие действия](#next-steps) раздела.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a>Создание приложения Node.js
Создайте пустое приложение Node.js. Инструкции по созданию приложений Node.js см. в разделе [создать и развернуть tooan приложений Node.js веб-сайта Azure], [Node.js облачной службы] [ Node.js Cloud Service] с помощью Windows PowerShell или веб-сайт в WebMatrix.

## <a name="configure-your-application-toouse-service-bus"></a>Настройка вашего приложения toouse Service Bus
toouse Service Bus, загрузите hello Node.js Azure пакета. Этот пакет содержит набор библиотек, взаимодействующих со службами Service Bus REST hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>С помощью диспетчера пакетов узла (NPM) tooobtain hello пакета
1. Использовать интерфейс командной строки, такие как **PowerShell** (Windows), **терминалов** (Mac), или **Bash** (Unix), перейдите в папку toohello, где создан пример приложения.
2. Тип **npm Установка azure** в командном окне приветствия, что должно привести к hello следующие выходные данные:

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
3. Вы можете вручную запустить hello **ls** tooverify команды, **узел\_модули** папка была создана. В этой папке можно найти **azure** пакет, который содержит hello библиотеки tooaccess разделы служебной шины.

### <a name="import-hello-module"></a>Импорт модуля hello
С помощью блокнота или другого текстового редактора, добавьте следующие toohello вверху hello hello **server.js** файл приложения hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a>Настройка подключения к Service Bus
Hello Azure модуль считывает переменные среды hello `AZURE_SERVICEBUS_NAMESPACE` и `AZURE_SERVICEBUS_ACCESS_KEY` сведения необходимые tooconnect tooService шины. Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello при вызове `createServiceBusService`.

Пример настройки переменных среды hello для облачной службы Azure см. в разделе [Node.js облачной службы с хранилищем][Node.js Cloud Service with Storage].

Пример настройки hello переменных среды для веб-сайта Azure, в разделе [Node.js веб-приложение с хранилищем][Node.js Web Application with Storage].

## <a name="create-a-topic"></a>Создание раздела
Hello **ServiceBusService** позволяет toowork с разделами. Следующий код создает объект **ServiceBusService**. Добавьте его в верхней части hello **server.js** файла после tooimport hello azure hello инструкции модуля:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Путем вызова `createTopicIfNotExists` на hello **ServiceBusService** объекта hello указано, раздел возвращается (если он существует), или создается новый раздел с указанным именем hello. Hello следующий код использует `createTopicIfNotExists` toocreate или подключения с именем раздела toohello `MyTopic`:

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

Hello `createServiceBusService` метод также поддерживает дополнительные параметры, позволяющие toooverride параметры раздела по умолчанию срок жизни сообщения или максимальный размер раздела. Hello следующий пример задает hello максимальное число разделов размер too5GB со временем toolive 1 минута:

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

### <a name="filters"></a>Фильтры
Необязательный операции фильтрации может быть применен toooperations, выполняемые с помощью **ServiceBusService**. К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, которые реализуют метод с сигнатурой hello:

```javascript
function handle (requestOptions, next)
```

После выполнения предварительной обработки на параметры запроса hello, hello вызовов метода `next`, передача обратный вызов с hello следующие подписи:

```javascript
function (returnObject, finalCallback, next)
```

В этот обратный вызов и после обработки hello `returnObject` (hello ответа от сервера toohello hello запроса), обратного вызова hello необходимы tooeither вызова рядом, если он существует toocontinue обработки других фильтров или вызвать `finalCallback` в противном случае — tooend hello вызов службы.

Два фильтра, которые реализовать логику повторных попыток входят в состав hello Azure SDK для Node.js **ExponentialRetryPolicyFilter** и **LinearRetryPolicyFilter**. Hello следующий код создает **ServiceBusService** объект, который использует hello **ExponentialRetryPolicyFilter**:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a>Создание подписок
Подписок раздела также создаются с hello **ServiceBusService** объекта. Подписки представляют собой именованные и может иметь дополнительный фильтр, ограничивающий набор hello сообщения, доставленные toohello в виртуальную очередь подписки.

> [!NOTE]
> Подписки являются постоянными и продолжится до либо они tooexist или hello раздел они связаны, будут удалены. Если приложение содержит логику toocreate подписки, он сначала проверить Если hello подписка уже существует, с помощью `getSubscription` метод.
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Создайте подписку с фильтром (MatchAll) по умолчанию hello
Hello **MatchAll** фильтром является фильтр по умолчанию hello, который используется, если не указан фильтр при создании новой подписки. Здравствуйте, когда **MatchAll** используется фильтр, раздел опубликованного toohello все сообщения помещаются в виртуальную очередь подписки. Hello следующем примере создается подписка с именем «AllMessages» и по умолчанию hello использует **MatchAll** фильтра.

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a>Создание подписок с фильтрами
Можно также создать фильтры, позволяющие tooscope сообщений отправила разделе tooa должно отображаться в рамках подписки определенный раздел.

Hello самый гибкий тип фильтра, поддерживаемых подписок — **SqlFilter**, который реализует подмножество SQL92. Фильтры SQL работают с свойств сообщений hello, раздел опубликованного toohello hello. Дополнительные сведения о выражениях hello, которые могут использоваться с фильтром SQL просмотрите hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] синтаксиса.

Фильтры можно добавлять tooa подписки с помощью hello `createRule` метод hello **ServiceBusService** объекта. Этот метод позволяет добавить новую подписку tooan существующие фильтры.

> [!NOTE]
> Так как автоматически применяется фильтр по умолчанию hello tooall новых подписок, необходимо сначала удалить фильтр по умолчанию hello или **MatchAll** переопределит все фильтры, можно указать. Правило по умолчанию hello можно удалить с помощью hello `deleteRule` метод **ServiceBusService** объекта.
>
>

Hello следующий пример создает подписку с именем `HighMessages` с **SqlFilter** , выбирает только сообщения, которые содержат пользовательского `messagenumber` свойство больше 3:

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

Аналогичным образом hello следующий пример создает подписку с именем `LowMessages` с **SqlFilter** , выбирает только сообщения, которые содержат `messagenumber` свойства меньше или равно too3:

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

Если теперь отправляется сообщение слишком`MyTopic`, всегда будут предоставляться для приемников подписана toohello `AllMessages` подписки раздела и выборочно доставленный tooreceivers подписка toohello `HighMessages` и `LowMessages` подписок раздела (зависимости от содержимого сообщения hello).

## <a name="how-toosend-messages-tooa-topic"></a>Способ toosend сообщений tooa раздела
toosend раздела Service Bus tooa сообщения, приложение должно использовать `sendTopicMessage` метод hello **ServiceBusService** объекта.
Отправлять сообщения, разделы шины tooService **BrokeredMessage** объектов.
**BrokeredMessage** объекты имеют набор стандартных свойств (например, `Label` и `TimeToLive`), словаря, используемые toohold пользовательские свойства для конкретного приложения и текст строки данных. Приложение может установить текст hello приветственное сообщение, передав значение строки hello `sendTopicMessage` и любые необходимые стандартные свойства заполняются значениями по умолчанию.

Hello следующем примере показано, как toosend пять тестовых сообщений для `MyTopic`. Обратите внимание, что hello `messagenumber` зависит от значения свойства каждого сообщения hello итерацию цикла hello (Это определяет, какие подписки получают его):

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

Темы Service Bus поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md). Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ. Нет ограничений на hello количество сообщений, которые содержатся в разделе, но отсутствует ограничение на общий размер сообщений hello, удерживаемые раздела hello. Этот размер раздела определяется при создании с верхним пределом 5 ГБ.

## <a name="receive-messages-from-a-subscription"></a>Получение сообщений из подписки
Сообщения принимаются из подписки с помощью `receiveSubscriptionMessage` метод hello **ServiceBusService** объекта. По умолчанию сообщения удаляются из подписки hello, как они доступны для чтения; Однако можно считать (Просмотр) и заблокировать приветственное сообщение, не удаляя ее из подписки hello параметр необязательным параметром hello `isPeekLock` слишком**true**.

поведение по умолчанию Hello чтение и удаление приветственное сообщение, как часть операции receive — самая простая модель hello и работает лучше для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя. toounderstand это, рассмотрим сценарий, в котором hello проблемы потребителя получают запрос и затем ломается до его обработки. Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.

Если hello `isPeekLock` параметра установлено слишком**true**, получать hello становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения. Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения.
После приложения hello завершает обработку сообщения hello (или хранит его для будущей обработки), он завершается hello второй этап процесса получения путем вызова **deleteMessage** метод и предоставляя toobe сообщения удален в качестве параметра. Hello **deleteMessage** метод будет пометить приветственное сообщение как полученное и удалите его из подписки hello.

Hello следующем примере показано, как можно получать сообщения и обработанные с помощью `receiveSubscriptionMessage`. Hello примере впервые получает и удаляет сообщение из подписки «LowMessages» hello и затем получает сообщение из подписки «HighMessages» hello с помощью `isPeekLock` задать tootrue. Затем удаляет сообщение hello с помощью `deleteMessage`:

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Как происходит сбой toohandle приложения и может быть прочитан сообщений
Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения. Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlockMessage` метод **ServiceBusService** объекта. Это будет вызвать toounlock Service Bus сообщение в рамках подписки hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.

Также существует время ожидания, связанные с сообщением, заблокирован в подписке, и при сбое приложения hello tooprocess приветственное сообщение, прежде чем hello срок блокировки (например, если приложение hello терпит сбой), а затем Service Bus разблокирует сообщение hello автоматически и делает ее доступной toobe получили еще раз.

В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `deleteMessage` вызывается метод, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения. Это часто называется *по крайней мере после обработки*, то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений. Это можно сделать с помощью **MessageId** свойство сообщения hello, который остается постоянным протяжении всех попыток доставки.

## <a name="delete-topics-and-subscriptions"></a>Удаление разделов и подписок
Разделы и подписки являются постоянными, а должен быть явно удалены, либо через hello [портал Azure] [ Azure portal] или программными средствами.
Hello следующем примере показано, как toodelete hello раздел с именем `MyTopic`:

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

Удаление раздела приведет к удалению всех подписок, зарегистрированных в разделе hello. Подписки также можно удалять по отдельности. В следующем примере показано, как toodelete подписки именоваться `HighMessages` из hello `MyTopic` раздела:

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello разделов Service Bus, выполните следующие дополнительные toolearn ссылки.

* Дополнительные сведения см. в статье [Очереди, разделы и подписки служебной шины][Queues, topics, and subscriptions].
* Справочник API для [SqlFilter][SqlFilter].
* Посетите hello [Azure SDK для узла] [ Azure SDK for Node] репозитория в GitHub.

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[создать и развернуть tooan приложений Node.js веб-сайта Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
