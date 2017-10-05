---
title: "Панель мониторинга Power BI в Azure Stream Analytics | Документация Майкрософт"
description: "Используйте панель мониторинга Power BI для потоковой передачи, чтобы собирать данные бизнес-аналитики и анализировать большие объемы данных из задания Stream Analytics."
keywords: "панель мониторинга аналитики, панель мониторинга в режиме реального времени"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: 874d9b8701a24deb3cc21aa74cb51870155c7c9c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="fe9c1-104">Stream Analytics и Power BI. Панель мониторинга для анализа потоковой передачи данных</span><span class="sxs-lookup"><span data-stu-id="fe9c1-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="fe9c1-105">Azure Stream Analytics позволяет воспользоваться одним из лучших инструментов для бизнес-аналитики, [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-105">Azure Stream Analytics enables you to take advantage of one of the leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="fe9c1-106">В этой статье вы узнаете, как создавать средства бизнес-аналитики, отображая в Power BI выходные данные заданий Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="fe9c1-107">Вы также узнаете, как создавать информационные панели и использовать их в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-107">You also learn how to create and use a real-time dashboard.</span></span>

<span data-ttu-id="fe9c1-108">Эта статья является продолжением руководства Stream Analytics по [выявлению мошенничества в реальном времени](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-108">This article continues from the Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="fe9c1-109">Она создана на основе рабочего процесса, изложенного в этом руководстве. Кроме того, в ней добавлены выходные данные Power BI для визуализации мошеннических телефонных вызовов, обнаруженных заданием Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-109">It builds on the workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="fe9c1-110">Посмотрите [видео](https://www.youtube.com/watch?v=SGUpT-a99MA) об этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fe9c1-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fe9c1-111">Prerequisites</span></span>

<span data-ttu-id="fe9c1-112">Чтобы начать, у вас должны быть следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-112">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="fe9c1-113">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-113">An Azure account.</span></span>
* <span data-ttu-id="fe9c1-114">Учетная запись для Power BI.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-114">An account for Power BI.</span></span> <span data-ttu-id="fe9c1-115">Вы можете использовать рабочую или учебную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="fe9c1-116">Полная версия руководства по выявлению мошенничества в режиме реального времени представлена [здесь](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-116">A completed version of the [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="fe9c1-117">Руководство включает приложение, создающее вымышленные метаданные телефонных вызовов.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-117">The tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="fe9c1-118">В этом руководстве описано создание концентратора событий и отправка потоковых данных телефонных вызовов к нему.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-118">In the tutorial, you create an event hub and send the streaming phone call data to the event hub.</span></span> <span data-ttu-id="fe9c1-119">Вы напишете запрос, определяющий мошеннические вызовы (вызовы с одного и того же номера одновременно из разных мест).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-119">You write a query that detects fraudulent calls (calls from the same number at the same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="fe9c1-120">Добавление Power BI в качестве места назначения выходных данных</span><span class="sxs-lookup"><span data-stu-id="fe9c1-120">Add Power BI output</span></span>
<span data-ttu-id="fe9c1-121">В руководстве по выявлению мошенничества в реальном времени выходные данные отправлялись в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-121">In the real-time fraud detection tutorial, the output is sent to Azure Blob storage.</span></span> <span data-ttu-id="fe9c1-122">В этом разделе вы добавите выход, который отправляет сведения в Power BI.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-122">In this section, you add an output that sends information to Power BI.</span></span>

1. <span data-ttu-id="fe9c1-123">На портале Azure откройте задание Streaming Analytics, созданное ранее.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-123">In the Azure portal, open the Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="fe9c1-124">Если вы использовали рекомендуемое имя, задание называется `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-124">If you used the suggested name, the job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="fe9c1-125">В центре информационной панели задания выберите диалоговое окно **Выходные данные** и щелкните **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-125">Select the **Outputs** box in the middle of the job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="fe9c1-126">В поле **Выходной псевдоним** введите `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="fe9c1-127">Вы можете использовать другое имя.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-127">You can use a different name.</span></span> <span data-ttu-id="fe9c1-128">В таком случае запишите его, так как это имя понадобится вам позже.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-128">If you do, make a note of it, because you need the name later.</span></span> 

4. <span data-ttu-id="fe9c1-129">В поле **Приемник** выберите **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-129">Under **Sink**, select **Power BI**.</span></span>

   ![Создание выхода для Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="fe9c1-131">Щелкните **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-131">Click **Authorize**.</span></span>

    <span data-ttu-id="fe9c1-132">Откроется окно, где можно ввести учетные данные Azure (рабочей или учебной учетной записи).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Ввод учетных данных для доступа к Power BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="fe9c1-134">Введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-134">Enter your credentials.</span></span> <span data-ttu-id="fe9c1-135">Обратите внимание, что при этом вы даете заданию Stream Analytics разрешение на доступ к области Power BI.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-135">Be aware then when you enter your credentials, you're also giving permission to the Streaming Analytics job to access your Power BI area.</span></span>

7. <span data-ttu-id="fe9c1-136">Вернувшись в колонку **Новые выходные данные**, введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-136">When you're returned to the **New output** blade, enter the following information:</span></span>

    * <span data-ttu-id="fe9c1-137">**Рабочая область группы.** В клиенте Power BI выберите рабочую область, где необходимо создать набор данных.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want to create the dataset.</span></span>
    * <span data-ttu-id="fe9c1-138">**Имя набора данных.** Введите `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="fe9c1-139">Вы можете использовать другое имя.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-139">You can use a different name.</span></span> <span data-ttu-id="fe9c1-140">Если вы используете другое имя, запишите его.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="fe9c1-141">**Имя таблицы.** Введите `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="fe9c1-142">Сейчас для вывода выходных данных из заданий Stream Analytics в Power BI можно использовать только одну таблицу в наборе данных.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![Рабочая область Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="fe9c1-144">Если в Power BI есть набор данных и таблица с такими же именами, которые вы указали в задании Stream Analytics, имеющиеся имена будут перезаписаны.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-144">If Power BI has a dataset and table that have the same names as the ones that you specify in the Stream Analytics job, the existing ones are overwritten.</span></span>
    > <span data-ttu-id="fe9c1-145">Мы не рекомендуем явным образом создавать набор данных и таблицу в учетной записи Power BI.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="fe9c1-146">При запуске задания Stream Analytics они будут созданы автоматически, и задание начнет вносить выходные данные для Power BI.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-146">They are automatically created when you start your Stream Analytics job and the job starts pumping output into Power BI.</span></span> <span data-ttu-id="fe9c1-147">Если ваш запрос задания не возвращает никаких результатов, набор данных и таблица не создаются.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-147">If your job query doesn't return any results, the dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="fe9c1-148">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-148">Click **Create**.</span></span>

<span data-ttu-id="fe9c1-149">Набор данных создается со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-149">The dataset is created with the following settings:</span></span>

* <span data-ttu-id="fe9c1-150">**defaultRetentionPolicy: BasicFIFO**. Для данных используется метод FIFO, максимальное число строк — 200 тыс.;</span><span class="sxs-lookup"><span data-stu-id="fe9c1-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="fe9c1-151">**defaultMode: pushStreaming.** Набор данных поддерживает элементы потоковой передачи и традиционные визуальные объекты для отчетов</span><span class="sxs-lookup"><span data-stu-id="fe9c1-151">**defaultMode: pushStreaming**: The dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="fe9c1-152">(данные для отправки).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-152">push).</span></span>

<span data-ttu-id="fe9c1-153">Сейчас нельзя создавать наборы данных с другими флагами.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="fe9c1-154">Дополнительные сведения о наборах данных Power BI см. в справочнике по [REST API Power BI](https://msdn.microsoft.com/library/mt203562.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-154">For more information about Power BI datasets, see the [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-the-query"></a><span data-ttu-id="fe9c1-155">Написание запроса</span><span class="sxs-lookup"><span data-stu-id="fe9c1-155">Write the query</span></span>

1. <span data-ttu-id="fe9c1-156">Закройте колонку **Выходные данные** и вернитесь в колонку задания.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-156">Close the **Outputs** blade and return to the job blade.</span></span>

2. <span data-ttu-id="fe9c1-157">Щелкните поле **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-157">Click the **Query** box.</span></span> 

3. <span data-ttu-id="fe9c1-158">Введите следующий запрос.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-158">Enter the following query.</span></span> <span data-ttu-id="fe9c1-159">Этот запрос аналогичен запросу самосоединения, созданному в руководстве по обнаружению мошенничества.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-159">This query is similar to the self-join query you created in the fraud-detection tutorial.</span></span> <span data-ttu-id="fe9c1-160">Различие заключается в том, что этот запрос передает результаты в новые выходные данные, созданные вами (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-160">The difference is that this query sends results to the new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="fe9c1-161">Если вы не присвоили имя входным данным `CallStream` в руководстве по обнаружению мошенничества, замените имя `CallStream` в предложениях **FROM** и **JOIN** в запросе.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-161">If you did not name the input `CallStream` in the fraud-detection tutorial, substitute your name for `CallStream` in the **FROM** and **JOIN** clauses in the query.</span></span>

        /* Our criteria for fraud:
        Calls made from the same caller to two phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where the caller is the same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where the switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="fe9c1-162">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-162">Click **Save**.</span></span>


## <a name="test-the-query"></a><span data-ttu-id="fe9c1-163">Проверка запроса</span><span class="sxs-lookup"><span data-stu-id="fe9c1-163">Test the query</span></span>
<span data-ttu-id="fe9c1-164">Этот раздел необязательный, но мы рекомендуем ознакомиться с ним.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="fe9c1-165">Если сейчас приложение TelcoStreaming не запущено, запустите его, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-165">If the TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="fe9c1-166">Откройте командное окно.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-166">Open a command window.</span></span>
    * <span data-ttu-id="fe9c1-167">Перейдите в папку, где находятся измененные файлы telcogenerator.exe и telcodatagen.exe.config.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-167">Go to the folder where the telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="fe9c1-168">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-168">Run the following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="fe9c1-169">В колонке **Запрос** щелкните точки рядом с входными данными `CallStream`, а затем выберите **Образец данных со входа**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-169">In the **Query** blade, click the dots next to the `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="fe9c1-170">Укажите, что необходим трехминутный образец данных, и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="fe9c1-171">Дождитесь уведомления о выборке данных.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-171">Wait until you're notified that the data has been sampled.</span></span>

4. <span data-ttu-id="fe9c1-172">Щелкните **Тест** и убедитесь, что вы получаете результаты.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-the-job"></a><span data-ttu-id="fe9c1-173">Выполнение задания</span><span class="sxs-lookup"><span data-stu-id="fe9c1-173">Run the job</span></span>

1. <span data-ttu-id="fe9c1-174">Убедитесь, что приложение TelcoStreaming выполняется.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-174">Make sure that the TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="fe9c1-175">Закройте колонку **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-175">Close the **Query** blade.</span></span>

3. <span data-ttu-id="fe9c1-176">В колонке задания щелкните **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-176">In the job blade, click **Start**.</span></span>

    ![Запуск задания Stream Analytics](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="fe9c1-178">Задание Stream Analytics начинает искать мошеннические вызовы во входящем потоке.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-178">Your Streaming Analytics job starts looking for fraudulent calls in the incoming stream.</span></span> <span data-ttu-id="fe9c1-179">Задание также создает набор данных и таблицу в Power BI и начинает отправлять данные о мошеннических вызовах к ним.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-179">The job also creates the dataset and table in Power BI and starts sending data about the fraudulent calls to them.</span></span>


## <a name="create-the-dashboard-in-power-bi"></a><span data-ttu-id="fe9c1-180">Создание панели мониторинга в Power BI</span><span class="sxs-lookup"><span data-stu-id="fe9c1-180">Create the dashboard in Power BI</span></span>

1. <span data-ttu-id="fe9c1-181">Перейдите на сайт [Powerbi.com](https://powerbi.com) и войдите с помощью рабочей или учебной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-181">Go to [Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="fe9c1-182">Если результаты запроса задания Stream Analytics были выведены, вы увидите уже созданный набор данных:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-182">If the Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Набор данных потоковой передачи в Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="fe9c1-184">В рабочей области щелкните **+&nbsp;Создать**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![Кнопка "Создать" в рабочей области Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="fe9c1-186">Создайте информационную панель и назовите ее `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Создание информационной панели и присвоение ей имени в рабочей области Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="fe9c1-188">В верхней части окна щелкните **Добавить плитку**, выберите **Пользовательские данные потоковой передачи**, а затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-188">At the top of the window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Пользовательский набор данных потоковой передачи](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="fe9c1-190">В области **Your datsets** (Ваши наборы данных) выберите свой набор данных и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Ваш набор данных потоковой передачи](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="fe9c1-192">В поле **Тип визуализации** выберите **Карточка**, а затем в списке **Поля** выберите **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-192">Under **Visualization Type**, select **Card**, and then in the **Fields** list, select **fraudulentcalls**.</span></span>

    ![Сведения о визуализации для новой плитки](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="fe9c1-194">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-194">Click **Next**.</span></span>

8. <span data-ttu-id="fe9c1-195">Заполните сведения о плитке, такие как заголовок и подзаголовок.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-195">Fill in tile details like a title and subtitle.</span></span>

    ![Заголовок и подзаголовок для новой плитки](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="fe9c1-197">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-197">Click **Apply**.</span></span>

    <span data-ttu-id="fe9c1-198">Теперь у вас есть счетчик попыток совершения мошенничества.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-198">Now you have a fraud counter!</span></span>

    ![Счетчик попыток мошенничества](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="fe9c1-200">Повторите весь процесс еще раз, чтобы добавить плитку (начиная с шага 4).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-200">Follow the steps again to add a tile (starting with step 4).</span></span> <span data-ttu-id="fe9c1-201">В этот раз сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-201">This time, do the following:</span></span>

    * <span data-ttu-id="fe9c1-202">В поле **Тип визуализации** выберите **График**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-202">When you get to **Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="fe9c1-203">Добавьте ось и выберите **windowend**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="fe9c1-204">Добавьте значение и выберите **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="fe9c1-205">В списке **Отображаемый интервал времени** укажите последние 10 минут.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-205">For **Time window to display**, select the last 10 minutes.</span></span>

    ![Создание плитки графика](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="fe9c1-207">Щелкните **Далее**, добавьте заголовок и подзаголовок, а затем щелкните **Применить**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="fe9c1-208">Теперь на информационной панели Power BI есть два представления данных о мошеннических вызовах, обнаруженных в потоковой передаче данных.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-208">The Power BI dashboard now gives you two views of data about fraudulent calls as detected in the streaming data.</span></span>

    ![Готовая информационная панель Power BI, отображающая 2 плитки со сведениями о мошеннических вызовах](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="fe9c1-210">Подробнее о Power BI</span><span class="sxs-lookup"><span data-stu-id="fe9c1-210">Learn more about Power BI</span></span>

<span data-ttu-id="fe9c1-211">В этом руководстве демонстрируется, как создать некоторые визуализации для набора данных.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-211">This tutorial demonstrates how to create only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="fe9c1-212">Power BI позволяет создавать другие клиентские инструменты бизнес-аналитики для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="fe9c1-213">Дополнительные идеи см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-213">For more ideas, see the following resources:</span></span>

* <span data-ttu-id="fe9c1-214">С еще одним примером панели мониторинга Power BI можно ознакомиться в видео [Приступая к работе с Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) .</span><span class="sxs-lookup"><span data-stu-id="fe9c1-214">For another example of a Power BI dashboard, watch the [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="fe9c1-215">Дополнительные сведения о настройке вывода задания Streaming Analytics в Power BI и использовании групп Power BI см. разделе [Power BI](stream-analytics-define-outputs.md#power-bi) статьи [Выходные данные Stream Analytics: возможности хранения и анализа](stream-analytics-define-outputs.md).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-215">For more information about configuring Streaming Analytics job output to Power BI and using Power BI groups, review the [Power BI](stream-analytics-define-outputs.md#power-bi) section of the [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="fe9c1-216">Дополнительные сведения об использовании Power BI см. в статье [Панели мониторинга в службе Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="fe9c1-217">Информация об ограничениях и рекомендациях</span><span class="sxs-lookup"><span data-stu-id="fe9c1-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="fe9c1-218">Сейчас Power BI можно вызывать примерно один раз в секунду.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="fe9c1-219">Визуальные элементы потоковой передачи поддерживают пакеты размером в 15 КБ.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="fe9c1-220">При превышении этого порога визуальные элементы потоковой передачи останавливаются (но данные для отправки продолжают обрабатываться).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-220">Beyond that, streaming visuals fail (but push continues to work).</span></span> <span data-ttu-id="fe9c1-221">С учетом этого Power BI лучше всего подходит для случаев, когда Azure Stream Analytics значительно уменьшает объем передаваемых данных.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-221">Because of these limitations, Power BI lends itself most naturally to cases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="fe9c1-222">Мы рекомендуем использовать переворачивающееся или прыгающее окно, чтобы отправка данных происходила не чаще одного раза в секунду, а запрос отвечал требованиям к пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-222">We recommend using a Tumbling window or Hopping window to ensure that data push is at most one push per second, and that your query lands within the throughput requirements.</span></span>

<span data-ttu-id="fe9c1-223">Можно использовать следующую формулу для вычисления длительности окна в секундах:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-223">You can use the following equation to compute the value to give your window in seconds:</span></span>

![Выражение 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="fe9c1-225">Например:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-225">For example:</span></span>

* <span data-ttu-id="fe9c1-226">У вас есть 1000 устройств, отправляющих данные с интервалами в 1 секунду.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="fe9c1-227">Вы используете лицензию Power BI Pro, которая поддерживает 1 000 000 строк в час.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-227">You are using the Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="fe9c1-228">Вы хотите публиковать в Power BI средний объем данных на каждом устройстве.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-228">You want to publish the amount of average data per device to Power BI.</span></span>

<span data-ttu-id="fe9c1-229">Соответствующее выражение для расчета выглядит так:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-229">As a result, the equation becomes:</span></span>

![Выражение 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="fe9c1-231">При такой конфигурации можно изменить исходный запрос на следующий:</span><span class="sxs-lookup"><span data-stu-id="fe9c1-231">Given this configuration, you can change the original query to the following:</span></span>

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a><span data-ttu-id="fe9c1-232">Обновление авторизации</span><span class="sxs-lookup"><span data-stu-id="fe9c1-232">Renew authorization</span></span>
<span data-ttu-id="fe9c1-233">Если с момента создания задания или последней аутентификации пароль был изменен, необходимо повторно выполнить аутентификацию с учетной записью Power BI.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-233">If the password has changed since your job was created or last authenticated, you need to reauthenticate your Power BI account.</span></span> <span data-ttu-id="fe9c1-234">Если в клиенте Azure Active Directory (AAD) настроена многофакторная идентификация Azure, вам потребуется каждые две недели обновлять авторизацию Power BI.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need to renew Power BI authorization every two weeks.</span></span> <span data-ttu-id="fe9c1-235">Если вы этого не сделаете, возможны такие проблемы, как отсутствие выходных данных задания или `Authenticate user error` в журнале операций.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in the operation logs.</span></span>

<span data-ttu-id="fe9c1-236">Аналогично, если задание запускается после истечения срока действия маркера, возникает ошибка и происходит сбой задания.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-236">Similarly, if a job starts after the token has expired, an error occurs and the job fails.</span></span> <span data-ttu-id="fe9c1-237">Чтобы устранить эту проблему, остановите выполнение задания и перейдите к выходным данным Power BI.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-237">To resolve this issue, stop the job that's running and go to your Power BI output.</span></span> <span data-ttu-id="fe9c1-238">Чтобы избежать потери данных, щелкните ссылку **Обновить авторизацию** и перезапустите задание со **времени последней остановки**.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-238">To avoid data loss, select the **Renew authorization** link, and then restart your job from the **Last Stopped Time**.</span></span>

<span data-ttu-id="fe9c1-239">Когда вы обновите авторизацию в Power BI, в области авторизации появится оповещение зеленого цвета о том, что проблема устранена.</span><span class="sxs-lookup"><span data-stu-id="fe9c1-239">After the authorization has been refreshed with Power BI, a green alert appears in the authorization area to reflect that the issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="fe9c1-240">Получение справки</span><span class="sxs-lookup"><span data-stu-id="fe9c1-240">Get help</span></span>
<span data-ttu-id="fe9c1-241">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe9c1-242">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fe9c1-242">Next steps</span></span>
* [<span data-ttu-id="fe9c1-243">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fe9c1-243">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fe9c1-244">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fe9c1-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="fe9c1-245">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fe9c1-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="fe9c1-246">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Azure Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="fe9c1-246">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)</span></span>
* [<span data-ttu-id="fe9c1-247">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fe9c1-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
