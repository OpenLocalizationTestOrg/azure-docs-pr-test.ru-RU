---
title: "Основные сведения о службе Stream Analytics и журналах операций | Документация Майкрософт"
description: "Порядок работы с журналами операций Stream Analytics"
keywords: "журналы служб"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: c95d240ebef6a84228eb98db70002792fcfbdea6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="b24ba-104">Основные сведения о службе Stream Analytics и журналах операций</span><span class="sxs-lookup"><span data-stu-id="b24ba-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="b24ba-105">Все службы Azure предоставляют пользователям сообщения операционного журнала для записи данных, связанных с операциями управления.</span><span class="sxs-lookup"><span data-stu-id="b24ba-105">All Azure services supply operational logging messages to users to record details related to management operations.</span></span> <span data-ttu-id="b24ba-106">В службе Azure Stream Analytics эти данные можно использовать в целях отладки, например для просмотра состояния задания, хода его выполнения и сообщений об ошибках, а также для отслеживания хода выполнения задания с течением времени, от запуска до обработки и получения выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b24ba-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages to track the progress of a job over time, from start to processing to output.</span></span>

## <a name="find-operation-logs-in-the-azure-management-portal"></a><span data-ttu-id="b24ba-107">Поиск журналов операций на портале управления Azure</span><span class="sxs-lookup"><span data-stu-id="b24ba-107">Find operation logs in the Azure Management portal</span></span>
<span data-ttu-id="b24ba-108">Доступ к журналам операций можно получить одним из двух способов.</span><span class="sxs-lookup"><span data-stu-id="b24ba-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="b24ba-109">Панель мониторинга задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b24ba-109">Dashboard of the Stream Analytics job</span></span>  
* <span data-ttu-id="b24ba-110">Службы управления на классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="b24ba-110">Management Services in the Azure Classic portal</span></span>  

