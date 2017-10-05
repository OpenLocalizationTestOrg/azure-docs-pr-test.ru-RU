---
title: "Работа с триггерами и привязками в Функциях Azure | Документация Майкрософт"
description: "Узнайте, как подключить выполнение кода к интерактивным мероприятиям и облачным службам, используя триггеры и привязки в Функциях Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, веб-перехватчики, динамические вычисления, независимая архитектура"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: cc41debb2523df77be4db05817a4c7ac55604439
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="7ee31-104">Основные понятия триггеров и привязок в Функциях Azure</span><span class="sxs-lookup"><span data-stu-id="7ee31-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="7ee31-105">Функции Azure позволяют писать код в ответ на события в Azure и других службах с помощью *триггеров* и *привязок*.</span><span class="sxs-lookup"><span data-stu-id="7ee31-105">Azure Functions allows you to write code in response to events in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="7ee31-106">В этой статье приведены общие сведения о триггерах и привязках для всех поддерживаемых языков программирования.</span><span class="sxs-lookup"><span data-stu-id="7ee31-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="7ee31-107">Здесь описываются функции, которые являются общими для всех привязок.</span><span class="sxs-lookup"><span data-stu-id="7ee31-107">Features that are common to all bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="7ee31-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="7ee31-108">Overview</span></span>

<span data-ttu-id="7ee31-109">Триггеры и привязки реализуют декларативный способ определения того, как должны вызываться функции и с какими данными одни будут работать.</span><span class="sxs-lookup"><span data-stu-id="7ee31-109">Triggers and bindings are a declarative way to define how a function is invoked and what data it works with.</span></span> <span data-ttu-id="7ee31-110">*Триггер* определяет способ вызова функции.</span><span class="sxs-lookup"><span data-stu-id="7ee31-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="7ee31-111">У функции должен быть только один триггер.</span><span class="sxs-lookup"><span data-stu-id="7ee31-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="7ee31-112">С триггерами могут быть связанны данные, которые обычно являются полезными и активируют функцию.</span><span class="sxs-lookup"><span data-stu-id="7ee31-112">Triggers have associated data, which is usually the payload that triggered the function.</span></span> 

<span data-ttu-id="7ee31-113">Входные и выходные *привязки* реализуют декларативный способ подключения к данным из кода.</span><span class="sxs-lookup"><span data-stu-id="7ee31-113">Input and output *bindings* provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="7ee31-114">Как и в случае триггеров, для них необходимо указать строки подключения и другие свойства в конфигурации функции.</span><span class="sxs-lookup"><span data-stu-id="7ee31-114">Similar to triggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="7ee31-115">Привязки необязательны, а у функции может быть несколько входных и выходных привязок.</span><span class="sxs-lookup"><span data-stu-id="7ee31-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="7ee31-116">Используя триггеры и привязки, можно писать более универсальный код без жесткого кодирования данных служб, с которыми он взаимодействует.</span><span class="sxs-lookup"><span data-stu-id="7ee31-116">Using triggers and bindings, you can write code that is more generic and does not hardcode the details of the services with which it interacts.</span></span> <span data-ttu-id="7ee31-117">Данные, поступающие из служб, становятся для кода вашей функции обычными входными значениями.</span><span class="sxs-lookup"><span data-stu-id="7ee31-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="7ee31-118">Для вывода данных в другую службу (например, создания новой строки в Хранилище таблиц Azure) следует использовать возвращаемое значение метода.</span><span class="sxs-lookup"><span data-stu-id="7ee31-118">To output data to another service (such as creating a new row in Azure Table Storage), use the return value of the method.</span></span> <span data-ttu-id="7ee31-119">Если требуется вывести несколько значений, воспользуйтесь вспомогательным объектом.</span><span class="sxs-lookup"><span data-stu-id="7ee31-119">Or, if you need to output multiple values, use a helper object.</span></span> <span data-ttu-id="7ee31-120">Триггеры и привязки получают свойство **name**, которое представляет собой идентификатор, используемый в коде для доступа к привязке.</span><span class="sxs-lookup"><span data-stu-id="7ee31-120">Triggers and bindings have a **name** property, which is an identifier you use in your code to access the binding.</span></span>

