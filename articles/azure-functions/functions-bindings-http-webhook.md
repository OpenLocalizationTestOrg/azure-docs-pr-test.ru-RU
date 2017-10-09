---
title: "привязки функции HTTP и веб-перехватчика aaaAzure | Документы Microsoft"
description: "Понять, каким образом toouse HTTP и веб-перехватчика триггеры и привязки в функциях Azure."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, webhook, динамические вычисления, бессерверная архитектура, HTTP, API, REST"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a>Привязки HTTP и webhook в функциях Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

В этой статье объясняется, как триггеры tooconfigure и работа с HTTP и привязками в функциях Azure.
С этими можно использовать функции Azure toobuild без сервера API-интерфейсов и отправки ответа toowebhooks.

Функции Azure предоставляет следующие привязки hello:
- [Триггер HTTP](#httptrigger) позволяет вызвать функцию с помощью HTTP-запроса. Это может быть слишком настраиваемые toorespond[веб-перехватчиков](#hooktrigger).
- [Привязка для вывода HTTP](#output) позволяет toorespond toohello запроса.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a>Триггер HTTP
функция будет выполняться в триггер HTTP Hello в ответ tooan HTTP-запроса. Его можно настраивать определенный URL-адрес toorespond tooa или набор методов HTTP. Триггер HTTP также может быть настроенный toorespond toowebhooks. 

Если с помощью портала функции hello, можно также начинается немедленно с помощью готового шаблона. Выберите **новая функция** и выберите команду «Веб-перехватчиков & API» hello **сценарий** раскрывающегося списка. Выберите один из шаблонов hello и нажмите кнопку **создать**.

По умолчанию триггер HTTP будет отвечать toohello запрос с кодом состояния HTTP 200 OK и пустой текст. toomodify ответ hello, настройте [привязка для вывода HTTP](#output)

### <a name="configuring-an-http-trigger"></a>Настройка триггера HTTP
Определен триггер HTTP, включая JSON объект аналогичные toohello, выполнив в hello `bindings` массив function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
Привязка Hello поддерживает hello следующие свойства:

* **имя** : требуется "-" hello переменной имя, используемое в коде функция для запроса hello или текст запроса. См. раздел [Использование триггера HTTP в коде программы](#httptriggerusage).
* **Тип** : требуется — должен быть задан слишком «httpTrigger».
* **Направление** : требуется - должно быть задано слишком «in».
* _authLevel_ : Определяет, какие ключи, должны toobe есть в запросе hello в функции hello tooinvoke заказа. См. раздел [Работа с ключами](#keys) далее в этой статье. Hello значение может быть одним из следующих hello:
    * _anonymous_: ключи API не требуются.
    * _function_: требуется ключ API для конкретной функции. Это значение по умолчанию hello, если не указан.
    * _Администратор_ : hello главный ключ не требуется.
* **методы** : это массив будет отвечать функции hello toowhich методы hello HTTP. Если не указано, функция hello ответит tooall HTTP-методов. В разделе [Настройка конечной точки hello HTTP](#url).
* **маршрут** : Определяет шаблон маршрута hello, управление toowhich URL-адресов будет отвечать функции запроса. Hello значение по умолчанию, если не указан — `<functionname>`. В разделе [Настройка конечной точки hello HTTP](#url).
* **webHookType** : Это настраивает tooact триггер hello HTTP в качестве веб-перехватчика получателем для указанного поставщика hello. Hello _методы_ свойство не должно быть установлено, если вы выбрали это. В разделе [toowebhooks отвечает](#hooktrigger). Hello значение может быть одним из следующих hello:
    * _genericJson_: конечная точка webhook общего назначения без логики для конкретного поставщика.
    * _github_ : функции hello ответит tooGitHub веб-привязок. Hello _authLevel_ свойство не должно быть установлено, если вы выбрали это.
    * _резерв_ : функции hello ответит tooSlack веб-привязок. Hello _authLevel_ свойство не должно быть установлено, если вы выбрали это.

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a>Использование триггера HTTP в коде программы
Для функции C# и F #, можно объявить тип входного toobe ваш триггер hello либо `HttpRequestMessage` или пользовательского типа. При выборе `HttpRequestMessage`, а затем получите объект запроса toohello полный доступ. Для пользовательского типа (например, POCO) функции попытается текст запроса hello tooparse как свойства объекта JSON toopopulate hello.

Для функций, Node.js среда выполнения функции hello предоставляет текст hello запроса вместо hello объекта запроса.

В разделе [Образцы триггеров HTTP](#httptriggersample) приводятся примеры использования.


<a name="output"></a>
## <a name="http-response-output-binding"></a>Привязка для вывода HTTP-ответа
Используйте hello HTTP выходные данные привязки toorespond toohello HTTP отправитель запроса. Эта привязка требует триггер HTTP и позволяет toocustomize hello ответа, связанного с запрос hello триггера. Если привязка для вывода HTTP отсутствует, триггер HTTP возвращает ответ HTTP "200 ОК" с пустым текстом. 

### <a name="configuring-an-http-output-binding"></a>Настройка привязки для вывода HTTP
выходные данные Hello HTTP, включая JSON объект аналогичные toohello, выполнив в hello определена привязка `bindings` массив function.json:

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
Привязка Hello содержит hello следующие свойства:

* **имя** : требуется — имя переменной, используемые в коде функция в ответе hello "hello". См. раздел [Работа с привязкой для вывода HTTP в коде программы](#outputusage).
* **Тип** : требуется — должен быть задан слишком «http».
* **Направление** : требуется - должно быть задано слишком «out».

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a>Работа с привязкой для вывода HTTP в коде программы
Можно использовать hello выходной параметр (например, «res») toorespond toohello http или веб-перехватчика вызывающего объекта. Кроме того, можно использовать стандартные `Request.CreateResponse()` (C#) или `context.res` (Node.JS) шаблон tooreturn ответ пользователя. Примеры как toouse hello последний метод см. в разделе [образцы триггер HTTP](#httptriggersample) и [образцы триггер веб-перехватчика](#hooktriggersample).


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a>Отвечать на запросы toowebhooks
Триггер HTTP с hello _webHookType_ свойство будет иметь настроенное toorespond слишком[веб-перехватчиков](https://en.wikipedia.org/wiki/Webhook). Основная конфигурация Hello использует параметр «genericJson» hello. Это ограничивает запросы tooonly их с помощью HTTP POST и с hello `application/json` тип содержимого.

Hello триггер Кроме того можно специально настроенные tooa конкретного веб-перехватчика поставщика (например, [GitHub](https://developer.github.com/webhooks/) и [Slack](https://api.slack.com/outgoing-webhooks)). Если указан поставщик, среда выполнения функции hello заняться hello поставщика логику проверки для вас.  

### <a name="configuring-github-as-a-webhook-provider"></a>Настройка GitHub в качестве поставщика webhook
веб-привязок tooGitHub toorespond, сначала создайте функции с триггером HTTP и задайте hello _webHookType_ свойство слишком «github». Затем скопируйте его [URL-адрес](#url) и [ключ API](#keys) в репозиторий GitHub, используя страницу **Добавить веб-перехватчик**. Дополнительные сведения см. в разделе документации GitHub [о создании webhook](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409).

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a>Настройка Slack в качестве поставщика webhook
Резерв Hello веб-перехватчика создается маркер вместо позволяет указать, поэтому необходимо настроить ключ конкретными функциями с маркером hello из Slack. См. раздел [Работа с ключами](#keys).

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a>Настройка конечной точки HTTP hello
По умолчанию при создании функции для триггера HTTP или веб-перехватчика, функции hello адресуемые с маршрутом hello формы:

    http://<yourapp>.azurewebsites.net/api/<funcname> 

Вы можете настроить этот маршрут, используя необязательный hello `route` свойство в триггере hello HTTP входных привязки. Пример: hello следующие *function.json* файл определяет `route` свойство для триггера HTTP:

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

Используя эту конфигурацию, функции hello теперь адресуемый с hello следующий маршрут вместо hello исходный маршрут.

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

Это позволяет коду функции hello toosupport двух параметров в адрес hello, «категория» и «id». Для параметров можно использовать любое [ограничение маршрута веб-API](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints). Здравствуйте, следующие функции кода C# используются оба параметра.

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

Ниже приведен код toouse Node.js функции hello такими же параметрами маршрута.

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

По умолчанию все маршруты функций начинаются с префикса *api*. Также можно настроить или удалить с помощью hello префикс hello `http.routePrefix` свойство в вашей *host.json* файла. Hello следующий пример удаляет hello *api* префикс маршрута, используя пустую строку для префикса hello в hello *host.json* файла.

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

Подробные сведения о том, как tooupdate hello *host.json* файл функции, см. в разделе [как tooupdate функция файлов приложения](functions-reference.md#fileupdate). 

Дополнительные сведения о других свойствах, которые можно настроить в файле *host.json*, см. в [справочнике по host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).


<a name="keys"></a>
## <a name="working-with-keys"></a>Работа с ключами
Триггеры HTTP могут использовать ключи для повышения безопасности. Стандартная HttpTrigger можно использовать как ключ API требует hello ключа toobe есть в запросе hello. Веб-привязок можно использовать ключи tooauthorize запросы различными способами, в зависимости от того, какой поставщик hello поддерживает.

Ключи хранятся в Azure в составе приложения-функции в зашифрованном виде. tooview ключей необходимо создать новые или toonew значения ключей данных наката, перейдите tooone функций hello портале и выберите «Управление». 

Существует два типа ключей.
- **Ключи узла**: эти ключи являются общими для всех функций в приложение функции hello. Если используется как ключ API, они позволяют функция tooany доступ в приложении функции hello.
- **Функциональные клавиши**: эти ключи применяются только toohello определенные функции в которых они определены. При использовании в качестве ключа API, эти только разрешить toothat функции доступа.

Каждый ключ имеет имя для ссылки и отсутствует ключ по умолчанию (с именем «default») на уровне функций и узла hello. Hello **главный ключ** ключ узла по умолчанию с именем «_master», определенное для каждой функции приложения и не может быть отменено. Он предоставляет административный доступ toohello API среды выполнения. С помощью `"authLevel": "admin"` в hello привязки JSON потребует этого ключа toobe, представленные в запросе hello; ошибка авторизации приведет к любой другой ключ.

> [!NOTE]
> Из-за toohello повышенные разрешения, предоставляемые hello главный ключ базы данных не следует предоставлять этот ключ третьим лицам или распространять его в собственные клиентские приложения. Соблюдайте осторожность при выборе уровень авторизации администратора hello.
> 
> 

### <a name="api-key-authorization"></a>Проверка подлинности с помощью ключа API
По умолчанию HttpTrigger требуется ключ API в HTTP-запросе hello. Поэтому HTTP-запрос обычно выглядит следующим образом:

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

Hello ключ может быть включено в переменную строки запроса с именем `code`, как описано выше, или он может быть включено в `x-functions-key` заголовка HTTP. значение Hello hello ключа может быть любого сочетания клавиш, определенные для функции hello или ключ любого узла.

Можно выбрать запросы tooallow без ключей или указать, что hello основного ключа необходимо использовать, изменив hello `authLevel` свойство в hello привязки JSON (см. [триггер HTTP](#httptrigger)).

### <a name="keys-and-webhooks"></a>Ключи и вызовы webhook
Авторизация веб-перехватчика обрабатывается компонентом получателем hello веб-перехватчика, часть hello HttpTrigger и механизм hello варьируется в зависимости от типа веб-перехватчика hello. Но каждый из этих механизмов использует ключи. По умолчанию будет использоваться hello функциональную клавишу с именем «default». Если вы хотите toouse другой ключ, необходимо будет tooconfigure hello веб-перехватчика toosend hello имя ключа для поставщика с запросом hello в одном из следующих способов hello:

- **Строка запроса**: hello Поставщик передает имя ключа hello в hello `clientid` параметр строки запроса (например, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).
- **Заголовок запроса**: hello Поставщик передает имя ключа hello в hello `x-functions-clientid` заголовок.

> [!NOTE]
> Ключи функций имеют приоритет над ключами узла. Если два ключа определены с точно такое же имя, hello hello функция ключ будет использоваться.
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a>Образцы триггеров HTTP
Предположим, что имеется следующий триггер HTTP в hello hello `bindings` массив function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

См. Образец hello конкретного языка, выполняющий поиск `name` параметр в строку запроса hello или текста hello hello HTTP-запроса.

* [C#](#httptriggercsharp)
* [F#](#httptriggerfsharp)
* [Node.js](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a>Пример триггера HTTP на языке C# #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

Можно также привязать tooa POCO вместо `HttpRequestMessage`. Это будет структура из текста hello запроса hello, интерпретировать как JSON. Аналогичным образом тип может быть передан вывода ответа toohello HTTP привязки, и это будет возвращаться в виде текста ответа hello, с кодом состояния 200.
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a>Пример триггера HTTP на языке F# #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

Требуется `project.json` файла, который использует NuGet tooreference hello `FSharp.Interop.Dynamic` и `Dynamitey` сборки следующим образом:

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

Это будет использовать NuGet toofetch зависимостей и будет ссылаться на них в скрипте.

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a>Пример триггера HTTP для Node.js
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a>Примеры вызовов webhook
Предположим, что имеется следующая веб-перехватчика триггера в hello hello `bindings` массив function.json:

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

См. Образец hello конкретного языка, зарегистрировавший GitHub проблема комментарии.

* [C#](#hooktriggercsharp)
* [F#](#hooktriggerfsharp)
* [Node.js](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a>Пример веб-перехватчика на языке C# #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a>Пример веб-перехватчика на языке F# #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a>Пример webhook для Node.js
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

