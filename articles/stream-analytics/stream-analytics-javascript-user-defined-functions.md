---
title: "определяемые пользователем функции aaaAzure Stream Analytics JavaScript | Документы Microsoft"
description: "Выполнение расширенных запросов с помощью определяемых пользователем функций JavaScript"
keywords: "javascript, определяемые пользователем функции, udf"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="8d2c8-104">Определяемые пользователем функции JavaScript в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8d2c8-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="8d2c8-105">Azure Stream Analytics поддерживает определяемые пользователем функции, написанные на языке JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="8d2c8-106">С hello богатый набор **строка**, **RegExp**, **математические**, **массива**, и **даты** методы, Преобразования сложных данных с помощью задания Stream Analytics предоставляет JavaScript, и становятся проще toocreate.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-106">With hello rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier toocreate.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="8d2c8-107">Определяемые пользователем функции JavaScript</span><span class="sxs-lookup"><span data-stu-id="8d2c8-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="8d2c8-108">Определяемые пользователем функции JavaScript поддерживают скалярные вычислительные функции без отслеживания состояния, не требующие внешнего подключения.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="8d2c8-109">Hello возвращаемое значение функции может быть только скалярное значение (одно).</span><span class="sxs-lookup"><span data-stu-id="8d2c8-109">hello return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="8d2c8-110">После добавления задания tooa определяемой пользователем функции JavaScript, можно использовать функции hello в любом месте в hello запрос, подобный встроенной скалярной функции.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-110">After you add a JavaScript user-defined function tooa job, you can use hello function anywhere in hello query, like a built-in scalar function.</span></span>

<span data-ttu-id="8d2c8-111">Ниже приведены некоторые сценарии, в которых могут пригодиться определяемые пользователем функции JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="8d2c8-112">Анализ и обработка строки с использованием функций регулярных выражений, например **Regexp_Replace()** или **Regexp_Extract()**.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="8d2c8-113">Декодирование и кодирование данных, например преобразование двоичных данных в шестнадцатеричные.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="8d2c8-114">Математические вычисления с помощью объекта JavaScript **Math**.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="8d2c8-115">Операции с массивами, такие как сортировка, присоединение, поиск и заполнение.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="8d2c8-116">Вот некоторые действия, которые невозможно выполнить в Stream Analytics с помощью определяемой пользователем функции JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="8d2c8-117">Вызов внешних конечных точек REST, например выполнение обратного разрешения IP-адресов или извлечение ссылочных данных из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="8d2c8-118">Сериализация или десериализация входных и выходных данных в пользовательский формат сообщения.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="8d2c8-119">Создание пользовательских статистических функций.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-119">Create custom aggregates</span></span>

