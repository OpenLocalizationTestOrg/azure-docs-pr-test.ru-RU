---
title: "входные данные выборки AAA в Azure Stream Analytics | Документы Microsoft"
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
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="d9d08-104">Выборка потока входных данных Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d9d08-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="d9d08-105">С помощью Azure Stream Analytics, можно произвести выборку входных событий, которые берутся из файла и проверки запросов на портале hello без необходимости toostart или остановка задания.</span><span class="sxs-lookup"><span data-stu-id="d9d08-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in hello portal without needing toostart or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="d9d08-106">Тестирование запроса</span><span class="sxs-lookup"><span data-stu-id="d9d08-106">Testing your query</span></span>

<span data-ttu-id="d9d08-107">В области сведений задания Stream Analytics hello, откройте hello **редактора запросов** колонки, щелкнув имя запроса hello под **запроса**.</span><span class="sxs-lookup"><span data-stu-id="d9d08-107">In hello Stream Analytics job details pane, open hello **Query editor** blade by clicking hello query name under **Query**.</span></span> <span data-ttu-id="d9d08-108">(В нашем примере сценария, так как нет запроса была создана ранее, нажмите кнопку hello **< >** заполнителя.)</span><span class="sxs-lookup"><span data-stu-id="d9d08-108">(In our example scenario, because no query has been created yet, click hello **< >** placeholder.)</span></span>

![редактор запросов Stream Analytics Hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="d9d08-110">Hello колонке полнофункциональный редактор для создания запроса отображается, как это было в предыдущем выпуске hello.</span><span class="sxs-lookup"><span data-stu-id="d9d08-110">hello rich editor blade for creating your query is displayed as it was in hello previous release.</span></span> <span data-ttu-id="d9d08-111">Теперь колонки hello обновлена с новым левой области, показано hello входы и выходы, используемых запросом hello и определенные для этого задания.</span><span class="sxs-lookup"><span data-stu-id="d9d08-111">Now hello blade has been updated with a new left pane that shows hello inputs and outputs that are used by hello query and defined for this job.</span></span>

![редактор запросов Stream Analytics Hello получает на входе и выводит списки](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="d9d08-113">Кроме того, показаны и дополнительные не определенные входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="d9d08-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="d9d08-114">Они извлекаются из hello новый шаблон запроса, начинающихся с.</span><span class="sxs-lookup"><span data-stu-id="d9d08-114">They come from hello new query template that you start with.</span></span> <span data-ttu-id="d9d08-115">Измените, или даже исчезнуть, при редактировании запроса hello.</span><span class="sxs-lookup"><span data-stu-id="d9d08-115">They change, or even disappear altogether, as you edit hello query.</span></span> <span data-ttu-id="d9d08-116">Сейчас их можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="d9d08-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="d9d08-117">tootest с образцами входных данных, щелкните правой кнопкой мыши любой из введенных данных, а затем выберите **отправьте демонстрационные данные из файла**.</span><span class="sxs-lookup"><span data-stu-id="d9d08-117">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![Здравствуйте, Stream Analytics запрос редактора передачи данных выборки файл-команда](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="d9d08-119">После завершения передачи hello щелкните **тест** tootest этот запрос к hello образец данных, предоставляются только.</span><span class="sxs-lookup"><span data-stu-id="d9d08-119">After hello upload is complete, click **Test** tootest this query against hello sample data you have just provided.</span></span>

![кнопки теста редактора запросов Stream Analytics Hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="d9d08-121">Следует выходных данных toosave hello теста для последующего использования hello выходные данные запроса отображается в браузере hello результатами загрузки toohello ссылку.</span><span class="sxs-lookup"><span data-stu-id="d9d08-121">If you want toosave hello test output for later use, hello output of your query is displayed in hello browser with a link toohello download results.</span></span> <span data-ttu-id="d9d08-122">Теперь можно легко и последовательно изменения запроса и проверить его несколько раз toosee, как изменяется hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="d9d08-122">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Пример выходных данных редактора запросов Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="d9d08-124">В hello предшествующий изображения, второй выход была добавлена, называется **HighAvgTempOutput**.</span><span class="sxs-lookup"><span data-stu-id="d9d08-124">In hello preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="d9d08-125">При использовании в запросе несколько выходных данных, можно увидеть результаты hello для каждого выхода отдельно и легко переключаться между ними.</span><span class="sxs-lookup"><span data-stu-id="d9d08-125">When you use multiple outputs in a query, you can see hello results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="d9d08-126">После hello результаты вас устраивают, можно сохранить запрос, запустите задание, сядьте и контрольных magic hello объекта Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d9d08-126">After you are satisfied with hello results, you can save your query, start your job, sit back and watch hello magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="d9d08-127">Получение справки</span><span class="sxs-lookup"><span data-stu-id="d9d08-127">Get help</span></span>

<span data-ttu-id="d9d08-128">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="d9d08-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9d08-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9d08-129">Next steps</span></span>
* [<span data-ttu-id="d9d08-130">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d9d08-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d9d08-131">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d9d08-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d9d08-132">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d9d08-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="d9d08-133">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d9d08-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d9d08-134">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d9d08-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
