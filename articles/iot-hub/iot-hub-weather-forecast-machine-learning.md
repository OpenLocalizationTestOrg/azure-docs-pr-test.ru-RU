---
title: "Прогнозирование погоды с помощью машинного обучения Azure на основе данных Центра Интернета вещей | Документация Майкрософт"
description: "Используйте машинное обучение Azure, чтобы прогнозировать вероятность дождя на основе данных о температуре и влажности, которые собираются от датчиков в Центре Интернета вещей."
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
ms.openlocfilehash: 50ae54b9476c49b80236e295c0bf244df8236cff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="e27d6-104">Прогнозирование погоды в машинном обучении Azure с помощью данных от датчиков Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="e27d6-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="e27d6-106">Машинное обучение — это метод обработки и анализа данных, который позволяет компьютеру на основе исторических данных прогнозировать ожидаемые поведения, результаты и тенденции.</span><span class="sxs-lookup"><span data-stu-id="e27d6-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="e27d6-107">Служба машинного обучения Azure — это облачная служба прогнозной аналитики, которая позволяет быстро создавать и развертывать прогнозные модели в качестве решений аналитики.</span><span class="sxs-lookup"><span data-stu-id="e27d6-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="e27d6-108">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="e27d6-108">What you learn</span></span>

<span data-ttu-id="e27d6-109">Вы узнаете, как применить машинное обучение Azure для прогнозирования погоды (вероятности дождя) на основе данных о температуре и влажности, собранных в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="e27d6-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="e27d6-110">Вероятность дождя вычисляется по заранее подготовленной модели прогнозирования погоды.</span><span class="sxs-lookup"><span data-stu-id="e27d6-110">The chance of rain is the output of a prepared weather prediction model.</span></span> <span data-ttu-id="e27d6-111">Эта модель создается на основе исторических данных и применяется для оценки вероятности дождя, исходя из данных о температуре и влажности.</span><span class="sxs-lookup"><span data-stu-id="e27d6-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="e27d6-112">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="e27d6-112">What you do</span></span>

- <span data-ttu-id="e27d6-113">Развернем модель прогнозирования погоды как веб-службу.</span><span class="sxs-lookup"><span data-stu-id="e27d6-113">Deploy the weather prediction model as a web service.</span></span>
- <span data-ttu-id="e27d6-114">Добавить группу потребителей, чтобы обеспечить доступ к данным в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="e27d6-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="e27d6-115">Создадим задание Stream Analytics и настроим его на выполнение следующих задач:</span><span class="sxs-lookup"><span data-stu-id="e27d6-115">Create a Stream Analytics job and configure the job to:</span></span>
  - <span data-ttu-id="e27d6-116">получение данных о температуре и влажности от Центра Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="e27d6-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="e27d6-117">вызов веб-службы для получения оценки вероятности дождя;</span><span class="sxs-lookup"><span data-stu-id="e27d6-117">Call the web service to get the rain chance.</span></span>
  - <span data-ttu-id="e27d6-118">сохранение результатов в хранилище BLOB-объектов Azure;</span><span class="sxs-lookup"><span data-stu-id="e27d6-118">Save the result to an Azure blob storage.</span></span>
- <span data-ttu-id="e27d6-119">Откроем обозреватель хранилища Microsoft Azure для просмотра прогноза погоды.</span><span class="sxs-lookup"><span data-stu-id="e27d6-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e27d6-120">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="e27d6-120">What you need</span></span>

