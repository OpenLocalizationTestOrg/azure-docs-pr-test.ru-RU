---
title: "Проверка запросов Stream Analytics aaaAzure | Документы Microsoft"
description: "Как tootest запросах в заданий Stream Analytics."
keywords: "проверка запроса, устранение неполадок запроса"
documentation center: 
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a><span data-ttu-id="dc018-104">Проверить запросы Azure Stream Analytics в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="dc018-104">Test Azure Stream Analytics queries in hello Azure portal</span></span>

<span data-ttu-id="dc018-105">С Azure Stream Analytics можно проверить запросы в hello портал Azure без необходимости toostart или остановка задания.</span><span class="sxs-lookup"><span data-stu-id="dc018-105">With Azure Stream Analytics, you can test queries in hello Azure portal without needing toostart or stop a job.</span></span>

## <a name="test-hello-input"></a><span data-ttu-id="dc018-106">Входные данные теста hello</span><span class="sxs-lookup"><span data-stu-id="dc018-106">Test hello input</span></span>

1. <span data-ttu-id="dc018-107">tootest с образцами входных данных, щелкните правой кнопкой мыши любой из введенных данных, а затем выберите **отправьте демонстрационные данные из файла**.</span><span class="sxs-lookup"><span data-stu-id="dc018-107">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![Проверка запроса редактора запросов Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="dc018-109">После завершения передачи hello щелкните **теста** tootest этот запрос к hello образец данных, которые вы указали.</span><span class="sxs-lookup"><span data-stu-id="dc018-109">After hello upload is complete, click **Test** tootest this query against hello sample data you have provided.</span></span>

    ![Проверка демонстрационных данных редактора запросов Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="dc018-111">Hello выходные данные запроса отображается в браузере hello ссылке для загрузки результатов следует должны выходные данные теста hello toosave для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="dc018-111">hello output of your query is displayed in hello browser, with Download results link should you want toosave hello test output for later use.</span></span> <span data-ttu-id="dc018-112">Теперь можно легко и последовательно изменения запроса и проверить его несколько раз toosee, как изменяется hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="dc018-112">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Пример выходных данных редактора запросов Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="dc018-114">С несколькими выходами, используемые в запросе можно просмотреть результаты hello для обоих выходов отдельно и легко переключаться между ними.</span><span class="sxs-lookup"><span data-stu-id="dc018-114">With multiple outputs used in a query, you can see hello results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="dc018-115">После вы удовлетворены hello результаты, показанные в браузере hello, сохранить запрос, запуск задания и разрешить его обработки событий без ошибок.</span><span class="sxs-lookup"><span data-stu-id="dc018-115">After you are satisfied with hello results shown in hello browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="dc018-116">Получение справки</span><span class="sxs-lookup"><span data-stu-id="dc018-116">Get help</span></span>

<span data-ttu-id="dc018-117">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="dc018-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc018-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc018-118">Next steps</span></span>

* [<span data-ttu-id="dc018-119">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="dc018-119">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="dc018-120">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="dc018-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="dc018-121">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="dc018-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="dc018-122">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="dc018-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="dc018-123">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="dc018-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
