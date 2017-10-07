---
title: "aaaOptimizing Azure кода в Visual Studio | Документы Microsoft"
description: "Узнайте, каким образом средства оптимизации кода Azure в Visual Studio помогут сделать код более надежным и производительным."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a>Оптимизация кода Azure
При программировании приложений, использующих Microsoft Azure, существуют некоторые методики написания кода, необходимо следовать toohelp избежать проблем с масштабированием, поведения и производительности в облачной среде. Майкрософт предлагает инструмент анализа кода Azure, который распознает и идентифицирует часто встречающиеся проблемы, а также помогает их решить. Вы можете загрузить средство hello в Visual Studio через NuGet.

## <a name="azure-code-analysis-rules"></a>Правила анализа кода Azure
Средство анализа кода Azure Hello использует hello правилам tooautomatically пометок кода Azure при обнаружении известных проблем, влияющих на производительность. Обнаруженные проблемы отображаются в виде предупреждений или ошибок компилятора. Через значок лампочки часто предоставляются код исправления или подсказки tooresolve hello предупреждения или ошибки.

## <a name="avoid-using-default-in-process-session-state-mode"></a>Старайтесь не использовать режим состояния сеанса по умолчанию (внутрипроцессорный)
### <a name="id"></a>ИД
AP0000

### <a name="description"></a>Описание
Если вы используете режим состояния сеанса (в процессе) по умолчанию hello для облачных приложений, вы можете потерять состояние сеанса.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
По умолчанию режим состояния сеанса hello, указанных в файле web.config hello в процессе. Кроме того Если нет записи, указанную в файле конфигурации hello, hello режим состояния сеанса по умолчанию tooin процесса. Hello внутрипроцессный режим хранит состояние сеанса в памяти на веб-сервере hello. При перезапуске экземпляра или экземпляра используется для балансировки нагрузки и отработки отказа, не сохраняется состояние сеанса hello, хранятся в памяти на веб-сервере hello. Такая ситуация не позволяет hello приложению быть масштабируемым в облаке hello.

