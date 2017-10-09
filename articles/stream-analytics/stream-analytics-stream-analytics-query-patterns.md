---
title: "Примеры aaaQuery для распространенных шаблонов использования в Stream Analytics | Документы Microsoft"
description: "Общие шаблоны запросов Azure Stream Analytics"
keywords: "примеры запросов"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="f4c51-104">Примеры запросов для распространенных шаблонов использования Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4c51-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="f4c51-105">Введение</span><span class="sxs-lookup"><span data-stu-id="f4c51-105">Introduction</span></span>
<span data-ttu-id="f4c51-106">Запросы в Azure Stream Analytics выражаются на языке запросов на основе SQL.</span><span class="sxs-lookup"><span data-stu-id="f4c51-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="f4c51-107">Эти запросы, описаны в hello [Справочник по языку запросов Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) руководства.</span><span class="sxs-lookup"><span data-stu-id="f4c51-107">These queries are documented in hello [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="f4c51-108">Это статье структуры решения tooseveral распространенными шаблонами запросов, на основе реальных сценариев.</span><span class="sxs-lookup"><span data-stu-id="f4c51-108">This article outlines solutions tooseveral common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="f4c51-109">Он является незавершенным и по-прежнему toobe обновляется новых шаблонов на постоянной основе.</span><span class="sxs-lookup"><span data-stu-id="f4c51-109">It is a work in progress and continues toobe updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="f4c51-110">Пример запроса: преобразование типов данных</span><span class="sxs-lookup"><span data-stu-id="f4c51-110">Query example: Convert data types</span></span>
<span data-ttu-id="f4c51-111">**Описание**: определение типов hello свойств на hello входного потока.</span><span class="sxs-lookup"><span data-stu-id="f4c51-111">**Description**: Define hello types of properties on hello input stream.</span></span>
<span data-ttu-id="f4c51-112">Например, веса автомобиля hello поступает на hello входного потока, как строки и должен преобразовать слишком toobe**INT** tooperform **сумма** его.</span><span class="sxs-lookup"><span data-stu-id="f4c51-112">For example, hello car weight is coming on hello input stream as strings and needs toobe converted too**INT** tooperform **SUM** it up.</span></span>

<span data-ttu-id="f4c51-113">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-113">**Input**:</span></span>

| <span data-ttu-id="f4c51-114">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-114">Make</span></span> | <span data-ttu-id="f4c51-115">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-115">Time</span></span> | <span data-ttu-id="f4c51-116">Вес</span><span class="sxs-lookup"><span data-stu-id="f4c51-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-117">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-117">Honda</span></span> |<span data-ttu-id="f4c51-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="f4c51-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="f4c51-119">"1000"</span></span> |
| <span data-ttu-id="f4c51-120">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-120">Honda</span></span> |<span data-ttu-id="f4c51-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="f4c51-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="f4c51-122">"2000"</span></span> |

<span data-ttu-id="f4c51-123">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-123">**Output**:</span></span>

| <span data-ttu-id="f4c51-124">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-124">Make</span></span> | <span data-ttu-id="f4c51-125">Вес</span><span class="sxs-lookup"><span data-stu-id="f4c51-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="f4c51-126">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-126">Honda</span></span> |<span data-ttu-id="f4c51-127">3000</span><span class="sxs-lookup"><span data-stu-id="f4c51-127">3000</span></span> |

