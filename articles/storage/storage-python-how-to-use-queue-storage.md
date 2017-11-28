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
ms.openlocfilehash: ce8d999d9fafaef0dab48442560d004c034c0804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a><span data-ttu-id="f5625-103">Как toouse хранилища очередей из Python</span><span class="sxs-lookup"><span data-stu-id="f5625-103">How toouse Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="f5625-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f5625-104">Overview</span></span>
<span data-ttu-id="f5625-105">В этом руководстве показано, как с помощью распространенных сценариев tooperform hello службы хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="f5625-105">This guide shows you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="f5625-106">Hello примеры написаны на Python и использовать hello [пакет SDK хранилища Microsoft Azure для Python].</span><span class="sxs-lookup"><span data-stu-id="f5625-106">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="f5625-107">Hello сценарии включают **Вставка**, **Просмотр**, **начало**, и **удаление** очередь сообщений, а также  **Создание и удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="f5625-107">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="f5625-108">Дополнительные сведения об очередях см. в разделе toohello [дальнейшие действия].</span><span class="sxs-lookup"><span data-stu-id="f5625-108">For more information on queues, refer toohello [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="f5625-109">Практическое руководство. Создание очереди</span><span class="sxs-lookup"><span data-stu-id="f5625-109">How To: Create a Queue</span></span>
<span data-ttu-id="f5625-110">Hello **QueueService** объектов позволяет работать с очередями.</span><span class="sxs-lookup"><span data-stu-id="f5625-110">hello **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="f5625-111">Hello следующий код создает **QueueService** объекта.</span><span class="sxs-lookup"><span data-stu-id="f5625-111">hello following code creates a **QueueService** object.</span></span> <span data-ttu-id="f5625-112">Добавьте следующее hello верхней hello любого файла Python, в котором вы хотите tooprogrammatically доступа хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="f5625-112">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="f5625-113">Hello следующий код создает **QueueService** объекта с помощью hello ключ учетной записи хранения имени и учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f5625-113">hello following code creates a **QueueService** object using hello storage account name and account key.</span></span> <span data-ttu-id="f5625-114">Замените myaccount и mykey фактическими значениями имени и ключа учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f5625-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="f5625-115">Практическое руководство. Вставка сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="f5625-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="f5625-116">tooinsert сообщения в очереди, используйте hello **поместить\_сообщение** метод для создания нового сообщения и добавьте его toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="f5625-116">tooinsert a message into a queue, use hello **put\_message** method to create a new message and add it toohello queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="f5625-117">Практическое руководство: Просмотр следующего сообщения hello</span><span class="sxs-lookup"><span data-stu-id="f5625-117">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="f5625-118">Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **peek\_сообщений** метод.</span><span class="sxs-lookup"><span data-stu-id="f5625-118">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages** method.</span></span> <span data-ttu-id="f5625-119">По умолчанию метод **peek\_messages** просматривает одно сообщение.</span><span class="sxs-lookup"><span data-stu-id="f5625-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="f5625-120">Практическое руководство. Удаление следующего сообщения из очереди</span><span class="sxs-lookup"><span data-stu-id="f5625-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="f5625-121">Ваш код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="f5625-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="f5625-122">При вызове **получить\_сообщения**, получить следующее сообщение hello в очередь по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f5625-122">When you call **get\_messages**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="f5625-123">Сообщение, возвращенное из **получить\_сообщений** становится невидимой tooany другой код, чтение сообщений из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="f5625-123">A message returned from **get\_messages** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="f5625-124">По умолчанию это сообщение остается невидимым в течение 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="f5625-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="f5625-125">toofinish удаление приветственное сообщение из очереди hello, необходимо также вызвать **удаление\_сообщение**.</span><span class="sxs-lookup"><span data-stu-id="f5625-125">toofinish removing hello message from hello queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="f5625-126">Это двухэтапный процесс удаления сообщения гарантирует, что код в случае сбоя tooprocess сообщение из-за сбоя оборудования или программного обеспечения другой экземпляр кода можно получить то же сообщение и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="f5625-126">This two-step process of removing a message assures that when your code fails tooprocess a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="f5625-127">Вызовы кода **удаление\_сообщение** сразу после обработки сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="f5625-127">Your code calls **delete\_message** right after hello message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="f5625-128">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="f5625-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="f5625-129">Во-первых можно получить пакет сообщений (вверх too32).</span><span class="sxs-lookup"><span data-stu-id="f5625-129">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="f5625-130">Во-вторых можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="f5625-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="f5625-131">Hello следующий пример кода использует **получить\_сообщений** метод tooget 16 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="f5625-131">hello following code example uses the **get\_messages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="f5625-132">Затем он обрабатывает каждое сообщение с помощью цикла for.</span><span class="sxs-lookup"><span data-stu-id="f5625-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="f5625-133">Он также устанавливает время ожидания невидимости hello до пяти минут для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="f5625-133">It also sets hello invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="f5625-134">Практическое руководство: Изменение содержимого hello сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="f5625-134">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="f5625-135">Вы можете изменить содержимое сообщений на месте в очереди hello hello.</span><span class="sxs-lookup"><span data-stu-id="f5625-135">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="f5625-136">Если сообщение представляет рабочей задачи, можно использовать этот компонент tooupdate состояние hello рабочих задач.</span><span class="sxs-lookup"><span data-stu-id="f5625-136">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="f5625-137">Приведенный ниже код Hello использует hello **обновление\_сообщение** метод tooupdate сообщение.</span><span class="sxs-lookup"><span data-stu-id="f5625-137">hello code below uses hello **update\_message** method tooupdate a message.</span></span> <span data-ttu-id="f5625-138">время ожидания видимости Hello задается too0, то есть сообщение немедленно и обновление содержимого hello.</span><span class="sxs-lookup"><span data-stu-id="f5625-138">hello visibility timeout is set too0, meaning the message appears immediately and hello content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="f5625-139">Практическое руководство: Получение hello длина очереди</span><span class="sxs-lookup"><span data-stu-id="f5625-139">How To: Get hello Queue Length</span></span>
<span data-ttu-id="f5625-140">Можно получить оценку hello количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="f5625-140">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="f5625-141">**Получить\_очереди\_метаданные** метод запрашивает hello очереди службы tooreturn метаданные очереди hello и hello **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="f5625-141">The **get\_queue\_metadata** method asks hello queue service tooreturn metadata about hello queue, and hello **approximate_message_count**.</span></span> <span data-ttu-id="f5625-142">результат Hello только является приблизительным, так как сообщения можно добавить или удалить после запроса tooyour ответ службы очереди.</span><span class="sxs-lookup"><span data-stu-id="f5625-142">hello result is only approximate because messages can be added or removed after the queue service responds tooyour request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="f5625-143">Практическое руководство. Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="f5625-143">How To: Delete a Queue</span></span>
<span data-ttu-id="f5625-144">toodelete все сообщения hello и очереди содержащиеся в нем, вызовите метод **удаление\_очереди** метод.</span><span class="sxs-lookup"><span data-stu-id="f5625-144">toodelete a queue and all hello messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="f5625-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5625-145">Next Steps</span></span>
<span data-ttu-id="f5625-146">Теперь, когда вы узнали основы hello хранилища очередей, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="f5625-146">Now that you've learned hello basics of Queue storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="f5625-147">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="f5625-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="f5625-148">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="f5625-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="f5625-149">[Блог рабочей группы службы хранилища Azure]</span><span class="sxs-lookup"><span data-stu-id="f5625-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="f5625-150">[пакет SDK хранилища Microsoft Azure для Python]</span><span class="sxs-lookup"><span data-stu-id="f5625-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Блог рабочей группы службы хранилища Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[пакет SDK хранилища Microsoft Azure для Python]: https://github.com/Azure/azure-storage-python