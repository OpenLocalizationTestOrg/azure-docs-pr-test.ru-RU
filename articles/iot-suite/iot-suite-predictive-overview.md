---
title: "Предварительно настроенное решение диагностического обслуживания | Документация Майкрософт"
description: "Описание предварительно настроенного решения прогнозируемого обслуживания Azure IoT Suite."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 8bad198488c4940a83eb32ec02122a91d47ca86c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="32843-103">Обзор предварительно настроенного решения прогнозируемого обслуживания</span><span class="sxs-lookup"><span data-stu-id="32843-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="32843-104">[Предварительно настроенное решение][lnk_preconfigured_solutions] *диагностического обслуживания* является одним из предварительно настроенных решений, выпущенных как часть пакета [Azure IoT Suite][lnk_iot_suite].</span><span class="sxs-lookup"><span data-stu-id="32843-104">The *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of the [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="32843-105">Это решение интегрирует сбор данных телеметрии устройства в режиме реального времени и прогнозируемую модель, созданную с помощью [машинного обучения Azure][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="32843-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="32843-106">Azure IoT Suite позволяет быстро подключаться к ресурсам и отслеживать их, а также анализировать данные телеметрии в реальном времени с помощью панелей мониторинга и визуализаций.</span><span class="sxs-lookup"><span data-stu-id="32843-106">With Azure IoT Suite, you can quickly and easily connect to and monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="32843-107">Панели мониторинга и визуализации в решении прогнозного обслуживания предоставляют новые возможности аналитики, которые могут повысить эффективность работы и увеличить доход.</span><span class="sxs-lookup"><span data-stu-id="32843-107">In the predictive maintenance solution, the dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="the-scenario"></a><span data-ttu-id="32843-108">Сценарий</span><span class="sxs-lookup"><span data-stu-id="32843-108">The Scenario</span></span>

<span data-ttu-id="32843-109">Компания Fabrikam является региональной авиалинией, которая концентрируется на хорошем впечатлении клиентов по приемлемым ценам.</span><span class="sxs-lookup"><span data-stu-id="32843-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="32843-110">Одной из причин задержки рейсов являются проблемы обслуживания, в частности, особенно сложной задачей является обслуживание двигателей самолетов.</span><span class="sxs-lookup"><span data-stu-id="32843-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="32843-111">Компания Fabrikam должна избегать сбоя двигателя во время полета любой ценой, поэтому она регулярно выполняет проверку двигателей и придерживается программы запланированного обслуживания.</span><span class="sxs-lookup"><span data-stu-id="32843-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according to a plan.</span></span> <span data-ttu-id="32843-112">Однако износ двигателей самолетов не всегда одинаков.</span><span class="sxs-lookup"><span data-stu-id="32843-112">However, aircraft engines don’t always wear the same.</span></span> <span data-ttu-id="32843-113">В некоторых случаях выполняется ненужное обслуживание двигателей.</span><span class="sxs-lookup"><span data-stu-id="32843-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="32843-114">Что более важно, возникают проблемы, которые могут задержать самолет на земле до проведения обслуживания.</span><span class="sxs-lookup"><span data-stu-id="32843-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="32843-115">Это приводит к дорогостоящим задержкам, особенно если самолет находится там, где недоступны нужные специалисты или запасные части.</span><span class="sxs-lookup"><span data-stu-id="32843-115">If an aircraft is at a location where the right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="32843-116">Самолеты компании Fabrikam снабжены датчиками, которые отслеживают состояние двигателей во время полета.</span><span class="sxs-lookup"><span data-stu-id="32843-116">The engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="32843-117">В компании Fabrikam используют решение прогнозного обслуживания для сбора данных датчиков во время полета.</span><span class="sxs-lookup"><span data-stu-id="32843-117">Fabrikam uses the predictive maintenance solution to collect the sensor data collected during the flight.</span></span> <span data-ttu-id="32843-118">После нескольких лет накопления данных о работе и сбоях двигателей специалисты по анализу данных Fabrikam смоделировали способ прогнозирования оставшегося полезного срока службы (RUL) двигателя самолета.</span><span class="sxs-lookup"><span data-stu-id="32843-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="32843-119">В модели используется корреляция между данными четырех датчиков двигателя и износом двигателя (что в конечном счете и приводит к сбою).</span><span class="sxs-lookup"><span data-stu-id="32843-119">The model uses a correlation between data from four of the engine sensors and engine wear that leads to eventual failure.</span></span> <span data-ttu-id="32843-120">Хотя компания Fabrikam продолжает выполнять регулярные проверки, чтобы обеспечить безопасность, она теперь может использовать модели для вычисления RUL каждого двигателя после каждого рейса.</span><span class="sxs-lookup"><span data-stu-id="32843-120">While Fabrikam continues to perform regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span></span> <span data-ttu-id="32843-121">Модель использует данные телеметрии, собранные на двигателях во время полета.</span><span class="sxs-lookup"><span data-stu-id="32843-121">The model uses the telemetry collected from the engines during the flight.</span></span> <span data-ttu-id="32843-122">Fabrikam теперь может прогнозировать будущие точки сбоя и планировать обслуживание и ремонт заранее.</span><span class="sxs-lookup"><span data-stu-id="32843-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="32843-123">Модель решений использует данные о фактическом износе двигателя.</span><span class="sxs-lookup"><span data-stu-id="32843-123">The solution model uses actual engine wear data.</span></span>

