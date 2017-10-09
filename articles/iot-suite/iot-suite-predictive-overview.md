---
title: "обслуживание aaaPredictive предварительно настроенное решение | Документы Microsoft"
description: "Описание hello Azure IoT Suite превентивного обслуживания предварительно настроенных решений."
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
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="8917a-103">Обзор предварительно настроенного решения прогнозируемого обслуживания</span><span class="sxs-lookup"><span data-stu-id="8917a-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="8917a-104">Hello *превентивного обслуживания* [предварительно настроенное решение] [ lnk_preconfigured_solutions] является одним из hello [Microsoft Azure IoT Suite] [ lnk_iot_suite] предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="8917a-104">hello *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of hello [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="8917a-105">Это решение интегрирует сбор данных телеметрии устройства в режиме реального времени и прогнозируемую модель, созданную с помощью [машинного обучения Azure][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="8917a-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="8917a-106">С Azure IoT Suite можно быстро и легко подключиться tooand монитор ресурсов и анализ телеметрии в режиме реального времени в панелях мониторинга и визуализации.</span><span class="sxs-lookup"><span data-stu-id="8917a-106">With Azure IoT Suite, you can quickly and easily connect tooand monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="8917a-107">В решении превентивного обслуживания hello hello информационные панели и визуализации предоставляют новой аналитики, которые можно диска эффективность и улучшить дохода.</span><span class="sxs-lookup"><span data-stu-id="8917a-107">In hello predictive maintenance solution, hello dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="hello-scenario"></a><span data-ttu-id="8917a-108">Hello сценария</span><span class="sxs-lookup"><span data-stu-id="8917a-108">hello Scenario</span></span>

<span data-ttu-id="8917a-109">Компания Fabrikam является региональной авиалинией, которая концентрируется на хорошем впечатлении клиентов по приемлемым ценам.</span><span class="sxs-lookup"><span data-stu-id="8917a-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="8917a-110">Одной из причин задержки рейсов являются проблемы обслуживания, в частности, особенно сложной задачей является обслуживание двигателей самолетов.</span><span class="sxs-lookup"><span data-stu-id="8917a-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="8917a-111">Fabrikam необходимо избежать сбоя Ядро во время рейса любой ценой, поэтому регулярно проверяет ядра и планирует в соответствии с tooa плана обслуживания.</span><span class="sxs-lookup"><span data-stu-id="8917a-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according tooa plan.</span></span> <span data-ttu-id="8917a-112">Тем не менее самолет, модули не всегда носить hello таким же.</span><span class="sxs-lookup"><span data-stu-id="8917a-112">However, aircraft engines don’t always wear hello same.</span></span> <span data-ttu-id="8917a-113">В некоторых случаях выполняется ненужное обслуживание двигателей.</span><span class="sxs-lookup"><span data-stu-id="8917a-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="8917a-114">Что более важно, возникают проблемы, которые могут задержать самолет на земле до проведения обслуживания.</span><span class="sxs-lookup"><span data-stu-id="8917a-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="8917a-115">Если самолете находится в расположении где hello правой специалистов или запасные части недоступны, эти проблемы может быть особенно много ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8917a-115">If an aircraft is at a location where hello right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="8917a-116">Hello механизмах самолет Fabrikam инструментирования с датчиками, отслеживающих ядре СУБД во время рейса.</span><span class="sxs-lookup"><span data-stu-id="8917a-116">hello engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="8917a-117">Fabrikam использует датчик hello превентивного обслуживания решение toocollect hello данные, собранные во время полета hello.</span><span class="sxs-lookup"><span data-stu-id="8917a-117">Fabrikam uses hello predictive maintenance solution toocollect hello sensor data collected during hello flight.</span></span> <span data-ttu-id="8917a-118">После накопления лет подсистемы оперативной и данные ошибки специалисты по анализу данных компании Fabrikam моделировать hello toopredict способом оставшийся срок службы (RUL) для механизма самолет.</span><span class="sxs-lookup"><span data-stu-id="8917a-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="8917a-119">Hello модель использует корреляцию между данными из четырех датчиков engine hello и одежды ядра, который ведет tooeventual сбоя.</span><span class="sxs-lookup"><span data-stu-id="8917a-119">hello model uses a correlation between data from four of hello engine sensors and engine wear that leads tooeventual failure.</span></span> <span data-ttu-id="8917a-120">Прерывая Fabrikam tooperform регулярных проверок tooensure безопасности его теперь можно использовать hello моделей toocompute hello RUL для каждого ядра после каждого рейса.</span><span class="sxs-lookup"><span data-stu-id="8917a-120">While Fabrikam continues tooperform regular inspections tooensure safety, it can now use hello models toocompute hello RUL for each engine after every flight.</span></span> <span data-ttu-id="8917a-121">Hello модель использует hello телеметрии, собранных на основе механизмов hello в течение рейса hello.</span><span class="sxs-lookup"><span data-stu-id="8917a-121">hello model uses hello telemetry collected from hello engines during hello flight.</span></span> <span data-ttu-id="8917a-122">Fabrikam теперь может прогнозировать будущие точки сбоя и планировать обслуживание и ремонт заранее.</span><span class="sxs-lookup"><span data-stu-id="8917a-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="8917a-123">модель решения Hello использует данные износ фактические ядра.</span><span class="sxs-lookup"><span data-stu-id="8917a-123">hello solution model uses actual engine wear data.</span></span>

