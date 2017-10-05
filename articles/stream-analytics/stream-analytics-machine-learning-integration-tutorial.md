---
title: "Интеграция Azure Stream Analytics и Машинного обучения Azure | Документация Майкрософт"
description: "Использование определяемой пользователем функции и машинного обучения в задании Stream Analytics."
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
ms.openlocfilehash: 023033d5479fcf0e2dff168b6604431eef283d3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="fb7e0-103">Выполнение анализа тональности с помощью Azure Stream Analytics и Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="fb7e0-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="fb7e0-104">В этой статье описывается, как быстро настроить простое задание Azure Stream Analytics, интегрированное с Машинным обучением Azure.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-104">This article describes how to quickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="fb7e0-105">Вы используете модель машинного обучения для анализа тональности из коллекции Cortana Intelligence для анализа потока текстовых данных, а также определения оценки тональности в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-105">You use a Machine Learning sentiment analytics model from the Cortana Intelligence Gallery to analyze streaming text data and determine the sentiment score in real time.</span></span> <span data-ttu-id="fb7e0-106">С помощью Cortana Intelligence Suite вы сможете выполнить эту задачу, не вникая в особенности создания модели анализа тональности.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-106">Using the Cortana Intelligence Suite lets you accomplish this task without worrying about the intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="fb7e0-107">Вы сможете применить сведения, полученные в рамках этой статьи, в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-107">You can apply what you learn from this article to scenarios such as these:</span></span>

* <span data-ttu-id="fb7e0-108">при анализе тональности в режиме реального времени в потоковых данных Twitter;</span><span class="sxs-lookup"><span data-stu-id="fb7e0-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="fb7e0-109">при анализе записей разговоров клиента со специалистами службы поддержки;</span><span class="sxs-lookup"><span data-stu-id="fb7e0-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="fb7e0-110">при оценке комментариев на форумах, в блогах и видео;</span><span class="sxs-lookup"><span data-stu-id="fb7e0-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="fb7e0-111">а также во многих других сценариях прогнозной оценки в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="fb7e0-112">В реальном сценарии вы получите данные напрямую из потока данных Twitter.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-112">In a real-world scenario, you would get the data directly from a Twitter data stream.</span></span> <span data-ttu-id="fb7e0-113">Чтобы упростить работу с этим руководством, мы описали сценарий, когда задание Streaming Analytics получает твиты из CSV-файла в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-113">To simplify the tutorial, we've written it so that the Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="fb7e0-114">Вы можете создать собственный CSV-файл или использовать пример этого файла, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-114">You can create your own CSV file, or you can use a sample CSV file, as shown in the following image:</span></span>

