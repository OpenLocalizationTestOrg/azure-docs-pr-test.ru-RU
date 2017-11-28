---
title: "aaaWork триггеров и привязок в функциях Azure | Документы Microsoft"
description: "Узнайте, как триггеры toouse и привязки в tooconnect функции Azure вашей события tooonline выполнения кода и облачных служб."
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
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="a2cfc-104">Основные понятия триггеров и привязок в Функциях Azure</span><span class="sxs-lookup"><span data-stu-id="a2cfc-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="a2cfc-105">Функции Azure позволяет toowrite код в ответ tooevents Azure и другие службы через *триггеры* и *привязки*.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-105">Azure Functions allows you toowrite code in response tooevents in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="a2cfc-106">В этой статье приведены общие сведения о триггерах и привязках для всех поддерживаемых языков программирования.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="a2cfc-107">Здесь описаны компоненты, общие tooall привязки.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-107">Features that are common tooall bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="a2cfc-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="a2cfc-108">Overview</span></span>

<span data-ttu-id="a2cfc-109">Триггеры и привязки являются toodefine декларативным способом способ вызова функции и какие данные она работает с.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-109">Triggers and bindings are a declarative way toodefine how a function is invoked and what data it works with.</span></span> <span data-ttu-id="a2cfc-110">*Триггер* определяет способ вызова функции.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="a2cfc-111">У функции должен быть только один триггер.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="a2cfc-112">Триггеры имеют связанные данные, которые обычно являются полезные данные hello, запустившего функции hello.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-112">Triggers have associated data, which is usually hello payload that triggered hello function.</span></span> 

<span data-ttu-id="a2cfc-113">Ввод и вывод *привязки* предоставляют toodata tooconnect декларативным способом из кода.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-113">Input and output *bindings* provide a declarative way tooconnect toodata from within your code.</span></span> <span data-ttu-id="a2cfc-114">Аналогичные tootriggers можно определить строки соединений и другие свойства в конфигурации функции.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-114">Similar tootriggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="a2cfc-115">Привязки необязательны, а у функции может быть несколько входных и выходных привязок.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="a2cfc-116">С помощью триггеров и привязок, можно написать код, более универсален и выполняет не следует жестко кодировать hello сведения hello служб, с которыми он взаимодействует.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-116">Using triggers and bindings, you can write code that is more generic and does not hardcode hello details of hello services with which it interacts.</span></span> <span data-ttu-id="a2cfc-117">Данные, поступающие из служб, становятся для кода вашей функции обычными входными значениями.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="a2cfc-118">Служба tooanother toooutput данных (например, для создания новой строки в таблице хранилища Azure), использовать возвращаемое значение метода hello hello.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-118">toooutput data tooanother service (such as creating a new row in Azure Table Storage), use hello return value of hello method.</span></span> <span data-ttu-id="a2cfc-119">Также при необходимости toooutput несколько значений, можно использовать вспомогательный объект.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-119">Or, if you need toooutput multiple values, use a helper object.</span></span> <span data-ttu-id="a2cfc-120">Триггеры и привязки получают **имя** свойства, которое представляет собой идентификатор, который используется в привязке hello tooaccess кода.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-120">Triggers and bindings have a **name** property, which is an identifier you use in your code tooaccess hello binding.</span></span>

<span data-ttu-id="a2cfc-121">Триггеры и привязки можно настроить в hello **Интеграция** вкладка на портале Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-121">You can configure triggers and bindings in hello **Integrate** tab in hello Azure Functions portal.</span></span> <span data-ttu-id="a2cfc-122">На деле hello hello пользовательского интерфейса изменяет файл с именем *function.json* файл в каталоге функции hello.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-122">Under hello covers, hello UI modifies a file called *function.json* file in hello function directory.</span></span> <span data-ttu-id="a2cfc-123">Этот файл можно редактировать путем изменения toohello **расширенный редактор**.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-123">You can edit this file by changing toohello **Advanced editor**.</span></span>

<span data-ttu-id="a2cfc-124">Hello следующей таблице показаны триггеры hello и привязками, которые поддерживаются с помощью функций Azure.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-124">hello following table shows hello triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="a2cfc-125">Пример. Триггер очередей и выходная привязка таблицы</span><span class="sxs-lookup"><span data-stu-id="a2cfc-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="a2cfc-126">Предположим, требуется toowrite новый tooAzure строки таблицы хранилища, при появлении нового сообщения в очередь хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-126">Suppose you want toowrite a new row tooAzure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="a2cfc-127">Этот сценарий может быть реализован с помощью триггера очередей Azure и выходной привязки таблицы.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="a2cfc-128">Очередь триггера требуется hello следующую информацию в hello **Интеграция** вкладки:</span><span class="sxs-lookup"><span data-stu-id="a2cfc-128">A queue trigger requires hello following information in hello **Integrate** tab:</span></span>

