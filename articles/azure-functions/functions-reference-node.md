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
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="547bf-104">Руководство разработчика JavaScript для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="547bf-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="547bf-105">Сценарий C#</span><span class="sxs-lookup"><span data-stu-id="547bf-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="547bf-106">Скрипт F#</span><span class="sxs-lookup"><span data-stu-id="547bf-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="547bf-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="547bf-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="547bf-108">Здравствуйте взаимодействие JavaScript для функций Azure позволяет легко tooexport функции, которая передается в качестве `context` объекта для взаимодействия со средой выполнения hello и для получения и отправки данных с помощью привязки.</span><span class="sxs-lookup"><span data-stu-id="547bf-108">hello JavaScript experience for Azure Functions makes it easy tooexport a function, which is passed as a `context` object for communicating with hello runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="547bf-109">В этой статье предполагается, что вы прочитали hello [Справочник разработчика Azure функции](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="547bf-109">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="547bf-110">Экспорт функции</span><span class="sxs-lookup"><span data-stu-id="547bf-110">Exporting a function</span></span>
<span data-ttu-id="547bf-111">Все функции JavaScript необходимо экспортировать один `function` через `module.exports` для среды выполнения hello toofind функции hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="547bf-111">All JavaScript functions must export a single `function` via `module.exports` for hello runtime toofind hello function and run it.</span></span> <span data-ttu-id="547bf-112">Эта функция должна всегда включать объект `context` .</span><span class="sxs-lookup"><span data-stu-id="547bf-112">This function must always include a `context` object.</span></span>

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

