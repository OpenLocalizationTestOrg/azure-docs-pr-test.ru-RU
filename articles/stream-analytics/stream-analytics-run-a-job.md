---
title: "toostart aaaHow потоковых заданий в Stream Analytics | Документы Microsoft"
description: "Выполнение задания потоковой передачи в Azure Stream Analytics | сегмент схемы обучения."
keywords: "задания потоковой передачи"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="2f2aa-104">Способ задания toorun потоковой передачи в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2f2aa-104">How toorun a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="2f2aa-105">При задании входных данных, запроса и вывод всех были указаны, можно ли запустить задание Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="2f2aa-105">When a job input, query and output have all been specified you can start hello Stream Analytics job.</span></span>

<span data-ttu-id="2f2aa-106">toostart задания:</span><span class="sxs-lookup"><span data-stu-id="2f2aa-106">toostart your job:</span></span>

1. <span data-ttu-id="2f2aa-107">На портале Azure Classic hello с панели мониторинга задания hello, щелкните **запустить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="2f2aa-107">In hello Azure Classic portal, from hello job dashboard, click **Start** at hello bottom of hello page.</span></span>
   
   ![Кнопка запуска задания](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="2f2aa-109">В hello портал Azure, щелкните **запустить** вверху hello страница «задания».</span><span class="sxs-lookup"><span data-stu-id="2f2aa-109">In hello Azure portal, click **Start** at hello top of your job page.</span></span>
   
   ![Кнопка запуска задания на портале Azure](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="2f2aa-111">Укажите **запуск вывода** toodetermine значение, если это задание начнет создавать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="2f2aa-111">Specify a **Start Output** value toodetermine when this job will start producing output.</span></span> <span data-ttu-id="2f2aa-112">Hello по умолчанию для заданий, которые ранее не были запущены — **время запуска задания**, означающее задание hello немедленно начать обработку данных.</span><span class="sxs-lookup"><span data-stu-id="2f2aa-112">hello default setting for jobs that have not previously been started is **Job Start Time**, which means that hello job will immediately start processing data.</span></span> <span data-ttu-id="2f2aa-113">Можно также указать **настраиваемый** время в hello прошлом (для использования исторических данных) или будущих hello (toodelay обработку до время в будущем).</span><span class="sxs-lookup"><span data-stu-id="2f2aa-113">You can also specify a **Custom** time in hello past (for consuming historical data) or hello future (toodelay processing until a future time).</span></span> <span data-ttu-id="2f2aa-114">Для случаев, когда задание был ранее запуска и остановки hello параметр **время последней остановки** доступна в порядке tooresume hello в задании hello время последнего вывода и избежать потери данных.</span><span class="sxs-lookup"><span data-stu-id="2f2aa-114">For cases when a job has been previously started and stopped, hello option **Last Stopped Time** is available in order tooresume hello job from hello last output time and avoid data loss.</span></span>  
   
   ![Время запуска задания потоковой передачи](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Время запуска задания потоковой передачи на портале Azure](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="2f2aa-117">Подтвердите выбор.</span><span class="sxs-lookup"><span data-stu-id="2f2aa-117">Confirm your selection.</span></span> <span data-ttu-id="2f2aa-118">состояние задания Hello изменится слишком*запуск* и скоро будут перемещены слишком*под управлением* после запуска задания hello.</span><span class="sxs-lookup"><span data-stu-id="2f2aa-118">hello job status will change too*Starting* and will shortly move too*Running* once hello job has started.</span></span> <span data-ttu-id="2f2aa-119">Можно отслеживать ход выполнения hello hello **запустить** операции в hello **концентратора уведомлений**:</span><span class="sxs-lookup"><span data-stu-id="2f2aa-119">You can monitor hello progress of hello **Start** operation in hello **Notification Hub**:</span></span>
   
   ![ход выполнения задания потоковой передачи](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Ход выполнения задания потоковой передачи на портале Azure](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="2f2aa-122">Получение справки</span><span class="sxs-lookup"><span data-stu-id="2f2aa-122">Get help</span></span>
<span data-ttu-id="2f2aa-123">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="2f2aa-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f2aa-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f2aa-124">Next steps</span></span>
* [<span data-ttu-id="2f2aa-125">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2f2aa-125">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2f2aa-126">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2f2aa-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2f2aa-127">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2f2aa-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2f2aa-128">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2f2aa-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2f2aa-129">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2f2aa-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

