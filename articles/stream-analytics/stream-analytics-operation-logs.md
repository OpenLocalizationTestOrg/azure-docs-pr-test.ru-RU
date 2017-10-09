---
title: "с помощью операции и служба журналов в Stream Analytics aaaDebug | Документы Microsoft"
description: "Поток как toouse аналитика журналов операций"
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
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="7dab5-104">Основные сведения о службе Stream Analytics и журналах операций</span><span class="sxs-lookup"><span data-stu-id="7dab5-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="7dab5-105">Всех служб Azure, оперативной питания ведения журнала сообщений toousers toorecord сведений о связанных с toomanagement операций.</span><span class="sxs-lookup"><span data-stu-id="7dab5-105">All Azure services supply operational logging messages toousers toorecord details related toomanagement operations.</span></span> <span data-ttu-id="7dab5-106">В Azure Stream Analytics эти сведения можно использовать для отладки, такие как просмотр состояния задания, ход выполнения задания и сбой сообщения tootrack hello ход выполнения задания по времени, из начала tooprocessing toooutput.</span><span class="sxs-lookup"><span data-stu-id="7dab5-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages tootrack hello progress of a job over time, from start tooprocessing toooutput.</span></span>

## <a name="find-operation-logs-in-hello-azure-management-portal"></a><span data-ttu-id="7dab5-107">Найти журналы операций на портале управления Azure hello</span><span class="sxs-lookup"><span data-stu-id="7dab5-107">Find operation logs in hello Azure Management portal</span></span>
<span data-ttu-id="7dab5-108">Доступ к журналам операций можно получить одним из двух способов.</span><span class="sxs-lookup"><span data-stu-id="7dab5-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="7dab5-109">Панель мониторинга задания Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="7dab5-109">Dashboard of hello Stream Analytics job</span></span>  
* <span data-ttu-id="7dab5-110">Службы управления Azure классическом портале hello</span><span class="sxs-lookup"><span data-stu-id="7dab5-110">Management Services in hello Azure Classic portal</span></span>  

