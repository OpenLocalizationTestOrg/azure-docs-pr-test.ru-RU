---
title: "Отладка запросов Azure Stream Analytics с помощью SELECT INTO | Документация Майкрософт"
description: "Создайте демонстрационные данные во время запроса с помощью инструкции SELECT INTO в Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: b05222c6d6f4fc2c5b847dd75ff7e29352cd538c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="43b7d-103">Отладка запросов с помощью инструкции SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="43b7d-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="43b7d-104">При обработке данных в режиме реального времени важно знать, как выглядят данные во время запроса.</span><span class="sxs-lookup"><span data-stu-id="43b7d-104">In real-time data processing, knowing what the data looks like in the middle of the query can be helpful.</span></span> <span data-ttu-id="43b7d-105">Так как входные данные или шаги задания Azure Stream Analytics можно считать несколько раз, вы можете написать дополнительные инструкции SELECT INTO.</span><span class="sxs-lookup"><span data-stu-id="43b7d-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="43b7d-106">Таким образом вы получаете промежуточные данные в хранилище, на основе которых можно проверить правильность данных, так же, как и с помощью *переменных просмотра* при отладке программы.</span><span class="sxs-lookup"><span data-stu-id="43b7d-106">Doing so outputs intermediate data into storage and lets you inspect the correctness of the data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-to-check-the-data-stream"></a><span data-ttu-id="43b7d-107">Проверка потока данных с помощью SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="43b7d-107">Use SELECT INTO to check the data stream</span></span>

<span data-ttu-id="43b7d-108">В следующем примере запроса в задании Azure Stream Analytics содержится один поток входных данных, два ссылочных набора входных данных и выходные данные для Хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="43b7d-108">The following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output to Azure Table Storage.</span></span> <span data-ttu-id="43b7d-109">Запрос объединяет данные из концентратора событий и два ссылочных больших двоичных объекта, чтобы получить сведения об имени и категории:</span><span class="sxs-lookup"><span data-stu-id="43b7d-109">The query joins data from the event hub and two reference blobs to get the name and category information:</span></span>

![Пример запроса SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="43b7d-111">Обратите внимание, что задание выполняется, но события не создаются в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="43b7d-111">Note that the job is running, but no events are being produced in the output.</span></span> <span data-ttu-id="43b7d-112">На плитке **Мониторинг**, показанной здесь, можно увидеть, что данные выводятся, но невозможно определить, на каком шаге операции **JOIN** были удалены все события.</span><span class="sxs-lookup"><span data-stu-id="43b7d-112">On the **Monitoring** tile, shown here, you can see that the input is producing data, but you don’t know which step of the **JOIN** caused all the events to be dropped.</span></span>

![Плитка "Мониторинг"](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="43b7d-114">В этом случае можно добавить несколько дополнительных инструкций SELECT INTO для регистрации промежуточных результатов операции JOIN и данных, считываемых из входных данных.</span><span class="sxs-lookup"><span data-stu-id="43b7d-114">In this situation, you can add a few extra SELECT INTO statements to “log” the intermediate JOIN results and the data that's read from the input.</span></span>

<span data-ttu-id="43b7d-115">В этом примере мы добавили два новых временных набора выходных данных.</span><span class="sxs-lookup"><span data-stu-id="43b7d-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="43b7d-116">Они могут представлять собой любой приемник.</span><span class="sxs-lookup"><span data-stu-id="43b7d-116">They can be any sink you like.</span></span> <span data-ttu-id="43b7d-117">Ниже в качестве примера используется служба хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="43b7d-117">Here we use Azure Storage as an example:</span></span>

![Добавление дополнительных инструкций SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="43b7d-119">Затем можно переписать запрос следующим образом:</span><span class="sxs-lookup"><span data-stu-id="43b7d-119">You can then rewrite the query like this:</span></span>

![Перезаписанный запрос SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="43b7d-121">Теперь снова запустите задание, которое должно выполняться в течение нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="43b7d-121">Now start the job again, and let it run for a few minutes.</span></span> <span data-ttu-id="43b7d-122">Затем запросите temp1 и temp2 с помощью Visual Studio Cloud Explorer для создания следующих таблиц:</span><span class="sxs-lookup"><span data-stu-id="43b7d-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer to produce the following tables:</span></span>

<span data-ttu-id="43b7d-123">**Таблица temp1**
![Таблица temp1 инструкции SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="43b7d-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="43b7d-124">**Таблица temp2**
![Таблица temp2 инструкции SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="43b7d-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="43b7d-125">Как вы видите, обе таблицы содержат данные, а столбец имени в temp2 заполнен правильно.</span><span class="sxs-lookup"><span data-stu-id="43b7d-125">As you can see, temp1 and temp2 both have data, and the name column is populated correctly in temp2.</span></span> <span data-ttu-id="43b7d-126">Тем не менее, так как данные еще не выведены, произошла какая-то проблема:</span><span class="sxs-lookup"><span data-stu-id="43b7d-126">However, because there is still no data in output, something is wrong:</span></span>

![Таблица output1 инструкции SELECT INTO без данных](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="43b7d-128">Выполнив выборку данных, можно почти определенно сказать, что проблема связана со второй операцией JOIN.</span><span class="sxs-lookup"><span data-stu-id="43b7d-128">By sampling the data, you can be almost certain that the issue is with the second JOIN.</span></span> <span data-ttu-id="43b7d-129">Вы можете скачать ссылочные данные из большого двоичного объекта и убедиться в этом:</span><span class="sxs-lookup"><span data-stu-id="43b7d-129">You can download the reference data from the blob and take a look:</span></span>

![Справочная таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="43b7d-131">Как видно, формат GUID в этих справочных данных отличается от формата столбца в таблице temp2.</span><span class="sxs-lookup"><span data-stu-id="43b7d-131">As you can see, the format of the GUID in this reference data is different from the format of the [from] column in temp2.</span></span> <span data-ttu-id="43b7d-132">Именно поэтому данные не поступили в output1, как положено.</span><span class="sxs-lookup"><span data-stu-id="43b7d-132">That’s why the data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="43b7d-133">Вы можете исправить формат данных, передать их в ссылочный большой двоичный объект и повторить попытку:</span><span class="sxs-lookup"><span data-stu-id="43b7d-133">You can fix the data format, upload it to reference blob, and try again:</span></span>

![Временная таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="43b7d-135">На этот раз выходные данные форматируются и заполняются требуемым образом.</span><span class="sxs-lookup"><span data-stu-id="43b7d-135">This time, the data in the output is formatted and populated as expected.</span></span>

![Итоговая таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="43b7d-137">Получение справки</span><span class="sxs-lookup"><span data-stu-id="43b7d-137">Get help</span></span>

<span data-ttu-id="43b7d-138">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="43b7d-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43b7d-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="43b7d-139">Next steps</span></span>

* [<span data-ttu-id="43b7d-140">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="43b7d-140">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="43b7d-141">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="43b7d-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="43b7d-142">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="43b7d-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="43b7d-143">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="43b7d-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="43b7d-144">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="43b7d-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

