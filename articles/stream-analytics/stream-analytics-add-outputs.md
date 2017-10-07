---
title: "выводит данные tooconfigure aaaHow для задания Stream Analytics | Документы Microsoft"
description: "Настройка выходных данных для заданий Stream Analytics | Сегмент схемы обучения"
keywords: "вывод данных, перемещение данных"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="6e8e2-104">Каким образом данные tooconfigure выводов для задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6e8e2-104">How tooconfigure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="6e8e2-105">Задания Azure Stream Analytics может быть подключенным tooone или несколько выходных данных, определяющие приемник подключения tooan существующих данных.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-105">Azure Stream Analytics jobs can be connected tooone or more data outputs, which define a connection tooan existing data sink.</span></span> <span data-ttu-id="6e8e2-106">Задание Stream Analytics, обрабатывает и преобразует входящие данные, поток данных событий выхода записывается выходные данные задания tooyour.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written tooyour job's output.</span></span>

<span data-ttu-id="6e8e2-107">Выходных данных Stream Analytics может быть панелей мониторинга в реальном времени используется toosource или оповещения, рабочие процессы для перемещения данных триггера или просто архив данных для пакетной обработки впоследствии.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-107">Stream Analytics data outputs can be used toosource real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="6e8e2-108">Служба Stream Analytics обеспечивает первоклассную интеграцию с различными службами Azure, которые подробно описаны здесь.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="6e8e2-109">tooadd задание Stream Analytics tooyour выходные данные:</span><span class="sxs-lookup"><span data-stu-id="6e8e2-109">tooadd an output tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="6e8e2-110">В hello [портал Azure](https://portal.azure.com)откройте задание и выберите **выходов** и нажмите кнопку **добавить** в колонке выходы hello, который отображается.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-110">In hello [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in hello Outputs blade that appears.</span></span>
   
    ![Добавление выходных данных](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="6e8e2-112">Введите понятное имя для этого выхода в hello **Псевдоним выхода** поле.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-112">Provide a friendly name for this output in hello **Output Alias** box.</span></span> <span data-ttu-id="6e8e2-113">Это имя можно использовать в запросе в задание позже на выходе toohello toorefer.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-113">This name can be used in your job's query later on toorefer toohello output.</span></span>  
   
    <span data-ttu-id="6e8e2-114">Заполните rest hello hello требуется подключение свойства tooconnect tooyour выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-114">Fill in hello rest of hello required connection properties tooconnect tooyour output.</span></span>  <span data-ttu-id="6e8e2-115">Эти поля зависят от типа выходных данных и подробно описаны здесь.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Выбор типа перемещения данных](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="6e8e2-117">В зависимости от типа hello выходные данные может потребоваться toospecify способ hello сериализации или в формате.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-117">Depending on hello output type, you may need toospecify how hello data is serialized or formatted.</span></span> <span data-ttu-id="6e8e2-118">Здесь приводятся параметры конкретного сериализации Hello для каждого выходного типа.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-118">hello specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="6e8e2-119">Заполните остальные hello hello необходимые свойства tooconnect tooyour в источнике данных соединения.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-119">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="6e8e2-120">Эти поля различаются в зависимости от типа входных данных и источник и определены в hello подробно [создать задание статьи](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="6e8e2-120">These fields vary by type of input and source type and are defined in detail in hello [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="6e8e2-121">Любое задание добавлены toohello элемента выходных данных должна существовать до запуска задания hello и события начала передачи.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-121">Any output element added toohello job, must exist before hello job is started and events start flowing.</span></span> <span data-ttu-id="6e8e2-122">Например при использовании хранилища BLOB-объектов как выходные данные задания hello не учетной записи хранилища автоматически создаст.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-122">For example, if you use Blob storage as an output, hello job will not create a storage account automatically.</span></span> <span data-ttu-id="6e8e2-123">Ему toobe, созданный пользователем hello до запуска задания ASA hello.</span><span class="sxs-lookup"><span data-stu-id="6e8e2-123">It needs toobe created by hello user before hello ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="6e8e2-124">Получение справки</span><span class="sxs-lookup"><span data-stu-id="6e8e2-124">Get help</span></span>
<span data-ttu-id="6e8e2-125">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6e8e2-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e8e2-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e8e2-126">Next steps</span></span>
* [<span data-ttu-id="6e8e2-127">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6e8e2-127">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6e8e2-128">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6e8e2-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6e8e2-129">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6e8e2-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6e8e2-130">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6e8e2-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6e8e2-131">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6e8e2-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

