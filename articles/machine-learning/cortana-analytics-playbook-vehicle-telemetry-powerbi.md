---
title: "aaaPower мониторинга бизнес-Аналитики за vehicle работоспособности и управление им привычки - Azure | Документы Microsoft"
description: "Использовать возможности hello toogain Cortana аналитики в реальном времени и прогнозной аналитики на автомобиль работоспособности и пешком привычки."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="f711f-103">Инструкции по настройке информационной панели Power BI шаблона решения для аналитики телеметрии автомобилей</span><span class="sxs-lookup"><span data-stu-id="f711f-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="f711f-104">Это **меню** toohello главах этого репертуара ссылки.</span><span class="sxs-lookup"><span data-stu-id="f711f-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="f711f-105">решения для анализа телеметрии Vehicle Hello демонстрирует, как дилеров автомобиля, автомобиль производители и страховых компаний могут использовать возможности hello средств аналитики Cortana toogain в режиме реального времени и прогнозирующего анализа работоспособности транспортного средства и управление им Усовершенствования toodrive привычки hello области клиента возникают, R & D и маркетинговых кампаний.</span><span class="sxs-lookup"><span data-stu-id="f711f-105">hello Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits toodrive improvements in hello area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="f711f-106">Этот документ содержит инструкции по настройке hello Power BI отчеты и панели мониторинга после развертывания решения hello в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="f711f-106">This document contains step by step instructions on how you can configure hello Power BI reports and dashboard once hello solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f711f-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f711f-107">Prerequisites</span></span>
1. <span data-ttu-id="f711f-108">Развертывание hello [Analytics телеметрии](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) решения</span><span class="sxs-lookup"><span data-stu-id="f711f-108">Deploy hello [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="f711f-109">Установите Microsoft Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="f711f-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="f711f-110">[Подписка Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f711f-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="f711f-111">Если у вас нет подписки Azure, для начала получите бесплатную подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="f711f-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="f711f-112">Учетная запись Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="f711f-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="f711f-113">Компоненты Cortana Intelligence Suite</span><span class="sxs-lookup"><span data-stu-id="f711f-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="f711f-114">Как часть шаблона решения транспортных средств телеметрии Analytics hello следующие службы аналитики Cortana hello развертываются в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="f711f-114">As part of hello Vehicle Telemetry Analytics solution template, hello following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="f711f-115">**Концентратор событий** принимает миллионы событий телеметрии автомобилей в Azure.</span><span class="sxs-lookup"><span data-stu-id="f711f-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="f711f-116">**Stream Analytics** получает данные аналитики о работоспособности автомобиля в режиме реального времени и сохраняет их в долговременное хранилище для более детальной пакетной аналитики.</span><span class="sxs-lookup"><span data-stu-id="f711f-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="f711f-117">**Машинное Обучение** для обнаружения аномалий в режиме реального времени и пакетной обработки toogain прогнозной аналитики.</span><span class="sxs-lookup"><span data-stu-id="f711f-117">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="f711f-118">**HDInsight** tootransform использовать данные в масштабе</span><span class="sxs-lookup"><span data-stu-id="f711f-118">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="f711f-119">**Фабрика данных** обрабатывает orchestration, планирование, управление ресурсами и мониторинг hello конвейера обработки пакета.</span><span class="sxs-lookup"><span data-stu-id="f711f-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>

<span data-ttu-id="f711f-120">**Power BI** предоставляет для этого решения расширенную панель мониторинга для визуализации данных в режиме реального времени и прогнозной аналитики.</span><span class="sxs-lookup"><span data-stu-id="f711f-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="f711f-121">Hello решение использует два различных источников данных: **имитируемые vehicle сигналы и набор диагностических данных** и **vehicle каталога**.</span><span class="sxs-lookup"><span data-stu-id="f711f-121">hello solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="f711f-122">В это решение входит симулятор телематики автомобиля.</span><span class="sxs-lookup"><span data-stu-id="f711f-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="f711f-123">Он выдает диагностических сведений и сообщает состояние соответствующего toohello hello vehicle и определяющим шаблон в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="f711f-123">It emits diagnostic information and signals corresponding toohello state of hello vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="f711f-124">Hello Vehicle каталог представляет собой справочник по набора данных содержащего VIN toomodel сопоставление</span><span class="sxs-lookup"><span data-stu-id="f711f-124">hello Vehicle Catalog is a reference dataset containing VIN toomodel mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="f711f-125">Подготовка информационной панели Power BI</span><span class="sxs-lookup"><span data-stu-id="f711f-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="f711f-126">Настройка панели мониторинга Power BI в реальном времени</span><span class="sxs-lookup"><span data-stu-id="f711f-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="f711f-127">**Запустите приложение в режиме реального времени мониторинга hello** после завершения развертывания hello, необходимо выполнить инструкции по эксплуатации hello вручную</span><span class="sxs-lookup"><span data-stu-id="f711f-127">**Start hello real-time dashboard application** Once hello deployment is completed, you should follow hello Manual Operation Instructions</span></span>

* <span data-ttu-id="f711f-128">Скачайте файл RealtimeDashboardApp.zip с приложением панели мониторинга в режиме реального времени и распакуйте его.</span><span class="sxs-lookup"><span data-stu-id="f711f-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="f711f-129">В распакованную папку hello откройте файл конфигурации приложения «RealtimeDashboardApp.exe.config» replace appSettings для соединений службы Eventhub хранилища больших двоичных объектов и ML со значениями hello в hello инструкции операции вручную и сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="f711f-129">In hello unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with hello values in hello Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="f711f-130">Запустите приложение RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="f711f-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="f711f-131">Окно входа будет всплывающее окно, допустимым PowerBI учетные данные и нажмите кнопку hello **Accept** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f711f-131">A login window will pop up, provide your valid PowerBI credentials and click hello **Accept** button.</span></span> <span data-ttu-id="f711f-132">Затем приложение hello начнется toorun.</span><span class="sxs-lookup"><span data-stu-id="f711f-132">Then hello app will start toorun.</span></span>

   ![Вход tooPower бизнес-Аналитики](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Разрешения для информационной панели Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="f711f-135">Веб-сайт tooPowerBI входа в систему и создать панель мониторинга в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="f711f-135">Login tooPowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="f711f-136">Теперь вы являетесь панели мониторинга Power BI готов tooconfigure hello с широкими возможностями визуализации toogain в режиме реального времени и привычки прогнозной аналитики на автомобиль работоспособности и управление им.</span><span class="sxs-lookup"><span data-stu-id="f711f-136">Now, you are ready tooconfigure hello Power BI dashboard with rich visualizations toogain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="f711f-137">Занимает около 45 минут tooan час toocreate hello все отчеты и настройка панели hello.</span><span class="sxs-lookup"><span data-stu-id="f711f-137">It takes about 45 minutes tooan hour toocreate all hello reports and configure hello dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="f711f-138">Настройка отчетов Power BI</span><span class="sxs-lookup"><span data-stu-id="f711f-138">Configure Power BI reports</span></span>
<span data-ttu-id="f711f-139">Hello в режиме реального времени отчеты и панели мониторинга hello занимает приблизительно toocomplete 30 – 45 минут.</span><span class="sxs-lookup"><span data-stu-id="f711f-139">hello real-time reports and hello dashboard take about 30-45 minutes toocomplete.</span></span> <span data-ttu-id="f711f-140">Обзор слишком[http://powerbi.com](http://powerbi.com) и имя входа.</span><span class="sxs-lookup"><span data-stu-id="f711f-140">Browse too[http://powerbi.com](http://powerbi.com) and login.</span></span>

![Вход tooPower бизнес-Аналитики](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="f711f-142">В Power BI создается новый набор данных.</span><span class="sxs-lookup"><span data-stu-id="f711f-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="f711f-143">Нажмите кнопку hello **ConnectedCarsRealtime** набора данных.</span><span class="sxs-lookup"><span data-stu-id="f711f-143">Click hello **ConnectedCarsRealtime** dataset.</span></span>

![Выберите набор данных подключенных автомобилей в реальном времени](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="f711f-145">Сохранить с помощью пустого отчета hello **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="f711f-145">Save hello blank report using **Ctrl + s**.</span></span>

![Сохраните пустой отчет.](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="f711f-147">Введите для отчета имя *Аналитика телеметрии автомобилей в реальном времени: отчеты*.</span><span class="sxs-lookup"><span data-stu-id="f711f-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Присвойте имя отчету.](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="f711f-149">Отчеты в реальном времени</span><span class="sxs-lookup"><span data-stu-id="f711f-149">Real-time reports</span></span>
<span data-ttu-id="f711f-150">Это решение включает три отчета в реальном времени, описывающие:</span><span class="sxs-lookup"><span data-stu-id="f711f-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="f711f-151">исправные автомобили;</span><span class="sxs-lookup"><span data-stu-id="f711f-151">Vehicles in operation</span></span>
2. <span data-ttu-id="f711f-152">автомобили, которым требуется обслуживание;</span><span class="sxs-lookup"><span data-stu-id="f711f-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="f711f-153">Статистика работоспособности автомобилей</span><span class="sxs-lookup"><span data-stu-id="f711f-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="f711f-154">Можно выбрать tooconfigure всех отчетов в режиме реального времени hello для трех или остановить после любой стадии и вы toohello Настройка отчетов пакета hello следующего раздела.</span><span class="sxs-lookup"><span data-stu-id="f711f-154">You can choose tooconfigure all hello three real-time reports or stop after any stage and proceed toohello next section of configuring hello batch reports.</span></span> <span data-ttu-id="f711f-155">Мы рекомендуем toocreate всех трех hello сообщает toovisualize hello полный аналитики hello в режиме реального времени пути решения hello.</span><span class="sxs-lookup"><span data-stu-id="f711f-155">We recommend you toocreate all hello three reports toovisualize hello full insights of hello real-time path of hello solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="f711f-156">1. исправные автомобили;</span><span class="sxs-lookup"><span data-stu-id="f711f-156">1. Vehicles in operation</span></span>
<span data-ttu-id="f711f-157">Дважды щелкните **страница 1** и переименуйте его слишком «Транспортных средств в операции»</span><span class="sxs-lookup"><span data-stu-id="f711f-157">Double-click **Page 1** and rename it too“Vehicles in operation”</span></span>  
    <span data-ttu-id="f711f-158">![Подключенные автомобили — исправные автомобили](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="f711f-159">В разделе **Поля** выберите поле **VIN** и укажите тип визуализации **Карточка**.</span><span class="sxs-lookup"><span data-stu-id="f711f-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="f711f-160">Создается карточка визуализации, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="f711f-160">Card visualization is created as shown in figure.</span></span>  
    ![Подключенные автомобили — выберите номер шасси](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="f711f-162">Щелкните новую визуализацию hello пустую область tooadd.</span><span class="sxs-lookup"><span data-stu-id="f711f-162">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f711f-163">Выберите поля **Город** и **VIN**.</span><span class="sxs-lookup"><span data-stu-id="f711f-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="f711f-164">Измените визуализацию слишком**«Карта»**.</span><span class="sxs-lookup"><span data-stu-id="f711f-164">Change visualization too**“Map”**.</span></span> <span data-ttu-id="f711f-165">Перетащите поле **VIN** в область значений.</span><span class="sxs-lookup"><span data-stu-id="f711f-165">Drag **vin** in values area.</span></span> <span data-ttu-id="f711f-166">Перетащите **Город** из полей слишком**условных обозначений** области.</span><span class="sxs-lookup"><span data-stu-id="f711f-166">Drag **city** from fields too**Legend** area.</span></span>   
    <span data-ttu-id="f711f-167">![Подключенные автомобили — визуализация "Карточка"](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="f711f-168">Выберите **формат** статьи **визуализации**, нажмите кнопку **заголовок** и измените hello **текст** слишком**автомобилей» в Операция по городу»**.</span><span class="sxs-lookup"><span data-stu-id="f711f-168">Select **format** section from **Visualizations**, click **Title** and change hello **Text** too**“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="f711f-169">![Подключенные автомобили — исправные автомобили по городам](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="f711f-170">Визуализация будет выглядеть, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="f711f-170">Final visualization looks as shown in figure.</span></span>    
    ![Подключенные автомобили — итоговая визуализация](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="f711f-172">Щелкните новую визуализацию hello пустую область tooadd.</span><span class="sxs-lookup"><span data-stu-id="f711f-172">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f711f-173">Выберите **Город** и **vin**, измените тип визуализации слишком**гистограмму с группировкой**.</span><span class="sxs-lookup"><span data-stu-id="f711f-173">Select **City** and **vin**, change visualization type too**Clustered Column Chart**.</span></span> <span data-ttu-id="f711f-174">Убедитесь, что поле **Город** размещено в области **Ось**, а **VIN** — в области **Значение**.</span><span class="sxs-lookup"><span data-stu-id="f711f-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="f711f-175">Отсортируйте гистограмму по параметру **Count of vin** (Количество VIN).</span><span class="sxs-lookup"><span data-stu-id="f711f-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="f711f-176">![Подключенные автомобили — количество номеров шасси](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="f711f-177">Изменение диаграммы **заголовок** слишком**«Транспортных средств в операции по городам»**</span><span class="sxs-lookup"><span data-stu-id="f711f-177">Change chart **Title** too**“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="f711f-178">Нажмите кнопку hello **формат** статьи, а затем выберите **цвета данных**, щелкните hello **«На»** слишком**Показать все**</span><span class="sxs-lookup"><span data-stu-id="f711f-178">Click hello **Format** section, then select **Data Colors**,  Click hello **“On”** too**Show All**</span></span>  
    <span data-ttu-id="f711f-179">![Подключенные автомобили — отображение всех цветов данных](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="f711f-180">Измените цвет hello отдельные города, щелкнув значок цвета.</span><span class="sxs-lookup"><span data-stu-id="f711f-180">Change hello color of individual city by clicking on color icon.</span></span>  
    ![Подключенные автомобили — изменение цветов](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="f711f-182">Щелкните новую визуализацию hello пустую область tooadd.</span><span class="sxs-lookup"><span data-stu-id="f711f-182">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f711f-183">Выберите тип визуализации **Гистограмма с группировкой**, перетащите поле **Город** в область **Ось**, поле **Модель** — в область **Условные обозначения**, а поле **VIN** — в область **Значение**.</span><span class="sxs-lookup"><span data-stu-id="f711f-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="f711f-184">![Подключенные автомобили — кластеризованная гистограмма](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="f711f-185">![Подключенные автомобили — отрисовка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="f711f-186">Измените визуальное представление на странице, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="f711f-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Подключенные автомобили — визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="f711f-188">В режиме реального времени отчета «Транспортных средств в операции» hello успешно настроена.</span><span class="sxs-lookup"><span data-stu-id="f711f-188">You have successfully configured hello “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="f711f-189">Можно продолжить toocreate hello в режиме реального времени отчет или пропустить и настройки мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="f711f-189">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="f711f-190">2. автомобили, которым требуется обслуживание;</span><span class="sxs-lookup"><span data-stu-id="f711f-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="f711f-191">Нажмите кнопку ![добавить](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd нового отчета, переименуйте его слишком**«Автомобилей требует Maintenance»**</span><span class="sxs-lookup"><span data-stu-id="f711f-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd a new report, rename it too**“Vehicles Requiring Maintenance”**</span></span>

![Подключенные автомобили — автомобили, требующие обслуживания](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="f711f-193">Выберите **vin** и измените тип визуализации слишком**карты**.</span><span class="sxs-lookup"><span data-stu-id="f711f-193">Select **vin** field and change visualization type too**Card**.</span></span>  
    <span data-ttu-id="f711f-194">![Подключенные автомобили — визуализация "Карточка номера шасси"](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="f711f-195">У нас есть поле с именем «MaintenanceLabel» в наборе данных hello.</span><span class="sxs-lookup"><span data-stu-id="f711f-195">We have a field named “MaintenanceLabel” In hello dataset.</span></span> <span data-ttu-id="f711f-196">Это поле может иметь значение 0 или 1.</span><span class="sxs-lookup"><span data-stu-id="f711f-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="f711f-197">Он задается модели машинного обучения Azure hello подготовить как часть решения и интегрированные в путь в реальном времени hello.</span><span class="sxs-lookup"><span data-stu-id="f711f-197">It is set by hello Azure Machine Learning model provisioned as part of solution and integrated with hello real-time path.</span></span> <span data-ttu-id="f711f-198">Hello значение «1» указывает, что транспортного средства требуется его обслуживание.</span><span class="sxs-lookup"><span data-stu-id="f711f-198">hello value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="f711f-199">tooadd **уровне страниц** фильтр для отображения данных автомобилей, который, которым обслуживания:</span><span class="sxs-lookup"><span data-stu-id="f711f-199">tooadd a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="f711f-200">Перетащите hello **«MaintenanceLabel»** в **фильтры уровня страницы**.</span><span class="sxs-lookup"><span data-stu-id="f711f-200">Drag hello **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="f711f-201">![Подключенные автомобили — фильтры уровня страницы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="f711f-202">В нижней части фильтра уровня страницы MaintenanceLabel щелкните меню **Простая фильтрация** .</span><span class="sxs-lookup"><span data-stu-id="f711f-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="f711f-203">![Подключенные автомобили — базовая фильтрация](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="f711f-204">Присвойте ему значение фильтра слишком**«1»**  </span><span class="sxs-lookup"><span data-stu-id="f711f-204">Set its filter value too**“1”**  </span></span>  
   <span data-ttu-id="f711f-205">![Подключенные автомобили — значение фильтра](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="f711f-206">Щелкните новую визуализацию hello пустую область tooadd.</span><span class="sxs-lookup"><span data-stu-id="f711f-206">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f711f-207">Выберите тип визуализации **Гистограмма с группировкой**.</span><span class="sxs-lookup"><span data-stu-id="f711f-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="f711f-208">![Подключенные автомобили — визуализация «Карточка номера шасси»](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="f711f-209">![Подключенные автомобили — кластеризованная гистограмма](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="f711f-210">Перетащите поле **модель** в **оси** область, **Vin** слишком**значение** области.</span><span class="sxs-lookup"><span data-stu-id="f711f-210">Drag field **Model** into **Axis** area, **Vin** too**Value** area.</span></span> <span data-ttu-id="f711f-211">Отсортируйте визуализацию по параметру **Количество VIN**.</span><span class="sxs-lookup"><span data-stu-id="f711f-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="f711f-212">Изменение диаграммы **заголовок** слишком**«Транспортных средств требуется обслуживание модели»**</span><span class="sxs-lookup"><span data-stu-id="f711f-212">Change chart **Title** too**“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="f711f-213">Перетащите поля **VIN** в область **Насыщенность цвета** (раздел **Поля** ![Поля](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) на вкладке **Визуализация**).</span><span class="sxs-lookup"><span data-stu-id="f711f-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="f711f-214">![Подключенные автомобили — насыщенность цвета](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="f711f-215">Измените тип визуализации параметра **Цвета данных** из раздела **Формат**.</span><span class="sxs-lookup"><span data-stu-id="f711f-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="f711f-216">Измените минимальное значение цвета на **F2C812**.</span><span class="sxs-lookup"><span data-stu-id="f711f-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="f711f-217">Измените максимальное значение цвета на **FF6300**.</span><span class="sxs-lookup"><span data-stu-id="f711f-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="f711f-218">![Подключенные автомобили — изменения цвета](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="f711f-219">![Подключенные автомобили — новые цвета визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="f711f-220">Щелкните новую визуализацию hello пустую область tooadd.</span><span class="sxs-lookup"><span data-stu-id="f711f-220">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f711f-221">Выберите тип визуализации **Гистограмма с группировкой**. Затем перетащите поле **VIN** в область **Значение**, а поле **Город** — в область **Ось**.</span><span class="sxs-lookup"><span data-stu-id="f711f-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="f711f-222">Отсортируйте гистограмму по параметру **Count of vin** (Количество VIN).</span><span class="sxs-lookup"><span data-stu-id="f711f-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="f711f-223">Изменение диаграммы **заголовок** слишком**«Автомобилей, требующие обслуживания по городам»** </span><span class="sxs-lookup"><span data-stu-id="f711f-223">Change chart **Title** too**“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="f711f-224">![Подключенные автомобили — автомобили, требующие обслуживания, по городам](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="f711f-225">Щелкните новую визуализацию hello пустую область tooadd.</span><span class="sxs-lookup"><span data-stu-id="f711f-225">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f711f-226">Выберите **многострочных карточек** визуализации из визуализаций, перетащите **модель** и **vin** в hello **поля** области.</span><span class="sxs-lookup"><span data-stu-id="f711f-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into hello **Fields** area.</span></span>  
<span data-ttu-id="f711f-227">![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="f711f-228">Реорганизовать все визуализации hello, hello окончательный отчет выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f711f-228">Rearranging all of hello visualization, hello final report looks as follows:</span></span>  
![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="f711f-230">Отчет в режиме реального времени «Автомобилей требует обслуживания» hello успешно настроена.</span><span class="sxs-lookup"><span data-stu-id="f711f-230">You have successfully configured hello “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="f711f-231">Можно продолжить toocreate hello в режиме реального времени отчет или пропустить и настройки мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="f711f-231">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="f711f-232">3. Статистика работоспособности автомобилей</span><span class="sxs-lookup"><span data-stu-id="f711f-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="f711f-233">Нажмите кнопку ![добавить](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd нового отчета, переименуйте его слишком**«Статистика транспортных средств работоспособности»**</span><span class="sxs-lookup"><span data-stu-id="f711f-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd new report, rename it too**“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="f711f-234">Выберите **датчика** визуализации из визуализаций, затем перетащите hello **скорость** в **значение, минимальное, максимальное значение** областей.</span><span class="sxs-lookup"><span data-stu-id="f711f-234">Select **Gauge** visualization from visualizations, then drag hello **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="f711f-235">![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="f711f-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="f711f-236">Изменение статистической обработки по умолчанию hello **скорость** в **значение области** слишком**среднее**</span><span class="sxs-lookup"><span data-stu-id="f711f-236">Change hello default aggregation of **speed** in **Value area** too**Average**</span></span> 

<span data-ttu-id="f711f-237">Изменение статистической обработки по умолчанию hello **скорость** в **область минимум** слишком**минимум**</span><span class="sxs-lookup"><span data-stu-id="f711f-237">Change hello default aggregation of **speed** in **Minimum area** too**Minimum**</span></span>

<span data-ttu-id="f711f-238">Изменение статистической обработки по умолчанию hello **скорость** в **область максимально** слишком**максимальное**</span><span class="sxs-lookup"><span data-stu-id="f711f-238">Change hello default aggregation of **speed** in **Maximum area** too**Maximum**</span></span>

![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="f711f-240">Переименование hello **заголовок датчика** слишком**«Средняя скорость»**</span><span class="sxs-lookup"><span data-stu-id="f711f-240">Rename hello **Gauge Title** too**“Average speed”**</span></span> 

![Подключенные автомобили — датчик](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="f711f-242">Щелкните новую визуализацию hello пустую область tooadd.</span><span class="sxs-lookup"><span data-stu-id="f711f-242">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="f711f-243">Аналогичным образом добавьте следующие **датчики**: **Среднее количество моторного масла**, **Среднее количество топлива** и **Средняя температура двигателя**.</span><span class="sxs-lookup"><span data-stu-id="f711f-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="f711f-244">Изменение статистической обработки по умолчанию hello полей в каждой шкалы с указанными выше действия, описанные в **«Средняя скорость»** датчика.</span><span class="sxs-lookup"><span data-stu-id="f711f-244">Change hello default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Подключенные автомобили — датчики](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="f711f-246">Щелкните новую визуализацию hello пустую область tooadd.</span><span class="sxs-lookup"><span data-stu-id="f711f-246">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="f711f-247">Выберите **строки и гистограмму с группировкой** из визуализаций, затем перетащите **Город** в **общей оси**, перетащите **скорость**, **поля tirepressure и engineoil** в **значения столбца** область, изменить их тип статистической обработки слишком**среднее**.</span><span class="sxs-lookup"><span data-stu-id="f711f-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type too**Average**.</span></span> 

<span data-ttu-id="f711f-248">Перетащите hello **engineTemperature** в **значения строки** область, измените тип статистической обработки hello слишком**среднее**.</span><span class="sxs-lookup"><span data-stu-id="f711f-248">Drag hello **engineTemperature** field into **Line Values** area, change hello  aggregation type too**Average**.</span></span> 

![Подключенные автомобили — поля визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="f711f-250">Изменение диаграммы hello **заголовок** слишком**«Среднее значение скорости, нагрузка велосипеда, engine нефти и температуры подсистемы»**.</span><span class="sxs-lookup"><span data-stu-id="f711f-250">Change hello chart **Title** too**“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Подключенные автомобили — поля визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="f711f-252">Щелкните новую визуализацию hello пустую область tooadd.</span><span class="sxs-lookup"><span data-stu-id="f711f-252">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="f711f-253">Выберите **древовидной диаграммы** визуализации из визуализаций, перетащите hello **модель** в hello **группы** области и перетащите поле hello  **MaintenanceProbability** в hello **значения** области.</span><span class="sxs-lookup"><span data-stu-id="f711f-253">Select **Treemap** visualization from visualizations, drag hello **Model** field into hello **Group** area, and drag hello field **MaintenanceProbability** into hello **Values** area.</span></span>

<span data-ttu-id="f711f-254">Изменение диаграммы hello **заголовок** слишком**«Vehicle моделей, требующие обслуживания»**.</span><span class="sxs-lookup"><span data-stu-id="f711f-254">Change hello chart **Title** too**“Vehicle models requiring maintenance”**.</span></span>

![Подключенные автомобили — изменение заголовка диаграммы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="f711f-256">Щелкните новую визуализацию hello пустую область tooadd.</span><span class="sxs-lookup"><span data-stu-id="f711f-256">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="f711f-257">Выберите **Нормированная линейчатая диаграмма** из визуализации, перетащите hello **Город** в hello **оси** области и перетащите hello **MaintenanceProbability**, **RecallProbability** полей с получением hello **значение** области.</span><span class="sxs-lookup"><span data-stu-id="f711f-257">Select **100% Stacked Bar Chart** from visualization, drag hello **city** field into hello **Axis** area, and drag hello **MaintenanceProbability**, **RecallProbability** fields into hello **Value** area.</span></span>

![Подключенные автомобили — добавление новой визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="f711f-259">Нажмите кнопку **формат**выберите **цвета данных**и набор hello **MaintenanceProbability** цвета значение toohello **«F2C80F»**.</span><span class="sxs-lookup"><span data-stu-id="f711f-259">Click **Format**, select **Data Colors**, and set hello **MaintenanceProbability** color toohello value **“F2C80F”**.</span></span>

<span data-ttu-id="f711f-260">Изменение hello **заголовок** из hello диаграммы слишком**«Вероятность из транспортного средства обслуживания & отозвать по городам»**.</span><span class="sxs-lookup"><span data-stu-id="f711f-260">Change hello **Title** of hello chart too**“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Подключенные автомобили — добавление новой визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="f711f-262">Щелкните новую визуализацию hello пустую область tooadd.</span><span class="sxs-lookup"><span data-stu-id="f711f-262">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="f711f-263">Выберите **диаграмма с областями** визуализации из визуализаций, перетащите hello **модель** в hello **оси** области и перетащите hello **engineOil, tirepressure, скорость и MaintenanceProbability** полей с получением hello **значения** области.</span><span class="sxs-lookup"><span data-stu-id="f711f-263">Select **Area Chart** from visualization from visualizations, drag hello **Model** field into hello **Axis** area, and drag hello **engineOil, tirepressure, speed and MaintenanceProbability** fields into hello **Values** area.</span></span> <span data-ttu-id="f711f-264">Изменить их тип статистической обработки слишком**«Среднее»**.</span><span class="sxs-lookup"><span data-stu-id="f711f-264">Change their aggregation type too**“Average”**.</span></span> 

![Подключенные автомобили — изменение типа агрегирования](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="f711f-266">Измените заголовок hello hello диаграммы слишком**«Среднее нефти ядра, tire вероятность давления, скорости и обслуживание модели»**.</span><span class="sxs-lookup"><span data-stu-id="f711f-266">Change hello title of hello chart too**“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Подключенные автомобили — изменение заголовка диаграммы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="f711f-268">Щелкните новую визуализацию hello пустую область tooadd:</span><span class="sxs-lookup"><span data-stu-id="f711f-268">Click hello blank area tooadd new visualization:</span></span>

1. <span data-ttu-id="f711f-269">Выберите тип визуализации **Точечная диаграмма** .</span><span class="sxs-lookup"><span data-stu-id="f711f-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="f711f-270">Перетащите hello **модель** в hello **сведения** и **условных обозначений** области.</span><span class="sxs-lookup"><span data-stu-id="f711f-270">Drag hello **Model** field into hello **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="f711f-271">Перетащите hello **топливо** в hello **оси x** область, измените агрегирования данных hello слишком**среднее**.</span><span class="sxs-lookup"><span data-stu-id="f711f-271">Drag hello **fuel** field into hello **X-Axis** area, change hello aggregation too**Average**.</span></span>
4. <span data-ttu-id="f711f-272">Перетащите **engineTemparature** в **оси y области**, измените агрегирования данных hello слишком**среднее**</span><span class="sxs-lookup"><span data-stu-id="f711f-272">Drag **engineTemparature** into **Y-Axis area**, change hello aggregation too**Average**</span></span>
5. <span data-ttu-id="f711f-273">Перетащите hello **vin** в hello **размер** области.</span><span class="sxs-lookup"><span data-stu-id="f711f-273">Drag hello **vin** field into hello **Size** area.</span></span>

![Подключенные автомобили — добавление новой визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="f711f-275">Изменение диаграммы hello **заголовок** слишком**«Средних топливо, температуры ядра моделью»**.</span><span class="sxs-lookup"><span data-stu-id="f711f-275">Change hello chart **Title** too**“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Подключенные автомобили — изменение заголовка диаграммы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="f711f-277">Hello окончательный отчет будет выглядеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f711f-277">hello final report will look like as shown below.</span></span>

![Подключенные автомобили — итоговый отчет](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a><span data-ttu-id="f711f-279">Визуализации ПИН-код из панели мониторинга в реальном времени toohello hello отчеты</span><span class="sxs-lookup"><span data-stu-id="f711f-279">Pin visualizations from hello reports toohello real-time dashboard</span></span>
<span data-ttu-id="f711f-280">Создайте пустую панель, щелкнув значок "плюс" hello tooDashboards Далее.</span><span class="sxs-lookup"><span data-stu-id="f711f-280">Create a blank dashboard by clicking on hello plus icon next tooDashboards.</span></span> <span data-ttu-id="f711f-281">Панели можно присвоить имя «Панель мониторинга аналитики телеметрии автомобилей».</span><span class="sxs-lookup"><span data-stu-id="f711f-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Подключенные автомобили — панель мониторинга](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="f711f-283">Закрепление hello визуализацию на hello выше мониторинга toohello отчеты.</span><span class="sxs-lookup"><span data-stu-id="f711f-283">Pin hello visualization from hello above reports toohello dashboard.</span></span> 

![Подключенные автомобили — панель мониторинга](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="f711f-285">панель мониторинга Hello должен выглядеть следующим образом все hello три отчеты создаются и hello соответствующий визуализации, закрепленные toohello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="f711f-285">hello dashboard should look as follows when all hello three reports are created and hello corresponding visualizations are pinned toohello dashboard.</span></span> <span data-ttu-id="f711f-286">Если вы не создали все отчеты hello, панели мониторинга может выглядеть иначе.</span><span class="sxs-lookup"><span data-stu-id="f711f-286">If you have not created all hello reports, your dashboard could look different.</span></span> 

![Подключенные автомобили — панель мониторинга](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="f711f-288">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="f711f-288">Congratulations!</span></span> <span data-ttu-id="f711f-289">Панель мониторинга в реальном времени hello успешно создана.</span><span class="sxs-lookup"><span data-stu-id="f711f-289">You have successfully created hello real-time dashboard.</span></span> <span data-ttu-id="f711f-290">Как вы по-прежнему tooexecute CarEventGenerator.exe и RealtimeDashboardApp.exe, вы увидите динамические обновления на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="f711f-290">As you continue tooexecute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on hello dashboard.</span></span> <span data-ttu-id="f711f-291">Может потребоваться hello toocomplete too15 около 10 минут, следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="f711f-291">It should take about 10 too15 minutes toocomplete hello following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="f711f-292">Настройка панели мониторинга пакетной обработки Power BI</span><span class="sxs-lookup"><span data-stu-id="f711f-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="f711f-293">Он занимает примерно в два часа (из hello успешного завершения развертывания hello) для hello окончания tooend пакетной обработки toofinish выполнение конвейера и обрабатывает созданный данные за год.</span><span class="sxs-lookup"><span data-stu-id="f711f-293">It takes about two hours (from hello successful completion of hello deployment) for hello end tooend batch processing pipeline toofinish execution and process a year worth of generated data.</span></span> <span data-ttu-id="f711f-294">Поэтому дождитесь hello обработки toofinish перед продолжением hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="f711f-294">So wait for hello processing toofinish before proceeding with hello next steps.</span></span> 
> 
> 

<span data-ttu-id="f711f-295">**Загрузите файл конструктора Power BI hello**</span><span class="sxs-lookup"><span data-stu-id="f711f-295">**Download hello Power BI designer file**</span></span>

* <span data-ttu-id="f711f-296">Предварительно настроенный файл конструктора Power BI входит в состав развертывания hello инструкции операции вручную</span><span class="sxs-lookup"><span data-stu-id="f711f-296">A pre-configured Power BI designer file is included as part of hello deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="f711f-297">Найдите пункт 2.</span><span class="sxs-lookup"><span data-stu-id="f711f-297">Look for 2.</span></span> <span data-ttu-id="f711f-298">Установки PowerBI пакетной обработки мониторинга можно скачать шаблон PowerBI hello Пакетная обработка панели мониторинга расположена **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="f711f-298">Setup PowerBI batch processing dashboard You can download hello PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="f711f-299">Сохраните файл на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="f711f-299">Save locally</span></span>

<span data-ttu-id="f711f-300">**Настройка отчетов Power BI**</span><span class="sxs-lookup"><span data-stu-id="f711f-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="f711f-301">Привет открыть файл конструктора "**ConnectedCarsPbiReport.pbix**" с помощью Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="f711f-301">Open hello designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="f711f-302">Если вы уже не устанавливать hello Power BI Desktop из [установки Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="f711f-302">If you do not already have, install hello Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="f711f-303">Нажмите кнопку hello **изменить запросы**.</span><span class="sxs-lookup"><span data-stu-id="f711f-303">Click hello **Edit Queries**.</span></span>

![Изменение запроса Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="f711f-305">Дважды щелкните hello **источника**.</span><span class="sxs-lookup"><span data-stu-id="f711f-305">Double-click hello **Source**.</span></span>

![Настройка источника Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="f711f-307">Обновите строки соединения сервера с сервером Azure SQL hello, полученный подготовлены в ходе развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="f711f-307">Update Server connection string with hello Azure SQL server that got provisioned as part of hello deployment.</span></span>  <span data-ttu-id="f711f-308">Искать в hello вручную операции инструкции в разделе</span><span class="sxs-lookup"><span data-stu-id="f711f-308">Look in hello Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="f711f-309">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="f711f-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="f711f-310">Сервер: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="f711f-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="f711f-311">База данных: connectedcar</span><span class="sxs-lookup"><span data-stu-id="f711f-311">Database: connectedcar</span></span>
    * <span data-ttu-id="f711f-312">Имя пользователя: username</span><span class="sxs-lookup"><span data-stu-id="f711f-312">Username: username</span></span>
    * <span data-ttu-id="f711f-313">Пароль: паролем к серверу SQL можно управлять на портале Azure</span><span class="sxs-lookup"><span data-stu-id="f711f-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="f711f-314">Для параметра **База данных** оставьте значение *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="f711f-314">Leave **Database** as *connectedcar*.</span></span>

![Настройка базы данных Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="f711f-316">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f711f-316">Click **OK**.</span></span>
* <span data-ttu-id="f711f-317">Вы увидите **учетные данные Windows** вкладка по умолчанию, измените его слишком**учетные данные базы данных** , щелкнув **базы данных** вкладки справа.</span><span class="sxs-lookup"><span data-stu-id="f711f-317">You will see **Windows credential** tab selected by default, change it too**Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="f711f-318">Укажите hello **Username** и **пароль** , указанное во время его установки для развертывания базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f711f-318">Provide hello **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Указание учетных данных базы данных](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="f711f-320">Добавьте новый отчет, щелкнув **Подключить**</span><span class="sxs-lookup"><span data-stu-id="f711f-320">Click **Connect**</span></span>
* <span data-ttu-id="f711f-321">Повторите hello выше действия для каждого hello три остальных запросов отсутствует на правой панели, а затем обновите сведения о подключении источника данных hello.</span><span class="sxs-lookup"><span data-stu-id="f711f-321">Repeat hello above steps for each of hello three remaining queries present at right pane, and then update hello data source connection details.</span></span>
* <span data-ttu-id="f711f-322">Щелкните **Close and Load**(Закрыть и загрузить).</span><span class="sxs-lookup"><span data-stu-id="f711f-322">Click **Close and Load**.</span></span> <span data-ttu-id="f711f-323">Наборов данных Power BI Desktop файл — это таблицы подключенной tooSQL базы данных Azure.</span><span class="sxs-lookup"><span data-stu-id="f711f-323">Power BI Desktop file datasets are connected tooSQL Azure Database tables.</span></span>
* <span data-ttu-id="f711f-324">**Закройте** файл Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="f711f-324">**Close** Power BI Desktop file.</span></span>

![Закрытие Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="f711f-326">Нажмите кнопку **Сохранить** кнопку toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="f711f-326">Click **Save** button toosave hello changes.</span></span> 

<span data-ttu-id="f711f-327">Теперь вы настроили все отчеты hello соответствующий toohello пути обработки пакета в решении hello.</span><span class="sxs-lookup"><span data-stu-id="f711f-327">You have now configured all hello reports corresponding toohello batch processing path in hello solution.</span></span> 

## <a name="upload-toopowerbicom"></a><span data-ttu-id="f711f-328">Отправка слишком*powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="f711f-328">Upload too*powerbi.com*</span></span>
1. <span data-ttu-id="f711f-329">Перейдите toohello Power BI веб-портала на http://powerbi.com и входа.</span><span class="sxs-lookup"><span data-stu-id="f711f-329">Navigate toohello Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="f711f-330">Щелкните **Получить данные**</span><span class="sxs-lookup"><span data-stu-id="f711f-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="f711f-331">Отправьте файл Power BI Desktop hello.</span><span class="sxs-lookup"><span data-stu-id="f711f-331">Upload hello Power BI Desktop File.</span></span>  
4. <span data-ttu-id="f711f-332">tooupload, нажмите кнопку **получение данных "->" файлы, получение локальный файл "->"**</span><span class="sxs-lookup"><span data-stu-id="f711f-332">tooupload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="f711f-333">Перейдите toohello **»**ConnectedCarsPbiReport.pbix**»**</span><span class="sxs-lookup"><span data-stu-id="f711f-333">Navigate toohello **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="f711f-334">После загрузки файла hello можно навигацию задней tooyour Power BI в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="f711f-334">Once hello file is uploaded, you will be navigated back tooyour Power BI work space.</span></span>  

<span data-ttu-id="f711f-335">Набор данных, отчет и пустая панель мониторинга будут созданы автоматически.</span><span class="sxs-lookup"><span data-stu-id="f711f-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="f711f-336">Новая панель мониторинга tooa вызывается диаграммы ПИН-код **транспортного средства мониторинга аналитических данных телеметрии** в **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="f711f-336">Pin charts tooa new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="f711f-337">Щелкните пустую панель hello, созданная выше, а затем перейдите toohello **отчеты** щелкните hello вновь отправлен отчет.</span><span class="sxs-lookup"><span data-stu-id="f711f-337">Click hello blank dashboard created above and then navigate toohello **Reports** section click hello newly uploaded report.</span></span>  

![Телеметрия автомобилей Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="f711f-339">**Примечание hello отчет содержит шесть страниц:**</span><span class="sxs-lookup"><span data-stu-id="f711f-339">**Note hello report has six pages:**</span></span>  
<span data-ttu-id="f711f-340">Страница 1. Плотность автомобиля.</span><span class="sxs-lookup"><span data-stu-id="f711f-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="f711f-341">Страница 2. Работоспособность автомобилей в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="f711f-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="f711f-342">Страница 3. Агрессивно управляемые автомобили.</span><span class="sxs-lookup"><span data-stu-id="f711f-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="f711f-343">Страница 4. Отозванные автомобили.</span><span class="sxs-lookup"><span data-stu-id="f711f-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="f711f-344">Страница 5. Автомобили с экономным расходом топлива.</span><span class="sxs-lookup"><span data-stu-id="f711f-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="f711f-345">Страница 6. Логотип компании Contoso.</span><span class="sxs-lookup"><span data-stu-id="f711f-345">Page 6: Contoso Logo</span></span>  

![Подключенные автомобили Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="f711f-347">**На странице 3**, закрепить hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f711f-347">**From Page 3**, pin hello following:</span></span>  

1. <span data-ttu-id="f711f-348">Количество VIN</span><span class="sxs-lookup"><span data-stu-id="f711f-348">Count of VIN</span></span>  
   ![Подключенные автомобили Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="f711f-350">Агрессивно управляемые автомобили по моделям — каскадная диаграмма.</span><span class="sxs-lookup"><span data-stu-id="f711f-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Телеметрия автомобиля — закрепление диаграмм 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="f711f-352">**От 5 страницы**, закрепить hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f711f-352">**From Page 5**, pin hello following:</span></span> 

1. <span data-ttu-id="f711f-353">Количество VIN</span><span class="sxs-lookup"><span data-stu-id="f711f-353">Count of vin</span></span>    
   ![Телеметрия автомобиля — закрепление диаграмм 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="f711f-355">Автомобили с экономным расходом топлива по моделям: гистограмма с группировкой.</span><span class="sxs-lookup"><span data-stu-id="f711f-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Телеметрия автомобиля — закрепление диаграмм 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="f711f-357">**Страница 4**, закрепить hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f711f-357">**From Page 4**, pin hello following:</span></span>  

1. <span data-ttu-id="f711f-358">Количество VIN</span><span class="sxs-lookup"><span data-stu-id="f711f-358">Count of vin</span></span>  
   ![Телеметрия автомобиля — закрепление диаграмм 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="f711f-360">Отозванные автомобили по городам, моделям: диаграмма "дерево".</span><span class="sxs-lookup"><span data-stu-id="f711f-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Телеметрия автомобиля — закрепление диаграмм 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="f711f-362">**От 6 страницы**, закрепить hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f711f-362">**From Page 6**, pin hello following:</span></span>  

1. <span data-ttu-id="f711f-363">Логотип компании Contoso Motors.</span><span class="sxs-lookup"><span data-stu-id="f711f-363">Contoso Motors logo</span></span>  
   ![Телеметрия автомобиля — закрепление диаграмм 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="f711f-365">**Упорядочение мониторинга hello**</span><span class="sxs-lookup"><span data-stu-id="f711f-365">**Organize hello dashboard**</span></span>  

1. <span data-ttu-id="f711f-366">Перейдите на панель мониторинга toohello</span><span class="sxs-lookup"><span data-stu-id="f711f-366">Navigate toohello dashboard</span></span>
2. <span data-ttu-id="f711f-367">Наведите указатель мыши на каждой диаграммы и переименуйте его основании именования hello в приведенном ниже рисунке hello панелей мониторинга.</span><span class="sxs-lookup"><span data-stu-id="f711f-367">Hover over each chart and rename it based on hello naming provided in hello complete dashboard image below.</span></span> <span data-ttu-id="f711f-368">Также можно переместите hello диаграммы вокруг toolook как мониторинга "hello" ниже.</span><span class="sxs-lookup"><span data-stu-id="f711f-368">Also move hello charts around toolook like hello dashboard below.</span></span>  
   ![Телеметрия автомобиля — упорядочение панели мониторинга 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Телеметрия автомобилей Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="f711f-371">При создании все отчеты hello, описанным в этом документе hello последней завершенной мониторинга должна выглядеть как hello следующий рисунок.</span><span class="sxs-lookup"><span data-stu-id="f711f-371">If you have created all hello reports as mentioned in this document, hello final completed dashboard should look like hello following figure.</span></span> 

![Телеметрия автомобиля — упорядочение панели мониторинга 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="f711f-373">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="f711f-373">Congratulations!</span></span> <span data-ttu-id="f711f-374">Успешно создана отчеты hello и hello toogain панели мониторинга в режиме реального времени, прогнозирования и привычки пакета важные сведения о работоспособности транспортного средства и управление им.</span><span class="sxs-lookup"><span data-stu-id="f711f-374">You have successfully created hello reports and hello dashboard toogain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
