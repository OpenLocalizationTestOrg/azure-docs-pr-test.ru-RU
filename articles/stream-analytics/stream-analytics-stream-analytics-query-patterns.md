---
title: "Примеры запросов для распространенных шаблонов использования Stream Analytics | Документация Майкрософт"
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
ms.openlocfilehash: a00855c200b3fb365073bad4c5773b02c4c2c7fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="3e91b-104">Примеры запросов для распространенных шаблонов использования Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3e91b-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="3e91b-105">Введение</span><span class="sxs-lookup"><span data-stu-id="3e91b-105">Introduction</span></span>
<span data-ttu-id="3e91b-106">Запросы в Azure Stream Analytics выражаются на языке запросов на основе SQL.</span><span class="sxs-lookup"><span data-stu-id="3e91b-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="3e91b-107">Эти запросы описаны в руководстве [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="3e91b-107">These queries are documented in the [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="3e91b-108">В этой статье описаны решения для нескольких стандартных шаблонов запросов на основе реальных сценариев.</span><span class="sxs-lookup"><span data-stu-id="3e91b-108">This article outlines solutions to several common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="3e91b-109">Документ не завершен и будет дополняться новыми шаблонами на постоянной основе.</span><span class="sxs-lookup"><span data-stu-id="3e91b-109">It is a work in progress and continues to be updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="3e91b-110">Пример запроса: преобразование типов данных</span><span class="sxs-lookup"><span data-stu-id="3e91b-110">Query example: Convert data types</span></span>
<span data-ttu-id="3e91b-111">**Описание.** Определите типы свойств для входного потока.</span><span class="sxs-lookup"><span data-stu-id="3e91b-111">**Description**: Define the types of properties on the input stream.</span></span>
<span data-ttu-id="3e91b-112">Например, вес автомобиля поступает по входному потоку как строка и должен быть преобразован в тип **INT** для выполнения операции **SUM**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-112">For example, the car weight is coming on the input stream as strings and needs to be converted to **INT** to perform **SUM** it up.</span></span>

<span data-ttu-id="3e91b-113">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-113">**Input**:</span></span>

| <span data-ttu-id="3e91b-114">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-114">Make</span></span> | <span data-ttu-id="3e91b-115">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-115">Time</span></span> | <span data-ttu-id="3e91b-116">Вес</span><span class="sxs-lookup"><span data-stu-id="3e91b-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-117">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-117">Honda</span></span> |<span data-ttu-id="3e91b-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="3e91b-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="3e91b-119">"1000"</span></span> |
| <span data-ttu-id="3e91b-120">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-120">Honda</span></span> |<span data-ttu-id="3e91b-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="3e91b-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="3e91b-122">"2000"</span></span> |

<span data-ttu-id="3e91b-123">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-123">**Output**:</span></span>

| <span data-ttu-id="3e91b-124">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-124">Make</span></span> | <span data-ttu-id="3e91b-125">Вес</span><span class="sxs-lookup"><span data-stu-id="3e91b-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="3e91b-126">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-126">Honda</span></span> |<span data-ttu-id="3e91b-127">3000</span><span class="sxs-lookup"><span data-stu-id="3e91b-127">3000</span></span> |

