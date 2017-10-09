---
title: "aaaTesting функции Azure | Документы Microsoft"
description: "Тестирование функций Azure с помощью Postman, cURL и Node.js."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, webhook, динамические вычисления, независимая архитектура, тестирование"
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a>Методика тестирования кода с помощью Функций Azure

В этом разделе показаны различные функции tootest способами, включая использование hello следующие общие подходы hello:

+ инструменты на основе HTTP, например cURL, Postman и даже веб-браузер для веб-триггеров;
+ Azure Storage Explorer tootest триггеры, основанные на хранилища Azure
+ Вкладка теста на портале Azure функции hello
+ активируемая по таймеру функция;
+ приложение или платформа для тестирования.

Все эти методы тестирования использовать функцию триггер HTTP, принимающее вводимые данные через текст запроса hello или параметр строки запроса. В первом разделе hello создания этой функции.

## <a name="create-a-function-for-testing"></a>Создание функции для тестирования
Для большей части этого учебника мы используем немного измененной версии шаблона функции HttpTrigger JavaScript, который будет использоваться при создании функции hello. Если вам нужна помощь при создании функции, просмотрите этот [учебник](functions-create-first-azure-function.md). Выберите hello **HttpTrigger - JavaScript** шаблона при создании тестовой функции hello в hello [портал Azure].

Hello шаблона функции по умолчанию является по сути «hello world» функцией, выводящий имя серверной hello из hello запроса текст или параметром строки запроса, `name=<your name>`.  Мы обновим кода hello tooalso позволяют tooprovide hello имя и адрес как содержимое JSON в теле запроса hello. Затем функция hello возвращает эти задней toohello клиента при ее наличии.   

Добавьте функции hello hello, следующий код, который мы будет использовать для тестирования:

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a>Тестирование функции с помощью инструментов
За пределами hello портал Azure существуют различные инструменты, можно использовать tootrigger функций для тестирования. К ним относятся инструменты тестирования HTTP на основе пользовательского интерфейса или командной строки, средства доступа к службе хранилища Azure и даже простой веб-браузер.

### <a name="test-with-a-browser"></a>Тестирование с помощью браузера
веб-обозреватель Hello — функций tootrigger простым способом через HTTP. Браузер можно использовать для запросов GET, в которых не требуются полезные данные текста, а применяются только параметры строки запроса.

было определено ранее, hello копирования функции hello tootest **URL-адрес функции** из портала hello. Он имеет hello следующие формы:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Добавление hello `name` параметр строки запроса toohello. Использовать фактическое имя для hello `<Enter a name here>` заполнителя.

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

URL-адрес hello вставить в браузере и должны получить ответ аналогичные toohello следующее.

![Снимок экрана: вкладка браузера Chrome с ответом теста](./media/functions-test-a-function/browser-test.png)

Данный пример является браузера Chrome hello, который создает оболочку для hello вернул строку в формате XML. Другие обозреватели отображают только hello строковое значение.

