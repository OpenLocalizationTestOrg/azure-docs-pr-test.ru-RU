---
title: "Прогноз с использованием машинного обучения Azure с помощью данных из центра IoT aaaWeather | Документы Microsoft"
description: "Используйте машинное обучение Azure, вероятность hello toopredict дождь на основе hello температуры и влажности данные, которые собирает концентратор IoT из датчика."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Прогнозирование погоды с помощью машинного обучения"
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="82794-104">Прогноз погоды, используя данные датчика hello из вашего центра IoT в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="82794-104">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="82794-106">Машинное обучение методика обработки и анализа данных, позволяет компьютерам узнать из будущих поведения tooforecast существующих данных, результаты и тенденций.</span><span class="sxs-lookup"><span data-stu-id="82794-106">Machine learning is a technique of data science that helps computers learn from existing data tooforecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="82794-107">Машинное обучение Azure — облачной службы прогнозирующей аналитики, которая упрощает возможных tooquickly Создание и развертывание прогнозных моделей в качестве решения для аналитики.</span><span class="sxs-lookup"><span data-stu-id="82794-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible tooquickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="82794-108">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="82794-108">What you learn</span></span>

<span data-ttu-id="82794-109">Вы узнаете, как с помощью toouse машинного обучения Azure toodo прогноз погоды (вероятность дождь) Здравствуйте, температуры и влажности данные из вашего центра Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="82794-109">You learn how toouse Azure Machine Learning toodo weather forecast (chance of rain) using hello temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="82794-110">вероятность Hello дождь выводится hello подготовленного погоды модели прогнозирования.</span><span class="sxs-lookup"><span data-stu-id="82794-110">hello chance of rain is hello output of a prepared weather prediction model.</span></span> <span data-ttu-id="82794-111">Hello модель построена на основе вероятность на основе температуры и влажности дождь tooforecast данные за прошедший период.</span><span class="sxs-lookup"><span data-stu-id="82794-111">hello model is built upon historic data tooforecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="82794-112">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="82794-112">What you do</span></span>

- <span data-ttu-id="82794-113">Развертывание модели прогноза погоды hello в виде веб-службы.</span><span class="sxs-lookup"><span data-stu-id="82794-113">Deploy hello weather prediction model as a web service.</span></span>
- <span data-ttu-id="82794-114">добавим группу потребителей, чтобы обеспечить доступ к данным в Центре Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="82794-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="82794-115">Создание задания Stream Analytics и задать для задания hello:</span><span class="sxs-lookup"><span data-stu-id="82794-115">Create a Stream Analytics job and configure hello job to:</span></span>
  - <span data-ttu-id="82794-116">получение данных о температуре и влажности от Центра Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="82794-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="82794-117">Вызов hello web service tooget hello дождь вероятность.</span><span class="sxs-lookup"><span data-stu-id="82794-117">Call hello web service tooget hello rain chance.</span></span>
  - <span data-ttu-id="82794-118">Сохраните хранилище больших двоичных объектов tooan результат hello.</span><span class="sxs-lookup"><span data-stu-id="82794-118">Save hello result tooan Azure blob storage.</span></span>
- <span data-ttu-id="82794-119">Используйте прогноз погоды hello tooview обозреватель хранилищ Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="82794-119">Use Microsoft Azure Storage Explorer tooview hello weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="82794-120">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="82794-120">What you need</span></span>

