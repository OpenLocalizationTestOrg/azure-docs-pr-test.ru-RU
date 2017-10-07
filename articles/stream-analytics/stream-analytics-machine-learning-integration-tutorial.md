---
title: "Интеграция Stream Analytics и машинное обучение aaaAzure | Документы Microsoft"
description: "Как toouse определяемой пользователем функции и машинного обучения в задании Stream Analytics"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="eb880-103">Выполнение анализа тональности с помощью Azure Stream Analytics и Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="eb880-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="eb880-104">В этой статье описывается настройка для простого задания Azure Stream Analytics, который интегрирует машинного обучения Azure tooquickly.</span><span class="sxs-lookup"><span data-stu-id="eb880-104">This article describes how tooquickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="eb880-105">Используйте модель машинного обучения мнений analytics из hello коллекции аналитики Cortana tooanalyze потоковой передачи текстовых данных и определения мнений hello в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="eb880-105">You use a Machine Learning sentiment analytics model from hello Cortana Intelligence Gallery tooanalyze streaming text data and determine hello sentiment score in real time.</span></span> <span data-ttu-id="eb880-106">С помощью hello Cortana аналитики Suite позволяет выполнения этой задачи, не беспокоясь о особенностей hello построение модели анализа мнений.</span><span class="sxs-lookup"><span data-stu-id="eb880-106">Using hello Cortana Intelligence Suite lets you accomplish this task without worrying about hello intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="eb880-107">Полученные знания можно применить из этой статьи tooscenarios такие:</span><span class="sxs-lookup"><span data-stu-id="eb880-107">You can apply what you learn from this article tooscenarios such as these:</span></span>

* <span data-ttu-id="eb880-108">при анализе тональности в режиме реального времени в потоковых данных Twitter;</span><span class="sxs-lookup"><span data-stu-id="eb880-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="eb880-109">при анализе записей разговоров клиента со специалистами службы поддержки;</span><span class="sxs-lookup"><span data-stu-id="eb880-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="eb880-110">при оценке комментариев на форумах, в блогах и видео;</span><span class="sxs-lookup"><span data-stu-id="eb880-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="eb880-111">а также во многих других сценариях прогнозной оценки в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="eb880-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="eb880-112">В реальном сценарии получаемому hello данных непосредственно из потока данных Twitter.</span><span class="sxs-lookup"><span data-stu-id="eb880-112">In a real-world scenario, you would get hello data directly from a Twitter data stream.</span></span> <span data-ttu-id="eb880-113">toosimplify hello учебнике мы написали его, чтобы hello задание Streaming Analytics возвращает твиты из CSV-файла в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="eb880-113">toosimplify hello tutorial, we've written it so that hello Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="eb880-114">Можно создать CSV-файл, или можно использовать пример CSV-файла, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="eb880-114">You can create your own CSV file, or you can use a sample CSV file, as shown in hello following image:</span></span>

