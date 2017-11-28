---
title: "Справочник разработчика JavaScript для Функций Azure | Документация Майкрософт"
description: "Узнайте, как разрабатывать функции с помощью JavaScript."
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
ms.openlocfilehash: 7ea81ed47f391fbce1432c2b11ac176ab6c04ae0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="05169-104">Руководство разработчика JavaScript для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="05169-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="05169-105">Сценарий C#</span><span class="sxs-lookup"><span data-stu-id="05169-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="05169-106">Скрипт F#</span><span class="sxs-lookup"><span data-stu-id="05169-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="05169-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="05169-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="05169-108">Интерфейс JavaScript для Azure Functions позволяет легко экспортировать функцию, которая передается в качестве объекта `context`, для взаимодействия со средой выполнения, а также для получения и отправки данных с помощью привязок.</span><span class="sxs-lookup"><span data-stu-id="05169-108">The JavaScript experience for Azure Functions makes it easy to export a function, which is passed as a `context` object for communicating with the runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="05169-109">В этой статье предполагается, что вы уже прочли [справочник разработчика по Функциям Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="05169-109">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="05169-110">Экспорт функции</span><span class="sxs-lookup"><span data-stu-id="05169-110">Exporting a function</span></span>
<span data-ttu-id="05169-111">Все функции JavaScript должны экспортировать одну `function` с помощью `module.exports`, чтобы среда выполнения могла найти эту функцию и запустить ее.</span><span class="sxs-lookup"><span data-stu-id="05169-111">All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it.</span></span> <span data-ttu-id="05169-112">Эта функция должна всегда включать объект `context` .</span><span class="sxs-lookup"><span data-stu-id="05169-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by the arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="05169-113">Привязки `direction === "in"` передаются как аргументы функции, то есть вы можете использовать [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) для динамической обработки новых входных данных (например, используя `arguments.length` для итерации всех входных данных).</span><span class="sxs-lookup"><span data-stu-id="05169-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs).</span></span> <span data-ttu-id="05169-114">Эта возможность удобна, когда у вас есть только триггер без дополнительных входных данных, так как к данным триггера можно обращаться напрямую, без ссылки на объект `context`.</span><span class="sxs-lookup"><span data-stu-id="05169-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="05169-115">Аргументы всегда передаются в функцию в порядке их появления в файле *function.json*, даже если они не указаны в инструкциях экспорта.</span><span class="sxs-lookup"><span data-stu-id="05169-115">The arguments are always passed along to the function in the order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="05169-116">Например, если у вас есть функция `function(context, a, b)` и вы изменяете ее на `function(context, a)`, то значение `b` все равно можно получить в коде функции с помощью `arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="05169-116">For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.</span></span>

