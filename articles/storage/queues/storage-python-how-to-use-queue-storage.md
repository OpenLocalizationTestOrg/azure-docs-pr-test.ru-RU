---
title: "Как использовать хранилище очередей из Python | Документация Майкрософт"
description: "Узнайте о том, как использовать службу очередей Azure из Python для создания и удаления очередей, а также для вставки, получения и удаления сообщений."
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
ms.openlocfilehash: 963c11acb7939993568a774cd281145a8059b5a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-python"></a><span data-ttu-id="306a1-103">Использование хранилища очередей из Python</span><span class="sxs-lookup"><span data-stu-id="306a1-103">How to use Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="306a1-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="306a1-104">Overview</span></span>
<span data-ttu-id="306a1-105">В этом руководстве показано, как реализовать типичные сценарии с использованием службы хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="306a1-105">This guide shows you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="306a1-106">Примеры написаны на Python, и в них используется [пакет SDK для службы хранилища Microsoft Azure для Python].</span><span class="sxs-lookup"><span data-stu-id="306a1-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="306a1-107">Здесь описаны такие сценарии, как **вставка**, **просмотр**, **получение** и **удаление** сообщений очереди, а также **создание и удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="306a1-107">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="306a1-108">Дополнительные сведения об очередях см. в разделе [Дальнейшие действия].</span><span class="sxs-lookup"><span data-stu-id="306a1-108">For more information on queues, refer to the [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="306a1-109">Практическое руководство. Создание очереди</span><span class="sxs-lookup"><span data-stu-id="306a1-109">How To: Create a Queue</span></span>
<span data-ttu-id="306a1-110">Объект **QueueService** позволяет работать с очередями.</span><span class="sxs-lookup"><span data-stu-id="306a1-110">The **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="306a1-111">Следующий код создает объект **QueueService** .</span><span class="sxs-lookup"><span data-stu-id="306a1-111">The following code creates a **QueueService** object.</span></span> <span data-ttu-id="306a1-112">Добавьте следующий код в начало любого файла Python, из которого планируется получать доступ к хранилищу Azure программным способом:</span><span class="sxs-lookup"><span data-stu-id="306a1-112">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="306a1-113">Следующий код создает объект **QueueService** , используя имя и ключ доступа учетной записи.</span><span class="sxs-lookup"><span data-stu-id="306a1-113">The following code creates a **QueueService** object using the storage account name and account key.</span></span> <span data-ttu-id="306a1-114">Замените myaccount и mykey фактическими значениями имени и ключа учетной записи.</span><span class="sxs-lookup"><span data-stu-id="306a1-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="306a1-115">Практическое руководство. Вставка сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="306a1-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="306a1-116">Чтобы вставить сообщение в очередь, используйте метод **put\_message** для создания нового сообщения и добавления его в очередь.</span><span class="sxs-lookup"><span data-stu-id="306a1-116">To insert a message into a queue, use the **put\_message** method to create a new message and add it to the queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="306a1-117">Практическое руководство. Просмотр следующего сообщения</span><span class="sxs-lookup"><span data-stu-id="306a1-117">How To: Peek at the Next Message</span></span>
<span data-ttu-id="306a1-118">Вы можете просмотреть сообщение в начале очереди, не удаляя его из нее, вызвав метод **peek\_messages**.</span><span class="sxs-lookup"><span data-stu-id="306a1-118">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages** method.</span></span> <span data-ttu-id="306a1-119">По умолчанию метод **peek\_messages** просматривает одно сообщение.</span><span class="sxs-lookup"><span data-stu-id="306a1-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="306a1-120">Практическое руководство. Удаление следующего сообщения из очереди</span><span class="sxs-lookup"><span data-stu-id="306a1-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="306a1-121">Ваш код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="306a1-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="306a1-122">При вызове метода **get\_messages** вы по умолчанию получаете следующее сообщение в очереди.</span><span class="sxs-lookup"><span data-stu-id="306a1-122">When you call **get\_messages**, you get the next message in a queue by default.</span></span> <span data-ttu-id="306a1-123">Сообщение, возвращаемое методом **get\_messages**, становится невидимым для другого кода, считывающего сообщения из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="306a1-123">A message returned from **get\_messages** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="306a1-124">По умолчанию это сообщение остается невидимым в течение 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="306a1-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="306a1-125">Чтобы завершить удаление сообщения из очереди, необходимо также вызвать метод **delete\_message**.</span><span class="sxs-lookup"><span data-stu-id="306a1-125">To finish removing the message from the queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="306a1-126">Этот двухэтапный процесс удаления сообщения позволяет удостовериться, что если коду не удастся обработать сообщение из-за сбоя оборудования или программного обеспечения, другой экземпляр кода сможет получить то же сообщение и повторить попытку.</span><span class="sxs-lookup"><span data-stu-id="306a1-126">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="306a1-127">Код вызывает метод **delete\_message** сразу после обработки сообщения.</span><span class="sxs-lookup"><span data-stu-id="306a1-127">Your code calls **delete\_message** right after the message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="306a1-128">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="306a1-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="306a1-129">Во-первых, можно получить пакет сообщений (до 32 сообщений).</span><span class="sxs-lookup"><span data-stu-id="306a1-129">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="306a1-130">Во-вторых, можно задать более длительное или короткое время ожидания видимости, чтобы предоставить коду больше или меньше времени на полную обработку каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="306a1-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="306a1-131">В следующем примере кода метод **get\_messages** используется для получения 16 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="306a1-131">The following code example uses the **get\_messages** method to get 16 messages in one call.</span></span> <span data-ttu-id="306a1-132">Затем он обрабатывает каждое сообщение с помощью цикла for.</span><span class="sxs-lookup"><span data-stu-id="306a1-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="306a1-133">Он также задает время ожидания невидимости 5 минут для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="306a1-133">It also sets the invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="306a1-134">Практическое руководство. Изменение содержимого сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="306a1-134">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="306a1-135">Вы можете изменить содержимое сообщения непосредственно в очереди.</span><span class="sxs-lookup"><span data-stu-id="306a1-135">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="306a1-136">Если сообщение представляет собой рабочую задачу, можно использовать эту функцию для обновления состояния рабочей задачи.</span><span class="sxs-lookup"><span data-stu-id="306a1-136">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="306a1-137">Приведенный ниже код использует метод **update\_message** для обновления сообщения.</span><span class="sxs-lookup"><span data-stu-id="306a1-137">The code below uses the **update\_message** method to update a message.</span></span> <span data-ttu-id="306a1-138">Время ожидания видимости равно 0. Это означает, что сообщение появится немедленно, и содержимое обновится.</span><span class="sxs-lookup"><span data-stu-id="306a1-138">The visibility timeout is set to 0, meaning the message appears immediately and the content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="306a1-139">Практическое руководство. Получение длины очереди</span><span class="sxs-lookup"><span data-stu-id="306a1-139">How To: Get the Queue Length</span></span>
<span data-ttu-id="306a1-140">Вы можете узнать приблизительное количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="306a1-140">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="306a1-141">Метод **get\_queue\_metadata** запрашивает у службы очереди **приблизительное количество сообщений** и метаданные очереди.</span><span class="sxs-lookup"><span data-stu-id="306a1-141">The **get\_queue\_metadata** method asks the queue service to return metadata about the queue, and the **approximate_message_count**.</span></span> <span data-ttu-id="306a1-142">В результате число указывается лишь приблизительно, так как сообщения могут добавляться или удаляться после ответа службы очередей на ваш запрос.</span><span class="sxs-lookup"><span data-stu-id="306a1-142">The result is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="306a1-143">Практическое руководство. Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="306a1-143">How To: Delete a Queue</span></span>
<span data-ttu-id="306a1-144">Чтобы удалить очередь и все сообщения в ней, вызовите метод **delete\_queue**.</span><span class="sxs-lookup"><span data-stu-id="306a1-144">To delete a queue and all the messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="306a1-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="306a1-145">Next Steps</span></span>
<span data-ttu-id="306a1-146">Вы ознакомились с основными понятиями хранилища очередей. Дополнительные сведения см. по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="306a1-146">Now that you've learned the basics of Queue storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="306a1-147">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="306a1-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="306a1-148">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="306a1-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="306a1-149">[Блог рабочей группы службы хранилища Azure]</span><span class="sxs-lookup"><span data-stu-id="306a1-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="306a1-150">[пакет SDK для службы хранилища Microsoft Azure для Python]</span><span class="sxs-lookup"><span data-stu-id="306a1-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Блог рабочей группы службы хранилища Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[пакет SDK для службы хранилища Microsoft Azure для Python]: https://github.com/Azure/azure-storage-python