<span data-ttu-id="32843-124">Получив возможность прогнозировать момент, когда понадобится обслуживание, Fabrikam может оптимизировать операции для снижения затрат.</span><span class="sxs-lookup"><span data-stu-id="32843-124">By predicting the point when maintenance is required, Fabrikam can optimize its operations to reduce costs.</span></span>

<span data-ttu-id="32843-125">Координаторы технического обслуживания работают с планировщиками:</span><span class="sxs-lookup"><span data-stu-id="32843-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="32843-126">чтобы запланировать обслуживание там, где предполагается промежуточная посадка самолета;</span><span class="sxs-lookup"><span data-stu-id="32843-126">Plan maintenance to coincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="32843-127">чтобы обеспечить достаточное время для обслуживания самолета, не вызывая перебоев в расписании;</span><span class="sxs-lookup"><span data-stu-id="32843-127">Ensure sufficient time is available for the aircraft to be out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="32843-128">чтобы запланировать работу специалистов, что позволит обслуживать самолеты эффективно и без потери времени на ожидание.</span><span class="sxs-lookup"><span data-stu-id="32843-128">To schedule technicians to ensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="32843-129">Менеджеры снабжения получают планы обслуживания, чтобы оптимизировать процесс размещения заказов и хранение запасных частей.</span><span class="sxs-lookup"><span data-stu-id="32843-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="32843-130">Эти мероприятия позволяют Fabrikam минимизировать время, проведенное самолетом на земле, и снизить эксплуатационные расходы, одновременно обеспечивая безопасность пассажиров и сотрудников.</span><span class="sxs-lookup"><span data-stu-id="32843-130">These activities enable Fabrikam to minimize aircraft ground time and reduce operating costs while ensuring the safety of passengers and crew.</span></span>

