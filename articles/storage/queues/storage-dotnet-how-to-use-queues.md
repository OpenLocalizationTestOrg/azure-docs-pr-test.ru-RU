---
title: "aaaGet работы с хранилищем очередей Azure, с помощью .NET | Документы Microsoft"
description: "Очереди хранилища обеспечивают надежный асинхронный обмен сообщениями между компонентами приложения. Облака обмена сообщениями позволяет tooscale компоненты вашего приложения независимо друг от друга."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a>Приступая к работе с хранилищем очередей Azure с помощью .NET
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Обзор
Хранилище очередей Azure — это служба, обеспечивающая обмен сообщениями в облаке между компонентами приложения. При разработке приложений для масштабирования компоненты приложения часто не связаны между собой, так что они могут масштабироваться независимо друг от друга. Хранилище очередей обеспечивает асинхронный обмен сообщениями для взаимодействия между компонентами приложения, ли они выполняются в облаке hello, на рабочем столе hello, на локальном сервере или на мобильном устройстве. Хранилище очередей также поддерживает управление асинхронными задачами и создание рабочих процессов.

### <a name="about-this-tutorial"></a>О данном учебнике
В этом учебнике показано, как toowrite .NET кода в некоторых распространенных сценариях, с помощью хранилища очередей Azure. Эти сценарии включают создание и удаление очередей, а также добавление, чтение и удаление сообщений.

**Предполагаемое время toocomplete:** 45 минут

**Предварительные требования**

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Клиентская библиотека хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Диспетчер конфигураций Azure для .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [учетная запись хранения Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Добавление директив using
Добавьте следующее hello `using` директивы toohello вверху hello `Program.cs` файла:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a>Синтаксический анализ строки соединения hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a>Создание клиента службы очередей hello
Hello **CloudQueueClient** класс позволяет вам tooretrieve очереди, хранящиеся в очереди хранилища. Вот один из способов toocreate hello службы клиента.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
Теперь все готово toowrite код, который считывает и записывает tooQueue хранения данных.

## <a name="create-a-queue"></a>Создание очереди
В этом примере показано, как toocreate очереди, если он еще не существует:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a>Вставка сообщения в очередь
tooinsert сообщения в существующую очередь, сначала создайте **CloudQueueMessage**. Затем вызовите hello **AddMessage** метод. Для создания объекта **CloudQueueMessage** можно использовать строку (в формате UTF-8) или массив **байтов**. Ниже приведен код (если он не существует), который создает очередь и вставок приветственное сообщение «Hello, World»:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a>Просмотр следующего сообщения hello
Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **PeekMessage** метод.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a>Изменить содержимое hello сообщение из очереди
Вы можете изменить содержимое сообщений на месте в очереди hello hello. Если сообщение представляет рабочей задачи, можно использовать этот компонент tooupdate состояние hello рабочих задач. После кода Hello обновляется приветственное сообщение очереди новое содержимое и наборы hello tooextend время ожидания видимости другой 60 секунд. Сохраняет состояние работ, сопряженные с приветственное сообщение hello и предоставляет другой минуты toocontinue работа на приветственное сообщение клиента hello. Можно использовать этот рабочих процессов способ tootrack многоэтапной для очереди сообщений без необходимости toostart через от начала hello при неудачном завершении шага обработки из-за toohardware или ошибок программного обеспечения. Как правило, будет хранить значение числа повторов, и если hello сообщение повторяется более  *n*  раз, следует удалить его. Это обеспечивает защиту от сообщений, которые инициируют ошибку приложения при каждой попытке обработки.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a>Отмена очередь следующего сообщения hello
Код удаляет сообщение из очереди в два этапа. При вызове **GetMessage**, вы получаете следующее сообщение hello в очереди. Сообщение, возвращенное из **GetMessage** становится невидимой tooany другой код, чтение сообщений из этой очереди. По умолчанию это сообщение остается невидимым в течение 30 секунд. toofinish удаление приветственное сообщение из очереди hello, необходимо также вызвать **DeleteMessage**. Это двухэтапный процесс удаления сообщения подтверждает, если tooprocess получит сообщение toohardware или ошибок программного обеспечения, другой экземпляр кода из-за сбоя программы hello одного сообщения и повторите попытку. Вызовы кода **DeleteMessage** сразу после обработки сообщения hello.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>Использование алгоритма Async-Await со стандартными интерфейсами API хранилища очередей
В этом примере показано, как hello toouse Async-Await шаблона с хранилищем общих очередей API-интерфейсы. Образец Hello вызывает hello асинхронную версию каждого hello, учитывая методы, как указано в hello *Async* суффикс каждого метода. При использовании асинхронного метода hello async-await шаблон приостанавливает локальное выполнение до завершения вызова hello. Такое поведение позволяет hello текущий поток toodo другие типы работ, что позволяет избежать проблем с производительностью и повышает общую скорость реагирования приложения hello. Дополнительные сведения об использовании hello шаблон Async-Await в .NET см. в разделе [Async и Await (C# и Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>Дополнительные параметры для удаления сообщений из очереди
Способ извлечения сообщения из очереди можно настроить двумя способами.
Во-первых можно получить пакет сообщений (вверх too32). Во-вторых можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения. Hello следующий пример кода использует **GetMessages** метод tooget 20 сообщений в одном вызове. Затем он обрабатывает каждое сообщение с помощью цикла **foreach** . Он также устанавливает минут toofive hello невидимости время ожидания для каждого сообщения. Обратите внимание, что hello 5 минут запускается для всех сообщений в hello же время, поэтому после 5 минут с момента вызова hello слишком**GetMessages**, все сообщения, которые не были удалены становятся видимыми.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a>Получает длину очереди hello
Можно получить оценку hello количество сообщений в очереди. **FetchAttributes** метод запрашивает hello службы очередей для получения атрибутов hello очереди, включая количество сообщений hello. Hello **ApproximateMessageCount** свойство возвращает последнее значение hello извлекается с **FetchAttributes** метод без вызова службы очередей hello.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a>Удаление очереди
toodelete все сообщения hello и очереди содержащиеся в нем, вызовите метод **удалить** метод hello объекта очереди.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища очередей, выполните эти ссылки toolearn о более сложных задач хранилища.

* Просмотрите hello очереди службы справочной документации для получения подробной информации о доступных API-интерфейсы:
  * [Справочник по клиентской библиотеке хранилища для .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [Справочник по REST API](http://msdn.microsoft.com/library/azure/dd179355)
* Узнайте, как код hello toosimplify создавать toowork со службой хранилища Azure с помощью hello [SDK веб-заданий Azure](../../app-service-web/websites-dotnet-webjobs-sdk.md).
* Просмотрите дополнительные toolearn функция руководства о дополнительных параметрах для хранения данных в Azure.
  * [Начало работы с хранилищем таблиц Azure, с помощью .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore структурированные данные.
  * [Начало работы с хранилищем больших двоичных объектов Azure с помощью .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore неструктурированных данных.
  * [Подключение tooSQL базы данных с помощью .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore реляционных данных.

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