## <a name="dashboard-of-hello-stream-analytics-job"></a><span data-ttu-id="7dab5-111">Панель мониторинга задания Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="7dab5-111">Dashboard of hello Stream Analytics job</span></span>
<span data-ttu-id="7dab5-112">Ссылка toohello соответствующие журналы задания Stream Analytics отображаются на вкладке панели мониторинга hello задания. Если щелкнуть эту ссылку, установит hello фильтры таким образом, что в нем отображаются последние журналы для этого конкретного задания.</span><span class="sxs-lookup"><span data-stu-id="7dab5-112">A link toohello corresponding logs of a Stream Analytics job is displayed on hello job’s Dashboard tab. If you click on that link, it will set hello filters in a way that it shows latest logs for that specific job.</span></span>

  ![Выбор журналов служб управления](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="7dab5-114">Службы управления</span><span class="sxs-lookup"><span data-stu-id="7dab5-114">Management Services</span></span>
<span data-ttu-id="7dab5-115">toomanually перейдите журналы операций toohello Stream Analytics и других служб Azure в классическом портале hello:</span><span class="sxs-lookup"><span data-stu-id="7dab5-115">toomanually navigate toohello Operation Logs for Stream Analytics and other services in hello Azure Classic portal:</span></span>

1. <span data-ttu-id="7dab5-116">Щелкните **служб управления** в hello [Azure классический портал](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="7dab5-116">Click on **Management Services** in hello [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="7dab5-117">Выберите **Stream Analytics** для **тип** и имя hello hello задания для **имя службы**.</span><span class="sxs-lookup"><span data-stu-id="7dab5-117">Select **Stream Analytics** for **Type** and hello name of hello job for **Service Name**.</span></span>  
   
   ![Выбор Stream Analytics](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a><span data-ttu-id="7dab5-119">Найти журналы аудита в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7dab5-119">Find audit logs in hello Azure portal</span></span>
<span data-ttu-id="7dab5-120">toofind операционные журналы для задания Stream Analytics в hello портала Azure щелкните **Обзор** , а затем выберите **журналы аудита**.</span><span class="sxs-lookup"><span data-stu-id="7dab5-120">toofind operational logs for your Stream Analytics job in hello Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Выбор Stream Analytics на портале Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="7dab5-122">Откроется колонка событий из hello последние 7 дней для всех ресурсов в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="7dab5-122">This will open a blade showing events from hello last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="7dab5-123">Можно отфильтровать такие события toosee, укажите тип или промежуток времени, щелкнув hello **фильтра** команды.</span><span class="sxs-lookup"><span data-stu-id="7dab5-123">You can filter toosee events of a specify type or time frame by clicking hello **Filter** command.</span></span>

  ![Выбор Stream Analytics на портале Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="7dab5-125">Получение подробных сведений журнала</span><span class="sxs-lookup"><span data-stu-id="7dab5-125">Get log details</span></span>
<span data-ttu-id="7dab5-126">Можно отфильтровать диапазон времени и состояние tooview hello журналы для задания.</span><span class="sxs-lookup"><span data-stu-id="7dab5-126">You can filter by Time Range and Status tooview hello logs for your job.</span></span>

<span data-ttu-id="7dab5-127">На портале управления Azure hello, нажмите кнопку hello **сведения** кнопку внизу hello tooview окно hello подробной информации о выбранном событии.</span><span class="sxs-lookup"><span data-stu-id="7dab5-127">In hello Azure Management portal, click on hello **Details** button at hello bottom of hello window tooview more details about a selected event.</span></span> 

  ![Выбор сведений](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="7dab5-129">В hello портал Azure, щелкните запись журнала toosee hello подробные события внутри него.</span><span class="sxs-lookup"><span data-stu-id="7dab5-129">In hello Azure portal, click on a log entry toosee hello detailed events inside it.</span></span>

  ![Выбор подробных сведений на портале Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="7dab5-131">После этого можно открыть hello **сведений** колонки, щелкнув событие hello.</span><span class="sxs-lookup"><span data-stu-id="7dab5-131">From there, you can open hello **Detail** blade by clicking on hello event.</span></span>

  ![Выбор подробных сведений на портале Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="7dab5-133">Отладка невыполненного задания</span><span class="sxs-lookup"><span data-stu-id="7dab5-133">Debug a failed job</span></span>
<span data-ttu-id="7dab5-134">На портале управления Azure hello щелкните значок поиска hello и введите «сбой».</span><span class="sxs-lookup"><span data-stu-id="7dab5-134">In hello Azure Management portal, click on hello Search icon and type ‘failed’.</span></span> <span data-ttu-id="7dab5-135">Это позволит получить все журналы с ошибками.</span><span class="sxs-lookup"><span data-stu-id="7dab5-135">This gives a result of all logs with failures.</span></span> 

  ![Отладка задания с ошибкой](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="7dab5-137">В hello портал Azure, можно фильтровать по уровень сообщения tooview **критическое** события.</span><span class="sxs-lookup"><span data-stu-id="7dab5-137">In hello Azure portal, you can filter by level of message tooview **Critical** events.</span></span>

  ![Отладка на портале Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="7dab5-139">Можно выбрать любой из ошибок hello и щелкнуть hello **сведения** Дополнительные сведения об ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="7dab5-139">You can select any one of hello failures, and click on hello **Details** for more information on hello error.</span></span>  <span data-ttu-id="7dab5-140">Некоторые сообщения об ошибках также предоставляют сведения о как toomitigate hello проблему.</span><span class="sxs-lookup"><span data-stu-id="7dab5-140">Some error messages also provide information about how toomitigate hello issue.</span></span> 

  ![Сведения об операции](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="7dab5-142">При необходимости toocontact [поддержки](https://azure.microsoft.com/support/options/) или предоставить авторам toohello сведения через hello [форум MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), имейте в виду hello сведения об операции, в частности hello **идентификатор корреляции**.</span><span class="sxs-lookup"><span data-stu-id="7dab5-142">In case you need toocontact [Support](https://azure.microsoft.com/support/options/) or provide information toohello team via hello [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note hello Operation Details, specifically hello **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="7dab5-143">Получение справки</span><span class="sxs-lookup"><span data-stu-id="7dab5-143">Get help</span></span>
<span data-ttu-id="7dab5-144">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="7dab5-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7dab5-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7dab5-145">Next steps</span></span>
* [<span data-ttu-id="7dab5-146">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7dab5-146">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7dab5-147">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7dab5-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7dab5-148">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7dab5-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7dab5-149">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7dab5-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7dab5-150">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7dab5-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

