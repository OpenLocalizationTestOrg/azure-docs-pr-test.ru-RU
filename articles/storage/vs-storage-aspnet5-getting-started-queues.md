---
title: "aaaGet работы с хранилищем очередей и Visual Studio подключенных служб (ASP.NET Core) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища очереди Azure в проекте ASP.NET Core в Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 75adb7163827ab17ad89707051ff0e48dbae9c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a>Приступая к работе с хранилищем очередей и подключенными службами Visual Studio (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Обзор
В этой статье описывается, как tooget запущена с помощью хранилища очередей Azure в Visual Studio после создания или ссылка на учетную запись хранилища Azure в проекте ASP.NET Core с помощью Visual Studio hello **Добавление подключенных служб** диалогового окна. Hello **Добавление подключенных служб** операция устанавливает пакеты tooaccess hello соответствующие NuGet хранилища Azure в проекте и добавляет строку hello подключения для hello учетную запись хранилища, tooyour файлы конфигурации проекта.

Хранилище очередей Azure — это служба для хранения большого числа сообщений, которые может осуществляться из любого места в Здравствуй, мир! через вызовы прошедшего проверку подлинности, протокол HTTP или HTTPS. Сообщение одной очереди может быть вверх too64 килобайт (КБ), размер и очередь может содержать миллионы сообщений вверх toohello предел общая емкость учетной записи хранения.

tooget работы, необходимо сначала toocreate очереди Azure в вашей учетной записи хранилища. Мы покажем, как toocreate очередь в коде. Мы также покажем, как tooperform basic очередь операций, таких как добавление, изменение, чтение и удаление сообщений очереди. Hello примеры на языке C\# кода и использовать hello клиентская библиотека хранилища Azure для .NET. Дополнительные сведения см. на сайте [ASP.NET](http://www.asp.net).

**Примечание:** некоторые интерфейсы API, которые выполняют вызовы tooAzure хранилища в ASP.NET Core hello являются асинхронными. Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)). Приведенный ниже код Hello предполагается, что используются асинхронные методы программирования.

* Дополнительные сведения о выполнении программных операций с очередями см. в статье [Приступая к работе с хранилищем очередей Azure с помощью .NET](storage-dotnet-how-to-use-queues.md).
* Общие сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).
* Общие сведения об облачных службах Azure см. в [документации по облачным службам](https://azure.microsoft.com/documentation/services/cloud-services/).
* Дополнительную информацию о программировании для ASP.NET см. в разделе [ASP.NET](http://www.asp.net).

## <a name="access-queues-in-code"></a>Доступ к очередям в коде
tooaccess очереди в проектах ASP.NET Core, требуются следующие hello tooinclude элементы tooany C# исходного файла, который получает доступ к хранилищу очереди Azure.

1. Убедитесь, что объявления пространств имен hello hello верхней части файла hello C# включить эти **с помощью** инструкции.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения. Hello используйте следующий код tooget hello хранения строки соединения и сведения об учетной записи хранилища из конфигурации службы Azure hello.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Получить **CloudQueueClient** объектов tooreference hello очереди в учетной записи.  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Получить **CloudQueue** объекта tooreference определенной очереди.
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Примечание:** используются hello над кодом перед кода hello из hello следующие примеры.

### <a name="create-a-queue-in-code"></a>Создание очереди в коде
hello toocreate очереди Azure в коде, просто добавьте вызов слишком**CreateIfNotExistsAsync**.

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a>Добавить tooa очереди сообщений
tooinsert сообщения в существующей очереди, создайте новый **CloudQueueMessage** объект, а затем вызов hello **AddMessageAsync** метод.

Для создания объекта **CloudQueueMessage** можно использовать либо строку (в формате UTF-8), либо массив типа byte.

Ниже приведен пример, который вставляет приветственное сообщение «Hello, World».

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a>Чтение сообщения в очереди
Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **PeekMessageAsync** метод.

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a>Чтение и удаление сообщения в очереди
Ваш код может удалить сообщение из очереди в два этапа.

1. Вызовите **GetMessageAsync** tooget hello следующего сообщения в очереди. Сообщение, возвращенное из **GetMessageAsync** становится невидимой tooany другой код, чтение сообщений из этой очереди. По умолчанию это сообщение остается невидимым в течение 30 секунд.
2. Удаление приветственное сообщение из очереди hello, вызов toofinish **DeleteMessageAsync**.

Это двухэтапный процесс удаления сообщения подтверждает, если tooprocess получит сообщение toohardware или ошибок программного обеспечения, другой экземпляр кода из-за сбоя программы hello одного сообщения и повторите попытку. Hello следующий код вызывает **DeleteMessageAsync** сразу после обработки сообщения hello.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a>Дополнительные варианты удаления сообщений из очереди
Способ извлечения сообщения из очереди можно настроить двумя способами.
Во-первых можно получить пакет сообщений (вверх too32). Во-вторых можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения. Hello следующий пример кода использует **GetMessages** метод tooget 20 сообщений в одном вызове. Затем он обрабатывает каждое сообщение с помощью цикла **foreach** . Он также устанавливает минут too5 hello невидимости время ожидания для каждого сообщения. Обратите внимание, что начала hello 5 минут для всех сообщений в hello же времени, поэтому после 5 минут после вызова hello слишком**GetMessages**, все сообщения, которые не были удалены становятся видимыми.

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a>Получает длину очереди hello
Можно получить оценку hello количество сообщений в очереди. **FetchAttributes** метод запрашивает hello службы очередей для получения атрибутов hello очереди, включая количество сообщений hello. Hello **ApproximateMethodCount** свойство возвращает последнее значение hello извлекается с **FetchAttributes** метод без вызова службы очередей hello.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a>Использование шаблона hello Async-Await с очередь общих API-интерфейсов
В этом примере показано, как toouse hello Async-Await шаблоном очередь общих интерфейсов API. Hello образец вызовы hello асинхронной версии каждого hello, учитывая методы. Это можно заметить исправлением hello Async после каждого метода. При использовании асинхронного метода hello шаблон Async-Await приостанавливает локальное выполнение до завершения вызова hello. Такое поведение позволяет hello текущий поток toodo другие типы работ, который позволяет избежать проблем с производительностью и повышает общую скорость реагирования приложения hello. Дополнительные сведения об использовании hello шаблон Async-Await в .NET, см. в разделе [Async и Await (C# и Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a>Удаление очереди
toodelete все сообщения hello и очереди содержащиеся в нем, вызовите метод **удалить** метод hello объекта очереди.

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

