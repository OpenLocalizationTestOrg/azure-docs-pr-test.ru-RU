---
title: "API-интерфейсы управления API Azure, концентраторов событий и Runscope aaaMonitor | Документы Microsoft"
description: "Образец приложения, демонстрирующий hello журнала к eventhub политики, подключающегося управления API Azure, концентраторов событий Azure и Runscope для протокола HTTP, ведение журнала и мониторинг"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a>Мониторинг API-интерфейсов с помощью службы управления API Azure, концентраторов событий и Runscope
Hello [службы управления API](api-management-key-concepts.md) предоставляет множество возможностей tooenhance hello обработку tooyour запросы, отправленные HTTP HTTP API. Однако hello существование hello запросы и ответы являются временными. запрос Hello и ее прохождения через hello API управления службы tooyour API внутреннего сервера. API обрабатывает hello запрос и ответ проходит обратно через toohello API потребителя. Hello службы управления API отслеживает важными данными статистики о hello API-интерфейсы для отображения на панели мониторинга портала издателя hello, но кроме этого, hello сведения будут удалены.

С помощью hello [журнала к eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [политики](api-management-howto-policies.md) в службе управления API hello может отправлять любые данные из запроса и ответа tooan hello [концентратор событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md). Существует множество причин, почему вы можете toogenerate события от HTTP-сообщений, отправляемых tooyour API-интерфейсы. В частности, это происходит при создании журнала аудита обновлений, анализе использования, оповещении об исключениях или интеграции служб сторонних поставщиков.   

В этой статье демонстрируется toocapture hello всего HTTP-запроса и ответного сообщения, отправить его tooan концентратора событий и затем ретрансляции сообщений службы сторонних производителей tooa, предоставляющий HTTP ведение журнала и мониторинг служб.

## <a name="why-send-from-api-management-service"></a>Почему лучше отправлять сообщения из службы управления API?
Это возможно toowrite HTTP по промежуточного слоя, можно подключить HTTP API платформы toocapture запросов и ответов HTTP и передать их в ведение журнала и мониторинг системы. Hello недостаток toothis подходом является по промежуточного слоя hello HTTP должен toobe интегрированы в API внутреннего сервера hello и должна соответствовать hello платформе hello API. Если существует несколько интерфейсов API каждого из них необходимо развернуть hello по промежуточного слоя. Зачастую серверный API-интерфейс невозможно обновить по той или иной причине.

С помощью toointegrate службы управления API Azure hello с инфраструктурой ведения журнала предоставляет решение централизованной и независимая от платформы. Он является масштабируемым частично из-за toohello [георепликации](api-management-howto-deploy-multi-region.md) возможности управления API Azure.

## <a name="why-send-tooan-azure-event-hub"></a>Зачем отправлять tooan концентратор событий Azure?
Это слишком много tooask, почему создать политику, которая имеет определенные tooAzure концентраторов событий? Существует много разных местах, когда необходимы toolog "Мои запросы". Почему нельзя просто отправьте hello запросы непосредственно окончательный адресат toohello?  Такой вариант возможен. Однако при составлении запросов ведения журнала из службы управления API, это необходимые tooconsider как сообщения для ведения журнала будут влиять на производительность hello hello API. Постепенное увеличение нагрузки можно компенсировать, увеличив количество доступных экземпляров компонентов системы или используя георепликацию. Однако короткие всплески нагрузки трафика может привести к toobe запросов, существенно задержки, если tooslow под нагрузкой запуска инфраструктуры toologging запросов.

Hello концентраторов событий Azure спроектированный tooingress огромного количества данных, емкости для работы с гораздо более высокие число событий, чем число hello HTTP запрашивает большинство API-интерфейсы процесса. Hello концентраторов событий действует в качестве сложных буфера между API управления службой и hello инфраструктуры, будет хранить и обрабатывать сообщения hello. Это гарантирует, что API производительность не снижается из-за toohello инфраструктуры ведения журналов.  

После hello данных была передана tooan концентратора событий, он сохраняется и будет ожидать tooprocess потребителей концентратора событий его. Hello концентратора событий не имеет значения, как оно будет обработано, просто заботится о том, как убедиться, что будет успешно доставлено сообщение hello.     

Концентраторы событий имеют hello возможность toostream события toomultiple групп потребителей. Это позволяет toobe события, обрабатываемые совершенно разных систем. Благодаря этому поддержка многих сценариев интеграции не помещая Добавление задержек на hello обработки запроса API hello в службе управления API hello мере toobe создается только одно событие.

## <a name="a-policy-toosend-applicationhttp-messages"></a>Сообщение http приложений toosend политики
Концентратор событий принимает данные события в виде простой строки содержимое строки Hello полностью функционируют tooyou. возможности toopackage toobe Настройка HTTP-запроса и отправляют tooEvent концентраторы, нам нужно строка hello tooformat с данными запроса или ответа hello. В таких ситуациях при наличии существующего формата, которую мы можно повторно использовать, затем мы отсутствуют toowrite нашей синтаксического анализа кода. Вначале я считается с помощью hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) для отправки запросов и ответов HTTP. Но этот формат оптимизирован для сохранения последовательности HTTP-запросов в формате JSON. Он содержит ряд обязательных элементов, которые добавлены излишней сложности для сценария hello передачи по сети hello сообщение hello HTTP.  

