---
title: "aaaHow toocreate задание обработки анализа данных для Stream Analytics | Документы Microsoft"
description: "Создание задания обработки аналитики данных для Stream Analytics | Сегмент схемы обучения."
keywords: "обработка аналитики данных"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="7c7a2-104">Как toocreate обработки данных аналитики задания для Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7c7a2-104">How toocreate a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="7c7a2-105">ресурс верхнего уровня Hello в Azure Stream Analytics — задании Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-105">hello top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="7c7a2-106">Он состоит из одного или нескольких входных источников данных, преобразования данных hello выражения запроса и один или несколько целевых объектов выходных данных, результаты будут записаны.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-106">It consists of one or more input data sources, a query expressing hello data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="7c7a2-107">Вместе с их помощью hello пользователя tooperform данных аналитики сценариев обработки для потоковой передачи данных.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-107">Together these enable hello user tooperform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="7c7a2-108">toostart с помощью Stream Analytics, сначала необходимо создать новое задание Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-108">toostart using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="7c7a2-109">Обратите внимание, что это действие имеет не финансовые последствия, пока не будет запущено задание hello.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-109">Note this action has no billing implications until hello job is started.</span></span>

1. <span data-ttu-id="7c7a2-110">Войдите в систему на hello сети [классический портал Azure](http://manage.windowsazure.com) или hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7c7a2-110">Sign in on hello online [Azure classic portal](http://manage.windowsazure.com) or hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7c7a2-111">На портале hello: **щелкните новый**, нажмите кнопку **Data Services** или **анализа данных** в зависимости от того, портал и нажмите кнопку **Azure Stream Analytics** или **потоковой аналитики** и затем **быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-111">In hello portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Мастер заданий обработки аналитики данных](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Создание задания обработки аналитики данных](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="7c7a2-114">Укажите требуемую конфигурацию hello для задания Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-114">Specify hello desired configuration for hello Stream Analytics job.</span></span>
   
   * <span data-ttu-id="7c7a2-115">В hello **имя задания** введите имя задания Stream Analytics hello tooidentify.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-115">In hello **Job Name** box, enter a name tooidentify hello Stream Analytics job.</span></span> <span data-ttu-id="7c7a2-116">Здравствуйте, когда **имя задания** проверяется, отображается зеленый флажок в поле Имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-116">When hello **Job Name** is validated, a green check mark appears in hello Job Name box.</span></span> <span data-ttu-id="7c7a2-117">Hello **имя задания** могут содержать только буквенно-цифровые символы и hello '-' символов и должно содержать от 3 до 63 символов.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-117">hello **Job Name** may contain only alphanumeric characters and hello '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="7c7a2-118">Используйте **область** в hello портал Azure или **расположение** в hello Azure портала toospecify hello место задания hello toorun географическое расположение.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-118">Use **Region** in hello Azure portal or **Location** in hello Azure portal toospecify hello geographic location where you want toorun hello job.</span></span>
   * <span data-ttu-id="7c7a2-119">Если с помощью hello портал Azure, выберите или создайте toouse учетной записи хранилища как hello **мониторинг учетная запись хранения регионального**.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-119">If using hello Azure portal, select or create a storage account toouse as hello **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="7c7a2-120">Эта учетная запись хранения — используется toostore наблюдение за данными для все задания Stream Analytics, выполняемые в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-120">This storage account is used toostore monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="7c7a2-121">Если с помощью hello портал Azure, укажите новую или существующую **группы ресурсов** toohold связанные ресурсы для приложения.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-121">If using hello Azure portal, specify a new or existing **Resource Group** toohold related resources for your application.</span></span>
4. <span data-ttu-id="7c7a2-122">Настроив hello новые параметры задания Stream Analytics, щелкните **создать задание Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-122">Once hello new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="7c7a2-123">Он может занять несколько минут для hello Stream Analytics задания toobe создан.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-123">It can take a few minutes for hello Stream Analytics job toobe created.</span></span> <span data-ttu-id="7c7a2-124">состояние toocheck hello, позволяющее наблюдать за hello в концентраторе уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-124">toocheck hello status, you can monitor hello progress in hello Notifications hub.</span></span>
   
   ![Концентратор уведомлений для задания обработки аналитики данных](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Создание задания обработки аналитики данных на портале Azure](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="7c7a2-127">Hello новое задание будет отображаться статус **Created**.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-127">hello new job will show a status of **Created**.</span></span> <span data-ttu-id="7c7a2-128">Обратите внимание, что hello **запустить** кнопка отключена.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-128">Notice that hello **Start** button is disabled.</span></span> <span data-ttu-id="7c7a2-129">Перед началом работы hello, настройте входных данных задания hello, запроса и выход.</span><span class="sxs-lookup"><span data-stu-id="7c7a2-129">Configure hello job input, query, and output before you start hello job.</span></span>
   
   ![Состояние задания обработки аналитики данных](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Состояние задания обработки аналитики данных на портале Azure](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="7c7a2-132">Получение справки</span><span class="sxs-lookup"><span data-stu-id="7c7a2-132">Get help</span></span>
<span data-ttu-id="7c7a2-133">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c7a2-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c7a2-134">Next steps</span></span>
* [<span data-ttu-id="7c7a2-135">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7c7a2-135">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7c7a2-136">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7c7a2-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7c7a2-137">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7c7a2-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7c7a2-138">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7c7a2-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7c7a2-139">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7c7a2-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

