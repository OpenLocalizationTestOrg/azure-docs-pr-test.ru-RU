---
title: "Входные данные выборки в Azure Stream Analytics | Документация Майкрософт"
description: "Оперативно обнаруживайте проблемы при устранении неполадок с заданиями Stream Analytics."
keywords: "устранение неполадок с входными данными, выборка входных данных"
documentationcenter: 
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 0bb66090b5025d57f5ca8f30713aef4e444fa8e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="1a660-104">Выборка потока входных данных Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1a660-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="1a660-105">Используя Azure Stream Analytics, можно создать выборку входных событий из файла и проверить запросы на портале без необходимости запуска или остановки задания.</span><span class="sxs-lookup"><span data-stu-id="1a660-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in the portal without needing to start or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="1a660-106">Тестирование запроса</span><span class="sxs-lookup"><span data-stu-id="1a660-106">Testing your query</span></span>

<span data-ttu-id="1a660-107">На панели сведений о задании Stream Analytics откройте колонку **редактора запросов**, щелкнув имя запроса в разделе **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="1a660-107">In the Stream Analytics job details pane, open the **Query editor** blade by clicking the query name under **Query**.</span></span> <span data-ttu-id="1a660-108">(В нашем примере сценария щелкните заполнитель **< >**, так как запрос еще не создан.)</span><span class="sxs-lookup"><span data-stu-id="1a660-108">(In our example scenario, because no query has been created yet, click the **< >** placeholder.)</span></span>

![Редактор запросов Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="1a660-110">Появится колонка полнофункционального редактора для создания запроса (как и в предыдущей версии).</span><span class="sxs-lookup"><span data-stu-id="1a660-110">The rich editor blade for creating your query is displayed as it was in the previous release.</span></span> <span data-ttu-id="1a660-111">Теперь в колонке есть новая панель слева, в которой отображаются входные и выходные данные, используемые в запросе и определенные для этого задания.</span><span class="sxs-lookup"><span data-stu-id="1a660-111">Now the blade has been updated with a new left pane that shows the inputs and outputs that are used by the query and defined for this job.</span></span>

![Список входных и выходных данных редактора запросов Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="1a660-113">Кроме того, показаны и дополнительные не определенные входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="1a660-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="1a660-114">Они находятся в новом шаблоне запроса, с которого вы начнете свою работу.</span><span class="sxs-lookup"><span data-stu-id="1a660-114">They come from the new query template that you start with.</span></span> <span data-ttu-id="1a660-115">При изменении запроса они изменяются и могут даже полностью исчезнуть.</span><span class="sxs-lookup"><span data-stu-id="1a660-115">They change, or even disappear altogether, as you edit the query.</span></span> <span data-ttu-id="1a660-116">Сейчас их можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="1a660-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="1a660-117">Чтобы проверить пример входных данных, щелкните любые из них правой кнопкой мыши и выберите **Отправить образец данных из файла**.</span><span class="sxs-lookup"><span data-stu-id="1a660-117">To test with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![Команда "Отправить образец данных из файла" редактора запросов Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="1a660-119">После завершения загрузки нажмите кнопку **Тест** для проверки этого запроса на основе указанных демонстрационных данных.</span><span class="sxs-lookup"><span data-stu-id="1a660-119">After the upload is complete, click **Test** to test this query against the sample data you have just provided.</span></span>

![Кнопка "Тест" редактора запросов Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="1a660-121">Если вы хотите сохранить выходные данные проверки для последующего использования, в браузере отображается ссылка для скачивания результатов по выходным данным запроса.</span><span class="sxs-lookup"><span data-stu-id="1a660-121">If you want to save the test output for later use, the output of your query is displayed in the browser with a link to the download results.</span></span> <span data-ttu-id="1a660-122">Теперь можно легко и последовательно изменить запрос, а также несколько раз проверить его, чтобы увидеть, как изменятся выходные данные.</span><span class="sxs-lookup"><span data-stu-id="1a660-122">You can now easily and iteratively modify your query and test it repeatedly to see how the output changes.</span></span>

![Пример выходных данных редактора запросов Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="1a660-124">На предыдущем рисунке видно, что добавлен второй набор выходных данных с именем **HighAvgTempOutput**.</span><span class="sxs-lookup"><span data-stu-id="1a660-124">In the preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="1a660-125">При использовании нескольких наборов выходных данных в запросе можно просмотреть результаты для каждого из них отдельно и легко переключаться между ними.</span><span class="sxs-lookup"><span data-stu-id="1a660-125">When you use multiple outputs in a query, you can see the results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="1a660-126">Если результаты удовлетворительные, вы можете сохранить запрос, запустить задание и наблюдать за работой Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="1a660-126">After you are satisfied with the results, you can save your query, start your job, sit back and watch the magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="1a660-127">Получение справки</span><span class="sxs-lookup"><span data-stu-id="1a660-127">Get help</span></span>

<span data-ttu-id="1a660-128">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="1a660-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a660-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a660-129">Next steps</span></span>
* [<span data-ttu-id="1a660-130">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1a660-130">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1a660-131">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1a660-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1a660-132">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1a660-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1a660-133">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1a660-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1a660-134">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1a660-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
