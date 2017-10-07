---
title: "Визуализация данных во время aaaReal датчиков данных из центра IoT Azure — Power BI | Документы Microsoft"
description: "Используйте Power BI toovisualize температуры и влажности данные, полученные от датчика hello и отправляются tooyour центр Azure IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "визуализация данных, полученных в реальном времени, визуализация интерактивных данных, визуализация данных датчиков"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="5dbbe-104">Визуализация данных, поступающих от датчиков в реальном времени, из Центра Интернета вещей с помощью Power BI</span><span class="sxs-lookup"><span data-stu-id="5dbbe-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="5dbbe-106">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="5dbbe-106">What you learn</span></span>

<span data-ttu-id="5dbbe-107">Вы узнаете, как toovisualize в режиме реального времени датчиков, получающий ваш центр Azure IoT по Power BI.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-107">You learn how toovisualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="5dbbe-108">Если вы хотите tootry визуализации данных hello в концентратор IoT с веб-приложений, см. в разделе [веб-приложениях Azure используйте toovisualize в режиме реального времени датчиков из центра IoT Azure](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="5dbbe-108">If you want tootry visualize hello data in your IoT hub with Web Apps, please see [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="5dbbe-109">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="5dbbe-109">What you do</span></span>

- <span data-ttu-id="5dbbe-110">добавим группу потребителей, чтобы обеспечить доступ к данным в Центре Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="5dbbe-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="5dbbe-111">Создать, настроить и запустить задание Stream Analytics для передачи данных из вашего tooyour концентратора IoT учетной записи Power BI.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub tooyour Power BI account.</span></span>
- <span data-ttu-id="5dbbe-112">Создание и публикация данных hello toovisualize отчета Power BI.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-112">Create and publish a Power BI report toovisualize hello data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5dbbe-113">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="5dbbe-113">What you need</span></span>