* <span data-ttu-id="a2cfc-129">Имя параметра приложения hello, содержащий hello строка подключения учетной записи хранилища для очереди hello Hello</span><span class="sxs-lookup"><span data-stu-id="a2cfc-129">hello name of hello app setting that contains hello storage account connection string for hello queue</span></span>
* <span data-ttu-id="a2cfc-130">Имя очереди Hello</span><span class="sxs-lookup"><span data-stu-id="a2cfc-130">hello queue name</span></span>
* <span data-ttu-id="a2cfc-131">Здравствуйте, идентификатор в ваш код tooread hello содержимое сообщения hello очереди, такие как `order`.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-131">hello identifier in your code tooread hello contents of hello queue message, such as `order`.</span></span>

<span data-ttu-id="a2cfc-132">toowrite tooAzure хранилище таблиц использовать привязку с возможностью вывода hello, приведенные ниже сведения:</span><span class="sxs-lookup"><span data-stu-id="a2cfc-132">toowrite tooAzure Table Storage, use an output binding with hello following details:</span></span>

* <span data-ttu-id="a2cfc-133">Имя параметра приложения hello, содержащий hello строка подключения учетной записи хранилища для таблицы hello Hello</span><span class="sxs-lookup"><span data-stu-id="a2cfc-133">hello name of hello app setting that contains hello storage account connection string for hello table</span></span>
* <span data-ttu-id="a2cfc-134">Имя таблицы Hello</span><span class="sxs-lookup"><span data-stu-id="a2cfc-134">hello table name</span></span>
* <span data-ttu-id="a2cfc-135">Идентификатор Hello в ваш код toocreate выходные элементы или возвращаемое значение функции hello hello.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-135">hello identifier in your code toocreate output items, or hello return value from hello function.</span></span>

<span data-ttu-id="a2cfc-136">Привязки использовать параметры приложения для практики наиболее hello tooenforce строки подключения, *function.json* не содержит секретные данные службы.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-136">Bindings use app settings for connection strings tooenforce hello best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="a2cfc-137">Затем с помощью идентификаторов hello вам предоставлены toointegrate хранилища Azure в коде.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-137">Then, use hello identifiers you provided toointegrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
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
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
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

<span data-ttu-id="a2cfc-138">Вот hello *function.json* , соответствующий toohello предшествующий код.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-138">Here is hello *function.json* that corresponds toohello preceding code.</span></span> <span data-ttu-id="a2cfc-139">Обратите внимание, что hello, можно использовать такую же настройку независимо от языка hello реализации функции hello.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-139">Note that hello same configuration can be used, regardless of hello language of hello function implementation.</span></span>

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
<span data-ttu-id="a2cfc-140">tooview и измените hello содержимое *function.json* в hello портал Azure, щелкните hello **расширенный редактор** параметр hello **Интеграция** вкладку этой функции.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-140">tooview and edit hello contents of *function.json* in hello Azure portal, click hello **Advanced editor** option on hello **Integrate** tab of your function.</span></span>

