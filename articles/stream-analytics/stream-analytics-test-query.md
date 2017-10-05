---
title: "Тестирование запросов Azure Stream Analytics | Документация Майкрософт"
description: "Сведения о том, как проверить запросы в заданиях Stream Analytics."
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
ms.openlocfilehash: 16bb3f26ec3a69e5204162db9e54a186cf1ec6a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="test-azure-stream-analytics-queries-in-the-azure-portal"></a><span data-ttu-id="9db90-104">Проверка запросов Azure Stream Analytics на портале Azure</span><span class="sxs-lookup"><span data-stu-id="9db90-104">Test Azure Stream Analytics queries in the Azure portal</span></span>

<span data-ttu-id="9db90-105">В Azure Stream Analytics можно проверить запросы на портале Azure, не запуская и не останавливая задание.</span><span class="sxs-lookup"><span data-stu-id="9db90-105">With Azure Stream Analytics, you can test queries in the Azure portal without needing to start or stop a job.</span></span>

## <a name="test-the-input"></a><span data-ttu-id="9db90-106">Проверки входных данных</span><span class="sxs-lookup"><span data-stu-id="9db90-106">Test the input</span></span>

1. <span data-ttu-id="9db90-107">Чтобы проверить пример входных данных, щелкните любые из них правой кнопкой мыши и выберите **Отправить образец данных из файла**.</span><span class="sxs-lookup"><span data-stu-id="9db90-107">To test with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![Проверка запроса редактора запросов Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="9db90-109">После завершения загрузки нажмите кнопку **Тест** для проверки этого запроса на основе указанных демонстрационных данных.</span><span class="sxs-lookup"><span data-stu-id="9db90-109">After the upload is complete, click **Test** to test this query against the sample data you have provided.</span></span>

    ![Проверка демонстрационных данных редактора запросов Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="9db90-111">Если вам понадобится сохранить выходные данные проверки для последующего использования, в браузере отображается ссылка для скачивания результатов по выходным данным запроса.</span><span class="sxs-lookup"><span data-stu-id="9db90-111">The output of your query is displayed in the browser, with Download results link should you want to save the test output for later use.</span></span> <span data-ttu-id="9db90-112">Теперь можно легко и последовательно изменить запрос, а также несколько раз проверить его, чтобы увидеть, как изменятся выходные данные.</span><span class="sxs-lookup"><span data-stu-id="9db90-112">You can now easily and iteratively modify your query and test it repeatedly to see how the output changes.</span></span>

![Пример выходных данных редактора запросов Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="9db90-114">При использовании нескольких наборов выходных данных в запросе можно просмотреть результаты для каждого из них отдельно и легко переключаться между ними.</span><span class="sxs-lookup"><span data-stu-id="9db90-114">With multiple outputs used in a query, you can see the results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="9db90-115">Если результаты в браузере удовлетворительны, можно сохранить запрос, запустить задание и наблюдать за обработкой событий без ошибок.</span><span class="sxs-lookup"><span data-stu-id="9db90-115">After you are satisfied with the results shown in the browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="9db90-116">Получение справки</span><span class="sxs-lookup"><span data-stu-id="9db90-116">Get help</span></span>

<span data-ttu-id="9db90-117">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="9db90-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9db90-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9db90-118">Next steps</span></span>

* [<span data-ttu-id="9db90-119">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9db90-119">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="9db90-120">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9db90-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="9db90-121">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9db90-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="9db90-122">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9db90-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="9db90-123">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9db90-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
