---
title: "aaaHow toouse хранилища очередей из Python | Документы Microsoft"
description: "Узнайте, как toouse hello службы очередей Azure из Python toocreate и удалять очереди и вставки, получения и удаления сообщения."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: f4f902a2c314401e5c1768fbc80566c8ba25c058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a>Как toouse хранилища очередей из Python
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Обзор
В этом руководстве показано, как с помощью распространенных сценариев tooperform hello службы хранилища очередей Azure. Hello примеры написаны на Python и использовать hello [пакет SDK хранилища Microsoft Azure для Python]. Hello сценарии включают **Вставка**, **Просмотр**, **начало**, и **удаление** очередь сообщений, а также  **Создание и удаление очередей**. Дополнительные сведения об очередях см. в разделе toohello [дальнейшие действия].

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a>Практическое руководство. Создание очереди
Hello **QueueService** объектов позволяет работать с очередями. Hello следующий код создает **QueueService** объекта. Добавьте следующее hello верхней hello любого файла Python, в котором вы хотите tooprogrammatically доступа хранилища Azure:

```python
from azure.storage.queue import QueueService
```

Hello следующий код создает **QueueService** объекта с помощью hello ключ учетной записи хранения имени и учетной записи. Замените myaccount и mykey фактическими значениями имени и ключа учетной записи.

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Практическое руководство. Вставка сообщения в очередь
tooinsert сообщения в очереди, используйте hello **поместить\_сообщение** метод для создания нового сообщения и добавьте его toohello очереди.

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a>Практическое руководство: Просмотр следующего сообщения hello
Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **peek\_сообщений** метод. По умолчанию метод **peek\_messages** просматривает одно сообщение.

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a>Практическое руководство. Удаление следующего сообщения из очереди
Ваш код удаляет сообщение из очереди в два этапа. При вызове **получить\_сообщения**, получить следующее сообщение hello в очередь по умолчанию. Сообщение, возвращенное из **получить\_сообщений** становится невидимой tooany другой код, чтение сообщений из этой очереди. По умолчанию это сообщение остается невидимым в течение 30 секунд. toofinish удаление приветственное сообщение из очереди hello, необходимо также вызвать **удаление\_сообщение**. Это двухэтапный процесс удаления сообщения гарантирует, что код в случае сбоя tooprocess сообщение из-за сбоя оборудования или программного обеспечения другой экземпляр кода можно получить то же сообщение и повторите попытку. Вызовы кода **удаление\_сообщение** сразу после обработки сообщения hello.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

Способ извлечения сообщения из очереди можно настроить двумя способами.
Во-первых можно получить пакет сообщений (вверх too32). Во-вторых можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения. Hello следующий пример кода использует **получить\_сообщений** метод tooget 16 сообщений в одном вызове. Затем он обрабатывает каждое сообщение с помощью цикла for. Он также устанавливает время ожидания невидимости hello до пяти минут для каждого сообщения.

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Практическое руководство: Изменение содержимого hello сообщения в очереди
Вы можете изменить содержимое сообщений на месте в очереди hello hello. Если сообщение представляет рабочей задачи, можно использовать этот компонент tooupdate состояние hello рабочих задач. Приведенный ниже код Hello использует hello **обновление\_сообщение** метод tooupdate сообщение. время ожидания видимости Hello задается too0, то есть сообщение немедленно и обновление содержимого hello.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a>Практическое руководство: Получение hello длина очереди
Можно получить оценку hello количество сообщений в очереди. **Получить\_очереди\_метаданные** метод запрашивает hello очереди службы tooreturn метаданные очереди hello и hello **approximate_message_count**. результат Hello только является приблизительным, так как сообщения можно добавить или удалить после запроса tooyour ответ службы очереди.

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a>Практическое руководство. Удаление очереди
toodelete все сообщения hello и очереди содержащиеся в нем, вызовите метод **удаление\_очереди** метод.

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища очередей, выполните следующие дополнительные toolearn ссылки.

* [Центр по разработке для Python](/develop/python/)
* [API-интерфейс REST служб хранилища Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [Блог рабочей группы службы хранилища Azure]
* [пакет SDK хранилища Microsoft Azure для Python]

[Блог рабочей группы службы хранилища Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[пакет SDK хранилища Microsoft Azure для Python]: https://github.com/Azure/azure-storage-python