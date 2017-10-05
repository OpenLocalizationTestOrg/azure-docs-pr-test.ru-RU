---
title: "Мониторинг интерфейсов API с помощью службы управления API Azure, концентраторов событий и Runscope | Документация Майкрософт"
description: "Пример приложения, демонстрирующий политику регистрации в концентраторе событий путем подключения службы управления API Azure, концентраторов событий Azure и службы Runscope для регистрации и мониторинга HTTP-запросов"
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
ms.openlocfilehash: 70ee752c5639c90f77dde104ce85eec0a1062300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="29fc7-103">Мониторинг API-интерфейсов с помощью службы управления API Azure, концентраторов событий и Runscope</span><span class="sxs-lookup"><span data-stu-id="29fc7-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="29fc7-104">[Служба управления API](api-management-key-concepts.md) предоставляет множество возможностей для улучшения обработки HTTP-запросов, адресованных API-интерфейсу HTTP.</span><span class="sxs-lookup"><span data-stu-id="29fc7-104">The [API Management service](api-management-key-concepts.md) provides many capabilities to enhance the processing of HTTP requests sent to your HTTP API.</span></span> <span data-ttu-id="29fc7-105">Однако запросы и ответы существуют очень недолго.</span><span class="sxs-lookup"><span data-stu-id="29fc7-105">However, the existence of the requests and responses are transient.</span></span> <span data-ttu-id="29fc7-106">Созданный запрос проходит через службу управления API на серверный API вашей службы.</span><span class="sxs-lookup"><span data-stu-id="29fc7-106">The request is made and it flows through the API Management service to your backend API.</span></span> <span data-ttu-id="29fc7-107">API обрабатывает запрос и отправляет ответ обратно потребителю API.</span><span class="sxs-lookup"><span data-stu-id="29fc7-107">Your API processes the request and a response flows back through to the API consumer.</span></span> <span data-ttu-id="29fc7-108">Служба управления API частично сохраняет важные статистические данные об API-интерфейсах и отображает их на панели мониторинга портала издателя, но вся остальная информация теряется безвозвратно.</span><span class="sxs-lookup"><span data-stu-id="29fc7-108">The API Management service keeps some important statistics about the APIs for display in the Publisher portal dashboard, but beyond that, the details are gone.</span></span>

