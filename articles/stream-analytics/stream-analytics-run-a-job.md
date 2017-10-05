---
title: "Запуск заданий потоковой передачи в Stream Analytics | Документация Майкрософт"
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
ms.openlocfilehash: 9a3ff37a893b0f29a2ac2eda6cd50687ee779ead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-run-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="f8f75-104">Выполнение задания потоковой передачи в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f8f75-104">How to run a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="f8f75-105">После указания входных данных, запроса и выходных данных вы можете запустить задание Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="f8f75-105">When a job input, query and output have all been specified you can start the Stream Analytics job.</span></span>

<span data-ttu-id="f8f75-106">Для запуска задания:</span><span class="sxs-lookup"><span data-stu-id="f8f75-106">To start your job:</span></span>

1. <span data-ttu-id="f8f75-107">На панели мониторинга заданий классического портала Azure нажмите кнопку **Запустить** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="f8f75-107">In the Azure Classic portal, from the job dashboard, click **Start** at the bottom of the page.</span></span>
   
   ![Кнопка запуска задания](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="f8f75-109">На портале Azure нажмите кнопку **Запустить** в верхней части страницы вашего задания.</span><span class="sxs-lookup"><span data-stu-id="f8f75-109">In the Azure portal, click **Start** at the top of your job page.</span></span>
   
   ![Кнопка запуска задания на портале Azure](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="f8f75-111">Укажите значение параметра **Начало передачи выходных данных** , чтобы определить время, когда задание начнет выдавать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="f8f75-111">Specify a **Start Output** value to determine when this job will start producing output.</span></span> <span data-ttu-id="f8f75-112">Для заданий, которые не были запущены ранее, значение по умолчанию — **Время начала задания**, то есть задание начнет обработку данных немедленно.</span><span class="sxs-lookup"><span data-stu-id="f8f75-112">The default setting for jobs that have not previously been started is **Job Start Time**, which means that the job will immediately start processing data.</span></span> <span data-ttu-id="f8f75-113">Вы также можете указать **Настраиваемое** время в прошлом (для использования данных за прошедший период) или в будущем (для задержки обработки до будущего времени).</span><span class="sxs-lookup"><span data-stu-id="f8f75-113">You can also specify a **Custom** time in the past (for consuming historical data) or the future (to delay processing until a future time).</span></span> <span data-ttu-id="f8f75-114">В случаях, когда задание было запущено и остановлено ранее, становится доступен параметр **Время последней остановки** , который позволяет возобновить задание с момента последнего вывода и избежать потери данных.</span><span class="sxs-lookup"><span data-stu-id="f8f75-114">For cases when a job has been previously started and stopped, the option **Last Stopped Time** is available in order to resume the job from the last output time and avoid data loss.</span></span>  
   
   ![Время запуска задания потоковой передачи](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Время запуска задания потоковой передачи на портале Azure](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="f8f75-117">Подтвердите выбор.</span><span class="sxs-lookup"><span data-stu-id="f8f75-117">Confirm your selection.</span></span> <span data-ttu-id="f8f75-118">Состояние задания изменится на *Запуск*, а после запуска задания — на *Выполняется*.</span><span class="sxs-lookup"><span data-stu-id="f8f75-118">The job status will change to *Starting* and will shortly move to *Running* once the job has started.</span></span> <span data-ttu-id="f8f75-119">Ход выполнения операции **Запуск** можно отслеживать в **центре уведомлений**:</span><span class="sxs-lookup"><span data-stu-id="f8f75-119">You can monitor the progress of the **Start** operation in the **Notification Hub**:</span></span>
   
   ![ход выполнения задания потоковой передачи](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Ход выполнения задания потоковой передачи на портале Azure](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="f8f75-122">Получение справки</span><span class="sxs-lookup"><span data-stu-id="f8f75-122">Get help</span></span>
<span data-ttu-id="f8f75-123">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="f8f75-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8f75-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f8f75-124">Next steps</span></span>
* [<span data-ttu-id="f8f75-125">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f8f75-125">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f8f75-126">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f8f75-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f8f75-127">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f8f75-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f8f75-128">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f8f75-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f8f75-129">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f8f75-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

