---
title: "темы Service Bus toouse aaaHow (Ruby) | Документы Microsoft"
description: "Узнайте, как toouse Service Bus разделы и подписки в Azure. Примеры кода написаны для приложений Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a>Как toouse Service Bus разделов и подписок с Ruby
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

В этой статье описывается как toouse Service Bus разделов и подписок из приложений Ruby. Hello сценарии включают **создания разделов и подписок, создание фильтров подписку, отправляя сообщения** разделе tooa **получения сообщений из подписки**, и  **Удаление разделов и подписок**. Дополнительные сведения о разделах и подписках см. в разделе hello [дальнейшие действия](#next-steps) раздела.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a>Создание раздела
Hello **Azure::ServiceBusService** позволяет toowork с разделами. Hello следующий код создает **Azure::ServiceBusService** объекта. toocreate разделом, использовать hello `create_topic()` метод. Следующий пример Hello создает раздел или выводит hello ошибки, если таковые имеются.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

Можно также передать **Azure::ServiceBus::Topic** объекта с дополнительными параметрами, позволяющие toooverride исходные разделе параметры, такие как очереди toolive или максимальный размер сообщения времени. Hello в следующем примере параметр Максимальное очереди hello размером too5 ГБ и время toolive too1 минуту:

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a>Создание подписок
Подписок раздела также создаются с hello **Azure::ServiceBusService** объекта. Подписки представляют собой именованные и может иметь дополнительный фильтр, ограничивающий набор hello сообщения, доставленные toohello в виртуальную очередь подписки.

Подписки являются постоянными и продолжится до либо они tooexist или hello раздел они связаны, будут удалены. Если приложение содержит логику toocreate подписки, он должен сначала проверяет, существует ли hello подписка уже с помощью метода getSubscription hello.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Создайте подписку с фильтром (MatchAll) по умолчанию hello
Hello **MatchAll** фильтром является фильтр по умолчанию hello, который используется, если не указан фильтр при создании новой подписки. Здравствуйте, когда **MatchAll** используется фильтр, раздел опубликованного toohello все сообщения помещаются в виртуальную очередь подписки hello. Hello следующем примере создается подписка с именем «все сообщения» и использует hello по умолчанию **MatchAll** фильтра.

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a>Создание подписок с фильтрами
Также можно определить фильтры, позволяющие toospecify сообщений отправила разделе tooa должно отображаться в конкретной подписки.

Hello самый гибкий тип фильтра, поддерживаемых подписок — hello **Azure::ServiceBus::SqlFilter**, который реализует подмножество SQL92. Фильтры SQL работают с свойств сообщений hello, раздел опубликованного toohello hello. Дополнительные сведения о выражениях hello, которые могут использоваться с фильтром SQL просмотрите hello [SqlFilter](service-bus-messaging-sql-filter.md) синтаксиса.

Можно добавить фильтры tooa подписки с помощью hello `create_rule()` метод hello **Azure::ServiceBusService** объекта. Этот метод позволяет tooadd новые фильтры tooan существующую подписку.

Так как автоматически применяется фильтр по умолчанию hello tooall новых подписках, сначала необходимо удалить фильтр по умолчанию hello или hello **MatchAll** переопределит все фильтры, можно указать. Правило по умолчанию hello можно удалить с помощью hello `delete_rule()` метод hello **Azure::ServiceBusService** объекта.

Hello следующий пример создает подписку с именем «высокой сообщений» **Azure::ServiceBus::SqlFilter** , выбирает только сообщения, которые содержат пользовательского `message_number` свойство больше 3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Аналогичным образом hello следующий пример создает подписку с именем `low-messages` с **Azure::ServiceBus::SqlFilter** , выбирает только сообщения, которые содержат `message_number` свойства меньше или равно too3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Если теперь отправляется сообщение слишком`test-topic`, это всегда быть toohello доставленный tooreceivers подписка `all-messages` подписки раздела и выборочно доставленный tooreceivers подписка toohello `high-messages` и `low-messages` (подписки) раздела зависимости от содержимого сообщения hello).