<span data-ttu-id="8917a-124">Прогнозирование hello точки, при необходимости обслуживания, Fabrikam оптимизировать его стоимости tooreduce операций.</span><span class="sxs-lookup"><span data-stu-id="8917a-124">By predicting hello point when maintenance is required, Fabrikam can optimize its operations tooreduce costs.</span></span>

<span data-ttu-id="8917a-125">Координаторы технического обслуживания работают с планировщиками:</span><span class="sxs-lookup"><span data-stu-id="8917a-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="8917a-126">План обслуживания toocoincide с самолете остановки в определенном месте.</span><span class="sxs-lookup"><span data-stu-id="8917a-126">Plan maintenance toocoincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="8917a-127">Убедитесь, что достаточно времени для hello самолет toobe обслуживания без вызвал перерыв в работе расписания.</span><span class="sxs-lookup"><span data-stu-id="8917a-127">Ensure sufficient time is available for hello aircraft toobe out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="8917a-128">tooensure специалистов tooschedule эффективно обслуживать самолет без времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="8917a-128">tooschedule technicians tooensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="8917a-129">Менеджеры снабжения получают планы обслуживания, чтобы оптимизировать процесс размещения заказов и хранение запасных частей.</span><span class="sxs-lookup"><span data-stu-id="8917a-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="8917a-130">Эти действия включить Fabrikam toominimize самолет фактическое время и сократить эксплуатационные расходы, одновременно обеспечивая безопасность hello пассажиров и сотрудники.</span><span class="sxs-lookup"><span data-stu-id="8917a-130">These activities enable Fabrikam toominimize aircraft ground time and reduce operating costs while ensuring hello safety of passengers and crew.</span></span>