<span data-ttu-id="8d2c8-120">Несмотря на то, что функции, например **Date.GetDate()** или **Math.random()** не блокируются в определении функции hello, следует избегать их использования.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in hello functions definition, you should avoid using them.</span></span> <span data-ttu-id="8d2c8-121">Эти функции **не** возвращаемого hello же привести при каждом их вызове и hello службой Azure Stream Analytics не вести журнал вызовов функций и возвращены результаты.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-121">These functions **do not** return hello same result every time you call them, and hello Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="8d2c8-122">Если функция возвращает другой результат на hello того же события, повторяемость не гарантируется при перезапуске задания пользователем или службой hello Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-122">If a function returns different result on hello same events, repeatability is not guaranteed when a job is restarted by you or by hello Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a><span data-ttu-id="8d2c8-123">Добавьте определяемую пользователем функцию JavaScript в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8d2c8-123">Add a JavaScript user-defined function in hello Azure portal</span></span>
<span data-ttu-id="8d2c8-124">toocreate простой JavaScript определяемой пользователем функции в существующее задание Stream Analytics, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8d2c8-124">toocreate a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="8d2c8-125">Найдите задание Stream Analytics в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-125">In hello Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="8d2c8-126">В разделе **топология задания** выберите нужную функцию.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="8d2c8-127">Откроется пустой список функций.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="8d2c8-128">Выберите toocreate новой определяемой пользователем функции, **добавить**.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-128">toocreate a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="8d2c8-129">На hello **новая функция** колонке для **тип функции**выберите **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-129">On hello **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="8d2c8-130">Функция шаблона по умолчанию отображается в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-130">A default function template appears in hello editor.</span></span>
5.  <span data-ttu-id="8d2c8-131">Для hello **псевдоним определяемая пользователем Функция**, введите **hex2Int**и измените реализацию функции hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8d2c8-131">For hello **UDF alias**, enter **hex2Int**, and change hello function implementation as follows:</span></span>

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="8d2c8-132">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-132">Select **Save**.</span></span> <span data-ttu-id="8d2c8-133">Функции отображается в списке hello функции.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-133">Your function appears in hello list of functions.</span></span>
7.  <span data-ttu-id="8d2c8-134">Выберите hello новый **hex2Int** функцией и проверьте определение функции hello.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-134">Select hello new **hex2Int** function, and check hello function definition.</span></span> <span data-ttu-id="8d2c8-135">Все функции имеют **определяемой пользователем функции** префикс toohello добавлена функция псевдоним.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-135">All functions have a **UDF** prefix added toohello function alias.</span></span> <span data-ttu-id="8d2c8-136">Требуется слишком*включать префикс hello* при вызове функции hello в запросе Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-136">You need too*include hello prefix* when you call hello function in your Stream Analytics query.</span></span> <span data-ttu-id="8d2c8-137">В нашем примере нужно вызывать функцию **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="8d2c8-138">Вызов определяемой пользователем функции из запроса</span><span class="sxs-lookup"><span data-stu-id="8d2c8-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="8d2c8-139">В hello редактор запросов, в разделе **ТОПОЛОГИИ задания**выберите **запроса**.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-139">In hello query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="8d2c8-140">Изменение запроса, а затем вызвать hello определяемой пользователем функции, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8d2c8-140">Edit your query, and then call hello user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="8d2c8-141">hello tooupload образец файла данных, щелкните правой кнопкой мыши hello задания ввода.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-141">tooupload hello sample data file, right-click hello job input.</span></span>
4.  <span data-ttu-id="8d2c8-142">tootest ваш запрос, выберите **теста**.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-142">tootest your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="8d2c8-143">Поддерживаемые объекты JavaScript</span><span class="sxs-lookup"><span data-stu-id="8d2c8-143">Supported JavaScript objects</span></span>
<span data-ttu-id="8d2c8-144">Определяемые пользователем функции JavaScript в Azure Stream Analytics могут использовать все стандартные встроенные объекты JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="8d2c8-145">Список этих объектов вы найдете [здесь](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="8d2c8-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="8d2c8-146">Преобразование типов Stream Analytics и JavaScript</span><span class="sxs-lookup"><span data-stu-id="8d2c8-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="8d2c8-147">Существуют различия в hello типы, поддерживающие язык запросов Stream Analytics hello и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-147">There are differences in hello types that hello Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="8d2c8-148">В этой таблице перечислены hello преобразование сопоставления между двумя hello.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-148">This table lists hello conversion mappings between hello two:</span></span>

<span data-ttu-id="8d2c8-149">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8d2c8-149">Stream Analytics</span></span> | <span data-ttu-id="8d2c8-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="8d2c8-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="8d2c8-151">bigint</span><span class="sxs-lookup"><span data-stu-id="8d2c8-151">bigint</span></span> | <span data-ttu-id="8d2c8-152">Номер (JavaScript может представлять только целые числа вверх tooprecisely 2 ^ 53)</span><span class="sxs-lookup"><span data-stu-id="8d2c8-152">Number (JavaScript can only represent integers up tooprecisely 2^53)</span></span>
<span data-ttu-id="8d2c8-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="8d2c8-153">DateTime</span></span> | <span data-ttu-id="8d2c8-154">Дата (JavaScript поддерживает только миллисекунды)</span><span class="sxs-lookup"><span data-stu-id="8d2c8-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="8d2c8-155">double</span><span class="sxs-lookup"><span data-stu-id="8d2c8-155">double</span></span> | <span data-ttu-id="8d2c8-156">Number</span><span class="sxs-lookup"><span data-stu-id="8d2c8-156">Number</span></span>
<span data-ttu-id="8d2c8-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="8d2c8-157">nvarchar(MAX)</span></span> | <span data-ttu-id="8d2c8-158">Строка</span><span class="sxs-lookup"><span data-stu-id="8d2c8-158">String</span></span>
<span data-ttu-id="8d2c8-159">Record</span><span class="sxs-lookup"><span data-stu-id="8d2c8-159">Record</span></span> | <span data-ttu-id="8d2c8-160">Объект</span><span class="sxs-lookup"><span data-stu-id="8d2c8-160">Object</span></span>
<span data-ttu-id="8d2c8-161">Массив,</span><span class="sxs-lookup"><span data-stu-id="8d2c8-161">Array</span></span> | <span data-ttu-id="8d2c8-162">Массив,</span><span class="sxs-lookup"><span data-stu-id="8d2c8-162">Array</span></span>
<span data-ttu-id="8d2c8-163">NULL</span><span class="sxs-lookup"><span data-stu-id="8d2c8-163">NULL</span></span> | <span data-ttu-id="8d2c8-164">Null</span><span class="sxs-lookup"><span data-stu-id="8d2c8-164">Null</span></span>


<span data-ttu-id="8d2c8-165">Ниже описаны преобразования из типов JavaScript в типы Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="8d2c8-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="8d2c8-166">JavaScript</span></span> | <span data-ttu-id="8d2c8-167">Анализ потока</span><span class="sxs-lookup"><span data-stu-id="8d2c8-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="8d2c8-168">Number</span><span class="sxs-lookup"><span data-stu-id="8d2c8-168">Number</span></span> | <span data-ttu-id="8d2c8-169">Bigint (если число hello round и между долго. MinValue и долго. MaxValue; в противном случае — double)</span><span class="sxs-lookup"><span data-stu-id="8d2c8-169">Bigint (if hello number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="8d2c8-170">Дата</span><span class="sxs-lookup"><span data-stu-id="8d2c8-170">Date</span></span> | <span data-ttu-id="8d2c8-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="8d2c8-171">DateTime</span></span>
<span data-ttu-id="8d2c8-172">Строка</span><span class="sxs-lookup"><span data-stu-id="8d2c8-172">String</span></span> | <span data-ttu-id="8d2c8-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="8d2c8-173">nvarchar(MAX)</span></span>
<span data-ttu-id="8d2c8-174">Объект</span><span class="sxs-lookup"><span data-stu-id="8d2c8-174">Object</span></span> | <span data-ttu-id="8d2c8-175">Record</span><span class="sxs-lookup"><span data-stu-id="8d2c8-175">Record</span></span>
<span data-ttu-id="8d2c8-176">Массив,</span><span class="sxs-lookup"><span data-stu-id="8d2c8-176">Array</span></span> | <span data-ttu-id="8d2c8-177">Массив,</span><span class="sxs-lookup"><span data-stu-id="8d2c8-177">Array</span></span>
<span data-ttu-id="8d2c8-178">NULL, не определено</span><span class="sxs-lookup"><span data-stu-id="8d2c8-178">Null, Undefined</span></span> | <span data-ttu-id="8d2c8-179">NULL</span><span class="sxs-lookup"><span data-stu-id="8d2c8-179">NULL</span></span>
<span data-ttu-id="8d2c8-180">Любой другой тип (например, функция или ошибка)</span><span class="sxs-lookup"><span data-stu-id="8d2c8-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="8d2c8-181">Не поддерживается (возникает ошибка времени выполнения)</span><span class="sxs-lookup"><span data-stu-id="8d2c8-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8d2c8-182">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="8d2c8-182">Troubleshooting</span></span>
<span data-ttu-id="8d2c8-183">Ошибки среды выполнения JavaScript считаются неустранимыми и подключаемых через журнал действий hello.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-183">JavaScript runtime errors are considered fatal, and are surfaced through hello Activity log.</span></span> <span data-ttu-id="8d2c8-184">Журнал hello tooretrieve, hello портал Azure, откройте tooyour задание и выберите **журнал действий**.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-184">tooretrieve hello log, in hello Azure portal, go tooyour job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="8d2c8-185">Другие методы использования определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="8d2c8-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-toooutput"></a><span data-ttu-id="8d2c8-186">Записи вложенных toooutput JSON</span><span class="sxs-lookup"><span data-stu-id="8d2c8-186">Write nested JSON toooutput</span></span>
<span data-ttu-id="8d2c8-187">Если имеются дополнительные инструкции обработки шаг, который используется в качестве входных данных выходные данные задания Stream Analytics, и его требуется формат JSON, можно написать toooutput строка JSON.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string toooutput.</span></span> <span data-ttu-id="8d2c8-188">Следующий пример Hello вызывает hello **JSON.stringify()** функции toopack все пары "имя значение" hello входные данные и записывают их в виде одно строковое значение в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8d2c8-188">hello next example calls hello **JSON.stringify()** function toopack all name/value pairs of hello input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="8d2c8-189">**Определение определяемой пользователем функции JavaScript:**</span><span class="sxs-lookup"><span data-stu-id="8d2c8-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="8d2c8-190">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="8d2c8-190">**Sample query:**</span></span>
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a><span data-ttu-id="8d2c8-191">Получение справки</span><span class="sxs-lookup"><span data-stu-id="8d2c8-191">Get help</span></span>
<span data-ttu-id="8d2c8-192">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="8d2c8-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d2c8-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d2c8-193">Next steps</span></span>
* [<span data-ttu-id="8d2c8-194">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8d2c8-194">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8d2c8-195">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8d2c8-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8d2c8-196">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8d2c8-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="8d2c8-197">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Azure Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="8d2c8-197">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)</span></span>
* <span data-ttu-id="8d2c8-198">[Azure Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx) (Справочник по API-интерфейсу REST для управления Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="8d2c8-198">[Azure Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)</span></span>
