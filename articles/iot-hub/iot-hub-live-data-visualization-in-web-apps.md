---
title: "Визуализация данных времени aaaReal датчиков данных из вашего центра Azure IoT — веб-приложений | Документы Microsoft"
description: "Используйте функцию службу приложений Microsoft Azure toovisualize температуры и влажности данные, полученные от датчика hello и отправляются в центр Iot tooyour hello веб-приложений."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "визуализация данных, полученных в реальном времени, визуализация интерактивных данных, визуализация данных датчиков"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="3e5d5-104">Визуализация данных датчика в режиме реального времени из вашего центра Azure IoT с помощью функции hello веб-приложениях службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="3e5d5-104">Visualize real-time sensor data from your Azure IoT hub by using hello Web Apps feature of Azure App Service</span></span>

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="3e5d5-106">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="3e5d5-106">What you learn</span></span>

<span data-ttu-id="3e5d5-107">В этом учебнике вы узнаете, как toovisualize в режиме реального времени датчиков, получающий концентратор IoT путем запуска веб-приложения, размещенного на веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-107">In this tutorial, you learn how toovisualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="3e5d5-108">Если вам нужны данные hello toovisualize tootry в ваш центр IoT с помощью Power BI, см. раздел [данных датчика в режиме реального времени toovisualize используйте Power BI из центра IoT Azure](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="3e5d5-108">If you want tootry toovisualize hello data in your IoT hub by using Power BI, see [Use Power BI toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3e5d5-109">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="3e5d5-109">What you do</span></span>

- <span data-ttu-id="3e5d5-110">Создание веб-приложения в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-110">Create a web app in hello Azure portal.</span></span>
- <span data-ttu-id="3e5d5-111">добавим группу потребителей, чтобы обеспечить доступ к данным в Центре Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="3e5d5-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="3e5d5-112">Настройте hello web app tooread датчиков из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-112">Configure hello web app tooread sensor data from your IoT hub.</span></span>
- <span data-ttu-id="3e5d5-113">Отправьте toobe приложения web, расположенных на веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-113">Upload a web application toobe hosted by hello web app.</span></span>
- <span data-ttu-id="3e5d5-114">Откройте hello веб-приложения toosee в режиме реального времени температуры и влажности данных из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-114">Open hello web app toosee real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3e5d5-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="3e5d5-115">What you need</span></span>

- <span data-ttu-id="3e5d5-116">[Настройка устройства](iot-hub-raspberry-pi-kit-node-get-started.md), который охватывает hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="3e5d5-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers hello following requirements:</span></span>
  - <span data-ttu-id="3e5d5-117">активная подписка Azure;</span><span class="sxs-lookup"><span data-stu-id="3e5d5-117">An active Azure subscription</span></span>
  - <span data-ttu-id="3e5d5-118">Центр Интернета вещей в подписке;</span><span class="sxs-lookup"><span data-stu-id="3e5d5-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="3e5d5-119">Клиентское приложение, которое отправляет сообщения tooyour Iot hub</span><span class="sxs-lookup"><span data-stu-id="3e5d5-119">A client application that sends messages tooyour Iot hub</span></span>