<span data-ttu-id="7ee31-121">Триггеры и привязки можно настроить на вкладке **Интегрировать** на портале Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee31-121">You can configure triggers and bindings in the **Integrate** tab in the Azure Functions portal.</span></span> <span data-ttu-id="7ee31-122">На самом деле пользовательский интерфейс изменяет файл с именем *function.json* в каталоге функции.</span><span class="sxs-lookup"><span data-stu-id="7ee31-122">Under the covers, the UI modifies a file called *function.json* file in the function directory.</span></span> <span data-ttu-id="7ee31-123">Этот файл можно изменить с помощью **расширенного редактора**.</span><span class="sxs-lookup"><span data-stu-id="7ee31-123">You can edit this file by changing to the **Advanced editor**.</span></span>

<span data-ttu-id="7ee31-124">В следующей таблице приведены триггеры и привязки, поддерживаемые Функциями Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee31-124">The following table shows the triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="7ee31-125">Пример. Триггер очередей и выходная привязка таблицы</span><span class="sxs-lookup"><span data-stu-id="7ee31-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="7ee31-126">Предположим, что всякий раз, когда в хранилище очередей Azure появляется новое сообщение, требуется создать новую строку для Хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee31-126">Suppose you want to write a new row to Azure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="7ee31-127">Этот сценарий может быть реализован с помощью триггера очередей Azure и выходной привязки таблицы.</span><span class="sxs-lookup"><span data-stu-id="7ee31-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="7ee31-128">Для триггера очередей требуются следующие данные с вкладки **Интегрировать**:</span><span class="sxs-lookup"><span data-stu-id="7ee31-128">A queue trigger requires the following information in the **Integrate** tab:</span></span>

* <span data-ttu-id="7ee31-129">имя параметра приложения, который содержит строку подключения учетной записи хранения для очереди;</span><span class="sxs-lookup"><span data-stu-id="7ee31-129">The name of the app setting that contains the storage account connection string for the queue</span></span>
* <span data-ttu-id="7ee31-130">имя очереди;</span><span class="sxs-lookup"><span data-stu-id="7ee31-130">The queue name</span></span>
* <span data-ttu-id="7ee31-131">идентификатор в коде, используемый для считывания содержимого сообщений очереди, например `order`.</span><span class="sxs-lookup"><span data-stu-id="7ee31-131">The identifier in your code to read the contents of the queue message, such as `order`.</span></span>

<span data-ttu-id="7ee31-132">Для записи в Хранилище таблиц Azure необходимо использовать выходную привязку со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="7ee31-132">To write to Azure Table Storage, use an output binding with the following details:</span></span>

* <span data-ttu-id="7ee31-133">имя параметра приложения, который содержит строку подключения учетной записи хранения для таблицы;</span><span class="sxs-lookup"><span data-stu-id="7ee31-133">The name of the app setting that contains the storage account connection string for the table</span></span>
* <span data-ttu-id="7ee31-134">имя таблицы;</span><span class="sxs-lookup"><span data-stu-id="7ee31-134">The table name</span></span>
* <span data-ttu-id="7ee31-135">идентификатор в коде для создания выходных элементов или возвращаемое значение функции.</span><span class="sxs-lookup"><span data-stu-id="7ee31-135">The identifier in your code to create output items, or the return value from the function.</span></span>

<span data-ttu-id="7ee31-136">Привязки используют параметры приложения для строк подключения, чтобы обеспечить соблюдение рекомендаций, согласно которым файл *function.json* не должен содержать секреты службы.</span><span class="sxs-lookup"><span data-stu-id="7ee31-136">Bindings use app settings for connection strings to enforce the best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="7ee31-137">Затем используются идентификаторы, указанные в коде для интеграции со службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee31-137">Then, use the identifiers you provided to integrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The second parameter to context.done is used as the value for the new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