<span data-ttu-id="a2cfc-141">Дополнительные примеры кода и сведения об интеграции со службой хранилища Azure см. в статье [Привязки больших двоичных объектов службы хранилища для Функций Azure](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a2cfc-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="a2cfc-142">Направление привязки</span><span class="sxs-lookup"><span data-stu-id="a2cfc-142">Binding direction</span></span>

<span data-ttu-id="a2cfc-143">У всех триггеров и привязок есть направление (свойство `direction`):</span><span class="sxs-lookup"><span data-stu-id="a2cfc-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="a2cfc-144">Для триггеров всегда является направление hello`in`</span><span class="sxs-lookup"><span data-stu-id="a2cfc-144">For triggers, hello direction is always `in`</span></span>
- <span data-ttu-id="a2cfc-145">Для входных и выходных привязок используется как входящее (`in`), так и исходящее (`out`) направление.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="a2cfc-146">Некоторые привязки поддерживают специальное направление `inout`.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="a2cfc-147">Если вы используете `inout`, только hello **расширенный редактор** доступен в hello **интеграции** вкладку.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-147">If you use `inout`, only hello **Advanced editor** is available in hello **Integrate** tab.</span></span>

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a><span data-ttu-id="a2cfc-148">С помощью tooreturn тип возвращаемого значения функции hello один выход</span><span class="sxs-lookup"><span data-stu-id="a2cfc-148">Using hello function return type tooreturn a single output</span></span>

<span data-ttu-id="a2cfc-149">Hello предыдущем примере показано, как tooprovide возвращаемое значение функции hello toouse вывода tooa привязку, что достигается с помощью параметра специальным именем hello `$return`.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-149">hello preceding example shows how toouse hello function return value tooprovide output tooa binding, which is achieved by using hello special name parameter `$return`.</span></span> <span data-ttu-id="a2cfc-150">(Это поддерживается только в языках, у которых есть возвращаемое значение, например C#, JavaScript и F#.) Если функция имеет несколько привязок выходные данные, используйте `$return` только для одного из привязок выходного hello.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of hello output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="a2cfc-151">Примеры Hello ниже показано как возвращаемые типы используются с привязками выходные данные в C#, JavaScript и F #.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-151">hello examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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
// JavaScript: return a value in hello second parameter toocontext.done
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

## <a name="binding-datatype-property"></a><span data-ttu-id="a2cfc-152">Свойство привязки dataType</span><span class="sxs-lookup"><span data-stu-id="a2cfc-152">Binding dataType property</span></span>

<span data-ttu-id="a2cfc-153">В .NET используйте типы toodefine hello hello-тип данных для входных данных.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-153">In .NET, use hello types toodefine hello data type for input data.</span></span> <span data-ttu-id="a2cfc-154">Например, использовать `string` toobind toohello текст триггера очереди и tooread массива байтов в двоичном виде.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-154">For instance, use `string` toobind toohello text of a queue trigger and a byte array tooread as binary.</span></span>

<span data-ttu-id="a2cfc-155">Для языков, которые вводятся динамически, таких как JavaScript, использовать hello `dataType` свойство в определении hello привязки.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-155">For languages that are dynamically typed such as JavaScript, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="a2cfc-156">Например, tooread hello содержимого HTTP-запроса в двоичном формате, используйте тип hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="a2cfc-156">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="a2cfc-157">Другие варианты для `dataType` — `stream` и `string`.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="a2cfc-158">Разрешение параметров приложения</span><span class="sxs-lookup"><span data-stu-id="a2cfc-158">Resolving app settings</span></span>
<span data-ttu-id="a2cfc-159">Для управления секретами и строками подключения рекомендуется использовать параметры приложения, а не файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="a2cfc-160">Это ограничивает доступ toothese секреты и делает его безопасный toostore *function.json* в репозитории открытого исходного элемента управления.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-160">This limits access toothese secrets and makes it safe toostore *function.json* in a public source control repository.</span></span>

<span data-ttu-id="a2cfc-161">Параметры приложения также полезны, когда захотите toochange конфигурации, в зависимости от среды hello.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-161">App settings are also useful whenever you want toochange configuration based on hello environment.</span></span> <span data-ttu-id="a2cfc-162">Например в тестовой среде, может потребоваться toomonitor в другой контейнер хранилища очереди или большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-162">For example, in a test environment, you may want toomonitor a different queue or blob storage container.</span></span>

<span data-ttu-id="a2cfc-163">Параметры приложения разрешаются, если значение заключено в знаки процента, например `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="a2cfc-164">Обратите внимание, что hello `connection` свойства триггеров и привязки является особым случаем и автоматически разрешает значения как параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-164">Note that hello `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="a2cfc-165">Hello следующий пример является очередь триггер, который использует Настройка приложения `%input-queue-name%` tootrigger очереди toodefine hello на.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-165">hello following example is a queue trigger that uses an app setting `%input-queue-name%` toodefine hello queue tootrigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="a2cfc-166">Свойства метаданных триггера</span><span class="sxs-lookup"><span data-stu-id="a2cfc-166">Trigger metadata properties</span></span>

<span data-ttu-id="a2cfc-167">В полезных данных toohello сложения, предоставляемые триггера (например приветственное сообщение очереди, вызвавшей функцию) многие триггеры предоставляют дополнительные метаданные значения.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-167">In addition toohello data payload provided by a trigger (such as hello queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="a2cfc-168">Эти значения можно использовать в качестве входных параметров в C# и F # или свойствам hello `context.bindings` в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-168">These values can be used as input parameters in C# and F# or properties on hello `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="a2cfc-169">Например триггер очереди поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a2cfc-169">For example, a queue trigger supports hello following properties:</span></span>

* <span data-ttu-id="a2cfc-170">QueueTrigger (содержимое активирующего сообщения, если строка допустима)</span><span class="sxs-lookup"><span data-stu-id="a2cfc-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="a2cfc-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="a2cfc-171">DequeueCount</span></span>
* <span data-ttu-id="a2cfc-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="a2cfc-172">ExpirationTime</span></span>
* <span data-ttu-id="a2cfc-173">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="a2cfc-173">Id</span></span>
* <span data-ttu-id="a2cfc-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="a2cfc-174">InsertionTime</span></span>
* <span data-ttu-id="a2cfc-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="a2cfc-175">NextVisibleTime</span></span>
* <span data-ttu-id="a2cfc-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="a2cfc-176">PopReceipt</span></span>

<span data-ttu-id="a2cfc-177">Подробные сведения о метаданных свойства для каждого триггера, описаны в hello соответствующие разделы справки.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-177">Details of metadata properties for each trigger are described in hello corresponding reference topic.</span></span> <span data-ttu-id="a2cfc-178">Документация доступна также в hello **Интеграция** вкладку портала hello в hello **документации** ниже hello область конфигурации привязки.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-178">Documentation is also available in hello **Integrate** tab of hello portal, in hello **Documentation** section below hello binding configuration area.</span></span>  

<span data-ttu-id="a2cfc-179">Например, поскольку триггеры BLOB-объекта некоторое время, можно использовать очереди триггера toorun функции (см. [триггер хранилища больших двоичных объектов](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="a2cfc-179">For example, since blob triggers have some delays, you can use a queue trigger toorun your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="a2cfc-180">на приветственное сообщение очереди будет содержать tootrigger filename hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-180">hello queue message would contain hello blob filename tootrigger on.</span></span> <span data-ttu-id="a2cfc-181">С помощью hello `queueTrigger` свойства метаданных, можно указать данное поведение в конфигурацию, а не в коде.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-181">Using hello `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="a2cfc-182">Свойства метаданных из триггера может также использоваться в *выражение привязки* для другой привязке, как описано в разделе hello в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in hello following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="a2cfc-183">Выражения привязки и шаблоны</span><span class="sxs-lookup"><span data-stu-id="a2cfc-183">Binding expressions and patterns</span></span>

<span data-ttu-id="a2cfc-184">Одним из наиболее мощных функций hello триггеров и привязки является *привязки выражений*.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-184">One of hello most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="a2cfc-185">В привязке можно определить шаблоны выражений, которые затем можно использовать в других привязках или коде.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="a2cfc-186">Метаданные триггер также могут использоваться в привязке выражений, как показано в образце hello в предшествующих раздел hello.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-186">Trigger metadata can also be used in binding expressions, as show in hello sample in hello preceding section.</span></span>

<span data-ttu-id="a2cfc-187">Предположим, что вы хотите tooresize образы в контейнере отдельного большого двоичного объекта хранилища, аналогичные toohello **изменения размера изображения** шаблона в hello **новая функция** страницы.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-187">For example, suppose you want tooresize images in particular blob storage container, similar toohello **Image Resizer** template in hello **New Function** page.</span></span> <span data-ttu-id="a2cfc-188">Go слишком**новая функция** -> язык **C#** -> сценарии **образцы** -> **ImageResizer CSharp**.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-188">Go too**New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="a2cfc-189">Вот hello *function.json* определение:</span><span class="sxs-lookup"><span data-stu-id="a2cfc-189">Here is hello *function.json* definition:</span></span>

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

<span data-ttu-id="a2cfc-190">Обратите внимание, что hello `filename` используется параметр в определение триггера hello большого двоичного объекта как, так и больших двоичных объектов hello привязка для вывода.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-190">Notice that hello `filename` parameter is used in both hello blob trigger definition as well as hello blob output binding.</span></span> <span data-ttu-id="a2cfc-191">Этот параметр можно также использовать в коде функции.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="a2cfc-192">Случайные значения GUID</span><span class="sxs-lookup"><span data-stu-id="a2cfc-192">Random GUIDs</span></span>
<span data-ttu-id="a2cfc-193">Функции Azure предоставляет удобный синтаксис для формирования идентификаторов GUID в привязки, через hello `{rand-guid}` выражение привязки.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through hello `{rand-guid}` binding expression.</span></span> <span data-ttu-id="a2cfc-194">Hello следующий пример использует этот toogenerate имя уникальным большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-194">hello following example uses this toogenerate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="a2cfc-195">Текущее время</span><span class="sxs-lookup"><span data-stu-id="a2cfc-195">Current time</span></span>

<span data-ttu-id="a2cfc-196">Можно использовать выражение привязки hello `DateTime`, который разрешается слишком`DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-196">You can use hello binding expression `DateTime`, which resolves too`DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a><span data-ttu-id="a2cfc-197">Привязать свойства toocustom входа в выражение привязки</span><span class="sxs-lookup"><span data-stu-id="a2cfc-197">Bind toocustom input properties in a binding expression</span></span>

<span data-ttu-id="a2cfc-198">Привязки выражений может также ссылаться на свойства, определенные в полезных данных триггер hello сам.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-198">Binding expressions can also reference properties that are defined in hello trigger payload itself.</span></span> <span data-ttu-id="a2cfc-199">Например требуется файл toodynamically bind tooa BLOB-объекта хранилища из имени файла в веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-199">For example, you may want toodynamically bind tooa blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="a2cfc-200">Здравствуйте, например, следующая *function.json* использует свойство с именем `BlobName` из полезных данных триггер hello:</span><span class="sxs-lookup"><span data-stu-id="a2cfc-200">For example, hello following *function.json* uses a property called `BlobName` from hello trigger payload:</span></span>

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

<span data-ttu-id="a2cfc-201">tooaccomplish этого в C# и F #, необходимо определить POCO, определяющая hello поля, которые будут десериализованы в полезных данных hello триггера.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-201">tooaccomplish this in C# and F#, you must define a POCO that defines hello fields that will be deserialized in hello trigger payload.</span></span>

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

<span data-ttu-id="a2cfc-202">На языке JavaScript автоматически выполняется десериализация JSON и hello свойства можно использовать напрямую.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-202">In JavaScript, JSON deserialization is automatically performed and you can use hello properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="a2cfc-203">Настройка данных привязки во время выполнения</span><span class="sxs-lookup"><span data-stu-id="a2cfc-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="a2cfc-204">В C# и других языков .NET, можно использовать шаблон императивного привязки как противоположность toohello декларативной привязки в *function.json*.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed toohello declarative bindings in *function.json*.</span></span> <span data-ttu-id="a2cfc-205">Принудительный привязки полезно в том случае, если параметры привязки должны toobe вычислено во время выполнения, а не конструктора.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-205">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="a2cfc-206">toolearn более, в разделе [привязки во время выполнения с помощью императивного привязок](functions-reference-csharp.md#imperative-bindings) в Справочник разработчика hello C#.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-206">toolearn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in hello C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2cfc-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a2cfc-207">Next steps</span></span>
<span data-ttu-id="a2cfc-208">Дополнительные сведения о конкретной привязки см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="a2cfc-208">For more information on a specific binding, see hello following articles:</span></span>

- [<span data-ttu-id="a2cfc-209">HTTP и вызовы webhook</span><span class="sxs-lookup"><span data-stu-id="a2cfc-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="a2cfc-210">Таймер</span><span class="sxs-lookup"><span data-stu-id="a2cfc-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="a2cfc-211">Хранилище очередей</span><span class="sxs-lookup"><span data-stu-id="a2cfc-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="a2cfc-212">Хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="a2cfc-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="a2cfc-213">Хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="a2cfc-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="a2cfc-214">Концентратор событий</span><span class="sxs-lookup"><span data-stu-id="a2cfc-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="a2cfc-215">Служебная шина</span><span class="sxs-lookup"><span data-stu-id="a2cfc-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="a2cfc-216">База данных Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a2cfc-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="a2cfc-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="a2cfc-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="a2cfc-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="a2cfc-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="a2cfc-219">Центры уведомлений</span><span class="sxs-lookup"><span data-stu-id="a2cfc-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="a2cfc-220">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="a2cfc-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="a2cfc-221">Внешний файл</span><span class="sxs-lookup"><span data-stu-id="a2cfc-221">External file</span></span>](functions-bindings-external-file.md)
