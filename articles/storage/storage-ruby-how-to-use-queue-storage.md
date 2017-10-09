---
title: "aaaHow toouse хранилища очередей из Ruby | Документы Microsoft"
description: "Узнайте, как toocreate службы очередей Azure hello toouse и очереди delete и insert, получение и удаление сообщений. Примеры кода написаны на Ruby."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a>Как toouse хранилища очередей из Ruby
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Обзор
В этом руководстве показано, как tooperform распространенных сценариев использования hello службы хранилища очередей Microsoft Azure. образцы Hello записываются с помощью API-интерфейса Azure Ruby hello.
Hello сценарии включают **Вставка**, **Просмотр**, **начало**, и **удаление** очередь сообщений, а также  **Создание и удаление очередей**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Создание приложения Ruby
Создайте приложение Ruby. Инструкции см. в разделе [Веб-приложение Ruby on Rails на виртуальной машине Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Настройка приложения tooAccess хранилища
toouse хранилища Azure, понадобится toodownload и используйте hello Ruby azure пакет, который включает в себя набор библиотек удобства, взаимодействующих со службами REST hello хранилища.

### <a name="use-rubygems-tooobtain-hello-package"></a>Используйте RubyGems tooobtain hello пакет
1. Используйте интерфейс командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix).
2. Введите команду «gem Установка azure» в hello команда окна tooinstall hello gem и зависимости.

### <a name="import-hello-package"></a>Импорт пакета hello
Используйте текстовый редактор, добавить следующие toohello вверху hello Ruby файл, куда будет toouse хранилища hello:

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a>Настройка подключения к службе хранилища Azure
модуль Hello azure будет считывать переменные среды hello **AZURE\_ХРАНЕНИЯ\_учетной записи** и **AZURE\_ХРАНЕНИЯ\_ключ_доступа** для сведения, необходимые учетной записи хранилища Azure tooyour tooconnect. Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello перед использованием **Azure::QueueService** с hello, следующий код:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

tooobtain эти значения из классические или диспетчер ресурсов хранилища учетной записи в hello портала Azure:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Перейдите toohello необходимом toouse учетной записи хранилища.
3. В колонке параметров hello на hello вправо, щелкните **клавиши доступа**.
4. В колонке ключи hello доступа, отображается вы увидите ключ доступа hello 1 и ключ доступа 2. Можно использовать любой из них. 
5. Щелкните hello скопировать значок toocopy hello ключа toohello буфер обмена. 

Эти значения из классической хранилища учетной записи в классический портал Azure hello tooobtain:

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. Перейдите toohello необходимом toouse учетной записи хранилища.
3. Нажмите кнопку **УПРАВЛЕНИЕ КЛЮЧАМИ доступа** hello нижней части панели навигации hello.
4. В hello всплывающее диалоговое окно вы увидите имя учетной записи хранения hello, первичный ключ доступа и вторичный ключ доступа. Клавиша доступа можно использовать hello первичной или вторичной hello. 
5. Щелкните hello скопировать значок toocopy hello ключа toohello буфер обмена.

## <a name="how-to-create-a-queue"></a>Практическое руководство. Создание очереди
Hello следующий код создает **Azure::QueueService** объекта, который позволяет toowork с очередями.

```ruby
azure_queue_service = Azure::QueueService.new
```

Используйте hello **create_queue()** toocreate метод очередь с hello заданное имя.

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Практическое руководство. Вставка сообщения в очередь
tooinsert сообщения в очереди, используйте hello **create_message()** toocreate метод новое сообщение и добавьте его toohello очереди.

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a>Практическое руководство: Просмотр следующего сообщения hello
Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **peek\_messages()** метод. По умолчанию метод **peek\_messages()** просматривает одно сообщение. Можно также указать, сколько сообщений требуется toopeek.

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a>Практическое руководство: Следующее сообщение hello вывода из очереди
Вы можете удалить сообщение из очереди в два этапа.

1. При вызове **списка\_messages()**, получить следующее сообщение hello в очередь по умолчанию. Можно также указать, сколько сообщений требуется tooget. Здравствуйте, сообщения, возвращаемые из **списка\_messages()** становится невидимой tooany другой код, чтение сообщений из этой очереди. Передать hello видимость тайм-аута в секундах в виде параметра.
2. toofinish удаление приветственное сообщение из очереди hello, необходимо также вызвать **delete_message()**.

Это двухэтапный процесс удаления сообщения гарантирует, что при tooprocess завершается с ошибкой вашего кода, получит сообщение из-за toohardware или ошибок программного обеспечения, другой экземпляр кода hello же сообщение и повторите. Вызовы кода **удаление\_message()** сразу после обработки сообщения hello.

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Практическое руководство: Изменение содержимого hello сообщения в очереди
Вы можете изменить содержимое сообщений на месте в очереди hello hello. Приведенный ниже код Hello использует hello **update_message()** tooupdate метод сообщение. метод Hello возвращает кортеж, содержащий hello подтверждение сообщения в очереди hello и UTC значения даты-времени, представляющая hello сообщение будет видимо в очереди hello.

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Практическое руководство. Использование дополнительных параметров для удаления сообщений из очереди
Способ извлечения сообщения из очереди можно настроить двумя способами.

1. Можно получить пакет сообщения.
2. Можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения.

Hello следующий пример кода использует hello **списка\_messages()** метод tooget 15 сообщений в одном вызове. Затем код выводит и удаляет все сообщения. Он также устанавливает минут toofive hello невидимости время ожидания для каждого сообщения.

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a>Практическое руководство: Получение hello длина очереди
Можно получить оценки hello количество сообщений в очереди hello. Hello **получить\_очереди\_metadata()** метод запрашивает hello очереди службы tooreturn hello приблизительное количество сообщений и метаданные о hello очереди.

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a>Практическое руководство. Удаление очереди
toodelete все сообщения hello и очереди содержащиеся в нем, вызов hello **удаление\_queue()** метод hello объекта очереди.

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища очередей, выполните эти ссылки toolearn о более сложных задач хранилища.

* Посетите hello [блог группы разработчиков хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Посетите hello [пакет Azure SDK для Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) репозитория в GitHub

Сравнение между hello службы очередей Azure, рассматриваемые в данной статье, рассматриваемые в hello очереди шины обслуживания Azure [как toouse очереди Service Bus](/develop/ruby/how-to-guides/service-bus-queues/) статьи см. в разделе [очереди Azure и очереди шины обслуживания — сравнение и Отличия](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)
