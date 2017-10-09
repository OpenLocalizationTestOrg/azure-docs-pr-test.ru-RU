---
title: "запросы toowrite aaaHow в Stream Analytics | Документы Microsoft"
description: "Написание запросов в Stream Analytics и запрос данных | Сегмент схемы обучения"
keywords: "как toowrite запросы, данные запроса, написать запрос, написание запросов"
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
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a><span data-ttu-id="00b89-104">Как toowrite запросы в Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="00b89-104">How toowrite queries in Stream Analytics</span></span>
<span data-ttu-id="00b89-105">Написание запросов для обработки логики в Azure Stream Analytics потоков реализуется как «постоянный запрос», определенный перед запуском задания, а также содержать данные достигнет hello задания.</span><span class="sxs-lookup"><span data-stu-id="00b89-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches hello job.</span></span> <span data-ttu-id="00b89-106">Преобразование данных Hello выражается на языке SQL-подобного запроса, который во многом подмножество T-SQL с некоторыми добавляется расширений языка, например [оконных](https://msdn.microsoft.com/library/azure/dn835019.aspx) использовать временную семантику tooexpress.</span><span class="sxs-lookup"><span data-stu-id="00b89-106">hello data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used tooexpress temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="00b89-107">Написание запросов:</span><span class="sxs-lookup"><span data-stu-id="00b89-107">Writing Queries:</span></span>
1. <span data-ttu-id="00b89-108">В вашей задание Stream Analytics на портале управления Azure hello, щелкните **запроса**.</span><span class="sxs-lookup"><span data-stu-id="00b89-108">In your Stream Analytics Job in hello Azure Management portal, click **Query**.</span></span>
   
    ![Выбор запроса](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="00b89-110">В hello портала Azure щелкните **запроса**.</span><span class="sxs-lookup"><span data-stu-id="00b89-110">In hello Azure Portal, click **Query**.</span></span>
   
    ![Выбор запроса в предварительной версии](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="00b89-112">Новые задания имеют toohelp шаблона запроса приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="00b89-112">New jobs have a query template toohelp get you started.</span></span> <span data-ttu-id="00b89-113">Hello что шаблона выполняет «сквозной» направляет запрос эти проекты все поля из события ввода в выходные данные hello.</span><span class="sxs-lookup"><span data-stu-id="00b89-113">hello query template performs a "pass-through" query that projects all fields from input events into hello output.</span></span>  
   
   * <span data-ttu-id="00b89-114">При наличии по крайней мере один вход и выход для задания можно заменить hello заполнитель «[YourOutputAlias]» и «[YourInputAlias]» полей псевдонимов hello hello ввода и вывода, сначала нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="00b89-114">If you have defined at least one input and output for your job, you can replace hello placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with hello aliases of hello input and output that you wish use first.</span></span> <span data-ttu-id="00b89-115">Кроме того по-прежнему можно создать и проверить запрос в hello классический портал Azure без определения входных и выходных данных задания hello.</span><span class="sxs-lookup"><span data-stu-id="00b89-115">In addition, you can still author and test your query in hello Azure Classic Portal without defining inputs and outputs on hello job.</span></span>
   * <span data-ttu-id="00b89-116">При необходимости дополнительной обработки, чем простой сквозной tooperform можно изменить определение запроса hello.</span><span class="sxs-lookup"><span data-stu-id="00b89-116">If you wish tooperform more processing than a simple pass-through, you can edit hello query definition.</span></span> <span data-ttu-id="00b89-117">tooget к созданию запроса, рассмотрим некоторые из распространенных запросов регистрируются шаблоны [здесь](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="00b89-117">tooget started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Окно данных запросов](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a><span data-ttu-id="00b89-119">данные запроса toovalidate работает:</span><span class="sxs-lookup"><span data-stu-id="00b89-119">toovalidate query data is working:</span></span>
<span data-ttu-id="00b89-120">Можно проверить, что запрос правильно работает, запустив его в браузере hello через один или несколько локальных JSON файлы, содержащие данные теста.</span><span class="sxs-lookup"><span data-stu-id="00b89-120">You can test that your query behaves as expected by running it in hello browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="00b89-121">Это будет запустить задание hello или не имеет отношения к выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="00b89-121">This will not start hello job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="00b89-122">В настоящее время тестирование в браузере запроса не поддерживается в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="00b89-122">Currently in-browser query testing is not supported in hello Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="00b89-123">Убедитесь, что отсутствии ошибок в запросе hello (в противном случае hello теста кнопка будет неактивной) и нажмите кнопку "Тест" hello ".</span><span class="sxs-lookup"><span data-stu-id="00b89-123">Make sure that there are no errors in hello query (otherwise hello Test button will be disabled) and then click hello Test button.</span></span>  
   
   ![Проверка данных запросов](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="00b89-125">Появится запрос toospecify файлов для каждого входа hello, указанным в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="00b89-125">You will be prompted toospecify files for each of hello inputs referenced in hello query.</span></span> <span data-ttu-id="00b89-126">В этом примере hello шаблона запроса останется значение-настолько, запрашивает у диалогового окна hello для входа с именем «yourinputalias».</span><span class="sxs-lookup"><span data-stu-id="00b89-126">In this example, hello template query is left as-is, so hello dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![Проверка запроса данных](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="00b89-128">Найдите файл tooa теста.</span><span class="sxs-lookup"><span data-stu-id="00b89-128">Browse tooa test file.</span></span> <span data-ttu-id="00b89-129">Несколько файлов примеров доступны на [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) и образец данных также можно извлечь из собственных входные данные потока через hello функция образцы данных на вкладке hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="00b89-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via hello Sample Data function on hello inputs tab.</span></span>  
   
   ![Входные данные запроса](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="00b89-131">После закрытия диалогового окна hello, запрос будет выполняться через hello тестовых данных и вы увидите результаты hello внизу hello hello запроса страницы.</span><span class="sxs-lookup"><span data-stu-id="00b89-131">After closing hello dialog, your query will be run over hello test data and you will see hello results at hello bottom of hello Query page.</span></span>  
   
   ![Сводные данные запроса](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="00b89-133">Получение справки</span><span class="sxs-lookup"><span data-stu-id="00b89-133">Get help</span></span>
<span data-ttu-id="00b89-134">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="00b89-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="00b89-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="00b89-135">Next steps</span></span>
* [<span data-ttu-id="00b89-136">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="00b89-136">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="00b89-137">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="00b89-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="00b89-138">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="00b89-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="00b89-139">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="00b89-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="00b89-140">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="00b89-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