Состояние сеанса ASP.NET поддерживает несколько различных параметров хранения данных о состоянии сеанса: InProc, StateServer, SQLServer, Custom и Off. Рекомендуется использовать пользовательский режим toohost данных на внешнем хранилище состояния сеанса, таких как [поставщик состояния сеанса Azure для Redis](http://go.microsoft.com/fwlink/?LinkId=401521).

### <a name="solution"></a>Решение
Одно из рекомендуемых решений — toostore состояние сеанса на управляемой службы кэша. Узнайте, как toouse [поставщик состояния сеанса Azure для Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore состояния сеанса. Можно также сеанс магазина указать его в других местах tooensure что масштабируемые приложения в облаке hello. Дополнительные сведения об альтернативных решений прочитайте toolearn [режимы состояния сеанса](https://msdn.microsoft.com/library/ms178586).

## <a name="run-method-should-not-be-async"></a>Метод Run не должен быть асинхронным
### <a name="id"></a>ИД
AP1000

### <a name="description"></a>Описание
Создайте асинхронные методы (такие как [await](https://msdn.microsoft.com/library/hh156528.aspx)) за пределами hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метода, а затем вызов hello асинхронные методы из [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx). Объявления hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод асинхронным приводит hello рабочей роли tooenter цикл перезагрузки.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
Вызов асинхронных методов в hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод вызывает hello облачной службы среды выполнения toorecycle hello рабочей роли. При запуске рабочей роли все выполнение программы происходит внутри hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод. Для существующих hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод вызывает рабочий hello toorestart роли. Среда выполнения hello рабочей роли, достигнув hello асинхронного метода, он производит диспетчеризацию всех операций после асинхронного метода hello и возвращается. В результате hello рабочей роли tooexit из hello [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод и перезапуска. В следующей итерации hello выполнения hello рабочей роли попаданий hello попытку асинхронного метода и вызывает hello рабочей роли toorecycle еще раз, а также перезагрузки.

### <a name="solution"></a>Решение
Разместите все асинхронные операции вне hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод. Затем вызовите асинхронный метод hello рефакторинг из внутри hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метода, например .wait RunAsync (). Средство анализа кода Azure Hello может помочь решить эту проблему.

Привет, следующий фрагмент кода демонстрирует hello исправление кода для устранения этой проблемы:

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>Использование проверки подлинности подписанного URL-адреса с помощью служебной шины
### <a name="id"></a>ИД
AP2000

### <a name="description"></a>Description (Описание)
Используйте для проверки подлинности подписанный URL-адрес (SAS). Служба управления доступом (ACS) больше не используется для проверки подлинности служебной шины.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
Для повышения уровня безопасности Azure Active Directory заменяет проверку подлинности с помощью ACS на проверку подлинности с использованием SAS. В разделе [Azure Active Directory является hello будущих служб ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) сведения о плане перехода hello.

### <a name="solution"></a>Решение
В приложениях используйте проверку подлинности SAS. Hello в следующем примере показано, как toouse существующие SAS маркера tooaccess службы шины пространства имен или сущности.

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

В разделе hello в следующих разделах приводятся дополнительные сведения.

* Общие сведения см. в статье [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx) (Аутентификация на основе подписанного URL-адреса с помощью служебной шины).
* [Как toouse проверки подлинности подписи общий доступ со служебной шиной](https://msdn.microsoft.com/library/dn205161.aspx)
* Пример проекта см. на странице [Примеры кода Azure](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c).

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a>Рассмотрите возможность использования OnMessage метод tooavoid «цикла получения»
### <a name="id"></a>ИД
AP2002

### <a name="description"></a>Описание
tooavoid, поступающих в «цикл получения», вызывающему Привет **OnMessage** метод является лучшим решением для получения сообщений, чем вызывающему Привет **Receive** метод. Тем не менее если необходимо использовать hello **Receive** метод и укажите значение времени ожидания сервера не по умолчанию, убедитесь, что время ожидания сервера hello более одной минуты.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
При вызове **OnMessage**, hello клиент начинает процесс обработки внутренних сообщений, который постоянно опрашивает hello очереди или подписки. Этот процесс обработки сообщений содержит бесконечный цикл, который отправляет вызов tooreceive сообщений. Если время ожидания вызова hello, он выдает новый вызов. интервал времени ожидания Hello определяется по значению hello hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) свойство hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx), который используется.

Здравствуйте, преимущество использования **OnMessage** по сравнению слишком**Receive** является то, что пользователи не toomanually опрос на наличие сообщений, обработки исключений, обработки нескольких сообщений в параллельном режиме и завершить hello сообщения.

При вызове метода **Receive** без использования значения по умолчанию, было бы убедиться, что hello *ServerWaitTime* значение — более одной минуты. Установка *ServerWaitTime* toomore, чем на одну минуту предотвратит превышение времени ожидания до полного получения сообщения hello hello сервера.

### <a name="solution"></a>Решение
См. следующие примеры рекомендованного использования кода hello. Дополнительные сведения см. в статьях [Метод QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) и [Метод QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).

производительность hello tooimprove hello инфраструктуры обмена сообщениями Azure, см. шаблон проектирования hello [начало асинхронного обмена сообщениями](https://msdn.microsoft.com/library/dn589781.aspx).

Hello ниже приведен пример использования **OnMessage** tooreceive сообщений.

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

Hello ниже приведен пример использования **Receive** время ожидания сервера по умолчанию hello.

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

Hello ниже приведен пример использования **Receive** с сервера не по умолчанию время ожидания.

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a>Рассмотрите возможность использования асинхронных методов служебной шины
### <a name="id"></a>ИД
AP2003

### <a name="description"></a>Описание
Используйте асинхронную Service Bus методы tooimprove производительности обмена сообщениями через посредника.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
Использование асинхронных методов обеспечивает программный параллелизм приложений, так как выполнение каждого вызова не блокирует основной поток hello. При использовании методов обмена сообщениями служебной шины требуется время на выполнение операции (отправки, получения, удаления и т. д.). Это время включает в себя hello обработку hello операции по hello службы Service Bus задержки toohello сложения hello запроса и ответа hello. tooincrease число hello операций в единицу времени, необходимо выполнять их параллельно. Дополнительные сведения см. слишком[советы и рекомендации по производительности улучшения с помощью Service Bus обмен сообщениями](https://msdn.microsoft.com/library/azure/hh528527.aspx).

### <a name="solution"></a>Решение
В разделе [класс QueueClient (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) сведения о как toouse hello рекомендуется асинхронного метода.

производительность hello tooimprove hello инфраструктуры обмена сообщениями Azure, см. шаблон проектирования hello [начало асинхронного обмена сообщениями](https://msdn.microsoft.com/library/dn589781.aspx).

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>Попробуйте секционировать очереди и разделы служебной шины
### <a name="id"></a>ИД
AP2004

### <a name="description"></a>Description (Описание)
Секционирование очередей и разделов служебной шины для повышения производительности обмена сообщениями служебной шины.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
Секционирование очередей и разделов Service Bus повышает производительность пропускную способность и доступность службы, так как hello общая пропускная способность секционированной очереди или раздела больше не ограничивается hello производительностью одного брокера сообщений или хранилища обмена сообщениями. Кроме того, из-за временного сбоя хранилища сообщений секционированная очередь или раздел не становятся недоступными. Дополнительную информацию см. в разделе [Разделение сущностей обмена сообщениями](https://msdn.microsoft.com/library/azure/dn520246.aspx).

### <a name="solution"></a>Решение
Здравствуйте, в следующем фрагменте кода показан код как toopartition сущностей обмена сообщениями.

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Дополнительные сведения см. в разделе [секционированные очереди Service Bus и разделы | Блог Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) и извлечь hello [Microsoft Azure Service Bus секционированной очереди](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) образца.

## <a name="do-not-set-sharedaccessstarttime"></a>Не задавайте значение SharedAccessStartTime
### <a name="id"></a>ИД
AP3001

### <a name="description"></a>Описание
Следует избегать использования SharedAccessStartTimeset toohello текущей загрузке tooimmediately hello политики общего доступа. Требуется только tooset это свойство Если политики общего доступа toostart hello позже.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
Синхронизация часов вызывает небольшую разницу во времени между центрами обработки данных. Например можно логически подразумевается параметр hello время запуска политики SAS хранилища hello текущее время с помощью DateTime.Now или аналогичного метода может привести к тому hello SAS политики tootake силу немедленно. Однако hello небольшая разница во времени между центрами обработки данных может вызвать проблемы с данным, так как иногда центра обработки данных может быть немного позже, чем время начала hello, а другие — опережать. В результате hello политики SAS может истечь, быстро (или даже немедленно) Если слишком короткое время жизни политики hello.

Дополнительные рекомендации по использованию подписи общего доступа в службе хранилища Azure см. в разделе [Знакомство с SAS таблицы (подпись общего доступа) SAS очереди сайта и обновление tooBlob SAS - блоге разработчиков хранилища Microsoft Azure — Главная — блоги MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Решение
Удалите оператор hello, которое задает время начала hello hello общей политики доступа. Средство анализа кода Azure Hello предоставляется исправление, устраняющее эту проблему. Дополнительные сведения об управлении безопасностью см. в разделе шаблон разработки hello [шаблон ключа Valet](https://msdn.microsoft.com/library/dn568102.aspx).

Привет, следующий фрагмент кода демонстрирует hello исправление кода для устранения этой проблемы.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>Время окончания срока действия общей политики доступа должно быть больше пяти минут
### <a name="id"></a>ИД
AP3002

### <a name="description"></a>Описание
Может быть как разница пять минут в часы между центрами обработки данных в другое расположение, из-за tooa, называемое «расфазировки синхронизирующих импульсов.» tooprevent hello SAS маркера политики раньше, чем запланировано, задать toobe время истечения срока действия hello более пяти минут.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
Центры обработки данных в разных местах по всему Здравствуй, мир! синхронизировать по сигналу часов. Поскольку требуется времени для расположений toodifferent tootravel сигнал часов, хотя теоретически все синхронизировано может быть разница во времени между центрами обработки данных в разных географических местоположениях. Разница во времени может повлиять на hello общего доступа начала времени и истечения срока действия интервала политики. Таким образом tooensure политику общего доступа вступает в силу немедленно, не указывается время начала hello. Кроме того убедитесь, что срок действия hello больше, чем 5 минут, раннее tooprevent истечение времени ожидания.

Дополнительные сведения об использовании подписи общего доступа в службе хранилища Azure см. в разделе [Знакомство с SAS таблицы (подпись общего доступа) SAS очереди сайта и обновление tooBlob SAS - блоге разработчиков хранилища Microsoft Azure — Главная — блоги MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Решение
Дополнительные сведения об управлении безопасностью см. шаблон проектирования hello [шаблон ключа Valet](https://msdn.microsoft.com/library/dn568102.aspx).

Hello ниже приведен пример не указано время запуска политики общего доступа.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Hello ниже приведен пример указано время запуска политики общего доступа с длительностью политики более пять минут.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Дополнительную информацию см. в статье [Создание и использование подписанного URL-адреса](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="use-cloudconfigurationmanager"></a>Используйте CloudConfigurationManager
### <a name="id"></a>ИД
AP4000

### <a name="description"></a>Описание
С помощью hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) класса для проектов, таких как веб-сайт Azure и мобильных служб Azure, не вызовет проблемы среды выполнения. Рекомендуется, однако это рекомендуется toouse облака[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) как единый способ управления конфигурациями всех приложений облака Azure.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
CloudConfigurationManager считывает среду приложения toohello соответствующий файл конфигурации hello.

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>Решение
Рефакторинг toouse вашего кода hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx). Средство анализа кода Azure hello предоставляются исправления кода для этой проблемы.

Привет, следующий фрагмент кода демонстрирует hello исправление кода для устранения этой проблемы. Замените

`var settings = ConfigurationManager.AppSettings["mySettings"];`

на

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

Ниже приведен пример как toostore hello параметр конфигурации в файле App.config или Web.config. Добавьте параметры hello toohello раздел appSettings файла конфигурации hello. Hello Приведем hello файл Web.config для предыдущего примера кода hello.

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a>Избегайте использования жестко запрограммированных строк подключения
### <a name="id"></a>ИД
AP4001

### <a name="description"></a>Описание
Если использовать жестко запрограммированные строки подключения и необходимые tooupdate их позже будет toomake изменения tooyour исходный код и перекомпилировать приложение hello. Тем не менее если хранить строки подключения в файле конфигурации, можно изменить их позже, просто обновив файл конфигурации hello.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
Жестко запрограммированные строки подключения является нежелательным, поскольку возникают проблемы при toobe быстро изменить необходимые строки подключения. Кроме того Если hello проекту требуется возврат управления toosource toobe, жестко запрограммированные строки подключения привести уязвимости системы безопасности, поскольку hello строки можно увидеть в исходном коде hello.

### <a name="solution"></a>Решение
Хранение строк соединения в файлах конфигурации hello или средах Azure.

* Для автономных приложений используйте параметры строки подключения toostore app.config.
* Для размещенных в IIS веб-приложений используйте строки подключения toostore web.config.
* Для приложений ASP.NET vNext используйте configuration.json toostore соединения строки.

Сведения об использовании файлов конфигурации, таких как web.config или app.config, см. в разделе [Правила веб-конфигурации ASP.NET](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx). Сведения о принципах работы переменных среды Azure см. в записи блога [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) (Веб-сайты Microsoft Azure: как работают строки приложения и строки подключения). Чтобы узнать о хранении строки подключения в системе управления версиями см. в разделе [Source Control (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control) (Система управления версиями (создание реальных облачных приложений в Azure)).

## <a name="use-diagnostics-configuration-file"></a>Использование файла конфигурации диагностики
### <a name="id"></a>ИД
AP5000

### <a name="description"></a>Описание
Вместо настройки параметров диагностики в коде, например, с помощью Здравствуйте Microsoft.WindowsAzure.Diagnostics программным интерфейсом API, следует настроить параметры диагностики в файле diagnostics.wadcfg hello. (или в файле diagnostics.wadcfgx, если используется пакет Azure SDK 2.5). Таким образом, можно изменить параметры диагностики без необходимости toorecompile кода.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
Прежде чем Azure SDK 2.5 (с использованием диагностики Azure 1.3), Azure Diagnostics (WAD) можно было настраивать с использованием нескольких методов: добавление его toohello конфигурации BLOB-объектов в хранилище, с помощью императивного кода, декларативной конфигурации или по умолчанию hello Конфигурация. Тем не менее hello предпочтительный способ tooconfigure диагностики — toouse файла конфигурации XML (diagnostics.wadcfg или diagnositcs.wadcfgx для пакета SDK 2.5 и более поздние версии) в проект приложения hello. При таком подходе файл diagnostics.wadcfg hello полностью определяет конфигурацию hello и может обновляться и повторно развертываться по желанию. Смешивание hello использование файла конфигурации diagnostics.wadcfg hello с hello программными методами настройки конфигураций при применении hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)или [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) классы можно привести tooconfusion. Дополнительную информацию см. в статье [Инициализация или изменение конфигурации службы диагностики Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx).

Начиная с версии 1.3 службы WAD (входит в состав пакета Azure SDK 2.5), он больше не tooconfigure диагностики возможных toouse кода. В результате можно предоставить только hello конфигурации при применении или обновлении расширения диагностики hello.

### <a name="solution"></a>Решение
Использование hello конфигурации конструктора toomove параметров диагностики toohello диагностики файла конфигурации диагностики (diagnositcs.wadcfg или diagnositcs.wadcfgx для пакета SDK 2.5 и более поздние версии). Кроме того, рекомендуется установить [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) и использовать последние функции диагностики hello.

1. Hello контекстного меню для роли hello, которое следует tooconfigure выберите свойства и выберите вкладки "Конфигурация" hello.
2. В hello **диагностики** статьи, убедитесь, что hello **включить диагностику** установлен флажок.
3. Выберите hello **Настройка** кнопки.

   ![Доступ к параметр Включить диагностику hello](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   Дополнительную информацию см. в статье [Настройка системы диагностики для облачных служб и виртуальных машин Azure](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>Не объявляйте объекты DbContext статическими
### <a name="id"></a>ИД
AP6000

### <a name="description"></a>Описание
toosave памяти, не объявляйте объекты DBContext как статические.

Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Причина
Объекты DBContext содержат hello результаты запроса из каждого вызова. Статические объекты DBContext не удаляются, пока не будет выгружен домен приложения hello. В связи с этим статический объект DBContext может использовать большой объем памяти.

### <a name="solution"></a>Решение
Объявите DBContext как локальную переменную или поле нестатического экземпляра, используйте его для задачи, а после использования он будет удален.

Следующий пример класса контроллера MVC Hello показано, как toouse hello объекта DBContext.

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о оптимизация и устранение неполадок приложения Azure в разделе [Устранение неполадок веб-приложения в службе приложений Azure с помощью Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).
