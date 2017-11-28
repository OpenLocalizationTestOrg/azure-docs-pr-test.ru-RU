---
title: "aaaDebug Azure Stream Analytics запросы с помощью инструкции SELECT INTO | Документы Microsoft"
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
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="c31b8-103">Отладка запросов с помощью инструкции SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="c31b8-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="c31b8-104">В режиме реального времени обработки данных определить, какие данные hello похоже, в середине hello hello запроса могут оказаться полезными.</span><span class="sxs-lookup"><span data-stu-id="c31b8-104">In real-time data processing, knowing what hello data looks like in hello middle of hello query can be helpful.</span></span> <span data-ttu-id="c31b8-105">Так как входные данные или шаги задания Azure Stream Analytics можно считать несколько раз, вы можете написать дополнительные инструкции SELECT INTO.</span><span class="sxs-lookup"><span data-stu-id="c31b8-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="c31b8-106">Это генерирует промежуточные данные в хранилище и позволяет проверить правильность hello hello данных, так же как и *наблюдать за переменными* сделать при отладке программы.</span><span class="sxs-lookup"><span data-stu-id="c31b8-106">Doing so outputs intermediate data into storage and lets you inspect hello correctness of hello data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-toocheck-hello-data-stream"></a><span data-ttu-id="c31b8-107">Использование SELECT INTO toocheck hello потока данных</span><span class="sxs-lookup"><span data-stu-id="c31b8-107">Use SELECT INTO toocheck hello data stream</span></span>

<span data-ttu-id="c31b8-108">Hello следующий запрос в задание Azure Stream Analytics имеет один поток ввода, двух входов справочные данные и вывода tooAzure хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="c31b8-108">hello following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output tooAzure Table Storage.</span></span> <span data-ttu-id="c31b8-109">запрос Hello объединяет данные из концентратора событий hello и ссылки на две большие двоичные объекты tooget hello имя и сведения о категории:</span><span class="sxs-lookup"><span data-stu-id="c31b8-109">hello query joins data from hello event hub and two reference blobs tooget hello name and category information:</span></span>

![Пример запроса SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="c31b8-111">Обратите внимание, что hello задание выполняется, но события не создаются в выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="c31b8-111">Note that hello job is running, but no events are being produced in hello output.</span></span> <span data-ttu-id="c31b8-112">На hello **мониторинг** плитки, показано ниже, вы увидите, что зарегистрировавшем hello ввода данных, но вы не знаете, какой шаг hello **JOIN** вызвало все hello toobe события удалены.</span><span class="sxs-lookup"><span data-stu-id="c31b8-112">On hello **Monitoring** tile, shown here, you can see that hello input is producing data, but you don’t know which step of hello **JOIN** caused all hello events toobe dropped.</span></span>

![Мониторинг плитки приветствия](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="c31b8-114">В этом случае можно добавить несколько дополнительных инструкций SELECT INTO слишком «вход» hello промежуточные результаты СОЕДИНЕНИЯ и hello данные, считанные из входных данных hello.</span><span class="sxs-lookup"><span data-stu-id="c31b8-114">In this situation, you can add a few extra SELECT INTO statements too“log” hello intermediate JOIN results and hello data that's read from hello input.</span></span>

<span data-ttu-id="c31b8-115">В этом примере мы добавили два новых временных набора выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c31b8-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="c31b8-116">Они могут представлять собой любой приемник.</span><span class="sxs-lookup"><span data-stu-id="c31b8-116">They can be any sink you like.</span></span> <span data-ttu-id="c31b8-117">Ниже в качестве примера используется служба хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="c31b8-117">Here we use Azure Storage as an example:</span></span>

![Добавление дополнительных инструкций SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="c31b8-119">Затем можно переписать запрос hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c31b8-119">You can then rewrite hello query like this:</span></span>

![Перезаписанный запрос SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="c31b8-121">Теперь снова запустите задание hello и дать ему возможность работать в течение нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="c31b8-121">Now start hello job again, and let it run for a few minutes.</span></span> <span data-ttu-id="c31b8-122">Затем запрос temp1 и temp2 с Visual Studio Cloud Explorer tooproduce hello следующие таблицы:</span><span class="sxs-lookup"><span data-stu-id="c31b8-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer tooproduce hello following tables:</span></span>

<span data-ttu-id="c31b8-123">**Таблица temp1**
![Таблица temp1 инструкции SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="c31b8-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="c31b8-124">**Таблица temp2**
![Таблица temp2 инструкции SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="c31b8-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="c31b8-125">Как видите, temp1 и temp2 содержат данные и имя столбца hello в temp2 заполняются правильно.</span><span class="sxs-lookup"><span data-stu-id="c31b8-125">As you can see, temp1 and temp2 both have data, and hello name column is populated correctly in temp2.</span></span> <span data-ttu-id="c31b8-126">Тем не менее, так как данные еще не выведены, произошла какая-то проблема:</span><span class="sxs-lookup"><span data-stu-id="c31b8-126">However, because there is still no data in output, something is wrong:</span></span>

![Таблица output1 инструкции SELECT INTO без данных](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="c31b8-128">С помощью выборки данных hello, вам может быть почти наверняка, hello проблема связана с hello второй СОЕДИНЕНИЯ.</span><span class="sxs-lookup"><span data-stu-id="c31b8-128">By sampling hello data, you can be almost certain that hello issue is with hello second JOIN.</span></span> <span data-ttu-id="c31b8-129">Можно загрузить hello ссылочных данных из большого двоичного объекта hello и обратите внимание:</span><span class="sxs-lookup"><span data-stu-id="c31b8-129">You can download hello reference data from hello blob and take a look:</span></span>

![Справочная таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="c31b8-131">Как видите, формат hello hello GUID в этом ссылочных данных отличается от hello формат hello [из] столбца в temp2.</span><span class="sxs-lookup"><span data-stu-id="c31b8-131">As you can see, hello format of hello GUID in this reference data is different from hello format of hello [from] column in temp2.</span></span> <span data-ttu-id="c31b8-132">Вот почему hello данные не поступают в output1 должным образом.</span><span class="sxs-lookup"><span data-stu-id="c31b8-132">That’s why hello data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="c31b8-133">Можно устранить hello формат данных, передать его tooreference больших двоичных объектов и повторите попытку:</span><span class="sxs-lookup"><span data-stu-id="c31b8-133">You can fix hello data format, upload it tooreference blob, and try again:</span></span>

![Временная таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="c31b8-135">На этот раз данные hello в выходных данных hello форматируются и заполнены должным образом.</span><span class="sxs-lookup"><span data-stu-id="c31b8-135">This time, hello data in hello output is formatted and populated as expected.</span></span>

![Итоговая таблица SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="c31b8-137">Получение справки</span><span class="sxs-lookup"><span data-stu-id="c31b8-137">Get help</span></span>

<span data-ttu-id="c31b8-138">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="c31b8-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c31b8-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c31b8-139">Next steps</span></span>

* [<span data-ttu-id="c31b8-140">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c31b8-140">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c31b8-141">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c31b8-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c31b8-142">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c31b8-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c31b8-143">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c31b8-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c31b8-144">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c31b8-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

