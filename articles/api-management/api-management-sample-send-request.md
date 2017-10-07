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
# <a name="using-external-services-from-hello-azure-api-management-service"></a>Использование внешних служб из hello службы управления API Azure
Hello политик, доступных в службе управления API Azure можно сделать широкий спектр нормальной работе исключительно на основе входящего запроса hello, исходящего ответа hello и сведений об основной конфигурации. Тем не менее, могут toointeract с внешним службам из API управления политики открывает множество новых возможностей.

Мы видели ранее мы взаимодействие с hello [концентратор событий Azure service для ведения журнала, мониторинг и аналитику](api-management-log-to-eventhub-sample.md). В этой статье мы покажем, что служба на основе политик, которые позволяют вам toointeract с любой внешней HTTP. Эти политики можно использовать для запуска удаленных событий или для получения сведений, которые будут используется toomanipulate hello исходного запроса и ответа иным образом.

## <a name="send-one-way-request"></a>Отправка одностороннего запроса
Возможно hello простой внешнего взаимодействия не стиль выстрелил и забыл hello запрос, который позволяет внешней службе toobe уведомление о том, какой-либо важных событий. Мы используем политика потока управления hello `choose` toodetect любого вида условие, которое мы интересуют, а затем, если hello условие выполняется, можно сделать внешних HTTP-запроса с помощью hello [-один способом запрос на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) политики. Это может быть запрос tooa, системы, такие как Hipchat или Slack или почты API, например SendGrid или MailChimp обмена сообщениями или для обращения в службу поддержки критических что-то наподобие PagerDuty. Все эти системы обмена сообщениями обладают простыми API-интерфейсами HTTP, которые можно легко вызвать.

### <a name="alerting-with-slack"></a>Оповещения с использованием Slack
Следующий пример Hello демонстрирует временных резервов чат, если код состояния HTTP-ответа hello больше или равно too500 toosend tooa сообщения. Ошибка диапазона 500 указывает, что проблема с нашей API внутреннего сервера, hello клиента о нашем API не удается разрешить самостоятельно. Обычно требуется вмешательство с нашей стороны.  

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

Резерв имеет hello понятие входящего веб-обработчики. При настройке входящих веб-обработчик, Slack приводит к возникновению ошибки специальный URL-адрес, который позволяет toodo простой запрос POST и toopass сообщение в канале Slack hello. текст JSON, который мы создадим Hello основан на формате, заданном параметром Slack.