Альтернативным вариантом был toouse hello `application/http` тип мультимедиа, как описано в спецификации hello HTTP [RFC 7230](http://tools.ietf.org/html/rfc7230). Этот тип мультимедиа использует hello точно в том же формате, то есть используется tooactually отправки HTTP-сообщений по сети hello, но все сообщение hello может быть помещен в тексте hello другой HTTP-запроса. В нашем случае просто будет текст hello toouse как нашей tooEvent toosend сообщение концентраторов. К счастью, имеется средство синтаксического анализа, который существует в [клиента Microsoft ASP.NET Web API 2.2](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) библиотеки, которые можно проанализировать этот формат и преобразовать его в машинный код hello `HttpRequestMessage` и `HttpResponseMessage` объектов.

возможности toocreate toobe это сообщение, нам нужно tootake преимуществами C# на основе [выражения политики](https://msdn.microsoft.com/library/azure/dn910913.aspx) в службе управления API Azure. Вот hello политики, который отправляет tooAzure сообщения запроса HTTP концентраторов событий.

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a>Объявление политики
Некоторые элементы этого выражения политики следует разъяснить. политика журнала к eventhub Hello имеет атрибут с именем средства ведения журнала идентификатор, который ссылается toohello имя средства ведения журнала, созданного в службе управления API hello. Здравствуйте, подробные сведения о как toosetup средство ведения журнала концентратора событий в службе управления API hello можно найти в документе hello [как tooAzure toolog событий концентраторов событий в Azure API Management](api-management-howto-log-event-hubs.md). второй атрибут Hello имеет дополнительный параметр, который указывает, что концентраторы событий сообщений hello toostore секции в. Концентраторы событий используйте scalabilty tooenable секций и требуется как минимум два. упорядоченную доставку сообщений Hello гарантируется только внутри секции. Если мы не загружался концентратора событий, в какой секции tooplace приветственное сообщение, он будет использовать алгоритм циклического toodistribute hello нагрузки. Однако, может вызвать некоторые из наших toobe сообщений, обработанных не по порядку.  

### <a name="partitions"></a>Разделы
tooensure нашей сообщения доставляются по порядку tooconsumers и воспользоваться возможностью распределения нагрузки hello секций, я выбрал toosend HTTP запроса сообщения tooone и HTTP ответа сообщения tooa второй разделов. Это обеспечит равномерное распределение нагрузки и одновременно гарантирует, что все запросы и ответы будут обрабатываться по порядку. Существует возможность toobe ответа, перед hello соответствующего запроса, но как это не проблема, как у нас есть tooresponses запрашивает другой механизм корреляции, и мы знаем, что запросы всегда находятся перед ответов.

### <a name="http-payloads"></a>Полезные данные HTTP
После построения hello `requestLine` мы проверяем toosee, если hello текст запроса должен быть усечен. текст запроса Hello — усеченное tooonly 1024. Его можно увеличить, однако отдельные сообщения концентратора событий являются ограниченные too256KB, поэтому вполне вероятно, что некоторые сообщения HTTP институтов будет не помещаются в одно сообщение. При выполнении ведение журнала и аналитика значительный объем сведения могут быть производными от только что hello строка запроса HTTP и заголовки. Также много запросов API возвращает только небольших тел и поэтому потери hello информативные путем усечения больших фрагментов довольно минимален сравнения снижению toohello передачи, обработки и хранения обходится tookeep все содержимое тела. Последнее замечание об обработка текста hello является необходимость toopass `true` toohello как<string>метод () так, как мы читаете hello содержимое тела, однако указано также требуется hello API внутреннего сервера toobe может tooread hello текста. Передав значение true, toothis метод мы вызвать toobe текст hello в буфер, чтобы она могла считывать во второй раз. Это важные toobe помнить при наличии API-Интерфейсы, не передачи файлов очень большого объема и использует долго опрашивающего. В этих случаях было бы наиболее tooavoid чтения текста hello вообще.   

### <a name="http-headers"></a>HTTP-заголовки
HTTP-заголовков, можно просто передать по в формат сообщений hello в формате пары ключ значение. Мы выбрали toostrip безопасность, определенных полей, tooavoid без необходимости утечка учетные данные. Для анализа ключи API и другие учетные данные, скорее всего, не потребуются. Если мы toodo анализа для пользователя hello и конкретного продукта hello они используют, а затем, удалось получить из hello `context` и добавить это сообщение toohello.     

### <a name="message-metadata"></a>Метаданные сообщения
При создании концентратора событий toohello toosend полное сообщение hello, первая строка hello не фактически является частью hello `application/http` сообщения. Первая строка Hello это дополнительные метаданные, состоящий из ли сообщение hello — это сообщение запроса или ответа и идентификатора сообщения, используемые toocorrelate запрашивает tooresponses. Идентификатор сообщения Hello создается с помощью другой политики, который выглядит следующим образом:

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

Можно было создать сообщение запроса hello, сохраняется, переменная до hello ответ был возвращается и затем просто отправляется hello запроса и ответа в одном сообщении. Тем не менее, отправляя hello запроса и ответа независимо друг от друга и с помощью toocorrelate идентификатор сообщения hello два, получить более гибко размер сообщения hello, hello возможность tootake преимуществами нескольких секций одновременным сохраняя порядок сообщений и hello запрос появляется раньше, в нашей информационной панели ведения журнала. Также возможны некоторые сценарии где допустимый ответ никогда не отправляется концентратора событий toohello, возможно из-за tooa запрос Неустранимая ошибка в службе управления API hello, но мы по-прежнему будет иметь запись запроса hello.

сообщение Hello политики toosend hello ответа HTTP выглядит аналогично toohello запрос и завершить hello так конфигурация политики выглядит следующим образом:

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

Hello `set-variable` политика создает значение, которое доступно для обоих hello `log-to-eventhub` политики в hello `<inbound>` раздел и hello `<outbound>` раздела.  

## <a name="receiving-events-from-event-hubs"></a>Получение событий от концентраторов событий
Будут получены события из концентратора событий Azure с помощью hello [протокола AMQP](http://www.amqp.org/). Hello шину обслуживания Microsoft team были сделаны клиента использование событий проще hello toomake доступных библиотек. Существует два различных подхода поддерживается, создается один *прямой потребитель* и использует другие hello hello `EventProcessorHost` класса. Примеры этих двух подходов можно найти в hello [руководство по программированию концентраторов событий](../event-hubs/event-hubs-programming-guide.md). является краткой версией Hello hello различия, `Direct Consumer` предоставляет полный контроль и hello `EventProcessorHost` не часть работы направляющее hello для вас но делает определенные предположения о том, как будет обрабатывать эти события.  

### <a name="eventprocessorhost"></a>EventProcessorHost
В этом примере мы будем использовать hello `EventProcessorHost` для простоты, однако он может не hello наилучшим образом подходят для этой конкретной ситуации. `EventProcessorHost`Здравствуйте непростая работа убедиться, что у вас нет tooworry о работе с потоками проблемы в рамках конкретного процессора класса событий. Однако в нашем случае мы просто преобразование формата tooanother сообщение hello и передавая tooanother службы, с помощью асинхронного метода. У нас нет необходимости обновлять общее состояние, и нет риска возникновения проблем с потоками. В большинстве случаев `EventProcessorHost` , скорее всего, является лучшим выбором hello и это определенно hello простой вариант.     

### <a name="ieventprocessor"></a>IEventProcessor
Центральное понятие Hello при использовании `EventProcessorHost` toocreate является реализация hello `IEventProcessor` интерфейс, который содержит метод hello `ProcessEventAsync`. Hello суть этого метода показан ниже:

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

Список объектов EventData передаются в метод hello и мы перебора этого списка. байт Hello каждого метода синтаксического анализа в объект HttpMessage и этот объект передается экземпляр tooan IHttpMessageProcessor.

### <a name="httpmessage"></a>HttpMessage
Hello `HttpMessage` экземпляр содержит три элемента данных:

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

Hello `HttpMessage` экземпляр содержит `MessageId` идентификатор GUID, который позволяет нам запрос hello HTTP tooconnect toohello соответствующие HTTP-ответа и логическое значение, которое определяет, если hello содержит экземпляр HttpRequestMessage и HttpResponseMessage. С помощью hello, встроенных в классы HTTP из `System.Net.Http`, я был может tootake преимуществами hello `application/http` синтаксического анализа кода, который включен в `System.Net.Http.Formatting`.  

### <a name="ihttpmessageprocessor"></a>IHttpMessageProcessor
Hello `HttpMessage` tooimplementation объекта затем передается экземпляр `IHttpMessageProcessor` которого является интерфейсом, я создал toodecouple hello получение и интерпретация hello события из концентратора событий Azure и hello фактического его обработки.

## <a name="forwarding-hello-http-message"></a>Пересылка hello HTTP-сообщения
Для этого примера я решил было бы интересно toopush hello HTTP-запроса по слишком[Runscope](http://www.runscope.com). Runscope — это облачная служба, предназначенная для отладки, регистрации и мониторинга HTTP-запросов. Они имеют уровень free, поэтому просто tootry и позволяет нам toosee hello HTTP-запросов при передаче в режиме реального времени через наша служба управления API.

Hello `IHttpMessageProcessor` реализация выглядит следующим образом,

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

Я был преимуществами может tootake [существующую библиотеку клиента для Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) , делает его легко toopush `HttpRequestMessage` и `HttpResponseMessage` экземпляров вверх в их службу. В порядке tooaccess hello Runscope API, вам потребуется учетная запись и ключ API. Инструкции по получению ключа API можно найти в hello [tooAccess создание приложений Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) видеоролике.

## <a name="complete-sample"></a>Полный пример
Hello [исходный код](https://github.com/darrelmiller/ApimEventProcessor) и тесты для образца hello на GitHub. Вам потребуется [службы управления API](api-management-get-started.md), [подключенного концентратора событий](api-management-howto-log-event-hubs.md)и [учетной записи хранилища](../storage/common/storage-create-storage-account.md) образец hello toorun самостоятельно.   

Hello образец является просто простое консольное приложение, которое прослушивает события из концентратора событий, преобразует их в `HttpRequestMessage` и `HttpResponseMessage` объектов и затем перенаправляет их toohello Runscope API.

В следующих анимированного изображения hello появится запрос сделан tooan API в hello портал разработчиков, hello консольного приложения отображение hello полученное сообщение, обработки и пересылки и Здравствуйте, запросов и ответов, отображаются в hello Runscope трафика Инспектор.

![Демонстрация пересылку tooRunscope запроса](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a>Сводка
Служба управления API Azure предоставляет трафика hello HTTP toocapture идеальное место пути tooand из собственные интерфейсы API. Концентраторы событий Azure — это высокомасштабируемое недорогое решение, которое собирает информацию о трафике и передает ее в системы дополнительной обработки для регистрации, мониторинга и сложного анализа. Подключение трафика стороны too3rd контроль различных систем, как Runscope является простым, как несколько десятков строк кода.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительная информация о концентраторах событий Azure
  * [Приступая к работе с концентраторами событий Azure](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Прием сообщений через EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Руководство по программированию концентраторов событий](../event-hubs/event-hubs-programming-guide.md)
* Дополнительные сведения об интеграции службы управления API и концентраторов событий
  * [Как tooAzure toolog событий концентраторов событий в службе управления API Azure](api-management-howto-log-event-hubs.md)
  * [Справочник по сущности "Средство ведения журнала"](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [Справочник по политике регистрации в концентраторе событий](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
