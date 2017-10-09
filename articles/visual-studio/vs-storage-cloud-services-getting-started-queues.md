---
title: "aaaGet работы с хранилищем очередей и Visual Studio подключенных служб (облачных служб) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища очередей Azure в проект облачной службы в Visual Studio после подключения tooa учетной записи хранилища с помощью Visual Studio подключенные службы"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 1e90eeb826131cadca90dcb720c931fff5fedcb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Приступая к работе с подключенными службами хранилища очередей Azure и Visual Studio (проекты облачных служб)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Обзор
В этой статье описывается, как tooget запущена с помощью хранилища очередей Azure в Visual Studio после создания или ссылка на учетную запись хранилища Azure в проекте облачных служб с помощью Visual Studio hello **Добавление подключенных служб** диалоговое окно .

Мы покажем, как toocreate очередь в коде. Мы также покажем, как tooperform basic очередь операций, таких как добавление, изменение, чтение и удаление сообщений очереди. Hello примеры написаны на языке C# и использовать hello [клиентская библиотека хранилища Microsoft Azure для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Hello **Добавление подключенных служб** операция устанавливает пакеты tooaccess hello соответствующие NuGet хранилища Azure в проекте и добавляет строку hello подключения для hello учетную запись хранилища, tooyour файлы конфигурации проекта.

* Дополнительные сведения о выполнении операций с очередями в коде см. в статье [Приступая к работе с хранилищем очередей Azure с помощью .NET](../storage/queues/storage-dotnet-how-to-use-queues.md).
* Общие сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).
* Общие сведения об облачных службах Azure см. в [документации по облачным службам](https://azure.microsoft.com/documentation/services/cloud-services/).
* Дополнительную информацию о программировании для ASP.NET см. в разделе [ASP.NET](http://www.asp.net).

Хранилище Azure очереди — это служба для хранения большого количества сообщений, которые может осуществляться из любого места в Здравствуй, мир! через вызовы прошедшего проверку подлинности, протокол HTTP или HTTPS. Сообщение одной очереди может быть вверх too64 КБ и очередь может содержать миллионы сообщений вверх toohello предел общая емкость учетной записи хранения.

## <a name="access-queues-in-code"></a>Доступ к очередям в коде
tooaccess очереди в проектах Visual Studio облачные службы, необходимо следующее hello tooinclude элементы tooany C# исходный файл, доступ к хранилищу Azure очереди.

1. Убедитесь, что объявления пространств имен hello hello верхней части файла hello C# включить эти **с помощью** инструкции.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения. Hello используйте следующий код tooget hello хранения строки соединения и сведения об учетной записи хранилища из конфигурации службы Azure hello.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Получить **CloudQueueClient** объектов tooreference hello очереди в учетной записи.  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Получить **CloudQueue** объекта tooreference определенной очереди.
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Примечание:** используются hello над кодом перед кода hello из hello следующие примеры.

## <a name="create-a-queue-in-code"></a>Создание очереди в коде
очередь toocreate hello в коде, просто добавьте вызов слишком**CreateIfNotExists**.

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a>Добавить tooa очереди сообщений
tooinsert сообщения в существующей очереди, создайте новый **CloudQueueMessage** объект, а затем вызов hello **AddMessage** метод.

Для создания объекта **CloudQueueMessage** можно использовать либо строку (в формате UTF-8), либо массив типа byte.

Ниже приведен пример, который вставляет приветственное сообщение «Hello, World».

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a>Чтение сообщения в очереди
Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **PeekMessage** метод.

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a>Чтение и удаление сообщения в очереди
Ваш код может удалить сообщение из очереди в два этапа.

1. Вызовите **GetMessage** tooget hello следующего сообщения в очереди. Сообщение, возвращенное из **GetMessage** становится невидимой tooany другой код, чтение сообщений из этой очереди. По умолчанию это сообщение остается невидимым в течение 30 секунд.
2. Удаление приветственное сообщение из очереди hello, вызов toofinish **DeleteMessage**.

Это двухэтапный процесс удаления сообщения подтверждает, если tooprocess получит сообщение toohardware или ошибок программного обеспечения, другой экземпляр кода из-за сбоя программы hello одного сообщения и повторите попытку. Hello следующий код вызывает **DeleteMessage** сразу после обработки сообщения hello.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a>Используйте дополнительные параметры tooprocess и удаления очереди сообщений
Способ извлечения сообщения из очереди можно настроить двумя способами.

* Можно получить пакет сообщений (вверх too32).
* Можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения. Hello следующий пример кода использует **GetMessages** метод tooget 20 сообщений в одном вызове. Затем он обрабатывает каждое сообщение с помощью цикла **foreach** . Он также устанавливает минут toofive hello невидимости время ожидания для каждого сообщения. Обратите внимание, что hello 5 минут запускается для всех сообщений в hello же время, поэтому после 5 минут с момента вызова hello слишком**GetMessages**, все сообщения, которые не были удалены становятся видимыми.

Ниже приведен пример:

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a>Получает длину очереди hello
Можно получить оценку hello количество сообщений в очереди. **FetchAttributes** метод запрашивает hello службы очередей для получения атрибутов hello очереди, включая количество сообщений hello. Hello **ApproximateMethodCount** свойство возвращает последнее значение hello извлекается с **FetchAttributes** метод без вызова службы очередей hello.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a>Использовать hello Async-Await шаблон с общие интерфейсы API очереди Azure
Этот пример показывает, как шаблон toouse hello Async-Await с общие интерфейсы API очереди Azure. Образец Hello вызывает hello асинхронной версии каждого из заданного методы hello, это можно увидеть, hello **Async** исправления после каждого метода. При асинхронного метода используется hello async-await шаблон приостанавливает локальное выполнение до завершения вызова hello. Такое поведение позволяет hello текущий поток toodo другие типы работ, который позволяет избежать проблем с производительностью и повышает общую скорость реагирования приложения hello. Дополнительные сведения об использовании hello шаблон Async-Await в .NET см. в разделе [Async и Await (C# и Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a>Удаление очереди
все сообщения hello и очереди, содержащиеся в нем, вызов hello toodelete **удалить** метод hello объекта очереди.

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

