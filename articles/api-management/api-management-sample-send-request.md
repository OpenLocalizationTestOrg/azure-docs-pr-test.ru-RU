---
title: "запросы toogenerate HTTP службы управления API aaaUsing"
description: "Дополнительные сведения toouse политики запросов и ответов в внешние службы управления API toocall из API"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 4539c0fa-21ef-4b1c-a1d4-d89a38c242fa
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 8002ee453057513340328d99f298703c3b3a9531
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-external-services-from-hello-azure-api-management-service"></a><span data-ttu-id="3d11a-103">Использование внешних служб из hello службы управления API Azure</span><span class="sxs-lookup"><span data-stu-id="3d11a-103">Using external services from hello Azure API Management service</span></span>
<span data-ttu-id="3d11a-104">Hello политик, доступных в службе управления API Azure можно сделать широкий спектр нормальной работе исключительно на основе входящего запроса hello, исходящего ответа hello и сведений об основной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3d11a-104">hello policies available in Azure API Management service can do a wide range of useful work based purely on hello incoming request, hello outgoing response and basic configuration information.</span></span> <span data-ttu-id="3d11a-105">Тем не менее, могут toointeract с внешним службам из API управления политики открывает множество новых возможностей.</span><span class="sxs-lookup"><span data-stu-id="3d11a-105">However, being able toointeract with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="3d11a-106">Мы видели ранее мы взаимодействие с hello [концентратор событий Azure service для ведения журнала, мониторинг и аналитику](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="3d11a-106">We have previously seen how we can interact with hello [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="3d11a-107">В этой статье мы покажем, что служба на основе политик, которые позволяют вам toointeract с любой внешней HTTP.</span><span class="sxs-lookup"><span data-stu-id="3d11a-107">In this article we will demonstrate policies that allow you toointeract with any external HTTP based service.</span></span> <span data-ttu-id="3d11a-108">Эти политики можно использовать для запуска удаленных событий или для получения сведений, которые будут используется toomanipulate hello исходного запроса и ответа иным образом.</span><span class="sxs-lookup"><span data-stu-id="3d11a-108">These policies can be used for triggering remote events or for retrieving information that will be used toomanipulate hello original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="3d11a-109">Отправка одностороннего запроса</span><span class="sxs-lookup"><span data-stu-id="3d11a-109">Send-One-Way-Request</span></span>
<span data-ttu-id="3d11a-110">Возможно hello простой внешнего взаимодействия не стиль выстрелил и забыл hello запрос, который позволяет внешней службе toobe уведомление о том, какой-либо важных событий.</span><span class="sxs-lookup"><span data-stu-id="3d11a-110">Possibly hello simplest external interaction is hello fire-and-forget style of request that allows an external service toobe notified of some kind of important event.</span></span> <span data-ttu-id="3d11a-111">Мы используем политика потока управления hello `choose` toodetect любого вида условие, которое мы интересуют, а затем, если hello условие выполняется, можно сделать внешних HTTP-запроса с помощью hello [-один способом запрос на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) политики.</span><span class="sxs-lookup"><span data-stu-id="3d11a-111">We can use hello control flow policy `choose` toodetect any kind of condition that we are interested in and then, if hello condition is satisfied, we can make an external HTTP request using hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="3d11a-112">Это может быть запрос tooa, системы, такие как Hipchat или Slack или почты API, например SendGrid или MailChimp обмена сообщениями или для обращения в службу поддержки критических что-то наподобие PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="3d11a-112">This could be a request tooa messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="3d11a-113">Все эти системы обмена сообщениями обладают простыми API-интерфейсами HTTP, которые можно легко вызвать.</span><span class="sxs-lookup"><span data-stu-id="3d11a-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="3d11a-114">Оповещения с использованием Slack</span><span class="sxs-lookup"><span data-stu-id="3d11a-114">Alerting with Slack</span></span>
<span data-ttu-id="3d11a-115">Следующий пример Hello демонстрирует временных резервов чат, если код состояния HTTP-ответа hello больше или равно too500 toosend tooa сообщения.</span><span class="sxs-lookup"><span data-stu-id="3d11a-115">hello following example demonstrates how toosend a message tooa Slack chat room if hello HTTP response status code is greater than or equal too500.</span></span> <span data-ttu-id="3d11a-116">Ошибка диапазона 500 указывает, что проблема с нашей API внутреннего сервера, hello клиента о нашем API не удается разрешить самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="3d11a-116">A 500 range error indicates a problem with our backend API that hello client of our API cannot resolve themselves.</span></span> <span data-ttu-id="3d11a-117">Обычно требуется вмешательство с нашей стороны.</span><span class="sxs-lookup"><span data-stu-id="3d11a-117">It usually requires some kind of intervention on our part.</span></span>  