- <span data-ttu-id="3e5d5-120">[Скачайте Git](https://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="3e5d5-120">[Download Git](https://www.git-scm.com/downloads)</span></span>

## <a name="create-a-web-app"></a><span data-ttu-id="3e5d5-121">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="3e5d5-121">Create a web app</span></span>

1. <span data-ttu-id="3e5d5-122">В hello [портал Azure](https://ms.portal.azure.com/), нажмите кнопку **New** > **Интернет + мобильные устройства** > **веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-122">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="3e5d5-123">Введите имя задания уникальных проверьте hello подписки, укажите группу ресурсов и расположение, выберите **toodashboard ПИН-код**, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-123">Enter a unique job name, verify hello subscription, specify a resource group and a location, select **Pin toodashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="3e5d5-124">Рекомендуется выбирать hello же расположении, что и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-124">We recommend that you select hello same location as that of your resource group.</span></span> <span data-ttu-id="3e5d5-125">Это помогает выполнять скорость обработки и снижает затраты hello передачи данных.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-125">Doing so assists with processing speed and reduces hello cost of data transfer.</span></span>

   ![Создание веб-приложения](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a><span data-ttu-id="3e5d5-127">Настройка hello веб-приложения tooread данных из вашего центра IoT</span><span class="sxs-lookup"><span data-stu-id="3e5d5-127">Configure hello web app tooread data from your IoT hub</span></span>

1. <span data-ttu-id="3e5d5-128">Откройте веб-приложения hello, который только что провизионировал.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-128">Open hello web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="3e5d5-129">Нажмите кнопку **параметры приложения**, а затем на вкладке **параметры приложения**, добавить следующие пары "ключ значение" hello:</span><span class="sxs-lookup"><span data-stu-id="3e5d5-129">Click **Application settings**, and then, under **App settings**, add hello following key/value pairs:</span></span>

   | <span data-ttu-id="3e5d5-130">Ключ</span><span class="sxs-lookup"><span data-stu-id="3e5d5-130">Key</span></span>                                   | <span data-ttu-id="3e5d5-131">Значение</span><span class="sxs-lookup"><span data-stu-id="3e5d5-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="3e5d5-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="3e5d5-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="3e5d5-133">Получено из обозревателя Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="3e5d5-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="3e5d5-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="3e5d5-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="3e5d5-135">Имя группы потребителей hello добавления центра IoT tooyour Hello</span><span class="sxs-lookup"><span data-stu-id="3e5d5-135">hello name of hello consumer group that you add tooyour IoT hub</span></span>  |

   ![Добавить параметры tooyour веб-приложения с парами «ключ значение»](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="3e5d5-137">Нажмите кнопку **параметры приложения**в разделе **Общие параметры**, переключение hello **веб-сокеты** , а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-137">Click **Application settings**, under **General settings**, toggle hello **Web sockets** option, and then click **Save**.</span></span>

   ![Переключить режим сокеты hello Web](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a><span data-ttu-id="3e5d5-139">Отправка toobe приложения web, расположенных на веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="3e5d5-139">Upload a web application toobe hosted by hello web app</span></span>

<span data-ttu-id="3e5d5-140">Теперь веб-приложение доступно в GitHub. В нем отображаются данные, поступающие с датчиков в реальном времени, из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="3e5d5-141">Все, что нужно toodo — настройки hello web app toowork с репозиторием Git, загрузка веб-приложения hello из GitHub и затем передать его tooAzure для toohost приложения hello web.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-141">All you need toodo is configure hello web app toowork with a Git repository, download hello web application from GitHub, and then upload it tooAzure for hello web app toohost.</span></span>

1. <span data-ttu-id="3e5d5-142">В веб-приложения hello, нажмите кнопку **варианты развертывания** > **Выбор источника** > **локального репозитория Git**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-142">In hello web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![Настройка web app развертывания toouse hello локальный репозиторий Git](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="3e5d5-144">Нажмите кнопку **учетные данные развертывания**, создайте пользователя имя и пароль toouse tooconnect toohello репозитории в Azure и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-144">Click **Deployment Credentials**, create a user name and password toouse tooconnect toohello Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="3e5d5-145">Нажмите кнопку **Обзор**и запишите значение hello **URL-адрес клонирования Git**.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-145">Click **Overview**, and note hello value of **Git clone url**.</span></span>

   ![Получить URL-адрес клона Git hello веб-приложения](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="3e5d5-147">Откройте окно терминала или командной строки на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="3e5d5-148">Загрузите веб-приложения hello из GitHub и отправьте его tooAzure для toohost приложения hello web.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-148">Download hello web app from GitHub, and upload it tooAzure for hello web app toohost.</span></span> <span data-ttu-id="3e5d5-149">toodo таким образом, выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-149">toodo so, run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="3e5d5-150">\<URL-адрес клона Git\> hello URL-адрес репозитория Git hello, найденных на hello **Обзор** страницы приветствия веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-150">\<Git clone URL\> is hello URL of hello Git repository found on hello **Overview** page of hello web app.</span></span>

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="3e5d5-151">Откройте hello веб-приложения toosee в режиме реального времени температуры и влажности данных из вашего центра IoT</span><span class="sxs-lookup"><span data-stu-id="3e5d5-151">Open hello web app toosee real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="3e5d5-152">На hello **Обзор** страницы веб-приложения, нажмите кнопку hello URL-адрес tooopen hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-152">On hello **Overview** page of your web app, click hello URL tooopen hello web app.</span></span>

![Получить hello URL-адрес веб-приложения](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="3e5d5-154">Вы увидите hello в режиме реального времени температуры и влажности данные из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-154">You should see hello real-time temperature and humidity data from your IoT hub.</span></span>

![Страница веб-приложения с данными о температуре и влажности, полученными в реальном времени](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="3e5d5-156">Убедитесь, что приложение hello образец выполняется на устройстве.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-156">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="3e5d5-157">Если нет, вы получите пустую диаграмму, можно обратиться учебники toohello под [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3e5d5-157">If not, you will get a blank chart, you can refer toohello tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e5d5-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3e5d5-158">Next steps</span></span>
<span data-ttu-id="3e5d5-159">Успешно вы использовали данные в режиме реального времени датчика toovisualize web приложений из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="3e5d5-159">You've successfully used your web app toovisualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="3e5d5-160">Альтернативный способ toovisualize данные из центра IoT Azure, см. [используйте Power BI toovisualize датчика в режиме реального времени, данные из вашего центра IoT](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="3e5d5-160">For an alternative way toovisualize data from Azure IoT Hub, see [Use Power BI toovisualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