На портале hello **журналы** вывода окна, аналогичные toohello ниже регистрируется при выполнении функции hello:

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a>Тестирование с помощью приложения Postman
Рекомендуется использовать средство tootest Hello большинство функций — почтальон, который интегрируется с браузера Chrome hello. в разделе tooinstall почтальон, [получить почтальон](https://www.getpostman.com/). Приложение Postman позволяет контролировать намного больше атрибутов HTTP-запроса.

> [!TIP]
> Средство hello HTTP тестирования, наиболее вы знакомы с. Ниже приведены некоторые tooPostman альтернативных вариантов.  
>
> * [Fiddler](http://www.telerik.com/fiddler)  
> * [Paw.](https://luckymarmot.com/paw)  
>
>

функция hello tootest с текстом запроса в почтальон:

1. Запуск из hello почтальон **приложений** кнопку в hello верхнего левого угла окна браузера Chrome.
2. Скопируйте **URL-адрес функции** и вставьте его в Postman. Он включает параметр строки запроса доступа к коду hello.
3. Изменение метода hello HTTP слишком**POST**.
4. Нажмите кнопку **текст** > **необработанные**и добавьте аналогичные toohello следующий текст запроса JSON:

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. Нажмите кнопку **Send**(Отправить).

Hello ниже приведен пример функции простые эхо тестирования hello в этом учебнике.

![Снимок экрана: пользовательский интерфейс Postman](./media/functions-test-a-function/postman-test.png)

На портале hello **журналы** вывода окна, аналогичные toohello ниже регистрируется при выполнении функции hello:

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a>Тестирование с помощью перелистывание из командной строки hello
Часто при тестировании программного обеспечения не необходимые toolook любое дальнейшей, чем hello командной строки toohelp отладки приложения. То же самое справедливо и для функций. Обратите внимание, что перелистывание hello доступность по умолчанию в системах под управлением Linux. В Windows, необходимо сначала загрузить и установить hello [перелистывание средство](https://curl.haxx.se/).

функция tootest hello, что было определено ранее, hello копирования **URL-адрес функции** из портала hello. Он имеет hello следующие формы:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Это hello URL-адрес для запуска функции. Проверить это с помощью команды перелистывание hello в командной строке toomake hello GET (`-G` или `--get`) запрос к функции hello:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Для этого конкретного примера требуются параметр строки запроса, которую можно передать в качестве данных (`-d`) в hello cURL команды:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

Команда выполнения hello, отобразится hello следующие выходные данные функции hello в командной строке hello:

![Снимок экрана: выходные данные в командной строке](./media/functions-test-a-function/curl-test.png)

На портале hello **журналы** вывода окна, аналогичные toohello ниже регистрируется при выполнении функции hello:

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a>Тестирование триггера больших двоичных объектов с помощью Storage Explorer
Функцию триггера больших двоичных объектов можно протестировать с помощью [Azure Storage Explorer](http://storageexplorer.com/).

1. В hello [портал Azure] функции приложения, создайте функцию триггер больших двоичных объектов C#, F # и JavaScript. Задать hello toomonitor toohello путь контейнера больших двоичных объектов. Например:

        files
2. Нажмите кнопку hello  **+**  кнопку tooselect или создать учетную запись хранения hello требуется toouse. Затем щелкните **Создать**.
3. Создайте текстовый файл с после текста hello и сохраните его:

        A text file for blob trigger function testing.
4. Запустите [обозреватель хранилищ Azure](http://storageexplorer.com/)и соедините контейнер больших двоичных объектов toohello в учетной записи хранения hello отслеживается.
5. Нажмите кнопку **отправить** tooupload hello текстовый файл.

    ![Снимок экрана: Storage Explorer](./media/functions-test-a-function/azure-storage-explorer-test.png)

Код функции триггера больших двоичных объектов по умолчанию Hello сообщает обработки hello hello большого двоичного объекта в журналы hello:

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a>Тестирование функции в рамках функций
Hello Azure функции портал предназначен toolet проверки HTTP и таймер запускается функции. Можно также создать tootrigger функции других функций, которые вы тестируете.

### <a name="test-with-hello-functions-portal-run-button"></a>Тестирование с помощью портала кнопку запуска hello функции
Предоставляет портал Hello **запуска** кнопки, которые можно использовать некоторые toodo ограниченный тестирования. Текст запроса можно предоставить с помощью кнопки hello, но не может предоставить параметры строки запроса или обновления заголовков запроса.

Проверить функцию триггер hello HTTP, созданную ранее, добавив в hello JSON строка аналогичные toohello после **текст запроса** поля. Нажмите кнопку hello **запуска** кнопки.

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

На портале hello **журналы** вывода окна, аналогичные toohello ниже регистрируется при выполнении функции hello:

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a>Тестирование с помощью триггера таймера
Некоторые функции не удается проверить адекватно с упомянутых ранее средств hello. Например, функцию триггера очереди, которая выполняется при поступлении сообщения в [хранилище очередей Azure](../storage/queues/storage-dotnet-how-to-use-queues.md). Можно всегда написать код toodrop сообщения в очереди, и соответствующий пример приведен в проект консольного приложения предоставляется далее в этой статье. Однако существует другой подход, который можно использовать для непосредственного тестирования функций.  

Можно использовать триггер таймера, настроенный с привязкой для вывода очереди. Этот код триггера таймера можно написать тест сообщений hello toohello в очереди. В этом разделе описан пример.

Дополнительные сведения об использовании привязок с помощью функций Azure, в разделе hello [Справочник разработчика Azure функции](functions-reference.md).

#### <a name="create-a-queue-trigger-for-testing"></a>Создание триггера очереди для тестирования
toodemonstrate этого подхода сначала создается функция очереди триггера, мы хотим tootest для очереди с именем `queue-newusers`. Эта функция обрабатывает имя и адрес нового пользователя, поступившие в хранилище очередей.

> [!NOTE]
> При использовании имени другую очередь, убедитесь, что используется имя hello соответствует toohello [именование очередей и метаданные](https://msdn.microsoft.com/library/dd179349.aspx) правила. В противном случае возникает ошибка.
>
>

1. В hello [портал Azure] функции приложения, щелкните **новая функция** > **QueueTrigger - C#**.
2. Введите имя toobe hello очереди, отслеживаемый с помощью функции hello очереди:

        queue-newusers
3. Нажмите кнопку hello  **+**  кнопку tooselect или создать учетную запись хранения hello требуется toouse. Затем щелкните **Создать**.
4. Не закрывайте это окно браузера портала, можно наблюдать за hello записи в журнале для hello очереди функции шаблона по умолчанию.

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a>Создайте триггер таймера toodrop сообщение в очередь hello
1. Откройте hello [портал Azure] в новом окне браузера и перейдите tooyour функции приложения.
2. Щелкните **Новая функция** > **TimerTrigger — C#**. Введите выражение cron tooset частоту hello таймера код проверяет работу очереди. Затем щелкните **Создать**. Если требуется toorun теста hello каждые 30 секунд, можно использовать hello следующие [выражение CRON](https://wikipedia.org/wiki/Cron#CRON_expression):

        */30 * * * * *
3. Нажмите кнопку hello **Интеграция** вкладка нового таймера триггера.
4. В разделе **Выходные данные** щелкните **+ Новое выходное значение**. Затем последовательно щелкните **Очередь** и **Выбрать**.
5. Имя заметки hello, используйте для hello **объект очереди сообщений**. Можно использовать в коде функции hello таймера.

        myQueue
6. Введите имя очереди hello, куда отправлять сообщение hello:

        queue-newusers
7. Нажмите кнопку hello  **+**  кнопку tooselect учетной записи хранилища hello ранее используется с триггером очереди hello. Нажмите кнопку **Сохранить**.
8. Нажмите кнопку hello **разработка** вкладку, триггер таймера.
9. Привет, следующий код для функции таймера hello C#, можно использовать при условии, что вы использовали hello же очереди сообщений имя объекта, показанного выше. Нажмите кнопку **Сохранить**.

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

На этом этапе hello таймера функции C# выполняется каждые 30 секунд, если используется выражение cron hello. Каждый выполнение отчета Hello журналы для функции hello таймера:

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

В окне браузера hello для функции hello очереди можно увидеть каждого обрабатываемого сообщения:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a>Тестирование функции с помощью кода
Может потребоваться toocreate внешних tootest приложение или платформу функций.

### <a name="test-an-http-trigger-function-with-code-nodejs"></a>Тестирование функции HTTP-триггера с помощью кода: Node.js
Можно использовать функции tooexecute приложение Node.js tootest запроса HTTP.
Убедитесь, что tooset:

* Hello `host` в узел приложения tooyour функции hello запроса параметров.
* Имя функции в hello `path`.
* Код доступа (`<your code>`) в hello `path`.

Пример кода:

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


Выходные данные:

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

На портале hello **журналы** вывода окна, аналогичные toohello ниже регистрируется при выполнении функции hello:

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a>Тестирование функции триггера очереди с помощью кода: C# #
Упоминалось ранее, можно выполнить проверку очереди триггера с помощью кода toodrop сообщения в очереди. Привет, следующий пример кода основан на hello C# кода, представленного в hello [Приступая к работе с хранилищем очередей Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) учебника. По этой ссылке также доступен код для других языков.

tootest этот код в консольном приложении, необходимо:

* [Настройка строки подключения хранилища в файле app.config hello](../storage/queues/storage-dotnet-how-to-use-queues.md).
* Передайте `name` и `address` как приложение toohello параметров. Например, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`. (Этот код hello имя и адрес для нового пользователя в качестве принимает аргументы командной строки во время выполнения.)

Пример кода C#:

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

В окне браузера hello для функции hello очереди можно увидеть каждого обрабатываемого сообщения:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[портал Azure]: https://portal.azure.com