## <a name="dashboard-of-the-stream-analytics-job"></a><span data-ttu-id="b24ba-111">Панель мониторинга задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b24ba-111">Dashboard of the Stream Analytics job</span></span>
<span data-ttu-id="b24ba-112">Ссылка на соответствующие журналы задания Stream Analytics отображается на вкладке панели мониторинга задания. При переходе по этой ссылке фильтры настраиваются на отображение последних журналов соответствующего задания.</span><span class="sxs-lookup"><span data-stu-id="b24ba-112">A link to the corresponding logs of a Stream Analytics job is displayed on the job’s Dashboard tab. If you click on that link, it will set the filters in a way that it shows latest logs for that specific job.</span></span>

  ![Выбор журналов служб управления](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="b24ba-114">Службы управления</span><span class="sxs-lookup"><span data-stu-id="b24ba-114">Management Services</span></span>
<span data-ttu-id="b24ba-115">Чтобы перейти к журналам операций Stream Analytics и других служб на классическом портале Azure, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b24ba-115">To manually navigate to the Operation Logs for Stream Analytics and other services in the Azure Classic portal:</span></span>

1. <span data-ttu-id="b24ba-116">На **классическом портале Azure** щелкните [Службы управления](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b24ba-116">Click on **Management Services** in the [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b24ba-117">Выберите значение **Stream Analytics** в поле **Тип** и имя задания в поле **Имя службы**.</span><span class="sxs-lookup"><span data-stu-id="b24ba-117">Select **Stream Analytics** for **Type** and the name of the job for **Service Name**.</span></span>  
   
   ![Выбор Stream Analytics](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-the-azure-portal"></a><span data-ttu-id="b24ba-119">Поиск журналов аудита на портале Azure</span><span class="sxs-lookup"><span data-stu-id="b24ba-119">Find audit logs in the Azure portal</span></span>
<span data-ttu-id="b24ba-120">Чтобы найти на портале Azure журналы операций для задания Stream Analytics, щелкните **Обзор** и выберите **Журналы аудита**.</span><span class="sxs-lookup"><span data-stu-id="b24ba-120">To find operational logs for your Stream Analytics job in the Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Выбор Stream Analytics на портале Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="b24ba-122">Откроется колонка с событиями за последние 7 дней для всех ресурсов в подписке.</span><span class="sxs-lookup"><span data-stu-id="b24ba-122">This will open a blade showing events from the last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="b24ba-123">Вы можете применить фильтр, чтобы просмотреть события определенного типа или за указанный временной интервал, выбрав команду **Фильтр** .</span><span class="sxs-lookup"><span data-stu-id="b24ba-123">You can filter to see events of a specify type or time frame by clicking the **Filter** command.</span></span>

  ![Выбор Stream Analytics на портале Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="b24ba-125">Получение подробных сведений журнала</span><span class="sxs-lookup"><span data-stu-id="b24ba-125">Get log details</span></span>
<span data-ttu-id="b24ba-126">Для просмотра журналов задания можно использовать фильтры "Диапазон времени" и "Состояние".</span><span class="sxs-lookup"><span data-stu-id="b24ba-126">You can filter by Time Range and Status to view the logs for your job.</span></span>

<span data-ttu-id="b24ba-127">На портале управления Azure нажмите кнопку **Сведения** в нижней части окна, чтобы увидеть дополнительные сведения о выбранном событии.</span><span class="sxs-lookup"><span data-stu-id="b24ba-127">In the Azure Management portal, click on the **Details** button at the bottom of the window to view more details about a selected event.</span></span> 

  ![Выбор сведений](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="b24ba-129">На портале Azure щелкните раздел журнала, чтобы просмотреть включенные в него события.</span><span class="sxs-lookup"><span data-stu-id="b24ba-129">In the Azure portal, click on a log entry to see the detailed events inside it.</span></span>

  ![Выбор подробных сведений на портале Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="b24ba-131">Здесь вы можете открыть колонку **Сведения** , щелкнув событие.</span><span class="sxs-lookup"><span data-stu-id="b24ba-131">From there, you can open the **Detail** blade by clicking on the event.</span></span>

  ![Выбор подробных сведений на портале Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="b24ba-133">Отладка невыполненного задания</span><span class="sxs-lookup"><span data-stu-id="b24ba-133">Debug a failed job</span></span>
<span data-ttu-id="b24ba-134">На портале управления Azure нажмите значок поиска и введите "failed".</span><span class="sxs-lookup"><span data-stu-id="b24ba-134">In the Azure Management portal, click on the Search icon and type ‘failed’.</span></span> <span data-ttu-id="b24ba-135">Это позволит получить все журналы с ошибками.</span><span class="sxs-lookup"><span data-stu-id="b24ba-135">This gives a result of all logs with failures.</span></span> 

  ![Отладка задания с ошибкой](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="b24ba-137">На портале Azure журналы можно отфильтровать по уровню сообщений и просмотреть только **критические** события.</span><span class="sxs-lookup"><span data-stu-id="b24ba-137">In the Azure portal, you can filter by level of message to view **Critical** events.</span></span>

  ![Отладка на портале Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="b24ba-139">Выберите одну из ошибок, нажмите кнопку **Сведения** и ознакомьтесь с дополнительными сведениями об ошибке.</span><span class="sxs-lookup"><span data-stu-id="b24ba-139">You can select any one of the failures, and click on the **Details** for more information on the error.</span></span>  <span data-ttu-id="b24ba-140">Некоторые сообщения об ошибках содержат также информацию о том, как устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="b24ba-140">Some error messages also provide information about how to mitigate the issue.</span></span> 

  ![Сведения об операции](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="b24ba-142">Если вам нужно связаться со [службой поддержки](https://azure.microsoft.com/support/options/) или передать информацию специалистам через [форум MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), обратите внимание на раздел "Сведения об операции", особенно на **Идентификатор корреляции**.</span><span class="sxs-lookup"><span data-stu-id="b24ba-142">In case you need to contact [Support](https://azure.microsoft.com/support/options/) or provide information to the team via the [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note the Operation Details, specifically the **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="b24ba-143">Получение справки</span><span class="sxs-lookup"><span data-stu-id="b24ba-143">Get help</span></span>
<span data-ttu-id="b24ba-144">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="b24ba-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b24ba-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b24ba-145">Next steps</span></span>
* [<span data-ttu-id="b24ba-146">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b24ba-146">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b24ba-147">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b24ba-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b24ba-148">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b24ba-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b24ba-149">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b24ba-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b24ba-150">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b24ba-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

