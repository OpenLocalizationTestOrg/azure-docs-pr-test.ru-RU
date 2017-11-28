---
title: "панели мониторинга aaaPower BI в Azure Stream Analytics | Документы Microsoft"
description: "Использовать в режиме реального времени потоковой передачи Power BI панель мониторинга toogather бизнес-аналитики и анализа больших объемов данных из задания Stream Analytics."
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
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="17ffd-104">Stream Analytics и Power BI. Панель мониторинга для анализа потоковой передачи данных</span><span class="sxs-lookup"><span data-stu-id="17ffd-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="17ffd-105">Azure Stream Analytics дает преимущество tootake одного hello начальные средства бизнес-аналитики, [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="17ffd-105">Azure Stream Analytics enables you tootake advantage of one of hello leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="17ffd-106">В этой статье вы узнаете, как создавать средства бизнес-аналитики, отображая в Power BI выходные данные заданий Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="17ffd-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="17ffd-107">Вы также узнаете, как toocreate и использовать панели мониторинга в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="17ffd-107">You also learn how toocreate and use a real-time dashboard.</span></span>

<span data-ttu-id="17ffd-108">В этой статье продолжается с hello Stream Analytics [в режиме реального времени мошенничества](stream-analytics-real-time-fraud-detection.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="17ffd-108">This article continues from hello Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="17ffd-109">Он основан на hello рабочий процесс, созданный в этом учебнике и добавляет Power BI, выходные данные, чтобы вы можете визуализировать мошеннические телефонных звонков, которые определяются задание Streaming Analytics.</span><span class="sxs-lookup"><span data-stu-id="17ffd-109">It builds on hello workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="17ffd-110">Посмотрите [видео](https://www.youtube.com/watch?v=SGUpT-a99MA) об этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="17ffd-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="17ffd-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="17ffd-111">Prerequisites</span></span>

<span data-ttu-id="17ffd-112">Прежде чем начать, убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="17ffd-112">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="17ffd-113">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="17ffd-113">An Azure account.</span></span>
* <span data-ttu-id="17ffd-114">Учетная запись для Power BI.</span><span class="sxs-lookup"><span data-stu-id="17ffd-114">An account for Power BI.</span></span> <span data-ttu-id="17ffd-115">Вы можете использовать рабочую или учебную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="17ffd-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="17ffd-116">Полную версию hello [в режиме реального времени мошенничества](stream-analytics-real-time-fraud-detection.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="17ffd-116">A completed version of hello [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="17ffd-117">Hello учебник содержит приложение, создающее вымышленной телефону метаданных.</span><span class="sxs-lookup"><span data-stu-id="17ffd-117">hello tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="17ffd-118">В учебнике hello Создание концентратора событий и отправки hello потоковой передачи концентратора событий toohello данных телефонный звонок.</span><span class="sxs-lookup"><span data-stu-id="17ffd-118">In hello tutorial, you create an event hub and send hello streaming phone call data toohello event hub.</span></span> <span data-ttu-id="17ffd-119">При написании запроса, определяющую мошеннические вызовов (вызовы из hello одно и тоже число в hello одновременную в разных местах).</span><span class="sxs-lookup"><span data-stu-id="17ffd-119">You write a query that detects fraudulent calls (calls from hello same number at hello same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="17ffd-120">Добавление Power BI в качестве места назначения выходных данных</span><span class="sxs-lookup"><span data-stu-id="17ffd-120">Add Power BI output</span></span>
<span data-ttu-id="17ffd-121">В учебнике обнаружения мошенничества в режиме реального времени hello hello вывод направляется tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="17ffd-121">In hello real-time fraud detection tutorial, hello output is sent tooAzure Blob storage.</span></span> <span data-ttu-id="17ffd-122">В этом разделе добавьте вывода, который отправляет сведения tooPower бизнес-Аналитики.</span><span class="sxs-lookup"><span data-stu-id="17ffd-122">In this section, you add an output that sends information tooPower BI.</span></span>

1. <span data-ttu-id="17ffd-123">Hello портал Azure откройте задание Streaming Analytics hello, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="17ffd-123">In hello Azure portal, open hello Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="17ffd-124">При использовании предлагаемое имя hello hello задание называется `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="17ffd-124">If you used hello suggested name, hello job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="17ffd-125">Выберите hello **выходов** в середине hello панель мониторинга задания hello и затем выберите **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-125">Select hello **Outputs** box in hello middle of hello job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="17ffd-126">В поле **Выходной псевдоним** введите `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="17ffd-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="17ffd-127">Вы можете использовать другое имя.</span><span class="sxs-lookup"><span data-stu-id="17ffd-127">You can use a different name.</span></span> <span data-ttu-id="17ffd-128">В противном случае запишите его, поскольку его нужно имя hello.</span><span class="sxs-lookup"><span data-stu-id="17ffd-128">If you do, make a note of it, because you need hello name later.</span></span> 

4. <span data-ttu-id="17ffd-129">В поле **Приемник** выберите **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-129">Under **Sink**, select **Power BI**.</span></span>

   ![Создание выхода для Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="17ffd-131">Щелкните **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-131">Click **Authorize**.</span></span>

    <span data-ttu-id="17ffd-132">Откроется окно, где можно ввести учетные данные Azure (рабочей или учебной учетной записи).</span><span class="sxs-lookup"><span data-stu-id="17ffd-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Введите учетные данные для доступа к tooPower бизнес-Аналитики](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="17ffd-134">Введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="17ffd-134">Enter your credentials.</span></span> <span data-ttu-id="17ffd-135">Имейте в виду то при вводе учетных данных, можно также предоставить разрешение toohello Streaming Analytics задания tooaccess местных Power BI.</span><span class="sxs-lookup"><span data-stu-id="17ffd-135">Be aware then when you enter your credentials, you're also giving permission toohello Streaming Analytics job tooaccess your Power BI area.</span></span>

7. <span data-ttu-id="17ffd-136">Когда вы будете перенаправлены toohello **новый Выход** колонке введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="17ffd-136">When you're returned toohello **New output** blade, enter hello following information:</span></span>

    * <span data-ttu-id="17ffd-137">**Группы рабочей**: Выбор рабочей области в клиенте Power BI, где требуется набор данных toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="17ffd-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want toocreate hello dataset.</span></span>
    * <span data-ttu-id="17ffd-138">**Имя набора данных.** Введите `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="17ffd-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="17ffd-139">Вы можете использовать другое имя.</span><span class="sxs-lookup"><span data-stu-id="17ffd-139">You can use a different name.</span></span> <span data-ttu-id="17ffd-140">Если вы используете другое имя, запишите его.</span><span class="sxs-lookup"><span data-stu-id="17ffd-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="17ffd-141">**Имя таблицы.** Введите `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="17ffd-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="17ffd-142">Сейчас для вывода выходных данных из заданий Stream Analytics в Power BI можно использовать только одну таблицу в наборе данных.</span><span class="sxs-lookup"><span data-stu-id="17ffd-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![Рабочая область Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="17ffd-144">Если Power BI содержит источники данных и таблицы, для которых hello совпадают с именами hello те, которые указываются в задании Stream Analytics hello, перезаписываются существующих hello.</span><span class="sxs-lookup"><span data-stu-id="17ffd-144">If Power BI has a dataset and table that have hello same names as hello ones that you specify in hello Stream Analytics job, hello existing ones are overwritten.</span></span>
    > <span data-ttu-id="17ffd-145">Мы не рекомендуем явным образом создавать набор данных и таблицу в учетной записи Power BI.</span><span class="sxs-lookup"><span data-stu-id="17ffd-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="17ffd-146">Они создаются автоматически, если запустить задание Stream Analytics и hello заданий начинает инициализируемого выходные данные в Power BI.</span><span class="sxs-lookup"><span data-stu-id="17ffd-146">They are automatically created when you start your Stream Analytics job and hello job starts pumping output into Power BI.</span></span> <span data-ttu-id="17ffd-147">Если задание запрос не возвращает никаких результатов, hello набора данных и таблицы не создаются.</span><span class="sxs-lookup"><span data-stu-id="17ffd-147">If your job query doesn't return any results, hello dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="17ffd-148">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-148">Click **Create**.</span></span>

<span data-ttu-id="17ffd-149">Hello набор данных создается с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="17ffd-149">hello dataset is created with hello following settings:</span></span>

* <span data-ttu-id="17ffd-150">**defaultRetentionPolicy: BasicFIFO**. Для данных используется метод FIFO, максимальное число строк — 200 тыс.;</span><span class="sxs-lookup"><span data-stu-id="17ffd-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="17ffd-151">**defaultMode: pushStreaming**: hello поддерживает набор данных потоковой передачи плитки и традиционные визуальных элементов на основе отчетов (так)</span><span class="sxs-lookup"><span data-stu-id="17ffd-151">**defaultMode: pushStreaming**: hello dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="17ffd-152">(данные для отправки).</span><span class="sxs-lookup"><span data-stu-id="17ffd-152">push).</span></span>

<span data-ttu-id="17ffd-153">Сейчас нельзя создавать наборы данных с другими флагами.</span><span class="sxs-lookup"><span data-stu-id="17ffd-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="17ffd-154">Дополнительные сведения о наборах данных Power BI см. в разделе hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) ссылки.</span><span class="sxs-lookup"><span data-stu-id="17ffd-154">For more information about Power BI datasets, see hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-hello-query"></a><span data-ttu-id="17ffd-155">Написать запрос hello</span><span class="sxs-lookup"><span data-stu-id="17ffd-155">Write hello query</span></span>

1. <span data-ttu-id="17ffd-156">Закрыть hello **выходов** колонки и возврата toohello задания колонку.</span><span class="sxs-lookup"><span data-stu-id="17ffd-156">Close hello **Outputs** blade and return toohello job blade.</span></span>

2. <span data-ttu-id="17ffd-157">Нажмите кнопку hello **запроса** поле.</span><span class="sxs-lookup"><span data-stu-id="17ffd-157">Click hello **Query** box.</span></span> 

3. <span data-ttu-id="17ffd-158">Введите приветствия при следующем запросе.</span><span class="sxs-lookup"><span data-stu-id="17ffd-158">Enter hello following query.</span></span> <span data-ttu-id="17ffd-159">Этот запрос является подобный toohello самосоединение запрос, созданный в учебнике мошенничества hello.</span><span class="sxs-lookup"><span data-stu-id="17ffd-159">This query is similar toohello self-join query you created in hello fraud-detection tutorial.</span></span> <span data-ttu-id="17ffd-160">Hello отличается отправляет новый toohello результаты вывода был создан этот запрос (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="17ffd-160">hello difference is that this query sends results toohello new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="17ffd-161">Если не было имя входных данных hello `CallStream` в учебнике мошенничества hello, замените на имя `CallStream` в hello **FROM** и **JOIN** предложений в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="17ffd-161">If you did not name hello input `CallStream` in hello fraud-detection tutorial, substitute your name for `CallStream` in hello **FROM** and **JOIN** clauses in hello query.</span></span>

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="17ffd-162">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-162">Click **Save**.</span></span>


## <a name="test-hello-query"></a><span data-ttu-id="17ffd-163">Проверка запроса hello</span><span class="sxs-lookup"><span data-stu-id="17ffd-163">Test hello query</span></span>
<span data-ttu-id="17ffd-164">Этот раздел необязательный, но мы рекомендуем ознакомиться с ним.</span><span class="sxs-lookup"><span data-stu-id="17ffd-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="17ffd-165">Если приложение hello TelcoStreaming еще не запущен, запустите ее, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="17ffd-165">If hello TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="17ffd-166">Откройте командное окно.</span><span class="sxs-lookup"><span data-stu-id="17ffd-166">Open a command window.</span></span>
    * <span data-ttu-id="17ffd-167">Последовательно выберите toohello папку, где hello telcogenerator.exe и telcodatagen.exe.config измененные файлы.</span><span class="sxs-lookup"><span data-stu-id="17ffd-167">Go toohello folder where hello telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="17ffd-168">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="17ffd-168">Run hello following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="17ffd-169">В hello **запроса** колонке нажмите кнопку Далее toohello точек hello `CallStream` входных данных, а затем выберите **выборку данных из входных данных**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-169">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="17ffd-170">Укажите, что необходим трехминутный образец данных, и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="17ffd-171">Подождите, пока выполняется уведомление, что hello данные выборок значений.</span><span class="sxs-lookup"><span data-stu-id="17ffd-171">Wait until you're notified that hello data has been sampled.</span></span>

4. <span data-ttu-id="17ffd-172">Щелкните **Тест** и убедитесь, что вы получаете результаты.</span><span class="sxs-lookup"><span data-stu-id="17ffd-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-hello-job"></a><span data-ttu-id="17ffd-173">Запустить задание hello</span><span class="sxs-lookup"><span data-stu-id="17ffd-173">Run hello job</span></span>

1. <span data-ttu-id="17ffd-174">Убедитесь, что выполнение этого приложения hello TelcoStreaming.</span><span class="sxs-lookup"><span data-stu-id="17ffd-174">Make sure that hello TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="17ffd-175">Закрыть hello **запроса** колонку.</span><span class="sxs-lookup"><span data-stu-id="17ffd-175">Close hello **Query** blade.</span></span>

3. <span data-ttu-id="17ffd-176">В колонке hello задания, нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-176">In hello job blade, click **Start**.</span></span>

    ![Запустить задание Stream Analytics hello](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="17ffd-178">Ваше задание Streaming Analytics запускает поиск мошеннические вызовы в hello входящего потока.</span><span class="sxs-lookup"><span data-stu-id="17ffd-178">Your Streaming Analytics job starts looking for fraudulent calls in hello incoming stream.</span></span> <span data-ttu-id="17ffd-179">Задание Hello также создает hello набора данных и таблицы в Power BI и начинает отправлять данные об toothem мошеннические вызовы hello.</span><span class="sxs-lookup"><span data-stu-id="17ffd-179">hello job also creates hello dataset and table in Power BI and starts sending data about hello fraudulent calls toothem.</span></span>


## <a name="create-hello-dashboard-in-power-bi"></a><span data-ttu-id="17ffd-180">Создание панели мониторинга hello в Power BI</span><span class="sxs-lookup"><span data-stu-id="17ffd-180">Create hello dashboard in Power BI</span></span>

1. <span data-ttu-id="17ffd-181">Go слишком[Powerbi.com](https://powerbi.com) и выполните вход с рабочей или школьной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="17ffd-181">Go too[Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="17ffd-182">Если результат запроса задания Stream Analytics hello, отобразятся уже создан набор данных:</span><span class="sxs-lookup"><span data-stu-id="17ffd-182">If hello Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Набор данных потоковой передачи в Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="17ffd-184">В рабочей области щелкните **+&nbsp;Создать**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![кнопки "Создать" Hello в рабочей области Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="17ffd-186">Создайте информационную панель и назовите ее `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="17ffd-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Создание информационной панели и присвоение ей имени в рабочей области Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="17ffd-188">Hello верхней части окна hello, нажмите кнопку **добавить плитку**выберите **ПОЛЬЗОВАТЕЛЬСКИЕ данные потоковой ПЕРЕДАЧИ**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-188">At hello top of hello window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Пользовательский набор данных потоковой передачи](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="17ffd-190">В области **Your datsets** (Ваши наборы данных) выберите свой набор данных и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Ваш набор данных потоковой передачи](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="17ffd-192">В разделе **тип визуализации**выберите **карты**, а затем в hello **поля** выберите **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-192">Under **Visualization Type**, select **Card**, and then in hello **Fields** list, select **fraudulentcalls**.</span></span>

    ![Сведения о визуализации для новой плитки](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="17ffd-194">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-194">Click **Next**.</span></span>

8. <span data-ttu-id="17ffd-195">Заполните сведения о плитке, такие как заголовок и подзаголовок.</span><span class="sxs-lookup"><span data-stu-id="17ffd-195">Fill in tile details like a title and subtitle.</span></span>

    ![Заголовок и подзаголовок для новой плитки](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="17ffd-197">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-197">Click **Apply**.</span></span>

    <span data-ttu-id="17ffd-198">Теперь у вас есть счетчик попыток совершения мошенничества.</span><span class="sxs-lookup"><span data-stu-id="17ffd-198">Now you have a fraud counter!</span></span>

    ![Счетчик попыток мошенничества](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="17ffd-200">Hello выполните шаги tooadd плитки (начиная с шага 4) еще раз.</span><span class="sxs-lookup"><span data-stu-id="17ffd-200">Follow hello steps again tooadd a tile (starting with step 4).</span></span> <span data-ttu-id="17ffd-201">На этот раз hello следующие:</span><span class="sxs-lookup"><span data-stu-id="17ffd-201">This time, do hello following:</span></span>

    * <span data-ttu-id="17ffd-202">При получении слишком**тип визуализации**выберите **график**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-202">When you get too**Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="17ffd-203">Добавьте ось и выберите **windowend**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="17ffd-204">Добавьте значение и выберите **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="17ffd-205">Для **toodisplay окно времени**выберите hello последние 10 минут.</span><span class="sxs-lookup"><span data-stu-id="17ffd-205">For **Time window toodisplay**, select hello last 10 minutes.</span></span>

    ![Создание плитки графика](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="17ffd-207">Щелкните **Далее**, добавьте заголовок и подзаголовок, а затем щелкните **Применить**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="17ffd-208">панели мониторинга Power BI Hello теперь содержатся два представления данных о мошенничестве вызовы обнаруженного в hello потоковой передачи данных.</span><span class="sxs-lookup"><span data-stu-id="17ffd-208">hello Power BI dashboard now gives you two views of data about fraudulent calls as detected in hello streaming data.</span></span>

    ![Готовая информационная панель Power BI, отображающая 2 плитки со сведениями о мошеннических вызовах](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="17ffd-210">Подробнее о Power BI</span><span class="sxs-lookup"><span data-stu-id="17ffd-210">Learn more about Power BI</span></span>

<span data-ttu-id="17ffd-211">В этом учебнике показано как toocreate несколько видов визуализации для набора данных.</span><span class="sxs-lookup"><span data-stu-id="17ffd-211">This tutorial demonstrates how toocreate only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="17ffd-212">Power BI позволяет создавать другие клиентские инструменты бизнес-аналитики для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="17ffd-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="17ffd-213">Дополнительные идеи см. следующие ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="17ffd-213">For more ideas, see hello following resources:</span></span>

* <span data-ttu-id="17ffd-214">Другой пример панели мониторинга Power BI, посмотрите hello [Приступая к работе с Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) видео.</span><span class="sxs-lookup"><span data-stu-id="17ffd-214">For another example of a Power BI dashboard, watch hello [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="17ffd-215">Дополнительные сведения о настройке Streaming Analytics задания tooPower выходных данных бизнес-Аналитики и использование групп Power BI, проверьте hello [Power BI](stream-analytics-define-outputs.md#power-bi) раздел hello [выводит Stream Analytics](stream-analytics-define-outputs.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="17ffd-215">For more information about configuring Streaming Analytics job output tooPower BI and using Power BI groups, review hello [Power BI](stream-analytics-define-outputs.md#power-bi) section of hello [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="17ffd-216">Дополнительные сведения об использовании Power BI см. в статье [Панели мониторинга в службе Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="17ffd-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="17ffd-217">Информация об ограничениях и рекомендациях</span><span class="sxs-lookup"><span data-stu-id="17ffd-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="17ffd-218">Сейчас Power BI можно вызывать примерно один раз в секунду.</span><span class="sxs-lookup"><span data-stu-id="17ffd-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="17ffd-219">Визуальные элементы потоковой передачи поддерживают пакеты размером в 15 КБ.</span><span class="sxs-lookup"><span data-stu-id="17ffd-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="17ffd-220">Кроме этого Сбой потоковой передачи визуальные элементы (но по-прежнему toowork push).</span><span class="sxs-lookup"><span data-stu-id="17ffd-220">Beyond that, streaming visuals fail (but push continues toowork).</span></span> <span data-ttu-id="17ffd-221">Из-за этих ограничений Power BI пригоден наиболее естественным образом toocases, когда Azure Stream Analytics осуществляет сокращение загрузки значительного объема данных.</span><span class="sxs-lookup"><span data-stu-id="17ffd-221">Because of these limitations, Power BI lends itself most naturally toocases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="17ffd-222">Мы рекомендуем использовать «переворачивающееся» окно или tooensure окна «прыгающие» окна, принудительная отправка данных в журнал не чаще одного push в секунду и запрос попадает в hello пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="17ffd-222">We recommend using a Tumbling window or Hopping window tooensure that data push is at most one push per second, and that your query lands within hello throughput requirements.</span></span>

<span data-ttu-id="17ffd-223">Можно использовать окна Следующая формула toocompute hello значение toogive hello в секундах:</span><span class="sxs-lookup"><span data-stu-id="17ffd-223">You can use hello following equation toocompute hello value toogive your window in seconds:</span></span>

![Выражение 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="17ffd-225">Например:</span><span class="sxs-lookup"><span data-stu-id="17ffd-225">For example:</span></span>

* <span data-ttu-id="17ffd-226">У вас есть 1000 устройств, отправляющих данные с интервалами в 1 секунду.</span><span class="sxs-lookup"><span data-stu-id="17ffd-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="17ffd-227">Вы используете hello Power BI Pro номера SKU, поддерживающий 1 000 000 строк в час.</span><span class="sxs-lookup"><span data-stu-id="17ffd-227">You are using hello Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="17ffd-228">Вы хотите toopublish hello объем среднего значения данных на устройстве tooPower бизнес-Аналитики.</span><span class="sxs-lookup"><span data-stu-id="17ffd-228">You want toopublish hello amount of average data per device tooPower BI.</span></span>

<span data-ttu-id="17ffd-229">В результате hello уравнение выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="17ffd-229">As a result, hello equation becomes:</span></span>

![Выражение 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="17ffd-231">При такой конфигурации можно изменить hello исходного запроса toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="17ffd-231">Given this configuration, you can change hello original query toohello following:</span></span>

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


### <a name="renew-authorization"></a><span data-ttu-id="17ffd-232">Обновление авторизации</span><span class="sxs-lookup"><span data-stu-id="17ffd-232">Renew authorization</span></span>
<span data-ttu-id="17ffd-233">Если hello пароль изменен с момента создания задания или последний раз проверку подлинности, то необходимо tooreauthenticate учетную запись Power BI.</span><span class="sxs-lookup"><span data-stu-id="17ffd-233">If hello password has changed since your job was created or last authenticated, you need tooreauthenticate your Power BI account.</span></span> <span data-ttu-id="17ffd-234">Если Azure многофакторная проверка подлинности настроена в клиенте Azure Active Directory (Azure AD), необходимо также авторизации Power BI toorenew каждые две недели.</span><span class="sxs-lookup"><span data-stu-id="17ffd-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need toorenew Power BI authorization every two weeks.</span></span> <span data-ttu-id="17ffd-235">Если не будет обновлен, можно просмотреть проблемы, например об отсутствии выходные данные задания или `Authenticate user error` в журналах операций hello.</span><span class="sxs-lookup"><span data-stu-id="17ffd-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in hello operation logs.</span></span>

<span data-ttu-id="17ffd-236">Аналогично Если задание запускается после истечения срока действия токена hello, возникает ошибка и hello задание завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="17ffd-236">Similarly, if a job starts after hello token has expired, an error occurs and hello job fails.</span></span> <span data-ttu-id="17ffd-237">tooresolve эту проблему, остановить задание hello, на котором выполняется и перейти tooyour, выходные данные Power BI.</span><span class="sxs-lookup"><span data-stu-id="17ffd-237">tooresolve this issue, stop hello job that's running and go tooyour Power BI output.</span></span> <span data-ttu-id="17ffd-238">потеря данных tooavoid, выберите hello **авторизацию** связь, а затем перезапустите задание из hello **время последней остановки**.</span><span class="sxs-lookup"><span data-stu-id="17ffd-238">tooavoid data loss, select hello **Renew authorization** link, and then restart your job from hello **Last Stopped Time**.</span></span>

<span data-ttu-id="17ffd-239">После обновления hello авторизации с помощью Power BI появится зеленый предупреждение в области tooreflect hello авторизации hello проблема была разрешена.</span><span class="sxs-lookup"><span data-stu-id="17ffd-239">After hello authorization has been refreshed with Power BI, a green alert appears in hello authorization area tooreflect that hello issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="17ffd-240">Получение справки</span><span class="sxs-lookup"><span data-stu-id="17ffd-240">Get help</span></span>
<span data-ttu-id="17ffd-241">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="17ffd-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="17ffd-242">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17ffd-242">Next steps</span></span>
* [<span data-ttu-id="17ffd-243">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="17ffd-243">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="17ffd-244">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="17ffd-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="17ffd-245">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="17ffd-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="17ffd-246">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Azure Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="17ffd-246">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)</span></span>
* [<span data-ttu-id="17ffd-247">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="17ffd-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