<span data-ttu-id="7ee31-138">Ниже приведено содержимое файла *function.json*, соответствующее предыдущему коду.</span><span class="sxs-lookup"><span data-stu-id="7ee31-138">Here is the *function.json* that corresponds to the preceding code.</span></span> <span data-ttu-id="7ee31-139">Обратите внимание, что конфигурацию можно использовать независимо от языка реализации функции.</span><span class="sxs-lookup"><span data-stu-id="7ee31-139">Note that the same configuration can be used, regardless of the language of the function implementation.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
<span data-ttu-id="7ee31-140">Чтобы просмотреть и отредактировать содержимое файла *function.json* на портале Azure, щелкните параметр **Расширенный редактор** на вкладке **Интегрировать** этой функции.</span><span class="sxs-lookup"><span data-stu-id="7ee31-140">To view and edit the contents of *function.json* in the Azure portal, click the **Advanced editor** option on the **Integrate** tab of your function.</span></span>

<span data-ttu-id="7ee31-141">Дополнительные примеры кода и сведения об интеграции со службой хранилища Azure см. в статье [Привязки больших двоичных объектов службы хранилища для Функций Azure](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="7ee31-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="7ee31-142">Направление привязки</span><span class="sxs-lookup"><span data-stu-id="7ee31-142">Binding direction</span></span>

<span data-ttu-id="7ee31-143">У всех триггеров и привязок есть направление (свойство `direction`):</span><span class="sxs-lookup"><span data-stu-id="7ee31-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="7ee31-144">Для триггеров направление всегда входящее (`in`).</span><span class="sxs-lookup"><span data-stu-id="7ee31-144">For triggers, the direction is always `in`</span></span>
- <span data-ttu-id="7ee31-145">Для входных и выходных привязок используется как входящее (`in`), так и исходящее (`out`) направление.</span><span class="sxs-lookup"><span data-stu-id="7ee31-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="7ee31-146">Некоторые привязки поддерживают специальное направление `inout`.</span><span class="sxs-lookup"><span data-stu-id="7ee31-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="7ee31-147">При использовании `inout` на вкладке **Интегрировать** доступен только параметр **Расширенный редактор**.</span><span class="sxs-lookup"><span data-stu-id="7ee31-147">If you use `inout`, only the **Advanced editor** is available in the **Integrate** tab.</span></span>

## <a name="using-the-function-return-type-to-return-a-single-output"></a><span data-ttu-id="7ee31-148">Использование возвращаемого функцией типа для возврата одного выходного значения</span><span class="sxs-lookup"><span data-stu-id="7ee31-148">Using the function return type to return a single output</span></span>

<span data-ttu-id="7ee31-149">В предыдущем примере показано, как использовать возвращаемое значение функции для предоставления выходного значения привязке, обращение к которой осуществляется с помощью параметра специального имени `$return`.</span><span class="sxs-lookup"><span data-stu-id="7ee31-149">The preceding example shows how to use the function return value to provide output to a binding, which is achieved by using the special name parameter `$return`.</span></span> <span data-ttu-id="7ee31-150">(Это поддерживается только в языках, у которых есть возвращаемое значение, например C#, JavaScript и F#.) Если у функции несколько выходных привязок, используйте `$return` только для одной из них.</span><span class="sxs-lookup"><span data-stu-id="7ee31-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of the output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="7ee31-151">В примерах ниже показано, как возвращаемые типы используются с выходными привязками в C#, JavaScript и F#.</span><span class="sxs-lookup"><span data-stu-id="7ee31-151">The examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in the second parameter to context.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a><span data-ttu-id="7ee31-152">Свойство привязки dataType</span><span class="sxs-lookup"><span data-stu-id="7ee31-152">Binding dataType property</span></span>

<span data-ttu-id="7ee31-153">В .NET используйте типы для определения типа входных данных.</span><span class="sxs-lookup"><span data-stu-id="7ee31-153">In .NET, use the types to define the data type for input data.</span></span> <span data-ttu-id="7ee31-154">Например, используйте `string` для привязки к тексту триггера очереди и массив байтов для чтения в двоичном формате.</span><span class="sxs-lookup"><span data-stu-id="7ee31-154">For instance, use `string` to bind to the text of a queue trigger and a byte array to read as binary.</span></span>

<span data-ttu-id="7ee31-155">Для языков с динамическим вводом, таких как JavaScript, используйте свойство `dataType` в определении привязки.</span><span class="sxs-lookup"><span data-stu-id="7ee31-155">For languages that are dynamically typed such as JavaScript, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="7ee31-156">Например, чтобы считать содержимое HTTP-запроса в двоичном формате, используйте тип `binary`:</span><span class="sxs-lookup"><span data-stu-id="7ee31-156">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="7ee31-157">Другие параметры для `dataType`: `stream` и `string`.</span><span class="sxs-lookup"><span data-stu-id="7ee31-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="7ee31-158">Разрешение параметров приложения</span><span class="sxs-lookup"><span data-stu-id="7ee31-158">Resolving app settings</span></span>
<span data-ttu-id="7ee31-159">Для управления секретами и строками подключения рекомендуется использовать параметры приложения, а не файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7ee31-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="7ee31-160">Это ограничивает доступ к таким секретам и обеспечивает безопасное хранение файла *function.json* в общедоступном репозитории системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="7ee31-160">This limits access to these secrets and makes it safe to store *function.json* in a public source control repository.</span></span>

<span data-ttu-id="7ee31-161">Параметры приложений также удобно использовать при необходимости изменить конфигурации в соответствии со средой.</span><span class="sxs-lookup"><span data-stu-id="7ee31-161">App settings are also useful whenever you want to change configuration based on the environment.</span></span> <span data-ttu-id="7ee31-162">Например, в тестовой среде можно отслеживать другую очередь или контейнер хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="7ee31-162">For example, in a test environment, you may want to monitor a different queue or blob storage container.</span></span>

<span data-ttu-id="7ee31-163">Параметры приложения разрешаются, если значение заключено в знаки процента, например `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="7ee31-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="7ee31-164">Обратите внимание, что свойство `connection` триггеров и привязок является особым случаем и автоматически разрешает значения как параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="7ee31-164">Note that the `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="7ee31-165">Следующий пример представляет собой триггер очередей. Этот триггер использует параметр приложения `%input-queue-name%`, чтобы определить очередь, для которой он должен срабатывать.</span><span class="sxs-lookup"><span data-stu-id="7ee31-165">The following example is a queue trigger that uses an app setting `%input-queue-name%` to define the queue to trigger on.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a><span data-ttu-id="7ee31-166">Свойства метаданных триггера</span><span class="sxs-lookup"><span data-stu-id="7ee31-166">Trigger metadata properties</span></span>

<span data-ttu-id="7ee31-167">Помимо полезных данных, предоставляемых триггером (например, сообщения очереди, инициирующего вызов функции), многие триггеры предоставляют также дополнительные значения метаданных.</span><span class="sxs-lookup"><span data-stu-id="7ee31-167">In addition to the data payload provided by a trigger (such as the queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="7ee31-168">Эти значения можно использовать в качестве входных параметров в C# и F# или свойств объекта `context.bindings` в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7ee31-168">These values can be used as input parameters in C# and F# or properties on the `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="7ee31-169">Например, триггер очереди поддерживает следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="7ee31-169">For example, a queue trigger supports the following properties:</span></span>

* <span data-ttu-id="7ee31-170">QueueTrigger (содержимое активирующего сообщения, если строка допустима)</span><span class="sxs-lookup"><span data-stu-id="7ee31-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="7ee31-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="7ee31-171">DequeueCount</span></span>
* <span data-ttu-id="7ee31-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="7ee31-172">ExpirationTime</span></span>
* <span data-ttu-id="7ee31-173">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="7ee31-173">Id</span></span>
* <span data-ttu-id="7ee31-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="7ee31-174">InsertionTime</span></span>
* <span data-ttu-id="7ee31-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="7ee31-175">NextVisibleTime</span></span>
* <span data-ttu-id="7ee31-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="7ee31-176">PopReceipt</span></span>

<span data-ttu-id="7ee31-177">Сведения о свойствах метаданных для каждого триггера приведены в соответствующем разделе справки.</span><span class="sxs-lookup"><span data-stu-id="7ee31-177">Details of metadata properties for each trigger are described in the corresponding reference topic.</span></span> <span data-ttu-id="7ee31-178">Документация доступна также на портале на вкладке **Интегрировать** в разделе **Документация** под областью конфигурации привязки.</span><span class="sxs-lookup"><span data-stu-id="7ee31-178">Documentation is also available in the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.</span></span>  

<span data-ttu-id="7ee31-179">Например, поскольку у триггеров BLOB-объекта есть определенная задержка, для выполнения функции можно использовать триггер очередей (см. раздел [Триггер хранилища BLOB-объектов](functions-bindings-storage-blob.md#storage-blob-trigger)).</span><span class="sxs-lookup"><span data-stu-id="7ee31-179">For example, since blob triggers have some delays, you can use a queue trigger to run your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="7ee31-180">Сообщение очереди будет содержать имя файла BLOB-объекта, по которому активируется триггер.</span><span class="sxs-lookup"><span data-stu-id="7ee31-180">The queue message would contain the blob filename to trigger on.</span></span> <span data-ttu-id="7ee31-181">Используя свойство метаданных `queueTrigger`, можно задать такое поведение не в коде, а в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7ee31-181">Using the `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

<span data-ttu-id="7ee31-182">Свойства метаданных из триггера могут также использоваться в *выражении привязки* для другой привязки, как описано в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="7ee31-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in the following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="7ee31-183">Выражения привязки и шаблоны</span><span class="sxs-lookup"><span data-stu-id="7ee31-183">Binding expressions and patterns</span></span>

<span data-ttu-id="7ee31-184">*Выражения привязки* — это одна из самых эффективных функций триггеров и привязок.</span><span class="sxs-lookup"><span data-stu-id="7ee31-184">One of the most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="7ee31-185">В привязке можно определить шаблоны выражений, которые затем можно использовать в других привязках или коде.</span><span class="sxs-lookup"><span data-stu-id="7ee31-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="7ee31-186">Метаданные триггера также могут использоваться в выражениях привязки, как показано в примере в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="7ee31-186">Trigger metadata can also be used in binding expressions, as show in the sample in the preceding section.</span></span>

<span data-ttu-id="7ee31-187">Предположим, например, что необходимо изменить размер изображения в определенном контейнере хранилища BLOB-объектов аналогично тому, как это делается в шаблоне **изменения размера изображения** на странице **Новая функция**.</span><span class="sxs-lookup"><span data-stu-id="7ee31-187">For example, suppose you want to resize images in particular blob storage container, similar to the **Image Resizer** template in the **New Function** page.</span></span> <span data-ttu-id="7ee31-188">Последовательно выберите **Новая функция** -> Язык **C#** -> Сценарий **Примеры** -> **ImageResizer-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="7ee31-188">Go to **New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="7ee31-189">Ниже приведено определение *function.json*:</span><span class="sxs-lookup"><span data-stu-id="7ee31-189">Here is the *function.json* definition:</span></span>

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

<span data-ttu-id="7ee31-190">Обратите внимание, что параметр `filename` используется как в определении триггера BLOB-объектов, так и в выходной привязке большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="7ee31-190">Notice that the `filename` parameter is used in both the blob trigger definition as well as the blob output binding.</span></span> <span data-ttu-id="7ee31-191">Этот параметр можно также использовать в коде функции.</span><span class="sxs-lookup"><span data-stu-id="7ee31-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="7ee31-192">Случайные значения GUID</span><span class="sxs-lookup"><span data-stu-id="7ee31-192">Random GUIDs</span></span>
<span data-ttu-id="7ee31-193">Функции Azure предоставляют удобный синтаксис для создания в привязках идентификаторов GUID с помощью выражения привязки `{rand-guid}`.</span><span class="sxs-lookup"><span data-stu-id="7ee31-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through the `{rand-guid}` binding expression.</span></span> <span data-ttu-id="7ee31-194">В следующем примере эта возможность используется для создания уникального имени большого двоичного объекта:</span><span class="sxs-lookup"><span data-stu-id="7ee31-194">The following example uses this to generate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="7ee31-195">Текущее время</span><span class="sxs-lookup"><span data-stu-id="7ee31-195">Current time</span></span>

<span data-ttu-id="7ee31-196">Вы можете использовать выражение привязки `DateTime`, разрешающееся в `DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="7ee31-196">You can use the binding expression `DateTime`, which resolves to `DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-to-custom-input-properties-in-a-binding-expression"></a><span data-ttu-id="7ee31-197">Привязка к пользовательским входным свойствам в выражении привязки</span><span class="sxs-lookup"><span data-stu-id="7ee31-197">Bind to custom input properties in a binding expression</span></span>

<span data-ttu-id="7ee31-198">Выражения привязки могут также ссылаться на свойства, определенные в самих полезных данных.</span><span class="sxs-lookup"><span data-stu-id="7ee31-198">Binding expressions can also reference properties that are defined in the trigger payload itself.</span></span> <span data-ttu-id="7ee31-199">Например, можно установить динамическую привязку к файлу хранилища BLOB-объектов из файла, имя которого указанно в webhook.</span><span class="sxs-lookup"><span data-stu-id="7ee31-199">For example, you may want to dynamically bind to a blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="7ee31-200">Например, в приведенном ниже файле *function.json* используется свойство `BlobName` из полезных данных триггера.</span><span class="sxs-lookup"><span data-stu-id="7ee31-200">For example, the following *function.json* uses a property called `BlobName` from the trigger payload:</span></span>

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

<span data-ttu-id="7ee31-201">Для этого в C# и F# необходимо определить тип POCO, определяющий поля, которые будут десериализованы в полезные данные триггера.</span><span class="sxs-lookup"><span data-stu-id="7ee31-201">To accomplish this in C# and F#, you must define a POCO that defines the fields that will be deserialized in the trigger payload.</span></span>

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

<span data-ttu-id="7ee31-202">В JavaScript десериализация JSON выполняется автоматически и свойства можно использовать напрямую.</span><span class="sxs-lookup"><span data-stu-id="7ee31-202">In JavaScript, JSON deserialization is automatically performed and you can use the properties directly.</span></span>

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="7ee31-203">Настройка данных привязки во время выполнения</span><span class="sxs-lookup"><span data-stu-id="7ee31-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="7ee31-204">В C# и других языках .NET вы можете использовать императивный шаблон привязки в отличие от декларативных привязок в *function.json*.</span><span class="sxs-lookup"><span data-stu-id="7ee31-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in *function.json*.</span></span> <span data-ttu-id="7ee31-205">Императивную привязку удобно использовать, когда параметры привязки должны вычисляться не при проектировании, а во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="7ee31-205">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="7ee31-206">Дополнительные сведения см. в разделе справочника разработчика C# [Привязка в среде выполнения с помощью императивных привязок](functions-reference-csharp.md#imperative-bindings).</span><span class="sxs-lookup"><span data-stu-id="7ee31-206">To learn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in the C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ee31-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ee31-207">Next steps</span></span>
<span data-ttu-id="7ee31-208">Дополнительные сведения о конкретной привязке см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="7ee31-208">For more information on a specific binding, see the following articles:</span></span>

- [<span data-ttu-id="7ee31-209">HTTP и вызовы webhook</span><span class="sxs-lookup"><span data-stu-id="7ee31-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="7ee31-210">Таймер</span><span class="sxs-lookup"><span data-stu-id="7ee31-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="7ee31-211">Хранилище очередей</span><span class="sxs-lookup"><span data-stu-id="7ee31-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="7ee31-212">Хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="7ee31-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="7ee31-213">Хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="7ee31-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="7ee31-214">Концентратор событий</span><span class="sxs-lookup"><span data-stu-id="7ee31-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="7ee31-215">Служебная шина</span><span class="sxs-lookup"><span data-stu-id="7ee31-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="7ee31-216">База данных Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7ee31-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="7ee31-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="7ee31-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="7ee31-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="7ee31-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="7ee31-219">Центры уведомлений</span><span class="sxs-lookup"><span data-stu-id="7ee31-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="7ee31-220">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="7ee31-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="7ee31-221">Внешний файл</span><span class="sxs-lookup"><span data-stu-id="7ee31-221">External file</span></span>](functions-bindings-external-file.md)
