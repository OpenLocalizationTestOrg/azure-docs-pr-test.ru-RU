---
title: "Определяемые пользователем функции JavaScript в Azure Stream Analytics | Документация Майкрософт"
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
ms.openlocfilehash: e4a9e6c7078031240c22a51378c0459426b7f626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="d63df-104">Определяемые пользователем функции JavaScript в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d63df-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="d63df-105">Azure Stream Analytics поддерживает определяемые пользователем функции, написанные на языке JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d63df-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="d63df-106">Благодаря обширному набору методов, которые предоставляют объекты JavaScript **String**, **RegExp**, **Math**, **Array** и **Date**, в заданиях Stream Analytics стало проще создавать сложные преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="d63df-106">With the rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier to create.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="d63df-107">Определяемые пользователем функции JavaScript</span><span class="sxs-lookup"><span data-stu-id="d63df-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="d63df-108">Определяемые пользователем функции JavaScript поддерживают скалярные вычислительные функции без отслеживания состояния, не требующие внешнего подключения.</span><span class="sxs-lookup"><span data-stu-id="d63df-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="d63df-109">Возвращаемое значение функции может быть только скалярным (одиночным).</span><span class="sxs-lookup"><span data-stu-id="d63df-109">The return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="d63df-110">Добавив в задание определяемую пользователем функцию JavaScript, вы сможете использовать ее в любом месте запроса, например во встроенной скалярной функции.</span><span class="sxs-lookup"><span data-stu-id="d63df-110">After you add a JavaScript user-defined function to a job, you can use the function anywhere in the query, like a built-in scalar function.</span></span>

<span data-ttu-id="d63df-111">Ниже приведены некоторые сценарии, в которых могут пригодиться определяемые пользователем функции JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d63df-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="d63df-112">Анализ и обработка строки с использованием функций регулярных выражений, например **Regexp_Replace()** или **Regexp_Extract()**.</span><span class="sxs-lookup"><span data-stu-id="d63df-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="d63df-113">Декодирование и кодирование данных, например преобразование двоичных данных в шестнадцатеричные.</span><span class="sxs-lookup"><span data-stu-id="d63df-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="d63df-114">Математические вычисления с помощью объекта JavaScript **Math**.</span><span class="sxs-lookup"><span data-stu-id="d63df-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="d63df-115">Операции с массивами, такие как сортировка, присоединение, поиск и заполнение.</span><span class="sxs-lookup"><span data-stu-id="d63df-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="d63df-116">Вот некоторые действия, которые невозможно выполнить в Stream Analytics с помощью определяемой пользователем функции JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d63df-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="d63df-117">Вызов внешних конечных точек REST, например выполнение обратного разрешения IP-адресов или извлечение ссылочных данных из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="d63df-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="d63df-118">Сериализация или десериализация входных и выходных данных в пользовательский формат сообщения.</span><span class="sxs-lookup"><span data-stu-id="d63df-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="d63df-119">Создание пользовательских статистических функций.</span><span class="sxs-lookup"><span data-stu-id="d63df-119">Create custom aggregates</span></span>