![пример твитов в CSV-файле](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="eb880-116">Задание Streaming Analytics Hello, создаваемом применяется модель анализа мнений hello определяемой пользователем функции (UDF) на hello образца текстовых данных из хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-116">hello Streaming Analytics job that you create applies hello sentiment analytics model as a user-defined function (UDF) on hello sample text data from hello blob store.</span></span> <span data-ttu-id="eb880-117">Hello (hello результат анализа мнений hello) записываться toohello одного хранилища BLOB-объекта в другой файл CSV.</span><span class="sxs-lookup"><span data-stu-id="eb880-117">hello output (hello result of hello sentiment analysis) is written toohello same blob store in a different CSV file.</span></span> 

<span data-ttu-id="eb880-118">Hello на рисунке ниже демонстрируется этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="eb880-118">hello following figure demonstrates this configuration.</span></span> <span data-ttu-id="eb880-119">Как указано, для повышения реалистичности сценария элемент ввода для хранилища BLOB-объектов можно заменить потоковыми данными Twitter из элемента ввода концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="eb880-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="eb880-120">Кроме того, можно построить [Microsoft Power BI](https://powerbi.microsoft.com/) в режиме реального времени визуализацию статистических мнений hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of hello aggregate sentiment.</span></span>    

![Обзор интеграции машинного обучения в Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="eb880-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="eb880-122">Prerequisites</span></span>
<span data-ttu-id="eb880-123">Прежде чем начать, убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="eb880-123">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="eb880-124">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="eb880-124">An active Azure subscription.</span></span>
* <span data-ttu-id="eb880-125">CSV-файл с данными.</span><span class="sxs-lookup"><span data-stu-id="eb880-125">A CSV file with some data in it.</span></span> <span data-ttu-id="eb880-126">Вы можете скачать файл hello, показанного выше из [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), или можно создать свой собственный файл.</span><span class="sxs-lookup"><span data-stu-id="eb880-126">You can download hello file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="eb880-127">В этой статье мы предполагаем, что вы используете файл hello из GitHub.</span><span class="sxs-lookup"><span data-stu-id="eb880-127">For this article, we assume that you're using hello file from GitHub.</span></span>

<span data-ttu-id="eb880-128">На высоком уровне toocomplete hello задачи, описанные в этой статье вы hello следующие:</span><span class="sxs-lookup"><span data-stu-id="eb880-128">At a high level, toocomplete hello tasks demonstrated in this article, you do hello following:</span></span>

1. <span data-ttu-id="eb880-129">Создайте учетную запись хранилища Azure и контейнер хранилища больших двоичных объектов и отправьте контейнер toohello входной файл в формате CSV.</span><span class="sxs-lookup"><span data-stu-id="eb880-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file toohello container.</span></span>
3. <span data-ttu-id="eb880-130">Добавьте модель анализа мнений hello коллекции аналитики Cortana tooyour машинного обучения Azure рабочей и развернуть эту модель в качестве веб-службы в рабочей области машинного обучения hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-130">Add a sentiment analytics model from hello Cortana Intelligence Gallery tooyour Azure Machine Learning workspace and deploy this model as a web service in hello Machine Learning workspace.</span></span>
5. <span data-ttu-id="eb880-131">Создайте задание Stream Analytics, которое вызывает веб-службу в качестве функции спада toodetermine заказа для ввода текста hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-131">Create a Stream Analytics job that calls this web service as a function in order toodetermine sentiment for hello text input.</span></span>
6. <span data-ttu-id="eb880-132">Запустить задание Stream Analytics hello и проверьте выходные данные hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-132">Start hello Stream Analytics job and check hello output.</span></span>

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a><span data-ttu-id="eb880-133">Создать контейнер хранилища и передачи входного файла CSV hello</span><span class="sxs-lookup"><span data-stu-id="eb880-133">Create a storage container and upload hello CSV input file</span></span>
<span data-ttu-id="eb880-134">Для выполнения этого шага можно использовать любой CSV-файла, например hello один, доступный из GitHub.</span><span class="sxs-lookup"><span data-stu-id="eb880-134">For this step, you can use any CSV file, such as hello one available from GitHub.</span></span>

1. <span data-ttu-id="eb880-135">В hello портал Azure, щелкните **New** &gt; **хранения** &gt; **учетной записи хранилища**.</span><span class="sxs-lookup"><span data-stu-id="eb880-135">In hello Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![создание новой учетной записи хранения](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="eb880-137">Введите имя (`samldemo` в примере hello).</span><span class="sxs-lookup"><span data-stu-id="eb880-137">Provide a name (`samldemo` in hello example).</span></span> <span data-ttu-id="eb880-138">Имя Hello можно использовать только строчные буквы и цифры и должно быть уникальным среди Azure.</span><span class="sxs-lookup"><span data-stu-id="eb880-138">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="eb880-139">Укажите существующую группу ресурсов и расположение.</span><span class="sxs-lookup"><span data-stu-id="eb880-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="eb880-140">Для расположения, мы рекомендуем, все ресурсы hello, созданные в данном руководстве используйте hello же расположение.</span><span class="sxs-lookup"><span data-stu-id="eb880-140">For location, we recommend that all hello resources created in this tutorial use hello same location.</span></span>

    ![указание сведений об учетной записи хранения](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="eb880-142">В hello портал Azure выберите учетную запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-142">In hello Azure portal, select hello storage account.</span></span> <span data-ttu-id="eb880-143">В колонке hello учетной записи хранилища щелкните **контейнеры** и нажмите кнопку  **+ &nbsp;контейнера** toocreate хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="eb880-143">In hello storage account blade, click **Containers** and then click **+&nbsp;Container** toocreate blob storage.</span></span>

    ![создание контейнера больших двоичных объектов](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="eb880-145">Введите имя для контейнера hello (`azuresamldemoblob` в примере hello) и убедитесь, что **тип доступа** задано слишком**большого двоичного объекта**.</span><span class="sxs-lookup"><span data-stu-id="eb880-145">Provide a name for hello container (`azuresamldemoblob` in hello example) and verify that **Access type** is set too**Blob**.</span></span> <span data-ttu-id="eb880-146">Закончив, нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb880-146">When you're done, click **OK**.</span></span>

    ![указание сведений о контейнере больших двоичных объектов](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="eb880-148">В hello **контейнеры** колонки, выберите hello новый контейнер, который открывает колонку hello для этого контейнера.</span><span class="sxs-lookup"><span data-stu-id="eb880-148">In hello **Containers** blade, select hello new container, which opens hello blade for that container.</span></span>

7. <span data-ttu-id="eb880-149">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="eb880-149">Click **Upload**.</span></span>

    ![Кнопка передачи для контейнера](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="eb880-151">В hello **передачи BLOB-объекта** колонке укажите hello CSV-файла, что требуется toouse для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="eb880-151">In hello **Upload blob** blade, specify hello CSV file that you want toouse for this tutorial.</span></span> <span data-ttu-id="eb880-152">Для **больших двоичных объектов типа**выберите **блочного BLOB-объекта** и набор hello блока размером too4 МБ, что вполне достаточно для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="eb880-152">For **Blob type**, select **Block blob** and set hello block size too4 MB, which is sufficient for this tutorial.</span></span>

    ![отправка файла большого двоичного объекта](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="eb880-154">Нажмите кнопку hello **отправить** кнопку в нижней части hello колонка hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-154">Click hello **Upload** button at hello bottom of hello blade.</span></span>

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a><span data-ttu-id="eb880-155">Добавить модель анализа мнений hello из коллекции аналитики Cortana hello</span><span class="sxs-lookup"><span data-stu-id="eb880-155">Add hello sentiment analytics model from hello Cortana Intelligence Gallery</span></span>

<span data-ttu-id="eb880-156">Теперь, когда данные образца hello в большом двоичном объекте, можно включить модели анализа мнений hello в коллекции Cortana аналитики.</span><span class="sxs-lookup"><span data-stu-id="eb880-156">Now that hello sample data is in a blob, you can enable hello sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="eb880-157">Go toohello [мнений прогнозной модели analytics](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) страницы в коллекции Cortana аналитики hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-157">Go toohello [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in hello Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="eb880-158">Щелкните **Открыть в Studio**.</span><span class="sxs-lookup"><span data-stu-id="eb880-158">Click **Open in Studio**.</span></span>  
   
   ![Машинное обучение и Stream Analytics, открытие Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="eb880-160">Войдите в рабочую область toohello toogo.</span><span class="sxs-lookup"><span data-stu-id="eb880-160">Sign in toogo toohello workspace.</span></span> <span data-ttu-id="eb880-161">Выберите расположение.</span><span class="sxs-lookup"><span data-stu-id="eb880-161">Select a location.</span></span>

4. <span data-ttu-id="eb880-162">Нажмите кнопку **запуска** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="eb880-162">Click **Run** at hello bottom of hello page.</span></span> <span data-ttu-id="eb880-163">Здравствуйте выполнения процесса, который занимает около минуты.</span><span class="sxs-lookup"><span data-stu-id="eb880-163">hello process runs, which takes about a minute.</span></span>

   ![выполнение эксперимента в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="eb880-165">После успешного выполнения процесса hello выберите **развертывание веб-службы** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="eb880-165">After hello process has run successfully, select **Deploy Web Service** at hello bottom of hello page.</span></span>

   ![развертывание эксперимента как веб-службы в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="eb880-167">toovalidate, hello модель analytics — Готово toouse мнений щелкните hello **тест** кнопки.</span><span class="sxs-lookup"><span data-stu-id="eb880-167">toovalidate that hello sentiment analytics model is ready toouse, click hello **Test** button.</span></span> <span data-ttu-id="eb880-168">Введите текст "Мне нравится Майкрософт".</span><span class="sxs-lookup"><span data-stu-id="eb880-168">Provide text input such as "I love Microsoft".</span></span> 

   ![проверка эксперимента в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="eb880-170">Если hello тест работает, появится примерно toohello результат, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="eb880-170">If hello test works, you see a result similar toohello following example:</span></span>

   ![результаты проверки в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="eb880-172">В hello **приложения** столбец, щелкните hello **Excel 2010 или более ранних книги** toodownload ссылку книги Excel.</span><span class="sxs-lookup"><span data-stu-id="eb880-172">In hello **Apps** column, click hello **Excel 2010 or earlier workbook** link toodownload an Excel workbook.</span></span> <span data-ttu-id="eb880-173">Hello книга содержит ключ hello API и URL-адрес hello, необходимо более поздней версии tooset задание Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-173">hello workbook contains hello an API key and hello URL that you need later tooset up hello Stream Analytics job.</span></span>

    ![Машинное обучение и Stream Analytics, сводка](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a><span data-ttu-id="eb880-175">Создать задание Stream Analytics, которое использует модель машинного обучения hello</span><span class="sxs-lookup"><span data-stu-id="eb880-175">Create a Stream Analytics job that uses hello Machine Learning model</span></span>

<span data-ttu-id="eb880-176">Теперь можно создать задание Stream Analytics, считывающий твиты образец hello из hello CSV-файла в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="eb880-176">You can now create a Stream Analytics job that reads hello sample tweets from hello CSV file in blob storage.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="eb880-177">Создание задания hello</span><span class="sxs-lookup"><span data-stu-id="eb880-177">Create hello job</span></span>

1. <span data-ttu-id="eb880-178">Go toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eb880-178">Go toohello [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="eb880-179">Щелкните **Создать** > **"Интернет вещей"** > **Задание Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="eb880-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Azure портала путь для получения tooa новое задание Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="eb880-181">Имя задания hello `azure-sa-ml-demo`укажите подписки, укажите существующую группу ресурсов или создайте новый и выберите расположение hello для задания hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-181">Name hello job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select hello location for hello job.</span></span>

   ![указание параметров для нового задания Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a><span data-ttu-id="eb880-183">Настройка задания ввода hello</span><span class="sxs-lookup"><span data-stu-id="eb880-183">Configure hello job input</span></span>
<span data-ttu-id="eb880-184">Задание Hello получает входные данные из CSV-файла hello, что был загружен ранее tooblob хранилища.</span><span class="sxs-lookup"><span data-stu-id="eb880-184">hello job gets its input from hello CSV file that you uploaded earlier tooblob storage.</span></span>

1. <span data-ttu-id="eb880-185">После задания hello будет создана, в разделе **топологии задания** в колонке задания hello щелкните hello **входов** поле.</span><span class="sxs-lookup"><span data-stu-id="eb880-185">After hello job has been created, under **Job Topology** in hello job blade, click hello **Inputs** box.</span></span>  
   
   ![Поле "Входные данные" в колонке задания Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="eb880-187">В hello **входов** колонка, щелкните **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="eb880-187">In hello **Inputs** blade, click **+ Add**.</span></span>

   ![Кнопка для добавления задания Stream Analytics ввода toohello «добавить»](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="eb880-189">Заполните hello **вводимые** колонка со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="eb880-189">Fill out hello **New input** blade with these values:</span></span>

    * <span data-ttu-id="eb880-190">**Входной псевдоним**: hello используйте имя `datainput`.</span><span class="sxs-lookup"><span data-stu-id="eb880-190">**Input alias**: Use hello name `datainput`.</span></span>
    * <span data-ttu-id="eb880-191">**Тип источника**: выберите **Поток данных**.</span><span class="sxs-lookup"><span data-stu-id="eb880-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="eb880-192">**Источник**: выберите **Хранилище BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="eb880-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="eb880-193">**Параметры импорта**: выберите **Использовать хранилище BLOB-объектов из текущей подписки**.</span><span class="sxs-lookup"><span data-stu-id="eb880-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="eb880-194">**Учетная запись хранения**:</span><span class="sxs-lookup"><span data-stu-id="eb880-194">**Storage account**.</span></span> <span data-ttu-id="eb880-195">Выберите учетную запись хранения hello, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="eb880-195">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="eb880-196">**Контейнер**:</span><span class="sxs-lookup"><span data-stu-id="eb880-196">**Container**.</span></span> <span data-ttu-id="eb880-197">Выберите hello контейнера, созданную ранее (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="eb880-197">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="eb880-198">**Формат сериализации событий**:</span><span class="sxs-lookup"><span data-stu-id="eb880-198">**Event serialization format**.</span></span> <span data-ttu-id="eb880-199">выберите **CSV**.</span><span class="sxs-lookup"><span data-stu-id="eb880-199">Select **CSV**.</span></span>

    ![Параметры для новых входных данных задания](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="eb880-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="eb880-201">Click **Create**.</span></span>

### <a name="configure-hello-job-output"></a><span data-ttu-id="eb880-202">Настройка выходных данных задания hello</span><span class="sxs-lookup"><span data-stu-id="eb880-202">Configure hello job output</span></span>
<span data-ttu-id="eb880-203">Hello задания отправляет результаты toohello же хранилище, где он получает входные больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="eb880-203">hello job sends results toohello same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="eb880-204">В разделе **топологии задания** в колонке задания hello щелкните hello **выходов** поле.</span><span class="sxs-lookup"><span data-stu-id="eb880-204">Under **Job Topology** in hello job blade, click hello **Outputs** box.</span></span>  
  
   ![Создание новых выходных данных для задания Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="eb880-206">В hello **выходов** колонка, щелкните **+ добавить**и затем добавить выход с псевдонимом hello `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="eb880-206">In hello **Outputs** blade, click **+ Add**, and then add an output with hello alias `datamloutput`.</span></span> 

3. <span data-ttu-id="eb880-207">Для поля **Приемник** выберите **Хранилище BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="eb880-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="eb880-208">Затем заполните остальные hello hello выходных параметров с помощью hello одинаковые значения, которые используются для хранения больших двоичных объектов hello для входа:</span><span class="sxs-lookup"><span data-stu-id="eb880-208">Then fill in hello rest of hello output settings using hello same values that you used for hello blob storage for input:</span></span>

    * <span data-ttu-id="eb880-209">**Учетная запись хранения**:</span><span class="sxs-lookup"><span data-stu-id="eb880-209">**Storage account**.</span></span> <span data-ttu-id="eb880-210">Выберите учетную запись хранения hello, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="eb880-210">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="eb880-211">**Контейнер**:</span><span class="sxs-lookup"><span data-stu-id="eb880-211">**Container**.</span></span> <span data-ttu-id="eb880-212">Выберите hello контейнера, созданную ранее (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="eb880-212">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="eb880-213">**Формат сериализации событий**:</span><span class="sxs-lookup"><span data-stu-id="eb880-213">**Event serialization format**.</span></span> <span data-ttu-id="eb880-214">выберите **CSV**.</span><span class="sxs-lookup"><span data-stu-id="eb880-214">Select **CSV**.</span></span>

   ![Параметры для новых выходных данных задания](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="eb880-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="eb880-216">Click **Create**.</span></span>   


### <a name="add-hello-machine-learning-function"></a><span data-ttu-id="eb880-217">Добавление функции машинного обучения hello</span><span class="sxs-lookup"><span data-stu-id="eb880-217">Add hello Machine Learning function</span></span> 
<span data-ttu-id="eb880-218">Ранее вы опубликовали tooa веб-службы машинного обучения модели.</span><span class="sxs-lookup"><span data-stu-id="eb880-218">Earlier you published a Machine Learning model tooa web service.</span></span> <span data-ttu-id="eb880-219">В нашем сценарии анализа потока выполнения задания hello отправляет твит каждого образца из входного toohello hello веб-службы для анализа мнений.</span><span class="sxs-lookup"><span data-stu-id="eb880-219">In our scenario, when hello Stream Analysis job runs, it sends each sample tweet from hello input toohello web service for sentiment analysis.</span></span> <span data-ttu-id="eb880-220">веб-службы машинного обучения Hello возвращает мнений (`positive`, `neutral`, или `negative`) и вероятность твит hello, положительным.</span><span class="sxs-lookup"><span data-stu-id="eb880-220">hello Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of hello tweet being positive.</span></span> 

<span data-ttu-id="eb880-221">В этом разделе учебника hello определить функцию в задание анализа потока hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-221">In this section of hello tutorial, you define a function in hello Stream Analysis job.</span></span> <span data-ttu-id="eb880-222">функции Hello можно вызванный toosend твит toohello веб-службы и вернуть ответ hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-222">hello function can be invoked toosend a tweet toohello web service and get hello response back.</span></span> 

1. <span data-ttu-id="eb880-223">Убедитесь, что у вас есть hello ключ веб-службе URL-адрес и API-интерфейса, загруженный ранее в книге Excel hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-223">Make sure you have hello web service URL and API key that you downloaded earlier in hello Excel workbook.</span></span>

2. <span data-ttu-id="eb880-224">Возвращает колонку Обзор toohello задания.</span><span class="sxs-lookup"><span data-stu-id="eb880-224">Return toohello job overview blade.</span></span>

3. <span data-ttu-id="eb880-225">В разделе **Параметры** выберите **Функции**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="eb880-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Добавить задание Stream Analytics toohello функции](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="eb880-227">Введите `sentiment` как hello функцией псевдоним и заполнить rest hello колонка hello, используя следующие значения:</span><span class="sxs-lookup"><span data-stu-id="eb880-227">Enter `sentiment` as hello function alias and fill out hello rest of hello blade using these values:</span></span>

    * <span data-ttu-id="eb880-228">**Тип функции**: выберите **Машинное обучение Azure**.</span><span class="sxs-lookup"><span data-stu-id="eb880-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="eb880-229">**Метод импорта**: выберите **Импортировать из другой подписки**.</span><span class="sxs-lookup"><span data-stu-id="eb880-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="eb880-230">Это дает возможность tooenter hello и URL-адрес и ключ.</span><span class="sxs-lookup"><span data-stu-id="eb880-230">This gives you a chance tooenter hello URL and key.</span></span>
    * <span data-ttu-id="eb880-231">**URL-адрес**: вставить в hello URL веб-службы.</span><span class="sxs-lookup"><span data-stu-id="eb880-231">**URL**: Paste in hello web service URL.</span></span>
    * <span data-ttu-id="eb880-232">**Ключ**: вставить в ключе hello API.</span><span class="sxs-lookup"><span data-stu-id="eb880-232">**Key**: Paste in hello API key.</span></span>
  
    ![Параметры для добавления задания Stream Analytics toohello функции машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="eb880-234">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="eb880-234">Click **Create**.</span></span>

### <a name="create-a-query-tootransform-hello-data"></a><span data-ttu-id="eb880-235">Создание запроса данных hello tootransform</span><span class="sxs-lookup"><span data-stu-id="eb880-235">Create a query tootransform hello data</span></span>

<span data-ttu-id="eb880-236">Stream Analytics использует вход hello tooexamine декларативный, основанный на SQL запроса и его обработки.</span><span class="sxs-lookup"><span data-stu-id="eb880-236">Stream Analytics uses a declarative, SQL-based query tooexamine hello input and process it.</span></span> <span data-ttu-id="eb880-237">В этом разделе создайте запрос, который считывает каждый твит из входных данных, а затем вызывает анализ мнений tooperform функции машинного обучения hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-237">In this section, you create a query that reads each tweet from input and then invokes hello Machine Learning function tooperform sentiment analysis.</span></span> <span data-ttu-id="eb880-238">запрос Hello затем отправляет результат toohello hello выходных данных определенного (хранилище больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="eb880-238">hello query then sends hello result toohello output that you defined (blob storage).</span></span>

1. <span data-ttu-id="eb880-239">Возвращает колонку Обзор toohello задания.</span><span class="sxs-lookup"><span data-stu-id="eb880-239">Return toohello job overview blade.</span></span>

2.  <span data-ttu-id="eb880-240">В разделе **топологии задания**, нажмите кнопку hello **запроса** поле.</span><span class="sxs-lookup"><span data-stu-id="eb880-240">Under **Job Topology**, click hello **Query** box.</span></span>

    ![Создание запроса для задания Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="eb880-242">Введите приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="eb880-242">Enter hello following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="eb880-243">Hello запрос вызывает функцию hello, созданную ранее (`sentiment`) в анализ мнений tooperform заказа для каждого твит во входном файле hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-243">hello query invokes hello function you created earlier (`sentiment`) in order tooperform sentiment analysis on each tweet in hello input.</span></span> 

4. <span data-ttu-id="eb880-244">Нажмите кнопку **Сохранить** toosave hello запроса.</span><span class="sxs-lookup"><span data-stu-id="eb880-244">Click **Save** toosave hello query.</span></span>


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a><span data-ttu-id="eb880-245">Запустить задание Stream Analytics hello и проверьте выходные данные hello</span><span class="sxs-lookup"><span data-stu-id="eb880-245">Start hello Stream Analytics job and check hello output</span></span>

<span data-ttu-id="eb880-246">Теперь вы можете запустить задание Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-246">You can now start hello Stream Analytics job.</span></span>

### <a name="start-hello-job"></a><span data-ttu-id="eb880-247">Запустить задание hello</span><span class="sxs-lookup"><span data-stu-id="eb880-247">Start hello job</span></span>
1. <span data-ttu-id="eb880-248">Возвращает колонку Обзор toohello задания.</span><span class="sxs-lookup"><span data-stu-id="eb880-248">Return toohello job overview blade.</span></span>

2. <span data-ttu-id="eb880-249">Нажмите кнопку **запустить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-249">Click **Start** at hello top of hello blade.</span></span>

    ![Создание запроса для задания Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="eb880-251">В hello **запуска задания**выберите **настраиваемый**и выберите один день предыдущего toowhen загруженный хранилища tooblob файл CSV hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-251">In hello **Start job**, select **Custom**, and then select one day prior toowhen you uploaded hello CSV file tooblob storage.</span></span> <span data-ttu-id="eb880-252">После этого нажмите кнопку **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="eb880-252">When you're done, click **Start**.</span></span>  


### <a name="check-hello-output"></a><span data-ttu-id="eb880-253">Проверьте выходные данные hello</span><span class="sxs-lookup"><span data-stu-id="eb880-253">Check hello output</span></span>
1. <span data-ttu-id="eb880-254">Let hello задания, выполняемого на несколько минут, пока не увидите действия в hello **мониторинг** поле.</span><span class="sxs-lookup"><span data-stu-id="eb880-254">Let hello job run for a few minutes until you see activity in hello **Monitoring** box.</span></span> 

2. <span data-ttu-id="eb880-255">Если у вас есть средство, обычно используемое содержимое hello tooexamine хранилища больших двоичных объектов, использовать этот инструмент tooexamine hello `azuresamldemoblob` контейнера.</span><span class="sxs-lookup"><span data-stu-id="eb880-255">If you have a tool that you normally use tooexamine hello contents of blob storage, use that tool tooexamine hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="eb880-256">Кроме того hello шагов в hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="eb880-256">Alternatively, do hello following steps in hello Azure portal:</span></span>

    1. <span data-ttu-id="eb880-257">На портале hello найти hello `samldemo` хранилища учетную запись, а в пределах учетной записи hello, найти hello `azuresamldemoblob` контейнера.</span><span class="sxs-lookup"><span data-stu-id="eb880-257">In hello portal, find hello `samldemo` storage account, and within hello account, find hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="eb880-258">Вы видите два файла в контейнере hello: hello файл, содержащий твиты образец hello и CSV-файла, созданные задания Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-258">You see two files in hello container: hello file that contains hello sample tweets and a CSV file generated by hello Stream Analytics job.</span></span>
    2. <span data-ttu-id="eb880-259">Щелкните правой кнопкой мыши файл создан hello, а затем выберите **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="eb880-259">Right-click hello generated file and then select **Download**.</span></span> 

   ![Скачивание выходных данных задания в виде CSV-файла из хранилища BLOB-объектов](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="eb880-261">Привет открыть созданный CSV-файла.</span><span class="sxs-lookup"><span data-stu-id="eb880-261">Open hello generated CSV file.</span></span> <span data-ttu-id="eb880-262">Можно наблюдать нечто похожее на следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="eb880-262">You see something like hello following example:</span></span>  
   
   ![Машинное обучение и Stream Analytics, просмотр CSV-файла](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="eb880-264">Просмотр метрик</span><span class="sxs-lookup"><span data-stu-id="eb880-264">View metrics</span></span>
<span data-ttu-id="eb880-265">Вы можете также просматривать метрики, связанные с функциями Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="eb880-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="eb880-266">Следующая функция метрик Hello отображаются в hello **мониторинг** поле в колонке hello задания:</span><span class="sxs-lookup"><span data-stu-id="eb880-266">hello following function-related metrics are displayed in hello **Monitoring** box in hello job blade:</span></span>

* <span data-ttu-id="eb880-267">**Функции запросов** указывает hello число запросов, отправленных tooa веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="eb880-267">**Function Requests** indicates hello number of requests sent tooa Machine Learning web service.</span></span>  
* <span data-ttu-id="eb880-268">**Функция событий** указывает номер события в запросе hello hello.</span><span class="sxs-lookup"><span data-stu-id="eb880-268">**Function Events** indicates hello number of events in hello request.</span></span> <span data-ttu-id="eb880-269">По умолчанию каждый запрос tooa веб-службы машинного обучения содержит до too1 000 событий.</span><span class="sxs-lookup"><span data-stu-id="eb880-269">By default, each request tooa Machine Learning web service contains up too1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="eb880-270">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb880-270">Next steps</span></span>

* [<span data-ttu-id="eb880-271">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eb880-271">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="eb880-272">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eb880-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="eb880-273">Интеграция машинного обучения в Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eb880-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="eb880-274">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eb880-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



