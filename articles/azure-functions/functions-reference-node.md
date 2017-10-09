---
title: "Справочник разработчика aaaJavaScript для функций Azure | Документы Microsoft"
description: "Понять, как toodevelop функционирует с использованием JavaScript."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, веб-перехватчики, динамические вычисления, независимая архитектура"
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a>Руководство разработчика JavaScript для Функций Azure
> [!div class="op_single_selector"]
> * [Сценарий C#](functions-reference-csharp.md)
> * [Скрипт F#](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

Здравствуйте взаимодействие JavaScript для функций Azure позволяет легко tooexport функции, которая передается в качестве `context` объекта для взаимодействия со средой выполнения hello и для получения и отправки данных с помощью привязки.

В этой статье предполагается, что вы прочитали hello [Справочник разработчика Azure функции](functions-reference.md).

## <a name="exporting-a-function"></a>Экспорт функции
Все функции JavaScript необходимо экспортировать один `function` через `module.exports` для среды выполнения hello toofind функции hello и запустите его. Эта функция должна всегда включать объект `context` .

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

Привязки `direction === "in"` передаются как аргументы функции, которая означает, что можно использовать [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically обрабатывать новые входные данные (например, с помощью `arguments.length` tooiterate через все входные данные). Эта возможность удобна, когда у вас есть только триггер без дополнительных входных данных, так как к данным триггера можно обращаться напрямую, без ссылки на объект `context`.

всегда Hello аргументы передаются функции toohello в порядке hello, в котором они расположены в *function.json*, даже если не указать их в операторе экспортов. Например, если у вас есть `function(context, a, b)` и измените его слишком`function(context, a)`, можно получить значение hello `b` в коде функции с помощью ссылки слишком`arguments[3]`.

Все привязки, независимо от направления, также передаются на hello `context` (см. раздел hello, выполнив сценарий). 

## <a name="context-object"></a>Объект context
Hello среда выполнения использует `context` tooand данные toopass объекта из функции и toolet взаимодействовать со средой выполнения hello.

Hello объекта контекста всегда tooa функции первого параметра hello и должен быть включен, так как он содержит методы, такие как `context.done` и `context.log`, которой не требуется toouse hello выполнения правильно. Можно присвоить имя hello объекта будет угодно (например, `ctx` или `c`).

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a>Свойство context.bindings

```
context.bindings
```
Возвращает именованный объект, который содержит все входные и выходные данные. Здравствуйте, например, следующая определение привязки в вашей *function.json* позволяет выполнять доступ к hello содержимое очереди hello из hello `context.bindings.myInput` объекта. 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a>Метод context.done
```
context.done([err],[propertyBag])
```

Информирует выполнения hello, завершения вашего кода. Необходимо вызвать метод `context.done`, или else среды выполнения hello никогда не знает, что функции завершена, и выполнения hello выдаст ошибку времени ожидания. 

Hello `context.done` метод позволяет toopass резервное toohello пользовательской ошибки среды выполнения и контейнер свойств, свойств, которые перезаписывают hello свойства hello `context.bindings` объекта.

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a>Метод context.log  

```
context.log(message)
```
Позволяет журналов toohello потоковой передачи toowrite консоли на уровне трассировки по умолчанию hello. На `context.log`, дополнительные записи в журнал методы доступны, позволяют писать toohello журнала консоли на других уровнях трассировки:


| Метод                 | Описание                                |
| ---------------------- | ------------------------------------------ |
| **error(_message_)**   | Записывает tooerror уровень ведения журнала или ниже.   |
| **warn(_message_)**    | Записывает toowarning уровень ведения журнала или ниже. |
| **info(_message_)**    | Записывает tooinfo уровень ведения журнала или ниже.    |
| **verbose(_message_)** | Записывает tooverbose уровня ведения журнала.           |

Hello следующий пример записывает toohello консоли на уровне трассировки hello предупреждений:

```javascript
context.log.warn("Something has happened."); 
```
Можно задать порог hello уровень трассировки для ведения журнала в файле host.json hello, или отключите его.  Дополнительные сведения о как журналы toowrite toohello hello следующем разделе.

## <a name="binding-data-type"></a>Тип данных привязки

toodefine для привязки ввода, тип данных hello использовать hello `dataType` свойство в определении hello привязки. Например, tooread hello содержимого HTTP-запроса в двоичном формате, используйте тип hello `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Другие варианты для `dataType` — `stream` и `string`.

## <a name="writing-trace-output-toohello-console"></a>Консоль toohello выходные данные трассировки записи 

В функциях, используйте hello `context.log` консоли toohello выходные данные трассировки toowrite методы. На этом этапе нельзя использовать `console.log` toowrite toohello консоли.

При вызове `context.log()`, сообщение записывается toohello консоли на уровень трассировки по умолчанию hello, являющийся hello _сведения_ уровень трассировки. Hello следующий код записывает toohello консоли на уровне трассировки hello сведения:

```javascript
context.log({hello: 'world'});  
```

Hello выше код является эквивалентные toohello следующий код:

```javascript
context.log.info({hello: 'world'});  
```

Hello следующий код записывает toohello консоли на уровне ошибки hello:

```javascript
context.log.error("An error has occurred.");  
```

Поскольку _ошибка_ hello наибольший трассировка уровня, это происходит запись трассировки toohello вывода на всех уровнях трассировки при условии, что включено ведение журнала.  


Все `context.log` методы поддерживают hello совпадает с форматом параметра, поддерживаемый hello Node.js [util.format метод](https://nodejs.org/api/util.html#util_util_format_format). Рассмотрим следующий код, который записывает toohello консоли, используя уровень трассировки по умолчанию hello hello.

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

Вы также можете же код в кодировке hello hello записи:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a>Настройка hello уровня трассировки для ведения журнала консоли

Функции можно определить уровень трассировки hello пороговое значение для записи toohello консоли, что делает его легко toocontrol hello способ трассировки записываются toohello консоли из функций. Пороговое значение hello tooset для всех трассировок, записанных toohello консоли используйте hello `tracing.consoleLevel` свойство в файле host.json hello. Этот параметр применяется tooall функций в вашем приложении функции. Hello следующий пример устанавливает hello пороговое значение tooenable подробное ведение журнала трассировки.

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

Значения **consoleLevel** соответствуют имена toohello hello `context.log` методы. задать все трассировки, ведения журнала консоли toohello toodisable **consoleLevel** too_off_. Дополнительные сведения о файле host.json hello см. в разделе hello [host.json справочном разделе](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

## <a name="http-triggers-and-bindings"></a>Триггеры и привязки HTTP

HTTP и веб-перехватчика триггеры HTTP вывода и использовать привязки запроса и ответа объекты toorepresent hello HTTP системы обмена сообщениями.  

### <a name="request-object"></a>Объект запроса

Hello `request` объект имеет hello следующие свойства:

| Свойство      | Описание                                                    |
| ------------- | -------------------------------------------------------------- |
| _body_        | Объект, содержащий текст hello hello запроса.               |
| _headers_     | Объект, содержащий заголовки запроса hello.                   |
| _method_      | Здравствуйте, метод HTTP запроса hello.                                |
| _originalUrl_ | URL-адрес Hello hello запроса.                                        |
| _params_      | Объект, содержащий параметры маршрутизации hello hello запроса. |
| _query_       | Объект, содержащий параметры запроса hello.                  |
| _rawBody_     | текст Hello приветственное сообщение как строку.                           |


### <a name="response-object"></a>Объект ответа

Hello `response` объект имеет hello следующие свойства:

| Свойство  | Описание                                               |
| --------- | --------------------------------------------------------- |
| _body_    | Объект, содержащий текст hello hello ответа.         |
| _headers_ | Объект, содержащий заголовки ответа hello.             |
| _isRaw_   | Указывает, что форматирование пропущена для hello ответа.    |
| _состояние_  | Здравствуйте, код состояния HTTP ответа hello.                     |

### <a name="accessing-hello-request-and-response"></a>Доступ к hello запросов и ответов 

При работе с триггерами HTTP, вы можете использовать hello HTTP объекты запроса и ответа в любом из трех способов:

+ Из hello с именем входа и выхода привязок. Таким образом триггер HTTP hello и привязки hello же, как любые другие привязки. Hello следующий пример задает hello объекта ответа с помощью именованного `response` привязки: 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ Из `req` и `res` свойства hello `context` объекта. Таким образом, данные tooaccess HTTP обычный шаблон hello объекта контекста hello, можно использовать вместо полного hello toouse `context.bindings.name` шаблон. Следующий пример показывает как Hello tooaccess hello `req` и `res` объектов на hello `context`:

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ Путем вызова `context.done()`. Специальный вид привязку HTTP возвращает hello ответ, который передается toohello `context.done()` метод. Hello, выполнив HTTP вывода привязка определяет `$return` выходной параметр:

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    Привязка для вывода предполагается, что вы toosupply hello ответа при вызове `done()`, как показано ниже:

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a>Управление версиями и пакетами Node
версия узла Hello заблокирован на `6.5.0`. Мы работаем над тем, чтобы добавить поддержку дополнительных версий и настройки для этих версий.

Hello следующие шаги позволяют включить пакеты в приложения функции: 

1. Go слишком`https://<function_app_name>.scm.azurewebsites.net`.

2. Щелкните **Debug Console** (Консоль отладки)  > **CMD**.

3. Go слишком`D:\home\site\wwwroot`и затем перетащите файл вашей package.json toohello **wwwroot** папку в верхней части страницы приветствия hello.  
    Также можно передать файлы tooyour функции приложения по-другому. Дополнительные сведения см. в разделе [как tooupdate функция файлов приложения](functions-reference.md#fileupdate). 

4. После передачи файла package.json hello запустите hello `npm install` в hello **консоли удаленного выполнения Kudu**.  
    Это действие загружает пакеты hello, указанный в файле package.json hello и перезапускает приложение функции hello.

После hello необходимые пакеты установлены, импорте tooyour функции путем вызова `require('packagename')`, как показано в следующий пример hello:

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

Следует определить `package.json` файла в корне hello функции приложения. Определение hello файл разрешает все функции в папке приложения hello hello же кэшированные пакеты, что дает hello наилучшей производительности. Если возникает конфликт версий, можно разрешить ее, добавив `package.json` файл в папке hello конкретной функции.  

## <a name="environment-variables"></a>Переменные среды
tooget переменной среды или значение параметра приложения, используйте `process.env`, как показано в следующем примере кода hello:

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a>Рекомендации для функций JavaScript

При работе с функции JavaScript, помните о hello рекомендации в следующих двух разделах hello.

### <a name="choose-single-core-app-service-plans"></a>Выбор одноядерных планов службы приложений

При создании функции приложения, в котором используется hello план служб приложений, рекомендуется выбрать план одним ядром, а не план с несколькими ядрами. В настоящее время функции выполняется функции JavaScript более эффективно на виртуальных машинах одноядерный и с использованием большего размера виртуальных машин не дает hello ожидаемого улучшения производительности. При необходимости вы можете вручную добавить дополнительные экземпляры одноядерных виртуальных машин или включить автоматическое масштабирование. Дополнительные сведения см. в статье [Масштабирование числа экземпляров вручную или автоматически](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).    

### <a name="typescript-and-coffeescript-support"></a>Поддержка TypeScript и CoffeeScript
Поскольку Прямая поддержка еще не существует для компиляции автоматически TypeScript или CoffeeScript через hello среды выполнения, такая поддержка должен toobe обрабатывается вне среды hello во время развертывания. 

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello следующие ресурсы:

* [Рекомендации по функциям Azure](functions-best-practices.md)
* [Справочник разработчика по функциям Azure](functions-reference.md)
* [Справочник разработчика C# по функциям Azure](functions-reference-csharp.md)
* [Справочник разработчика F# по Функциям Azure](functions-reference-fsharp.md)
* [Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)](functions-triggers-bindings.md)