![пример твитов в CSV-файле](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="fb7e0-116">Задание Streaming Analytics, которое вы создаете, применяет модель анализа тональности как определяемую пользователем функцию к образцу текстовых данных из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-116">The Streaming Analytics job that you create applies the sentiment analytics model as a user-defined function (UDF) on the sample text data from the blob store.</span></span> <span data-ttu-id="fb7e0-117">Выходные данные (результат анализа тональности) записываются в то же хранилище BLOB-объектов в другом CSV-файле.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-117">The output (the result of the sentiment analysis) is written to the same blob store in a different CSV file.</span></span> 

<span data-ttu-id="fb7e0-118">На следующем рисунке показана эта конфигурация.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-118">The following figure demonstrates this configuration.</span></span> <span data-ttu-id="fb7e0-119">Как указано, для повышения реалистичности сценария элемент ввода для хранилища BLOB-объектов можно заменить потоковыми данными Twitter из элемента ввода концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="fb7e0-120">Кроме того, можно создать визуализацию совокупной тональности [Microsoft Power BI](https://powerbi.microsoft.com/) в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of the aggregate sentiment.</span></span>    

![Обзор интеграции машинного обучения в Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="fb7e0-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fb7e0-122">Prerequisites</span></span>
<span data-ttu-id="fb7e0-123">Чтобы начать, у вас должны быть следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-123">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="fb7e0-124">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-124">An active Azure subscription.</span></span>
* <span data-ttu-id="fb7e0-125">CSV-файл с данными.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-125">A CSV file with some data in it.</span></span> <span data-ttu-id="fb7e0-126">Файл, показанный ранее, можно скачать с сайта [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv). Вы можете также создать собственный файл.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-126">You can download the file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="fb7e0-127">В этой статьей предполагается использование файла из GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-127">For this article, we assume that you're using the file from GitHub.</span></span>

<span data-ttu-id="fb7e0-128">В общих чертах, чтобы выполнить задачи, описанные в этой статье, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-128">At a high level, to complete the tasks demonstrated in this article, you do the following:</span></span>

1. <span data-ttu-id="fb7e0-129">Создайте учетную запись хранения Azure и контейнер хранилища BLOB-объектов, а затем передайте в контейнер входной файл в формате CSV.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file to the container.</span></span>
3. <span data-ttu-id="fb7e0-130">Добавьте модель анализа тональности из коллекции Cortana Intelligence в рабочую область Машинного обучения Azure и разверните в ней эту модель как веб-службу.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-130">Add a sentiment analytics model from the Cortana Intelligence Gallery to your Azure Machine Learning workspace and deploy this model as a web service in the Machine Learning workspace.</span></span>
5. <span data-ttu-id="fb7e0-131">Создайте задание Stream Analytics, вызывающее эту веб-службу как функцию, для определения тональности входного текста.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-131">Create a Stream Analytics job that calls this web service as a function in order to determine sentiment for the text input.</span></span>
6. <span data-ttu-id="fb7e0-132">Запустите задание Stream Analytics и просмотрите выходные данные.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-132">Start the Stream Analytics job and check the output.</span></span>

## <a name="create-a-storage-container-and-upload-the-csv-input-file"></a><span data-ttu-id="fb7e0-133">Создание контейнера хранилища и передача входного CSV-файла</span><span class="sxs-lookup"><span data-stu-id="fb7e0-133">Create a storage container and upload the CSV input file</span></span>
<span data-ttu-id="fb7e0-134">Для этого шага можно использовать любой CSV-файл, например файл, доступный на GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-134">For this step, you can use any CSV file, such as the one available from GitHub.</span></span>

1. <span data-ttu-id="fb7e0-135">На портале Azure щелкните **Создать** &gt; **Хранилище** &gt; **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-135">In the Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![создание новой учетной записи хранения](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="fb7e0-137">Введите имя (в примере используется `samldemo`).</span><span class="sxs-lookup"><span data-stu-id="fb7e0-137">Provide a name (`samldemo` in the example).</span></span> <span data-ttu-id="fb7e0-138">Имя должно быть уникальным в Azure и может содержать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-138">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="fb7e0-139">Укажите существующую группу ресурсов и расположение.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="fb7e0-140">Мы рекомендуем, чтобы все ресурсы, созданные в рамках этого руководства, использовали одно расположение.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-140">For location, we recommend that all the resources created in this tutorial use the same location.</span></span>

    ![указание сведений об учетной записи хранения](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="fb7e0-142">На портале Azure выберите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-142">In the Azure portal, select the storage account.</span></span> <span data-ttu-id="fb7e0-143">В колонке учетной записи хранения щелкните **Контейнеры**, а затем щелкните **+&nbsp;Контейнер**, чтобы создать хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-143">In the storage account blade, click **Containers** and then click **+&nbsp;Container** to create blob storage.</span></span>

    ![создание контейнера больших двоичных объектов](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="fb7e0-145">Укажите имя для контейнера (в примере это `azuresamldemoblob`) и выберите для **типа доступа** значение **BLOB-объект**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-145">Provide a name for the container (`azuresamldemoblob` in the example) and verify that **Access type** is set to **Blob**.</span></span> <span data-ttu-id="fb7e0-146">Закончив, нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-146">When you're done, click **OK**.</span></span>

    ![указание сведений о контейнере больших двоичных объектов](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="fb7e0-148">В колонке **Контейнеры** выберите новый контейнер, чтобы открыть его колонку.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-148">In the **Containers** blade, select the new container, which opens the blade for that container.</span></span>

7. <span data-ttu-id="fb7e0-149">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-149">Click **Upload**.</span></span>

    ![Кнопка передачи для контейнера](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="fb7e0-151">В колонке **Отправить BLOB-объект** укажите CSV-файл, который вы хотите использовать для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-151">In the **Upload blob** blade, specify the CSV file that you want to use for this tutorial.</span></span> <span data-ttu-id="fb7e0-152">В поле **Тип BLOB-объекта** выберите **Блочный BLOB-объект**, а для размера блока задайте значение 4 МБ (для работы с этим руководством это оптимальный вариант).</span><span class="sxs-lookup"><span data-stu-id="fb7e0-152">For **Blob type**, select **Block blob** and set the block size to 4 MB, which is sufficient for this tutorial.</span></span>

    ![отправка файла большого двоичного объекта](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="fb7e0-154">Нажмите кнопку **Передать** в нижней области колонки.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-154">Click the **Upload** button at the bottom of the blade.</span></span>

## <a name="add-the-sentiment-analytics-model-from-the-cortana-intelligence-gallery"></a><span data-ttu-id="fb7e0-155">Добавление модели анализа тональности из коллекции Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="fb7e0-155">Add the sentiment analytics model from the Cortana Intelligence Gallery</span></span>

<span data-ttu-id="fb7e0-156">Теперь, когда образец данных находится в большом двоичном объекте, вы можете включить модель анализа тональности в коллекции Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-156">Now that the sample data is in a blob, you can enable the sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="fb7e0-157">Перейдите на страницу [модели прогнозной аналитики тональности](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) в коллекции Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-157">Go to the [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in the Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="fb7e0-158">Щелкните **Открыть в Studio**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-158">Click **Open in Studio**.</span></span>  
   
   ![Машинное обучение и Stream Analytics, открытие Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="fb7e0-160">Выполните вход, чтобы перейти в рабочую область.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-160">Sign in to go to the workspace.</span></span> <span data-ttu-id="fb7e0-161">Выберите расположение.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-161">Select a location.</span></span>

4. <span data-ttu-id="fb7e0-162">В нижней части страницы щелкните **Run** (Выполнить).</span><span class="sxs-lookup"><span data-stu-id="fb7e0-162">Click **Run** at the bottom of the page.</span></span> <span data-ttu-id="fb7e0-163">Процесс выполнения занимает около минуты.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-163">The process runs, which takes about a minute.</span></span>

   ![выполнение эксперимента в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="fb7e0-165">После успешного выполнения процесса выберите кнопку **Deploy Web Service** (Развернуть веб-службу) в нижней области страницы.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-165">After the process has run successfully, select **Deploy Web Service** at the bottom of the page.</span></span>

   ![развертывание эксперимента как веб-службы в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="fb7e0-167">Чтобы проверить, что модель анализа тональности готова к использованию, нажмите кнопку **Проверка**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-167">To validate that the sentiment analytics model is ready to use, click the **Test** button.</span></span> <span data-ttu-id="fb7e0-168">Введите текст "Мне нравится Майкрософт".</span><span class="sxs-lookup"><span data-stu-id="fb7e0-168">Provide text input such as "I love Microsoft".</span></span> 

   ![проверка эксперимента в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="fb7e0-170">Если проверка завершится успешно, вы увидите результат, аналогичный следующему:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-170">If the test works, you see a result similar to the following example:</span></span>

   ![результаты проверки в Студии машинного обучения](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="fb7e0-172">В столбце **Приложения** щелкните ссылку **Excel 2010 or earlier workbook** (Книга Excel 2010 или более ранней версии), чтобы скачать книгу Excel.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-172">In the **Apps** column, click the **Excel 2010 or earlier workbook** link to download an Excel workbook.</span></span> <span data-ttu-id="fb7e0-173">Книга содержит ключ API и URL-адрес, которые понадобятся вам позже для настройки задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-173">The workbook contains the an API key and the URL that you need later to set up the Stream Analytics job.</span></span>

    ![Машинное обучение и Stream Analytics, сводка](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-the-machine-learning-model"></a><span data-ttu-id="fb7e0-175">Создание задания Stream Analytics, использующего модель машинного обучения</span><span class="sxs-lookup"><span data-stu-id="fb7e0-175">Create a Stream Analytics job that uses the Machine Learning model</span></span>

<span data-ttu-id="fb7e0-176">Теперь вы можете создать задание Stream Analytics, считывающее пример твитов из CSV-файла в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-176">You can now create a Stream Analytics job that reads the sample tweets from the CSV file in blob storage.</span></span> 

### <a name="create-the-job"></a><span data-ttu-id="fb7e0-177">Создание задания</span><span class="sxs-lookup"><span data-stu-id="fb7e0-177">Create the job</span></span>

1. <span data-ttu-id="fb7e0-178">Перейдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb7e0-178">Go to the [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="fb7e0-179">Щелкните **Создать** > **"Интернет вещей"** > **Задание Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Путь на портале Azure для перехода к новому заданию Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="fb7e0-181">Назовите задание `azure-sa-ml-demo`, укажите подписку, существующую группу ресурсов (или создайте новую), а затем выберите расположение для задания.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-181">Name the job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select the location for the job.</span></span>

   ![указание параметров для нового задания Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-the-job-input"></a><span data-ttu-id="fb7e0-183">Настройка входных данных для задания</span><span class="sxs-lookup"><span data-stu-id="fb7e0-183">Configure the job input</span></span>
<span data-ttu-id="fb7e0-184">Задание получает входные данные из CSV-файла, переданного ранее в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-184">The job gets its input from the CSV file that you uploaded earlier to blob storage.</span></span>

1. <span data-ttu-id="fb7e0-185">После создания задания в разделе **Топология задания** в колонке задания щелкните поле **Входные данные**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-185">After the job has been created, under **Job Topology** in the job blade, click the **Inputs** box.</span></span>  
   
   ![Поле "Входные данные" в колонке задания Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="fb7e0-187">В колонке **Входные данные** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-187">In the **Inputs** blade, click **+ Add**.</span></span>

   ![Кнопка "Добавить" для добавления входных данных в задание Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="fb7e0-189">Заполните колонку **Новые входные данные** следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-189">Fill out the **New input** blade with these values:</span></span>

    * <span data-ttu-id="fb7e0-190">**Входной псевдоним**: используйте имя `datainput`.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-190">**Input alias**: Use the name `datainput`.</span></span>
    * <span data-ttu-id="fb7e0-191">**Тип источника**: выберите **Поток данных**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="fb7e0-192">**Источник**: выберите **Хранилище BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="fb7e0-193">**Параметры импорта**: выберите **Использовать хранилище BLOB-объектов из текущей подписки**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="fb7e0-194">**Учетная запись хранения**:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-194">**Storage account**.</span></span> <span data-ttu-id="fb7e0-195">выберите учетную запись хранения, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-195">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="fb7e0-196">**Контейнер**:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-196">**Container**.</span></span> <span data-ttu-id="fb7e0-197">выберите созданный ранее контейнер (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="fb7e0-197">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="fb7e0-198">**Формат сериализации событий**:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-198">**Event serialization format**.</span></span> <span data-ttu-id="fb7e0-199">выберите **CSV**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-199">Select **CSV**.</span></span>

    ![Параметры для новых входных данных задания](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="fb7e0-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-201">Click **Create**.</span></span>

### <a name="configure-the-job-output"></a><span data-ttu-id="fb7e0-202">Настройка выходных данных для задания</span><span class="sxs-lookup"><span data-stu-id="fb7e0-202">Configure the job output</span></span>
<span data-ttu-id="fb7e0-203">Задание передает результаты в то же хранилище BLOB-объектов, в котором получает входные данные.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-203">The job sends results to the same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="fb7e0-204">В разделе **Топология задания** в колонке задания щелкните поле **Выходные данные**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-204">Under **Job Topology** in the job blade, click the **Outputs** box.</span></span>  
  
   ![Создание новых выходных данных для задания Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="fb7e0-206">В колонке **Выходные данные** щелкните **Добавить**, а затем добавьте выходные данные с псевдонимом `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-206">In the **Outputs** blade, click **+ Add**, and then add an output with the alias `datamloutput`.</span></span> 

3. <span data-ttu-id="fb7e0-207">Для поля **Приемник** выберите **Хранилище BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="fb7e0-208">Укажите остальные параметры выходных данных, используя те же значения, которые использовались для хранилища BLOB-объектов для входных данных.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-208">Then fill in the rest of the output settings using the same values that you used for the blob storage for input:</span></span>

    * <span data-ttu-id="fb7e0-209">**Учетная запись хранения**:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-209">**Storage account**.</span></span> <span data-ttu-id="fb7e0-210">выберите учетную запись хранения, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-210">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="fb7e0-211">**Контейнер**:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-211">**Container**.</span></span> <span data-ttu-id="fb7e0-212">выберите созданный ранее контейнер (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="fb7e0-212">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="fb7e0-213">**Формат сериализации событий**:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-213">**Event serialization format**.</span></span> <span data-ttu-id="fb7e0-214">выберите **CSV**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-214">Select **CSV**.</span></span>

   ![Параметры для новых выходных данных задания](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="fb7e0-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-216">Click **Create**.</span></span>   


### <a name="add-the-machine-learning-function"></a><span data-ttu-id="fb7e0-217">Добавление функции машинного обучения</span><span class="sxs-lookup"><span data-stu-id="fb7e0-217">Add the Machine Learning function</span></span> 
<span data-ttu-id="fb7e0-218">Ранее вы опубликовали модель машинного обучения в веб-службе.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-218">Earlier you published a Machine Learning model to a web service.</span></span> <span data-ttu-id="fb7e0-219">В нашем сценарии выполняемое задание Stream Analytics отправляет каждый образец твита из входных данных в веб-службу для анализа тональности.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-219">In our scenario, when the Stream Analysis job runs, it sends each sample tweet from the input to the web service for sentiment analysis.</span></span> <span data-ttu-id="fb7e0-220">Веб-служба машинного обучения возвращает тональность (`positive`, `neutral` или `negative`) и вероятность того, что твит положительный.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-220">The Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of the tweet being positive.</span></span> 

<span data-ttu-id="fb7e0-221">В этом разделе руководства вы определите функцию в задании Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-221">In this section of the tutorial, you define a function in the Stream Analysis job.</span></span> <span data-ttu-id="fb7e0-222">Эту функцию можно вызывать для отправки твита в веб-службу и получения ответа.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-222">The function can be invoked to send a tweet to the web service and get the response back.</span></span> 

1. <span data-ttu-id="fb7e0-223">У вас должны быть URL-адрес веб-службы и ключ API в скачанной ранее книге Excel.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-223">Make sure you have the web service URL and API key that you downloaded earlier in the Excel workbook.</span></span>

2. <span data-ttu-id="fb7e0-224">Вернитесь в колонку обзора задания.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-224">Return to the job overview blade.</span></span>

3. <span data-ttu-id="fb7e0-225">В разделе **Параметры** выберите **Функции**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Добавление функции в задание Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="fb7e0-227">Введите `sentiment` как псевдоним для функции и заполните остальные параметры колонки следующими значениями.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-227">Enter `sentiment` as the function alias and fill out the rest of the blade using these values:</span></span>

    * <span data-ttu-id="fb7e0-228">**Тип функции**: выберите **Машинное обучение Azure**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="fb7e0-229">**Метод импорта**: выберите **Импортировать из другой подписки**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="fb7e0-230">Это позволит вам ввести URL-адрес и ключ.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-230">This gives you a chance to enter the URL and key.</span></span>
    * <span data-ttu-id="fb7e0-231">**URL-адрес**: вставьте URL-адрес веб-службы.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-231">**URL**: Paste in the web service URL.</span></span>
    * <span data-ttu-id="fb7e0-232">**Ключ**: вставьте ключ API.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-232">**Key**: Paste in the API key.</span></span>
  
    ![Параметры для добавления функции машинного обучения в задание Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="fb7e0-234">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-234">Click **Create**.</span></span>

### <a name="create-a-query-to-transform-the-data"></a><span data-ttu-id="fb7e0-235">Создание запроса для преобразования данных</span><span class="sxs-lookup"><span data-stu-id="fb7e0-235">Create a query to transform the data</span></span>

<span data-ttu-id="fb7e0-236">Stream Analytics использует декларативный запрос на основе SQL для проверки входных данных и их обработки.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-236">Stream Analytics uses a declarative, SQL-based query to examine the input and process it.</span></span> <span data-ttu-id="fb7e0-237">В этом разделе вы создадите запрос, который считывает каждый твит из входных данных, а затем вызывает функцию машинного обучения для выполнения анализа тональности.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-237">In this section, you create a query that reads each tweet from input and then invokes the Machine Learning function to perform sentiment analysis.</span></span> <span data-ttu-id="fb7e0-238">Затем запрос отправляет результат в приемник выходных данных (хранилище BLOB-объектов).</span><span class="sxs-lookup"><span data-stu-id="fb7e0-238">The query then sends the result to the output that you defined (blob storage).</span></span>

1. <span data-ttu-id="fb7e0-239">Вернитесь в колонку обзора задания.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-239">Return to the job overview blade.</span></span>

2.  <span data-ttu-id="fb7e0-240">В разделе **Топология задания** щелкните поле **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-240">Under **Job Topology**, click the **Query** box.</span></span>

    ![Создание запроса для задания Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="fb7e0-242">Введите следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-242">Enter the following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="fb7e0-243">Запрос вызывает созданную ранее функцию (`sentiment`) для выполнения анализа тональности каждого твита во входных данных.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-243">The query invokes the function you created earlier (`sentiment`) in order to perform sentiment analysis on each tweet in the input.</span></span> 

4. <span data-ttu-id="fb7e0-244">Щелкните **Сохранить** , чтобы сохранить запрос.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-244">Click **Save** to save the query.</span></span>


## <a name="start-the-stream-analytics-job-and-check-the-output"></a><span data-ttu-id="fb7e0-245">Запуск задания Stream Analytics и просмотр выходных данных</span><span class="sxs-lookup"><span data-stu-id="fb7e0-245">Start the Stream Analytics job and check the output</span></span>

<span data-ttu-id="fb7e0-246">Теперь вы можете запустить задание Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-246">You can now start the Stream Analytics job.</span></span>

### <a name="start-the-job"></a><span data-ttu-id="fb7e0-247">Запустите задание</span><span class="sxs-lookup"><span data-stu-id="fb7e0-247">Start the job</span></span>
1. <span data-ttu-id="fb7e0-248">Вернитесь в колонку обзора задания.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-248">Return to the job overview blade.</span></span>

2. <span data-ttu-id="fb7e0-249">Нажмите кнопку **Запуск** в верхней области колонки.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-249">Click **Start** at the top of the blade.</span></span>

    ![Создание запроса для задания Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="fb7e0-251">В диалоговом окне **Запуск задания** выберите **Настраиваемый** и укажите один день до передачи CSV-файла в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-251">In the **Start job**, select **Custom**, and then select one day prior to when you uploaded the CSV file to blob storage.</span></span> <span data-ttu-id="fb7e0-252">После этого нажмите кнопку **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-252">When you're done, click **Start**.</span></span>  


### <a name="check-the-output"></a><span data-ttu-id="fb7e0-253">Просмотр выходных данных</span><span class="sxs-lookup"><span data-stu-id="fb7e0-253">Check the output</span></span>
1. <span data-ttu-id="fb7e0-254">Задание может выполняться несколько минут, прежде чем вы увидите выполнение этой операции в поле **Мониторинг**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-254">Let the job run for a few minutes until you see activity in the **Monitoring** box.</span></span> 

2. <span data-ttu-id="fb7e0-255">Если у вас есть средство, которое вы обычно используете для просмотра содержимого хранилища BLOB-объектов, используйте его для просмотра контейнера `azuresamldemoblob`.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-255">If you have a tool that you normally use to examine the contents of blob storage, use that tool to examine the `azuresamldemoblob` container.</span></span> <span data-ttu-id="fb7e0-256">Кроме того, на портале Azure выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-256">Alternatively, do the following steps in the Azure portal:</span></span>

    1. <span data-ttu-id="fb7e0-257">Найдите на портале учетную запись хранения `samldemo`, а в ней найдите контейнер `azuresamldemoblob`.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-257">In the portal, find the `samldemo` storage account, and within the account, find the `azuresamldemoblob` container.</span></span> <span data-ttu-id="fb7e0-258">Вы увидите в нем два файла: файл, содержащий образец твитов, и CSV-файл, созданный заданием Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-258">You see two files in the container: the file that contains the sample tweets and a CSV file generated by the Stream Analytics job.</span></span>
    2. <span data-ttu-id="fb7e0-259">Щелкните правой кнопкой мыши созданный файл, а затем выберите **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-259">Right-click the generated file and then select **Download**.</span></span> 

   ![Скачивание выходных данных задания в виде CSV-файла из хранилища BLOB-объектов](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="fb7e0-261">Откройте созданный CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-261">Open the generated CSV file.</span></span> <span data-ttu-id="fb7e0-262">Вы должны увидеть примерно следующее:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-262">You see something like the following example:</span></span>  
   
   ![Машинное обучение и Stream Analytics, просмотр CSV-файла](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="fb7e0-264">Просмотр метрик</span><span class="sxs-lookup"><span data-stu-id="fb7e0-264">View metrics</span></span>
<span data-ttu-id="fb7e0-265">Вы можете также просматривать метрики, связанные с функциями Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="fb7e0-266">В поле **Мониторинг** в колонке задания отображаются следующие метрики, связанные с функцией:</span><span class="sxs-lookup"><span data-stu-id="fb7e0-266">The following function-related metrics are displayed in the **Monitoring** box in the job blade:</span></span>

* <span data-ttu-id="fb7e0-267">**Запросы функций** отображает количество запросов, отправленных к веб-службе машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-267">**Function Requests** indicates the number of requests sent to a Machine Learning web service.</span></span>  
* <span data-ttu-id="fb7e0-268">**События функций** отображает количество событий в запросе.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-268">**Function Events** indicates the number of events in the request.</span></span> <span data-ttu-id="fb7e0-269">По умолчанию каждый запрос к веб-службе машинного обучения может содержать до 1000 событий.</span><span class="sxs-lookup"><span data-stu-id="fb7e0-269">By default, each request to a Machine Learning web service contains up to 1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="fb7e0-270">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fb7e0-270">Next steps</span></span>

* [<span data-ttu-id="fb7e0-271">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fb7e0-271">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fb7e0-272">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fb7e0-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="fb7e0-273">Интеграция машинного обучения в Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fb7e0-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="fb7e0-274">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fb7e0-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