<span data-ttu-id="05169-117">Все привязки, независимо от направления, также передаются в объекте `context` (см. указанный ниже скрипт).</span><span class="sxs-lookup"><span data-stu-id="05169-117">All bindings, regardless of direction, are also passed along on the `context` object (see the following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="05169-118">Объект context</span><span class="sxs-lookup"><span data-stu-id="05169-118">context object</span></span>
<span data-ttu-id="05169-119">Среда выполнения использует объект `context` для передачи данных в функцию и из нее, а также для взаимодействия со средой выполнения.</span><span class="sxs-lookup"><span data-stu-id="05169-119">The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.</span></span>

<span data-ttu-id="05169-120">Объект context всегда является первым параметром функции, и его надо указывать всегда, так как он содержит методы, необходимые для правильного использования среды выполнения, такие как `context.done` и `context.log`.</span><span class="sxs-lookup"><span data-stu-id="05169-120">The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log`, which are required to use the runtime correctly.</span></span> <span data-ttu-id="05169-121">Для этого объекта можно указать любое имя (например, `ctx` или `c`).</span><span class="sxs-lookup"><span data-stu-id="05169-121">You can name the object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="05169-122">Свойство context.bindings</span><span class="sxs-lookup"><span data-stu-id="05169-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="05169-123">Возвращает именованный объект, который содержит все входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="05169-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="05169-124">Например, следующее определение привязки в *function.json* позволяет вам получить доступ к содержимому очереди с помощью объекта `context.bindings.myInput`.</span><span class="sxs-lookup"><span data-stu-id="05169-124">For example, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains the input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="05169-125">Метод context.done</span><span class="sxs-lookup"><span data-stu-id="05169-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="05169-126">Информирует среду выполнения о завершении выполнения кода.</span><span class="sxs-lookup"><span data-stu-id="05169-126">Informs the runtime that your code has finished.</span></span> <span data-ttu-id="05169-127">Необходимо вызвать метод `context.done`, или в противном случае среда выполнения не узнает, что функция завершена, и время ожидания выполнения истечет.</span><span class="sxs-lookup"><span data-stu-id="05169-127">You must call `context.done`, or else the runtime never knows that your function is complete, and the execution will time out.</span></span> 

<span data-ttu-id="05169-128">Метод `context.done` позволяет передавать в среду выполнения пользовательское сообщение об ошибке, а также контейнер свойств, которые перезапишут свойства объекта `context.bindings`.</span><span class="sxs-lookup"><span data-stu-id="05169-128">The `context.done` method allows you to pass back both a user-defined error to the runtime and a property bag of properties that overwrite the properties on the `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput to have:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object to the done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// the done method will overwrite the myOutput binding to be: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="05169-129">Метод context.log</span><span class="sxs-lookup"><span data-stu-id="05169-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="05169-130">Этот метод позволяет делать записи в потоковые журналы консоли на уровне трассировки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="05169-130">Allows you to write to the streaming console logs at the default trace level.</span></span> <span data-ttu-id="05169-131">В `context.log` доступны дополнительные методы ведения журнала, позволяющие выполнять запись в журнал консоли на других уровнях трассировки:</span><span class="sxs-lookup"><span data-stu-id="05169-131">On `context.log`, additional logging methods are available that let you write to the console log at other trace levels:</span></span>


| <span data-ttu-id="05169-132">Метод</span><span class="sxs-lookup"><span data-stu-id="05169-132">Method</span></span>                 | <span data-ttu-id="05169-133">Описание</span><span class="sxs-lookup"><span data-stu-id="05169-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="05169-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="05169-134">**error(_message_)**</span></span>   | <span data-ttu-id="05169-135">Записывает сообщение в журнал на уровне ошибок или более низком.</span><span class="sxs-lookup"><span data-stu-id="05169-135">Writes to error level logging, or lower.</span></span>   |
| <span data-ttu-id="05169-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="05169-136">**warn(_message_)**</span></span>    | <span data-ttu-id="05169-137">Записывает сообщение в журнал на уровне предупреждений или более низком.</span><span class="sxs-lookup"><span data-stu-id="05169-137">Writes to warning level logging, or lower.</span></span> |
| <span data-ttu-id="05169-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="05169-138">**info(_message_)**</span></span>    | <span data-ttu-id="05169-139">Записывает сообщение в журнал на уровне сведений или более низком.</span><span class="sxs-lookup"><span data-stu-id="05169-139">Writes to info level logging, or lower.</span></span>    |
| <span data-ttu-id="05169-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="05169-140">**verbose(_message_)**</span></span> | <span data-ttu-id="05169-141">Записывает сообщение в журнал на уровне детализации.</span><span class="sxs-lookup"><span data-stu-id="05169-141">Writes to verbose level logging.</span></span>           |

<span data-ttu-id="05169-142">Следующий пример записывает в консоль на уровне трассировки "предупреждения":</span><span class="sxs-lookup"><span data-stu-id="05169-142">The following example writes to the console at the warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="05169-143">Вы можете задать пороговое значение уровня трассировки для ведения журнала в файле host.json или отключить эту функцию.</span><span class="sxs-lookup"><span data-stu-id="05169-143">You can set the trace-level threshold for logging in the host.json file, or turn it off.</span></span>  <span data-ttu-id="05169-144">Дополнительные сведения о том, как делать записи в журнал, см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="05169-144">For more information about how to write to the logs, see the next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="05169-145">Тип данных привязки</span><span class="sxs-lookup"><span data-stu-id="05169-145">Binding data type</span></span>

<span data-ttu-id="05169-146">Чтобы определить тип данных для входной привязки, используйте свойство `dataType` в определении привязки.</span><span class="sxs-lookup"><span data-stu-id="05169-146">To define the data type for an input binding, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="05169-147">Например, чтобы прочитать содержимое HTTP-запроса в двоичном формате, используйте тип `binary`:</span><span class="sxs-lookup"><span data-stu-id="05169-147">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="05169-148">Другие варианты для `dataType` — `stream` и `string`.</span><span class="sxs-lookup"><span data-stu-id="05169-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-to-the-console"></a><span data-ttu-id="05169-149">Вывод выходных данных трассировки на консоль</span><span class="sxs-lookup"><span data-stu-id="05169-149">Writing trace output to the console</span></span> 

<span data-ttu-id="05169-150">В Azure Functions воспользуйтесь методами `context.log` для записи выходных данных трассировки в консоль.</span><span class="sxs-lookup"><span data-stu-id="05169-150">In Functions, you use the `context.log` methods to write trace output to the console.</span></span> <span data-ttu-id="05169-151">На этом этапе для записи в консоль нельзя использовать метод `console.log`.</span><span class="sxs-lookup"><span data-stu-id="05169-151">At this point, you cannot use `console.log` to write to the console.</span></span>

<span data-ttu-id="05169-152">При вызове `context.log()` ваше сообщение записывается в консоль на уровне трассировки по умолчанию — уровень _сведений_.</span><span class="sxs-lookup"><span data-stu-id="05169-152">When you call `context.log()`, your message is written to the console at the default trace level, which is the _info_ trace level.</span></span> <span data-ttu-id="05169-153">Следующий код записывает на консоль на уровне трассировки "сведения":</span><span class="sxs-lookup"><span data-stu-id="05169-153">The following code writes to the console at the info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="05169-154">Предыдущий код аналогичен следующему:</span><span class="sxs-lookup"><span data-stu-id="05169-154">The preceding code is equivalent to the following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="05169-155">Следующий код записывает на консоль на уровне трассировки "ошибки":</span><span class="sxs-lookup"><span data-stu-id="05169-155">The following code writes to the console at the error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="05169-156">Так как _уровень ошибок_ является наивысшим уровнем трасировки, эта трассировка записывается в выходные данные на всех уровнях трассировки при условии, что ведение журнала включено.</span><span class="sxs-lookup"><span data-stu-id="05169-156">Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="05169-157">Все методы `context.log` поддерживают тот же формат параметров, что и метод Node.js [util.format](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="05169-157">All `context.log` methods support the same parameter format that's supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="05169-158">Просмотрите следующий код, который выполняет запись в консоль, используя уровень трассировки по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="05169-158">Consider the following code, which writes to the console by using the default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="05169-159">Этот же код можно записать в таком формате:</span><span class="sxs-lookup"><span data-stu-id="05169-159">You can also write the same code in the following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-the-trace-level-for-console-logging"></a><span data-ttu-id="05169-160">Настройка уровня трассировки для ведения журнала консоли</span><span class="sxs-lookup"><span data-stu-id="05169-160">Configure the trace level for console logging</span></span>

<span data-ttu-id="05169-161">В Функциях Azure можно определить пороговое значение уровня трассировки для записи в консоль, чтобы легко контролировать, как трассировки записываются в консоль из ваших функций.</span><span class="sxs-lookup"><span data-stu-id="05169-161">Functions lets you define the threshold trace level for writing to the console, which makes it easy to control the way traces are written to the console from your functions.</span></span> <span data-ttu-id="05169-162">Чтобы задать пороговое значение для всех трассировок, которые записываются в консоль, используйте свойство `tracing.consoleLevel` в файле host.json.</span><span class="sxs-lookup"><span data-stu-id="05169-162">To set the threshold for all traces written to the console, use the `tracing.consoleLevel` property in the host.json file.</span></span> <span data-ttu-id="05169-163">Этот параметр применяется ко всем функциям в приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="05169-163">This setting applies to all functions in your function app.</span></span> <span data-ttu-id="05169-164">В следующем примере задается пороговое значение трассировки, чтобы включить подробное ведение журнала:</span><span class="sxs-lookup"><span data-stu-id="05169-164">The following example sets the trace threshold to enable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="05169-165">Значения **consoleLevel** соответствуют именам методов в `context.log`.</span><span class="sxs-lookup"><span data-stu-id="05169-165">Values of **consoleLevel** correspond to the names of the `context.log` methods.</span></span> <span data-ttu-id="05169-166">Чтобы отключить ведение журнала трассировки в консоли, задайте для параметра **consoleLevel** значение _off_.</span><span class="sxs-lookup"><span data-stu-id="05169-166">To disable all trace logging to the console, set **consoleLevel** to _off_.</span></span> <span data-ttu-id="05169-167">Дополнительные сведения о файле host.json см. [в этом разделе](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="05169-167">For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="05169-168">Триггеры и привязки HTTP</span><span class="sxs-lookup"><span data-stu-id="05169-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="05169-169">Триггеры HTTP и webhook, а также привязки вывода HTTP используют объекты запроса и ответа для обмена сообщениями HTTP.</span><span class="sxs-lookup"><span data-stu-id="05169-169">HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="05169-170">Объект запроса</span><span class="sxs-lookup"><span data-stu-id="05169-170">Request object</span></span>

<span data-ttu-id="05169-171">Объект `request` имеет следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="05169-171">The `request` object has the following properties:</span></span>

| <span data-ttu-id="05169-172">Свойство</span><span class="sxs-lookup"><span data-stu-id="05169-172">Property</span></span>      | <span data-ttu-id="05169-173">Описание</span><span class="sxs-lookup"><span data-stu-id="05169-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="05169-174">_body_</span><span class="sxs-lookup"><span data-stu-id="05169-174">_body_</span></span>        | <span data-ttu-id="05169-175">Объект, содержащий текст запроса.</span><span class="sxs-lookup"><span data-stu-id="05169-175">An object that contains the body of the request.</span></span>               |
| <span data-ttu-id="05169-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="05169-176">_headers_</span></span>     | <span data-ttu-id="05169-177">Объект, содержащий заголовок запроса.</span><span class="sxs-lookup"><span data-stu-id="05169-177">An object that contains the request headers.</span></span>                   |
| <span data-ttu-id="05169-178">_method_</span><span class="sxs-lookup"><span data-stu-id="05169-178">_method_</span></span>      | <span data-ttu-id="05169-179">Метод HTTP, используемый для запроса.</span><span class="sxs-lookup"><span data-stu-id="05169-179">The HTTP method of the request.</span></span>                                |
| <span data-ttu-id="05169-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="05169-180">_originalUrl_</span></span> | <span data-ttu-id="05169-181">URL-адрес запроса.</span><span class="sxs-lookup"><span data-stu-id="05169-181">The URL of the request.</span></span>                                        |
| <span data-ttu-id="05169-182">_params_</span><span class="sxs-lookup"><span data-stu-id="05169-182">_params_</span></span>      | <span data-ttu-id="05169-183">Объект, содержащий параметры маршрутизации запроса.</span><span class="sxs-lookup"><span data-stu-id="05169-183">An object that contains the routing parameters of the request.</span></span> |
| <span data-ttu-id="05169-184">_query_</span><span class="sxs-lookup"><span data-stu-id="05169-184">_query_</span></span>       | <span data-ttu-id="05169-185">Объект, содержащий параметры запроса.</span><span class="sxs-lookup"><span data-stu-id="05169-185">An object that contains the query parameters.</span></span>                  |
| <span data-ttu-id="05169-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="05169-186">_rawBody_</span></span>     | <span data-ttu-id="05169-187">Текст сообщения в виде строки.</span><span class="sxs-lookup"><span data-stu-id="05169-187">The body of the message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="05169-188">Объект ответа</span><span class="sxs-lookup"><span data-stu-id="05169-188">Response object</span></span>

<span data-ttu-id="05169-189">Объект `response` имеет следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="05169-189">The `response` object has the following properties:</span></span>

| <span data-ttu-id="05169-190">Свойство</span><span class="sxs-lookup"><span data-stu-id="05169-190">Property</span></span>  | <span data-ttu-id="05169-191">Описание</span><span class="sxs-lookup"><span data-stu-id="05169-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="05169-192">_body_</span><span class="sxs-lookup"><span data-stu-id="05169-192">_body_</span></span>    | <span data-ttu-id="05169-193">Объект, содержащий текст ответа.</span><span class="sxs-lookup"><span data-stu-id="05169-193">An object that contains the body of the response.</span></span>         |
| <span data-ttu-id="05169-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="05169-194">_headers_</span></span> | <span data-ttu-id="05169-195">Объект, содержащий заголовок ответа.</span><span class="sxs-lookup"><span data-stu-id="05169-195">An object that contains the response headers.</span></span>             |
| <span data-ttu-id="05169-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="05169-196">_isRaw_</span></span>   | <span data-ttu-id="05169-197">Указывает, что форматирование пропускается для ответа.</span><span class="sxs-lookup"><span data-stu-id="05169-197">Indicates that formatting is skipped for the response.</span></span>    |
| <span data-ttu-id="05169-198">_состояние_</span><span class="sxs-lookup"><span data-stu-id="05169-198">_status_</span></span>  | <span data-ttu-id="05169-199">Код состояния HTTP ответа.</span><span class="sxs-lookup"><span data-stu-id="05169-199">The HTTP status code of the response.</span></span>                     |

### <a name="accessing-the-request-and-response"></a><span data-ttu-id="05169-200">Доступ к запросу и ответу</span><span class="sxs-lookup"><span data-stu-id="05169-200">Accessing the request and response</span></span> 

<span data-ttu-id="05169-201">При работе с триггерами HTTP вы можете получить доступ к объектам запроса и ответа HTTP одним из 3 способов:</span><span class="sxs-lookup"><span data-stu-id="05169-201">When you work with HTTP triggers, you can access the HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="05169-202">С помощью именованных входных и выходных привязок.</span><span class="sxs-lookup"><span data-stu-id="05169-202">From the named input and output bindings.</span></span> <span data-ttu-id="05169-203">В этом случае триггер и привязки HTTP работают как любая другая привязка.</span><span class="sxs-lookup"><span data-stu-id="05169-203">In this way, the HTTP trigger and bindings work the same as any other binding.</span></span> <span data-ttu-id="05169-204">В следующем примере объект ответа задается с помощью именованной привязки `response`:</span><span class="sxs-lookup"><span data-stu-id="05169-204">The following example sets the response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="05169-205">От свойств `req` и `res` объекта `context`.</span><span class="sxs-lookup"><span data-stu-id="05169-205">From `req` and `res` properties on the `context` object.</span></span> <span data-ttu-id="05169-206">В этом случае можно использовать обычный шаблон доступа к данным HTTP из объекта context вместо полного шаблона `context.bindings.name`.</span><span class="sxs-lookup"><span data-stu-id="05169-206">In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern.</span></span> <span data-ttu-id="05169-207">Следующий пример демонстрирует доступ к объектам `req` и `res` в `context`:</span><span class="sxs-lookup"><span data-stu-id="05169-207">The following example shows how to access the `req` and `res` objects on the `context`:</span></span>

    ```javascript
    // You can access your http request off the context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="05169-208">Путем вызова `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="05169-208">By calling `context.done()`.</span></span> <span data-ttu-id="05169-209">Специальный тип привязки HTTP возвращает ответ, передавшийся методу `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="05169-209">A special kind of HTTP binding returns the response that is passed to the `context.done()` method.</span></span> <span data-ttu-id="05169-210">Следующая привязка вывода HTTP определяет параметр вывода `$return`:</span><span class="sxs-lookup"><span data-stu-id="05169-210">The following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="05169-211">Эта привязка вывода ожидает предоставления ответа при вызове `done()` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="05169-211">This output binding expects you to supply the response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="05169-212">Управление версиями и пакетами Node</span><span class="sxs-lookup"><span data-stu-id="05169-212">Node version and Package Management</span></span>
<span data-ttu-id="05169-213">Версия Node сейчас зафиксирована в значении `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="05169-213">The node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="05169-214">Мы работаем над тем, чтобы добавить поддержку дополнительных версий и настройки для этих версий.</span><span class="sxs-lookup"><span data-stu-id="05169-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="05169-215">Следующие шаги позволяют включить пакеты в приложение-функцию:</span><span class="sxs-lookup"><span data-stu-id="05169-215">The following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="05169-216">Перейдите на сайт `https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="05169-216">Go to `https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="05169-217">Щелкните **Debug Console** (Консоль отладки)  > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="05169-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="05169-218">Перейдите к `D:\home\site\wwwroot`, а затем перетащите файл package.json в папку **wwwroot** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="05169-218">Go to `D:\home\site\wwwroot`, and then drag your package.json file to the **wwwroot** folder at the top half of the page.</span></span>  
    <span data-ttu-id="05169-219">Существуют другие способы передачи файлов в приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="05169-219">You can upload files to your function app in other ways also.</span></span> <span data-ttu-id="05169-220">Дополнительные сведения см. в разделе [Как обновить файлы приложения-функции](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="05169-220">For more information, see [How to update function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="05169-221">После загрузки файла package.json запустите команду `npm install` в **консоли удаленного выполнения Kudu**.</span><span class="sxs-lookup"><span data-stu-id="05169-221">After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="05169-222">В результате этого действия будут загружены пакеты, указанные в файле package.json, и перезапущено приложение-функция.</span><span class="sxs-lookup"><span data-stu-id="05169-222">This action downloads the packages indicated in the package.json file and restarts the function app.</span></span>

<span data-ttu-id="05169-223">После установки необходимых пакетов их необходимо импортировать в функцию, вызвав `require('packagename')`, как это показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="05169-223">After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example:</span></span>

```javascript
// Import the underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="05169-224">Следует определить файл `package.json` в корне вашего приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="05169-224">You should define a `package.json` file at the root of your function app.</span></span> <span data-ttu-id="05169-225">После этого все функции в приложении будут совместно использовать одни и те же кэшированные пакеты, что обеспечивает наилучшую производительность.</span><span class="sxs-lookup"><span data-stu-id="05169-225">Defining the file lets all functions in the app share the same cached packages, which gives the best performance.</span></span> <span data-ttu-id="05169-226">При возникновении конфликтов версий их можно разрешить, добавив файл `package.json` в папку определенной функции.</span><span class="sxs-lookup"><span data-stu-id="05169-226">If a version conflict arises, you can resolve it by adding a `package.json` file in the folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="05169-227">Переменные среды</span><span class="sxs-lookup"><span data-stu-id="05169-227">Environment variables</span></span>
<span data-ttu-id="05169-228">Чтобы получить значение переменной среды или значение параметра приложения, используйте `process.env`, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="05169-228">To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:</span></span>

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
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="05169-229">Рекомендации для функций JavaScript</span><span class="sxs-lookup"><span data-stu-id="05169-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="05169-230">При работе с функциями JavaScript следует помнить о рекомендациях, приведенных в двух следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="05169-230">When you work with JavaScript functions, be aware of the considerations in the following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="05169-231">Выбор одноядерных планов службы приложений</span><span class="sxs-lookup"><span data-stu-id="05169-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="05169-232">При создании приложения-функции, которое использует план службы приложения, мы советуем выбирать план для одного ядра вместо плана для нескольких ядер.</span><span class="sxs-lookup"><span data-stu-id="05169-232">When you create a function app that uses the App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="05169-233">Сейчас Функции Azure намного эффективнее выполняют функции JavaScript на одноядерных виртуальных машинах. Использование более крупных виртуальных машин не приводит к ожидаемому улучшению производительности.</span><span class="sxs-lookup"><span data-stu-id="05169-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce the expected performance improvements.</span></span> <span data-ttu-id="05169-234">При необходимости вы можете вручную добавить дополнительные экземпляры одноядерных виртуальных машин или включить автоматическое масштабирование.</span><span class="sxs-lookup"><span data-stu-id="05169-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="05169-235">Дополнительные сведения см. в статье [Масштабирование числа экземпляров вручную или автоматически](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05169-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="05169-236">Поддержка TypeScript и CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="05169-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="05169-237">Так как прямой поддержки автоматической компиляции TypeScript и CoffeeScript в среде выполнения сейчас нет, соответствующую обработку необходимо осуществлять вне среды выполнения во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="05169-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via the runtime, such support needs to be handled outside the runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="05169-238">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05169-238">Next steps</span></span>
<span data-ttu-id="05169-239">Для получения дополнительных сведений см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="05169-239">For more information, see the following resources:</span></span>

* [<span data-ttu-id="05169-240">Рекомендации по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="05169-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="05169-241">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="05169-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="05169-242">Справочник разработчика C# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="05169-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="05169-243">Справочник разработчика F# по Функциям Azure</span><span class="sxs-lookup"><span data-stu-id="05169-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="05169-244">Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)</span><span class="sxs-lookup"><span data-stu-id="05169-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

