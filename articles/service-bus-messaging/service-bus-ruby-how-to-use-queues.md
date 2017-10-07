---
title: "Помещает в очередь aaaHow toouse Azure Service Bus с Ruby | Документы Microsoft"
description: "Узнайте, как очереди toouse Service Bus в Azure. Примеры кода написаны на Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a>Как очереди toouse Service Bus с Ruby

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

В этом руководстве описаны как toouse очереди Service Bus. Hello примеры на языке Ruby и использовать hello Azure gem. Hello сценарии включают **создание очередей, отправки и получения сообщений**, и **удаление очередей**. Дополнительные сведения об очередях Service Bus см. в разделе hello [дальнейшие действия](#next-steps) раздела.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a>Как toocreate очереди
Hello **Azure::ServiceBusService** позволяет toowork с очередями. toocreate очереди, используйте hello `create_queue()` метод. Hello следующий пример создает очередь или выводит все ошибки.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

Можно также передать **Azure::ServiceBus::Queue** объекта с дополнительными параметрами, что позволяет toooverride hello параметров по умолчанию очереди, такие как очереди toolive или максимальный размер сообщения времени. Hello в следующем примере показано, как tooset hello ГБ too5 максимальный размер и время toolive too1 минуту:

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a>Способ toosend сообщений очереди tooa
toosend очередью сообщений tooa Service Bus, приложение вызывает hello `send_queue_message()` метод hello **Azure::ServiceBusService** объекта. Сообщений, отправленных слишком (и, полученных от) служебной шины, очереди являются **Azure::ServiceBus::BrokeredMessage** объектов и иметь набор стандартных свойств (например, `label` и `time_to_live`), словарь, который будет использоваться toohold пользовательские свойства для конкретного приложения и текст из произвольных данных приложения. Приложения можно задать текст hello приветственное сообщение, передав значение строки в качестве приветственное сообщение и все стандартные свойства заполняются значениями по умолчанию.

Hello следующем примере показано, как toosend toohello очереди сообщений теста именоваться `test-queue` с помощью `send_queue_message()`:

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

Очереди шины обслуживания поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md). Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ. Нет ограничений на число hello сообщения помещаются в очередь, но отсутствует ограничение на общий размер сообщений hello, хранящиеся в очереди hello. Этот размер очереди, определяемый в момент ее создания, не должен превышать 5 ГБ.

## <a name="how-tooreceive-messages-from-a-queue"></a>Как tooreceive сообщений из очереди
Сообщения принимаются из очереди с помощью hello `receive_queue_message()` метод hello **Azure::ServiceBusService** объекта. По умолчанию сообщения чтения и блокировки не удаляется из очереди hello. Тем не менее, можно удалять сообщения из очереди hello мере их считывания параметр hello `:peek_lock` параметр слишком**false**.

поведение по умолчанию Hello делает hello чтение и удаление двух шаговой операцией, который также вполне возможно toosupport приложений, которые не удается обработать отсутствующие сообщения. Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения. После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова `delete_queue_message()` метод и предоставляя toobe сообщение hello удален в качестве параметра. Hello `delete_queue_message()` метод будет пометить приветственное сообщение как полученное и удалите его из очереди hello.

Если hello `:peek_lock` параметра установлено слишком**false**, чтение и удаление приветственное сообщение становится hello самая простая модель и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello для события Произошла ошибка. toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки. Поскольку Service Bus пометил приветственное сообщение как полученное, когда приложение hello перезапускается и начинает получать сообщения снова, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.

Hello следующий пример демонстрирует способ tooreceive и процесс сообщений с помощью `receive_queue_message()`. пример Hello сначала получает и удаляет сообщение с помощью `:peek_lock` значение слишком**false**, он получает сообщение и затем удаляет hello сообщения с помощью `delete_queue_message()`:

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Как происходит сбой toohandle приложения и может быть прочитан сообщений
Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения. Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlock_queue_message()` метод hello **Azure::ServiceBusService** объекта. Этот вызов причины hello toounlock Service Bus сообщений в очереди hello и сделать ее доступной toobe получения, либо путем hello же потреблять приложение или другое приложение потребителя.

Также существует время ожидания, связанные с сообщением, заблокировать в течение hello очереди, и при сбое приложения hello tooprocess приветственное сообщение, прежде чем hello срок блокировки (например, если приложение hello терпит сбой), а затем Service Bus разблокирует сообщение hello автоматически и делает ее доступной toobe получили еще раз.

В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `delete_queue_message()` вызывается метод, то приветственное сообщение будет повторно доставлены toohello приложения после его перезапуска. Этот процесс часто называют *по крайней мере после обработки*; то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений. Это можно сделать с помощью hello `message_id` свойства сообщения hello, остается постоянным на протяжении всех попыток доставки.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello очередей Service Bus, выполните следующие дополнительные toolearn ссылки.

* Обзор [очередей, разделов и подписок](service-bus-queues-topics-subscriptions.md).
* Посетите hello [пакет Azure SDK для Ruby](https://github.com/Azure/azure-sdk-for-ruby) репозитория в GitHub.

Сравнение между очередями Azure Service Bus hello, описанные в этой статье и очереди Azure, рассматриваемые в hello [как toouse хранилища очередей из Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) статьи см. в разделе [очереди Azure и очереди шины обслуживания Azure — сравнение Анализ производительности и масштабируемости](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