![Веб-привязка Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a>Достаточно ли хорош автономный запрос?
Использование автономного запроса связано с некоторыми компромиссами. Если для какой-либо причине hello запрос завершается ошибкой, а затем hello ошибки не будут отображаться. В этом случае конкретной системе отчетов об ошибках получателя и hello дополнительные издержки, связанные Ожидание ответа hello сложности hello могут не поддерживать. Для сценариев, где essential toocheck hello ответа, hello [запрос на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) политики является лучшим вариантом.

## <a name="send-request"></a>запроса на отправку
Hello `send-request` политика позволяет с помощью сложной обработки функций и службы управления toohello API возвращаемых данных, который может использоваться для дальнейшей обработке политики tooperform внешней службы.

### <a name="authorizing-reference-tokens"></a>Авторизация маркеров ссылок
Основная задача API управления состоит в защите серверных ресурсов. Если сервер авторизации hello, используемый API создает [маркеры JWT](http://jwt.io/) как часть его OAuth2 поток как [Azure Active Directory](../active-directory/active-directory-aadconnect.md) так, то можно использовать hello `validate-jwt` допустимость tooverify hello политики токен Hello. Тем не менее, некоторые серверы авторизации создавать, называемых [ссылаться токены](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) без создания сервера авторизации toohello обратного вызова, не могут быть проверены.

### <a name="standardized-introspection"></a>Стандартизованный самоанализ
В прошлом hello был не стандартизированные может проверить токен ссылки с сервера авторизации. Однако недавно Предложенный стандарт [RFC 7662](https://tools.ietf.org/html/rfc7662) опубликовал hello IETF, определяющий, как сервер ресурсов можно проверить действительность hello маркера.

### <a name="extracting-hello-token"></a>Извлечение маркера hello
Hello первым шагом является tooextract hello токен из заголовка авторизации hello. значение заголовка Hello должны иметь формат hello `Bearer` схемы авторизации, пробел и затем hello авторизации токен согласно [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1). К сожалению, существуют случаи, где опущен схему авторизации hello. tooaccount для этого во время синтаксического анализа, мы разделить значение заголовка hello пространство и выберите hello последняя строка из hello, возвращаемый массив строк. Это возможное решение позволяет справиться с неправильно отформатированными заголовками авторизации.

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a>Запрос проверки hello
После получения маркера авторизации hello, можно сделать маркер hello toovalidate hello запроса. RFC 7662 вызывает интроспекции этот процесс и требуется, вы `POST` toohello интроспекции HTML-формы ресурса. Hello HTML-формы по крайней мере должен содержать пару ключ значение с ключом hello `token`. Сервер авторизации toohello этот запрос также должен быть tooensure прошедшего проверку подлинности, который вредоносных клиентов не удается перейти trawling для допустимых маркеров.

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

### <a name="checking-hello-response"></a>Проверка ответов hello
Hello `response-variable-name` атрибут является hello доступа используется toogive отклик. Hello имя, определенное в этом свойстве можно использовать в качестве ключа в hello `context.Variables` tooaccess hello словарь `IResponse` объекта.

Из hello объекта ответа можно извлечь текст hello и RFC 7622 указывает, что hello ответ должен быть объектом JSON и должен содержать по крайней мере свойство с именем `active` , логическое значение. Когда `active` имеет значение true, то токен hello считается допустимым.

### <a name="reporting-failure"></a>Отчеты об ошибках
Мы используем `<choose>` toodetect политики, если hello маркер является недопустимым и если да, возвращают ответ 401.

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

Согласно [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) описано, как `bearer` следует использовать токены, мы также возвращают `WWW-Authenticate` заголовок с ответом hello 401. Привет, WWW-Authenticate является предполагаемым tooinstruct клиента о том, как tooconstruct правильно авторизованный запрос. Из-за toohello различных подходов, возможно с hello OAuth2 framework, трудно toocommunicate hello все необходимые сведения. К счастью существует усилия ведется toohelp [клиентам обнаруживать как tooproperly авторизации запросов tooa ресурсов сервера](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).

### <a name="final-solution"></a>Окончательное решение
Совместное размещение все составляющие hello, мы получаем hello следующие политики:

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

Это только один из многих примеры hello `send-request` политики может быть полезным внешних служб используется toointegrate в процесс hello запросов и ответов, проходящей через hello службы управления API.

## <a name="response-composition"></a>Структура ответа
Hello `send-request` политика может использоваться для повышения серверной системе tooa основного запроса, как было показано в предыдущем примере hello, или он может использоваться как полный замены для внутреннего вызова hello. С помощью этой методики можно легко создавать сложные ресурсы, которые объединяются из нескольких разных систем.

### <a name="building-a-dashboard"></a>Создание панели мониторинга
Иногда требуется toobe может tooexpose данные из нескольких серверных системах, к примеру, toodrive панели мониторинга. Hello ключевые показатели эффективности берутся из разных все назад элементов, но вы предпочитаете не toothem tooprovide прямой доступ и было бы неплохо, если в одном запросе может получить все сведения о hello. Возможно некоторые из сведений о серверной части hello должен некоторые срезы и разделять и немного очистки данных сначала! Выполняется доступ toocache, что составной ресурс будет полезно tooreduce серверной hello загрузить как вам известно, что пользователи имеют привычка подбору паролей hello клавишу F5 в порядке toosee, если их неэффективно метрики могут измениться.    

### <a name="faking-hello-resource"></a>Faking hello ресурсов
Здравствуйте, первый шаг toobuilding нашего ресурса панели мониторинга — tooconfigure новую операцию в портал издателя управления API hello. Это будет tooconfigure заполнитель операции, используемой политики нашей композиции toobuild нашей динамический ресурс.

![Операция панели мониторинга](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a>Создание запросов hello
Здравствуйте, один раз `dashboard` созданный операцией можно настроить политики специально для этой операции. 

![Операция панели мониторинга](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

Hello первым шагом является tooextract все параметры запроса из входящего запроса hello, мы перенаправлять их tooour серверной части. В этом примере на панели мониторинга сведения отображаются на основе определенного периода времени, поэтому здесь присутствуют параметры `fromDate` и `toDate`. Мы используем hello `set-variable` политики tooextract hello сведения из URL-адрес запроса hello.

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

После получения этих сведений можно сделать запросов tooall hello серверных системах. Каждый запрос создает новый URL-адрес с сведения о параметрах hello и вызывает его соответствующий сервер и сохраняет ответ hello в переменной контекста.

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

Эти запросы выполняются последовательно, что не очень удобно. В следующих выпусках Корпорация Майкрософт представит новую политику с именем `wait` , обеспечивающие все эти запросы tooexecute параллельно.

### <a name="responding"></a>Ответы на запросы
tooconstruct hello составной ответ можно использовать hello [возврата ответа](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) политики. Hello `set-body` элемент можно использовать выражение tooconstruct новый `JObject` с все представления компонента hello, внедренных в качестве свойства.

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

политика завершения Hello выглядит следующим образом:

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

В конфигурации hello hello заполнитель операции, которые можно настроить toobe ресурсов панели мониторинга hello в кэше по крайней мере один час пониманием того, что характер hello hello данных означает, что даже если он является устаревшим, он все равно будет достаточно эффективных часа Пользователи toohello tooconvey ценные сведения.

## <a name="summary"></a>Сводка
Служба управления API Azure предоставляет гибкие политики, которые можно выборочно применить tooHTTP трафика и позволяет композиции внутренних служб. Здравствуйте, является ли tooenhance шлюз API с предупреждением, функции, проверки, возможности проверки или создайте новый составной ресурсы в зависимости от нескольких серверных служб, `send-request` и связанные политики откройте мир новых возможностей.

## <a name="watch-a-video-overview-of-these-policies"></a>Посмотрите видеообзор этих политик.
Дополнительные сведения о hello [-один способом запрос на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [запрос на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), и [возврата ответа](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) политики, описанные в данной статье, обратите внимание на следующие видео hello.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