<span data-ttu-id="d63df-120">Следует избегать использования таких функций, как **Date.GetDate()** или **Math.random()**, хотя они не запрещены в определении функции.</span><span class="sxs-lookup"><span data-stu-id="d63df-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in the functions definition, you should avoid using them.</span></span> <span data-ttu-id="d63df-121">Эти функции возвращают **разные** результаты при каждом вызове, а служба Azure Stream Analytics не ведет журнал вызовов и возвращаемых результатов для функций.</span><span class="sxs-lookup"><span data-stu-id="d63df-121">These functions **do not** return the same result every time you call them, and the Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="d63df-122">Если функция возвращает разные результаты для одних и тех же событий, невозможно гарантировать повторяемость при перезапуске задания пользователем или службой Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d63df-122">If a function returns different result on the same events, repeatability is not guaranteed when a job is restarted by you or by the Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-the-azure-portal"></a><span data-ttu-id="d63df-123">Добавление определяемой пользователем функции JavaScript на портале Azure</span><span class="sxs-lookup"><span data-stu-id="d63df-123">Add a JavaScript user-defined function in the Azure portal</span></span>
<span data-ttu-id="d63df-124">Чтобы создать простую определяемую пользователем функцию JavaScript в существующем задании Stream Analytics, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d63df-124">To create a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="d63df-125">Найдите нужное задание Stream Analytics на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d63df-125">In the Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="d63df-126">В разделе **топология задания** выберите нужную функцию.</span><span class="sxs-lookup"><span data-stu-id="d63df-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="d63df-127">Откроется пустой список функций.</span><span class="sxs-lookup"><span data-stu-id="d63df-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="d63df-128">Чтобы создать определяемую пользователем функцию, выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d63df-128">To create a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="d63df-129">В колонке **Новая функция** для параметра **Тип функции** выберите значение **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="d63df-129">On the **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="d63df-130">В редакторе отобразится стандартный шаблон функции.</span><span class="sxs-lookup"><span data-stu-id="d63df-130">A default function template appears in the editor.</span></span>
5.  <span data-ttu-id="d63df-131">В качестве значения для параметра **UDF alias**, введите **hex2Int**, затем измените реализацию функции, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d63df-131">For the **UDF alias**, enter **hex2Int**, and change the function implementation as follows:</span></span>

    ```
    // Convert Hex value to integer.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="d63df-132">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d63df-132">Select **Save**.</span></span> <span data-ttu-id="d63df-133">Функция отобразится в списке функций.</span><span class="sxs-lookup"><span data-stu-id="d63df-133">Your function appears in the list of functions.</span></span>
7.  <span data-ttu-id="d63df-134">Выберите новую функцию **hex2Int** и проверьте определение функции.</span><span class="sxs-lookup"><span data-stu-id="d63df-134">Select the new **hex2Int** function, and check the function definition.</span></span> <span data-ttu-id="d63df-135">Для всех пользовательских функций к псевдониму добавляется префикс **UDF**.</span><span class="sxs-lookup"><span data-stu-id="d63df-135">All functions have a **UDF** prefix added to the function alias.</span></span> <span data-ttu-id="d63df-136">Этот *префикс нужно использовать* при вызове функции из запроса Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d63df-136">You need to *include the prefix* when you call the function in your Stream Analytics query.</span></span> <span data-ttu-id="d63df-137">В нашем примере нужно вызывать функцию **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="d63df-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="d63df-138">Вызов определяемой пользователем функции из запроса</span><span class="sxs-lookup"><span data-stu-id="d63df-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="d63df-139">В редакторе запросов для параметра **Топология задания** выберите значение **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="d63df-139">In the query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="d63df-140">Откройте режим редактирования запроса и добавьте вызов определяемой пользователем функции, как показано здесь:</span><span class="sxs-lookup"><span data-stu-id="d63df-140">Edit your query, and then call the user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="d63df-141">Чтобы передать пример файла данных, щелкните правой кнопкой мыши входные данные задания.</span><span class="sxs-lookup"><span data-stu-id="d63df-141">To upload the sample data file, right-click the job input.</span></span>
4.  <span data-ttu-id="d63df-142">Чтобы проверить запрос, выберите **Тестирование**.</span><span class="sxs-lookup"><span data-stu-id="d63df-142">To test your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="d63df-143">Поддерживаемые объекты JavaScript</span><span class="sxs-lookup"><span data-stu-id="d63df-143">Supported JavaScript objects</span></span>
<span data-ttu-id="d63df-144">Определяемые пользователем функции JavaScript в Azure Stream Analytics могут использовать все стандартные встроенные объекты JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d63df-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="d63df-145">Список этих объектов вы найдете [здесь](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="d63df-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="d63df-146">Преобразование типов Stream Analytics и JavaScript</span><span class="sxs-lookup"><span data-stu-id="d63df-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="d63df-147">Существуют различия между типами, которые поддерживаются в языке запросов Stream Analytics и в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d63df-147">There are differences in the types that the Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="d63df-148">В следующей таблице перечислены сопоставления преобразования между этими типами.</span><span class="sxs-lookup"><span data-stu-id="d63df-148">This table lists the conversion mappings between the two:</span></span>

<span data-ttu-id="d63df-149">Анализ потока</span><span class="sxs-lookup"><span data-stu-id="d63df-149">Stream Analytics</span></span> | <span data-ttu-id="d63df-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d63df-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="d63df-151">bigint</span><span class="sxs-lookup"><span data-stu-id="d63df-151">bigint</span></span> | <span data-ttu-id="d63df-152">Число (JavaScript может представлять целые числа только до значения 2^53).</span><span class="sxs-lookup"><span data-stu-id="d63df-152">Number (JavaScript can only represent integers up to precisely 2^53)</span></span>
<span data-ttu-id="d63df-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="d63df-153">DateTime</span></span> | <span data-ttu-id="d63df-154">Дата (JavaScript поддерживает только миллисекунды)</span><span class="sxs-lookup"><span data-stu-id="d63df-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="d63df-155">double</span><span class="sxs-lookup"><span data-stu-id="d63df-155">double</span></span> | <span data-ttu-id="d63df-156">Number</span><span class="sxs-lookup"><span data-stu-id="d63df-156">Number</span></span>
<span data-ttu-id="d63df-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="d63df-157">nvarchar(MAX)</span></span> | <span data-ttu-id="d63df-158">Строка</span><span class="sxs-lookup"><span data-stu-id="d63df-158">String</span></span>
<span data-ttu-id="d63df-159">Record</span><span class="sxs-lookup"><span data-stu-id="d63df-159">Record</span></span> | <span data-ttu-id="d63df-160">Объект</span><span class="sxs-lookup"><span data-stu-id="d63df-160">Object</span></span>
<span data-ttu-id="d63df-161">Массив,</span><span class="sxs-lookup"><span data-stu-id="d63df-161">Array</span></span> | <span data-ttu-id="d63df-162">Массив,</span><span class="sxs-lookup"><span data-stu-id="d63df-162">Array</span></span>
<span data-ttu-id="d63df-163">NULL</span><span class="sxs-lookup"><span data-stu-id="d63df-163">NULL</span></span> | <span data-ttu-id="d63df-164">Null</span><span class="sxs-lookup"><span data-stu-id="d63df-164">Null</span></span>


<span data-ttu-id="d63df-165">Ниже описаны преобразования из типов JavaScript в типы Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d63df-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="d63df-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d63df-166">JavaScript</span></span> | <span data-ttu-id="d63df-167">Анализ потока</span><span class="sxs-lookup"><span data-stu-id="d63df-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="d63df-168">Number</span><span class="sxs-lookup"><span data-stu-id="d63df-168">Number</span></span> | <span data-ttu-id="d63df-169">Значение типа bigint, если это целое число в диапазоне от long.MinValue до long.MaxValue. Иначе используется тип double.</span><span class="sxs-lookup"><span data-stu-id="d63df-169">Bigint (if the number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="d63df-170">Дата</span><span class="sxs-lookup"><span data-stu-id="d63df-170">Date</span></span> | <span data-ttu-id="d63df-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="d63df-171">DateTime</span></span>
<span data-ttu-id="d63df-172">Строка</span><span class="sxs-lookup"><span data-stu-id="d63df-172">String</span></span> | <span data-ttu-id="d63df-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="d63df-173">nvarchar(MAX)</span></span>
<span data-ttu-id="d63df-174">Объект</span><span class="sxs-lookup"><span data-stu-id="d63df-174">Object</span></span> | <span data-ttu-id="d63df-175">Record</span><span class="sxs-lookup"><span data-stu-id="d63df-175">Record</span></span>
<span data-ttu-id="d63df-176">Массив,</span><span class="sxs-lookup"><span data-stu-id="d63df-176">Array</span></span> | <span data-ttu-id="d63df-177">Массив,</span><span class="sxs-lookup"><span data-stu-id="d63df-177">Array</span></span>
<span data-ttu-id="d63df-178">NULL, не определено</span><span class="sxs-lookup"><span data-stu-id="d63df-178">Null, Undefined</span></span> | <span data-ttu-id="d63df-179">NULL</span><span class="sxs-lookup"><span data-stu-id="d63df-179">NULL</span></span>
<span data-ttu-id="d63df-180">Любой другой тип (например, функция или ошибка)</span><span class="sxs-lookup"><span data-stu-id="d63df-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="d63df-181">Не поддерживается (возникает ошибка времени выполнения)</span><span class="sxs-lookup"><span data-stu-id="d63df-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d63df-182">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="d63df-182">Troubleshooting</span></span>
<span data-ttu-id="d63df-183">Ошибки времени выполнения JavaScript считаются неустранимыми и регистрируются в журнале действий.</span><span class="sxs-lookup"><span data-stu-id="d63df-183">JavaScript runtime errors are considered fatal, and are surfaced through the Activity log.</span></span> <span data-ttu-id="d63df-184">Чтобы получить этот журнал, перейдите на портале Azure к нужному заданию и щелкните **Журнал действий**.</span><span class="sxs-lookup"><span data-stu-id="d63df-184">To retrieve the log, in the Azure portal, go to your job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="d63df-185">Другие методы использования определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="d63df-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-to-output"></a><span data-ttu-id="d63df-186">Вывод вложенных значений JSON</span><span class="sxs-lookup"><span data-stu-id="d63df-186">Write nested JSON to output</span></span>
<span data-ttu-id="d63df-187">Если вы используете этап обработки результатов, на котором входными данными являются выходные данные в формате JSON задания Stream Analytics, вам нужно записать строку JSON в выходные данные.</span><span class="sxs-lookup"><span data-stu-id="d63df-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string to output.</span></span> <span data-ttu-id="d63df-188">Приведенный ниже пример вызывает функцию **JSON.stringify()**, которая упаковывает все полученные пары "имя — значение" и передает их единой строкой в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="d63df-188">The next example calls the **JSON.stringify()** function to pack all name/value pairs of the input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="d63df-189">**Определение определяемой пользователем функции JavaScript:**</span><span class="sxs-lookup"><span data-stu-id="d63df-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="d63df-190">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="d63df-190">**Sample query:**</span></span>
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

## <a name="get-help"></a><span data-ttu-id="d63df-191">Получение справки</span><span class="sxs-lookup"><span data-stu-id="d63df-191">Get help</span></span>
<span data-ttu-id="d63df-192">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="d63df-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d63df-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d63df-193">Next steps</span></span>
* [<span data-ttu-id="d63df-194">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d63df-194">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d63df-195">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d63df-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d63df-196">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d63df-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="d63df-197">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Azure Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="d63df-197">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)</span></span>
* <span data-ttu-id="d63df-198">[Azure Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx) (Справочник по API-интерфейсу REST для управления Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="d63df-198">[Azure Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)</span></span>
