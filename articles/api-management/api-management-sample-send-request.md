---
title: "Использование службы управления API для создания HTTP-запросов"
description: "Узнайте, как использовать политики запросов и ответов в службе управления API для вызова внешних служб из API."
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
ms.openlocfilehash: e778943715d6ca5256ad612d82bdc1f82197df0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-external-services-from-the-azure-api-management-service"></a><span data-ttu-id="69417-103">Использование внешних служб из службы управления API Azure</span><span class="sxs-lookup"><span data-stu-id="69417-103">Using external services from the Azure API Management service</span></span>
<span data-ttu-id="69417-104">Политики, доступные в службе управления API Azure, позволяют выполнять множество полезных задач исключительно на основе входящих запросов, исходящих ответов и сведений о базовой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="69417-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span></span> <span data-ttu-id="69417-105">Однако возможность взаимодействия с внешними службами управления из политик управления API предоставляет гораздо больше преимуществ.</span><span class="sxs-lookup"><span data-stu-id="69417-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="69417-106">Мы уже имеем представление о взаимодействии со [службой концентратора событий Azure для ведения журнала, мониторинга и анализа](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="69417-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="69417-107">В этой статье вы узнаете о политиках, которые позволяют работать с любой внешней HTTP-службой.</span><span class="sxs-lookup"><span data-stu-id="69417-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span></span> <span data-ttu-id="69417-108">Эти политики можно использовать для запуска удаленных событий или для получения данных, которые определенным образом будут применяться для обработки исходного запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="69417-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="69417-109">Отправка одностороннего запроса</span><span class="sxs-lookup"><span data-stu-id="69417-109">Send-One-Way-Request</span></span>
<span data-ttu-id="69417-110">Возможно, самым простым вариантом внешнего взаимодействия является автономный запрос, который позволяет уведомлять внешнюю службу о каком-либо важном событии.</span><span class="sxs-lookup"><span data-stu-id="69417-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span></span> <span data-ttu-id="69417-111">Мы будем использовать политику потока управления `choose` для обнаружения интересующего нас состояния, а затем в случае выполнения условия мы осуществим внешний HTTP-запрос с помощью политики [отправки одностороннего запроса](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) .</span><span class="sxs-lookup"><span data-stu-id="69417-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="69417-112">Это может быть запрос к системе обмена сообщениями, например Hipchat или Slack, или к почтовому API, например SendGrid или MailChimp, или для обращения в службу поддержки критических инцидентов, например PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="69417-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="69417-113">Все эти системы обмена сообщениями обладают простыми API-интерфейсами HTTP, которые можно легко вызвать.</span><span class="sxs-lookup"><span data-stu-id="69417-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="69417-114">Оповещения с использованием Slack</span><span class="sxs-lookup"><span data-stu-id="69417-114">Alerting with Slack</span></span>
<span data-ttu-id="69417-115">В следующем примере демонстрируется отправка сообщения в чат Slack, если код состояния HTTP-ответа больше или равен 500.</span><span class="sxs-lookup"><span data-stu-id="69417-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span></span> <span data-ttu-id="69417-116">Ошибка в диапазоне 500 указывает на наличие проблемы с API серверной части, которую клиент API не может устранить самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="69417-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span></span> <span data-ttu-id="69417-117">Обычно требуется вмешательство с нашей стороны.</span><span class="sxs-lookup"><span data-stu-id="69417-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="69417-118">В системе Slack используется понятие входящих веб-привязок.</span><span class="sxs-lookup"><span data-stu-id="69417-118">Slack has the notion of inbound web hooks.</span></span> <span data-ttu-id="69417-119">При настройке входящей веб-привязки Slack создает специальный URL-адрес, который служит для выполнения простого запроса POST и передачи сообщения в канал Slack.</span><span class="sxs-lookup"><span data-stu-id="69417-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span></span> <span data-ttu-id="69417-120">Создаваемый текст JSON основан на формате, определенном системой Slack.</span><span class="sxs-lookup"><span data-stu-id="69417-120">The JSON body that we create is based on a format defined by Slack.</span></span>

![Веб-привязка Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="69417-122">Достаточно ли хорош автономный запрос?</span><span class="sxs-lookup"><span data-stu-id="69417-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="69417-123">Использование автономного запроса связано с некоторыми компромиссами.</span><span class="sxs-lookup"><span data-stu-id="69417-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="69417-124">Если по какой-либо причине запрос завершается ошибкой, сообщение о сбое не выводится.</span><span class="sxs-lookup"><span data-stu-id="69417-124">If for some reason, the request fails, then the failure will not be reported.</span></span> <span data-ttu-id="69417-125">В этой конкретной ситуации сложности, связанные с необходимостью наличия вторичной системы сообщений о сбоях и дополнительными издержками при ожидании ответа, являются неоправданными.</span><span class="sxs-lookup"><span data-stu-id="69417-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span></span> <span data-ttu-id="69417-126">В ситуациях, где проверка ответа имеет важное значение, лучшим вариантом будет политика [запроса на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) .</span><span class="sxs-lookup"><span data-stu-id="69417-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="69417-127">запроса на отправку</span><span class="sxs-lookup"><span data-stu-id="69417-127">Send-Request</span></span>
<span data-ttu-id="69417-128">Политика `send-request` позволяет использовать внешнюю службу для выполнения сложных действий по обработке и возврату данных в службу управления API для дальнейшей обработки политики.</span><span class="sxs-lookup"><span data-stu-id="69417-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="69417-129">Авторизация маркеров ссылок</span><span class="sxs-lookup"><span data-stu-id="69417-129">Authorizing reference tokens</span></span>
<span data-ttu-id="69417-130">Основная задача API управления состоит в защите серверных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="69417-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="69417-131">Если сервер авторизации, используемый API-интерфейсом, создает [маркеры JWT](http://jwt.io/) в рамках потока OAuth2, как это делается в [Azure Active Directory](../active-directory/active-directory-aadconnect.md), с помощью политики `validate-jwt` можно проверить допустимость маркера.</span><span class="sxs-lookup"><span data-stu-id="69417-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span></span> <span data-ttu-id="69417-132">Однако некоторые серверы авторизации создают так называемые [маркеры ссылок](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) , для проверки которых требуется обратный вызов к серверу авторизации.</span><span class="sxs-lookup"><span data-stu-id="69417-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="69417-133">Стандартизованный самоанализ</span><span class="sxs-lookup"><span data-stu-id="69417-133">Standardized introspection</span></span>
<span data-ttu-id="69417-134">Раньше не было стандартизированного способа проверки маркера ссылки на сервере авторизации.</span><span class="sxs-lookup"><span data-stu-id="69417-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="69417-135">Однако группа IETF опубликовала недавно предложенный стандарт [RFC 7662](https://tools.ietf.org/html/rfc7662) , определяющий метод проверки допустимости маркера сервером ресурсов.</span><span class="sxs-lookup"><span data-stu-id="69417-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span></span>

### <a name="extracting-the-token"></a><span data-ttu-id="69417-136">Извлечение маркера</span><span class="sxs-lookup"><span data-stu-id="69417-136">Extracting the token</span></span>
<span data-ttu-id="69417-137">Первым действием является извлечение маркера из заголовка авторизации.</span><span class="sxs-lookup"><span data-stu-id="69417-137">The first step is to extract the token from the Authorization header.</span></span> <span data-ttu-id="69417-138">Значение заголовка должно быть отформатировано с помощью схемы авторизации `Bearer` — согласно [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1)сначала указывается одиночный пробел, за которым следует маркер авторизации.</span><span class="sxs-lookup"><span data-stu-id="69417-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="69417-139">К сожалению, существуют случаи, когда схема авторизации опускается.</span><span class="sxs-lookup"><span data-stu-id="69417-139">Unfortunately there are cases where the authorization scheme is omitted.</span></span> <span data-ttu-id="69417-140">Чтобы учесть этот момент во время анализа, мы разделили значение заголовка и в возвращенном массиве строк выбрали последнюю строку.</span><span class="sxs-lookup"><span data-stu-id="69417-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span></span> <span data-ttu-id="69417-141">Это возможное решение позволяет справиться с неправильно отформатированными заголовками авторизации.</span><span class="sxs-lookup"><span data-stu-id="69417-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-the-validation-request"></a><span data-ttu-id="69417-142">Выполнение запроса на проверку</span><span class="sxs-lookup"><span data-stu-id="69417-142">Making the validation request</span></span>
<span data-ttu-id="69417-143">После получения маркера авторизации можно выполнить запрос на проверку маркера.</span><span class="sxs-lookup"><span data-stu-id="69417-143">Once we have the authorization token, we can make the request to validate the token.</span></span> <span data-ttu-id="69417-144">В RFC 7662 этот процесс называется самоанализом, и требуется, чтобы вы `POST` HTML-форму в ресурс самоанализа.</span><span class="sxs-lookup"><span data-stu-id="69417-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span></span> <span data-ttu-id="69417-145">HTML-форма должна содержать по крайней мере пару "ключ-значение" с ключом `token`.</span><span class="sxs-lookup"><span data-stu-id="69417-145">The HTML form must at least contain a key/value pair with the key `token`.</span></span> <span data-ttu-id="69417-146">Этот запрос к серверу авторизации также должен пройти проверку подлинности, чтобы гарантировать, что вредоносным клиентам не удается найти допустимые маркеры.</span><span class="sxs-lookup"><span data-stu-id="69417-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span></span>

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

### <a name="checking-the-response"></a><span data-ttu-id="69417-147">Проверка ответа</span><span class="sxs-lookup"><span data-stu-id="69417-147">Checking the response</span></span>
<span data-ttu-id="69417-148">Для предоставления доступа к возвращаемому ответу используется атрибут `response-variable-name` .</span><span class="sxs-lookup"><span data-stu-id="69417-148">The `response-variable-name` attribute is used to give access the returned response.</span></span> <span data-ttu-id="69417-149">Имя, определенное в этом свойстве, можно использовать в качестве ключа к словарю `context.Variables` для доступа к объекту `IResponse`.</span><span class="sxs-lookup"><span data-stu-id="69417-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span></span>

<span data-ttu-id="69417-150">Из объекта ответа можно извлечь текст, а согласно RFC 7622 ответ должен быть объектом JSON и содержать как минимум свойство с именем `active` , которое является логическим значением.</span><span class="sxs-lookup"><span data-stu-id="69417-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="69417-151">Если `active` имеет значение "true", маркер считается допустимым.</span><span class="sxs-lookup"><span data-stu-id="69417-151">When `active` is true then the token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="69417-152">Отчеты об ошибках</span><span class="sxs-lookup"><span data-stu-id="69417-152">Reporting failure</span></span>
<span data-ttu-id="69417-153">Для обнаружения недопустимого маркера используется политика `<choose>` , и, если маркер является недопустимым, возвращается ответ 401.</span><span class="sxs-lookup"><span data-stu-id="69417-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="69417-154">Согласно документу [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3), содержащему сведения об использовании маркеров `bearer`, вместе с ответом 401 также возвращается заголовок `WWW-Authenticate`.</span><span class="sxs-lookup"><span data-stu-id="69417-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span></span> <span data-ttu-id="69417-155">WWW-Authenticate предназначен для предоставления клиенту сведений о создании надлежащим образом авторизованного запроса.</span><span class="sxs-lookup"><span data-stu-id="69417-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span></span> <span data-ttu-id="69417-156">Наличие множества разнообразных подходов, действующих в рамках платформы OAuth2, делает передачу всех необходимых данных довольно сложной задачей.</span><span class="sxs-lookup"><span data-stu-id="69417-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span></span> <span data-ttu-id="69417-157">К счастью, существуют возможности, позволяющие [клиентам узнать о правильной авторизации запросов к серверу ресурсов](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="69417-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="69417-158">Окончательное решение</span><span class="sxs-lookup"><span data-stu-id="69417-158">Final solution</span></span>
<span data-ttu-id="69417-159">Объединив все составляющие, мы получим следующую политику.</span><span class="sxs-lookup"><span data-stu-id="69417-159">Putting all the pieces together, we get the following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request to Token Server to validate token (see RFC 7662) -->
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

<span data-ttu-id="69417-160">Это только один из многочисленных примеров использования политики `send-request` для интеграции полезных внешних служб в процесс выполнения запросов и получения ответов, реализуемый через службу управления API.</span><span class="sxs-lookup"><span data-stu-id="69417-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="69417-161">Структура ответа</span><span class="sxs-lookup"><span data-stu-id="69417-161">Response Composition</span></span>
<span data-ttu-id="69417-162">Политику `send-request` можно использовать для совершенствования основного запроса к серверной системе (как показано в предыдущем примере) или в качестве полной замены вызова серверной части.</span><span class="sxs-lookup"><span data-stu-id="69417-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span></span> <span data-ttu-id="69417-163">С помощью этой методики можно легко создавать сложные ресурсы, которые объединяются из нескольких разных систем.</span><span class="sxs-lookup"><span data-stu-id="69417-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="69417-164">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="69417-164">Building a dashboard</span></span>
<span data-ttu-id="69417-165">Иногда требуется возможность предоставлять информацию, которая существует в нескольких серверных системах, для улучшения взаимодействия с панелью мониторинга.</span><span class="sxs-lookup"><span data-stu-id="69417-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span></span> <span data-ttu-id="69417-166">Ключевые показатели эффективности поставляются из разных серверных систем, но вы не хотите предоставлять к ним прямой доступ и планируете получать все данные в одном запросе.</span><span class="sxs-lookup"><span data-stu-id="69417-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span></span> <span data-ttu-id="69417-167">Возможно, некоторые извлеченные сведения потребуется сначала секционировать, фрагментировать и немного очистить.</span><span class="sxs-lookup"><span data-stu-id="69417-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="69417-168">Возможность кэширования составного ресурса будет полезна для снижения нагрузки серверной части, поскольку вам известно, что пользователи имеют привычку многократно нажимать клавишу F5, чтобы увидеть изменение показателей низкой производительности.</span><span class="sxs-lookup"><span data-stu-id="69417-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span></span>    

### <a name="faking-the-resource"></a><span data-ttu-id="69417-169">Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="69417-169">Faking the resource</span></span>
<span data-ttu-id="69417-170">Первым шагом в создании ресурса панели мониторинга является настройка новой операции на портале издателя управления API.</span><span class="sxs-lookup"><span data-stu-id="69417-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span></span> <span data-ttu-id="69417-171">Это будет операция с заполнителем, используемая для настройки политики построения для создания динамического ресурса.</span><span class="sxs-lookup"><span data-stu-id="69417-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span></span>

![Операция панели мониторинга](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-the-requests"></a><span data-ttu-id="69417-173">Выполнение запросов</span><span class="sxs-lookup"><span data-stu-id="69417-173">Making the requests</span></span>
<span data-ttu-id="69417-174">После создания операции `dashboard` можно настроить политику специально для этой операции.</span><span class="sxs-lookup"><span data-stu-id="69417-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Операция панели мониторинга](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="69417-176">Первым шагом является извлечение всех параметров запроса из входящего запроса, чтобы их можно было переслать в серверную часть.</span><span class="sxs-lookup"><span data-stu-id="69417-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span></span> <span data-ttu-id="69417-177">В этом примере на панели мониторинга сведения отображаются на основе определенного периода времени, поэтому здесь присутствуют параметры `fromDate` и `toDate`.</span><span class="sxs-lookup"><span data-stu-id="69417-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="69417-178">С помощью политики `set-variable` можно извлечь сведения из URL-адреса запроса.</span><span class="sxs-lookup"><span data-stu-id="69417-178">We can use the `set-variable` policy to extract the information from the request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="69417-179">После получения этой информации можно выполнять запросы ко всем серверным системам.</span><span class="sxs-lookup"><span data-stu-id="69417-179">Once we have this information we can make requests to all the backend systems.</span></span> <span data-ttu-id="69417-180">Каждый запрос создает новый URL-адрес со сведениями о параметрах, вызывает соответствующий сервер и сохраняет ответ в переменной контекста.</span><span class="sxs-lookup"><span data-stu-id="69417-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span></span>

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

<span data-ttu-id="69417-181">Эти запросы выполняются последовательно, что не очень удобно.</span><span class="sxs-lookup"><span data-stu-id="69417-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="69417-182">В предстоящем выпуске будет представлена новая политика с именем `wait` , которая обеспечит параллельное выполнение всех этих запросов.</span><span class="sxs-lookup"><span data-stu-id="69417-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="69417-183">Ответы на запросы</span><span class="sxs-lookup"><span data-stu-id="69417-183">Responding</span></span>
<span data-ttu-id="69417-184">Для формирования составного запроса можно использовать политику [возврата ответа](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) .</span><span class="sxs-lookup"><span data-stu-id="69417-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="69417-185">Элемент `set-body` может применять выражение для создания нового `JObject` со всеми представлениями компонентов, внедренными в качестве свойств.</span><span class="sxs-lookup"><span data-stu-id="69417-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span></span>

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

<span data-ttu-id="69417-186">Законченная политика выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="69417-186">The complete policy looks as follows:</span></span>

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

<span data-ttu-id="69417-187">В конфигурации операции заполнителя можно настроить ресурс панели мониторинга для кэширования в течение как минимум часа, поскольку согласно своей природе, даже если данные устарели на час, они все равно будут достаточно эффективными для передачи пользователям.</span><span class="sxs-lookup"><span data-stu-id="69417-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span></span>

## <a name="summary"></a><span data-ttu-id="69417-188">Сводка</span><span class="sxs-lookup"><span data-stu-id="69417-188">Summary</span></span>
<span data-ttu-id="69417-189">Служба управления API Azure предоставляет гибкие политики, выборочно применяемые к HTTP-трафику, и позволяет формировать серверные службы.</span><span class="sxs-lookup"><span data-stu-id="69417-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="69417-190">Если вы хотите усовершенствовать имеющийся шлюз API за счет функций оповещения, проверки или создать новые сложные ресурсы на основе нескольких серверных служб, `send-request` и связанные политики предоставят вам широкий диапазон новых возможностей.</span><span class="sxs-lookup"><span data-stu-id="69417-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="69417-191">Посмотрите видеообзор этих политик.</span><span class="sxs-lookup"><span data-stu-id="69417-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="69417-192">Дополнительные сведения о политиках [отправки одностороннего запроса](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [запроса на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) и [возврата ответа](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse), которые рассматриваются в этой статье, см. в следующем видеоролике.</span><span class="sxs-lookup"><span data-stu-id="69417-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

