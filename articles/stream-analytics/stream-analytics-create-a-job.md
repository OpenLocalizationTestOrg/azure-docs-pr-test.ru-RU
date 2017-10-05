---
title: "Создание задания обработки аналитики данных для Stream Analytics | Документация Майкрософт"
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
ms.openlocfilehash: 05fdf1e20efd129cdfc27e1d37bc9e124edf5dcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="b7c8a-104">Создание задания обработки аналитики данных для Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b7c8a-104">How to create a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="b7c8a-105">Важнейшим ресурсом в службе Azure Stream Analytics является задание Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-105">The top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="b7c8a-106">Оно состоит из одного или нескольких источников входных данных, запроса, определяющего преобразование данных, и одного или нескольких назначений выходных данных для записи результатов.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-106">It consists of one or more input data sources, a query expressing the data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="b7c8a-107">Вместе они позволяют пользователю обрабатывать аналитику данных для сценариев потоковой передачи данных.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-107">Together these enable the user to perform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="b7c8a-108">Чтобы начать работу со службой Stream Analytics, создайте новое задание Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-108">To start using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="b7c8a-109">Обратите внимание, пока задание не будет запущено, на стоимости услуг оно не отразится.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-109">Note this action has no billing implications until the job is started.</span></span>

1. <span data-ttu-id="b7c8a-110">Войдите на [классический портал Azure](http://manage.windowsazure.com) или [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b7c8a-110">Sign in on the online [Azure classic portal](http://manage.windowsazure.com) or the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b7c8a-111">На портале щелкните **Создать**, щелкните **Службы данных** или **Аналитика данных** (в зависимости от портала), а затем щелкните **Azure Stream Analytics** или **Stream Analytics** и выберите **Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-111">In the portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Мастер заданий обработки аналитики данных](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Создание задания обработки аналитики данных](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="b7c8a-114">Укажите требуемую конфигурацию для задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-114">Specify the desired configuration for the Stream Analytics job.</span></span>
   
   * <span data-ttu-id="b7c8a-115">В поле **Имя задания** введите имя для идентификации задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-115">In the **Job Name** box, enter a name to identify the Stream Analytics job.</span></span> <span data-ttu-id="b7c8a-116">Как только значение поля **Имя задания** будет проверено, рядом с ним отобразится зеленая галочка.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-116">When the **Job Name** is validated, a green check mark appears in the Job Name box.</span></span> <span data-ttu-id="b7c8a-117">Значение в поле **Имя задания** может включать только буквы, цифры и символ "-" и должно содержать от 3 до 63 символов.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-117">The **Job Name** may contain only alphanumeric characters and the '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="b7c8a-118">Используйте поле **Регион** или **Расположение** на портале Azure, чтобы указать географическое расположение для запуска задания.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-118">Use **Region** in the Azure portal or **Location** in the Azure portal to specify the geographic location where you want to run the job.</span></span>
   * <span data-ttu-id="b7c8a-119">Если используется портал Azure, выберите или создайте учетную запись хранения для использования в качестве **учетной записи хранения регионального мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-119">If using the Azure portal, select or create a storage account to use as the **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="b7c8a-120">Она будет использоваться для хранения данных мониторинга для всех заданий Stream Analytics, выполняемых в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-120">This storage account is used to store monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="b7c8a-121">Если вы используете портал Azure, укажите новую или существующую **группу ресурсов** для хранения связанных ресурсов для приложения.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-121">If using the Azure portal, specify a new or existing **Resource Group** to hold related resources for your application.</span></span>
4. <span data-ttu-id="b7c8a-122">Настроив параметры нового задания Stream Analytics, нажмите **Создать задание Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-122">Once the new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="b7c8a-123">Задание Stream Analytics будет создано в течение нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-123">It can take a few minutes for the Stream Analytics job to be created.</span></span> <span data-ttu-id="b7c8a-124">Для контроля состояния можно отслеживать ход выполнения в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-124">To check the status, you can monitor the progress in the Notifications hub.</span></span>
   
   ![Концентратор уведомлений для задания обработки аналитики данных](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Создание задания обработки аналитики данных на портале Azure](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="b7c8a-127">Новое задание отобразится с состоянием **Создано**.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-127">The new job will show a status of **Created**.</span></span> <span data-ttu-id="b7c8a-128">Обратите внимание, что кнопка **Запуск** неактивна.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-128">Notice that the **Start** button is disabled.</span></span> <span data-ttu-id="b7c8a-129">Перед запуском задания настройте для него источник данных, запрос и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="b7c8a-129">Configure the job input, query, and output before you start the job.</span></span>
   
   ![Состояние задания обработки аналитики данных](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Состояние задания обработки аналитики данных на портале Azure](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="b7c8a-132">Получение справки</span><span class="sxs-lookup"><span data-stu-id="b7c8a-132">Get help</span></span>
<span data-ttu-id="b7c8a-133">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="b7c8a-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7c8a-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b7c8a-134">Next steps</span></span>
* [<span data-ttu-id="b7c8a-135">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b7c8a-135">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b7c8a-136">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b7c8a-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b7c8a-137">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b7c8a-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b7c8a-138">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b7c8a-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b7c8a-139">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b7c8a-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