```xml
<choose>
    <when condition="@(context.Response.StatusCode >= 500)">
      <send-one-way-request mode="new">
        <set-url>https://hooks.slack.com/services/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</set-url>
        <set-method>POST</set-method>
        <set-body>@{
                return new JObject(
                        new JProperty("username","APIM Alert"),
                        new JProperty("icon_emoji", ":ghost:"),
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",
                                                context.Request.Method,
                                                context.Request.Url.Path + context.Request.Url.QueryString,
                                                context.Request.Url.Host,
                                                context.Response.StatusCode,
                                                context.Response.StatusReason,
                                                context.User.Email
                                                ))
                        ).ToString();
            }</set-body>
      </send-one-way-request>
    </when>
</choose>
```

<span data-ttu-id="3d11a-118">Резерв имеет hello понятие входящего веб-обработчики.</span><span class="sxs-lookup"><span data-stu-id="3d11a-118">Slack has hello notion of inbound web hooks.</span></span> <span data-ttu-id="3d11a-119">При настройке входящих веб-обработчик, Slack приводит к возникновению ошибки специальный URL-адрес, который позволяет toodo простой запрос POST и toopass сообщение в канале Slack hello.</span><span class="sxs-lookup"><span data-stu-id="3d11a-119">When configuring an inbound web hook, Slack generates a special URL which allows you toodo a simple POST request and toopass a message into hello Slack channel.</span></span> <span data-ttu-id="3d11a-120">текст JSON, который мы создадим Hello основан на формате, заданном параметром Slack.</span><span class="sxs-lookup"><span data-stu-id="3d11a-120">hello JSON body that we create is based on a format defined by Slack.</span></span>