<span data-ttu-id="32843-131">Чтобы понять, как [Azure IoT Suite][lnk_iot_suite] предоставляет возможности, необходимые клиентам для реализации потенциала диагностического обслуживания, просмотрите эту [инфографику][lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="32843-131">To understand how [Azure IoT Suite][lnk_iot_suite] provides the capabilities customers need to realize the potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-the-predictive-maintenance-solution-is-built"></a><span data-ttu-id="32843-132">Принцип построения решения прогнозируемого обслуживания</span><span class="sxs-lookup"><span data-stu-id="32843-132">How the predictive maintenance solution is built</span></span>

<span data-ttu-id="32843-133">Чтобы продемонстрировать эти возможности на основе данных телеметрии устройства, собранных с помощью служб IoT Suite, решение использует существующую модель машинного обучения Azure, доступную в виде шаблона.</span><span class="sxs-lookup"><span data-stu-id="32843-133">The solution uses an existing Azure Machine Learning model available as a template to show these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="32843-134">Корпорация Майкрософт разработала [модель регрессии][lnk_regression_model] двигателя самолета на основе общедоступных данных <sup>\[1\]</sup> и пошаговое руководство по использованию модели.</span><span class="sxs-lookup"><span data-stu-id="32843-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how to use the model.</span></span>

<span data-ttu-id="32843-135">Решение прогнозного обслуживания Azure IoT использует модель регрессии, созданную на основе этого шаблона.</span><span class="sxs-lookup"><span data-stu-id="32843-135">The Azure IoT predictive maintenance solution uses the regression model created from this template.</span></span> <span data-ttu-id="32843-136">Это решение развертывается в подписке Azure и предоставляется с помощью автоматически созданного интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="32843-136">The model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="32843-137">Решение включает набор проверочных данных, представляющий 4 (из 100) двигателя и 4 (из 21) потока данных датчиков.</span><span class="sxs-lookup"><span data-stu-id="32843-137">The solution includes a subset of the testing data representing 4 (of 100 total) engines and the 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="32843-138">Эти данные обеспечивают точный результат из обученной модели.</span><span class="sxs-lookup"><span data-stu-id="32843-138">This data is sufficient to provide an accurate result from the trained model.</span></span>

<span data-ttu-id="32843-139">*\[1\] А. Саксена (A. Saxena) и К. Гебель (K. Goebel) (2008 г.). "Набор данных для симуляции деградации турбореактивного двигателя" (Turbofan Engine Degradation Simulation Data Set), Хранилище данных Центра прогнозирования Эймса (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/, Исследовательский центр Эймса, Моффетт-филд, Калифорния*</span><span class="sxs-lookup"><span data-stu-id="32843-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="32843-140">Приступая к работе с прогнозируемым обслуживанием</span><span class="sxs-lookup"><span data-stu-id="32843-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="32843-141">В этом руководстве показано, как подготовить решение прогнозируемого обслуживания.</span><span class="sxs-lookup"><span data-stu-id="32843-141">This tutorial shows you how to provision the predictive maintenance solution.</span></span> <span data-ttu-id="32843-142">Кроме того, здесь описываются основные функции этого решения.</span><span class="sxs-lookup"><span data-stu-id="32843-142">It also walks you through the basic features of the predictive maintenance solution.</span></span> <span data-ttu-id="32843-143">Многие функции доступны на панели мониторинга решения, которая развертывается вместе с предварительно настроенным решением:</span><span class="sxs-lookup"><span data-stu-id="32843-143">You can access many of these features through the solution dashboard that deploys along with the preconfigured solution.</span></span>

<span data-ttu-id="32843-144">Для работы с этим руководством требуется активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="32843-144">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="32843-145">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="32843-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="32843-146">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="32843-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="32843-147">Войдите на сайт [azureiotsuite.com][lnk-azureiotsuite] с помощью учетных данных Azure и щелкните **+**, чтобы создать решение.</span><span class="sxs-lookup"><span data-stu-id="32843-147">Log on to [azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** to create a solution.</span></span>
1. <span data-ttu-id="32843-148">Щелкните, чтобы **выбрать** элемент **Predictive maintenance** (Прогнозируемое обслуживание).</span><span class="sxs-lookup"><span data-stu-id="32843-148">Click **Select** the **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="32843-149">Укажите **имя** для предварительно настроенного решения прогнозируемого обслуживания.</span><span class="sxs-lookup"><span data-stu-id="32843-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="32843-150">Выберите **область** и **подписку**, которые вы хотите использовать для подготовки решения.</span><span class="sxs-lookup"><span data-stu-id="32843-150">Select the **Region** and **Subscription** you want to use to provision the solution.</span></span>
1. <span data-ttu-id="32843-151">Щелкните **Создать решение** , чтобы начать процесс подготовки.</span><span class="sxs-lookup"><span data-stu-id="32843-151">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="32843-152">Этот процесс обычно занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="32843-152">This process typically takes several minutes to run.</span></span>

### <a name="wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="32843-153">Дождитесь завершения процесса подготовки.</span><span class="sxs-lookup"><span data-stu-id="32843-153">Wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="32843-154">Щелкните плитку решения с состоянием **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="32843-154">Click the tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="32843-155">Следите за **состояниями подготовки** по мере развертывания служб Azure в рамках подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="32843-155">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="32843-156">Когда подготовка будет завершена, состояние изменится на **Готово**.</span><span class="sxs-lookup"><span data-stu-id="32843-156">Once provisioning completes, the status changes to **Ready**.</span></span>
1. <span data-ttu-id="32843-157">Щелкните плитку, чтобы просмотреть подробные сведения о решении на правой панели.</span><span class="sxs-lookup"><span data-stu-id="32843-157">Click the tile to see the details of your solution in the right-hand pane.</span></span> <span data-ttu-id="32843-158">На этой панели можно запустить панель мониторинга решения и получить доступ к рабочей области машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="32843-158">From this pane, you can launch the solution dashboard and access the Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="32843-159">Если при развертывании предварительно настроенного решения возникают проблемы, см. статьи [Разрешения на сайте azureiotsuite.com][lnk-permissions] и [Часто задаваемые вопросы об IoT Suite][lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="32843-159">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [FAQ][lnk-faq].</span></span> <span data-ttu-id="32843-160">Если проблемы не удается устранить, отправьте запрос в службу поддержки на [портале][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="32843-160">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="32843-161">Есть ли сведения, которые вы ожидали увидеть и которые не указаны для вашего решения?</span><span class="sxs-lookup"><span data-stu-id="32843-161">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="32843-162">Сообщите нам о своих предложениях на сайте [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="32843-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-the-solution"></a><span data-ttu-id="32843-163">Просмотр решения</span><span class="sxs-lookup"><span data-stu-id="32843-163">View the solution</span></span>

<span data-ttu-id="32843-164">В этом разделе рассматривается пользовательский интерфейс решения.</span><span class="sxs-lookup"><span data-stu-id="32843-164">This section guides you through the solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="32843-165">Панель мониторинга диагностического обслуживания</span><span class="sxs-lookup"><span data-stu-id="32843-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="32843-166">Эта страница веб-приложения использует элементы управления PowerBI JavaScript (см. [репозиторий визуальных элементов PowerBI][lnk-powerbi]) для визуализации:</span><span class="sxs-lookup"><span data-stu-id="32843-166">This page in the web application uses PowerBI JavaScript controls (see the [PowerBI-visuals repository][lnk-powerbi]) to visualize:</span></span>

* <span data-ttu-id="32843-167">выходных данных из задания Stream Analytics, поступающих в хранилище BLOB-объектов;</span><span class="sxs-lookup"><span data-stu-id="32843-167">The output data from the Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="32843-168">значений остаточного срока эксплуатации и количества циклов для каждого двигателя самолета.</span><span class="sxs-lookup"><span data-stu-id="32843-168">The RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-the-behavior-of-the-cloud-solution"></a><span data-ttu-id="32843-169">Наблюдение за поведением облачного решения</span><span class="sxs-lookup"><span data-stu-id="32843-169">Observing the behavior of the cloud solution</span></span>

<span data-ttu-id="32843-170">Чтобы просмотреть подготовленные ресурсы, на портале Azure перейдите к группе ресурсов с выбранным вами именем решения.</span><span class="sxs-lookup"><span data-stu-id="32843-170">In the Azure portal, navigate to the resource group with the solution name you chose to view your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="32843-171">При подготовке предварительно настроенного решения вы получите электронное сообщение со ссылкой на рабочую область машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="32843-171">When you provision the preconfigured solution, you receive an email with a link to the Machine Learning workspace.</span></span> <span data-ttu-id="32843-172">Кроме того, вы можете перейти в рабочую область машинного обучения со страницы [azureiotsuite.com][lnk-azureiotsuite] подготовленного решения.</span><span class="sxs-lookup"><span data-stu-id="32843-172">You can also navigate to the Machine Learning workspace from the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="32843-173">На этой странице отображается плитка для перехода, когда решение находится в состоянии **Готово**.</span><span class="sxs-lookup"><span data-stu-id="32843-173">A tile is available on this page when the solution is in the **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="32843-174">На портале решения можно увидеть, что в этом примере есть четыре виртуальных устройства, представляющие два самолета с двумя двигателями в каждом. При этом на каждом двигателе установлено по четыре датчика.</span><span class="sxs-lookup"><span data-stu-id="32843-174">In the solution portal, you can see that the sample is provisioned with four simulated devices to represent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="32843-175">При первом переходе на портал решения моделирование будет остановлено.</span><span class="sxs-lookup"><span data-stu-id="32843-175">When you first navigate to the solution portal, the simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="32843-176">Щелкните **Запустить имитацию**, чтобы начать моделирование.</span><span class="sxs-lookup"><span data-stu-id="32843-176">Click **Start simulation** to begin the simulation.</span></span> <span data-ttu-id="32843-177">На панели мониторинга отобразится журнал датчика, оставшийся срок полезного использования, циклы и журнал оставшегося срока полезного использования.</span><span class="sxs-lookup"><span data-stu-id="32843-177">The sensor history, RUL, Cycles, and RUL history populate the dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="32843-178">Когда значение оставшегося срока полезного использования станет меньше 160 (произвольное пороговое значение, выбранное для демонстрационных целей), на портале решения рядом с этим значением появится символ предупреждения.</span><span class="sxs-lookup"><span data-stu-id="32843-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display.</span></span> <span data-ttu-id="32843-179">Кроме того, цвет двигателя на портале решения изменится на желтый.</span><span class="sxs-lookup"><span data-stu-id="32843-179">The solution portal also highlights the aircraft engine in yellow.</span></span> <span data-ttu-id="32843-180">Как можно заметить, значения оставшегося срока полезного использования имеют общую тенденцию к уменьшению, но при этом наблюдаются скачки вверх и вниз.</span><span class="sxs-lookup"><span data-stu-id="32843-180">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span></span> <span data-ttu-id="32843-181">Это происходит из-за различной продолжительности циклов и точности модели.</span><span class="sxs-lookup"><span data-stu-id="32843-181">This behavior results from the varying cycle lengths and the model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="32843-182">Полное моделирование, которое включает 148 циклов, занимает около 35 минут.</span><span class="sxs-lookup"><span data-stu-id="32843-182">The full simulation takes around 35 minutes to complete 148 cycles.</span></span> <span data-ttu-id="32843-183">Пороговое значение остаточного срока эксплуатации, равное 160, достигается примерно через 5 минут, а порог для обоих двигателей достигается примерно через 8 минут.</span><span class="sxs-lookup"><span data-stu-id="32843-183">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span></span>

<span data-ttu-id="32843-184">В процессе моделирования обрабатывается весь набор данных со 148 циклами. В результате можно получить окончательные значения остаточного срока эксплуатации и количества выполненных циклов.</span><span class="sxs-lookup"><span data-stu-id="32843-184">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="32843-185">Моделирование можно остановить в любой момент, но, если нажать кнопку **Запустить моделирование** , процесс перезапустится с самого начала.</span><span class="sxs-lookup"><span data-stu-id="32843-185">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32843-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32843-186">Next steps</span></span>

<span data-ttu-id="32843-187">Дополнительные сведения о том, как Интернет вещей Azure реализует сценарии диагностического обслуживания, см. в статье [Захват значения из Интернета вещей][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="32843-187">To learn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from the Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="32843-188">Воспользуйтесь [пошаговым руководством][lnk-predictive-walkthrough] по работе с решением прогнозного обслуживания.</span><span class="sxs-lookup"><span data-stu-id="32843-188">Take a [walkthrough][lnk-predictive-walkthrough] of the predictive maintenance solution.</span></span>

<span data-ttu-id="32843-189">Вы также можете ознакомиться с другими функциями и возможностями предварительно настроенных решений IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="32843-189">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="32843-190">[Часто задаваемые вопросы об IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="32843-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="32843-191">[Все аспекты безопасности Интернета вещей][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="32843-191">[IoT security from the ground up][lnk-security-groundup]</span></span>

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/