- <span data-ttu-id="82794-121">Учебник по [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md) завершения, который охватывает hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="82794-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="82794-122">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="82794-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="82794-123">Центр Интернета вещей Azure в подписке;</span><span class="sxs-lookup"><span data-stu-id="82794-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="82794-124">Клиентское приложение, которое отправляет центр Azure IoT tooyour сообщений.</span><span class="sxs-lookup"><span data-stu-id="82794-124">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="82794-125">учетную запись Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="82794-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="82794-126">([Бесплатно ознакомьтесь с работой студии машинного обучения](https://studio.azureml.net/).)</span><span class="sxs-lookup"><span data-stu-id="82794-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="82794-127">Развертывание модели прогноза погоды hello в виде веб-службы</span><span class="sxs-lookup"><span data-stu-id="82794-127">Deploy hello weather prediction model as a web service</span></span>

1. <span data-ttu-id="82794-128">Go toohello [страницы модели прогноза погоды](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="82794-128">Go toohello [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="82794-129">Щелкните **Открыть в Studio** в Студии машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="82794-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="82794-130">![Страница модели прогноза погоды Привет открыть в коллекции Cortana аналитики](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="82794-130">![Open hello weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="82794-131">Нажмите кнопку **запуска** toovalidate hello шагов в модели hello.</span><span class="sxs-lookup"><span data-stu-id="82794-131">Click **Run** toovalidate hello steps in hello model.</span></span> <span data-ttu-id="82794-132">Этот шаг может занять toocomplete 2 минуты.</span><span class="sxs-lookup"><span data-stu-id="82794-132">This step might take 2 minutes toocomplete.</span></span>
   <span data-ttu-id="82794-133">![Привет открыть модель прогноза погоды в студии машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="82794-133">![Open hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="82794-134">Щелкните действие **SET UP WEB SERVICE** (Настроить веб-службу)  > **Predictive Web Service** (Прогнозная веб-служба).</span><span class="sxs-lookup"><span data-stu-id="82794-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="82794-135">![Развертывание модели прогноза погоды hello в студии машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="82794-135">![Deploy hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="82794-136">В диаграмме hello перетащите hello **веб-службе входные данные** модуля, где-нибудь рядом hello **модель оценки** модуля.</span><span class="sxs-lookup"><span data-stu-id="82794-136">In hello diagram, drag hello **Web service input** module somewhere near hello **Score Model** module.</span></span>
1. <span data-ttu-id="82794-137">Подключение hello **веб-службе входные данные** toohello модуль **модель оценки** модуля.</span><span class="sxs-lookup"><span data-stu-id="82794-137">Connect hello **Web service input** module toohello **Score Model** module.</span></span>
   <span data-ttu-id="82794-138">![Соединение модулей в Студии машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="82794-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="82794-139">Нажмите кнопку **ЗАПУСКА** toovalidate hello шагов в модели hello.</span><span class="sxs-lookup"><span data-stu-id="82794-139">Click **RUN** toovalidate hello steps in hello model.</span></span>
1. <span data-ttu-id="82794-140">Нажмите кнопку **развертывание веб-службы** toodeploy hello модели веб-службы.</span><span class="sxs-lookup"><span data-stu-id="82794-140">Click **DEPLOY WEB SERVICE** toodeploy hello model as a web service.</span></span>
1. <span data-ttu-id="82794-141">На панели мониторинга hello hello модели, загрузите hello **Excel 2010 или более ранних книги** для **ЗАПРОСОВ и ОТВЕТОВ**.</span><span class="sxs-lookup"><span data-stu-id="82794-141">On hello dashboard of hello model, download hello **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="82794-142">Убедитесь, необходимо загрузить hello **Excel 2010 или более ранних книги** даже если на компьютере более поздней версии Excel на компьютере.</span><span class="sxs-lookup"><span data-stu-id="82794-142">Ensure that you download hello **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Загрузите hello Excel для конечной точки ОТВЕТА запрос hello](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="82794-144">Откройте книгу Excel hello, запишите hello **URL веб-службы** и **ключ доступа**.</span><span class="sxs-lookup"><span data-stu-id="82794-144">Open hello Excel workbook, make a note of hello **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="82794-145">Создание, настройка и выполнение заданий Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="82794-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="82794-146">Создание задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="82794-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="82794-147">В hello [портал Azure](https://ms.portal.azure.com/), нажмите кнопку **New** > **Интернета вещей** > **задания Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="82794-147">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="82794-148">Введите следующую информацию для задания hello hello.</span><span class="sxs-lookup"><span data-stu-id="82794-148">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="82794-149">**Имя задания**: hello имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="82794-149">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="82794-150">Hello имя должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="82794-150">hello name must be globally unique.</span></span>

   <span data-ttu-id="82794-151">**Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="82794-151">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="82794-152">**Расположение**: используйте hello же расположении, что и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="82794-152">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="82794-153">**ПИН-код toodashboard**: Установите этот флажок для центра IoT tooyour простой доступ из панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="82794-153">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Создание задания Stream Analytics в Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="82794-155">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="82794-155">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="82794-156">Добавьте задание Stream Analytics входного toohello</span><span class="sxs-lookup"><span data-stu-id="82794-156">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="82794-157">Задание Stream Analytics откройте hello.</span><span class="sxs-lookup"><span data-stu-id="82794-157">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="82794-158">В разделе **Топология задания** щелкните **Входные данные**.</span><span class="sxs-lookup"><span data-stu-id="82794-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="82794-159">В hello **входные данные** области, нажмите кнопку **добавить**и нажмите ВВОД hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="82794-159">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="82794-160">**Входной псевдоним**: hello уникальный псевдоним для hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="82794-160">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="82794-161">**Источник**. Выберите **Центр Интернета вещей**.</span><span class="sxs-lookup"><span data-stu-id="82794-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="82794-162">**Группа потребителей**: созданную группу потребителей выберите hello.</span><span class="sxs-lookup"><span data-stu-id="82794-162">**Consumer group**: Select hello consumer group you created.</span></span>

   ![Добавить задание Stream Analytics ввода toohello в Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="82794-164">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="82794-164">Click **Create**.</span></span>

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="82794-165">Добавление выходных данных задания Stream Analytics toohello</span><span class="sxs-lookup"><span data-stu-id="82794-165">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="82794-166">В разделе **Топология задания** щелкните **Выходные данные**.</span><span class="sxs-lookup"><span data-stu-id="82794-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="82794-167">В hello **выходные данные** области, нажмите кнопку **добавить**и нажмите ВВОД hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="82794-167">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="82794-168">**Псевдоним вывода**: hello уникальный псевдоним для выходной hello.</span><span class="sxs-lookup"><span data-stu-id="82794-168">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="82794-169">**Приемник.** Выберите **хранилище BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="82794-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="82794-170">**Учетная запись хранения**: hello учетной записи хранилища для хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="82794-170">**Storage account**: hello storage account for your blob storage.</span></span> <span data-ttu-id="82794-171">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="82794-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="82794-172">**Контейнер**: hello контейнер хранения больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="82794-172">**Container**: hello container where hello blob is saved.</span></span> <span data-ttu-id="82794-173">Вы можете создать новый контейнер или использовать уже существующий.</span><span class="sxs-lookup"><span data-stu-id="82794-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="82794-174">**Формат сериализации событий.** Выберите вариант **CSV**.</span><span class="sxs-lookup"><span data-stu-id="82794-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Добавить задание Stream Analytics toohello выходные данные в Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="82794-176">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="82794-176">Click **Create**.</span></span>

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a><span data-ttu-id="82794-177">Добавление функции toohello Stream Analytics задания toocall hello веб-службы, развернутые</span><span class="sxs-lookup"><span data-stu-id="82794-177">Add a function toohello Stream Analytics job toocall hello web service you deployed</span></span>

1. <span data-ttu-id="82794-178">В разделе **Топология задания** щелкните **Функции** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="82794-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="82794-179">Введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="82794-179">Enter hello following information:</span></span>

   <span data-ttu-id="82794-180">**Псевдоним функции**: введите значение `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="82794-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="82794-181">**Тип функции**: выберите вариант **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="82794-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="82794-182">**Метод импорта**: выберите **Импортировать из другой подписки**.</span><span class="sxs-lookup"><span data-stu-id="82794-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="82794-183">**URL-адрес**: Введите URL веб-службы, отмеченный вниз hello из книги Excel hello.</span><span class="sxs-lookup"><span data-stu-id="82794-183">**URL**: Enter hello WEB SERVICE URL that you noted down from hello Excel workbook.</span></span>

   <span data-ttu-id="82794-184">**Ключ**: Введите ключ доступа, отмеченный вниз hello из книги Excel hello.</span><span class="sxs-lookup"><span data-stu-id="82794-184">**Key**: Enter hello ACCESS KEY that you noted down from hello Excel workbook.</span></span>

   ![Добавить задание Stream Analytics toohello функции в Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="82794-186">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="82794-186">Click **Create**.</span></span>

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="82794-187">Настройка запроса hello задания Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="82794-187">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="82794-188">В разделе **Топология задания** щелкните **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="82794-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="82794-189">Замените существующий код hello hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="82794-189">Replace hello existing code with hello following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="82794-190">Замените `[YourInputAlias]` с псевдонимом входного hello hello задания.</span><span class="sxs-lookup"><span data-stu-id="82794-190">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>

   <span data-ttu-id="82794-191">Замените `[YourOutputAlias]` с Псевдоним выхода hello hello задания.</span><span class="sxs-lookup"><span data-stu-id="82794-191">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>

1. <span data-ttu-id="82794-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="82794-192">Click **Save**.</span></span>

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="82794-193">Запустить задание Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="82794-193">Run hello Stream Analytics job</span></span>

<span data-ttu-id="82794-194">В задании Stream Analytics hello, нажмите кнопку **запустить** > **теперь** > **запустить**.</span><span class="sxs-lookup"><span data-stu-id="82794-194">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="82794-195">После успешного запуска задания hello hello состояние задания меняется с **остановлена** слишком**под управлением**.</span><span class="sxs-lookup"><span data-stu-id="82794-195">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Запустить задание Stream Analytics hello](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a><span data-ttu-id="82794-197">Использовать прогноз погоды hello tooview обозреватель хранилищ Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="82794-197">Use Microsoft Azure Storage Explorer tooview hello weather forecast</span></span>

<span data-ttu-id="82794-198">Выполните сбор toostart hello клиентского приложения и отправку температуры и влажности центра IoT tooyour данных.</span><span class="sxs-lookup"><span data-stu-id="82794-198">Run hello client application toostart collecting and sending temperature and humidity data tooyour IoT hub.</span></span> <span data-ttu-id="82794-199">Для каждого сообщения, получающего концентратор IoT задание Stream Analytics hello вызывает hello прогноз погоды web service tooproduce hello вероятность дождь.</span><span class="sxs-lookup"><span data-stu-id="82794-199">For each message that your IoT hub receives, hello Stream Analytics job calls hello weather forecast web service tooproduce hello chance of rain.</span></span> <span data-ttu-id="82794-200">Затем результат Hello сохраняется tooyour хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="82794-200">hello result is then saved tooyour Azure blob storage.</span></span> <span data-ttu-id="82794-201">Azure Storage Explorer — это средство, можно использовать tooview hello результат.</span><span class="sxs-lookup"><span data-stu-id="82794-201">Azure Storage Explorer is a tool that you can use tooview hello result.</span></span>

1. <span data-ttu-id="82794-202">[Скачайте и установите обозреватель хранилищ Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="82794-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="82794-203">Откройте обозреватель службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="82794-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="82794-204">Войдите в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="82794-204">Sign in tooyour Azure account.</span></span>
1. <span data-ttu-id="82794-205">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="82794-205">Select your subscription.</span></span>
1. <span data-ttu-id="82794-206">Щелкните подписку Azure > **Учетные записи хранения** > учетная запись хранения > **Контейнеры больших двоичных объектов** и выберите нужный контейнер.</span><span class="sxs-lookup"><span data-stu-id="82794-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="82794-207">Откройте результат hello toosee файл CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="82794-207">Open a .csv file toosee hello result.</span></span> <span data-ttu-id="82794-208">последний столбец записи Hello hello вероятность дождь.</span><span class="sxs-lookup"><span data-stu-id="82794-208">hello last column records hello chance of rain.</span></span>

   ![Получение прогноза погоды с помощью машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="82794-210">Сводка</span><span class="sxs-lookup"><span data-stu-id="82794-210">Summary</span></span>

<span data-ttu-id="82794-211">Вы использовали успешно вероятность hello tooproduce машинного обучения Azure на основе данных температуры и влажности hello, получающий концентратор IoT дождь.</span><span class="sxs-lookup"><span data-stu-id="82794-211">You’ve successfully used Azure Machine Learning tooproduce hello chance of rain based on hello temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]