<span data-ttu-id="3e91b-128">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="3e91b-129">**Объяснение.** Используйте инструкцию **CAST** в поле **Weight** для указания типа данных.</span><span class="sxs-lookup"><span data-stu-id="3e91b-129">**Explanation**: Use a **CAST** statement in the **Weight** field to specify its data type.</span></span> <span data-ttu-id="3e91b-130">Список поддерживаемых типов данных Azure Stream Analytics см. в [этой статье](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e91b-130">See the list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-to-do-pattern-matching"></a><span data-ttu-id="3e91b-131">Пример запроса: использование функции Like/Not like для сопоставления шаблонов</span><span class="sxs-lookup"><span data-stu-id="3e91b-131">Query example: Use Like/Not like to do pattern matching</span></span>
<span data-ttu-id="3e91b-132">**Описание.** Проверьте, соответствует ли значение поля в событии определенному шаблону.</span><span class="sxs-lookup"><span data-stu-id="3e91b-132">**Description**: Check that a field value on the event matches a certain pattern.</span></span>
<span data-ttu-id="3e91b-133">Например, проверьте, возвращает ли результат номерные знаки, которые начинаются с A и заканчиваться на 9.</span><span class="sxs-lookup"><span data-stu-id="3e91b-133">For example, check that the result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="3e91b-134">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-134">**Input**:</span></span>

| <span data-ttu-id="3e91b-135">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-135">Make</span></span> | <span data-ttu-id="3e91b-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3e91b-136">LicensePlate</span></span> | <span data-ttu-id="3e91b-137">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-138">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-138">Honda</span></span> |<span data-ttu-id="3e91b-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="3e91b-139">ABC-123</span></span> |<span data-ttu-id="3e91b-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-141">Toyota</span></span> |<span data-ttu-id="3e91b-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="3e91b-142">AAA-999</span></span> |<span data-ttu-id="3e91b-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="3e91b-144">Nissan</span></span> |<span data-ttu-id="3e91b-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="3e91b-145">ABC-369</span></span> |<span data-ttu-id="3e91b-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3e91b-147">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-147">**Output**:</span></span>

| <span data-ttu-id="3e91b-148">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-148">Make</span></span> | <span data-ttu-id="3e91b-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3e91b-149">LicensePlate</span></span> | <span data-ttu-id="3e91b-150">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-151">Toyota</span></span> |<span data-ttu-id="3e91b-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="3e91b-152">AAA-999</span></span> |<span data-ttu-id="3e91b-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="3e91b-154">Nissan</span></span> |<span data-ttu-id="3e91b-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="3e91b-155">ABC-369</span></span> |<span data-ttu-id="3e91b-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3e91b-157">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="3e91b-158">**Объяснение.** Используйте инструкцию **LIKE** для проверки значения поля **LicensePlate**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-158">**Explanation**: Use the **LIKE** statement to check the **LicensePlate** field value.</span></span> <span data-ttu-id="3e91b-159">Оно должно начинаться с А, затем должна идти любая строка из нуля или более символов и, наконец, цифра 9.</span><span class="sxs-lookup"><span data-stu-id="3e91b-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="3e91b-160">Пример запроса: укажите логику для различных случаев и значений (операторы CASE)</span><span class="sxs-lookup"><span data-stu-id="3e91b-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="3e91b-161">**Описание.** Укажите разные вычисления для поля на основе определенных условий.</span><span class="sxs-lookup"><span data-stu-id="3e91b-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="3e91b-162">Например, укажите строковое описание для количества переданных автомобилей одной и той же марки с особым условием для значения 1.</span><span class="sxs-lookup"><span data-stu-id="3e91b-162">For example, provide a string description for how many cars of the same make passed, with a special case for 1.</span></span>

<span data-ttu-id="3e91b-163">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-163">**Input**:</span></span>

| <span data-ttu-id="3e91b-164">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-164">Make</span></span> | <span data-ttu-id="3e91b-165">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3e91b-166">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-166">Honda</span></span> |<span data-ttu-id="3e91b-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-168">Toyota</span></span> |<span data-ttu-id="3e91b-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-170">Toyota</span></span> |<span data-ttu-id="3e91b-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3e91b-172">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-172">**Output**:</span></span>

| <span data-ttu-id="3e91b-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="3e91b-173">CarsPassed</span></span> | <span data-ttu-id="3e91b-174">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-175">1 Honda</span></span> |<span data-ttu-id="3e91b-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="3e91b-177">2 Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-177">2 Toyotas</span></span> |<span data-ttu-id="3e91b-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="3e91b-179">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-179">**Solution**:</span></span>

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

<span data-ttu-id="3e91b-180">**Объяснение.** Выражение **CASE** позволяет нам предоставить различные вычисления на основе определенных критериев (в нашем случае это число автомобилей в окне статистики).</span><span class="sxs-lookup"><span data-stu-id="3e91b-180">**Explanation**: The **CASE** clause allows us to provide a different computation, based on some criteria (in our case, the count of the cars in the aggregate window).</span></span>

## <a name="query-example-send-data-to-multiple-outputs"></a><span data-ttu-id="3e91b-181">Пример запроса: отправка данных на несколько выходов</span><span class="sxs-lookup"><span data-stu-id="3e91b-181">Query example: Send data to multiple outputs</span></span>
<span data-ttu-id="3e91b-182">**Описание**: отправьте данные в несколько целевых объектов выходных данных из одного задания.</span><span class="sxs-lookup"><span data-stu-id="3e91b-182">**Description**: Send data to multiple output targets from a single job.</span></span>
<span data-ttu-id="3e91b-183">Например, проанализируйте данные для оповещения на основе пороговых значений и заархивируйте все события в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="3e91b-183">For example, analyze data for a threshold-based alert and archive all events to blob storage.</span></span>

<span data-ttu-id="3e91b-184">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-184">**Input**:</span></span>

| <span data-ttu-id="3e91b-185">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-185">Make</span></span> | <span data-ttu-id="3e91b-186">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3e91b-187">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-187">Honda</span></span> |<span data-ttu-id="3e91b-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-189">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-189">Honda</span></span> |<span data-ttu-id="3e91b-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-191">Toyota</span></span> |<span data-ttu-id="3e91b-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-193">Toyota</span></span> |<span data-ttu-id="3e91b-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-195">Toyota</span></span> |<span data-ttu-id="3e91b-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3e91b-197">**Выходные данные 1**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-197">**Output1**:</span></span>

| <span data-ttu-id="3e91b-198">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-198">Make</span></span> | <span data-ttu-id="3e91b-199">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3e91b-200">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-200">Honda</span></span> |<span data-ttu-id="3e91b-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-202">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-202">Honda</span></span> |<span data-ttu-id="3e91b-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-204">Toyota</span></span> |<span data-ttu-id="3e91b-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-206">Toyota</span></span> |<span data-ttu-id="3e91b-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-208">Toyota</span></span> |<span data-ttu-id="3e91b-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3e91b-210">**Выходные данные 2**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-210">**Output2**:</span></span>

| <span data-ttu-id="3e91b-211">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-211">Make</span></span> | <span data-ttu-id="3e91b-212">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-212">Time</span></span> | <span data-ttu-id="3e91b-213">Count</span><span class="sxs-lookup"><span data-stu-id="3e91b-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-214">Toyota</span></span> |<span data-ttu-id="3e91b-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="3e91b-216">3</span><span class="sxs-lookup"><span data-stu-id="3e91b-216">3</span></span> |

<span data-ttu-id="3e91b-217">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-217">**Solution**:</span></span>

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

<span data-ttu-id="3e91b-218">**Объяснение.** Выражение **INTO** сообщает Stream Analytics, в какие выходные данные записывать данные из этого оператора.</span><span class="sxs-lookup"><span data-stu-id="3e91b-218">**Explanation**: The **INTO** clause tells Stream Analytics which of the outputs to write the data to from this statement.</span></span>
<span data-ttu-id="3e91b-219">Первый запрос является передачей полученных данных в выходные данные с именем **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-219">The first query is a pass-through of the data we received to an output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="3e91b-220">Второй запрос выполняет некоторую простую статистическую обработку и фильтрацию и отправляет результаты нижестоящей системе оповещений.</span><span class="sxs-lookup"><span data-stu-id="3e91b-220">The second query does some simple aggregation and filtering, and it sends the results to a downstream alerting system.</span></span>

<span data-ttu-id="3e91b-221">Обратите внимание, что можно повторно использовать результаты обобщенных табличных выражений (таких как инструкции **WITH**) в нескольких выходных инструкциях.</span><span class="sxs-lookup"><span data-stu-id="3e91b-221">Note that you can also reuse the results of the common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="3e91b-222">При этом вы получаете дополнительное преимущество, так как нужно открывать меньше читателей в источнике входных данных.</span><span class="sxs-lookup"><span data-stu-id="3e91b-222">This option has the added benefit of opening fewer readers to the input source.</span></span>
<span data-ttu-id="3e91b-223">Например:</span><span class="sxs-lookup"><span data-stu-id="3e91b-223">For example:</span></span> 

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

## <a name="query-example-count-unique-values"></a><span data-ttu-id="3e91b-224">Пример запроса: подсчет уникальных значений</span><span class="sxs-lookup"><span data-stu-id="3e91b-224">Query example: Count unique values</span></span>
<span data-ttu-id="3e91b-225">**Описание.** Подсчитайте количество уникальных значений поля, которые отображаются в потоке в течение определенного интервала.</span><span class="sxs-lookup"><span data-stu-id="3e91b-225">**Description**: Count the number of unique field values that appear in the stream within a time window.</span></span>
<span data-ttu-id="3e91b-226">Например, сколько уникальных марок автомобилей проходят через пункт взимания дорожного сбора за 2 секунды?</span><span class="sxs-lookup"><span data-stu-id="3e91b-226">For example, how many unique makes of cars passed through the toll booth in a 2-second window?</span></span>

<span data-ttu-id="3e91b-227">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-227">**Input**:</span></span>

| <span data-ttu-id="3e91b-228">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-228">Make</span></span> | <span data-ttu-id="3e91b-229">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3e91b-230">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-230">Honda</span></span> |<span data-ttu-id="3e91b-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-232">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-232">Honda</span></span> |<span data-ttu-id="3e91b-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-234">Toyota</span></span> |<span data-ttu-id="3e91b-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-236">Toyota</span></span> |<span data-ttu-id="3e91b-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-238">Toyota</span></span> |<span data-ttu-id="3e91b-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="3e91b-240">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="3e91b-240">**Output:**</span></span>

| <span data-ttu-id="3e91b-241">Count</span><span class="sxs-lookup"><span data-stu-id="3e91b-241">Count</span></span> | <span data-ttu-id="3e91b-242">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3e91b-243">2</span><span class="sxs-lookup"><span data-stu-id="3e91b-243">2</span></span> |<span data-ttu-id="3e91b-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="3e91b-245">1</span><span class="sxs-lookup"><span data-stu-id="3e91b-245">1</span></span> |<span data-ttu-id="3e91b-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="3e91b-247">**Решение.**</span><span class="sxs-lookup"><span data-stu-id="3e91b-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="3e91b-248">**Объяснение.**
**COUNT(DISTINCT Make)** возвращает количество уникальных значений в столбце **Марка** в течение определенного интервала.</span><span class="sxs-lookup"><span data-stu-id="3e91b-248">**Explanation:**
**COUNT(DISTINCT Make)** returns the number of distinct values in the **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="3e91b-249">Пример запроса: определение изменения значения</span><span class="sxs-lookup"><span data-stu-id="3e91b-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="3e91b-250">**Описание.** Изучите предыдущее значение, чтобы определить, отличается ли оно от текущего.</span><span class="sxs-lookup"><span data-stu-id="3e91b-250">**Description**: Look at a previous value to determine if it is different than the current value.</span></span>
<span data-ttu-id="3e91b-251">Например, предыдущий автомобиль на платной дороге той же марки, что и текущий автомобиль?</span><span class="sxs-lookup"><span data-stu-id="3e91b-251">For example, is the previous car on the toll road the same make as the current car?</span></span>

<span data-ttu-id="3e91b-252">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-252">**Input**:</span></span>

| <span data-ttu-id="3e91b-253">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-253">Make</span></span> | <span data-ttu-id="3e91b-254">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3e91b-255">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-255">Honda</span></span> |<span data-ttu-id="3e91b-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-257">Toyota</span></span> |<span data-ttu-id="3e91b-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="3e91b-259">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-259">**Output**:</span></span>

| <span data-ttu-id="3e91b-260">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-260">Make</span></span> | <span data-ttu-id="3e91b-261">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="3e91b-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-262">Toyota</span></span> |<span data-ttu-id="3e91b-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="3e91b-264">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="3e91b-265">**Объяснение.** Используйте **LAG**, чтобы заглянуть в поток входных данных на одно событие назад и получить значение **Make**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-265">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="3e91b-266">Затем сравните его со значением **Make** в текущем событии и поместите событие в выходные данные, если они отличаются.</span><span class="sxs-lookup"><span data-stu-id="3e91b-266">Then compare it to the **Make** value on the current event and output the event if they are different.</span></span>

## <a name="query-example-find-the-first-event-in-a-window"></a><span data-ttu-id="3e91b-267">Пример запроса: поиск первого события в окне</span><span class="sxs-lookup"><span data-stu-id="3e91b-267">Query example: Find the first event in a window</span></span>
<span data-ttu-id="3e91b-268">**Описание.** Найдите первый автомобиль за каждые 10 минут.</span><span class="sxs-lookup"><span data-stu-id="3e91b-268">**Description**: Find the first car in every 10-minute interval.</span></span>

<span data-ttu-id="3e91b-269">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-269">**Input**:</span></span>

| <span data-ttu-id="3e91b-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3e91b-270">LicensePlate</span></span> | <span data-ttu-id="3e91b-271">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-271">Make</span></span> | <span data-ttu-id="3e91b-272">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="3e91b-273">DXE 5291</span></span> |<span data-ttu-id="3e91b-274">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-274">Honda</span></span> |<span data-ttu-id="3e91b-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="3e91b-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="3e91b-276">YZK 5704</span></span> |<span data-ttu-id="3e91b-277">Ford</span><span class="sxs-lookup"><span data-stu-id="3e91b-277">Ford</span></span> |<span data-ttu-id="3e91b-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="3e91b-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="3e91b-279">RMV 8282</span></span> |<span data-ttu-id="3e91b-280">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-280">Honda</span></span> |<span data-ttu-id="3e91b-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="3e91b-282">YHN 6970</span></span> |<span data-ttu-id="3e91b-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-283">Toyota</span></span> |<span data-ttu-id="3e91b-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="3e91b-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="3e91b-285">VFE 1616</span></span> |<span data-ttu-id="3e91b-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-286">Toyota</span></span> |<span data-ttu-id="3e91b-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="3e91b-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="3e91b-288">QYF 9358</span></span> |<span data-ttu-id="3e91b-289">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-289">Honda</span></span> |<span data-ttu-id="3e91b-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="3e91b-291">MDR 6128</span></span> |<span data-ttu-id="3e91b-292">BMW</span><span class="sxs-lookup"><span data-stu-id="3e91b-292">BMW</span></span> |<span data-ttu-id="3e91b-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="3e91b-294">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-294">**Output**:</span></span>

| <span data-ttu-id="3e91b-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3e91b-295">LicensePlate</span></span> | <span data-ttu-id="3e91b-296">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-296">Make</span></span> | <span data-ttu-id="3e91b-297">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="3e91b-298">DXE 5291</span></span> |<span data-ttu-id="3e91b-299">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-299">Honda</span></span> |<span data-ttu-id="3e91b-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="3e91b-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="3e91b-301">QYF 9358</span></span> |<span data-ttu-id="3e91b-302">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-302">Honda</span></span> |<span data-ttu-id="3e91b-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="3e91b-304">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="3e91b-305">Теперь изменим проблему и найдем первый автомобиль определенной марки за каждые 10 минут.</span><span class="sxs-lookup"><span data-stu-id="3e91b-305">Now let’s change the problem and find the first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="3e91b-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3e91b-306">LicensePlate</span></span> | <span data-ttu-id="3e91b-307">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-307">Make</span></span> | <span data-ttu-id="3e91b-308">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="3e91b-309">DXE 5291</span></span> |<span data-ttu-id="3e91b-310">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-310">Honda</span></span> |<span data-ttu-id="3e91b-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="3e91b-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="3e91b-312">YZK 5704</span></span> |<span data-ttu-id="3e91b-313">Ford</span><span class="sxs-lookup"><span data-stu-id="3e91b-313">Ford</span></span> |<span data-ttu-id="3e91b-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="3e91b-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="3e91b-315">YHN 6970</span></span> |<span data-ttu-id="3e91b-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-316">Toyota</span></span> |<span data-ttu-id="3e91b-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="3e91b-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="3e91b-318">QYF 9358</span></span> |<span data-ttu-id="3e91b-319">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-319">Honda</span></span> |<span data-ttu-id="3e91b-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="3e91b-321">MDR 6128</span></span> |<span data-ttu-id="3e91b-322">BMW</span><span class="sxs-lookup"><span data-stu-id="3e91b-322">BMW</span></span> |<span data-ttu-id="3e91b-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="3e91b-324">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-the-last-event-in-a-window"></a><span data-ttu-id="3e91b-325">Пример запроса: поиск последнего события в окне</span><span class="sxs-lookup"><span data-stu-id="3e91b-325">Query example: Find the last event in a window</span></span>
<span data-ttu-id="3e91b-326">**Описание.** Найдите последний автомобиль за каждые 10 минут.</span><span class="sxs-lookup"><span data-stu-id="3e91b-326">**Description**: Find the last car in every 10-minute interval.</span></span>

<span data-ttu-id="3e91b-327">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-327">**Input**:</span></span>

| <span data-ttu-id="3e91b-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3e91b-328">LicensePlate</span></span> | <span data-ttu-id="3e91b-329">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-329">Make</span></span> | <span data-ttu-id="3e91b-330">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="3e91b-331">DXE 5291</span></span> |<span data-ttu-id="3e91b-332">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-332">Honda</span></span> |<span data-ttu-id="3e91b-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="3e91b-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="3e91b-334">YZK 5704</span></span> |<span data-ttu-id="3e91b-335">Ford</span><span class="sxs-lookup"><span data-stu-id="3e91b-335">Ford</span></span> |<span data-ttu-id="3e91b-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="3e91b-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="3e91b-337">RMV 8282</span></span> |<span data-ttu-id="3e91b-338">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-338">Honda</span></span> |<span data-ttu-id="3e91b-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="3e91b-340">YHN 6970</span></span> |<span data-ttu-id="3e91b-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-341">Toyota</span></span> |<span data-ttu-id="3e91b-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="3e91b-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="3e91b-343">VFE 1616</span></span> |<span data-ttu-id="3e91b-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-344">Toyota</span></span> |<span data-ttu-id="3e91b-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="3e91b-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="3e91b-346">QYF 9358</span></span> |<span data-ttu-id="3e91b-347">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-347">Honda</span></span> |<span data-ttu-id="3e91b-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="3e91b-349">MDR 6128</span></span> |<span data-ttu-id="3e91b-350">BMW</span><span class="sxs-lookup"><span data-stu-id="3e91b-350">BMW</span></span> |<span data-ttu-id="3e91b-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="3e91b-352">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-352">**Output**:</span></span>

| <span data-ttu-id="3e91b-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3e91b-353">LicensePlate</span></span> | <span data-ttu-id="3e91b-354">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-354">Make</span></span> | <span data-ttu-id="3e91b-355">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="3e91b-356">VFE 1616</span></span> |<span data-ttu-id="3e91b-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-357">Toyota</span></span> |<span data-ttu-id="3e91b-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="3e91b-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="3e91b-359">MDR 6128</span></span> |<span data-ttu-id="3e91b-360">BMW</span><span class="sxs-lookup"><span data-stu-id="3e91b-360">BMW</span></span> |<span data-ttu-id="3e91b-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="3e91b-362">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-362">**Solution**:</span></span>

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

<span data-ttu-id="3e91b-363">**Объяснение.** Запрос состоит из двух этапов.</span><span class="sxs-lookup"><span data-stu-id="3e91b-363">**Explanation**: There are two steps in the query.</span></span> <span data-ttu-id="3e91b-364">На первом выполняется поиск последней метки времени в 10-минутном окне,</span><span class="sxs-lookup"><span data-stu-id="3e91b-364">The first one finds the latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="3e91b-365">а на втором — объединение результатов первого запроса с исходным потоком, чтобы найти события, соответствующие последней метке времени в каждом окне.</span><span class="sxs-lookup"><span data-stu-id="3e91b-365">The second step joins the results of the first query with the original stream to find the events that match the last time stamps in each window.</span></span> 

## <a name="query-example-detect-the-absence-of-events"></a><span data-ttu-id="3e91b-366">Пример запроса: обнаружение отсутствия событий</span><span class="sxs-lookup"><span data-stu-id="3e91b-366">Query example: Detect the absence of events</span></span>
<span data-ttu-id="3e91b-367">**Описание.** Убедитесь, что в потоке отсутствует значение, соответствующее определенным условиям.</span><span class="sxs-lookup"><span data-stu-id="3e91b-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="3e91b-368">Например, два автомобиля одной и той же марки подряд въезжают на платную дорогу за последние 90 секунд.</span><span class="sxs-lookup"><span data-stu-id="3e91b-368">For example, have 2 consecutive cars from the same make entered the toll road within the last 90 seconds?</span></span>

<span data-ttu-id="3e91b-369">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-369">**Input**:</span></span>

| <span data-ttu-id="3e91b-370">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-370">Make</span></span> | <span data-ttu-id="3e91b-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="3e91b-371">LicensePlate</span></span> | <span data-ttu-id="3e91b-372">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-373">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-373">Honda</span></span> |<span data-ttu-id="3e91b-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="3e91b-374">ABC-123</span></span> |<span data-ttu-id="3e91b-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="3e91b-376">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-376">Honda</span></span> |<span data-ttu-id="3e91b-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="3e91b-377">AAA-999</span></span> |<span data-ttu-id="3e91b-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="3e91b-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-379">Toyota</span></span> |<span data-ttu-id="3e91b-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="3e91b-380">DEF-987</span></span> |<span data-ttu-id="3e91b-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="3e91b-382">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-382">Honda</span></span> |<span data-ttu-id="3e91b-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="3e91b-383">GHI-345</span></span> |<span data-ttu-id="3e91b-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="3e91b-385">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-385">**Output**:</span></span>

| <span data-ttu-id="3e91b-386">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-386">Make</span></span> | <span data-ttu-id="3e91b-387">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-387">Time</span></span> | <span data-ttu-id="3e91b-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="3e91b-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="3e91b-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="3e91b-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="3e91b-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="3e91b-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="3e91b-391">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-391">Honda</span></span> |<span data-ttu-id="3e91b-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="3e91b-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="3e91b-393">AAA-999</span></span> |<span data-ttu-id="3e91b-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="3e91b-394">ABC-123</span></span> |<span data-ttu-id="3e91b-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="3e91b-396">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-396">**Solution**:</span></span>

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

<span data-ttu-id="3e91b-397">**Объяснение.** Используйте **LAG**, чтобы заглянуть в поток входных данных на одно событие назад и получить значение **Make**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-397">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="3e91b-398">Сравните его со значением **MAKE** в текущем событии и поместите событие в выходные данные, если они совпадают.</span><span class="sxs-lookup"><span data-stu-id="3e91b-398">Compare it to the **MAKE** value in the current event, and then output the event if they are the same.</span></span> <span data-ttu-id="3e91b-399">**LAG** также можно использовать для получения данных о предыдущем автомобиле.</span><span class="sxs-lookup"><span data-stu-id="3e91b-399">You can also use **LAG** to get data about the previous car.</span></span>

## <a name="query-example-detect-the-duration-between-events"></a><span data-ttu-id="3e91b-400">Пример запроса: определение промежутка между событиями</span><span class="sxs-lookup"><span data-stu-id="3e91b-400">Query example: Detect the duration between events</span></span>
<span data-ttu-id="3e91b-401">**Описание**: найдите длительность заданного события.</span><span class="sxs-lookup"><span data-stu-id="3e91b-401">**Description**: Find the duration of a given event.</span></span> <span data-ttu-id="3e91b-402">Например, на основе сведений о посещениях веб-сайта определите время, затраченное на использование функции.</span><span class="sxs-lookup"><span data-stu-id="3e91b-402">For example, given a web clickstream, determine the time spent on a feature.</span></span>

<span data-ttu-id="3e91b-403">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-403">**Input**:</span></span>  

| <span data-ttu-id="3e91b-404">Пользователь</span><span class="sxs-lookup"><span data-stu-id="3e91b-404">User</span></span> | <span data-ttu-id="3e91b-405">Функция</span><span class="sxs-lookup"><span data-stu-id="3e91b-405">Feature</span></span> | <span data-ttu-id="3e91b-406">Событие</span><span class="sxs-lookup"><span data-stu-id="3e91b-406">Event</span></span> | <span data-ttu-id="3e91b-407">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="3e91b-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="3e91b-408">RightMenu</span></span> |<span data-ttu-id="3e91b-409">Начало</span><span class="sxs-lookup"><span data-stu-id="3e91b-409">Start</span></span> |<span data-ttu-id="3e91b-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="3e91b-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="3e91b-411">RightMenu</span></span> |<span data-ttu-id="3e91b-412">End</span><span class="sxs-lookup"><span data-stu-id="3e91b-412">End</span></span> |<span data-ttu-id="3e91b-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="3e91b-414">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-414">**Output**:</span></span>  

| <span data-ttu-id="3e91b-415">Пользователь</span><span class="sxs-lookup"><span data-stu-id="3e91b-415">User</span></span> | <span data-ttu-id="3e91b-416">Функция</span><span class="sxs-lookup"><span data-stu-id="3e91b-416">Feature</span></span> | <span data-ttu-id="3e91b-417">Длительность</span><span class="sxs-lookup"><span data-stu-id="3e91b-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="3e91b-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="3e91b-418">RightMenu</span></span> |<span data-ttu-id="3e91b-419">7</span><span class="sxs-lookup"><span data-stu-id="3e91b-419">7</span></span> |

<span data-ttu-id="3e91b-420">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="3e91b-421">**Объяснение.** Функция **LAST** позволяет получить последнее значение времени **TIME** для события типа **Start**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-421">**Explanation**: Use the **LAST** function to retrieve the last **TIME** value when the event type was **Start**.</span></span> <span data-ttu-id="3e91b-422">Для обозначения того, что результат будет вычисляться для каждого уникального пользователя, функция **LAST** включает параметр **PARTITION BY [user]**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-422">The **LAST** function uses **PARTITION BY [user]** to indicate that the result is computed per unique user.</span></span> <span data-ttu-id="3e91b-423">Максимальный промежуток между событиями **Start** и **Stop** в запросе составляет 1 час, но при необходимости это значение можно изменить **(LIMIT DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="3e91b-423">The query has a 1-hour maximum threshold for the time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-the-duration-of-a-condition"></a><span data-ttu-id="3e91b-424">Пример запроса: определение продолжительности условия</span><span class="sxs-lookup"><span data-stu-id="3e91b-424">Query example: Detect the duration of a condition</span></span>
<span data-ttu-id="3e91b-425">**Описание.** Определите продолжительность условия.</span><span class="sxs-lookup"><span data-stu-id="3e91b-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="3e91b-426">Предположим, произошла ошибка, которая привела к неправильному отображению массы всех автомобилей (больше 9 тонн).</span><span class="sxs-lookup"><span data-stu-id="3e91b-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="3e91b-427">Необходимо вычислить длительность ошибки.</span><span class="sxs-lookup"><span data-stu-id="3e91b-427">We want to compute the duration of the bug.</span></span>

<span data-ttu-id="3e91b-428">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-428">**Input**:</span></span>

| <span data-ttu-id="3e91b-429">Убедитесь,</span><span class="sxs-lookup"><span data-stu-id="3e91b-429">Make</span></span> | <span data-ttu-id="3e91b-430">Время</span><span class="sxs-lookup"><span data-stu-id="3e91b-430">Time</span></span> | <span data-ttu-id="3e91b-431">Вес</span><span class="sxs-lookup"><span data-stu-id="3e91b-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-432">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-432">Honda</span></span> |<span data-ttu-id="3e91b-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="3e91b-434">2000</span><span class="sxs-lookup"><span data-stu-id="3e91b-434">2000</span></span> |
| <span data-ttu-id="3e91b-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-435">Toyota</span></span> |<span data-ttu-id="3e91b-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="3e91b-437">25000</span><span class="sxs-lookup"><span data-stu-id="3e91b-437">25000</span></span> |
| <span data-ttu-id="3e91b-438">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-438">Honda</span></span> |<span data-ttu-id="3e91b-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="3e91b-440">26000</span><span class="sxs-lookup"><span data-stu-id="3e91b-440">26000</span></span> |
| <span data-ttu-id="3e91b-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-441">Toyota</span></span> |<span data-ttu-id="3e91b-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="3e91b-443">25000</span><span class="sxs-lookup"><span data-stu-id="3e91b-443">25000</span></span> |
| <span data-ttu-id="3e91b-444">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-444">Honda</span></span> |<span data-ttu-id="3e91b-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="3e91b-446">26000</span><span class="sxs-lookup"><span data-stu-id="3e91b-446">26000</span></span> |
| <span data-ttu-id="3e91b-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-447">Toyota</span></span> |<span data-ttu-id="3e91b-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="3e91b-449">25000</span><span class="sxs-lookup"><span data-stu-id="3e91b-449">25000</span></span> |
| <span data-ttu-id="3e91b-450">Honda</span><span class="sxs-lookup"><span data-stu-id="3e91b-450">Honda</span></span> |<span data-ttu-id="3e91b-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="3e91b-452">26000</span><span class="sxs-lookup"><span data-stu-id="3e91b-452">26000</span></span> |
| <span data-ttu-id="3e91b-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="3e91b-453">Toyota</span></span> |<span data-ttu-id="3e91b-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="3e91b-455">2000</span><span class="sxs-lookup"><span data-stu-id="3e91b-455">2000</span></span> |

<span data-ttu-id="3e91b-456">**Выходные данные**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-456">**Output**:</span></span>

| <span data-ttu-id="3e91b-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="3e91b-457">StartFault</span></span> | <span data-ttu-id="3e91b-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="3e91b-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="3e91b-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="3e91b-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="3e91b-461">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-461">**Solution**:</span></span>

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

<span data-ttu-id="3e91b-462">**Объяснение.** Функция **LAG** позволяет просмотреть входной поток данных за 24-часовой период и найти экземпляры, в которых **StartFault** и **StopFault** связаны весом менее 20 000.</span><span class="sxs-lookup"><span data-stu-id="3e91b-462">**Explanation**: Use **LAG** to view the input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by the weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="3e91b-463">Пример запроса: заполнить отсутствующие значения</span><span class="sxs-lookup"><span data-stu-id="3e91b-463">Query example: Fill missing values</span></span>
<span data-ttu-id="3e91b-464">**Описание.** Для потока событий с отсутствующими значениями создайте поток событий с регулярными интервалами.</span><span class="sxs-lookup"><span data-stu-id="3e91b-464">**Description**: For the stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="3e91b-465">Например, создавайте каждые 5 секунд событие, сообщающее последнюю видимую точку данных.</span><span class="sxs-lookup"><span data-stu-id="3e91b-465">For example, generate an event every 5 seconds that reports the most recently seen data point.</span></span>

<span data-ttu-id="3e91b-466">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="3e91b-466">**Input**:</span></span>

| <span data-ttu-id="3e91b-467">t</span><span class="sxs-lookup"><span data-stu-id="3e91b-467">t</span></span> | <span data-ttu-id="3e91b-468">value</span><span class="sxs-lookup"><span data-stu-id="3e91b-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="3e91b-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="3e91b-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="3e91b-470">1</span><span class="sxs-lookup"><span data-stu-id="3e91b-470">1</span></span> |
| <span data-ttu-id="3e91b-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="3e91b-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="3e91b-472">2</span><span class="sxs-lookup"><span data-stu-id="3e91b-472">2</span></span> |
| <span data-ttu-id="3e91b-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="3e91b-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="3e91b-474">3</span><span class="sxs-lookup"><span data-stu-id="3e91b-474">3</span></span> |
| <span data-ttu-id="3e91b-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="3e91b-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="3e91b-476">4</span><span class="sxs-lookup"><span data-stu-id="3e91b-476">4</span></span> |
| <span data-ttu-id="3e91b-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="3e91b-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="3e91b-478">5</span><span class="sxs-lookup"><span data-stu-id="3e91b-478">5</span></span> |
| <span data-ttu-id="3e91b-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="3e91b-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="3e91b-480">6</span><span class="sxs-lookup"><span data-stu-id="3e91b-480">6</span></span> |

<span data-ttu-id="3e91b-481">**Выходные данные (первые 10 строк)**:</span><span class="sxs-lookup"><span data-stu-id="3e91b-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="3e91b-482">windowend</span><span class="sxs-lookup"><span data-stu-id="3e91b-482">windowend</span></span> | <span data-ttu-id="3e91b-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="3e91b-483">lastevent.t</span></span> | <span data-ttu-id="3e91b-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="3e91b-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e91b-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="3e91b-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="3e91b-487">1</span><span class="sxs-lookup"><span data-stu-id="3e91b-487">1</span></span> |
| <span data-ttu-id="3e91b-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="3e91b-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="3e91b-490">2</span><span class="sxs-lookup"><span data-stu-id="3e91b-490">2</span></span> |
| <span data-ttu-id="3e91b-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="3e91b-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="3e91b-493">3</span><span class="sxs-lookup"><span data-stu-id="3e91b-493">3</span></span> |
| <span data-ttu-id="3e91b-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="3e91b-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="3e91b-496">4</span><span class="sxs-lookup"><span data-stu-id="3e91b-496">4</span></span> |
| <span data-ttu-id="3e91b-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="3e91b-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="3e91b-499">4</span><span class="sxs-lookup"><span data-stu-id="3e91b-499">4</span></span> |
| <span data-ttu-id="3e91b-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="3e91b-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="3e91b-502">4</span><span class="sxs-lookup"><span data-stu-id="3e91b-502">4</span></span> |
| <span data-ttu-id="3e91b-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="3e91b-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="3e91b-505">5</span><span class="sxs-lookup"><span data-stu-id="3e91b-505">5</span></span> |
| <span data-ttu-id="3e91b-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="3e91b-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="3e91b-508">6</span><span class="sxs-lookup"><span data-stu-id="3e91b-508">6</span></span> |
| <span data-ttu-id="3e91b-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="3e91b-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="3e91b-511">6</span><span class="sxs-lookup"><span data-stu-id="3e91b-511">6</span></span> |
| <span data-ttu-id="3e91b-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="3e91b-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="3e91b-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="3e91b-514">6</span><span class="sxs-lookup"><span data-stu-id="3e91b-514">6</span></span> |

<span data-ttu-id="3e91b-515">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3e91b-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="3e91b-516">**Объяснение.** Этот запрос создает события каждые 5 секунд и выводит последнее событие, полученное ранее.</span><span class="sxs-lookup"><span data-stu-id="3e91b-516">**Explanation**: This query generates events every 5 seconds and outputs the last event that was received previously.</span></span> <span data-ttu-id="3e91b-517">Длительность ["прыгающего"](https://msdn.microsoft.com/library/dn835041.aspx ""Прыгающее окно" — Azure Stream Analytics") окна определяет, насколько далеко в прошлое уходит запрос в поисках последнего события (300 секунд в этом примере).</span><span class="sxs-lookup"><span data-stu-id="3e91b-517">The [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back the query looks to find the latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="3e91b-518">Получение справки</span><span class="sxs-lookup"><span data-stu-id="3e91b-518">Get help</span></span>
<span data-ttu-id="3e91b-519">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="3e91b-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e91b-520">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3e91b-520">Next steps</span></span>
* [<span data-ttu-id="3e91b-521">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3e91b-521">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3e91b-522">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3e91b-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3e91b-523">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3e91b-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3e91b-524">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3e91b-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3e91b-525">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3e91b-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