## <a name="send-messages-tooa-topic"></a>Отправить tooa темы о сообщениях
toosend раздела Service Bus tooa сообщения, приложение должно использовать hello `send_topic_message()` метод hello **Azure::ServiceBusService** объекта. Сообщения отправляются разделы шины tooService являются экземплярами hello **Azure::ServiceBus::BrokeredMessage** объектов. **Azure::ServiceBus::BrokeredMessage** объекты имеют набор стандартных свойств (например, `label` и `time_to_live`), словаря, используемые toohold пользовательские свойства для конкретного приложения и текст строки данных. Приложение может установить текст hello приветственное сообщение, передав значение строки toohello `send_topic_message()` метод и все обязательные, стандартные свойства заполняются значениями по умолчанию.

Hello следующий пример демонстрирует способ тестирования toosend пяти сообщений слишком`test-topic`. Обратите внимание, что hello `message_number` изменяется значение настраиваемого свойства каждого сообщения hello итерацию цикла hello (этим определяется, какая подписка получит его):

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

Темы Service Bus поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md). Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ. Нет ограничений на hello количество сообщений, которые содержатся в разделе, но отсутствует ограничение на общий размер сообщений hello, удерживаемые раздела hello. Этот размер раздела определяется при создании с верхним пределом 5 ГБ.

## <a name="receive-messages-from-a-subscription"></a>Получение сообщений из подписки
Сообщения принимаются из подписки с помощью hello `receive_subscription_message()` метод hello **Azure::ServiceBusService** объекта. По умолчанию сообщения read(peak) и заблокирован, не удаляя ее из подписки hello. Можно читать и удалять приветственное сообщение из подписки hello, установка hello `peek_lock` параметр слишком**false**.

поведение по умолчанию Hello делает hello чтение и удаление двух шаговой операцией, который также вполне возможно toosupport приложений, которые не удается обработать отсутствующие сообщения. Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения. После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова `delete_subscription_message()` метод и предоставляя toobe сообщение hello удален в качестве параметра. Hello `delete_subscription_message()` метод будет пометить приветственное сообщение как полученное и удалите его из подписки hello.

Если hello `:peek_lock` параметра установлено слишком**false**, чтение и удаление приветственное сообщение становится hello самая простая модель и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello для события Произошла ошибка. toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки. Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.

Hello следующем примере показано, как можно получать сообщения и обработанные с помощью `receive_subscription_message()`. Hello пример сначала получает и удаляет сообщение из hello `low-messages` подписки с помощью `:peek_lock` значение слишком**false**, а затем получает сообщение от hello `high-messages` и затем удаляет hello сообщения с помощью `delete_subscription_message()`:

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Как происходит сбой toohandle приложения и может быть прочитан сообщений
Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения. Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlock_subscription_message()` метод hello **Azure::ServiceBusService** объекта. Это приводит hello toounlock Service Bus сообщение в рамках подписки hello и сделать ее доступной toobe получения, либо путем hello же потреблять приложение или другое приложение потребителя.

Также существует время ожидания, связанные с сообщением, заблокировать в течение hello подписки, и при сбое приложения hello tooprocess приветственное сообщение, прежде чем hello срок блокировки (например, если приложение hello терпит сбой), разблокируйте Service Bus приветственное сообщение автоматически и сделать ее доступной toobe получили еще раз.

В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `delete_subscription_message()` вызывается метод, то приветственное сообщение будет повторно доставлены toohello приложения после его перезапуска. Это часто называется *по крайней мере после обработки*; то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений. Эта логика часто достигается с помощью hello `message_id` свойство сообщения hello, который остается постоянным протяжении всех попыток доставки.

## <a name="delete-topics-and-subscriptions"></a>Удаление разделов и подписок
Разделы и подписки являются постоянными, а должен быть явно удалены, либо через hello [портал Azure] [ Azure portal] или программными средствами. Приведенный ниже пример Hello показывает, как toodelete hello раздел с именем `test-topic`.

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

При удалении раздела также удаляются все подписки, которые зарегистрированы в разделе hello. Подписки также можно удалять по отдельности. Hello следующем коде показано, как с именем подписки hello toodelete `high-messages` из hello `test-topic` раздела:

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello разделов Service Bus, выполните следующие дополнительные toolearn ссылки.

* См. статью [Очереди, разделы и подписки](service-bus-queues-topics-subscriptions.md).
* Справочник API для [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).
* Посетите hello [пакет Azure SDK для Ruby](https://github.com/Azure/azure-sdk-for-ruby) репозитория в GitHub.

[Azure portal]: https://portal.azure.com
