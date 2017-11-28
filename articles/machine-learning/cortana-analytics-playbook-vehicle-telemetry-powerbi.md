---
title: "Использование панели Power BI для прогнозирования исправности автомобиля и манеры вождения с помощью Azure | Документация Майкрософт"
description: "Используйте возможности Cortana Intelligence, чтобы получить прогнозы и актуальную информацию об исправности и манере вождения автомобиля в режиме реального времени."
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
ms.openlocfilehash: f880aceb1657ffdfe909b73f175b9673d9ab02cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="c2abb-103">Инструкции по настройке информационной панели Power BI шаблона решения для аналитики телеметрии автомобилей</span><span class="sxs-lookup"><span data-stu-id="c2abb-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="c2abb-104">Из этого **меню** можно открыть разделы сборника тренировочных заданий.</span><span class="sxs-lookup"><span data-stu-id="c2abb-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="c2abb-105">Ниже приведены примеры использования решения для аналитики телеметрии автомобилей. Они демонстрируют, как возможности Cortana Intelligence помогают автодилерам, производителям автомобилей и страховым компаниям получать прогнозы и актуальную информацию об исправности автомобиля и манере вождения в реальном времени, чтобы повышать качество обслуживания клиентов, исследований и маркетинговых кампаний.</span><span class="sxs-lookup"><span data-stu-id="c2abb-105">The Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits to drive improvements in the area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="c2abb-106">В этом документе приведены пошаговые инструкции по настройке отчетов и информационной панели Power BI после развертывания решения в подписке.</span><span class="sxs-lookup"><span data-stu-id="c2abb-106">This document contains step by step instructions on how you can configure the Power BI reports and dashboard once the solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c2abb-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c2abb-107">Prerequisites</span></span>
1. <span data-ttu-id="c2abb-108">Разверните решение [аналитики телеметрии](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90).</span><span class="sxs-lookup"><span data-stu-id="c2abb-108">Deploy the [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="c2abb-109">Установите Microsoft Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c2abb-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="c2abb-110">[Подписка Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2abb-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="c2abb-111">Если у вас нет подписки Azure, для начала получите бесплатную подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="c2abb-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="c2abb-112">Учетная запись Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="c2abb-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="c2abb-113">Компоненты Cortana Intelligence Suite</span><span class="sxs-lookup"><span data-stu-id="c2abb-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="c2abb-114">В вашей подписке будут развернуты следующие службы Cortana Intelligence из шаблона решения для аналитики телеметрии автомобилей.</span><span class="sxs-lookup"><span data-stu-id="c2abb-114">As part of the Vehicle Telemetry Analytics solution template, the following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="c2abb-115">**Концентратор событий** принимает миллионы событий телеметрии автомобилей в Azure.</span><span class="sxs-lookup"><span data-stu-id="c2abb-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="c2abb-116">**Stream Analytics** получает данные аналитики о работоспособности автомобиля в режиме реального времени и сохраняет их в долговременное хранилище для более детальной пакетной аналитики.</span><span class="sxs-lookup"><span data-stu-id="c2abb-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="c2abb-117">**Машинное обучение** обнаруживает аномалии в режиме реального времени и выполняет пакетную обработку для прогнозирования состояний.</span><span class="sxs-lookup"><span data-stu-id="c2abb-117">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="c2abb-118">**HDInsight** используется для преобразования данных при масштабировании.</span><span class="sxs-lookup"><span data-stu-id="c2abb-118">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="c2abb-119">**Фабрика данных** предназначена для координации, планирования и мониторинга конвейера пакетной обработки, а также управления ресурсами.</span><span class="sxs-lookup"><span data-stu-id="c2abb-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>

<span data-ttu-id="c2abb-120">**Power BI** предоставляет для этого решения расширенную панель мониторинга для визуализации данных в режиме реального времени и прогнозной аналитики.</span><span class="sxs-lookup"><span data-stu-id="c2abb-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="c2abb-121">В решении используются два источника данных: **симулированные сигналы автомобиля с набором диагностических данных** и **каталог автомобиля**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-121">The solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="c2abb-122">В это решение входит симулятор телематики автомобиля.</span><span class="sxs-lookup"><span data-stu-id="c2abb-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="c2abb-123">Он выдает диагностическую информацию и сигналы, соответствующие состоянию автомобиля и манере вождения в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="c2abb-123">It emits diagnostic information and signals corresponding to the state of the vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="c2abb-124">Каталог автомобилей — это справочный набор данных для сопоставления номера шасси знака (VIN) с моделью автомобиля.</span><span class="sxs-lookup"><span data-stu-id="c2abb-124">The Vehicle Catalog is a reference dataset containing VIN to model mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="c2abb-125">Подготовка информационной панели Power BI</span><span class="sxs-lookup"><span data-stu-id="c2abb-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="c2abb-126">Настройка панели мониторинга Power BI в реальном времени</span><span class="sxs-lookup"><span data-stu-id="c2abb-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="c2abb-127">**Запустите приложение панели мониторинга в режиме реального времени**. По завершении развертывания следует выполнить инструкции по ручному управлению.</span><span class="sxs-lookup"><span data-stu-id="c2abb-127">**Start the real-time dashboard application** Once the deployment is completed, you should follow the Manual Operation Instructions</span></span>

* <span data-ttu-id="c2abb-128">Скачайте файл RealtimeDashboardApp.zip с приложением панели мониторинга в режиме реального времени и распакуйте его.</span><span class="sxs-lookup"><span data-stu-id="c2abb-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="c2abb-129">В распакованной папке откройте файл конфигурации приложения RealtimeDashboardApp.exe.config, замените appSettings для подключений к Eventhub, хранилищу BLOB-объектов и службы машинного обучения на значения из инструкций по ручному управлению, а затем сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="c2abb-129">In the unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with the values in the Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="c2abb-130">Запустите приложение RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="c2abb-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="c2abb-131">Появится окно входа. Укажите в нем действительные учетные данные PowerBI и нажмите кнопку **Принять**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-131">A login window will pop up, provide your valid PowerBI credentials and click the **Accept** button.</span></span> <span data-ttu-id="c2abb-132">Приложение начнет выполняться.</span><span class="sxs-lookup"><span data-stu-id="c2abb-132">Then the app will start to run.</span></span>

   ![Войдите в Power BI.](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Разрешения для информационной панели Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="c2abb-135">Войдите на веб-сайт PowerBI и создайте панель мониторинга в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="c2abb-135">Login to PowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="c2abb-136">Теперь все готово к настройке информационной панели Power BI с расширенными возможностями визуализации для получения информации об исправности автомобиля и манере вождения в реальном времени, а также прогнозных данных.</span><span class="sxs-lookup"><span data-stu-id="c2abb-136">Now, you are ready to configure the Power BI dashboard with rich visualizations to gain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="c2abb-137">Создание отчетов и настройка панели мониторинга займут от 45 минут до часа.</span><span class="sxs-lookup"><span data-stu-id="c2abb-137">It takes about 45 minutes to an hour to create all the reports and configure the dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="c2abb-138">Настройка отчетов Power BI</span><span class="sxs-lookup"><span data-stu-id="c2abb-138">Configure Power BI reports</span></span>
<span data-ttu-id="c2abb-139">Подготовка отчетов и панели мониторинга в реальном времени занимает около 30–45 минут.</span><span class="sxs-lookup"><span data-stu-id="c2abb-139">The real-time reports and the dashboard take about 30-45 minutes to complete.</span></span> <span data-ttu-id="c2abb-140">Перейдите на страницу [http://powerbi.com](http://powerbi.com) и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="c2abb-140">Browse to [http://powerbi.com](http://powerbi.com) and login.</span></span>

![Войдите в Power BI.](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="c2abb-142">В Power BI создается новый набор данных.</span><span class="sxs-lookup"><span data-stu-id="c2abb-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="c2abb-143">Щелкните набор данных **ConnectedCarsRealtime** .</span><span class="sxs-lookup"><span data-stu-id="c2abb-143">Click the **ConnectedCarsRealtime** dataset.</span></span>

![Выберите набор данных подключенных автомобилей в реальном времени](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="c2abb-145">Сохраните пустой отчет, нажав **CTRL+S**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-145">Save the blank report using **Ctrl + s**.</span></span>

![Сохраните пустой отчет.](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="c2abb-147">Введите для отчета имя *Аналитика телеметрии автомобилей в реальном времени: отчеты*.</span><span class="sxs-lookup"><span data-stu-id="c2abb-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Присвойте имя отчету.](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="c2abb-149">Отчеты в реальном времени</span><span class="sxs-lookup"><span data-stu-id="c2abb-149">Real-time reports</span></span>
<span data-ttu-id="c2abb-150">Это решение включает три отчета в реальном времени, описывающие:</span><span class="sxs-lookup"><span data-stu-id="c2abb-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="c2abb-151">исправные автомобили;</span><span class="sxs-lookup"><span data-stu-id="c2abb-151">Vehicles in operation</span></span>
2. <span data-ttu-id="c2abb-152">автомобили, которым требуется обслуживание;</span><span class="sxs-lookup"><span data-stu-id="c2abb-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="c2abb-153">Статистика работоспособности автомобилей</span><span class="sxs-lookup"><span data-stu-id="c2abb-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="c2abb-154">Вы можете настроить все три отчета в реальном времени или перейти к следующему разделу, в котором описана настройка пакетных отчетов.</span><span class="sxs-lookup"><span data-stu-id="c2abb-154">You can choose to configure all the three real-time reports or stop after any stage and proceed to the next section of configuring the batch reports.</span></span> <span data-ttu-id="c2abb-155">Мы рекомендуем сразу создать все три отчета для визуализации всей аналитической информации, предоставляемой этим решением в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="c2abb-155">We recommend you to create all the three reports to visualize the full insights of the real-time path of the solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="c2abb-156">1. исправные автомобили;</span><span class="sxs-lookup"><span data-stu-id="c2abb-156">1. Vehicles in operation</span></span>
<span data-ttu-id="c2abb-157">Дважды щелкните элемент **Страница 1** и переименуйте его на "Исправные автомобили".</span><span class="sxs-lookup"><span data-stu-id="c2abb-157">Double-click **Page 1** and rename it to “Vehicles in operation”</span></span>  
    <span data-ttu-id="c2abb-158">![Подключенные автомобили — исправные автомобили](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="c2abb-159">В разделе **Поля** выберите поле **VIN** и укажите тип визуализации **Карточка**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="c2abb-160">Создается карточка визуализации, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="c2abb-160">Card visualization is created as shown in figure.</span></span>  
    ![Подключенные автомобили — выберите номер шасси](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="c2abb-162">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-162">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c2abb-163">Выберите поля **Город** и **VIN**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="c2abb-164">Измените тип визуализации на **Карта**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-164">Change visualization to **“Map”**.</span></span> <span data-ttu-id="c2abb-165">Перетащите поле **VIN** в область значений.</span><span class="sxs-lookup"><span data-stu-id="c2abb-165">Drag **vin** in values area.</span></span> <span data-ttu-id="c2abb-166">Перетащите поле **Город** из раздела "Поля" в область **Условные обозначения**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-166">Drag **city** from fields to **Legend** area.</span></span>   
    <span data-ttu-id="c2abb-167">![Подключенные автомобили — визуализация "Карточка"](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="c2abb-168">В разделе **Визуализации** откройте раздел **Формат**, щелкните **Заголовок** и измените значение поля **Текст** на **Исправные автомобили по городам**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-168">Select **format** section from **Visualizations**, click **Title** and change the **Text** to **“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="c2abb-169">![Подключенные автомобили — исправные автомобили по городам](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="c2abb-170">Визуализация будет выглядеть, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="c2abb-170">Final visualization looks as shown in figure.</span></span>    
    ![Подключенные автомобили — итоговая визуализация](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="c2abb-172">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-172">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c2abb-173">Выберите поля **Город** и **VIN**. Затем измените тип визуализации на **Гистограмма с группировкой**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-173">Select **City** and **vin**, change visualization type to **Clustered Column Chart**.</span></span> <span data-ttu-id="c2abb-174">Убедитесь, что поле **Город** размещено в области **Ось**, а **VIN** — в области **Значение**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="c2abb-175">Отсортируйте гистограмму по параметру **Count of vin** (Количество VIN).</span><span class="sxs-lookup"><span data-stu-id="c2abb-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="c2abb-176">![Подключенные автомобили — количество номеров шасси](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="c2abb-177">Измените заголовок гистограммы в поле **Заголовок** на **Исправные автомобили по городам**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-177">Change chart **Title** to **“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="c2abb-178">В разделе **Формат** выберите **Цвета данных** и щелкните **On** (Вкл.) для параметра **Показать все**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-178">Click the **Format** section, then select **Data Colors**,  Click the **“On”** to **Show All**</span></span>  
    <span data-ttu-id="c2abb-179">![Подключенные автомобили — отображение всех цветов данных](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="c2abb-180">Измените цвет для каждого города, щелкнув цветной значок.</span><span class="sxs-lookup"><span data-stu-id="c2abb-180">Change the color of individual city by clicking on color icon.</span></span>  
    ![Подключенные автомобили — изменение цветов](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="c2abb-182">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-182">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c2abb-183">Выберите тип визуализации **Гистограмма с группировкой**, перетащите поле **Город** в область **Ось**, поле **Модель** — в область **Условные обозначения**, а поле **VIN** — в область **Значение**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="c2abb-184">![Подключенные автомобили — кластеризованная гистограмма](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="c2abb-185">![Подключенные автомобили — отрисовка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="c2abb-186">Измените визуальное представление на странице, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="c2abb-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Подключенные автомобили — визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="c2abb-188">Отчет «Исправные автомобили» в реальном времени настроен.</span><span class="sxs-lookup"><span data-stu-id="c2abb-188">You have successfully configured the “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="c2abb-189">Вы можете создать следующий отчет в реальном времени или перейти к настройке панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c2abb-189">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="c2abb-190">2) автомобили, которым требуется обслуживание;</span><span class="sxs-lookup"><span data-stu-id="c2abb-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="c2abb-191">Добавьте новый отчет, щелкнув ![Добавить](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) , и переименуйте его в **Автомобили, которым требуется обслуживание**</span><span class="sxs-lookup"><span data-stu-id="c2abb-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report, rename it to **“Vehicles Requiring Maintenance”**</span></span>

![Подключенные автомобили — автомобили, требующие обслуживания](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="c2abb-193">Выберите поле **VIN** и измените тип визуализации на **Карточка**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-193">Select **vin** field and change visualization type to **Card**.</span></span>  
    <span data-ttu-id="c2abb-194">![Подключенные автомобили — визуализация "Карточка номера шасси"](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="c2abb-195">В наборе данных есть поле с именем MaintenanceLabel.</span><span class="sxs-lookup"><span data-stu-id="c2abb-195">We have a field named “MaintenanceLabel” In the dataset.</span></span> <span data-ttu-id="c2abb-196">Это поле может иметь значение 0 или 1.</span><span class="sxs-lookup"><span data-stu-id="c2abb-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="c2abb-197">Оно задается моделью машинного обучения Azure, которая включена в решение и интегрирована с механизмом обработки в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="c2abb-197">It is set by the Azure Machine Learning model provisioned as part of solution and integrated with the real-time path.</span></span> <span data-ttu-id="c2abb-198">Значение 1 означает, что автомобилю требуется обслуживание.</span><span class="sxs-lookup"><span data-stu-id="c2abb-198">The value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="c2abb-199">Вот как добавить фильтр **уровня страницы** для отображения данных об автомобилях, которым требуется обслуживание.</span><span class="sxs-lookup"><span data-stu-id="c2abb-199">To add a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="c2abb-200">Перетащите поле **MaintenanceLabel** в область **Фильтры уровня страницы**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-200">Drag the **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="c2abb-201">![Подключенные автомобили — фильтры уровня страницы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="c2abb-202">В нижней части фильтра уровня страницы MaintenanceLabel щелкните меню **Простая фильтрация** .</span><span class="sxs-lookup"><span data-stu-id="c2abb-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="c2abb-203">![Подключенные автомобили — базовая фильтрация](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="c2abb-204">Задайте значение фильтра **1**  .</span><span class="sxs-lookup"><span data-stu-id="c2abb-204">Set its filter value to **“1”**  </span></span>  
   <span data-ttu-id="c2abb-205">![Подключенные автомобили — значение фильтра](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="c2abb-206">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-206">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c2abb-207">Выберите тип визуализации **Гистограмма с группировкой**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="c2abb-208">![Подключенные автомобили — визуализация «Карточка номера шасси»](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="c2abb-209">![Подключенные автомобили — кластеризованная гистограмма](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="c2abb-210">Перетащите поле **Модель** в область **Оси**, а поле **VIN** — в область **Значение**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-210">Drag field **Model** into **Axis** area, **Vin** to **Value** area.</span></span> <span data-ttu-id="c2abb-211">Отсортируйте визуализацию по параметру **Количество VIN**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="c2abb-212">Измените заголовок гистограммы в поле **Заголовок** на **Автомобили, которым требуется обслуживание, по моделям**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-212">Change chart **Title** to **“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="c2abb-213">Перетащите поля **VIN** в область **Насыщенность цвета** (раздел **Поля** ![Поля](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) на вкладке **Визуализация**).</span><span class="sxs-lookup"><span data-stu-id="c2abb-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="c2abb-214">![Подключенные автомобили — насыщенность цвета](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="c2abb-215">Измените тип визуализации параметра **Цвета данных** из раздела **Формат**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="c2abb-216">Измените минимальное значение цвета на **F2C812**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="c2abb-217">Измените максимальное значение цвета на **FF6300**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="c2abb-218">![Подключенные автомобили — изменения цвета](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="c2abb-219">![Подключенные автомобили — новые цвета визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="c2abb-220">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-220">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c2abb-221">Выберите тип визуализации **Гистограмма с группировкой**. Затем перетащите поле **VIN** в область **Значение**, а поле **Город** — в область **Ось**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="c2abb-222">Отсортируйте гистограмму по параметру **Count of vin** (Количество VIN).</span><span class="sxs-lookup"><span data-stu-id="c2abb-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="c2abb-223">Измените заголовок гистограммы в поле **Заголовок** на **Автомобили, требующие обслуживания, по городам** .</span><span class="sxs-lookup"><span data-stu-id="c2abb-223">Change chart **Title** to **“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="c2abb-224">![Подключенные автомобили — автомобили, требующие обслуживания, по городам](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="c2abb-225">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-225">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c2abb-226">Выберите визуализацию **Многострочная карточка**, а затем перетащите поля **Модель** и **VIN** в область **Поля**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into the **Fields** area.</span></span>  
<span data-ttu-id="c2abb-227">![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="c2abb-228">После переупорядочивания всех элементов визуализации итоговый отчет будет выглядеть следующим образом: </span><span class="sxs-lookup"><span data-stu-id="c2abb-228">Rearranging all of the visualization, the final report looks as follows:</span></span>  
![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="c2abb-230">Отчет «Автомобили, которым требуется обслуживание» в реальном времени настроен.</span><span class="sxs-lookup"><span data-stu-id="c2abb-230">You have successfully configured the “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="c2abb-231">Вы можете создать следующий отчет в реальном времени или перейти к настройке панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c2abb-231">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="c2abb-232">3. Статистика работоспособности автомобилей</span><span class="sxs-lookup"><span data-stu-id="c2abb-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="c2abb-233">Добавьте новый отчет, щелкнув ![Добавить](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) , и переименуйте его в **Статистика работоспособности автомобилей**</span><span class="sxs-lookup"><span data-stu-id="c2abb-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add new report, rename it to **“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="c2abb-234">Выберите тип визуализации **Датчик**. Затем перетащите поле **Скорость** в области **Value, Minimum Value, Maximum Value** (Значение, Минимальное значение, Максимальное значение).</span><span class="sxs-lookup"><span data-stu-id="c2abb-234">Select **Gauge** visualization from visualizations, then drag the **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="c2abb-235">![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="c2abb-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="c2abb-236">В области **Значение** для параметра **Скорость** измените агрегирование по умолчанию на **Среднее**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-236">Change the default aggregation of **speed** in **Value area** to **Average**</span></span> 

<span data-ttu-id="c2abb-237">В области **Minimum area** (Минимальное значение) для параметра **Скорость** измените агрегирование по умолчанию на **Минимум**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-237">Change the default aggregation of **speed** in **Minimum area** to **Minimum**</span></span>

<span data-ttu-id="c2abb-238">В области **Maximum area** (Максимальное значение) для параметра **Скорость** измените агрегирование по умолчанию на **Максимум**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-238">Change the default aggregation of **speed** in **Maximum area** to **Maximum**</span></span>

![Подключенные автомобили — многострочная карточка](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="c2abb-240">В качестве **заголовка датчика** укажите **Средняя скорость**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-240">Rename the **Gauge Title** to **“Average speed”**</span></span> 

![Подключенные автомобили — датчик](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="c2abb-242">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-242">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c2abb-243">Аналогичным образом добавьте следующие **датчики**: **Среднее количество моторного масла**, **Среднее количество топлива** и **Средняя температура двигателя**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="c2abb-244">В поле каждого датчика измените агрегирование по умолчанию, выполнив шаги, приведенные выше для датчика **Средняя скорость** .</span><span class="sxs-lookup"><span data-stu-id="c2abb-244">Change the default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Подключенные автомобили — датчики](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="c2abb-246">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-246">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="c2abb-247">Из раздела "Визуализации" выберите **График и гистограмма с группировкой** и перетащите поле **Город** в область **Общая ось**. Затем перетащите поля **Скорость**, **Давление в шинах и Моторное масло** в область **Значения столбцов**. Измените тип агрегирования на **Среднее**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type to **Average**.</span></span> 

<span data-ttu-id="c2abb-248">Перетащите поле **Температура двигателя** в область **Значения строк** и измените тип агрегирования на **Среднее**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-248">Drag the **engineTemperature** field into **Line Values** area, change the  aggregation type to **Average**.</span></span> 

![Подключенные автомобили — поля визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="c2abb-250">Измените **заголовок** диаграммы в соответствующем поле на **Среднее значение скорости, давления в шинах, температуры моторного масла и двигателя**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-250">Change the chart **Title** to **“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Подключенные автомобили — поля визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="c2abb-252">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-252">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="c2abb-253">Выберите визуализацию **Диаграмма дерева** из раздела "Визуализации" и перетащите поле **Модель** в область **Группа**. Затем перетащите поле **Вероятность обслуживания** в область **Значения**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-253">Select **Treemap** visualization from visualizations, drag the **Model** field into the **Group** area, and drag the field **MaintenanceProbability** into the **Values** area.</span></span>

<span data-ttu-id="c2abb-254">Измените **заголовок** диаграммы в соответствующем поле на **Модели автомобилей, которым требуется обслуживание**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-254">Change the chart **Title** to **“Vehicle models requiring maintenance”**.</span></span>

![Подключенные автомобили — изменение заголовка диаграммы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="c2abb-256">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-256">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="c2abb-257">Выберите тип визуализации **100% Stacked Bar Chart** (Нормированная линейчатая диаграмма) и перетащите поле **Город** в область **Ось**. Затем перетащите поля **Вероятность обслуживания** и **Вероятность отзыва** в область **Значение**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-257">Select **100% Stacked Bar Chart** from visualization, drag the **city** field into the **Axis** area, and drag the **MaintenanceProbability**, **RecallProbability** fields into the **Value** area.</span></span>

![Подключенные автомобили — добавление новой визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="c2abb-259">Щелкните **Формат**, выберите **Цвета данных** и задайте для цвета **Вероятность обслуживания** значение **F2C80F**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-259">Click **Format**, select **Data Colors**, and set the **MaintenanceProbability** color to the value **“F2C80F”**.</span></span>

<span data-ttu-id="c2abb-260">Измените **заголовок** диаграммы в соответствующем поле на **Вероятность обслуживания и отзыва автомобилей по городам**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-260">Change the **Title** of the chart to **“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Подключенные автомобили — добавление новой визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="c2abb-262">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-262">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="c2abb-263">Выберите тип визуализации **Диаграмма с областями** и перетащите поле **Модель** в область **Ось**. Затем перетащите поля **Моторное масло, Давление в шинах, Скорость, Вероятность обслуживания** в область **Значения**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-263">Select **Area Chart** from visualization from visualizations, drag the **Model** field into the **Axis** area, and drag the **engineOil, tirepressure, speed and MaintenanceProbability** fields into the **Values** area.</span></span> <span data-ttu-id="c2abb-264">Измените тип агрегирования на **Среднее**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-264">Change their aggregation type to **“Average”**.</span></span> 

![Подключенные автомобили — изменение типа агрегирования](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="c2abb-266">Измените заголовок диаграммы на **Среднее значение количества моторного масла, давления в шинах, скорости и вероятности обслуживания по моделям**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-266">Change the title of the chart to **“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Подключенные автомобили — изменение заголовка диаграммы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="c2abb-268">Щелкните пустую область, чтобы добавить новую визуализацию.</span><span class="sxs-lookup"><span data-stu-id="c2abb-268">Click the blank area to add new visualization:</span></span>

1. <span data-ttu-id="c2abb-269">Выберите тип визуализации **Точечная диаграмма** .</span><span class="sxs-lookup"><span data-stu-id="c2abb-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="c2abb-270">Перетащите поле **Модель** в области **Сведения** и **Условные обозначения**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-270">Drag the **Model** field into the **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="c2abb-271">Перетащите поле **Топливо** в область **Ось X** и измените тип агрегирования на **Среднее**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-271">Drag the **fuel** field into the **X-Axis** area, change the aggregation to **Average**.</span></span>
4. <span data-ttu-id="c2abb-272">Перетащите поле **Температура двигателя** в область **Ось Y** и измените тип агрегирования на **Среднее**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-272">Drag **engineTemparature** into **Y-Axis area**, change the aggregation to **Average**</span></span>
5. <span data-ttu-id="c2abb-273">Перетащите поле **VIN** в область **Размер**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-273">Drag the **vin** field into the **Size** area.</span></span>

![Подключенные автомобили — добавление новой визуализации](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="c2abb-275">Измените **заголовок** диаграммы в соответствующем поле на **Среднее значение количества топлива и температуры двигателя по моделям**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-275">Change the chart **Title** to **“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Подключенные автомобили — изменение заголовка диаграммы](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="c2abb-277">Итоговый отчет будет выглядеть так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c2abb-277">The final report will look like as shown below.</span></span>

![Подключенные автомобили — итоговый отчет](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-the-reports-to-the-real-time-dashboard"></a><span data-ttu-id="c2abb-279">Закрепление визуализаций из отчетов на панели мониторинга в реальном времени</span><span class="sxs-lookup"><span data-stu-id="c2abb-279">Pin visualizations from the reports to the real-time dashboard</span></span>
<span data-ttu-id="c2abb-280">Чтобы создать пустую панель мониторинга, щелкните значок плюса рядом с заголовком «Панели мониторинга».</span><span class="sxs-lookup"><span data-stu-id="c2abb-280">Create a blank dashboard by clicking on the plus icon next to Dashboards.</span></span> <span data-ttu-id="c2abb-281">Панели можно присвоить имя «Панель мониторинга аналитики телеметрии автомобилей».</span><span class="sxs-lookup"><span data-stu-id="c2abb-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Подключенные автомобили — панель мониторинга](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="c2abb-283">Закрепите визуализацию с созданными отчетами на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c2abb-283">Pin the visualization from the above reports to the dashboard.</span></span> 

![Подключенные автомобили — панель мониторинга](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="c2abb-285">После того как вы создадите все три отчета и закрепите соответствующие визуализации на панели мониторинга, она будет выглядеть так, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="c2abb-285">The dashboard should look as follows when all the three reports are created and the corresponding visualizations are pinned to the dashboard.</span></span> <span data-ttu-id="c2abb-286">Если вы создали не все отчеты, панель мониторинга может выглядеть иначе.</span><span class="sxs-lookup"><span data-stu-id="c2abb-286">If you have not created all the reports, your dashboard could look different.</span></span> 

![Подключенные автомобили — панель мониторинга](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="c2abb-288">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="c2abb-288">Congratulations!</span></span> <span data-ttu-id="c2abb-289">Вы настроили панель мониторинга в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="c2abb-289">You have successfully created the real-time dashboard.</span></span> <span data-ttu-id="c2abb-290">По мере выполнения файлов CarEventGenerator.exe и RealtimeDashboardApp.exe на панели мониторинга будут отображаться соответствующие обновления в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="c2abb-290">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on the dashboard.</span></span> <span data-ttu-id="c2abb-291">Для выполнения следующих действий может потребоваться 10–15 минут.</span><span class="sxs-lookup"><span data-stu-id="c2abb-291">It should take about 10 to 15 minutes to complete the following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="c2abb-292">Настройка панели мониторинга пакетной обработки Power BI</span><span class="sxs-lookup"><span data-stu-id="c2abb-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="c2abb-293">Чтобы завершить выполнение и обработать данные за год, конвейеру пакетной обработки потребуется около двух часов (после завершения развертывания).</span><span class="sxs-lookup"><span data-stu-id="c2abb-293">It takes about two hours (from the successful completion of the deployment) for the end to end batch processing pipeline to finish execution and process a year worth of generated data.</span></span> <span data-ttu-id="c2abb-294">Поэтому дождитесь завершения обработки перед выполнением следующих шагов.</span><span class="sxs-lookup"><span data-stu-id="c2abb-294">So wait for the processing to finish before proceeding with the next steps.</span></span> 
> 
> 

<span data-ttu-id="c2abb-295">**Скачивание файла конструктора Power BI**</span><span class="sxs-lookup"><span data-stu-id="c2abb-295">**Download the Power BI designer file**</span></span>

* <span data-ttu-id="c2abb-296">Предварительно настроенный файл конструктора Power BI входит в состав инструкций по ручному управлению развертыванием.</span><span class="sxs-lookup"><span data-stu-id="c2abb-296">A pre-configured Power BI designer file is included as part of the deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="c2abb-297">Найдите пункт 2.</span><span class="sxs-lookup"><span data-stu-id="c2abb-297">Look for 2.</span></span> <span data-ttu-id="c2abb-298">Установите панель мониторинга пакетной обработки PowerBI. Вы можете скачать шаблон PowerBI для панели пакетной обработки с именем **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-298">Setup PowerBI batch processing dashboard You can download the PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="c2abb-299">Сохраните файл на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c2abb-299">Save locally</span></span>

<span data-ttu-id="c2abb-300">**Настройка отчетов Power BI**</span><span class="sxs-lookup"><span data-stu-id="c2abb-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="c2abb-301">Откройте файл конструктора **ConnectedCarsPbiReport.pbix** с помощью Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c2abb-301">Open the designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="c2abb-302">Установите Power BI Desktop (если вы еще не сделали это) с помощью [установщика Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="c2abb-302">If you do not already have, install the Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="c2abb-303">Щелкните **Изменить запросы**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-303">Click the **Edit Queries**.</span></span>

![Изменение запроса Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="c2abb-305">Дважды щелкните **Источник**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-305">Double-click the **Source**.</span></span>

![Настройка источника Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="c2abb-307">Обновите строку подключения, указав сервер Azure SQL, подготовленный как часть развертывания.</span><span class="sxs-lookup"><span data-stu-id="c2abb-307">Update Server connection string with the Azure SQL server that got provisioned as part of the deployment.</span></span>  <span data-ttu-id="c2abb-308">Найдите в инструкциях по ручному управлению следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="c2abb-308">Look in the Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="c2abb-309">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c2abb-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="c2abb-310">Сервер: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="c2abb-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="c2abb-311">База данных: connectedcar</span><span class="sxs-lookup"><span data-stu-id="c2abb-311">Database: connectedcar</span></span>
    * <span data-ttu-id="c2abb-312">Имя пользователя: username</span><span class="sxs-lookup"><span data-stu-id="c2abb-312">Username: username</span></span>
    * <span data-ttu-id="c2abb-313">Пароль: паролем к серверу SQL можно управлять на портале Azure</span><span class="sxs-lookup"><span data-stu-id="c2abb-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="c2abb-314">Для параметра **База данных** оставьте значение *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="c2abb-314">Leave **Database** as *connectedcar*.</span></span>

![Настройка базы данных Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="c2abb-316">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-316">Click **OK**.</span></span>
* <span data-ttu-id="c2abb-317">Отобразится вкладка **Windows credential** (Учетные данные Windows), выбранная по умолчанию. Измените ее на **Учетные данные базы данных**, щелкнув вкладку **База данных** справа.</span><span class="sxs-lookup"><span data-stu-id="c2abb-317">You will see **Windows credential** tab selected by default, change it to **Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="c2abb-318">Укажите **имя пользователя** и **пароль** в соответствующих полях для доступа к Базе данных SQL Azure (выбрано на этапе развертывания).</span><span class="sxs-lookup"><span data-stu-id="c2abb-318">Provide the **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Указание учетных данных базы данных](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="c2abb-320">Добавьте новый отчет, щелкнув **Подключить**</span><span class="sxs-lookup"><span data-stu-id="c2abb-320">Click **Connect**</span></span>
* <span data-ttu-id="c2abb-321">Повторите описанные выше действия для каждого из оставшихся трех запросов на правой панели. Затем обновите сведения о подключении к источнику данных.</span><span class="sxs-lookup"><span data-stu-id="c2abb-321">Repeat the above steps for each of the three remaining queries present at right pane, and then update the data source connection details.</span></span>
* <span data-ttu-id="c2abb-322">Щелкните **Close and Load**(Закрыть и загрузить).</span><span class="sxs-lookup"><span data-stu-id="c2abb-322">Click **Close and Load**.</span></span> <span data-ttu-id="c2abb-323">Наборы данных файла Power BI Desktop подключены к таблицам базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c2abb-323">Power BI Desktop file datasets are connected to SQL Azure Database tables.</span></span>
* <span data-ttu-id="c2abb-324">**Закройте** файл Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c2abb-324">**Close** Power BI Desktop file.</span></span>

![Закрытие Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="c2abb-326">Нажмите кнопку **Сохранить** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="c2abb-326">Click **Save** button to save the changes.</span></span> 

<span data-ttu-id="c2abb-327">Теперь вы настроили все отчеты для пакетной обработки в решении.</span><span class="sxs-lookup"><span data-stu-id="c2abb-327">You have now configured all the reports corresponding to the batch processing path in the solution.</span></span> 

## <a name="upload-to-powerbicom"></a><span data-ttu-id="c2abb-328">Отправка на *powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="c2abb-328">Upload to *powerbi.com*</span></span>
1. <span data-ttu-id="c2abb-329">Перейдите на веб-портал Power BI по адресу http://powerbi.com и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="c2abb-329">Navigate to the Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="c2abb-330">Щелкните **Получить данные**</span><span class="sxs-lookup"><span data-stu-id="c2abb-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="c2abb-331">Отправьте файл Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c2abb-331">Upload the Power BI Desktop File.</span></span>  
4. <span data-ttu-id="c2abb-332">Для этого щелкните **Получить данные -> Files Get (Получение файлов) -> Локальный файл**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-332">To upload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="c2abb-333">Перейдите к файлу **"**ConnectedCarsPbiReport.pbix**"**</span><span class="sxs-lookup"><span data-stu-id="c2abb-333">Navigate to the **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="c2abb-334">После отправки файла вы перейдете обратно в свою рабочую область Power BI.</span><span class="sxs-lookup"><span data-stu-id="c2abb-334">Once the file is uploaded, you will be navigated back to your Power BI work space.</span></span>  

<span data-ttu-id="c2abb-335">Набор данных, отчет и пустая панель мониторинга будут созданы автоматически.</span><span class="sxs-lookup"><span data-stu-id="c2abb-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="c2abb-336">Закрепите диаграммы на новой панели мониторинга **Vehicle Telemetry Analytics Dashboard** (Информационная панель аналитики телеметрии автомобилей) в **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="c2abb-336">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="c2abb-337">Щелкните пустую панель мониторинга, созданную ранее, а затем перейдите к разделу **Отчеты** и щелкните отправленный отчет.</span><span class="sxs-lookup"><span data-stu-id="c2abb-337">Click the blank dashboard created above and then navigate to the **Reports** section click the newly uploaded report.</span></span>  

![Телеметрия автомобилей Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="c2abb-339">**Обратите внимание, что в отчете шесть страниц.**</span><span class="sxs-lookup"><span data-stu-id="c2abb-339">**Note the report has six pages:**</span></span>  
<span data-ttu-id="c2abb-340">Страница 1. Плотность автомобиля.</span><span class="sxs-lookup"><span data-stu-id="c2abb-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="c2abb-341">Страница 2. Работоспособность автомобилей в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="c2abb-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="c2abb-342">Страница 3. Агрессивно управляемые автомобили.</span><span class="sxs-lookup"><span data-stu-id="c2abb-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="c2abb-343">Страница 4. Отозванные автомобили.</span><span class="sxs-lookup"><span data-stu-id="c2abb-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="c2abb-344">Страница 5. Автомобили с экономным расходом топлива.</span><span class="sxs-lookup"><span data-stu-id="c2abb-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="c2abb-345">Страница 6. Логотип компании Contoso.</span><span class="sxs-lookup"><span data-stu-id="c2abb-345">Page 6: Contoso Logo</span></span>  

![Подключенные автомобили Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="c2abb-347">**На странице 3**закрепите следующие данные.</span><span class="sxs-lookup"><span data-stu-id="c2abb-347">**From Page 3**, pin the following:</span></span>  

1. <span data-ttu-id="c2abb-348">Количество VIN</span><span class="sxs-lookup"><span data-stu-id="c2abb-348">Count of VIN</span></span>  
   ![Подключенные автомобили Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="c2abb-350">Агрессивно управляемые автомобили по моделям — каскадная диаграмма.</span><span class="sxs-lookup"><span data-stu-id="c2abb-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Телеметрия автомобиля — закрепление диаграмм 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="c2abb-352">**На странице 5**закрепите следующие данные.</span><span class="sxs-lookup"><span data-stu-id="c2abb-352">**From Page 5**, pin the following:</span></span> 

1. <span data-ttu-id="c2abb-353">Количество VIN</span><span class="sxs-lookup"><span data-stu-id="c2abb-353">Count of vin</span></span>    
   ![Телеметрия автомобиля — закрепление диаграмм 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="c2abb-355">Автомобили с экономным расходом топлива по моделям: гистограмма с группировкой.</span><span class="sxs-lookup"><span data-stu-id="c2abb-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Телеметрия автомобиля — закрепление диаграмм 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="c2abb-357">**На странице 4**закрепите следующие данные.</span><span class="sxs-lookup"><span data-stu-id="c2abb-357">**From Page 4**, pin the following:</span></span>  

1. <span data-ttu-id="c2abb-358">Количество VIN</span><span class="sxs-lookup"><span data-stu-id="c2abb-358">Count of vin</span></span>  
   ![Телеметрия автомобиля — закрепление диаграмм 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="c2abb-360">Отозванные автомобили по городам, моделям: диаграмма "дерево".</span><span class="sxs-lookup"><span data-stu-id="c2abb-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Телеметрия автомобиля — закрепление диаграмм 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="c2abb-362">**На странице 6**закрепите следующие данные.</span><span class="sxs-lookup"><span data-stu-id="c2abb-362">**From Page 6**, pin the following:</span></span>  

1. <span data-ttu-id="c2abb-363">Логотип компании Contoso Motors.</span><span class="sxs-lookup"><span data-stu-id="c2abb-363">Contoso Motors logo</span></span>  
   ![Телеметрия автомобиля — закрепление диаграмм 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="c2abb-365">**Упорядочение панели мониторинга**</span><span class="sxs-lookup"><span data-stu-id="c2abb-365">**Organize the dashboard**</span></span>  

1. <span data-ttu-id="c2abb-366">Перейдите к панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c2abb-366">Navigate to the dashboard</span></span>
2. <span data-ttu-id="c2abb-367">Наведите указатель на каждую диаграмму и переименуйте ее на основании наименований на приведенном ниже изображении панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c2abb-367">Hover over each chart and rename it based on the naming provided in the complete dashboard image below.</span></span> <span data-ttu-id="c2abb-368">Расположите диаграммы, как показано на экране панели мониторинга ниже.</span><span class="sxs-lookup"><span data-stu-id="c2abb-368">Also move the charts around to look like the dashboard below.</span></span>  
   ![Телеметрия автомобиля — упорядочение панели мониторинга 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Телеметрия автомобилей Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="c2abb-371">Если вы создали все отчеты, рассмотренные в этой статье, настроенная панель мониторинга будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c2abb-371">If you have created all the reports as mentioned in this document, the final completed dashboard should look like the following figure.</span></span> 

![Телеметрия автомобиля — упорядочение панели мониторинга 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="c2abb-373">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="c2abb-373">Congratulations!</span></span> <span data-ttu-id="c2abb-374">Вы создали отчеты и панель мониторинга для сбора данных о состоянии автомобилей и манере вождения (в том числе прогнозные данные и данные пакетной обработки) в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="c2abb-374">You have successfully created the reports and the dashboard to gain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