<span data-ttu-id="f4c51-128">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="f4c51-129">**Объяснение**: использование **ПРИВЕДЕНИЯ** инструкции в hello **вес** его тип данных поля toospecify.</span><span class="sxs-lookup"><span data-stu-id="f4c51-129">**Explanation**: Use a **CAST** statement in hello **Weight** field toospecify its data type.</span></span> <span data-ttu-id="f4c51-130">Просмотреть список поддерживаемых типов данных в hello [типы данных (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4c51-130">See hello list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a><span data-ttu-id="f4c51-131">Пример запроса: используйте Like или Not как toodo соответствие шаблону</span><span class="sxs-lookup"><span data-stu-id="f4c51-131">Query example: Use Like/Not like toodo pattern matching</span></span>
<span data-ttu-id="f4c51-132">**Описание**: Проверьте, что значение поля для hello событие соответствует определенному шаблону.</span><span class="sxs-lookup"><span data-stu-id="f4c51-132">**Description**: Check that a field value on hello event matches a certain pattern.</span></span>
<span data-ttu-id="f4c51-133">Например проверьте, результат hello возвращает форм лицензии, которые начинаются с и заканчиваться 9.</span><span class="sxs-lookup"><span data-stu-id="f4c51-133">For example, check that hello result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="f4c51-134">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-134">**Input**:</span></span>

| <span data-ttu-id="f4c51-135">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-135">Make</span></span> | <span data-ttu-id="f4c51-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f4c51-136">LicensePlate</span></span> | <span data-ttu-id="f4c51-137">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-138">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-138">Honda</span></span> |<span data-ttu-id="f4c51-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="f4c51-139">ABC-123</span></span> |<span data-ttu-id="f4c51-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-141">Toyota</span></span> |<span data-ttu-id="f4c51-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="f4c51-142">AAA-999</span></span> |<span data-ttu-id="f4c51-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="f4c51-144">Nissan</span></span> |<span data-ttu-id="f4c51-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="f4c51-145">ABC-369</span></span> |<span data-ttu-id="f4c51-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f4c51-147">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-147">**Output**:</span></span>

| <span data-ttu-id="f4c51-148">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-148">Make</span></span> | <span data-ttu-id="f4c51-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f4c51-149">LicensePlate</span></span> | <span data-ttu-id="f4c51-150">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-151">Toyota</span></span> |<span data-ttu-id="f4c51-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="f4c51-152">AAA-999</span></span> |<span data-ttu-id="f4c51-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="f4c51-154">Nissan</span></span> |<span data-ttu-id="f4c51-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="f4c51-155">ABC-369</span></span> |<span data-ttu-id="f4c51-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f4c51-157">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="f4c51-158">**Объяснение**: hello используйте **как** hello инструкции toocheck **LicensePlate** значение поля.</span><span class="sxs-lookup"><span data-stu-id="f4c51-158">**Explanation**: Use hello **LIKE** statement toocheck hello **LicensePlate** field value.</span></span> <span data-ttu-id="f4c51-159">Оно должно начинаться с А, затем должна идти любая строка из нуля или более символов и, наконец, цифра 9.</span><span class="sxs-lookup"><span data-stu-id="f4c51-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="f4c51-160">Пример запроса: укажите логику для различных случаев и значений (операторы CASE)</span><span class="sxs-lookup"><span data-stu-id="f4c51-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="f4c51-161">**Описание.** Укажите разные вычисления для поля на основе определенных условий.</span><span class="sxs-lookup"><span data-stu-id="f4c51-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="f4c51-162">Например введите описание строки сколько автомобили hello одинаковы, переданный особый случай 1.</span><span class="sxs-lookup"><span data-stu-id="f4c51-162">For example, provide a string description for how many cars of hello same make passed, with a special case for 1.</span></span>

<span data-ttu-id="f4c51-163">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-163">**Input**:</span></span>

| <span data-ttu-id="f4c51-164">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-164">Make</span></span> | <span data-ttu-id="f4c51-165">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f4c51-166">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-166">Honda</span></span> |<span data-ttu-id="f4c51-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-168">Toyota</span></span> |<span data-ttu-id="f4c51-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-170">Toyota</span></span> |<span data-ttu-id="f4c51-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f4c51-172">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-172">**Output**:</span></span>

| <span data-ttu-id="f4c51-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="f4c51-173">CarsPassed</span></span> | <span data-ttu-id="f4c51-174">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-175">1 Honda</span></span> |<span data-ttu-id="f4c51-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="f4c51-177">2 Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-177">2 Toyotas</span></span> |<span data-ttu-id="f4c51-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="f4c51-179">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-179">**Solution**:</span></span>

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="f4c51-180">**Объяснение**: hello **случай** предложение позволяет нам tooprovide различных вычислений на основе определенных критериев (в нашем случае hello число автомобилей hello в окне статистические hello).</span><span class="sxs-lookup"><span data-stu-id="f4c51-180">**Explanation**: hello **CASE** clause allows us tooprovide a different computation, based on some criteria (in our case, hello count of hello cars in hello aggregate window).</span></span>

## <a name="query-example-send-data-toomultiple-outputs"></a><span data-ttu-id="f4c51-181">Пример запроса: Отправка выводит toomultiple данных</span><span class="sxs-lookup"><span data-stu-id="f4c51-181">Query example: Send data toomultiple outputs</span></span>
<span data-ttu-id="f4c51-182">**Описание**: toomultiple отправки данных выходные данные целевых объектов из одного задания.</span><span class="sxs-lookup"><span data-stu-id="f4c51-182">**Description**: Send data toomultiple output targets from a single job.</span></span>
<span data-ttu-id="f4c51-183">Например анализа данных для предупреждения на основе пороговых значений и архивное хранилище tooblob все события.</span><span class="sxs-lookup"><span data-stu-id="f4c51-183">For example, analyze data for a threshold-based alert and archive all events tooblob storage.</span></span>

<span data-ttu-id="f4c51-184">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-184">**Input**:</span></span>

| <span data-ttu-id="f4c51-185">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-185">Make</span></span> | <span data-ttu-id="f4c51-186">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f4c51-187">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-187">Honda</span></span> |<span data-ttu-id="f4c51-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-189">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-189">Honda</span></span> |<span data-ttu-id="f4c51-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-191">Toyota</span></span> |<span data-ttu-id="f4c51-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-193">Toyota</span></span> |<span data-ttu-id="f4c51-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-195">Toyota</span></span> |<span data-ttu-id="f4c51-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f4c51-197">**Выходные данные 1**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-197">**Output1**:</span></span>

| <span data-ttu-id="f4c51-198">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-198">Make</span></span> | <span data-ttu-id="f4c51-199">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f4c51-200">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-200">Honda</span></span> |<span data-ttu-id="f4c51-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-202">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-202">Honda</span></span> |<span data-ttu-id="f4c51-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-204">Toyota</span></span> |<span data-ttu-id="f4c51-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-206">Toyota</span></span> |<span data-ttu-id="f4c51-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-208">Toyota</span></span> |<span data-ttu-id="f4c51-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f4c51-210">**Выходные данные 2**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-210">**Output2**:</span></span>

| <span data-ttu-id="f4c51-211">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-211">Make</span></span> | <span data-ttu-id="f4c51-212">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-212">Time</span></span> | <span data-ttu-id="f4c51-213">Count</span><span class="sxs-lookup"><span data-stu-id="f4c51-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-214">Toyota</span></span> |<span data-ttu-id="f4c51-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="f4c51-216">3</span><span class="sxs-lookup"><span data-stu-id="f4c51-216">3</span></span> |

<span data-ttu-id="f4c51-217">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-217">**Solution**:</span></span>

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

<span data-ttu-id="f4c51-218">**Объяснение**: hello **INTO** предложение сообщает Stream Analytics, который hello выводит данные toofrom toowrite hello этой инструкции.</span><span class="sxs-lookup"><span data-stu-id="f4c51-218">**Explanation**: hello **INTO** clause tells Stream Analytics which of hello outputs toowrite hello data toofrom this statement.</span></span>
<span data-ttu-id="f4c51-219">первый запрос Hello является сквозной данных hello, мы получили tooan выхода, который мы назвали **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="f4c51-219">hello first query is a pass-through of hello data we received tooan output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="f4c51-220">второй запрос Hello простой статистическую обработку и фильтрации и выполняет его отправляет результаты hello tooa подчиненных системой предупреждений.</span><span class="sxs-lookup"><span data-stu-id="f4c51-220">hello second query does some simple aggregation and filtering, and it sends hello results tooa downstream alerting system.</span></span>

<span data-ttu-id="f4c51-221">Обратите внимание, что можно также повторно использовать результаты hello hello обобщенные табличные выражения (CTE) (такие как **WITH** операторов) в нескольких операторах выходных данных.</span><span class="sxs-lookup"><span data-stu-id="f4c51-221">Note that you can also reuse hello results of hello common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="f4c51-222">Этот параметр имеет hello дополнительное преимущество открытия входного источника toohello меньшее число модулей чтения.</span><span class="sxs-lookup"><span data-stu-id="f4c51-222">This option has hello added benefit of opening fewer readers toohello input source.</span></span>
<span data-ttu-id="f4c51-223">Например:</span><span class="sxs-lookup"><span data-stu-id="f4c51-223">For example:</span></span> 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a><span data-ttu-id="f4c51-224">Пример запроса: подсчет уникальных значений</span><span class="sxs-lookup"><span data-stu-id="f4c51-224">Query example: Count unique values</span></span>
<span data-ttu-id="f4c51-225">**Описание**: количество hello уникальное поле значений, отображаемых в потоке hello в за период времени.</span><span class="sxs-lookup"><span data-stu-id="f4c51-225">**Description**: Count hello number of unique field values that appear in hello stream within a time window.</span></span>
<span data-ttu-id="f4c51-226">Например сколько уникальных делает автомобилей, передаются через кабинку hello в окне второй 2?</span><span class="sxs-lookup"><span data-stu-id="f4c51-226">For example, how many unique makes of cars passed through hello toll booth in a 2-second window?</span></span>

<span data-ttu-id="f4c51-227">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-227">**Input**:</span></span>

| <span data-ttu-id="f4c51-228">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-228">Make</span></span> | <span data-ttu-id="f4c51-229">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f4c51-230">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-230">Honda</span></span> |<span data-ttu-id="f4c51-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-232">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-232">Honda</span></span> |<span data-ttu-id="f4c51-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-234">Toyota</span></span> |<span data-ttu-id="f4c51-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-236">Toyota</span></span> |<span data-ttu-id="f4c51-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-238">Toyota</span></span> |<span data-ttu-id="f4c51-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="f4c51-240">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="f4c51-240">**Output:**</span></span>

| <span data-ttu-id="f4c51-241">Count</span><span class="sxs-lookup"><span data-stu-id="f4c51-241">Count</span></span> | <span data-ttu-id="f4c51-242">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f4c51-243">2</span><span class="sxs-lookup"><span data-stu-id="f4c51-243">2</span></span> |<span data-ttu-id="f4c51-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="f4c51-245">1</span><span class="sxs-lookup"><span data-stu-id="f4c51-245">1</span></span> |<span data-ttu-id="f4c51-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="f4c51-247">**Решение.**</span><span class="sxs-lookup"><span data-stu-id="f4c51-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="f4c51-248">**Описание:**
**COUNT (DISTINCT сделать)** Здравствуйте, возвращает количество уникальных значений в hello **сделать** столбец в пределах периода времени.</span><span class="sxs-lookup"><span data-stu-id="f4c51-248">**Explanation:**
**COUNT(DISTINCT Make)** returns hello number of distinct values in hello **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="f4c51-249">Пример запроса: определение изменения значения</span><span class="sxs-lookup"><span data-stu-id="f4c51-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="f4c51-250">**Описание**: просмотрите предыдущие toodetermine значение, если он отличается от текущего значения hello.</span><span class="sxs-lookup"><span data-stu-id="f4c51-250">**Description**: Look at a previous value toodetermine if it is different than hello current value.</span></span>
<span data-ttu-id="f4c51-251">Например включен hello платный road приветствия же внесите текущего car hello предыдущих car hello?</span><span class="sxs-lookup"><span data-stu-id="f4c51-251">For example, is hello previous car on hello toll road hello same make as hello current car?</span></span>

<span data-ttu-id="f4c51-252">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-252">**Input**:</span></span>

| <span data-ttu-id="f4c51-253">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-253">Make</span></span> | <span data-ttu-id="f4c51-254">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f4c51-255">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-255">Honda</span></span> |<span data-ttu-id="f4c51-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-257">Toyota</span></span> |<span data-ttu-id="f4c51-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="f4c51-259">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-259">**Output**:</span></span>

| <span data-ttu-id="f4c51-260">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-260">Make</span></span> | <span data-ttu-id="f4c51-261">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="f4c51-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-262">Toyota</span></span> |<span data-ttu-id="f4c51-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="f4c51-264">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="f4c51-265">**Объяснение**: использование **ЗАПАЗДЫВАНИЯ** toopeek в hello входной поток обратно в одно событие и получить hello **сделать** значение.</span><span class="sxs-lookup"><span data-stu-id="f4c51-265">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="f4c51-266">Сравните его toohello **сделать** значение для hello текущего события и события hello выходные данные, если они отличаются.</span><span class="sxs-lookup"><span data-stu-id="f4c51-266">Then compare it toohello **Make** value on hello current event and output hello event if they are different.</span></span>

## <a name="query-example-find-hello-first-event-in-a-window"></a><span data-ttu-id="f4c51-267">Пример запроса: hello найти первое событие в окне</span><span class="sxs-lookup"><span data-stu-id="f4c51-267">Query example: Find hello first event in a window</span></span>
<span data-ttu-id="f4c51-268">**Описание**: поиск hello автомобиль в каждые 10 минут.</span><span class="sxs-lookup"><span data-stu-id="f4c51-268">**Description**: Find hello first car in every 10-minute interval.</span></span>

<span data-ttu-id="f4c51-269">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-269">**Input**:</span></span>

| <span data-ttu-id="f4c51-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f4c51-270">LicensePlate</span></span> | <span data-ttu-id="f4c51-271">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-271">Make</span></span> | <span data-ttu-id="f4c51-272">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="f4c51-273">DXE 5291</span></span> |<span data-ttu-id="f4c51-274">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-274">Honda</span></span> |<span data-ttu-id="f4c51-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="f4c51-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="f4c51-276">YZK 5704</span></span> |<span data-ttu-id="f4c51-277">Ford</span><span class="sxs-lookup"><span data-stu-id="f4c51-277">Ford</span></span> |<span data-ttu-id="f4c51-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="f4c51-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="f4c51-279">RMV 8282</span></span> |<span data-ttu-id="f4c51-280">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-280">Honda</span></span> |<span data-ttu-id="f4c51-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="f4c51-282">YHN 6970</span></span> |<span data-ttu-id="f4c51-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-283">Toyota</span></span> |<span data-ttu-id="f4c51-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="f4c51-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="f4c51-285">VFE 1616</span></span> |<span data-ttu-id="f4c51-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-286">Toyota</span></span> |<span data-ttu-id="f4c51-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="f4c51-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="f4c51-288">QYF 9358</span></span> |<span data-ttu-id="f4c51-289">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-289">Honda</span></span> |<span data-ttu-id="f4c51-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="f4c51-291">MDR 6128</span></span> |<span data-ttu-id="f4c51-292">BMW</span><span class="sxs-lookup"><span data-stu-id="f4c51-292">BMW</span></span> |<span data-ttu-id="f4c51-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="f4c51-294">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-294">**Output**:</span></span>

| <span data-ttu-id="f4c51-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f4c51-295">LicensePlate</span></span> | <span data-ttu-id="f4c51-296">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-296">Make</span></span> | <span data-ttu-id="f4c51-297">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="f4c51-298">DXE 5291</span></span> |<span data-ttu-id="f4c51-299">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-299">Honda</span></span> |<span data-ttu-id="f4c51-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="f4c51-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="f4c51-301">QYF 9358</span></span> |<span data-ttu-id="f4c51-302">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-302">Honda</span></span> |<span data-ttu-id="f4c51-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="f4c51-304">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="f4c51-305">Теперь создадим изменение hello проблему и найти hello автомобиль конкретной каждые 10 минут.</span><span class="sxs-lookup"><span data-stu-id="f4c51-305">Now let’s change hello problem and find hello first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="f4c51-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f4c51-306">LicensePlate</span></span> | <span data-ttu-id="f4c51-307">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-307">Make</span></span> | <span data-ttu-id="f4c51-308">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="f4c51-309">DXE 5291</span></span> |<span data-ttu-id="f4c51-310">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-310">Honda</span></span> |<span data-ttu-id="f4c51-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="f4c51-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="f4c51-312">YZK 5704</span></span> |<span data-ttu-id="f4c51-313">Ford</span><span class="sxs-lookup"><span data-stu-id="f4c51-313">Ford</span></span> |<span data-ttu-id="f4c51-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="f4c51-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="f4c51-315">YHN 6970</span></span> |<span data-ttu-id="f4c51-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-316">Toyota</span></span> |<span data-ttu-id="f4c51-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="f4c51-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="f4c51-318">QYF 9358</span></span> |<span data-ttu-id="f4c51-319">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-319">Honda</span></span> |<span data-ttu-id="f4c51-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="f4c51-321">MDR 6128</span></span> |<span data-ttu-id="f4c51-322">BMW</span><span class="sxs-lookup"><span data-stu-id="f4c51-322">BMW</span></span> |<span data-ttu-id="f4c51-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="f4c51-324">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a><span data-ttu-id="f4c51-325">Пример запроса: поиск hello последнего события в окне</span><span class="sxs-lookup"><span data-stu-id="f4c51-325">Query example: Find hello last event in a window</span></span>
<span data-ttu-id="f4c51-326">**Описание**: hello поиска последнего автомобиля в каждые 10 минут.</span><span class="sxs-lookup"><span data-stu-id="f4c51-326">**Description**: Find hello last car in every 10-minute interval.</span></span>

<span data-ttu-id="f4c51-327">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-327">**Input**:</span></span>

| <span data-ttu-id="f4c51-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f4c51-328">LicensePlate</span></span> | <span data-ttu-id="f4c51-329">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-329">Make</span></span> | <span data-ttu-id="f4c51-330">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="f4c51-331">DXE 5291</span></span> |<span data-ttu-id="f4c51-332">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-332">Honda</span></span> |<span data-ttu-id="f4c51-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="f4c51-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="f4c51-334">YZK 5704</span></span> |<span data-ttu-id="f4c51-335">Ford</span><span class="sxs-lookup"><span data-stu-id="f4c51-335">Ford</span></span> |<span data-ttu-id="f4c51-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="f4c51-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="f4c51-337">RMV 8282</span></span> |<span data-ttu-id="f4c51-338">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-338">Honda</span></span> |<span data-ttu-id="f4c51-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="f4c51-340">YHN 6970</span></span> |<span data-ttu-id="f4c51-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-341">Toyota</span></span> |<span data-ttu-id="f4c51-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="f4c51-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="f4c51-343">VFE 1616</span></span> |<span data-ttu-id="f4c51-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-344">Toyota</span></span> |<span data-ttu-id="f4c51-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="f4c51-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="f4c51-346">QYF 9358</span></span> |<span data-ttu-id="f4c51-347">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-347">Honda</span></span> |<span data-ttu-id="f4c51-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="f4c51-349">MDR 6128</span></span> |<span data-ttu-id="f4c51-350">BMW</span><span class="sxs-lookup"><span data-stu-id="f4c51-350">BMW</span></span> |<span data-ttu-id="f4c51-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="f4c51-352">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-352">**Output**:</span></span>

| <span data-ttu-id="f4c51-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f4c51-353">LicensePlate</span></span> | <span data-ttu-id="f4c51-354">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-354">Make</span></span> | <span data-ttu-id="f4c51-355">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="f4c51-356">VFE 1616</span></span> |<span data-ttu-id="f4c51-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-357">Toyota</span></span> |<span data-ttu-id="f4c51-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="f4c51-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="f4c51-359">MDR 6128</span></span> |<span data-ttu-id="f4c51-360">BMW</span><span class="sxs-lookup"><span data-stu-id="f4c51-360">BMW</span></span> |<span data-ttu-id="f4c51-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="f4c51-362">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-362">**Solution**:</span></span>

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

<span data-ttu-id="f4c51-363">**Объяснение**: hello запроса состоит из двух шагов.</span><span class="sxs-lookup"><span data-stu-id="f4c51-363">**Explanation**: There are two steps in hello query.</span></span> <span data-ttu-id="f4c51-364">Hello первый один находит hello последняя отметка времени в windows 10 минут.</span><span class="sxs-lookup"><span data-stu-id="f4c51-364">hello first one finds hello latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="f4c51-365">второй шаг соединения Hello hello результаты первого запроса hello hello исходный поток toofind hello событий, которые соответствуют hello последней отметки времени в каждом окне.</span><span class="sxs-lookup"><span data-stu-id="f4c51-365">hello second step joins hello results of hello first query with hello original stream toofind hello events that match hello last time stamps in each window.</span></span> 

## <a name="query-example-detect-hello-absence-of-events"></a><span data-ttu-id="f4c51-366">Пример запроса: hello отсутствие событий обнаружения</span><span class="sxs-lookup"><span data-stu-id="f4c51-366">Query example: Detect hello absence of events</span></span>
<span data-ttu-id="f4c51-367">**Описание.** Убедитесь, что в потоке отсутствует значение, соответствующее определенным условиям.</span><span class="sxs-lookup"><span data-stu-id="f4c51-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="f4c51-368">Например 2 последовательные cars из приветствия одинаковы введенные road платный hello в hello последние 90 секунд?</span><span class="sxs-lookup"><span data-stu-id="f4c51-368">For example, have 2 consecutive cars from hello same make entered hello toll road within hello last 90 seconds?</span></span>

<span data-ttu-id="f4c51-369">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-369">**Input**:</span></span>

| <span data-ttu-id="f4c51-370">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-370">Make</span></span> | <span data-ttu-id="f4c51-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="f4c51-371">LicensePlate</span></span> | <span data-ttu-id="f4c51-372">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-373">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-373">Honda</span></span> |<span data-ttu-id="f4c51-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="f4c51-374">ABC-123</span></span> |<span data-ttu-id="f4c51-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="f4c51-376">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-376">Honda</span></span> |<span data-ttu-id="f4c51-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="f4c51-377">AAA-999</span></span> |<span data-ttu-id="f4c51-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="f4c51-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-379">Toyota</span></span> |<span data-ttu-id="f4c51-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="f4c51-380">DEF-987</span></span> |<span data-ttu-id="f4c51-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="f4c51-382">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-382">Honda</span></span> |<span data-ttu-id="f4c51-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="f4c51-383">GHI-345</span></span> |<span data-ttu-id="f4c51-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="f4c51-385">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-385">**Output**:</span></span>

| <span data-ttu-id="f4c51-386">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-386">Make</span></span> | <span data-ttu-id="f4c51-387">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-387">Time</span></span> | <span data-ttu-id="f4c51-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="f4c51-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="f4c51-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="f4c51-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="f4c51-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="f4c51-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="f4c51-391">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-391">Honda</span></span> |<span data-ttu-id="f4c51-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="f4c51-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="f4c51-393">AAA-999</span></span> |<span data-ttu-id="f4c51-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="f4c51-394">ABC-123</span></span> |<span data-ttu-id="f4c51-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="f4c51-396">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-396">**Solution**:</span></span>

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

<span data-ttu-id="f4c51-397">**Объяснение**: использование **ЗАПАЗДЫВАНИЯ** toopeek в hello входной поток обратно в одно событие и получить hello **сделать** значение.</span><span class="sxs-lookup"><span data-stu-id="f4c51-397">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="f4c51-398">Сравните его toohello **сделать** значение в hello текущего события, а затем выходное событие hello, если они являются hello таким же.</span><span class="sxs-lookup"><span data-stu-id="f4c51-398">Compare it toohello **MAKE** value in hello current event, and then output hello event if they are hello same.</span></span> <span data-ttu-id="f4c51-399">Можно также использовать **ЗАПАЗДЫВАНИЯ** tooget данных о предыдущих car hello.</span><span class="sxs-lookup"><span data-stu-id="f4c51-399">You can also use **LAG** tooget data about hello previous car.</span></span>

## <a name="query-example-detect-hello-duration-between-events"></a><span data-ttu-id="f4c51-400">Пример запроса: обнаружить hello время между событиями</span><span class="sxs-lookup"><span data-stu-id="f4c51-400">Query example: Detect hello duration between events</span></span>
<span data-ttu-id="f4c51-401">**Описание**: найти hello длительность для данного события.</span><span class="sxs-lookup"><span data-stu-id="f4c51-401">**Description**: Find hello duration of a given event.</span></span> <span data-ttu-id="f4c51-402">Например имея навигации web, определите hello время, затраченное на компонент.</span><span class="sxs-lookup"><span data-stu-id="f4c51-402">For example, given a web clickstream, determine hello time spent on a feature.</span></span>

<span data-ttu-id="f4c51-403">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-403">**Input**:</span></span>  

| <span data-ttu-id="f4c51-404">Пользователь</span><span class="sxs-lookup"><span data-stu-id="f4c51-404">User</span></span> | <span data-ttu-id="f4c51-405">Функция</span><span class="sxs-lookup"><span data-stu-id="f4c51-405">Feature</span></span> | <span data-ttu-id="f4c51-406">Событие</span><span class="sxs-lookup"><span data-stu-id="f4c51-406">Event</span></span> | <span data-ttu-id="f4c51-407">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="f4c51-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="f4c51-408">RightMenu</span></span> |<span data-ttu-id="f4c51-409">Начало</span><span class="sxs-lookup"><span data-stu-id="f4c51-409">Start</span></span> |<span data-ttu-id="f4c51-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="f4c51-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="f4c51-411">RightMenu</span></span> |<span data-ttu-id="f4c51-412">End</span><span class="sxs-lookup"><span data-stu-id="f4c51-412">End</span></span> |<span data-ttu-id="f4c51-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="f4c51-414">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-414">**Output**:</span></span>  

| <span data-ttu-id="f4c51-415">Пользователь</span><span class="sxs-lookup"><span data-stu-id="f4c51-415">User</span></span> | <span data-ttu-id="f4c51-416">Функция</span><span class="sxs-lookup"><span data-stu-id="f4c51-416">Feature</span></span> | <span data-ttu-id="f4c51-417">Длительность</span><span class="sxs-lookup"><span data-stu-id="f4c51-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="f4c51-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="f4c51-418">RightMenu</span></span> |<span data-ttu-id="f4c51-419">7</span><span class="sxs-lookup"><span data-stu-id="f4c51-419">7</span></span> |

<span data-ttu-id="f4c51-420">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="f4c51-421">**Объяснение**: hello используйте **ПОСЛЕДНЕГО** последние функции tooretrieve hello **время** значение в тип событий, hello **запустить**.</span><span class="sxs-lookup"><span data-stu-id="f4c51-421">**Explanation**: Use hello **LAST** function tooretrieve hello last **TIME** value when hello event type was **Start**.</span></span> <span data-ttu-id="f4c51-422">Hello **последний** функция использует **PARTITION BY [пользователь]** tooindicate, hello результат вычисляется на уникальный пользователя.</span><span class="sxs-lookup"><span data-stu-id="f4c51-422">hello **LAST** function uses **PARTITION BY [user]** tooindicate that hello result is computed per unique user.</span></span> <span data-ttu-id="f4c51-423">Hello запрос имеет максимальное пороговое значение 1 час hello разницу во времени между **запустить** и **остановить** события, но можно изменить при необходимости **(ограничение DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="f4c51-423">hello query has a 1-hour maximum threshold for hello time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-hello-duration-of-a-condition"></a><span data-ttu-id="f4c51-424">Пример запроса: определить длительность hello условия</span><span class="sxs-lookup"><span data-stu-id="f4c51-424">Query example: Detect hello duration of a condition</span></span>
<span data-ttu-id="f4c51-425">**Описание.** Определите продолжительность условия.</span><span class="sxs-lookup"><span data-stu-id="f4c51-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="f4c51-426">Предположим, произошла ошибка, которая привела к неправильному отображению массы всех автомобилей (больше 9 тонн).</span><span class="sxs-lookup"><span data-stu-id="f4c51-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="f4c51-427">Мы хотим длительность hello toocompute ошибки hello.</span><span class="sxs-lookup"><span data-stu-id="f4c51-427">We want toocompute hello duration of hello bug.</span></span>

<span data-ttu-id="f4c51-428">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-428">**Input**:</span></span>

| <span data-ttu-id="f4c51-429">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="f4c51-429">Make</span></span> | <span data-ttu-id="f4c51-430">Время</span><span class="sxs-lookup"><span data-stu-id="f4c51-430">Time</span></span> | <span data-ttu-id="f4c51-431">Вес</span><span class="sxs-lookup"><span data-stu-id="f4c51-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-432">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-432">Honda</span></span> |<span data-ttu-id="f4c51-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="f4c51-434">2000</span><span class="sxs-lookup"><span data-stu-id="f4c51-434">2000</span></span> |
| <span data-ttu-id="f4c51-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-435">Toyota</span></span> |<span data-ttu-id="f4c51-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="f4c51-437">25000</span><span class="sxs-lookup"><span data-stu-id="f4c51-437">25000</span></span> |
| <span data-ttu-id="f4c51-438">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-438">Honda</span></span> |<span data-ttu-id="f4c51-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="f4c51-440">26000</span><span class="sxs-lookup"><span data-stu-id="f4c51-440">26000</span></span> |
| <span data-ttu-id="f4c51-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-441">Toyota</span></span> |<span data-ttu-id="f4c51-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="f4c51-443">25000</span><span class="sxs-lookup"><span data-stu-id="f4c51-443">25000</span></span> |
| <span data-ttu-id="f4c51-444">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-444">Honda</span></span> |<span data-ttu-id="f4c51-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="f4c51-446">26000</span><span class="sxs-lookup"><span data-stu-id="f4c51-446">26000</span></span> |
| <span data-ttu-id="f4c51-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-447">Toyota</span></span> |<span data-ttu-id="f4c51-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="f4c51-449">25000</span><span class="sxs-lookup"><span data-stu-id="f4c51-449">25000</span></span> |
| <span data-ttu-id="f4c51-450">Honda</span><span class="sxs-lookup"><span data-stu-id="f4c51-450">Honda</span></span> |<span data-ttu-id="f4c51-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="f4c51-452">26000</span><span class="sxs-lookup"><span data-stu-id="f4c51-452">26000</span></span> |
| <span data-ttu-id="f4c51-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="f4c51-453">Toyota</span></span> |<span data-ttu-id="f4c51-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="f4c51-455">2000</span><span class="sxs-lookup"><span data-stu-id="f4c51-455">2000</span></span> |

<span data-ttu-id="f4c51-456">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-456">**Output**:</span></span>

| <span data-ttu-id="f4c51-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="f4c51-457">StartFault</span></span> | <span data-ttu-id="f4c51-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="f4c51-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="f4c51-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="f4c51-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="f4c51-461">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-461">**Solution**:</span></span>

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

<span data-ttu-id="f4c51-462">**Объяснение**: использование **ЗАПАЗДЫВАНИЯ** tooview hello входного потока на 24 часа и выполните поиск экземпляров where **StartFault** и **StopFault** занимаемых hello Вес < 20000.</span><span class="sxs-lookup"><span data-stu-id="f4c51-462">**Explanation**: Use **LAG** tooview hello input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by hello weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="f4c51-463">Пример запроса: заполнить отсутствующие значения</span><span class="sxs-lookup"><span data-stu-id="f4c51-463">Query example: Fill missing values</span></span>
<span data-ttu-id="f4c51-464">**Описание**: hello поток событий, в которых отсутствуют значения, создают поток событий с регулярными интервалами.</span><span class="sxs-lookup"><span data-stu-id="f4c51-464">**Description**: For hello stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="f4c51-465">Например можно создайте событие каждые 5 секунд, которое сообщает hello недавно обнаружена точка данных.</span><span class="sxs-lookup"><span data-stu-id="f4c51-465">For example, generate an event every 5 seconds that reports hello most recently seen data point.</span></span>

<span data-ttu-id="f4c51-466">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="f4c51-466">**Input**:</span></span>

| <span data-ttu-id="f4c51-467">t</span><span class="sxs-lookup"><span data-stu-id="f4c51-467">t</span></span> | <span data-ttu-id="f4c51-468">value</span><span class="sxs-lookup"><span data-stu-id="f4c51-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="f4c51-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="f4c51-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="f4c51-470">1</span><span class="sxs-lookup"><span data-stu-id="f4c51-470">1</span></span> |
| <span data-ttu-id="f4c51-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="f4c51-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="f4c51-472">2</span><span class="sxs-lookup"><span data-stu-id="f4c51-472">2</span></span> |
| <span data-ttu-id="f4c51-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="f4c51-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="f4c51-474">3</span><span class="sxs-lookup"><span data-stu-id="f4c51-474">3</span></span> |
| <span data-ttu-id="f4c51-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="f4c51-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="f4c51-476">4</span><span class="sxs-lookup"><span data-stu-id="f4c51-476">4</span></span> |
| <span data-ttu-id="f4c51-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="f4c51-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="f4c51-478">5</span><span class="sxs-lookup"><span data-stu-id="f4c51-478">5</span></span> |
| <span data-ttu-id="f4c51-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="f4c51-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="f4c51-480">6</span><span class="sxs-lookup"><span data-stu-id="f4c51-480">6</span></span> |

<span data-ttu-id="f4c51-481">**Выходные данные (первые 10 строк)**:</span><span class="sxs-lookup"><span data-stu-id="f4c51-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="f4c51-482">windowend</span><span class="sxs-lookup"><span data-stu-id="f4c51-482">windowend</span></span> | <span data-ttu-id="f4c51-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="f4c51-483">lastevent.t</span></span> | <span data-ttu-id="f4c51-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="f4c51-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4c51-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="f4c51-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="f4c51-487">1</span><span class="sxs-lookup"><span data-stu-id="f4c51-487">1</span></span> |
| <span data-ttu-id="f4c51-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="f4c51-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="f4c51-490">2</span><span class="sxs-lookup"><span data-stu-id="f4c51-490">2</span></span> |
| <span data-ttu-id="f4c51-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="f4c51-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="f4c51-493">3</span><span class="sxs-lookup"><span data-stu-id="f4c51-493">3</span></span> |
| <span data-ttu-id="f4c51-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="f4c51-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="f4c51-496">4</span><span class="sxs-lookup"><span data-stu-id="f4c51-496">4</span></span> |
| <span data-ttu-id="f4c51-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="f4c51-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="f4c51-499">4</span><span class="sxs-lookup"><span data-stu-id="f4c51-499">4</span></span> |
| <span data-ttu-id="f4c51-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="f4c51-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="f4c51-502">4</span><span class="sxs-lookup"><span data-stu-id="f4c51-502">4</span></span> |
| <span data-ttu-id="f4c51-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="f4c51-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="f4c51-505">5</span><span class="sxs-lookup"><span data-stu-id="f4c51-505">5</span></span> |
| <span data-ttu-id="f4c51-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="f4c51-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="f4c51-508">6</span><span class="sxs-lookup"><span data-stu-id="f4c51-508">6</span></span> |
| <span data-ttu-id="f4c51-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="f4c51-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="f4c51-511">6</span><span class="sxs-lookup"><span data-stu-id="f4c51-511">6</span></span> |
| <span data-ttu-id="f4c51-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="f4c51-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="f4c51-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="f4c51-514">6</span><span class="sxs-lookup"><span data-stu-id="f4c51-514">6</span></span> |

<span data-ttu-id="f4c51-515">**Решение**</span><span class="sxs-lookup"><span data-stu-id="f4c51-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="f4c51-516">**Объяснение**: этот запрос приводит к возникновению события каждые 5 секунд и выходы hello последнего события, который ранее был получен.</span><span class="sxs-lookup"><span data-stu-id="f4c51-516">**Explanation**: This query generates events every 5 seconds and outputs hello last event that was received previously.</span></span> <span data-ttu-id="f4c51-517">Hello [окна «прыгающие» окна](https://msdn.microsoft.com/library/dn835041.aspx "окна «прыгающие» окна — Azure Stream Analytics") длительность определяет, насколько далеко назад hello запрос выглядит toofind hello последнее событие (300 секунд, в этом примере).</span><span class="sxs-lookup"><span data-stu-id="f4c51-517">hello [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back hello query looks toofind hello latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="f4c51-518">Получение справки</span><span class="sxs-lookup"><span data-stu-id="f4c51-518">Get help</span></span>
<span data-ttu-id="f4c51-519">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f4c51-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4c51-520">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4c51-520">Next steps</span></span>
* [<span data-ttu-id="f4c51-521">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4c51-521">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f4c51-522">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4c51-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f4c51-523">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4c51-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f4c51-524">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4c51-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f4c51-525">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4c51-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

