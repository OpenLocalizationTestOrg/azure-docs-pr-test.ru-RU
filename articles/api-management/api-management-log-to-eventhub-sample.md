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
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="1fecd-103">Мониторинг API-интерфейсов с помощью службы управления API Azure, концентраторов событий и Runscope</span><span class="sxs-lookup"><span data-stu-id="1fecd-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="1fecd-104">Hello [службы управления API](api-management-key-concepts.md) предоставляет множество возможностей tooenhance hello обработку tooyour запросы, отправленные HTTP HTTP API.</span><span class="sxs-lookup"><span data-stu-id="1fecd-104">hello [API Management service](api-management-key-concepts.md) provides many capabilities tooenhance hello processing of HTTP requests sent tooyour HTTP API.</span></span> <span data-ttu-id="1fecd-105">Однако hello существование hello запросы и ответы являются временными.</span><span class="sxs-lookup"><span data-stu-id="1fecd-105">However, hello existence of hello requests and responses are transient.</span></span> <span data-ttu-id="1fecd-106">запрос Hello и ее прохождения через hello API управления службы tooyour API внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="1fecd-106">hello request is made and it flows through hello API Management service tooyour backend API.</span></span> <span data-ttu-id="1fecd-107">API обрабатывает hello запрос и ответ проходит обратно через toohello API потребителя.</span><span class="sxs-lookup"><span data-stu-id="1fecd-107">Your API processes hello request and a response flows back through toohello API consumer.</span></span> <span data-ttu-id="1fecd-108">Hello службы управления API отслеживает важными данными статистики о hello API-интерфейсы для отображения на панели мониторинга портала издателя hello, но кроме этого, hello сведения будут удалены.</span><span class="sxs-lookup"><span data-stu-id="1fecd-108">hello API Management service keeps some important statistics about hello APIs for display in hello Publisher portal dashboard, but beyond that, hello details are gone.</span></span>