<span data-ttu-id="547bf-113">Привязки `direction === "in"` передаются как аргументы функции, которая означает, что можно использовать [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically обрабатывать новые входные данные (например, с помощью `arguments.length` tooiterate через все входные данные).</span><span class="sxs-lookup"><span data-stu-id="547bf-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically handle new inputs (for example, by using `arguments.length` tooiterate over all your inputs).</span></span> <span data-ttu-id="547bf-114">Эта возможность удобна, когда у вас есть только триггер без дополнительных входных данных, так как к данным триггера можно обращаться напрямую, без ссылки на объект `context`.</span><span class="sxs-lookup"><span data-stu-id="547bf-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="547bf-115">всегда Hello аргументы передаются функции toohello в порядке hello, в котором они расположены в *function.json*, даже если не указать их в операторе экспортов.</span><span class="sxs-lookup"><span data-stu-id="547bf-115">hello arguments are always passed along toohello function in hello order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="547bf-116">Например, если у вас есть `function(context, a, b)` и измените его слишком`function(context, a)`, можно получить значение hello `b` в коде функции с помощью ссылки слишком`arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="547bf-116">For example, if you have `function(context, a, b)` and change it too`function(context, a)`, you can still get hello value of `b` in function code by referring too`arguments[3]`.</span></span>

<span data-ttu-id="547bf-117">Все привязки, независимо от направления, также передаются на hello `context` (см. раздел hello, выполнив сценарий).</span><span class="sxs-lookup"><span data-stu-id="547bf-117">All bindings, regardless of direction, are also passed along on hello `context` object (see hello following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="547bf-118">Объект context</span><span class="sxs-lookup"><span data-stu-id="547bf-118">context object</span></span>
<span data-ttu-id="547bf-119">Hello среда выполнения использует `context` tooand данные toopass объекта из функции и toolet взаимодействовать со средой выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-119">hello runtime uses a `context` object toopass data tooand from your function and toolet you communicate with hello runtime.</span></span>

<span data-ttu-id="547bf-120">Hello объекта контекста всегда tooa функции первого параметра hello и должен быть включен, так как он содержит методы, такие как `context.done` и `context.log`, которой не требуется toouse hello выполнения правильно.</span><span class="sxs-lookup"><span data-stu-id="547bf-120">hello context object is always hello first parameter tooa function and must be included because it has methods such as `context.done` and `context.log`, which are required toouse hello runtime correctly.</span></span> <span data-ttu-id="547bf-121">Можно присвоить имя hello объекта будет угодно (например, `ctx` или `c`).</span><span class="sxs-lookup"><span data-stu-id="547bf-121">You can name hello object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="547bf-122">Свойство context.bindings</span><span class="sxs-lookup"><span data-stu-id="547bf-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="547bf-123">Возвращает именованный объект, который содержит все входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="547bf-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="547bf-124">Здравствуйте, например, следующая определение привязки в вашей *function.json* позволяет выполнять доступ к hello содержимое очереди hello из hello `context.bindings.myInput` объекта.</span><span class="sxs-lookup"><span data-stu-id="547bf-124">For example, hello following binding definition in your *function.json* lets you access hello contents of hello queue from hello `context.bindings.myInput` object.</span></span> 

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

### <a name="contextdone-method"></a><span data-ttu-id="547bf-125">Метод context.done</span><span class="sxs-lookup"><span data-stu-id="547bf-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="547bf-126">Информирует выполнения hello, завершения вашего кода.</span><span class="sxs-lookup"><span data-stu-id="547bf-126">Informs hello runtime that your code has finished.</span></span> <span data-ttu-id="547bf-127">Необходимо вызвать метод `context.done`, или else среды выполнения hello никогда не знает, что функции завершена, и выполнения hello выдаст ошибку времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="547bf-127">You must call `context.done`, or else hello runtime never knows that your function is complete, and hello execution will time out.</span></span> 

<span data-ttu-id="547bf-128">Hello `context.done` метод позволяет toopass резервное toohello пользовательской ошибки среды выполнения и контейнер свойств, свойств, которые перезаписывают hello свойства hello `context.bindings` объекта.</span><span class="sxs-lookup"><span data-stu-id="547bf-128">hello `context.done` method allows you toopass back both a user-defined error toohello runtime and a property bag of properties that overwrite hello properties on hello `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="547bf-129">Метод context.log</span><span class="sxs-lookup"><span data-stu-id="547bf-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="547bf-130">Позволяет журналов toohello потоковой передачи toowrite консоли на уровне трассировки по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-130">Allows you toowrite toohello streaming console logs at hello default trace level.</span></span> <span data-ttu-id="547bf-131">На `context.log`, дополнительные записи в журнал методы доступны, позволяют писать toohello журнала консоли на других уровнях трассировки:</span><span class="sxs-lookup"><span data-stu-id="547bf-131">On `context.log`, additional logging methods are available that let you write toohello console log at other trace levels:</span></span>


| <span data-ttu-id="547bf-132">Метод</span><span class="sxs-lookup"><span data-stu-id="547bf-132">Method</span></span>                 | <span data-ttu-id="547bf-133">Описание</span><span class="sxs-lookup"><span data-stu-id="547bf-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="547bf-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="547bf-134">**error(_message_)**</span></span>   | <span data-ttu-id="547bf-135">Записывает tooerror уровень ведения журнала или ниже.</span><span class="sxs-lookup"><span data-stu-id="547bf-135">Writes tooerror level logging, or lower.</span></span>   |
| <span data-ttu-id="547bf-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="547bf-136">**warn(_message_)**</span></span>    | <span data-ttu-id="547bf-137">Записывает toowarning уровень ведения журнала или ниже.</span><span class="sxs-lookup"><span data-stu-id="547bf-137">Writes toowarning level logging, or lower.</span></span> |
| <span data-ttu-id="547bf-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="547bf-138">**info(_message_)**</span></span>    | <span data-ttu-id="547bf-139">Записывает tooinfo уровень ведения журнала или ниже.</span><span class="sxs-lookup"><span data-stu-id="547bf-139">Writes tooinfo level logging, or lower.</span></span>    |
| <span data-ttu-id="547bf-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="547bf-140">**verbose(_message_)**</span></span> | <span data-ttu-id="547bf-141">Записывает tooverbose уровня ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="547bf-141">Writes tooverbose level logging.</span></span>           |

<span data-ttu-id="547bf-142">Hello следующий пример записывает toohello консоли на уровне трассировки hello предупреждений:</span><span class="sxs-lookup"><span data-stu-id="547bf-142">hello following example writes toohello console at hello warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="547bf-143">Можно задать порог hello уровень трассировки для ведения журнала в файле host.json hello, или отключите его.</span><span class="sxs-lookup"><span data-stu-id="547bf-143">You can set hello trace-level threshold for logging in hello host.json file, or turn it off.</span></span>  <span data-ttu-id="547bf-144">Дополнительные сведения о как журналы toowrite toohello hello следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="547bf-144">For more information about how toowrite toohello logs, see hello next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="547bf-145">Тип данных привязки</span><span class="sxs-lookup"><span data-stu-id="547bf-145">Binding data type</span></span>

<span data-ttu-id="547bf-146">toodefine для привязки ввода, тип данных hello использовать hello `dataType` свойство в определении hello привязки.</span><span class="sxs-lookup"><span data-stu-id="547bf-146">toodefine hello data type for an input binding, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="547bf-147">Например, tooread hello содержимого HTTP-запроса в двоичном формате, используйте тип hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="547bf-147">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="547bf-148">Другие варианты для `dataType` — `stream` и `string`.</span><span class="sxs-lookup"><span data-stu-id="547bf-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-toohello-console"></a><span data-ttu-id="547bf-149">Консоль toohello выходные данные трассировки записи</span><span class="sxs-lookup"><span data-stu-id="547bf-149">Writing trace output toohello console</span></span> 

<span data-ttu-id="547bf-150">В функциях, используйте hello `context.log` консоли toohello выходные данные трассировки toowrite методы.</span><span class="sxs-lookup"><span data-stu-id="547bf-150">In Functions, you use hello `context.log` methods toowrite trace output toohello console.</span></span> <span data-ttu-id="547bf-151">На этом этапе нельзя использовать `console.log` toowrite toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="547bf-151">At this point, you cannot use `console.log` toowrite toohello console.</span></span>

<span data-ttu-id="547bf-152">При вызове `context.log()`, сообщение записывается toohello консоли на уровень трассировки по умолчанию hello, являющийся hello _сведения_ уровень трассировки.</span><span class="sxs-lookup"><span data-stu-id="547bf-152">When you call `context.log()`, your message is written toohello console at hello default trace level, which is hello _info_ trace level.</span></span> <span data-ttu-id="547bf-153">Hello следующий код записывает toohello консоли на уровне трассировки hello сведения:</span><span class="sxs-lookup"><span data-stu-id="547bf-153">hello following code writes toohello console at hello info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="547bf-154">Hello выше код является эквивалентные toohello следующий код:</span><span class="sxs-lookup"><span data-stu-id="547bf-154">hello preceding code is equivalent toohello following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="547bf-155">Hello следующий код записывает toohello консоли на уровне ошибки hello:</span><span class="sxs-lookup"><span data-stu-id="547bf-155">hello following code writes toohello console at hello error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="547bf-156">Поскольку _ошибка_ hello наибольший трассировка уровня, это происходит запись трассировки toohello вывода на всех уровнях трассировки при условии, что включено ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="547bf-156">Because _error_ is hello highest trace level, this trace is written toohello output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="547bf-157">Все `context.log` методы поддерживают hello совпадает с форматом параметра, поддерживаемый hello Node.js [util.format метод](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="547bf-157">All `context.log` methods support hello same parameter format that's supported by hello Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="547bf-158">Рассмотрим следующий код, который записывает toohello консоли, используя уровень трассировки по умолчанию hello hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-158">Consider hello following code, which writes toohello console by using hello default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="547bf-159">Вы также можете же код в кодировке hello hello записи:</span><span class="sxs-lookup"><span data-stu-id="547bf-159">You can also write hello same code in hello following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a><span data-ttu-id="547bf-160">Настройка hello уровня трассировки для ведения журнала консоли</span><span class="sxs-lookup"><span data-stu-id="547bf-160">Configure hello trace level for console logging</span></span>

<span data-ttu-id="547bf-161">Функции можно определить уровень трассировки hello пороговое значение для записи toohello консоли, что делает его легко toocontrol hello способ трассировки записываются toohello консоли из функций.</span><span class="sxs-lookup"><span data-stu-id="547bf-161">Functions lets you define hello threshold trace level for writing toohello console, which makes it easy toocontrol hello way traces are written toohello console from your functions.</span></span> <span data-ttu-id="547bf-162">Пороговое значение hello tooset для всех трассировок, записанных toohello консоли используйте hello `tracing.consoleLevel` свойство в файле host.json hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-162">tooset hello threshold for all traces written toohello console, use hello `tracing.consoleLevel` property in hello host.json file.</span></span> <span data-ttu-id="547bf-163">Этот параметр применяется tooall функций в вашем приложении функции.</span><span class="sxs-lookup"><span data-stu-id="547bf-163">This setting applies tooall functions in your function app.</span></span> <span data-ttu-id="547bf-164">Hello следующий пример устанавливает hello пороговое значение tooenable подробное ведение журнала трассировки.</span><span class="sxs-lookup"><span data-stu-id="547bf-164">hello following example sets hello trace threshold tooenable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="547bf-165">Значения **consoleLevel** соответствуют имена toohello hello `context.log` методы.</span><span class="sxs-lookup"><span data-stu-id="547bf-165">Values of **consoleLevel** correspond toohello names of hello `context.log` methods.</span></span> <span data-ttu-id="547bf-166">задать все трассировки, ведения журнала консоли toohello toodisable **consoleLevel** too_off_.</span><span class="sxs-lookup"><span data-stu-id="547bf-166">toodisable all trace logging toohello console, set **consoleLevel** too_off_.</span></span> <span data-ttu-id="547bf-167">Дополнительные сведения о файле host.json hello см. в разделе hello [host.json справочном разделе](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="547bf-167">For more information about hello host.json file, see hello [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="547bf-168">Триггеры и привязки HTTP</span><span class="sxs-lookup"><span data-stu-id="547bf-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="547bf-169">HTTP и веб-перехватчика триггеры HTTP вывода и использовать привязки запроса и ответа объекты toorepresent hello HTTP системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="547bf-169">HTTP and webhook triggers and HTTP output bindings use request and response objects toorepresent hello HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="547bf-170">Объект запроса</span><span class="sxs-lookup"><span data-stu-id="547bf-170">Request object</span></span>

<span data-ttu-id="547bf-171">Hello `request` объект имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="547bf-171">hello `request` object has hello following properties:</span></span>

| <span data-ttu-id="547bf-172">Свойство</span><span class="sxs-lookup"><span data-stu-id="547bf-172">Property</span></span>      | <span data-ttu-id="547bf-173">Описание</span><span class="sxs-lookup"><span data-stu-id="547bf-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="547bf-174">_body_</span><span class="sxs-lookup"><span data-stu-id="547bf-174">_body_</span></span>        | <span data-ttu-id="547bf-175">Объект, содержащий текст hello hello запроса.</span><span class="sxs-lookup"><span data-stu-id="547bf-175">An object that contains hello body of hello request.</span></span>               |
| <span data-ttu-id="547bf-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="547bf-176">_headers_</span></span>     | <span data-ttu-id="547bf-177">Объект, содержащий заголовки запроса hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-177">An object that contains hello request headers.</span></span>                   |
| <span data-ttu-id="547bf-178">_method_</span><span class="sxs-lookup"><span data-stu-id="547bf-178">_method_</span></span>      | <span data-ttu-id="547bf-179">Здравствуйте, метод HTTP запроса hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-179">hello HTTP method of hello request.</span></span>                                |
| <span data-ttu-id="547bf-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="547bf-180">_originalUrl_</span></span> | <span data-ttu-id="547bf-181">URL-адрес Hello hello запроса.</span><span class="sxs-lookup"><span data-stu-id="547bf-181">hello URL of hello request.</span></span>                                        |
| <span data-ttu-id="547bf-182">_params_</span><span class="sxs-lookup"><span data-stu-id="547bf-182">_params_</span></span>      | <span data-ttu-id="547bf-183">Объект, содержащий параметры маршрутизации hello hello запроса.</span><span class="sxs-lookup"><span data-stu-id="547bf-183">An object that contains hello routing parameters of hello request.</span></span> |
| <span data-ttu-id="547bf-184">_query_</span><span class="sxs-lookup"><span data-stu-id="547bf-184">_query_</span></span>       | <span data-ttu-id="547bf-185">Объект, содержащий параметры запроса hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-185">An object that contains hello query parameters.</span></span>                  |
| <span data-ttu-id="547bf-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="547bf-186">_rawBody_</span></span>     | <span data-ttu-id="547bf-187">текст Hello приветственное сообщение как строку.</span><span class="sxs-lookup"><span data-stu-id="547bf-187">hello body of hello message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="547bf-188">Объект ответа</span><span class="sxs-lookup"><span data-stu-id="547bf-188">Response object</span></span>

<span data-ttu-id="547bf-189">Hello `response` объект имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="547bf-189">hello `response` object has hello following properties:</span></span>

| <span data-ttu-id="547bf-190">Свойство</span><span class="sxs-lookup"><span data-stu-id="547bf-190">Property</span></span>  | <span data-ttu-id="547bf-191">Описание</span><span class="sxs-lookup"><span data-stu-id="547bf-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="547bf-192">_body_</span><span class="sxs-lookup"><span data-stu-id="547bf-192">_body_</span></span>    | <span data-ttu-id="547bf-193">Объект, содержащий текст hello hello ответа.</span><span class="sxs-lookup"><span data-stu-id="547bf-193">An object that contains hello body of hello response.</span></span>         |
| <span data-ttu-id="547bf-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="547bf-194">_headers_</span></span> | <span data-ttu-id="547bf-195">Объект, содержащий заголовки ответа hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-195">An object that contains hello response headers.</span></span>             |
| <span data-ttu-id="547bf-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="547bf-196">_isRaw_</span></span>   | <span data-ttu-id="547bf-197">Указывает, что форматирование пропущена для hello ответа.</span><span class="sxs-lookup"><span data-stu-id="547bf-197">Indicates that formatting is skipped for hello response.</span></span>    |
| <span data-ttu-id="547bf-198">_состояние_</span><span class="sxs-lookup"><span data-stu-id="547bf-198">_status_</span></span>  | <span data-ttu-id="547bf-199">Здравствуйте, код состояния HTTP ответа hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-199">hello HTTP status code of hello response.</span></span>                     |

### <a name="accessing-hello-request-and-response"></a><span data-ttu-id="547bf-200">Доступ к hello запросов и ответов</span><span class="sxs-lookup"><span data-stu-id="547bf-200">Accessing hello request and response</span></span> 

<span data-ttu-id="547bf-201">При работе с триггерами HTTP, вы можете использовать hello HTTP объекты запроса и ответа в любом из трех способов:</span><span class="sxs-lookup"><span data-stu-id="547bf-201">When you work with HTTP triggers, you can access hello HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="547bf-202">Из hello с именем входа и выхода привязок.</span><span class="sxs-lookup"><span data-stu-id="547bf-202">From hello named input and output bindings.</span></span> <span data-ttu-id="547bf-203">Таким образом триггер HTTP hello и привязки hello же, как любые другие привязки.</span><span class="sxs-lookup"><span data-stu-id="547bf-203">In this way, hello HTTP trigger and bindings work hello same as any other binding.</span></span> <span data-ttu-id="547bf-204">Hello следующий пример задает hello объекта ответа с помощью именованного `response` привязки:</span><span class="sxs-lookup"><span data-stu-id="547bf-204">hello following example sets hello response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="547bf-205">Из `req` и `res` свойства hello `context` объекта.</span><span class="sxs-lookup"><span data-stu-id="547bf-205">From `req` and `res` properties on hello `context` object.</span></span> <span data-ttu-id="547bf-206">Таким образом, данные tooaccess HTTP обычный шаблон hello объекта контекста hello, можно использовать вместо полного hello toouse `context.bindings.name` шаблон.</span><span class="sxs-lookup"><span data-stu-id="547bf-206">In this way, you can use hello conventional pattern tooaccess HTTP data from hello context object, instead of having toouse hello full `context.bindings.name` pattern.</span></span> <span data-ttu-id="547bf-207">Следующий пример показывает как Hello tooaccess hello `req` и `res` объектов на hello `context`:</span><span class="sxs-lookup"><span data-stu-id="547bf-207">hello following example shows how tooaccess hello `req` and `res` objects on hello `context`:</span></span>

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="547bf-208">Путем вызова `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="547bf-208">By calling `context.done()`.</span></span> <span data-ttu-id="547bf-209">Специальный вид привязку HTTP возвращает hello ответ, который передается toohello `context.done()` метод.</span><span class="sxs-lookup"><span data-stu-id="547bf-209">A special kind of HTTP binding returns hello response that is passed toohello `context.done()` method.</span></span> <span data-ttu-id="547bf-210">Hello, выполнив HTTP вывода привязка определяет `$return` выходной параметр:</span><span class="sxs-lookup"><span data-stu-id="547bf-210">hello following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="547bf-211">Привязка для вывода предполагается, что вы toosupply hello ответа при вызове `done()`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="547bf-211">This output binding expects you toosupply hello response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="547bf-212">Управление версиями и пакетами Node</span><span class="sxs-lookup"><span data-stu-id="547bf-212">Node version and Package Management</span></span>
<span data-ttu-id="547bf-213">версия узла Hello заблокирован на `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="547bf-213">hello node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="547bf-214">Мы работаем над тем, чтобы добавить поддержку дополнительных версий и настройки для этих версий.</span><span class="sxs-lookup"><span data-stu-id="547bf-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="547bf-215">Hello следующие шаги позволяют включить пакеты в приложения функции:</span><span class="sxs-lookup"><span data-stu-id="547bf-215">hello following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="547bf-216">Go слишком`https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="547bf-216">Go too`https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="547bf-217">Щелкните **Debug Console** (Консоль отладки)  > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="547bf-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="547bf-218">Go слишком`D:\home\site\wwwroot`и затем перетащите файл вашей package.json toohello **wwwroot** папку в верхней части страницы приветствия hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-218">Go too`D:\home\site\wwwroot`, and then drag your package.json file toohello **wwwroot** folder at hello top half of hello page.</span></span>  
    <span data-ttu-id="547bf-219">Также можно передать файлы tooyour функции приложения по-другому.</span><span class="sxs-lookup"><span data-stu-id="547bf-219">You can upload files tooyour function app in other ways also.</span></span> <span data-ttu-id="547bf-220">Дополнительные сведения см. в разделе [как tooupdate функция файлов приложения](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="547bf-220">For more information, see [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="547bf-221">После передачи файла package.json hello запустите hello `npm install` в hello **консоли удаленного выполнения Kudu**.</span><span class="sxs-lookup"><span data-stu-id="547bf-221">After hello package.json file is uploaded, run hello `npm install` command in hello **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="547bf-222">Это действие загружает пакеты hello, указанный в файле package.json hello и перезапускает приложение функции hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-222">This action downloads hello packages indicated in hello package.json file and restarts hello function app.</span></span>

<span data-ttu-id="547bf-223">После hello необходимые пакеты установлены, импорте tooyour функции путем вызова `require('packagename')`, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="547bf-223">After hello packages you need are installed, you import them tooyour function by calling `require('packagename')`, as in hello following example:</span></span>

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="547bf-224">Следует определить `package.json` файла в корне hello функции приложения.</span><span class="sxs-lookup"><span data-stu-id="547bf-224">You should define a `package.json` file at hello root of your function app.</span></span> <span data-ttu-id="547bf-225">Определение hello файл разрешает все функции в папке приложения hello hello же кэшированные пакеты, что дает hello наилучшей производительности.</span><span class="sxs-lookup"><span data-stu-id="547bf-225">Defining hello file lets all functions in hello app share hello same cached packages, which gives hello best performance.</span></span> <span data-ttu-id="547bf-226">Если возникает конфликт версий, можно разрешить ее, добавив `package.json` файл в папке hello конкретной функции.</span><span class="sxs-lookup"><span data-stu-id="547bf-226">If a version conflict arises, you can resolve it by adding a `package.json` file in hello folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="547bf-227">Переменные среды</span><span class="sxs-lookup"><span data-stu-id="547bf-227">Environment variables</span></span>
<span data-ttu-id="547bf-228">tooget переменной среды или значение параметра приложения, используйте `process.env`, как показано в следующем примере кода hello:</span><span class="sxs-lookup"><span data-stu-id="547bf-228">tooget an environment variable or an app setting value, use `process.env`, as shown in hello following code example:</span></span>

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
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="547bf-229">Рекомендации для функций JavaScript</span><span class="sxs-lookup"><span data-stu-id="547bf-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="547bf-230">При работе с функции JavaScript, помните о hello рекомендации в следующих двух разделах hello.</span><span class="sxs-lookup"><span data-stu-id="547bf-230">When you work with JavaScript functions, be aware of hello considerations in hello following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="547bf-231">Выбор одноядерных планов службы приложений</span><span class="sxs-lookup"><span data-stu-id="547bf-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="547bf-232">При создании функции приложения, в котором используется hello план служб приложений, рекомендуется выбрать план одним ядром, а не план с несколькими ядрами.</span><span class="sxs-lookup"><span data-stu-id="547bf-232">When you create a function app that uses hello App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="547bf-233">В настоящее время функции выполняется функции JavaScript более эффективно на виртуальных машинах одноядерный и с использованием большего размера виртуальных машин не дает hello ожидаемого улучшения производительности.</span><span class="sxs-lookup"><span data-stu-id="547bf-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce hello expected performance improvements.</span></span> <span data-ttu-id="547bf-234">При необходимости вы можете вручную добавить дополнительные экземпляры одноядерных виртуальных машин или включить автоматическое масштабирование.</span><span class="sxs-lookup"><span data-stu-id="547bf-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="547bf-235">Дополнительные сведения см. в статье [Масштабирование числа экземпляров вручную или автоматически](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="547bf-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="547bf-236">Поддержка TypeScript и CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="547bf-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="547bf-237">Поскольку Прямая поддержка еще не существует для компиляции автоматически TypeScript или CoffeeScript через hello среды выполнения, такая поддержка должен toobe обрабатывается вне среды hello во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="547bf-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via hello runtime, such support needs toobe handled outside hello runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="547bf-238">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="547bf-238">Next steps</span></span>
<span data-ttu-id="547bf-239">Дополнительные сведения см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="547bf-239">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="547bf-240">Рекомендации по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="547bf-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="547bf-241">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="547bf-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="547bf-242">Справочник разработчика C# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="547bf-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="547bf-243">Справочник разработчика F# по Функциям Azure</span><span class="sxs-lookup"><span data-stu-id="547bf-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="547bf-244">Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)</span><span class="sxs-lookup"><span data-stu-id="547bf-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