<span data-ttu-id="8917a-131">toounderstand как [Azure IoT Suite] [ lnk_iot_suite] предоставляет hello возможности клиенты должны toorealize hello потенциал превентивного обслуживания просмотрите это [инфографикой] [lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="8917a-131">toounderstand how [Azure IoT Suite][lnk_iot_suite] provides hello capabilities customers need toorealize hello potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-hello-predictive-maintenance-solution-is-built"></a><span data-ttu-id="8917a-132">Построение решения превентивного обслуживания hello</span><span class="sxs-lookup"><span data-stu-id="8917a-132">How hello predictive maintenance solution is built</span></span>

<span data-ttu-id="8917a-133">Hello решение использует существующую модель машинного обучения Azure как tooshow шаблона эти возможности работать из устройства телеметрии, полученные через IoT Suite служб.</span><span class="sxs-lookup"><span data-stu-id="8917a-133">hello solution uses an existing Azure Machine Learning model available as a template tooshow these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="8917a-134">Корпорация Майкрософт создала [модель регрессии] [ lnk_regression_model] подсистемы самолет, на основе данных общедоступные<sup>\[1\]</sup>и пошаговые руководство по как toouse hello модели.</span><span class="sxs-lookup"><span data-stu-id="8917a-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how toouse hello model.</span></span>

<span data-ttu-id="8917a-135">Hello превентивного обслуживания решения Azure IoT используется модель регрессии hello, созданные по этому шаблону.</span><span class="sxs-lookup"><span data-stu-id="8917a-135">hello Azure IoT predictive maintenance solution uses hello regression model created from this template.</span></span> <span data-ttu-id="8917a-136">развертывается в вашей подписке Azure и через API-Интерфейс автоматически созданный Hello модели.</span><span class="sxs-lookup"><span data-stu-id="8917a-136">hello model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="8917a-137">Hello решение включает в себя набор проверочных данных, представляющий 4 (всего 100) hello ядер и потоков данных датчика hello 4 (от 21 общее).</span><span class="sxs-lookup"><span data-stu-id="8917a-137">hello solution includes a subset of hello testing data representing 4 (of 100 total) engines and hello 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="8917a-138">Эти данные имеют достаточные tooprovide точный результат из обученной модели hello.</span><span class="sxs-lookup"><span data-stu-id="8917a-138">This data is sufficient tooprovide an accurate result from hello trained model.</span></span>

<span data-ttu-id="8917a-139">*\[1\] А. Саксена (A. Saxena) и К. Гебель (K. Goebel) (2008 г.). "Набор данных для симуляции деградации турбореактивного двигателя" (Turbofan Engine Degradation Simulation Data Set), Хранилище данных Центра прогнозирования Эймса (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/, Исследовательский центр Эймса, Моффетт-филд, Калифорния*</span><span class="sxs-lookup"><span data-stu-id="8917a-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="8917a-140">Приступая к работе с прогнозируемым обслуживанием</span><span class="sxs-lookup"><span data-stu-id="8917a-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="8917a-141">Этом учебнике показано, как tooprovision hello решения превентивного обслуживания.</span><span class="sxs-lookup"><span data-stu-id="8917a-141">This tutorial shows you how tooprovision hello predictive maintenance solution.</span></span> <span data-ttu-id="8917a-142">Он также поможет выполнить основные функции hello hello превентивного обслуживания решения.</span><span class="sxs-lookup"><span data-stu-id="8917a-142">It also walks you through hello basic features of hello predictive maintenance solution.</span></span> <span data-ttu-id="8917a-143">Многие из этих средств можно обращаться решения hello панель мониторинга, которая развертывает вместе с hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="8917a-143">You can access many of these features through hello solution dashboard that deploys along with hello preconfigured solution.</span></span>

<span data-ttu-id="8917a-144">toocomplete этого учебника требуется Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="8917a-144">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="8917a-145">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8917a-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8917a-146">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="8917a-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="8917a-147">Войдите на слишком[azureiotsuite.com] [ lnk-azureiotsuite] Azure с помощью учетных данных учетной записи и нажмите кнопку  **+**  toocreate решения.</span><span class="sxs-lookup"><span data-stu-id="8917a-147">Log on too[azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** toocreate a solution.</span></span>
1. <span data-ttu-id="8917a-148">Нажмите кнопку **выберите** hello **превентивного обслуживания** плитки.</span><span class="sxs-lookup"><span data-stu-id="8917a-148">Click **Select** hello **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="8917a-149">Укажите **имя** для предварительно настроенного решения прогнозируемого обслуживания.</span><span class="sxs-lookup"><span data-stu-id="8917a-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="8917a-150">Выберите hello **область** и **подписки** toouse tooprovision hello решение.</span><span class="sxs-lookup"><span data-stu-id="8917a-150">Select hello **Region** and **Subscription** you want toouse tooprovision hello solution.</span></span>
1. <span data-ttu-id="8917a-151">Нажмите кнопку **создать решение** toobegin hello процесса подготовки.</span><span class="sxs-lookup"><span data-stu-id="8917a-151">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="8917a-152">Этот процесс обычно занимает несколько минут toorun.</span><span class="sxs-lookup"><span data-stu-id="8917a-152">This process typically takes several minutes toorun.</span></span>

### <a name="wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="8917a-153">Дождитесь подготовки процесса toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="8917a-153">Wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="8917a-154">Щелкните плитку hello в решении с **Provisioning** состояния.</span><span class="sxs-lookup"><span data-stu-id="8917a-154">Click hello tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="8917a-155">Обратите внимание hello **подготовки состояний** мере развертывания служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="8917a-155">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="8917a-156">После завершения подготовки hello изменения состояния слишком**готовности**.</span><span class="sxs-lookup"><span data-stu-id="8917a-156">Once provisioning completes, hello status changes too**Ready**.</span></span>
1. <span data-ttu-id="8917a-157">Нажмите кнопку сведения hello toosee плитки hello решения в правой области окна hello.</span><span class="sxs-lookup"><span data-stu-id="8917a-157">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span> <span data-ttu-id="8917a-158">В этой области можно запустить hello решения панели мониторинга и доступа hello рабочей области машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="8917a-158">From this pane, you can launch hello solution dashboard and access hello Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="8917a-159">Если возникли проблемы при развертывании hello предварительно настроенных решений, просмотрите [разрешения на сайт azureiotsuite.com hello] [ lnk-permissions] и hello [часто задаваемые вопросы о] [ lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="8917a-159">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [FAQ][lnk-faq].</span></span> <span data-ttu-id="8917a-160">Если сохранить проблемы hello, создать билет службы для hello [портала][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="8917a-160">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="8917a-161">Существуют следовало ожидать toosee сведения, которые отсутствуют в списке для вашего решения?</span><span class="sxs-lookup"><span data-stu-id="8917a-161">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="8917a-162">Сообщите нам о своих предложениях на сайте [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="8917a-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-hello-solution"></a><span data-ttu-id="8917a-163">Представление решения hello</span><span class="sxs-lookup"><span data-stu-id="8917a-163">View hello solution</span></span>

<span data-ttu-id="8917a-164">Этот раздел поможет выполнить решение hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="8917a-164">This section guides you through hello solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="8917a-165">Панель мониторинга диагностического обслуживания</span><span class="sxs-lookup"><span data-stu-id="8917a-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="8917a-166">Эта страница в веб-приложение hello использует элементы управления PowerBI JavaScript (hello в разделе [репозитория визуальных элементов PowerBI][lnk-powerbi]) toovisualize:</span><span class="sxs-lookup"><span data-stu-id="8917a-166">This page in hello web application uses PowerBI JavaScript controls (see hello [PowerBI-visuals repository][lnk-powerbi]) toovisualize:</span></span>

* <span data-ttu-id="8917a-167">Hello выходных данных из задания Stream Analytics hello в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="8917a-167">hello output data from hello Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="8917a-168">Hello RUL и цикл количество на самолет ядра.</span><span class="sxs-lookup"><span data-stu-id="8917a-168">hello RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a><span data-ttu-id="8917a-169">Контролирует поведение hello hello облачные решения</span><span class="sxs-lookup"><span data-stu-id="8917a-169">Observing hello behavior of hello cloud solution</span></span>

<span data-ttu-id="8917a-170">В hello портал Azure, перейдите toohello группы ресурсов с именем решения hello выбрано tooview подготовленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8917a-170">In hello Azure portal, navigate toohello resource group with hello solution name you chose tooview your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="8917a-171">При подготовке hello предварительно настроенных решений появится сообщение электронной почты с рабочей области машинного обучения toohello ссылку.</span><span class="sxs-lookup"><span data-stu-id="8917a-171">When you provision hello preconfigured solution, you receive an email with a link toohello Machine Learning workspace.</span></span> <span data-ttu-id="8917a-172">Вы также можете переходить рабочей области машинного обучения toohello из hello [azureiotsuite.com] [ lnk-azureiotsuite] страницы для предоставленного решения.</span><span class="sxs-lookup"><span data-stu-id="8917a-172">You can also navigate toohello Machine Learning workspace from hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="8917a-173">Плитки доступно на этой странице, когда решение hello в hello **готовности** состояния.</span><span class="sxs-lookup"><span data-stu-id="8917a-173">A tile is available on this page when hello solution is in hello **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="8917a-174">Hello решение портала можно видно, что этот образец hello, предоставляется два самолет toorepresent четырех устройств, имитация двух ядер на самолет, каждый из которых четыре датчиков.</span><span class="sxs-lookup"><span data-stu-id="8917a-174">In hello solution portal, you can see that hello sample is provisioned with four simulated devices toorepresent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="8917a-175">При переходе сначала toohello решение портала моделирование hello остановлена.</span><span class="sxs-lookup"><span data-stu-id="8917a-175">When you first navigate toohello solution portal, hello simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="8917a-176">Нажмите кнопку **запустить моделирование** toobegin hello моделирования.</span><span class="sxs-lookup"><span data-stu-id="8917a-176">Click **Start simulation** toobegin hello simulation.</span></span> <span data-ttu-id="8917a-177">Здравствуйте журнал датчика, RUL, циклы и RUL hello мониторинга заполнения журнала.</span><span class="sxs-lookup"><span data-stu-id="8917a-177">hello sensor history, RUL, Cycles, and RUL history populate hello dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="8917a-178">Когда RUL меньше, чем 160 (произвольный пороговое значение для демонстрационных целей), hello решения портал отобразит предупреждение символ Далее toohello, RUL отображения.</span><span class="sxs-lookup"><span data-stu-id="8917a-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), hello solution portal displays a warning symbol next toohello RUL display.</span></span> <span data-ttu-id="8917a-179">портал Hello решения также выделяется engine самолет hello желтым цветом.</span><span class="sxs-lookup"><span data-stu-id="8917a-179">hello solution portal also highlights hello aircraft engine in yellow.</span></span> <span data-ttu-id="8917a-180">Обратите внимание на то, как значения RUL hello имеют общие вниз общая тенденция, но, как правило, toobounce вверх и вниз.</span><span class="sxs-lookup"><span data-stu-id="8917a-180">Notice how hello RUL values have a general downward trend overall, but tend toobounce up and down.</span></span> <span data-ttu-id="8917a-181">Это поведение возникает в результате hello переменной цикла длины и точности модели hello.</span><span class="sxs-lookup"><span data-stu-id="8917a-181">This behavior results from hello varying cycle lengths and hello model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="8917a-182">Полное моделирование Hello занимает около 35 минут toocomplete 148 циклов.</span><span class="sxs-lookup"><span data-stu-id="8917a-182">hello full simulation takes around 35 minutes toocomplete 148 cycles.</span></span> <span data-ttu-id="8917a-183">Оба ядер попадания hello пороговое значение на около 8 минут и Hello 160 RUL порога для hello первый раз около 5 минут.</span><span class="sxs-lookup"><span data-stu-id="8917a-183">hello 160 RUL threshold is met for hello first time at around 5 minutes and both engines hit hello threshold at around 8 minutes.</span></span>

<span data-ttu-id="8917a-184">Моделирование Hello завершит hello всего набора данных для 148 циклов и сопоставляет окончательного значения RUL и цикла.</span><span class="sxs-lookup"><span data-stu-id="8917a-184">hello simulation runs through hello complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="8917a-185">Вы можете остановить hello моделирование на любом этапе точка, но щелкнув **запустить моделирование** воспроизведения hello моделирование с начала hello hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="8917a-185">You can stop hello simulation at any point, but clicking **Start Simulation** replays hello simulation from hello start of hello dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8917a-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8917a-186">Next steps</span></span>

<span data-ttu-id="8917a-187">toolearn Дополнительные сведения о как Azure IoT позволяет использовать сценарии превентивного обслуживания, чтение [записать значение из Интернета вещей hello][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="8917a-187">toolearn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from hello Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="8917a-188">Принимать [Пошаговое руководство] [ lnk-predictive-walkthrough] решения hello превентивного обслуживания.</span><span class="sxs-lookup"><span data-stu-id="8917a-188">Take a [walkthrough][lnk-predictive-walkthrough] of hello predictive maintenance solution.</span></span>

<span data-ttu-id="8917a-189">Можно также изучить некоторые hello и другие возможности hello IoT Suite предварительно настроенных решений:</span><span class="sxs-lookup"><span data-stu-id="8917a-189">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="8917a-190">[Часто задаваемые вопросы об IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="8917a-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="8917a-191">[Основание безопасности IoT из hello,][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="8917a-191">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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