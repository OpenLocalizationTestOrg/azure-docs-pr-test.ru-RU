---
title: "toouse aaaHow Azure Service Bus с hello SDK веб-заданий"
description: "Узнайте, как toouse Azure Service Bus очереди и разделы с описанием hello SDK веб-заданий."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a>Как toouse шины обслуживания Azure с hello SDK веб-заданий
## <a name="overview"></a>Обзор
В этом руководстве содержатся C# образцы кода, Показать как tootrigger процесса при получении сообщения об Azure Service Bus. Используйте образцы кода Hello [SDK веб-заданий](websites-dotnet-webjobs-sdk.md) версии 1.x.

Hello руководстве предполагается, вы знаете [как проект веб-задания в Visual Studio с подключением toocreate строки этой учетной записи хранения tooyour точки](websites-dotnet-webjobs-sdk-get-started.md).

фрагменты кода Hello Показывать только функции, не hello код, создающий hello `JobHost` объекта, как показано в примере:

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

Объект [полный пример кода Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) находится в хранилище azure — веб-заданий sdk примеры hello на GitHub.com.

## <a id="prerequisites"></a> Предварительные требования
toowork со служебной шиной имеют tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet пакета Кроме toohello другие пакеты SDK веб-заданий. 

Также имеется строка подключения AzureWebJobsServiceBus tooset hello в строки подключения хранилища toohello сложения.  Это можно сделать в hello `connectionStrings` раздел файла App.config hello, как показано в следующий пример hello:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Пример проекта, который включает строку подключения Service Bus hello в файле App.config hello, в разделе [Service Bus пример](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

также можно задать строки подключения Hello в среде выполнения Azure hello, которая затем перекрывает hello App.config при hello веб-задание в Azure; Дополнительные сведения см. в разделе [Приступая к работе с hello SDK веб-задания](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a>Как происходит получение tootrigger функции, если сообщение очереди Service Bus
вызывает функцию, которая hello SDK веб-заданий toowrite при получении сообщения в очереди, используйте hello `ServiceBusTrigger` атрибута. Конструктор атрибута Hello принимает параметр, задающий имя hello toopoll очереди hello.

### <a name="how-servicebustrigger-works"></a>Как действует ServicebusTrigger
Hello пакет SDK получает сообщение в `PeekLock` режим и вызовы `Complete` на приветственное сообщение, если функции hello завершается успешно, или вызовы `Abandon` при сбое функции hello. Если функции hello выполняется дольше, чем hello `PeekLock` время ожидания блокировки hello автоматически обновляется.

Service Bus выполняет собственную обработку очереди подозрительных сообщений, который не может управлять или настройки hello SDK веб-заданий. 

### <a name="string-queue-message"></a>Строковое сообщение очереди
Hello следующий код считывает сообщение очереди, которое содержит строку и записывает строку hello toohello панели мониторинга пакета SDK веб-заданий.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Примечание:** при создании hello очереди сообщений в приложении, которое не использует hello SDK веб-задания, убедитесь, что tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) слишком «text/plain».

### <a name="poco-queue-message"></a>Сообщения очереди POCO
пакет SDK для Hello автоматически выполнит десериализацию очереди сообщение, содержащее JSON для POCO [(обычный объект CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) типа. Hello следующий пример кода считывает очередь сообщение, содержащее `BlobInformation` объект, имеющий `BlobName` свойство:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Образцы кода, показывающий, как же hello toouse свойства toowork POCO hello с BLOB-объектов и таблиц в см. в разделе hello [хранилища очередей версию этой статьи](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Если код, создающий приветственных очереди сообщений не использует hello SDK веб-задания, используйте toohello аналогичный код, следующий пример:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>Типы, с которыми работает атрибут ServiceBusTrigger
Помимо `string` и типами POCO, можно использовать hello `ServiceBusTrigger` атрибута с помощью байтового массива или `BrokeredMessage` объекта.

## <a id="create"></a>Как toocreate Service Bus очередь сообщений
функция, которая создает новое сообщение очереди toowrite использовать hello `ServiceBus` атрибута и передайте в конструктор атрибута toohello имя очереди hello. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Создание одного сообщения очереди в неасинхронной функции
Следующий образец кода Hello использует toocreate выходной параметр, новые сообщения в очереди hello с именем «outputqueue» с таким же содержимое, так как hello сообщения, полученного в очередь hello, с именем «inputqueue» hello.

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

Hello выходной параметр для создания одной очереди сообщения может быть любой hello следующие типы:

* `string`
* `byte[]`
* `BrokeredMessage`
* Сериализуемый тип POCO, заданный вами Сериализируется как JSON автоматически.

Для параметров типа POCO сообщения в очереди всегда создается при завершении функции hello; Если параметр hello имеет значение null, hello SDK создает очереди сообщение, которое будет возвращать значение null, при получении сообщения hello и десериализации. Для Здравствуйте других типов, если параметр hello не определен создается сообщение в очереди.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Создание нескольких сообщений очереди или сообщений в асинхронных функциях
toocreate использовать несколько сообщений hello `ServiceBus` атрибутом `ICollector<T>` или `IAsyncCollector<T>`, как показано в hello следующий образец кода:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Каждое сообщение очереди создается сразу после hello `Add` вызывается метод.

## <a id="topics"></a>Как toowork с разделы служебной шины
вызывает функцию, которая hello SDK toowrite при получении сообщения в раздел служебной шины, используйте hello `ServiceBusTrigger` атрибута с hello конструктор, который принимает имя раздела и имя подписки, как показано в hello следующий образец кода:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

toocreate сообщения по теме, используйте hello `ServiceBus` атрибутом типа hello имя раздела таким же, как используется с именем очереди.

## <a name="features-added-in-release-11"></a>Функции, добавленные в версии 1.1
Привет, следующие атрибуты были добавлены в версии 1.1:

* Добавлена возможность обширной настройки обработки сообщений с помощью `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider`поддерживает настройку hello Service Bus `MessagingFactory` и `NamespaceManager`.
* Объект `MessageProcessor` шаблон стратегии позволяет toospecify процессор на очереди или раздела.
* По умолчанию поддерживается параллелизм обработки сообщений. 
* Упрощена настройка `OnMessageOptions` через `ServiceBusConfiguration.MessageOptions`.
* Разрешить [права](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe, указанные на `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (для сценариев, где возможно управление правами). Обратите внимание, что веб-заданий Azure не удается tooautomatically подготовки несуществующей очереди и разделы без права на управление.

## <a id="queues"></a>Связанные разделы, охватываемых хранилища очередей hello как tooarticle
Сведения о сценариях SDK веб-заданий не только tooService шины см. в разделе [как хранилище с hello SDK веб-заданий очередей toouse Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

В этой статье рассматриваются следующие hello:

* Асинхронные функции
* Выполнение на нескольких экземплярах
* Корректное завершение работы
* Использование пакета SDK веб-задания атрибутов в теле функции hello
* Набор строк подключения пакета SDK для hello в коде
* Установка значений параметров конструктора пакета SDK для заданий WebJob в коде
* Вызов функции вручную
* Запись журналов

## <a id="nextsteps"></a> Дальнейшие действия
В этом руководстве предоставила код образцы где показано, как toohandle распространенные сценарии для работы с Azure Service Bus. Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [рекомендуется заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).