- <span data-ttu-id="e27d6-121">Изучите руководство [Настройка вашего устройства](iot-hub-raspberry-pi-kit-node-get-started.md), где описаны следующие требования.</span><span class="sxs-lookup"><span data-stu-id="e27d6-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="e27d6-122">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="e27d6-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="e27d6-123">Центр Интернета вещей Azure в подписке;</span><span class="sxs-lookup"><span data-stu-id="e27d6-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="e27d6-124">клиентское приложение, которое отправляет сообщения в Центр Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="e27d6-124">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="e27d6-125">учетную запись Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="e27d6-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="e27d6-126">([Бесплатно ознакомьтесь с работой студии машинного обучения](https://studio.azureml.net/).)</span><span class="sxs-lookup"><span data-stu-id="e27d6-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="e27d6-127">Развертывание модели прогнозирования погоды как веб-службы</span><span class="sxs-lookup"><span data-stu-id="e27d6-127">Deploy the weather prediction model as a web service</span></span>

1. <span data-ttu-id="e27d6-128">Откройте [страницу модели прогнозирования погоды](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="e27d6-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="e27d6-129">Щелкните **Открыть в Studio** в Студии машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e27d6-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="e27d6-130">![Открытая страница модели прогнозирования погоды в коллекции Cortana Intelligence](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="e27d6-130">![Open the weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="e27d6-131">Щелкните **Run** (Запуск), чтобы проверить действия модели.</span><span class="sxs-lookup"><span data-stu-id="e27d6-131">Click **Run** to validate the steps in the model.</span></span> <span data-ttu-id="e27d6-132">Выполнение этого шага может занять до 2 минут.</span><span class="sxs-lookup"><span data-stu-id="e27d6-132">This step might take 2 minutes to complete.</span></span>
   <span data-ttu-id="e27d6-133">![Открытая модель прогнозирования погоды в Студии машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="e27d6-133">![Open the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="e27d6-134">Щелкните действие **SET UP WEB SERVICE** (Настроить веб-службу)  > **Predictive Web Service** (Прогнозная веб-служба).</span><span class="sxs-lookup"><span data-stu-id="e27d6-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="e27d6-135">![Развертывание модели прогнозирования погоды в Студии машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="e27d6-135">![Deploy the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="e27d6-136">На схеме перетащите модуль **Web service input** (Вход веб-службы) куда-нибудь поближе к модулю **Score Model** (Оценка модели).</span><span class="sxs-lookup"><span data-stu-id="e27d6-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span></span>
1. <span data-ttu-id="e27d6-137">Соедините между собой модули **Web service input** (Вход веб-службы) и **Score Model** (Оценка модели).</span><span class="sxs-lookup"><span data-stu-id="e27d6-137">Connect the **Web service input** module to the **Score Model** module.</span></span>
   <span data-ttu-id="e27d6-138">![Соединение модулей в Студии машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="e27d6-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="e27d6-139">Щелкните **RUN** (Запуск), чтобы проверить действия модели.</span><span class="sxs-lookup"><span data-stu-id="e27d6-139">Click **RUN** to validate the steps in the model.</span></span>
1. <span data-ttu-id="e27d6-140">Щелкните **DEPLOY WEB SERVICE** (Развернуть веб-службу), чтобы преобразовать эту модель в веб-службу.</span><span class="sxs-lookup"><span data-stu-id="e27d6-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span></span>
1. <span data-ttu-id="e27d6-141">На панели мониторинга модели скачайте **Excel 2010 or earlier workbook** (Книга Excel 2010 или более ранних версий) для действия **REQUEST/RESPONSE** (Запрос — ответ).</span><span class="sxs-lookup"><span data-stu-id="e27d6-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="e27d6-142">Обязательно используйте именно **Excel 2010 or earlier workbook** (Книга Excel 2010 или более ранних версий), даже если на вашем компьютере установлена более поздняя версия Excel.</span><span class="sxs-lookup"><span data-stu-id="e27d6-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Скачивание книги Excel для конечной точки REQUEST RESPONSE ("запрос — ответ")](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="e27d6-144">Откройте эту книгу Excel и запишите параметры **WEB SERVICE URL** (URL веб-службы) и **ACCESS KEY** (Ключ доступа).</span><span class="sxs-lookup"><span data-stu-id="e27d6-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="e27d6-145">Создание, настройка и выполнение заданий Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e27d6-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="e27d6-146">Создание задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e27d6-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="e27d6-147">На [портале Azure](https://ms.portal.azure.com/) щелкните **Создание** > **Интернет вещей** > **Задание Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-147">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="e27d6-148">Введите представленные ниже сведения для задания.</span><span class="sxs-lookup"><span data-stu-id="e27d6-148">Enter the following information for the job.</span></span>

   <span data-ttu-id="e27d6-149">**Имя задания**. Имя задания.</span><span class="sxs-lookup"><span data-stu-id="e27d6-149">**Job name**: The name of the job.</span></span> <span data-ttu-id="e27d6-150">Оно должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="e27d6-150">The name must be globally unique.</span></span>

   <span data-ttu-id="e27d6-151">**Группа ресурсов**. Выберите ту же группу ресурсов, которую использует Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="e27d6-151">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="e27d6-152">**Расположение**. Выберите то же расположение, которое использует группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e27d6-152">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="e27d6-153">**Закрепить на панели мониторинга**. Установите этот флажок, чтобы быстро открывать Центр Интернета вещей с помощью панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="e27d6-153">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Создание задания Stream Analytics в Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="e27d6-155">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-155">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="e27d6-156">Добавление входных данных в задание Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e27d6-156">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="e27d6-157">Откройте задание Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="e27d6-157">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="e27d6-158">В разделе **Топология задания** щелкните **Входные данные**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="e27d6-159">В области **Входные данные** щелкните **Добавить**, а затем введите сведения, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="e27d6-159">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="e27d6-160">**Входной псевдоним**. Уникальный псевдоним для входных данных.</span><span class="sxs-lookup"><span data-stu-id="e27d6-160">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="e27d6-161">**Источник**. Выберите **Центр Интернета вещей**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="e27d6-162">**Группа потребителей.** Выберите созданную группу потребителей.</span><span class="sxs-lookup"><span data-stu-id="e27d6-162">**Consumer group**: Select the consumer group you created.</span></span>

   ![Добавление входных данных в задание Stream Analytics в Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="e27d6-164">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-164">Click **Create**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="e27d6-165">Добавление выходных данных в задание Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e27d6-165">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="e27d6-166">В разделе **Топология задания** щелкните **Выходные данные**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="e27d6-167">В области **Выходные данные** щелкните **Добавить**, а затем введите сведения, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="e27d6-167">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="e27d6-168">**Выходной псевдоним**. Уникальный псевдоним для выходных данных.</span><span class="sxs-lookup"><span data-stu-id="e27d6-168">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="e27d6-169">**Приемник.** Выберите **хранилище BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="e27d6-170">**Учетная запись хранения.** Это учетная запись хранения для вашего BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="e27d6-170">**Storage account**: The storage account for your blob storage.</span></span> <span data-ttu-id="e27d6-171">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="e27d6-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="e27d6-172">**Контейнер.** Это контейнер, в котором сохранен большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="e27d6-172">**Container**: The container where the blob is saved.</span></span> <span data-ttu-id="e27d6-173">Вы можете создать новый контейнер или использовать уже существующий.</span><span class="sxs-lookup"><span data-stu-id="e27d6-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="e27d6-174">**Формат сериализации событий.** Выберите вариант **CSV**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Добавление выходных данных в задание Stream Analytics в Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="e27d6-176">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-176">Click **Create**.</span></span>

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a><span data-ttu-id="e27d6-177">Добавление в задание Stream Analytics функции для вызова развернутой веб-службы</span><span class="sxs-lookup"><span data-stu-id="e27d6-177">Add a function to the Stream Analytics job to call the web service you deployed</span></span>

1. <span data-ttu-id="e27d6-178">В разделе **Топология задания** щелкните **Функции** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="e27d6-179">Введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="e27d6-179">Enter the following information:</span></span>

   <span data-ttu-id="e27d6-180">**Псевдоним функции**: введите значение `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="e27d6-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="e27d6-181">**Тип функции**: выберите вариант **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="e27d6-182">**Метод импорта**: выберите **Импортировать из другой подписки**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="e27d6-183">**URL-адрес**: введите URL веб-службы, который вы взяли из книги Excel.</span><span class="sxs-lookup"><span data-stu-id="e27d6-183">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span></span>

   <span data-ttu-id="e27d6-184">**Ключ**: введите ключ доступа, который вы взяли из книги Excel.</span><span class="sxs-lookup"><span data-stu-id="e27d6-184">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span></span>

   ![Добавление функции в задание Stream Analytics в Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="e27d6-186">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-186">Click **Create**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="e27d6-187">Настройка запроса задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e27d6-187">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="e27d6-188">В разделе **Топология задания** щелкните **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="e27d6-189">Замените текст запроса следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="e27d6-189">Replace the existing code with the following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="e27d6-190">Замените значение `[YourInputAlias]` значением псевдонима входных данных задания.</span><span class="sxs-lookup"><span data-stu-id="e27d6-190">Replace `[YourInputAlias]` with the input alias of the job.</span></span>

   <span data-ttu-id="e27d6-191">Замените значение `[YourOutputAlias]` значением псевдонима выходных данных задания.</span><span class="sxs-lookup"><span data-stu-id="e27d6-191">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>

1. <span data-ttu-id="e27d6-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-192">Click **Save**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="e27d6-193">Выполнение задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e27d6-193">Run the Stream Analytics job</span></span>

<span data-ttu-id="e27d6-194">В задании Stream Analytics щелкните **Запуск** > **Сейчас** > **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-194">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="e27d6-195">После успешного запуска состояние задания **Остановлено** изменится на **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="e27d6-195">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Выполнение задания Stream Analytics](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a><span data-ttu-id="e27d6-197">Использование обозревателя службы хранилища Microsoft Azure для просмотра прогноза погоды</span><span class="sxs-lookup"><span data-stu-id="e27d6-197">Use Microsoft Azure Storage Explorer to view the weather forecast</span></span>

<span data-ttu-id="e27d6-198">Запустите клиентское приложение, чтобы начать сбор и отправку данных о температуре и влажности в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="e27d6-198">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span></span> <span data-ttu-id="e27d6-199">Для каждого сообщения, полученного Центром Интернета вещей, задание Stream Analytics вызывает веб-службу прогнозирования погоды, чтобы оценить вероятности дождя.</span><span class="sxs-lookup"><span data-stu-id="e27d6-199">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span></span> <span data-ttu-id="e27d6-200">Полученный результат сохраняется в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="e27d6-200">The result is then saved to your Azure blob storage.</span></span> <span data-ttu-id="e27d6-201">Сохраненные результаты можно просмотреть с помощью обозревателя службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="e27d6-201">Azure Storage Explorer is a tool that you can use to view the result.</span></span>

1. <span data-ttu-id="e27d6-202">[Скачайте и установите обозреватель хранилищ Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e27d6-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="e27d6-203">Откройте обозреватель службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="e27d6-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="e27d6-204">Войдите в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e27d6-204">Sign in to your Azure account.</span></span>
1. <span data-ttu-id="e27d6-205">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="e27d6-205">Select your subscription.</span></span>
1. <span data-ttu-id="e27d6-206">Щелкните подписку Azure > **Учетные записи хранения** > учетная запись хранения > **Контейнеры больших двоичных объектов** и выберите нужный контейнер.</span><span class="sxs-lookup"><span data-stu-id="e27d6-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="e27d6-207">Откройте CSV-файл, чтобы увидеть результат.</span><span class="sxs-lookup"><span data-stu-id="e27d6-207">Open a .csv file to see the result.</span></span> <span data-ttu-id="e27d6-208">Последний столбец содержит прогнозируемую вероятность дождя.</span><span class="sxs-lookup"><span data-stu-id="e27d6-208">The last column records the chance of rain.</span></span>

   ![Получение прогноза погоды с помощью машинного обучения Azure](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="e27d6-210">Сводка</span><span class="sxs-lookup"><span data-stu-id="e27d6-210">Summary</span></span>

<span data-ttu-id="e27d6-211">Итак, вы успешно применили машинное обучение Azure, чтобы прогнозировать вероятность дождя на основе данных о температуре и влажности, которые получает Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="e27d6-211">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]