<span data-ttu-id="1fecd-109">С помощью hello [журнала к eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [политики](api-management-howto-policies.md) в службе управления API hello может отправлять любые данные из запроса и ответа tooan hello [концентратор событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="1fecd-109">By using hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in hello API Management service you can send any details from hello request and response tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="1fecd-110">Существует множество причин, почему вы можете toogenerate события от HTTP-сообщений, отправляемых tooyour API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="1fecd-110">There are a variety of reasons why you may want toogenerate events from HTTP messages being sent tooyour APIs.</span></span> <span data-ttu-id="1fecd-111">В частности, это происходит при создании журнала аудита обновлений, анализе использования, оповещении об исключениях или интеграции служб сторонних поставщиков.</span><span class="sxs-lookup"><span data-stu-id="1fecd-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="1fecd-112">В этой статье демонстрируется toocapture hello всего HTTP-запроса и ответного сообщения, отправить его tooan концентратора событий и затем ретрансляции сообщений службы сторонних производителей tooa, предоставляющий HTTP ведение журнала и мониторинг служб.</span><span class="sxs-lookup"><span data-stu-id="1fecd-112">This article demonstrates how toocapture hello entire HTTP request and response message, send it tooan Event Hub and then relay that message tooa third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="1fecd-113">Почему лучше отправлять сообщения из службы управления API?</span><span class="sxs-lookup"><span data-stu-id="1fecd-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="1fecd-114">Это возможно toowrite HTTP по промежуточного слоя, можно подключить HTTP API платформы toocapture запросов и ответов HTTP и передать их в ведение журнала и мониторинг системы.</span><span class="sxs-lookup"><span data-stu-id="1fecd-114">It is possible toowrite HTTP middleware that can plug into HTTP API frameworks toocapture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="1fecd-115">Hello недостаток toothis подходом является по промежуточного слоя hello HTTP должен toobe интегрированы в API внутреннего сервера hello и должна соответствовать hello платформе hello API.</span><span class="sxs-lookup"><span data-stu-id="1fecd-115">hello downside toothis approach is hello HTTP middleware needs toobe integrated into hello backend API and must match hello platform of hello API.</span></span> <span data-ttu-id="1fecd-116">Если существует несколько интерфейсов API каждого из них необходимо развернуть hello по промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="1fecd-116">If there are multiple APIs then each one must deploy hello middleware.</span></span> <span data-ttu-id="1fecd-117">Зачастую серверный API-интерфейс невозможно обновить по той или иной причине.</span><span class="sxs-lookup"><span data-stu-id="1fecd-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="1fecd-118">С помощью toointegrate службы управления API Azure hello с инфраструктурой ведения журнала предоставляет решение централизованной и независимая от платформы.</span><span class="sxs-lookup"><span data-stu-id="1fecd-118">Using hello Azure API Management service toointegrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="1fecd-119">Он является масштабируемым частично из-за toohello [георепликации](api-management-howto-deploy-multi-region.md) возможности управления API Azure.</span><span class="sxs-lookup"><span data-stu-id="1fecd-119">It is also scalable, in part due toohello [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-tooan-azure-event-hub"></a><span data-ttu-id="1fecd-120">Зачем отправлять tooan концентратор событий Azure?</span><span class="sxs-lookup"><span data-stu-id="1fecd-120">Why send tooan Azure Event Hub?</span></span>
<span data-ttu-id="1fecd-121">Это слишком много tooask, почему создать политику, которая имеет определенные tooAzure концентраторов событий?</span><span class="sxs-lookup"><span data-stu-id="1fecd-121">It is a reasonable tooask, why create a policy that is specific tooAzure Event Hubs?</span></span> <span data-ttu-id="1fecd-122">Существует много разных местах, когда необходимы toolog "Мои запросы".</span><span class="sxs-lookup"><span data-stu-id="1fecd-122">There are many different places where I might want toolog my requests.</span></span> <span data-ttu-id="1fecd-123">Почему нельзя просто отправьте hello запросы непосредственно окончательный адресат toohello?</span><span class="sxs-lookup"><span data-stu-id="1fecd-123">Why not just send hello requests directly toohello final destination?</span></span>  <span data-ttu-id="1fecd-124">Такой вариант возможен.</span><span class="sxs-lookup"><span data-stu-id="1fecd-124">That is an option.</span></span> <span data-ttu-id="1fecd-125">Однако при составлении запросов ведения журнала из службы управления API, это необходимые tooconsider как сообщения для ведения журнала будут влиять на производительность hello hello API.</span><span class="sxs-lookup"><span data-stu-id="1fecd-125">However, when making logging requests from an API management service, it is necessary tooconsider how logging messages will impact hello performance of hello API.</span></span> <span data-ttu-id="1fecd-126">Постепенное увеличение нагрузки можно компенсировать, увеличив количество доступных экземпляров компонентов системы или используя георепликацию.</span><span class="sxs-lookup"><span data-stu-id="1fecd-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="1fecd-127">Однако короткие всплески нагрузки трафика может привести к toobe запросов, существенно задержки, если tooslow под нагрузкой запуска инфраструктуры toologging запросов.</span><span class="sxs-lookup"><span data-stu-id="1fecd-127">However, short spikes in traffic can cause requests toobe significantly delayed if requests toologging infrastructure start tooslow under load.</span></span>

<span data-ttu-id="1fecd-128">Hello концентраторов событий Azure спроектированный tooingress огромного количества данных, емкости для работы с гораздо более высокие число событий, чем число hello HTTP запрашивает большинство API-интерфейсы процесса.</span><span class="sxs-lookup"><span data-stu-id="1fecd-128">hello Azure Event Hubs is designed tooingress huge volumes of data, with capacity for dealing with a far higher number of events than hello number of HTTP requests most APIs process.</span></span> <span data-ttu-id="1fecd-129">Hello концентраторов событий действует в качестве сложных буфера между API управления службой и hello инфраструктуры, будет хранить и обрабатывать сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-129">hello Event Hub acts as a kind of sophisticated buffer between your API management service and hello infrastructure that will store and process hello messages.</span></span> <span data-ttu-id="1fecd-130">Это гарантирует, что API производительность не снижается из-за toohello инфраструктуры ведения журналов.</span><span class="sxs-lookup"><span data-stu-id="1fecd-130">This ensures that your API performance will not suffer due toohello logging infrastructure.</span></span>  

<span data-ttu-id="1fecd-131">После hello данных была передана tooan концентратора событий, он сохраняется и будет ожидать tooprocess потребителей концентратора событий его.</span><span class="sxs-lookup"><span data-stu-id="1fecd-131">Once hello data has been passed tooan Event Hub it is persisted and will wait for Event Hub consumers tooprocess it.</span></span> <span data-ttu-id="1fecd-132">Hello концентратора событий не имеет значения, как оно будет обработано, просто заботится о том, как убедиться, что будет успешно доставлено сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-132">hello Event Hub does not care how it will be processed, it just cares about making sure hello message will be successfully delivered.</span></span>     

<span data-ttu-id="1fecd-133">Концентраторы событий имеют hello возможность toostream события toomultiple групп потребителей.</span><span class="sxs-lookup"><span data-stu-id="1fecd-133">Event Hubs have hello ability toostream events toomultiple consumer groups.</span></span> <span data-ttu-id="1fecd-134">Это позволяет toobe события, обрабатываемые совершенно разных систем.</span><span class="sxs-lookup"><span data-stu-id="1fecd-134">This allows events toobe processed by completely different systems.</span></span> <span data-ttu-id="1fecd-135">Благодаря этому поддержка многих сценариев интеграции не помещая Добавление задержек на hello обработки запроса API hello в службе управления API hello мере toobe создается только одно событие.</span><span class="sxs-lookup"><span data-stu-id="1fecd-135">This enables supporting many integration scenarios without putting addition delays on hello processing of hello API request within hello API Management service as only one event needs toobe generated.</span></span>

## <a name="a-policy-toosend-applicationhttp-messages"></a><span data-ttu-id="1fecd-136">Сообщение http приложений toosend политики</span><span class="sxs-lookup"><span data-stu-id="1fecd-136">A policy toosend application/http messages</span></span>
<span data-ttu-id="1fecd-137">Концентратор событий принимает данные события в виде простой строки</span><span class="sxs-lookup"><span data-stu-id="1fecd-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="1fecd-138">содержимое строки Hello полностью функционируют tooyou.</span><span class="sxs-lookup"><span data-stu-id="1fecd-138">hello contents of that string are completely up tooyou.</span></span> <span data-ttu-id="1fecd-139">возможности toopackage toobe Настройка HTTP-запроса и отправляют tooEvent концентраторы, нам нужно строка hello tooformat с данными запроса или ответа hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-139">toobe able toopackage up an HTTP request and send it off tooEvent Hubs we need tooformat hello string with hello request or response information.</span></span> <span data-ttu-id="1fecd-140">В таких ситуациях при наличии существующего формата, которую мы можно повторно использовать, затем мы отсутствуют toowrite нашей синтаксического анализа кода.</span><span class="sxs-lookup"><span data-stu-id="1fecd-140">In situations like this, if there is an existing format we can reuse, then we may not have toowrite our own parsing code.</span></span> <span data-ttu-id="1fecd-141">Вначале я считается с помощью hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) для отправки запросов и ответов HTTP.</span><span class="sxs-lookup"><span data-stu-id="1fecd-141">Initially I considered using hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="1fecd-142">Но этот формат оптимизирован для сохранения последовательности HTTP-запросов в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="1fecd-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="1fecd-143">Он содержит ряд обязательных элементов, которые добавлены излишней сложности для сценария hello передачи по сети hello сообщение hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="1fecd-143">It contained a number of mandatory elements that added unnecessary complexity for hello scenario of passing hello HTTP message over hello wire.</span></span>  

<span data-ttu-id="1fecd-144">Альтернативным вариантом был toouse hello `application/http` тип мультимедиа, как описано в спецификации hello HTTP [RFC 7230](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="1fecd-144">An alternative option was toouse hello `application/http` media type as described in hello HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="1fecd-145">Этот тип мультимедиа использует hello точно в том же формате, то есть используется tooactually отправки HTTP-сообщений по сети hello, но все сообщение hello может быть помещен в тексте hello другой HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="1fecd-145">This media type uses hello exact same format that is used tooactually send HTTP messages over hello wire, but hello entire message can be put in hello body of another HTTP request.</span></span> <span data-ttu-id="1fecd-146">В нашем случае просто будет текст hello toouse как нашей tooEvent toosend сообщение концентраторов.</span><span class="sxs-lookup"><span data-stu-id="1fecd-146">In our case we are just going toouse hello body as our message toosend tooEvent Hubs.</span></span> <span data-ttu-id="1fecd-147">К счастью, имеется средство синтаксического анализа, который существует в [клиента Microsoft ASP.NET Web API 2.2](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) библиотеки, которые можно проанализировать этот формат и преобразовать его в машинный код hello `HttpRequestMessage` и `HttpResponseMessage` объектов.</span><span class="sxs-lookup"><span data-stu-id="1fecd-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into hello native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="1fecd-148">возможности toocreate toobe это сообщение, нам нужно tootake преимуществами C# на основе [выражения политики](https://msdn.microsoft.com/library/azure/dn910913.aspx) в службе управления API Azure.</span><span class="sxs-lookup"><span data-stu-id="1fecd-148">toobe able toocreate this message we need tootake advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="1fecd-149">Вот hello политики, который отправляет tooAzure сообщения запроса HTTP концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="1fecd-149">Here is hello policy which sends a HTTP request message tooAzure Event Hubs.</span></span>

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

### <a name="policy-declaration"></a><span data-ttu-id="1fecd-150">Объявление политики</span><span class="sxs-lookup"><span data-stu-id="1fecd-150">Policy declaration</span></span>
<span data-ttu-id="1fecd-151">Некоторые элементы этого выражения политики следует разъяснить.</span><span class="sxs-lookup"><span data-stu-id="1fecd-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="1fecd-152">политика журнала к eventhub Hello имеет атрибут с именем средства ведения журнала идентификатор, который ссылается toohello имя средства ведения журнала, созданного в службе управления API hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-152">hello log-to-eventhub policy has an attribute called logger-id which refers toohello name of logger that has been created within hello API Management service.</span></span> <span data-ttu-id="1fecd-153">Здравствуйте, подробные сведения о как toosetup средство ведения журнала концентратора событий в службе управления API hello можно найти в документе hello [как tooAzure toolog событий концентраторов событий в Azure API Management](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="1fecd-153">hello details of how toosetup an Event Hub logger in hello API Management service can be found in hello document [How toolog events tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="1fecd-154">второй атрибут Hello имеет дополнительный параметр, который указывает, что концентраторы событий сообщений hello toostore секции в.</span><span class="sxs-lookup"><span data-stu-id="1fecd-154">hello second attribute is an optional parameter that instructs Event Hubs which partition toostore hello message in.</span></span> <span data-ttu-id="1fecd-155">Концентраторы событий используйте scalabilty tooenable секций и требуется как минимум два.</span><span class="sxs-lookup"><span data-stu-id="1fecd-155">Event Hubs use partitions tooenable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="1fecd-156">упорядоченную доставку сообщений Hello гарантируется только внутри секции.</span><span class="sxs-lookup"><span data-stu-id="1fecd-156">hello ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="1fecd-157">Если мы не загружался концентратора событий, в какой секции tooplace приветственное сообщение, он будет использовать алгоритм циклического toodistribute hello нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1fecd-157">If we do not instruct Event Hub in which partition tooplace hello message, it will use a round-robin algorithm toodistribute hello load.</span></span> <span data-ttu-id="1fecd-158">Однако, может вызвать некоторые из наших toobe сообщений, обработанных не по порядку.</span><span class="sxs-lookup"><span data-stu-id="1fecd-158">However, that may cause some of our messages toobe processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="1fecd-159">Разделы</span><span class="sxs-lookup"><span data-stu-id="1fecd-159">Partitions</span></span>
<span data-ttu-id="1fecd-160">tooensure нашей сообщения доставляются по порядку tooconsumers и воспользоваться возможностью распределения нагрузки hello секций, я выбрал toosend HTTP запроса сообщения tooone и HTTP ответа сообщения tooa второй разделов.</span><span class="sxs-lookup"><span data-stu-id="1fecd-160">tooensure our messages are delivered tooconsumers in order and take advantage of hello load distribution capability of partitions, I chose toosend HTTP request messages tooone partition and HTTP response messages tooa second partition.</span></span> <span data-ttu-id="1fecd-161">Это обеспечит равномерное распределение нагрузки и одновременно гарантирует, что все запросы и ответы будут обрабатываться по порядку.</span><span class="sxs-lookup"><span data-stu-id="1fecd-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="1fecd-162">Существует возможность toobe ответа, перед hello соответствующего запроса, но как это не проблема, как у нас есть tooresponses запрашивает другой механизм корреляции, и мы знаем, что запросы всегда находятся перед ответов.</span><span class="sxs-lookup"><span data-stu-id="1fecd-162">It is possible for a response toobe consumed before hello corresponding request, but as that is not a problem as we have a different mechanism for correlating requests tooresponses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="1fecd-163">Полезные данные HTTP</span><span class="sxs-lookup"><span data-stu-id="1fecd-163">HTTP payloads</span></span>
<span data-ttu-id="1fecd-164">После построения hello `requestLine` мы проверяем toosee, если hello текст запроса должен быть усечен.</span><span class="sxs-lookup"><span data-stu-id="1fecd-164">After building hello `requestLine` we check toosee if hello request body should be truncated.</span></span> <span data-ttu-id="1fecd-165">текст запроса Hello — усеченное tooonly 1024.</span><span class="sxs-lookup"><span data-stu-id="1fecd-165">hello request body is truncated tooonly 1024.</span></span> <span data-ttu-id="1fecd-166">Его можно увеличить, однако отдельные сообщения концентратора событий являются ограниченные too256KB, поэтому вполне вероятно, что некоторые сообщения HTTP институтов будет не помещаются в одно сообщение.</span><span class="sxs-lookup"><span data-stu-id="1fecd-166">This could be increased, however individual Event Hub messages are limited too256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="1fecd-167">При выполнении ведение журнала и аналитика значительный объем сведения могут быть производными от только что hello строка запроса HTTP и заголовки.</span><span class="sxs-lookup"><span data-stu-id="1fecd-167">When doing logging and analytics a significant amount of information can be derived from just hello HTTP request line and headers.</span></span> <span data-ttu-id="1fecd-168">Также много запросов API возвращает только небольших тел и поэтому потери hello информативные путем усечения больших фрагментов довольно минимален сравнения снижению toohello передачи, обработки и хранения обходится tookeep все содержимое тела.</span><span class="sxs-lookup"><span data-stu-id="1fecd-168">Also, many API requests only return small bodies and so hello loss of information value by truncating large bodies is fairly minimal in comparison toohello reduction in transfer, processing and storage costs tookeep all body contents.</span></span> <span data-ttu-id="1fecd-169">Последнее замечание об обработка текста hello является необходимость toopass `true` toohello как<string>метод () так, как мы читаете hello содержимое тела, однако указано также требуется hello API внутреннего сервера toobe может tooread hello текста.</span><span class="sxs-lookup"><span data-stu-id="1fecd-169">One final note about processing hello body is that we need toopass `true` toohello As<string>() method because we are reading hello body contents, but was also want hello backend API toobe able tooread hello body.</span></span> <span data-ttu-id="1fecd-170">Передав значение true, toothis метод мы вызвать toobe текст hello в буфер, чтобы она могла считывать во второй раз.</span><span class="sxs-lookup"><span data-stu-id="1fecd-170">By passing true toothis method we cause hello body toobe buffered so that it can be read a second time.</span></span> <span data-ttu-id="1fecd-171">Это важные toobe помнить при наличии API-Интерфейсы, не передачи файлов очень большого объема и использует долго опрашивающего.</span><span class="sxs-lookup"><span data-stu-id="1fecd-171">This is important toobe aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="1fecd-172">В этих случаях было бы наиболее tooavoid чтения текста hello вообще.</span><span class="sxs-lookup"><span data-stu-id="1fecd-172">In these cases it would be best tooavoid reading hello body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="1fecd-173">HTTP-заголовки</span><span class="sxs-lookup"><span data-stu-id="1fecd-173">HTTP headers</span></span>
<span data-ttu-id="1fecd-174">HTTP-заголовков, можно просто передать по в формат сообщений hello в формате пары ключ значение.</span><span class="sxs-lookup"><span data-stu-id="1fecd-174">HTTP Headers can be simply transferred over into hello message format in a simple key/value pair format.</span></span> <span data-ttu-id="1fecd-175">Мы выбрали toostrip безопасность, определенных полей, tooavoid без необходимости утечка учетные данные.</span><span class="sxs-lookup"><span data-stu-id="1fecd-175">We have chosen toostrip out certain security sensitive fields, tooavoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="1fecd-176">Для анализа ключи API и другие учетные данные, скорее всего, не потребуются.</span><span class="sxs-lookup"><span data-stu-id="1fecd-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="1fecd-177">Если мы toodo анализа для пользователя hello и конкретного продукта hello они используют, а затем, удалось получить из hello `context` и добавить это сообщение toohello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-177">If we wish toodo analysis on hello user and hello particular product they are using then we could get that from hello `context` object and add that toohello message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="1fecd-178">Метаданные сообщения</span><span class="sxs-lookup"><span data-stu-id="1fecd-178">Message Metadata</span></span>
<span data-ttu-id="1fecd-179">При создании концентратора событий toohello toosend полное сообщение hello, первая строка hello не фактически является частью hello `application/http` сообщения.</span><span class="sxs-lookup"><span data-stu-id="1fecd-179">When building hello complete message toosend toohello event hub, hello first line is not actually part of hello `application/http` message.</span></span> <span data-ttu-id="1fecd-180">Первая строка Hello это дополнительные метаданные, состоящий из ли сообщение hello — это сообщение запроса или ответа и идентификатора сообщения, используемые toocorrelate запрашивает tooresponses.</span><span class="sxs-lookup"><span data-stu-id="1fecd-180">hello first line is additional metadata consisting of whether hello message is a request or response message and a message id which is used toocorrelate requests tooresponses.</span></span> <span data-ttu-id="1fecd-181">Идентификатор сообщения Hello создается с помощью другой политики, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1fecd-181">hello message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="1fecd-182">Можно было создать сообщение запроса hello, сохраняется, переменная до hello ответ был возвращается и затем просто отправляется hello запроса и ответа в одном сообщении.</span><span class="sxs-lookup"><span data-stu-id="1fecd-182">We could have created hello request message, stored that in a variable until hello response was returned and then simply sent hello request and response as a single message.</span></span> <span data-ttu-id="1fecd-183">Тем не менее, отправляя hello запроса и ответа независимо друг от друга и с помощью toocorrelate идентификатор сообщения hello два, получить более гибко размер сообщения hello, hello возможность tootake преимуществами нескольких секций одновременным сохраняя порядок сообщений и hello запрос появляется раньше, в нашей информационной панели ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="1fecd-183">However, by sending hello request and response independently and using a message id toocorrelate hello two, we get a bit more flexibility in hello message size, hello ability tootake advantage of multiple partitions whilst maintaining message order and hello request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="1fecd-184">Также возможны некоторые сценарии где допустимый ответ никогда не отправляется концентратора событий toohello, возможно из-за tooa запрос Неустранимая ошибка в службе управления API hello, но мы по-прежнему будет иметь запись запроса hello.</span><span class="sxs-lookup"><span data-stu-id="1fecd-184">There also may be some scenarios where a valid response is never sent toohello event hub, possibly due tooa fatal request error in hello API Management service, but we still will have a record of hello request.</span></span>

<span data-ttu-id="1fecd-185">сообщение Hello политики toosend hello ответа HTTP выглядит аналогично toohello запрос и завершить hello так конфигурация политики выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1fecd-185">hello policy toosend hello response HTTP message looks very similar toohello request and so hello complete policy configuration looks like this:</span></span>

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

<span data-ttu-id="1fecd-186">Hello `set-variable` политика создает значение, которое доступно для обоих hello `log-to-eventhub` политики в hello `<inbound>` раздел и hello `<outbound>` раздела.</span><span class="sxs-lookup"><span data-stu-id="1fecd-186">hello `set-variable` policy creates a value that is accessible by both hello `log-to-eventhub` policy in hello `<inbound>` section and hello `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="1fecd-187">Получение событий от концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="1fecd-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="1fecd-188">Будут получены события из концентратора событий Azure с помощью hello [протокола AMQP](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="1fecd-188">Events from Azure Event Hub are received using hello [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="1fecd-189">Hello шину обслуживания Microsoft team были сделаны клиента использование событий проще hello toomake доступных библиотек.</span><span class="sxs-lookup"><span data-stu-id="1fecd-189">hello Microsoft Service Bus team have made client libraries available toomake hello consuming events easier.</span></span> <span data-ttu-id="1fecd-190">Существует два различных подхода поддерживается, создается один *прямой потребитель* и использует другие hello hello `EventProcessorHost` класса.</span><span class="sxs-lookup"><span data-stu-id="1fecd-190">There are two different approaches supported, one is being a *Direct Consumer* and hello other is using hello `EventProcessorHost` class.</span></span> <span data-ttu-id="1fecd-191">Примеры этих двух подходов можно найти в hello [руководство по программированию концентраторов событий](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="1fecd-191">Examples of these two approaches can be found in hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="1fecd-192">является краткой версией Hello hello различия, `Direct Consumer` предоставляет полный контроль и hello `EventProcessorHost` не часть работы направляющее hello для вас но делает определенные предположения о том, как будет обрабатывать эти события.</span><span class="sxs-lookup"><span data-stu-id="1fecd-192">hello short version of hello differences is, `Direct Consumer` gives you complete control and hello `EventProcessorHost` does some of hello plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="1fecd-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="1fecd-193">EventProcessorHost</span></span>
<span data-ttu-id="1fecd-194">В этом примере мы будем использовать hello `EventProcessorHost` для простоты, однако он может не hello наилучшим образом подходят для этой конкретной ситуации.</span><span class="sxs-lookup"><span data-stu-id="1fecd-194">In this sample, we will use hello `EventProcessorHost` for simplicity, however it may not hello best choice for this particular scenario.</span></span> <span data-ttu-id="1fecd-195">`EventProcessorHost`Здравствуйте непростая работа убедиться, что у вас нет tooworry о работе с потоками проблемы в рамках конкретного процессора класса событий.</span><span class="sxs-lookup"><span data-stu-id="1fecd-195">`EventProcessorHost` does hello hard work of making sure you don't have tooworry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="1fecd-196">Однако в нашем случае мы просто преобразование формата tooanother сообщение hello и передавая tooanother службы, с помощью асинхронного метода.</span><span class="sxs-lookup"><span data-stu-id="1fecd-196">However, in our scenario, we are simply converting hello message tooanother format and passing it along tooanother service using an async method.</span></span> <span data-ttu-id="1fecd-197">У нас нет необходимости обновлять общее состояние, и нет риска возникновения проблем с потоками.</span><span class="sxs-lookup"><span data-stu-id="1fecd-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="1fecd-198">В большинстве случаев `EventProcessorHost` , скорее всего, является лучшим выбором hello и это определенно hello простой вариант.</span><span class="sxs-lookup"><span data-stu-id="1fecd-198">For most scenarios, `EventProcessorHost` is probably hello best choice and it is certainly hello easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="1fecd-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="1fecd-199">IEventProcessor</span></span>
<span data-ttu-id="1fecd-200">Центральное понятие Hello при использовании `EventProcessorHost` toocreate является реализация hello `IEventProcessor` интерфейс, который содержит метод hello `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="1fecd-200">hello central concept when using `EventProcessorHost` is toocreate a an implementation of hello `IEventProcessor` interface which contains hello method `ProcessEventAsync`.</span></span> <span data-ttu-id="1fecd-201">Hello суть этого метода показан ниже:</span><span class="sxs-lookup"><span data-stu-id="1fecd-201">hello essence of that method is shown here:</span></span>

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

<span data-ttu-id="1fecd-202">Список объектов EventData передаются в метод hello и мы перебора этого списка.</span><span class="sxs-lookup"><span data-stu-id="1fecd-202">A list of EventData objects are passed into hello method and we iterate over that list.</span></span> <span data-ttu-id="1fecd-203">байт Hello каждого метода синтаксического анализа в объект HttpMessage и этот объект передается экземпляр tooan IHttpMessageProcessor.</span><span class="sxs-lookup"><span data-stu-id="1fecd-203">hello bytes of each method are parsed into a HttpMessage object and that object is passed tooan instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="1fecd-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="1fecd-204">HttpMessage</span></span>
<span data-ttu-id="1fecd-205">Hello `HttpMessage` экземпляр содержит три элемента данных:</span><span class="sxs-lookup"><span data-stu-id="1fecd-205">hello `HttpMessage` instance contains three pieces of data:</span></span>

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

<span data-ttu-id="1fecd-206">Hello `HttpMessage` экземпляр содержит `MessageId` идентификатор GUID, который позволяет нам запрос hello HTTP tooconnect toohello соответствующие HTTP-ответа и логическое значение, которое определяет, если hello содержит экземпляр HttpRequestMessage и HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="1fecd-206">hello `HttpMessage` instance contains a `MessageId` GUID that allows us tooconnect hello HTTP request toohello corresponding HTTP response and a boolean value that identifies if hello object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="1fecd-207">С помощью hello, встроенных в классы HTTP из `System.Net.Http`, я был может tootake преимуществами hello `application/http` синтаксического анализа кода, который включен в `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="1fecd-207">By using hello built in HTTP classes from `System.Net.Http`, I was able tootake advantage of hello `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="1fecd-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="1fecd-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="1fecd-209">Hello `HttpMessage` tooimplementation объекта затем передается экземпляр `IHttpMessageProcessor` которого является интерфейсом, я создал toodecouple hello получение и интерпретация hello события из концентратора событий Azure и hello фактического его обработки.</span><span class="sxs-lookup"><span data-stu-id="1fecd-209">hello `HttpMessage` instance is then forwarded tooimplementation of `IHttpMessageProcessor` which is an interface I created toodecouple hello receiving and interpretation of hello event from Azure Event Hub and hello actual processing of it.</span></span>

## <a name="forwarding-hello-http-message"></a><span data-ttu-id="1fecd-210">Пересылка hello HTTP-сообщения</span><span class="sxs-lookup"><span data-stu-id="1fecd-210">Forwarding hello HTTP message</span></span>
<span data-ttu-id="1fecd-211">Для этого примера я решил было бы интересно toopush hello HTTP-запроса по слишком[Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="1fecd-211">For this sample, I decided it would be interesting toopush hello HTTP Request over too[Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="1fecd-212">Runscope — это облачная служба, предназначенная для отладки, регистрации и мониторинга HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="1fecd-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="1fecd-213">Они имеют уровень free, поэтому просто tootry и позволяет нам toosee hello HTTP-запросов при передаче в режиме реального времени через наша служба управления API.</span><span class="sxs-lookup"><span data-stu-id="1fecd-213">They have a free tier, so it is easy tootry and it allows us toosee hello HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="1fecd-214">Hello `IHttpMessageProcessor` реализация выглядит следующим образом,</span><span class="sxs-lookup"><span data-stu-id="1fecd-214">hello `IHttpMessageProcessor` implementation looks like this,</span></span>

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

<span data-ttu-id="1fecd-215">Я был преимуществами может tootake [существующую библиотеку клиента для Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) , делает его легко toopush `HttpRequestMessage` и `HttpResponseMessage` экземпляров вверх в их службу.</span><span class="sxs-lookup"><span data-stu-id="1fecd-215">I was able tootake advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy toopush `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="1fecd-216">В порядке tooaccess hello Runscope API, вам потребуется учетная запись и ключ API.</span><span class="sxs-lookup"><span data-stu-id="1fecd-216">In order tooaccess hello Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="1fecd-217">Инструкции по получению ключа API можно найти в hello [tooAccess создание приложений Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) видеоролике.</span><span class="sxs-lookup"><span data-stu-id="1fecd-217">Instructions for getting an API key can be found in hello [Creating Applications tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="1fecd-218">Полный пример</span><span class="sxs-lookup"><span data-stu-id="1fecd-218">Complete sample</span></span>
<span data-ttu-id="1fecd-219">Hello [исходный код](https://github.com/darrelmiller/ApimEventProcessor) и тесты для образца hello на GitHub.</span><span class="sxs-lookup"><span data-stu-id="1fecd-219">hello [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for hello sample are on GitHub.</span></span> <span data-ttu-id="1fecd-220">Вам потребуется [службы управления API](api-management-get-started.md), [подключенного концентратора событий](api-management-howto-log-event-hubs.md)и [учетной записи хранилища](../storage/common/storage-create-storage-account.md) образец hello toorun самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="1fecd-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) toorun hello sample for yourself.</span></span>   

<span data-ttu-id="1fecd-221">Hello образец является просто простое консольное приложение, которое прослушивает события из концентратора событий, преобразует их в `HttpRequestMessage` и `HttpResponseMessage` объектов и затем перенаправляет их toohello Runscope API.</span><span class="sxs-lookup"><span data-stu-id="1fecd-221">hello sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on toohello Runscope API.</span></span>

<span data-ttu-id="1fecd-222">В следующих анимированного изображения hello появится запрос сделан tooan API в hello портал разработчиков, hello консольного приложения отображение hello полученное сообщение, обработки и пересылки и Здравствуйте, запросов и ответов, отображаются в hello Runscope трафика Инспектор.</span><span class="sxs-lookup"><span data-stu-id="1fecd-222">In hello following animated image, you can see a request being made tooan API in hello Developer Portal, hello Console application showing hello message being received, processed and forwarded and then hello request and response showing up in hello Runscope Traffic inspector.</span></span>

![Демонстрация пересылку tooRunscope запроса](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="1fecd-224">Сводка</span><span class="sxs-lookup"><span data-stu-id="1fecd-224">Summary</span></span>
<span data-ttu-id="1fecd-225">Служба управления API Azure предоставляет трафика hello HTTP toocapture идеальное место пути tooand из собственные интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="1fecd-225">Azure API Management service provides an ideal place toocapture hello HTTP traffic travelling tooand from your APIs.</span></span> <span data-ttu-id="1fecd-226">Концентраторы событий Azure — это высокомасштабируемое недорогое решение, которое собирает информацию о трафике и передает ее в системы дополнительной обработки для регистрации, мониторинга и сложного анализа.</span><span class="sxs-lookup"><span data-stu-id="1fecd-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="1fecd-227">Подключение трафика стороны too3rd контроль различных систем, как Runscope является простым, как несколько десятков строк кода.</span><span class="sxs-lookup"><span data-stu-id="1fecd-227">Connecting too3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fecd-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1fecd-228">Next steps</span></span>
* <span data-ttu-id="1fecd-229">Дополнительная информация о концентраторах событий Azure</span><span class="sxs-lookup"><span data-stu-id="1fecd-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="1fecd-230">Приступая к работе с концентраторами событий Azure</span><span class="sxs-lookup"><span data-stu-id="1fecd-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="1fecd-231">Прием сообщений через EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="1fecd-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="1fecd-232">Руководство по программированию концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="1fecd-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="1fecd-233">Дополнительные сведения об интеграции службы управления API и концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="1fecd-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="1fecd-234">Как tooAzure toolog событий концентраторов событий в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="1fecd-234">How toolog events tooAzure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="1fecd-235">Справочник по сущности "Средство ведения журнала"</span><span class="sxs-lookup"><span data-stu-id="1fecd-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="1fecd-236">Справочник по политике регистрации в концентраторе событий</span><span class="sxs-lookup"><span data-stu-id="1fecd-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