<span data-ttu-id="29fc7-109">Вы можете использовать [политику](api-management-howto-policies.md) [регистрации в концентраторах событий](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub), чтобы служба управления API отправляла любые нужные сведения о запросе и ответе в [концентратор событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="29fc7-109">By using the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in the API Management service you can send any details from the request and response to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="29fc7-110">Существует ряд причин для создания событий из сообщений HTTP, отправляемых в API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="29fc7-110">There are a variety of reasons why you may want to generate events from HTTP messages being sent to your APIs.</span></span> <span data-ttu-id="29fc7-111">В частности, это происходит при создании журнала аудита обновлений, анализе использования, оповещении об исключениях или интеграции служб сторонних поставщиков.</span><span class="sxs-lookup"><span data-stu-id="29fc7-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="29fc7-112">В этой статье мы покажем, как зафиксировать полное сообщение о запросе и ответе HTTP, как отправить это сообщение в концентратор событий, а затем передать его в сторонние службы, которые выполняют ведение журналов и мониторинг HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="29fc7-112">This article demonstrates how to capture the entire HTTP request and response message, send it to an Event Hub and then relay that message to a third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="29fc7-113">Почему лучше отправлять сообщения из службы управления API?</span><span class="sxs-lookup"><span data-stu-id="29fc7-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="29fc7-114">Конечно, можно создать ПО промежуточного слоя HTTP, которое может подключаться к платформам HTTP API для фиксации HTTP-запросов и ответов и их передачи в системы ведения журналов и мониторинга.</span><span class="sxs-lookup"><span data-stu-id="29fc7-114">It is possible to write HTTP middleware that can plug into HTTP API frameworks to capture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="29fc7-115">Но у этого подхода есть недостатки: ПО промежуточного слоя HTTP должно интегрироваться с серверной частью API и соответствовать платформе, на которой размещен API-интерфейс.</span><span class="sxs-lookup"><span data-stu-id="29fc7-115">The downside to this approach is the HTTP middleware needs to be integrated into the backend API and must match the platform of the API.</span></span> <span data-ttu-id="29fc7-116">Если используется несколько API, ПО промежуточного слоя следует развернуть на каждом из них.</span><span class="sxs-lookup"><span data-stu-id="29fc7-116">If there are multiple APIs then each one must deploy the middleware.</span></span> <span data-ttu-id="29fc7-117">Зачастую серверный API-интерфейс невозможно обновить по той или иной причине.</span><span class="sxs-lookup"><span data-stu-id="29fc7-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="29fc7-118">Служба управления API Azure предоставляет вам централизованное решение для интеграции с инфраструктурой ведения журналов, не зависящее от платформы.</span><span class="sxs-lookup"><span data-stu-id="29fc7-118">Using the Azure API Management service to integrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="29fc7-119">Также оно обеспечит хорошую масштабируемость, в том числе благодаря возможностям [георепликации](api-management-howto-deploy-multi-region.md) службы управления API Azure.</span><span class="sxs-lookup"><span data-stu-id="29fc7-119">It is also scalable, in part due to the [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-to-an-azure-event-hub"></a><span data-ttu-id="29fc7-120">Почему лучше отправлять сообщения в концентратор событий Azure?</span><span class="sxs-lookup"><span data-stu-id="29fc7-120">Why send to an Azure Event Hub?</span></span>
<span data-ttu-id="29fc7-121">Вполне логичным будет вопрос, почему создаваемая политика должна использовать концентраторы событий Azure.</span><span class="sxs-lookup"><span data-stu-id="29fc7-121">It is a reasonable to ask, why create a policy that is specific to Azure Event Hubs?</span></span> <span data-ttu-id="29fc7-122">Есть много различных служб, в которых можно регистрировать запросы.</span><span class="sxs-lookup"><span data-stu-id="29fc7-122">There are many different places where I might want to log my requests.</span></span> <span data-ttu-id="29fc7-123">Что мешает отправлять запросы сразу конечному получателю?</span><span class="sxs-lookup"><span data-stu-id="29fc7-123">Why not just send the requests directly to the final destination?</span></span>  <span data-ttu-id="29fc7-124">Такой вариант возможен.</span><span class="sxs-lookup"><span data-stu-id="29fc7-124">That is an option.</span></span> <span data-ttu-id="29fc7-125">Однако при отправке запросов на регистрацию из службы управления API следует учитывать влияние сообщений журнала на производительность API.</span><span class="sxs-lookup"><span data-stu-id="29fc7-125">However, when making logging requests from an API management service, it is necessary to consider how logging messages will impact the performance of the API.</span></span> <span data-ttu-id="29fc7-126">Постепенное увеличение нагрузки можно компенсировать, увеличив количество доступных экземпляров компонентов системы или используя георепликацию.</span><span class="sxs-lookup"><span data-stu-id="29fc7-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="29fc7-127">Но короткие пиковые скачки трафика могут привести к существенной задержке запросов, если при увеличении нагрузки замедляется обработка запросов к инфраструктуре ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="29fc7-127">However, short spikes in traffic can cause requests to be significantly delayed if requests to logging infrastructure start to slow under load.</span></span>

<span data-ttu-id="29fc7-128">Концентраторы событий Azure рассчитаны на огромные объемы входящих данных. Их пропускная способность существенно превышает возможности большинства API-процессов по обработке HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="29fc7-128">The Azure Event Hubs is designed to ingress huge volumes of data, with capacity for dealing with a far higher number of events than the number of HTTP requests most APIs process.</span></span> <span data-ttu-id="29fc7-129">Концентратор событий выполняет роль сложного буфера между службой управления API и инфраструктурой, которая хранит и обрабатывает сообщения.</span><span class="sxs-lookup"><span data-stu-id="29fc7-129">The Event Hub acts as a kind of sophisticated buffer between your API management service and the infrastructure that will store and process the messages.</span></span> <span data-ttu-id="29fc7-130">Это гарантирует, что ограничения инфраструктуры ведения журналов не повлияют на производительность API.</span><span class="sxs-lookup"><span data-stu-id="29fc7-130">This ensures that your API performance will not suffer due to the logging infrastructure.</span></span>  

<span data-ttu-id="29fc7-131">Данные, переданные в концентратор событий, сохраняются там и ожидают обработки со стороны потребителей концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="29fc7-131">Once the data has been passed to an Event Hub it is persisted and will wait for Event Hub consumers to process it.</span></span> <span data-ttu-id="29fc7-132">Для концентратора событий не имеет значения, как будет обработано сообщение, — он просто гарантирует успешную доставку сообщения.</span><span class="sxs-lookup"><span data-stu-id="29fc7-132">The Event Hub does not care how it will be processed, it just cares about making sure the message will be successfully delivered.</span></span>     

<span data-ttu-id="29fc7-133">Концентраторы событий могут выполнять потоковую передачу событий сразу нескольким группам потребителей.</span><span class="sxs-lookup"><span data-stu-id="29fc7-133">Event Hubs have the ability to stream events to multiple consumer groups.</span></span> <span data-ttu-id="29fc7-134">Это позволяет обрабатывать события совершенно различными системами.</span><span class="sxs-lookup"><span data-stu-id="29fc7-134">This allows events to be processed by completely different systems.</span></span> <span data-ttu-id="29fc7-135">Благодаря этому можно реализовать множество сценариев интеграции без увеличения задержек на обработку запросов в службе управления API. Службе в любом случае достаточно создать только одно событие.</span><span class="sxs-lookup"><span data-stu-id="29fc7-135">This enables supporting many integration scenarios without putting addition delays on the processing of the API request within the API Management service as only one event needs to be generated.</span></span>

## <a name="a-policy-to-send-applicationhttp-messages"></a><span data-ttu-id="29fc7-136">Политика отправки сообщений приложений и сообщений HTTP</span><span class="sxs-lookup"><span data-stu-id="29fc7-136">A policy to send application/http messages</span></span>
<span data-ttu-id="29fc7-137">Концентратор событий принимает данные события в виде простой строки</span><span class="sxs-lookup"><span data-stu-id="29fc7-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="29fc7-138">с произвольным содержимым.</span><span class="sxs-lookup"><span data-stu-id="29fc7-138">The contents of that string are completely up to you.</span></span> <span data-ttu-id="29fc7-139">Чтобы сформировать HTTP-запрос и отправить его в концентраторы событий, следует дополнить строку информацией о запросе или ответе.</span><span class="sxs-lookup"><span data-stu-id="29fc7-139">To be able to package up an HTTP request and send it off to Event Hubs we need to format the string with the request or response information.</span></span> <span data-ttu-id="29fc7-140">В таких случаях можно повторно использовать уже существующий формат, чтобы не писать новый код для синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="29fc7-140">In situations like this, if there is an existing format we can reuse, then we may not have to write our own parsing code.</span></span> <span data-ttu-id="29fc7-141">Сначала мне показалось, что для отправки HTTP-запросов и ответов подойдет формат [HAR](http://www.softwareishard.com/blog/har-12-spec/).</span><span class="sxs-lookup"><span data-stu-id="29fc7-141">Initially I considered using the [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="29fc7-142">Но этот формат оптимизирован для сохранения последовательности HTTP-запросов в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="29fc7-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="29fc7-143">Он содержит несколько обязательных элементов, которые создают излишние сложности при передаче HTTP-сообщения по сети.</span><span class="sxs-lookup"><span data-stu-id="29fc7-143">It contained a number of mandatory elements that added unnecessary complexity for the scenario of passing the HTTP message over the wire.</span></span>  

<span data-ttu-id="29fc7-144">Еще один вариант — тип носителя `application/http` , описанный в спецификации HTTP [RFC 7230](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="29fc7-144">An alternative option was to use the `application/http` media type as described in the HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="29fc7-145">Этот тип носителя имеет точно такой же формат, как и обычные HTTP-сообщения, отправляемые по сети, но позволяет разместить сообщение целиком в тексте другого HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="29fc7-145">This media type uses the exact same format that is used to actually send HTTP messages over the wire, but the entire message can be put in the body of another HTTP request.</span></span> <span data-ttu-id="29fc7-146">В нашем случае в тексте запроса мы и будем отправлять сообщение в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="29fc7-146">In our case we are just going to use the body as our message to send to Event Hubs.</span></span> <span data-ttu-id="29fc7-147">В библиотеках [клиента Microsoft ASP.NET Web API 2.2](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) уже есть средство синтаксического анализа для этого формата, которое преобразует его в собственные объекты `HttpRequestMessage` и `HttpResponseMessage`.</span><span class="sxs-lookup"><span data-stu-id="29fc7-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into the native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="29fc7-148">Чтобы создать такое сообщение, следует воспользоваться [выражениями политики](https://msdn.microsoft.com/library/azure/dn910913.aspx) службы управления API Azure, которые используют синтаксис C#.</span><span class="sxs-lookup"><span data-stu-id="29fc7-148">To be able to create this message we need to take advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="29fc7-149">Приведенная ниже политика будет отправлять сообщение с HTTP-запросом в концентраторы событий Azure.</span><span class="sxs-lookup"><span data-stu-id="29fc7-149">Here is the policy which sends a HTTP request message to Azure Event Hubs.</span></span>

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

### <a name="policy-declaration"></a><span data-ttu-id="29fc7-150">Объявление политики</span><span class="sxs-lookup"><span data-stu-id="29fc7-150">Policy declaration</span></span>
<span data-ttu-id="29fc7-151">Некоторые элементы этого выражения политики следует разъяснить.</span><span class="sxs-lookup"><span data-stu-id="29fc7-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="29fc7-152">Политика регистрации в концентраторе событий имеет атрибут logger-id, который обозначает средство ведения журнала, созданное в службе управления API.</span><span class="sxs-lookup"><span data-stu-id="29fc7-152">The log-to-eventhub policy has an attribute called logger-id which refers to the name of logger that has been created within the API Management service.</span></span> <span data-ttu-id="29fc7-153">Подробные сведения о том, как в службе управления API настроить средство ведения журналов в концентраторах событий, можно найти в документе [Как регистрировать события в концентраторах событий Azure в службе управления Azure API](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="29fc7-153">The details of how to setup an Event Hub logger in the API Management service can be found in the document [How to log events to Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="29fc7-154">Второй (необязательный) атрибут сообщает концентраторам событий, в каком разделе нужно хранить сообщение.</span><span class="sxs-lookup"><span data-stu-id="29fc7-154">The second attribute is an optional parameter that instructs Event Hubs which partition to store the message in.</span></span> <span data-ttu-id="29fc7-155">Концентраторы событий используют разделы для поддержки масштабируемости. Для работы требуется не меньше двух разделов.</span><span class="sxs-lookup"><span data-stu-id="29fc7-155">Event Hubs use partitions to enable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="29fc7-156">Правильная последовательность доставки сообщений гарантируется только в пределах раздела.</span><span class="sxs-lookup"><span data-stu-id="29fc7-156">The ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="29fc7-157">Если не указать, в каком разделе концентратор событий должен разместить сообщение, он будет использовать их поочередно для равномерного распределения нагрузки.</span><span class="sxs-lookup"><span data-stu-id="29fc7-157">If we do not instruct Event Hub in which partition to place the message, it will use a round-robin algorithm to distribute the load.</span></span> <span data-ttu-id="29fc7-158">Но это может привести к тому, что сообщения будут обрабатываться не по порядку.</span><span class="sxs-lookup"><span data-stu-id="29fc7-158">However, that may cause some of our messages to be processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="29fc7-159">Разделы</span><span class="sxs-lookup"><span data-stu-id="29fc7-159">Partitions</span></span>
<span data-ttu-id="29fc7-160">Чтобы обеспечить правильный порядок доставки сообщений потребителям, не теряя при этом преимущества распределения нагрузки по разделам, я решил отправлять сообщения с HTTP-запросами в один раздел, а сообщения с ответами — в другой.</span><span class="sxs-lookup"><span data-stu-id="29fc7-160">To ensure our messages are delivered to consumers in order and take advantage of the load distribution capability of partitions, I chose to send HTTP request messages to one partition and HTTP response messages to a second partition.</span></span> <span data-ttu-id="29fc7-161">Это обеспечит равномерное распределение нагрузки и одновременно гарантирует, что все запросы и ответы будут обрабатываться по порядку.</span><span class="sxs-lookup"><span data-stu-id="29fc7-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="29fc7-162">Может случиться так, что ответ будет обработан раньше соответствующего запроса, но это не проблема. У нас есть отдельный механизм сопоставления запросов и ответов, и мы доподлинно знаем, что запросы всегда поступают раньше ответов.</span><span class="sxs-lookup"><span data-stu-id="29fc7-162">It is possible for a response to be consumed before the corresponding request, but as that is not a problem as we have a different mechanism for correlating requests to responses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="29fc7-163">Полезные данные HTTP</span><span class="sxs-lookup"><span data-stu-id="29fc7-163">HTTP payloads</span></span>
<span data-ttu-id="29fc7-164">После создания `requestLine` мы проверяем, нужно ли обрезать текст запроса.</span><span class="sxs-lookup"><span data-stu-id="29fc7-164">After building the `requestLine` we check to see if the request body should be truncated.</span></span> <span data-ttu-id="29fc7-165">Длина текста запроса ограничена 1024 символами.</span><span class="sxs-lookup"><span data-stu-id="29fc7-165">The request body is truncated to only 1024.</span></span> <span data-ttu-id="29fc7-166">Это значение можно увеличить, но размер одного сообщения для концентратора событий не может превышать 256 КБ, поэтому есть вероятность, что некоторые HTTP-запросы не поместятся в одно сообщение.</span><span class="sxs-lookup"><span data-stu-id="29fc7-166">This could be increased, however individual Event Hub messages are limited to 256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="29fc7-167">При ведении журнала и анализе значительный объем информации можно получить уже из строки запроса HTTP и заголовка.</span><span class="sxs-lookup"><span data-stu-id="29fc7-167">When doing logging and analytics a significant amount of information can be derived from just the HTTP request line and headers.</span></span> <span data-ttu-id="29fc7-168">Кроме того, многие запросы к API имеют сравнительно короткий текст. Таким образом, потеря полезной информации от усечения больших фрагментов будет пренебрежимо мала по сравнению с экономией затрат на передачу, обработку и хранение полного текста запроса.</span><span class="sxs-lookup"><span data-stu-id="29fc7-168">Also, many API requests only return small bodies and so the loss of information value by truncating large bodies is fairly minimal in comparison to the reduction in transfer, processing and storage costs to keep all body contents.</span></span> <span data-ttu-id="29fc7-169">И еще одно замечание об обработке текста запроса: в метод As<string>() необходимо передать значение `true`, так как мы можем читать текст запроса, но его должна прочитать еще и серверная часть API.</span><span class="sxs-lookup"><span data-stu-id="29fc7-169">One final note about processing the body is that we need to pass `true` to the As<string>() method because we are reading the body contents, but was also want the backend API to be able to read the body.</span></span> <span data-ttu-id="29fc7-170">Если передать в этот метод значение true, текст запроса сохраняется в буфере и может быть прочитан повторно.</span><span class="sxs-lookup"><span data-stu-id="29fc7-170">By passing true to this method we cause the body to be buffered so that it can be read a second time.</span></span> <span data-ttu-id="29fc7-171">Об этом особенно важно помнить, если ваш API передает файлы очень большого объема или долгие опросы.</span><span class="sxs-lookup"><span data-stu-id="29fc7-171">This is important to be aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="29fc7-172">В таких случаях лучше вовсе не читать текст запроса.</span><span class="sxs-lookup"><span data-stu-id="29fc7-172">In these cases it would be best to avoid reading the body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="29fc7-173">HTTP-заголовки</span><span class="sxs-lookup"><span data-stu-id="29fc7-173">HTTP headers</span></span>
<span data-ttu-id="29fc7-174">HTTP-заголовки можно поместить в сообщение в простом формате пар «ключ — значение».</span><span class="sxs-lookup"><span data-stu-id="29fc7-174">HTTP Headers can be simply transferred over into the message format in a simple key/value pair format.</span></span> <span data-ttu-id="29fc7-175">Мы решили исключить из обработки некоторые поля с секретной информацией, чтобы избежать утечки учетных данных.</span><span class="sxs-lookup"><span data-stu-id="29fc7-175">We have chosen to strip out certain security sensitive fields, to avoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="29fc7-176">Для анализа ключи API и другие учетные данные, скорее всего, не потребуются.</span><span class="sxs-lookup"><span data-stu-id="29fc7-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="29fc7-177">Если позднее нам нужно будет проанализировать работу конкретного пользователя или конкретного продукта, мы можем получить нужные данные из объекта `context` и добавить их в сообщение.</span><span class="sxs-lookup"><span data-stu-id="29fc7-177">If we wish to do analysis on the user and the particular product they are using then we could get that from the `context` object and add that to the message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="29fc7-178">Метаданные сообщения</span><span class="sxs-lookup"><span data-stu-id="29fc7-178">Message Metadata</span></span>
<span data-ttu-id="29fc7-179">В полном тексте сообщения, которое будет отправлено в концентратор событий, первая строка не является частью сообщения `application/http`.</span><span class="sxs-lookup"><span data-stu-id="29fc7-179">When building the complete message to send to the event hub, the first line is not actually part of the `application/http` message.</span></span> <span data-ttu-id="29fc7-180">В первой строке содержатся дополнительные метаданные. Они указывают, является ли сообщение запросом или ответом, и содержат идентификатор сообщения, по которому можно сопоставить запросы и ответы.</span><span class="sxs-lookup"><span data-stu-id="29fc7-180">The first line is additional metadata consisting of whether the message is a request or response message and a message id which is used to correlate requests to responses.</span></span> <span data-ttu-id="29fc7-181">Идентификатор сообщения создается с помощью другой политики, которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="29fc7-181">The message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="29fc7-182">Мы могли бы создать сообщение с запросом, сохранить его в переменной до получения ответа, а затем отправить запрос и ответ в одном сообщении.</span><span class="sxs-lookup"><span data-stu-id="29fc7-182">We could have created the request message, stored that in a variable until the response was returned and then simply sent the request and response as a single message.</span></span> <span data-ttu-id="29fc7-183">Но раздельная отправка запроса и ответа с общим идентификатором для их сопоставления позволяет варьировать размер сообщения. Также мы получаем возможность использовать преимущества нескольких разделов с сохранением порядка сообщений. Кроме того, так мы быстрее увидим поступивший запрос в панели мониторинга журналов.</span><span class="sxs-lookup"><span data-stu-id="29fc7-183">However, by sending the request and response independently and using a message id to correlate the two, we get a bit more flexibility in the message size, the ability to take advantage of multiple partitions whilst maintaining message order and the request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="29fc7-184">Также возможны ситуации, когда допустимый ответ вообще не отправляется в концентратор событий, например в случае неустранимой ошибки запроса в службе управления API. В этом случае мы по крайней мере будем иметь в журнале запись о запросе.</span><span class="sxs-lookup"><span data-stu-id="29fc7-184">There also may be some scenarios where a valid response is never sent to the event hub, possibly due to a fatal request error in the API Management service, but we still will have a record of the request.</span></span>

<span data-ttu-id="29fc7-185">Политика отправки HTTP-сообщения с ответом выглядит почти так же, как политика для запроса. Вот полная конфигурация этой политики:</span><span class="sxs-lookup"><span data-stu-id="29fc7-185">The policy to send the response HTTP message looks very similar to the request and so the complete policy configuration looks like this:</span></span>

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

<span data-ttu-id="29fc7-186">Политика `set-variable` создает значение, которое политика `log-to-eventhub` может использовать в разделах `<inbound>` и `<outbound>`.</span><span class="sxs-lookup"><span data-stu-id="29fc7-186">The `set-variable` policy creates a value that is accessible by both the `log-to-eventhub` policy in the `<inbound>` section and the `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="29fc7-187">Получение событий от концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="29fc7-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="29fc7-188">События из концентратора событий Azure поступают по [протоколу AMQP](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="29fc7-188">Events from Azure Event Hub are received using the [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="29fc7-189">Команда служебной шины Microsoft предоставила в открытом доступе клиентские библиотеки, которые упрощают обработку событий.</span><span class="sxs-lookup"><span data-stu-id="29fc7-189">The Microsoft Service Bus team have made client libraries available to make the consuming events easier.</span></span> <span data-ttu-id="29fc7-190">Служба поддерживает два различных подхода: *прямой потребитель* и класс `EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="29fc7-190">There are two different approaches supported, one is being a *Direct Consumer* and the other is using the `EventProcessorHost` class.</span></span> <span data-ttu-id="29fc7-191">Примеры использования этих подходов можно найти в статье [Руководство по программированию концентраторов событий](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="29fc7-191">Examples of these two approaches can be found in the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="29fc7-192">Вкратце рассмотрим различия между ними. `Direct Consumer` дает вам полный контроль, а `EventProcessorHost` берет часть работы на себя, но делает некоторые предположения о том, как вы будете обрабатывать события.</span><span class="sxs-lookup"><span data-stu-id="29fc7-192">The short version of the differences is, `Direct Consumer` gives you complete control and the `EventProcessorHost` does some of the plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="29fc7-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="29fc7-193">EventProcessorHost</span></span>
<span data-ttu-id="29fc7-194">В этом примере мы для простоты будем использовать `EventProcessorHost` , хоть это и не лучший выбор в данном случае.</span><span class="sxs-lookup"><span data-stu-id="29fc7-194">In this sample, we will use the `EventProcessorHost` for simplicity, however it may not the best choice for this particular scenario.</span></span> <span data-ttu-id="29fc7-195">`EventProcessorHost` выполняет самую сложную работу по управлению потоками для конкретного класса обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="29fc7-195">`EventProcessorHost` does the hard work of making sure you don't have to worry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="29fc7-196">Но в нашем случае мы просто преобразуем сообщение в другой формат и передаем его в другую службу, используя асинхронный метод.</span><span class="sxs-lookup"><span data-stu-id="29fc7-196">However, in our scenario, we are simply converting the message to another format and passing it along to another service using an async method.</span></span> <span data-ttu-id="29fc7-197">У нас нет необходимости обновлять общее состояние, и нет риска возникновения проблем с потоками.</span><span class="sxs-lookup"><span data-stu-id="29fc7-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="29fc7-198">В большинстве случаев класс `EventProcessorHost` будет оптимальным вариантом, как минимум самым простым в использовании.</span><span class="sxs-lookup"><span data-stu-id="29fc7-198">For most scenarios, `EventProcessorHost` is probably the best choice and it is certainly the easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="29fc7-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="29fc7-199">IEventProcessor</span></span>
<span data-ttu-id="29fc7-200">Основной задачей при использовании `EventProcessorHost` является реализация интерфейса `IEventProcessor`, который содержит метод `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="29fc7-200">The central concept when using `EventProcessorHost` is to create a an implementation of the `IEventProcessor` interface which contains the method `ProcessEventAsync`.</span></span> <span data-ttu-id="29fc7-201">Суть этого метода показана ниже.</span><span class="sxs-lookup"><span data-stu-id="29fc7-201">The essence of that method is shown here:</span></span>

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

<span data-ttu-id="29fc7-202">Список объектов EventData передается в наш метод, где мы последовательно перебираем элементы этого списка.</span><span class="sxs-lookup"><span data-stu-id="29fc7-202">A list of EventData objects are passed into the method and we iterate over that list.</span></span> <span data-ttu-id="29fc7-203">Содержимое каждого метода преобразуется в объект HttpMessage, и этот объект передается в экземпляр IHttpMessageProcessor.</span><span class="sxs-lookup"><span data-stu-id="29fc7-203">The bytes of each method are parsed into a HttpMessage object and that object is passed to an instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="29fc7-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="29fc7-204">HttpMessage</span></span>
<span data-ttu-id="29fc7-205">Экземпляр `HttpMessage` содержит три фрагмента данных:</span><span class="sxs-lookup"><span data-stu-id="29fc7-205">The `HttpMessage` instance contains three pieces of data:</span></span>

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

<span data-ttu-id="29fc7-206">Экземпляр `HttpMessage` содержит идентификатор GUID `MessageId`, который позволяет связать HTTP-запрос с соответствующим ответом, а также логическое значение, которое сообщает, содержит ли этот объект экземпляр HttpRequestMessage и HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="29fc7-206">The `HttpMessage` instance contains a `MessageId` GUID that allows us to connect the HTTP request to the corresponding HTTP response and a boolean value that identifies if the object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="29fc7-207">Я применил встроенные классы HTTP из `System.Net.Http`, что позволило воспользоваться кодом синтаксического анализа `application/http`, который включен в `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="29fc7-207">By using the built in HTTP classes from `System.Net.Http`, I was able to take advantage of the `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="29fc7-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="29fc7-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="29fc7-209">Затем экземпляр `HttpMessage` передается в реализацию `IHttpMessageProcessor`, который я создал в качестве интерфейса, чтобы отделить получение и интерпретацию события из концентратора событий Azure от фактической обработки этого события.</span><span class="sxs-lookup"><span data-stu-id="29fc7-209">The `HttpMessage` instance is then forwarded to implementation of `IHttpMessageProcessor` which is an interface I created to decouple the receiving and interpretation of the event from Azure Event Hub and the actual processing of it.</span></span>

## <a name="forwarding-the-http-message"></a><span data-ttu-id="29fc7-210">Пересылка сообщения HTTP</span><span class="sxs-lookup"><span data-stu-id="29fc7-210">Forwarding the HTTP message</span></span>
<span data-ttu-id="29fc7-211">Мне показалось интересным использовать в нашем примере отправку HTTP-запроса в [Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="29fc7-211">For this sample, I decided it would be interesting to push the HTTP Request over to [Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="29fc7-212">Runscope — это облачная служба, предназначенная для отладки, регистрации и мониторинга HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="29fc7-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="29fc7-213">У службы есть бесплатный уровень, поэтому ее легко испытать в работе. Мы сможем в реальном времени отслеживать HTTP-запросы, которые проходят через службу управления API.</span><span class="sxs-lookup"><span data-stu-id="29fc7-213">They have a free tier, so it is easy to try and it allows us to see the HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="29fc7-214">Реализация `IHttpMessageProcessor` выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="29fc7-214">The `IHttpMessageProcessor` implementation looks like this,</span></span>

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
       _Logger.LogDebug("Request sent to Runscope");
   }
}
```

<span data-ttu-id="29fc7-215">Для этого применена [существующая клиентская библиотека для службы Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha), которая упрощает передачу экземпляров `HttpRequestMessage` и `HttpResponseMessage` в соответствующую службу.</span><span class="sxs-lookup"><span data-stu-id="29fc7-215">I was able to take advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy to push `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="29fc7-216">Чтобы получить доступ к Runscope API, нужна учетная запись и ключ API.</span><span class="sxs-lookup"><span data-stu-id="29fc7-216">In order to access the Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="29fc7-217">Инструкции по получению ключа API см. в видео [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) (Создание приложений для доступа к API Runscope).</span><span class="sxs-lookup"><span data-stu-id="29fc7-217">Instructions for getting an API key can be found in the [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="29fc7-218">Полный пример</span><span class="sxs-lookup"><span data-stu-id="29fc7-218">Complete sample</span></span>
<span data-ttu-id="29fc7-219">[Исходный код](https://github.com/darrelmiller/ApimEventProcessor) и тесты для этого примера доступны на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="29fc7-219">The [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for the sample are on GitHub.</span></span> <span data-ttu-id="29fc7-220">Чтобы запустить этот пример, вам потребуются [служба управления API](api-management-get-started.md), [подключенный к ней концентратор событий](api-management-howto-log-event-hubs.md) и [учетная запись хранения](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="29fc7-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) to run the sample for yourself.</span></span>   

<span data-ttu-id="29fc7-221">Пример представляет собой простое консольное приложение, которое прослушивает события, поступающие от концентратора событий, преобразует их в объекты `HttpRequestMessage` и `HttpResponseMessage`, а затем пересылает их на API-интерфейс Runscope.</span><span class="sxs-lookup"><span data-stu-id="29fc7-221">The sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on to the Runscope API.</span></span>

<span data-ttu-id="29fc7-222">На анимированном изображении ниже вы видите запрос к API на портале разработчика, получение, обработку и пересылку сообщений в консольном приложении, а также запрос и ответ, отображающиеся в инспекторе трафика Runscope.</span><span class="sxs-lookup"><span data-stu-id="29fc7-222">In the following animated image, you can see a request being made to an API in the Developer Portal, the Console application showing the message being received, processed and forwarded and then the request and response showing up in the Runscope Traffic inspector.</span></span>

![Демонстрация передачи запроса в Runscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="29fc7-224">Сводка</span><span class="sxs-lookup"><span data-stu-id="29fc7-224">Summary</span></span>
<span data-ttu-id="29fc7-225">Служба управления API Azure — это идеальное место для фиксации HTTP-трафика, поступающего на API-интерфейсы и в обратном направлении.</span><span class="sxs-lookup"><span data-stu-id="29fc7-225">Azure API Management service provides an ideal place to capture the HTTP traffic travelling to and from your APIs.</span></span> <span data-ttu-id="29fc7-226">Концентраторы событий Azure — это высокомасштабируемое недорогое решение, которое собирает информацию о трафике и передает ее в системы дополнительной обработки для регистрации, мониторинга и сложного анализа.</span><span class="sxs-lookup"><span data-stu-id="29fc7-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="29fc7-227">Для подключения к сторонним системам мониторинга трафика, например Runscope, потребуется всего несколько десятков строк кода.</span><span class="sxs-lookup"><span data-stu-id="29fc7-227">Connecting to 3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29fc7-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="29fc7-228">Next steps</span></span>
* <span data-ttu-id="29fc7-229">Дополнительная информация о концентраторах событий Azure</span><span class="sxs-lookup"><span data-stu-id="29fc7-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="29fc7-230">Приступая к работе с концентраторами событий Azure</span><span class="sxs-lookup"><span data-stu-id="29fc7-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="29fc7-231">Прием сообщений через EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="29fc7-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="29fc7-232">Руководство по программированию концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="29fc7-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="29fc7-233">Дополнительные сведения об интеграции службы управления API и концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="29fc7-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="29fc7-234">Как регистрировать события в концентраторах событий Azure в службе управления Azure API</span><span class="sxs-lookup"><span data-stu-id="29fc7-234">How to log events to Azure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="29fc7-235">Справочник по сущности "Средство ведения журнала"</span><span class="sxs-lookup"><span data-stu-id="29fc7-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="29fc7-236">Справочник по политике регистрации в концентраторе событий</span><span class="sxs-lookup"><span data-stu-id="29fc7-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