- <span data-ttu-id="5dbbe-114">Учебник по [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md) завершения, который охватывает hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="5dbbe-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="5dbbe-115">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="5dbbe-116">Центр Интернета вещей Azure в подписке;</span><span class="sxs-lookup"><span data-stu-id="5dbbe-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="5dbbe-117">Клиентское приложение, которое отправляет центр Azure IoT tooyour сообщений.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-117">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="5dbbe-118">Учетная запись Power BI.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-118">A Power BI account.</span></span> <span data-ttu-id="5dbbe-119">Доступна [бесплатная пробная версия](https://powerbi.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="5dbbe-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="5dbbe-120">Создание, настройка и выполнение заданий Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5dbbe-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="5dbbe-121">Создание задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5dbbe-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="5dbbe-122">В hello портал Azure, нажмите кнопку Создать > Интернета вещей > задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-122">In hello Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="5dbbe-123">Введите следующую информацию для задания hello hello.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-123">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="5dbbe-124">**Имя задания**: hello имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-124">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="5dbbe-125">Hello имя должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-125">hello name must be globally unique.</span></span>

   <span data-ttu-id="5dbbe-126">**Группа ресурсов**: используйте hello же группы ресурсов, который использует ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-126">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="5dbbe-127">**Расположение**: используйте hello же расположении, что и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-127">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="5dbbe-128">**ПИН-код toodashboard**: Установите этот флажок для центра IoT tooyour простой доступ из панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-128">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Создание задания Stream Analytics в Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="5dbbe-130">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-130">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="5dbbe-131">Добавьте задание Stream Analytics входного toohello</span><span class="sxs-lookup"><span data-stu-id="5dbbe-131">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="5dbbe-132">Задание Stream Analytics откройте hello.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-132">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="5dbbe-133">В разделе **Топология задания** щелкните **Входные данные**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="5dbbe-134">В hello **входные данные** области, нажмите кнопку **добавить**и нажмите ВВОД hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="5dbbe-134">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="5dbbe-135">**Входной псевдоним**: hello уникальный псевдоним для hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-135">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="5dbbe-136">**Источник**. Выберите **Центр Интернета вещей**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="5dbbe-137">**Группа потребителей**: только что созданную группу потребителей выберите hello.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-137">**Consumer group**: Select hello consumer group you just created.</span></span>
1. <span data-ttu-id="5dbbe-138">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-138">Click **Create**.</span></span>

   ![Добавить задание Stream Analytics ввода tooa в Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="5dbbe-140">Добавление выходных данных задания Stream Analytics toohello</span><span class="sxs-lookup"><span data-stu-id="5dbbe-140">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="5dbbe-141">В разделе **Топология задания** щелкните **Выходные данные**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="5dbbe-142">В hello **выходные данные** области, нажмите кнопку **добавить**и нажмите ВВОД hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="5dbbe-142">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="5dbbe-143">**Псевдоним вывода**: hello уникальный псевдоним для выходной hello.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-143">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="5dbbe-144">**Приемник**. Выберите **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="5dbbe-145">Щелкните **Авторизовать**, а затем выполните вход в учетную запись Power BI.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="5dbbe-146">После авторизации введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="5dbbe-146">Once authorized, enter hello following information:</span></span>

   <span data-ttu-id="5dbbe-147">**Рабочая область группы**. Выберите целевую рабочую область группы.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="5dbbe-148">**Имя набора данных**. Введите имя набора данных.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="5dbbe-149">**Имя таблицы**. Введите имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="5dbbe-150">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-150">Click **Create**.</span></span>

   ![Добавить задание Stream Analytics tooa выходные данные в Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="5dbbe-152">Настройка запроса hello задания Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="5dbbe-152">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="5dbbe-153">В разделе **Топология задания** щелкните **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="5dbbe-154">Замените `[YourInputAlias]` с псевдонимом входного hello hello задания.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-154">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>
1. <span data-ttu-id="5dbbe-155">Замените `[YourOutputAlias]` с Псевдоним выхода hello hello задания.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-155">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>
1. <span data-ttu-id="5dbbe-156">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-156">Click **Save**.</span></span>

   ![Добавить задание Stream Analytics tooa запросов в Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="5dbbe-158">Запустить задание Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="5dbbe-158">Run hello Stream Analytics job</span></span>

<span data-ttu-id="5dbbe-159">В задании Stream Analytics hello, нажмите кнопку **запустить** > **теперь** > **запустить**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-159">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="5dbbe-160">После успешного запуска задания hello hello состояние задания меняется с **остановлена** слишком**под управлением**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-160">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Выполнение задания Stream Analytics в Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a><span data-ttu-id="5dbbe-162">Создание и публикация данных hello toovisualize отчета Power BI</span><span class="sxs-lookup"><span data-stu-id="5dbbe-162">Create and publish a Power BI report toovisualize hello data</span></span>

1. <span data-ttu-id="5dbbe-163">Убедитесь, что приложение hello образец выполняется на устройстве.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-163">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="5dbbe-164">Если нет, можно ссылаться учебники toohello в разделе [настроить на устройстве](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="5dbbe-164">If not, you can refer toohello tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="5dbbe-165">Войдите в tooyour [Power BI](https://powerbi.microsoft.com/en-us/) учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-165">Sign in tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="5dbbe-166">Перейдите в рабочую область группы toohello, заданное при создании hello вывода для задания Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-166">Go toohello group workspace that you set when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="5dbbe-167">Щелкните **Потоковая передача наборов данных**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="5dbbe-168">Вы увидите hello в списке набора данных, который был указан при создании hello вывода для задания Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-168">You should see hello listed dataset that you specified when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="5dbbe-169">В разделе **действия**, щелкните первый hello toocreate значок отчета.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-169">Under **ACTIONS**, click hello first icon toocreate a report.</span></span>

   ![Создание отчета Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="5dbbe-171">Создание строки температуры в режиме реального времени диаграммы tooshow со временем.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-171">Create a line chart tooshow real-time temperature over time.</span></span>
   1. <span data-ttu-id="5dbbe-172">На странице создания отчета hello добавьте линейчатую диаграмму.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-172">On hello report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="5dbbe-173">На hello **поля** области, разверните таблицу hello, указанный при создании hello вывода для задания Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-173">On hello **Fields** pane, expand hello table that you specified when you created hello output for hello Stream Analytics job.</span></span>
   1. <span data-ttu-id="5dbbe-174">Перетащите **EventEnqueuedUtcTime** слишком**оси** на hello **визуализации** области.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-174">Drag **EventEnqueuedUtcTime** too**Axis** on hello **Visualizations** pane.</span></span>
   1. <span data-ttu-id="5dbbe-175">Перетащите **температуры** слишком**значения**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-175">Drag **temperature** too**Values**.</span></span>

      <span data-ttu-id="5dbbe-176">График создан.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-176">Now a line chart is created.</span></span> <span data-ttu-id="5dbbe-177">ось x Hello отображает дату и время в часовом поясе UTC hello.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-177">hello x-axis displays date and time in hello UTC time zone.</span></span> <span data-ttu-id="5dbbe-178">ось y Hello отображает температуру из hello датчика.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-178">hello y-axis displays temperature from hello sensor.</span></span>

      ![Добавление графика для tooa температуры отчете Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="5dbbe-180">Создайте другой линии диаграммы tooshow в режиме реального времени влажности со временем.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-180">Create another line chart tooshow real-time humidity over time.</span></span> <span data-ttu-id="5dbbe-181">toodo это, выполните же шаги выше hello и поместите **EventEnqueuedUtcTime** по оси x hello и **влажность** на оси y hello.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-181">toodo this, follow hello same steps above and place **EventEnqueuedUtcTime** on hello x-axis and **humidity** on hello y-axis.</span></span>

   ![Добавление графика для tooa влажность отчете Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="5dbbe-183">Нажмите кнопку **Сохранить** toosave hello отчета.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-183">Click **Save** toosave hello report.</span></span>
1. <span data-ttu-id="5dbbe-184">Нажмите кнопку **файл** > **публикации tooweb**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-184">Click **File** > **Publish tooweb**.</span></span>
1. <span data-ttu-id="5dbbe-185">Щелкните **Создать код внедрения**, а затем выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="5dbbe-186">Введенный hello ссылка на отчет, вы можете совместно использовать с любой пользователь, для доступа к отчетам и отчет hello toointegrate фрагмент кода в блоге или на веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-186">You're provided hello report link that you can share with anyone for report access and a code snippet toointegrate hello report into your blog or website.</span></span>

![Публикация отчета Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="5dbbe-188">Корпорация Майкрософт также предлагает hello [мобильных приложений Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) для просмотра и взаимодействия с помощью панелей мониторинга и отчеты на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-188">Microsoft also offers hello [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dbbe-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5dbbe-189">Next steps</span></span>

<span data-ttu-id="5dbbe-190">Данные в режиме реального времени датчиков toovisualize Power BI вы использовали успешно из вашего центра Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-190">You’ve successfully used Power BI toovisualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="5dbbe-191">Отсутствуют данные toovisualize альтернативный способ из центра IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="5dbbe-191">There is an alternate way toovisualize data from Azure IoT Hub.</span></span> <span data-ttu-id="5dbbe-192">В разделе [веб-приложениях Azure используйте toovisualize в режиме реального времени датчиков из центра IoT Azure](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="5dbbe-192">See [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
