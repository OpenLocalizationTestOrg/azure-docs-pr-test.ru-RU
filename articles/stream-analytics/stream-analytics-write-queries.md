---
title: "Написание запросов в Stream Analytics | Документация Майкрософт"
description: "Написание запросов в Stream Analytics и запрос данных | Сегмент схемы обучения"
keywords: "написание запросов, данные запросов, как писать запрос"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b44b0658a06761a805708e7fdeba9e3b2cf9d3ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-write-queries-in-stream-analytics"></a><span data-ttu-id="c9b44-104">Написание запросов в Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c9b44-104">How to write queries in Stream Analytics</span></span>
<span data-ttu-id="c9b44-105">Написание запросов для логической схемы обработки потоков в службе Azure Stream Analytics выполняется как "постоянный запрос", определенный до того, как задание было запущено и применено к поступившим данным.</span><span class="sxs-lookup"><span data-stu-id="c9b44-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches the job.</span></span> <span data-ttu-id="c9b44-106">Преобразование данных выражается с помощью SQL-подобного языка запросов, который по большом счету представляет собой подмножество T-SQL с рядом дополнительных расширений языка, таких как [Оконное расширение](https://msdn.microsoft.com/library/azure/dn835019.aspx) , которое используется для выражения временной семантики.</span><span class="sxs-lookup"><span data-stu-id="c9b44-106">The data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used to express temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="c9b44-107">Написание запросов:</span><span class="sxs-lookup"><span data-stu-id="c9b44-107">Writing Queries:</span></span>
1. <span data-ttu-id="c9b44-108">В задании Stream Analytics на портале управления Azure нажмите **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="c9b44-108">In your Stream Analytics Job in the Azure Management portal, click **Query**.</span></span>
   
    ![Выбор запроса](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="c9b44-110">На портале Azure нажмите кнопку **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="c9b44-110">In the Azure Portal, click **Query**.</span></span>
   
    ![Выбор запроса в предварительной версии](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="c9b44-112">Новые задания включают шаблон запроса, помогающий начать работу.</span><span class="sxs-lookup"><span data-stu-id="c9b44-112">New jobs have a query template to help get you started.</span></span> <span data-ttu-id="c9b44-113">Шаблон запроса выполняет запрос к серверу, проецирующий все поля из входных событий в выходные данные.</span><span class="sxs-lookup"><span data-stu-id="c9b44-113">The query template performs a "pass-through" query that projects all fields from input events into the output.</span></span>  
   
   * <span data-ttu-id="c9b44-114">Если в задании определен хотя бы один источник входных данных и один выход данных, заполнители [YourOutputAlias] и [YourInputAlias] в соответствующих полях можно заменить псевдонимами для входных и выходных данных, которые вы хотите использовать в первую очередь.</span><span class="sxs-lookup"><span data-stu-id="c9b44-114">If you have defined at least one input and output for your job, you can replace the placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with the aliases of the input and output that you wish use first.</span></span> <span data-ttu-id="c9b44-115">Кроме того, создать и проверить запрос по-прежнему можно на классическом портале Azure, не определяя входных и выходных данных для задания.</span><span class="sxs-lookup"><span data-stu-id="c9b44-115">In addition, you can still author and test your query in the Azure Classic Portal without defining inputs and outputs on the job.</span></span>
   * <span data-ttu-id="c9b44-116">Если вам нужно больше, чем простой запрос к серверу, определение запроса можно изменить.</span><span class="sxs-lookup"><span data-stu-id="c9b44-116">If you wish to perform more processing than a simple pass-through, you can edit the query definition.</span></span> <span data-ttu-id="c9b44-117">Чтобы приступить к созданию запроса, рассмотрите некоторые общие схемы запросов, которые показаны [здесь](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="c9b44-117">To get started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Окно данных запросов](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="to-validate-query-data-is-working"></a><span data-ttu-id="c9b44-119">Проверка работоспособности данных запроса:</span><span class="sxs-lookup"><span data-stu-id="c9b44-119">To validate query data is working:</span></span>
<span data-ttu-id="c9b44-120">Чтобы проверить работу запроса, запустите его в браузере, применив к одному или нескольким JSON-файлам с тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="c9b44-120">You can test that your query behaves as expected by running it in the browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="c9b44-121">При этом задание не выполняется, а стоимость услуг не увеличивается.</span><span class="sxs-lookup"><span data-stu-id="c9b44-121">This will not start the job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="c9b44-122">В настоящий момент на портале Azure тестирование запросов не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c9b44-122">Currently in-browser query testing is not supported in the Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="c9b44-123">Убедитесь, что в запросе нет ошибок (в противном случае кнопка «Тест» будет неактивна), и нажмите кнопку «Тест».</span><span class="sxs-lookup"><span data-stu-id="c9b44-123">Make sure that there are no errors in the query (otherwise the Test button will be disabled) and then click the Test button.</span></span>  
   
   ![Проверка данных запросов](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="c9b44-125">Система предложит вам указать файлы для каждого источника входных данных, указанного в запросе.</span><span class="sxs-lookup"><span data-stu-id="c9b44-125">You will be prompted to specify files for each of the inputs referenced in the query.</span></span> <span data-ttu-id="c9b44-126">В этом примере шаблон запроса сохранен в исходном виде, поэтому в диалоговом окне источник входных данных запрашивается под именем yourinputalias.</span><span class="sxs-lookup"><span data-stu-id="c9b44-126">In this example, the template query is left as-is, so the dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![Проверка запроса данных](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="c9b44-128">Найдите тестовый файл.</span><span class="sxs-lookup"><span data-stu-id="c9b44-128">Browse to a test file.</span></span> <span data-ttu-id="c9b44-129">В [GitHub](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) доступно несколько примеров файлов, а также возможность извлекать примеры данных из входных потоковых данных, используя функцию "Пример данных" на вкладке входных данных.</span><span class="sxs-lookup"><span data-stu-id="c9b44-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via the Sample Data function on the inputs tab.</span></span>  
   
   ![Входные данные запроса](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="c9b44-131">Когда вы закроете диалоговое окно, запрос будет применен к тестовым данным, а результаты его выполнения появятся в нижней части страницы «Запрос».</span><span class="sxs-lookup"><span data-stu-id="c9b44-131">After closing the dialog, your query will be run over the test data and you will see the results at the bottom of the Query page.</span></span>  
   
   ![Сводные данные запроса](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="c9b44-133">Получение справки</span><span class="sxs-lookup"><span data-stu-id="c9b44-133">Get help</span></span>
<span data-ttu-id="c9b44-134">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="c9b44-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9b44-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9b44-135">Next steps</span></span>
* [<span data-ttu-id="c9b44-136">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c9b44-136">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c9b44-137">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c9b44-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c9b44-138">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c9b44-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c9b44-139">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c9b44-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c9b44-140">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c9b44-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