![Веб-привязка Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="3d11a-122">Достаточно ли хорош автономный запрос?</span><span class="sxs-lookup"><span data-stu-id="3d11a-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="3d11a-123">Использование автономного запроса связано с некоторыми компромиссами.</span><span class="sxs-lookup"><span data-stu-id="3d11a-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="3d11a-124">Если для какой-либо причине hello запрос завершается ошибкой, а затем hello ошибки не будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="3d11a-124">If for some reason, hello request fails, then hello failure will not be reported.</span></span> <span data-ttu-id="3d11a-125">В этом случае конкретной системе отчетов об ошибках получателя и hello дополнительные издержки, связанные Ожидание ответа hello сложности hello могут не поддерживать.</span><span class="sxs-lookup"><span data-stu-id="3d11a-125">In this particular situation, hello complexity of having a secondary failure reporting system and hello additional performance cost of waiting for hello response is not warranted.</span></span> <span data-ttu-id="3d11a-126">Для сценариев, где essential toocheck hello ответа, hello [запрос на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) политики является лучшим вариантом.</span><span class="sxs-lookup"><span data-stu-id="3d11a-126">For scenarios where it is essential toocheck hello response, then hello [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="3d11a-127">запроса на отправку</span><span class="sxs-lookup"><span data-stu-id="3d11a-127">Send-Request</span></span>
<span data-ttu-id="3d11a-128">Hello `send-request` политика позволяет с помощью сложной обработки функций и службы управления toohello API возвращаемых данных, который может использоваться для дальнейшей обработке политики tooperform внешней службы.</span><span class="sxs-lookup"><span data-stu-id="3d11a-128">hello `send-request` policy enables using an external service tooperform complex processing functions and return data toohello API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="3d11a-129">Авторизация маркеров ссылок</span><span class="sxs-lookup"><span data-stu-id="3d11a-129">Authorizing reference tokens</span></span>
<span data-ttu-id="3d11a-130">Основная задача API управления состоит в защите серверных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3d11a-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="3d11a-131">Если сервер авторизации hello, используемый API создает [маркеры JWT](http://jwt.io/) как часть его OAuth2 поток как [Azure Active Directory](../active-directory/active-directory-aadconnect.md) так, то можно использовать hello `validate-jwt` допустимость tooverify hello политики токен Hello.</span><span class="sxs-lookup"><span data-stu-id="3d11a-131">If hello authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use hello `validate-jwt` policy tooverify hello validity of hello token.</span></span> <span data-ttu-id="3d11a-132">Тем не менее, некоторые серверы авторизации создавать, называемых [ссылаться токены](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) без создания сервера авторизации toohello обратного вызова, не могут быть проверены.</span><span class="sxs-lookup"><span data-stu-id="3d11a-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back toohello authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="3d11a-133">Стандартизованный самоанализ</span><span class="sxs-lookup"><span data-stu-id="3d11a-133">Standardized introspection</span></span>
<span data-ttu-id="3d11a-134">В прошлом hello был не стандартизированные может проверить токен ссылки с сервера авторизации.</span><span class="sxs-lookup"><span data-stu-id="3d11a-134">In hello past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="3d11a-135">Однако недавно Предложенный стандарт [RFC 7662](https://tools.ietf.org/html/rfc7662) опубликовал hello IETF, определяющий, как сервер ресурсов можно проверить действительность hello маркера.</span><span class="sxs-lookup"><span data-stu-id="3d11a-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by hello IETF that defines how a resource server can verify hello validity of a token.</span></span>

### <a name="extracting-hello-token"></a><span data-ttu-id="3d11a-136">Извлечение маркера hello</span><span class="sxs-lookup"><span data-stu-id="3d11a-136">Extracting hello token</span></span>
<span data-ttu-id="3d11a-137">Hello первым шагом является tooextract hello токен из заголовка авторизации hello.</span><span class="sxs-lookup"><span data-stu-id="3d11a-137">hello first step is tooextract hello token from hello Authorization header.</span></span> <span data-ttu-id="3d11a-138">значение заголовка Hello должны иметь формат hello `Bearer` схемы авторизации, пробел и затем hello авторизации токен согласно [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="3d11a-138">hello header value should be formatted with hello `Bearer` authorization scheme, a single space and then hello authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="3d11a-139">К сожалению, существуют случаи, где опущен схему авторизации hello.</span><span class="sxs-lookup"><span data-stu-id="3d11a-139">Unfortunately there are cases where hello authorization scheme is omitted.</span></span> <span data-ttu-id="3d11a-140">tooaccount для этого во время синтаксического анализа, мы разделить значение заголовка hello пространство и выберите hello последняя строка из hello, возвращаемый массив строк.</span><span class="sxs-lookup"><span data-stu-id="3d11a-140">tooaccount for this when parsing, we split hello header value on a space and select hello last string from hello returned array of strings.</span></span> <span data-ttu-id="3d11a-141">Это возможное решение позволяет справиться с неправильно отформатированными заголовками авторизации.</span><span class="sxs-lookup"><span data-stu-id="3d11a-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a><span data-ttu-id="3d11a-142">Запрос проверки hello</span><span class="sxs-lookup"><span data-stu-id="3d11a-142">Making hello validation request</span></span>
<span data-ttu-id="3d11a-143">После получения маркера авторизации hello, можно сделать маркер hello toovalidate hello запроса.</span><span class="sxs-lookup"><span data-stu-id="3d11a-143">Once we have hello authorization token, we can make hello request toovalidate hello token.</span></span> <span data-ttu-id="3d11a-144">RFC 7662 вызывает интроспекции этот процесс и требуется, вы `POST` toohello интроспекции HTML-формы ресурса.</span><span class="sxs-lookup"><span data-stu-id="3d11a-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form toohello introspection resource.</span></span> <span data-ttu-id="3d11a-145">Hello HTML-формы по крайней мере должен содержать пару ключ значение с ключом hello `token`.</span><span class="sxs-lookup"><span data-stu-id="3d11a-145">hello HTML form must at least contain a key/value pair with hello key `token`.</span></span> <span data-ttu-id="3d11a-146">Сервер авторизации toohello этот запрос также должен быть tooensure прошедшего проверку подлинности, который вредоносных клиентов не удается перейти trawling для допустимых маркеров.</span><span class="sxs-lookup"><span data-stu-id="3d11a-146">This request toohello authorization server must also be authenticated tooensure that malicious clients cannot go trawling for valid tokens.</span></span>

```xml
<send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
  <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
  <set-method>POST</set-method>
  <set-header name="Authorization" exists-action="override">
    <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
  </set-header>
  <set-header name="Content-Type" exists-action="override">
    <value>application/x-www-form-urlencoded</value>
  </set-header>
  <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
</send-request>
```

### <a name="checking-hello-response"></a><span data-ttu-id="3d11a-147">Проверка ответов hello</span><span class="sxs-lookup"><span data-stu-id="3d11a-147">Checking hello response</span></span>
<span data-ttu-id="3d11a-148">Hello `response-variable-name` атрибут является hello доступа используется toogive отклик.</span><span class="sxs-lookup"><span data-stu-id="3d11a-148">hello `response-variable-name` attribute is used toogive access hello returned response.</span></span> <span data-ttu-id="3d11a-149">Hello имя, определенное в этом свойстве можно использовать в качестве ключа в hello `context.Variables` tooaccess hello словарь `IResponse` объекта.</span><span class="sxs-lookup"><span data-stu-id="3d11a-149">hello name defined in this property can be used as a key into hello `context.Variables` dictionary tooaccess hello `IResponse` object.</span></span>

<span data-ttu-id="3d11a-150">Из hello объекта ответа можно извлечь текст hello и RFC 7622 указывает, что hello ответ должен быть объектом JSON и должен содержать по крайней мере свойство с именем `active` , логическое значение.</span><span class="sxs-lookup"><span data-stu-id="3d11a-150">From hello response object we can retrieve hello body and RFC 7622 tells us that hello response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="3d11a-151">Когда `active` имеет значение true, то токен hello считается допустимым.</span><span class="sxs-lookup"><span data-stu-id="3d11a-151">When `active` is true then hello token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="3d11a-152">Отчеты об ошибках</span><span class="sxs-lookup"><span data-stu-id="3d11a-152">Reporting failure</span></span>
<span data-ttu-id="3d11a-153">Мы используем `<choose>` toodetect политики, если hello маркер является недопустимым и если да, возвращают ответ 401.</span><span class="sxs-lookup"><span data-stu-id="3d11a-153">We use a `<choose>` policy toodetect if hello token is invalid and if so, return a 401 response.</span></span>

```xml
<choose>
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
    <return-response response-variable-name="existing response variable">
      <set-status code="401" reason="Unauthorized" />
      <set-header name="WWW-Authenticate" exists-action="override">
        <value>Bearer error="invalid_token"</value>
      </set-header>
    </return-response>
  </when>
</choose>
```

<span data-ttu-id="3d11a-154">Согласно [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) описано, как `bearer` следует использовать токены, мы также возвращают `WWW-Authenticate` заголовок с ответом hello 401.</span><span class="sxs-lookup"><span data-stu-id="3d11a-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with hello 401 response.</span></span> <span data-ttu-id="3d11a-155">Привет, WWW-Authenticate является предполагаемым tooinstruct клиента о том, как tooconstruct правильно авторизованный запрос.</span><span class="sxs-lookup"><span data-stu-id="3d11a-155">hello WWW-Authenticate is intended tooinstruct a client on how tooconstruct a properly authorized request.</span></span> <span data-ttu-id="3d11a-156">Из-за toohello различных подходов, возможно с hello OAuth2 framework, трудно toocommunicate hello все необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="3d11a-156">Due toohello wide variety of approaches possible with hello OAuth2 framework, it is difficult toocommunicate all hello needed information.</span></span> <span data-ttu-id="3d11a-157">К счастью существует усилия ведется toohelp [клиентам обнаруживать как tooproperly авторизации запросов tooa ресурсов сервера](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="3d11a-157">Fortunately there are efforts underway toohelp [clients discover how tooproperly authorize requests tooa resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="3d11a-158">Окончательное решение</span><span class="sxs-lookup"><span data-stu-id="3d11a-158">Final solution</span></span>
<span data-ttu-id="3d11a-159">Совместное размещение все составляющие hello, мы получаем hello следующие политики:</span><span class="sxs-lookup"><span data-stu-id="3d11a-159">Putting all hello pieces together, we get hello following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
    <set-method>POST</set-method>
    <set-header name="Authorization" exists-action="override">
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
    </set-header>
    <set-header name="Content-Type" exists-action="override">
      <value>application/x-www-form-urlencoded</value>
    </set-header>
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
  </send-request>

  <choose>
          <!-- Check active property in response -->
          <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
              <!-- Return 401 Unauthorized with http-problem payload -->
              <return-response response-variable-name="existing response variable">
                  <set-status code="401" reason="Unauthorized" />
                  <set-header name="WWW-Authenticate" exists-action="override">
                      <value>Bearer error="invalid_token"</value>
                  </set-header>
              </return-response>
          </when>
      </choose>
  <base />
</inbound>
```

<span data-ttu-id="3d11a-160">Это только один из многих примеры hello `send-request` политики может быть полезным внешних служб используется toointegrate в процесс hello запросов и ответов, проходящей через hello службы управления API.</span><span class="sxs-lookup"><span data-stu-id="3d11a-160">This is only one of many examples of how hello `send-request` policy can be used toointegrate useful external services into hello process of requests and responses flowing through hello API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="3d11a-161">Структура ответа</span><span class="sxs-lookup"><span data-stu-id="3d11a-161">Response Composition</span></span>
<span data-ttu-id="3d11a-162">Hello `send-request` политика может использоваться для повышения серверной системе tooa основного запроса, как было показано в предыдущем примере hello, или он может использоваться как полный замены для внутреннего вызова hello.</span><span class="sxs-lookup"><span data-stu-id="3d11a-162">hello `send-request` policy can be used for enhancing a primary request tooa backend system, as we saw in hello previous example, or it can be used as a complete replace for of hello backend call.</span></span> <span data-ttu-id="3d11a-163">С помощью этой методики можно легко создавать сложные ресурсы, которые объединяются из нескольких разных систем.</span><span class="sxs-lookup"><span data-stu-id="3d11a-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="3d11a-164">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="3d11a-164">Building a dashboard</span></span>
<span data-ttu-id="3d11a-165">Иногда требуется toobe может tooexpose данные из нескольких серверных системах, к примеру, toodrive панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="3d11a-165">Sometimes you want toobe able tooexpose information that exists in multiple backend systems, for example, toodrive a dashboard.</span></span> <span data-ttu-id="3d11a-166">Hello ключевые показатели эффективности берутся из разных все назад элементов, но вы предпочитаете не toothem tooprovide прямой доступ и было бы неплохо, если в одном запросе может получить все сведения о hello.</span><span class="sxs-lookup"><span data-stu-id="3d11a-166">hello KPIs come from all different back-ends, but you would prefer not tooprovide direct access toothem and it would be nice if all hello information could be retrieved in a single request.</span></span> <span data-ttu-id="3d11a-167">Возможно некоторые из сведений о серверной части hello должен некоторые срезы и разделять и немного очистки данных сначала!</span><span class="sxs-lookup"><span data-stu-id="3d11a-167">Perhaps some of hello backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="3d11a-168">Выполняется доступ toocache, что составной ресурс будет полезно tooreduce серверной hello загрузить как вам известно, что пользователи имеют привычка подбору паролей hello клавишу F5 в порядке toosee, если их неэффективно метрики могут измениться.</span><span class="sxs-lookup"><span data-stu-id="3d11a-168">Being able toocache that composite resource would be a useful tooreduce hello backend load as you know users have a habit of hammering hello F5 key in order toosee if their underperforming metrics might change.</span></span>    

### <a name="faking-hello-resource"></a><span data-ttu-id="3d11a-169">Faking hello ресурсов</span><span class="sxs-lookup"><span data-stu-id="3d11a-169">Faking hello resource</span></span>
<span data-ttu-id="3d11a-170">Здравствуйте, первый шаг toobuilding нашего ресурса панели мониторинга — tooconfigure новую операцию в портал издателя управления API hello.</span><span class="sxs-lookup"><span data-stu-id="3d11a-170">hello first step toobuilding our dashboard resource is tooconfigure a new operation in hello API Management publisher portal.</span></span> <span data-ttu-id="3d11a-171">Это будет tooconfigure заполнитель операции, используемой политики нашей композиции toobuild нашей динамический ресурс.</span><span class="sxs-lookup"><span data-stu-id="3d11a-171">This will be a placeholder operation used tooconfigure our composition policy toobuild our dynamic resource.</span></span>

![Операция панели мониторинга](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a><span data-ttu-id="3d11a-173">Создание запросов hello</span><span class="sxs-lookup"><span data-stu-id="3d11a-173">Making hello requests</span></span>
<span data-ttu-id="3d11a-174">Здравствуйте, один раз `dashboard` созданный операцией можно настроить политики специально для этой операции.</span><span class="sxs-lookup"><span data-stu-id="3d11a-174">Once hello `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Операция панели мониторинга](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="3d11a-176">Hello первым шагом является tooextract все параметры запроса из входящего запроса hello, мы перенаправлять их tooour серверной части.</span><span class="sxs-lookup"><span data-stu-id="3d11a-176">hello first step  is tooextract any query parameters from hello incoming request, so that we can forward them tooour backend.</span></span> <span data-ttu-id="3d11a-177">В этом примере на панели мониторинга сведения отображаются на основе определенного периода времени, поэтому здесь присутствуют параметры `fromDate` и `toDate`.</span><span class="sxs-lookup"><span data-stu-id="3d11a-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="3d11a-178">Мы используем hello `set-variable` политики tooextract hello сведения из URL-адрес запроса hello.</span><span class="sxs-lookup"><span data-stu-id="3d11a-178">We can use hello `set-variable` policy tooextract hello information from hello request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="3d11a-179">После получения этих сведений можно сделать запросов tooall hello серверных системах.</span><span class="sxs-lookup"><span data-stu-id="3d11a-179">Once we have this information we can make requests tooall hello backend systems.</span></span> <span data-ttu-id="3d11a-180">Каждый запрос создает новый URL-адрес с сведения о параметрах hello и вызывает его соответствующий сервер и сохраняет ответ hello в переменной контекста.</span><span class="sxs-lookup"><span data-stu-id="3d11a-180">Each request constructs a new URL with hello parameter information and calls its respective server and stores hello response in a context variable.</span></span>

```xml
<send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
  <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
  <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="3d11a-181">Эти запросы выполняются последовательно, что не очень удобно.</span><span class="sxs-lookup"><span data-stu-id="3d11a-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="3d11a-182">В следующих выпусках Корпорация Майкрософт представит новую политику с именем `wait` , обеспечивающие все эти запросы tooexecute параллельно.</span><span class="sxs-lookup"><span data-stu-id="3d11a-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests tooexecute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="3d11a-183">Ответы на запросы</span><span class="sxs-lookup"><span data-stu-id="3d11a-183">Responding</span></span>
<span data-ttu-id="3d11a-184">tooconstruct hello составной ответ можно использовать hello [возврата ответа](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) политики.</span><span class="sxs-lookup"><span data-stu-id="3d11a-184">tooconstruct hello composite response we can use hello [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="3d11a-185">Hello `set-body` элемент можно использовать выражение tooconstruct новый `JObject` с все представления компонента hello, внедренных в качестве свойства.</span><span class="sxs-lookup"><span data-stu-id="3d11a-185">hello `set-body` element can use an expression tooconstruct a new `JObject` with all hello component representations embedded as properties.</span></span>

```xml
<return-response response-variable-name="existing response variable">
  <set-status code="200" reason="OK" />
  <set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
  </set-header>
  <set-body>
    @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                  new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                  new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                  new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                  ).ToString())
  </set-body>
</return-response>
```

<span data-ttu-id="3d11a-186">политика завершения Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3d11a-186">hello complete policy looks as follows:</span></span>

```xml
<policies>
    <inbound>

  <set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
  <set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">

    <send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
      <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
      <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <return-response response-variable-name="existing response variable">
      <set-status code="200" reason="OK" />
      <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
      </set-header>
      <set-body>
        @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                      new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                      new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                      new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                      ).ToString())
      </set-body>
    </return-response>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="3d11a-187">В конфигурации hello hello заполнитель операции, которые можно настроить toobe ресурсов панели мониторинга hello в кэше по крайней мере один час пониманием того, что характер hello hello данных означает, что даже если он является устаревшим, он все равно будет достаточно эффективных часа Пользователи toohello tooconvey ценные сведения.</span><span class="sxs-lookup"><span data-stu-id="3d11a-187">In hello configuration of hello placeholder operation we can configure hello dashboard resource toobe cached for at least an hour because we understand hello nature of hello data means that even if it is an hour out of date, it will still be sufficiently effective tooconvey valuable information toohello users.</span></span>

## <a name="summary"></a><span data-ttu-id="3d11a-188">Сводка</span><span class="sxs-lookup"><span data-stu-id="3d11a-188">Summary</span></span>
<span data-ttu-id="3d11a-189">Служба управления API Azure предоставляет гибкие политики, которые можно выборочно применить tooHTTP трафика и позволяет композиции внутренних служб.</span><span class="sxs-lookup"><span data-stu-id="3d11a-189">Azure API Management service provides flexible policies that can be selectively applied tooHTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="3d11a-190">Здравствуйте, является ли tooenhance шлюз API с предупреждением, функции, проверки, возможности проверки или создайте новый составной ресурсы в зависимости от нескольких серверных служб, `send-request` и связанные политики откройте мир новых возможностей.</span><span class="sxs-lookup"><span data-stu-id="3d11a-190">Whether you want tooenhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, hello `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="3d11a-191">Посмотрите видеообзор этих политик.</span><span class="sxs-lookup"><span data-stu-id="3d11a-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="3d11a-192">Дополнительные сведения о hello [-один способом запрос на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [запрос на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), и [возврата ответа](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) политики, описанные в данной статье, обратите внимание на следующие видео hello.</span><span class="sxs-lookup"><span data-stu-id="3d11a-192">For more information on hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

