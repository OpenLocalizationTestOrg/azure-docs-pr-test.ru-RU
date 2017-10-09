---
title: "Обзор фабрики подключен aaaAzure IoT Suite | Документы Microsoft"
description: "Описание hello Azure IoT Suite подключен фабрики предварительно настроенных решений."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a><span data-ttu-id="d0346-103">Приступая к работе с hello подключен фабрики предварительно настроенных решений</span><span class="sxs-lookup"><span data-stu-id="d0346-103">Get started with hello connected factory preconfigured solution</span></span>

<span data-ttu-id="d0346-104">Azure IoT Suite [предварительно настроенных решений] [ lnk-preconfigured-solutions] объединить несколько конца в конец решений toodeliver Azure IoT служб, реализующие общих деловых сценариях IoT.</span><span class="sxs-lookup"><span data-stu-id="d0346-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="d0346-105">Hello *подключенных фабрики* предварительно настроенных решений подключается tooand мониторы промышленных устройствах.</span><span class="sxs-lookup"><span data-stu-id="d0346-105">hello *connected factory* preconfigured solution connects tooand monitors your industrial devices.</span></span> <span data-ttu-id="d0346-106">Можно использовать hello tooanalyze решения hello поток данных из устройств и повышения производительности рабочей toodrive и рентабельности.</span><span class="sxs-lookup"><span data-stu-id="d0346-106">You can use hello solution tooanalyze hello stream of data from your devices and toodrive operational productivity and profitability.</span></span>

<span data-ttu-id="d0346-107">В этом учебнике показано, как tooprovision hello подключаться фабрики предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="d0346-107">This tutorial shows you how tooprovision hello connected factory preconfigured solution.</span></span> <span data-ttu-id="d0346-108">Он также поможет выполнить основные функции hello hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="d0346-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="d0346-109">Многие из этих средств можно получить из решения hello *мониторинга* , которая выполняет развертывание в рамках hello предварительно настроенных решений:</span><span class="sxs-lookup"><span data-stu-id="d0346-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Панель мониторинга предварительно настроенного решения для подключенной фабрики][img-cf-home]

<span data-ttu-id="d0346-111">toocomplete этого учебника требуется Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="d0346-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d0346-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d0346-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d0346-113">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="d0346-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-hello-solution"></a><span data-ttu-id="d0346-114">Подготовка к работе hello решения</span><span class="sxs-lookup"><span data-stu-id="d0346-114">Provision hello solution</span></span>

1. <span data-ttu-id="d0346-115">Войдите в систему tooazureiotsuite.com, используя учетные данные учетной записи Azure и нажмите кнопку «**+**» toocreate решения.</span><span class="sxs-lookup"><span data-stu-id="d0346-115">Log on tooazureiotsuite.com using your Azure account credentials, and click "**+**" toocreate a solution.</span></span>
2. <span data-ttu-id="d0346-116">Нажмите кнопку **выберите** на hello **подключенных фабрики** плитки.</span><span class="sxs-lookup"><span data-stu-id="d0346-116">Click **Select** on hello **Connected factory** tile.</span></span>
3. <span data-ttu-id="d0346-117">Укажите **имя** для предварительно настроенного решения подключенной фабрики.</span><span class="sxs-lookup"><span data-stu-id="d0346-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="d0346-118">Выберите hello **подписки** и **область** toouse tooprovision hello решение.</span><span class="sxs-lookup"><span data-stu-id="d0346-118">Select hello **Subscription** and **Region** you want toouse tooprovision hello solution.</span></span>
5. <span data-ttu-id="d0346-119">Нажмите кнопку **создать решение** toobegin hello процесса подготовки.</span><span class="sxs-lookup"><span data-stu-id="d0346-119">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="d0346-120">Этот процесс обычно занимает несколько минут toorun.</span><span class="sxs-lookup"><span data-stu-id="d0346-120">This process typically takes several minutes toorun.</span></span>

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="d0346-121">Во время ожидания подготовки процесса toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="d0346-121">While you wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="d0346-122">Щелкните плитку hello в решении с **Provisioning** состояния.</span><span class="sxs-lookup"><span data-stu-id="d0346-122">Click hello tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="d0346-123">Обратите внимание hello **подготовки состояний** мере развертывания служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="d0346-123">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="d0346-124">После завершения подготовки hello изменения состояния слишком**готовности**.</span><span class="sxs-lookup"><span data-stu-id="d0346-124">Once provisioning completes, hello status changes too**Ready**.</span></span>
4. <span data-ttu-id="d0346-125">Нажмите кнопку сведения hello toosee плитки hello решения в правой области окна hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-125">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="d0346-126">Если возникли проблемы при развертывании hello предварительно настроенных решений, просмотрите [разрешения на сайт azureiotsuite.com hello] [ lnk-permissions] и hello [подключен фабрики часто задаваемые вопросы о](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="d0346-126">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="d0346-127">Если сохранить проблемы hello, создать билет службы для hello [портала][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="d0346-127">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="d0346-128">Существуют следовало ожидать toosee сведения, которые отсутствуют в списке для вашего решения?</span><span class="sxs-lookup"><span data-stu-id="d0346-128">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="d0346-129">Сообщите нам о своих предложениях на сайте [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="d0346-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="d0346-130">Обзор сценария</span><span class="sxs-lookup"><span data-stu-id="d0346-130">Scenario overview</span></span>

<span data-ttu-id="d0346-131">При развертывании hello подключен фабрики предварительно настроенных решений, заполнена ресурсы, которые позволяют toostep через промышленным чаще.</span><span class="sxs-lookup"><span data-stu-id="d0346-131">When you deploy hello connected factory preconfigured solution, it is prepopulated with resources that enable you toostep through a common industrial scenario.</span></span> <span data-ttu-id="d0346-132">В этом сценарии несколько фабрик подключен toohello решений отчетов hello значения требуется toocompute общую эффективность работы оборудования (OEE) и ключевые показатели эффективности (KPI).</span><span class="sxs-lookup"><span data-stu-id="d0346-132">In this scenario, several factories connected toohello solution report hello data values required toocompute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="d0346-133">Hello следующих разделах показано, как для:</span><span class="sxs-lookup"><span data-stu-id="d0346-133">hello following sections show you how to:</span></span>

* <span data-ttu-id="d0346-134">Выполнять мониторинг фабрик, производственных линий, общей эффективности оборудования узла и значений ключевых показателей эффективности.</span><span class="sxs-lookup"><span data-stu-id="d0346-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="d0346-135">Анализировать данные телеметрии hello, созданные из этих устройств с помощью ряда времени Azure Insights</span><span class="sxs-lookup"><span data-stu-id="d0346-135">Analyze hello telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="d0346-136">Реагировать на проблемы toofix оповещения</span><span class="sxs-lookup"><span data-stu-id="d0346-136">Act on alerts toofix issues</span></span>

<span data-ttu-id="d0346-137">Ключевой особенностью этого сценария заключается в, можно выполнить все эти действия удаленно с панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="d0346-137">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="d0346-138">Не обязательно toohello физического доступа к устройствам.</span><span class="sxs-lookup"><span data-stu-id="d0346-138">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="d0346-139">Представление hello решений мониторинга</span><span class="sxs-lookup"><span data-stu-id="d0346-139">View hello solution dashboard</span></span>

<span data-ttu-id="d0346-140">панель мониторинга Hello решение позволяет toomanage hello развертывания решения.</span><span class="sxs-lookup"><span data-stu-id="d0346-140">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="d0346-141">Это иерархическое представление глобальной конфигурации фабрик.</span><span class="sxs-lookup"><span data-stu-id="d0346-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="d0346-142">Например, вы можете просматривать значения общей эффективности оборудования и ключевых показателей эффективности, публиковать новые узлы для передачи телеметрии и оповещений о действиях.</span><span class="sxs-lookup"><span data-stu-id="d0346-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="d0346-143">После подготовки hello завершения и указывает hello плитки для предварительно настроенного решения **готовности**, выберите **запуска** tooopen портал подключенных фабрики решение в новой вкладке.</span><span class="sxs-lookup"><span data-stu-id="d0346-143">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your connected factory solution portal in a new tab.</span></span>

    ![Запустите hello предварительно настроенных решений][img-launch-solution]

1. <span data-ttu-id="d0346-145">По умолчанию hello решение портала отображает hello *мониторинга*.</span><span class="sxs-lookup"><span data-stu-id="d0346-145">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="d0346-146">toonavigate tooother области портала hello, используйте меню hello hello левой стороны страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="d0346-146">toonavigate tooother areas of hello portal, use hello menu on hello left-hand side of hello page.</span></span>

    ![Панель мониторинга предварительно настроенного решения для подключенной фабрики][cf-img-menu]

<span data-ttu-id="d0346-148">панель мониторинга Hello отображает hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="d0346-148">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="d0346-149">Объект **список фабрики** панель, на которой показано состояние hello, расположение и текущей рабочей конфигурации в решении hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-149">A **Factory list** panel that shows hello status, location, and current production configuration in hello solution.</span></span> <span data-ttu-id="d0346-150">При первом запуске hello решения, существует несколько устройств, имитация.</span><span class="sxs-lookup"><span data-stu-id="d0346-150">When you first run hello solution, there are a number of simulated devices.</span></span> <span data-ttu-id="d0346-151">моделирования рабочей строки Hello состоит из трех реальных OPC UA серверов на рабочей строки, выполняющие задачи имитацию и совместно использовать данные.</span><span class="sxs-lookup"><span data-stu-id="d0346-151">hello production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="d0346-152">Дополнительные сведения о OPC UA см. в разделе hello [подключен фабрики часто задаваемые вопросы о](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="d0346-152">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="d0346-153">Объект **карты** , расположение hello отображает все устройства подключены toohello решения.</span><span class="sxs-lookup"><span data-stu-id="d0346-153">A **map** that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="d0346-154">решение Hello hello Bing Maps API tooplot сведения можно использовать на карте hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-154">hello solution can use hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="d0346-155">Если в вашей подписке включен Enterprise API для Карт Bing, этот компонент будет использоваться автоматически.</span><span class="sxs-lookup"><span data-stu-id="d0346-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="d0346-156">Hello см. в противном случае [часто задаваемые вопросы о] [ lnk-faq] toolearn как toomake hello динамической карты.</span><span class="sxs-lookup"><span data-stu-id="d0346-156">If not, see hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="d0346-157">На панели **Оповещения** отображаются оповещения, создаваемые, когда значения телеметрии, общей эффективности оборудования или ключевых показателей эффективности превышают указанное пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="d0346-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="d0346-158">**Общую эффективность оборудования** панель, на которой показано hello OEE значения для всего предприятия hello или hello фабрики или рабочего строки/станции вы просматриваете.</span><span class="sxs-lookup"><span data-stu-id="d0346-158">An **Overall Equipment Efficiency** panel that shows hello OEE values for hello whole enterprise, or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="d0346-159">Это значение вычисляется hello станции представление toohello корпоративного уровня.</span><span class="sxs-lookup"><span data-stu-id="d0346-159">This value is aggregated from hello station view toohello enterprise level.</span></span> <span data-ttu-id="d0346-160">Рисунок OEE Hello и его составляющие элементы можно далее проанализировать.</span><span class="sxs-lookup"><span data-stu-id="d0346-160">hello OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="d0346-161">**Ключевые показатели эффективности** панель, которая отображает hello число единиц, производимых и энергии, используемых hello всего предприятия или строку hello фабрики или рабочего/станции вы просматриваете.</span><span class="sxs-lookup"><span data-stu-id="d0346-161">**Key Performance Indicators** panel that displays hello number of units produced and energy used by hello whole enterprise or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="d0346-162">Эти значения суммируются из станции Просмотр toohello корпоративного уровня.</span><span class="sxs-lookup"><span data-stu-id="d0346-162">These values are aggregated from a station view toohello enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="d0346-163">Просмотр фабрик</span><span class="sxs-lookup"><span data-stu-id="d0346-163">View factories</span></span>

<span data-ttu-id="d0346-164">Hello *фабрик* панели показано hello географическое расположение всех фабрик hello в решение hello, состояние и текущей рабочей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d0346-164">hello *Factories* panel shows you hello geographical location of all hello factories in hello solution, their status, and current production configuration.</span></span> <span data-ttu-id="d0346-165">Из списка расположений hello можно перейти toohello другие уровни в иерархии решения hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-165">From hello locations list, you can navigate toohello other levels in hello solution hierarchy.</span></span> <span data-ttu-id="d0346-166">Hello строк в списке hello, гиперссылки, которые ссылаются подробные сведения о производственных линиях hello в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="d0346-166">hello rows in hello list are hyperlinks that link details of hello production lines at that location.</span></span> <span data-ttu-id="d0346-167">Затем это возможных toodrill в детали строки производственного hello "и" вниз toohello станции уровня представления.</span><span class="sxs-lookup"><span data-stu-id="d0346-167">It is then possible toodrill into hello production line details and down toohello station level view.</span></span> <span data-ttu-id="d0346-168">Можно также применить toohello список фильтров.</span><span class="sxs-lookup"><span data-stu-id="d0346-168">You can also apply a filter toohello list.</span></span>

![Фабрики в предварительно настроенном решении для подключенной фабрики][cf-img-factories] 

1. <span data-ttu-id="d0346-170">Hello **панель фабрики** показано hello список фабрика для этого решения.</span><span class="sxs-lookup"><span data-stu-id="d0346-170">hello **Factory panel** shows hello factory list for this solution.</span></span>

2. <span data-ttu-id="d0346-171">Hello фабрики изначально перечислены шесть фабрик, созданных hello процесса подготовки.</span><span class="sxs-lookup"><span data-stu-id="d0346-171">hello factory list initially shows six factories created by hello provisioning process.</span></span> <span data-ttu-id="d0346-172">Можно добавить решение toohello дополнительных имитацию и физических устройств.</span><span class="sxs-lookup"><span data-stu-id="d0346-172">You can add additional simulated and physical devices toohello solution.</span></span>

3. <span data-ttu-id="d0346-173">сведения о hello tooview фабрики, щелкните строку hello в списке фабрики hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-173">tooview hello details of a factory, click hello row in hello factory list.</span></span>

4. <span data-ttu-id="d0346-174">сведения о hello tooview строки производства, щелкните строку hello в списке hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-174">tooview hello details of a production line, click hello row in hello list.</span></span>

5. <span data-ttu-id="d0346-175">tooview hello публикации OPC UA узлы строке hello рабочей станции, щелкните строку hello в списке hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-175">tooview hello published OPC UA nodes of a station on hello production line, click hello row in hello list.</span></span>

6. <span data-ttu-id="d0346-176">tooview сведения о конкретном узле в станции hello, щелкните строку hello в списке hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-176">tooview details on a specific node in hello station, click hello row in hello list.</span></span> <span data-ttu-id="d0346-177">Это действие запускает hello контекста панель с визуализациями аналитики ряда времени.</span><span class="sxs-lookup"><span data-stu-id="d0346-177">This action launches hello context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="d0346-178">Щелкните эти графы toodo дальнейшего анализа в среде обозревателя hello аналитики ряда времени.</span><span class="sxs-lookup"><span data-stu-id="d0346-178">Click these graphs toodo further analysis in hello Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="d0346-179">Просмотр карты</span><span class="sxs-lookup"><span data-stu-id="d0346-179">View map</span></span>

<span data-ttu-id="d0346-180">Если ваша подписка имеет toohello доступа к API службы Bing Maps, hello *фабрик* карты отображаются hello географическое расположение и состояние всех фабрик hello в решение hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-180">If your subscription has access toohello Bing Maps API, hello *Factories* map shows you hello geographical location and status of all hello factories in hello solution.</span></span> <span data-ttu-id="d0346-181">toodrill сведения о расположении hello, щелкните расположение hello, отображаемых на карте hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-181">toodrill into hello location details, click hello locations displayed on hello map.</span></span>

![Карта предварительно настроенного решения для подключенной фабрики][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="d0346-183">Просмотр оповещений</span><span class="sxs-lookup"><span data-stu-id="d0346-183">View alerts</span></span>

<span data-ttu-id="d0346-184">Hello **предупреждения** панель показывает предупреждения, созданные из-за tooa отображается значение или значение, вычисленное OEE/ключевого показателя Эффективности превышает настроенное пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="d0346-184">hello **Alert** panel shows you alerts generated due tooa reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="d0346-185">Эта панель отображает предупреждения на каждом уровне иерархии hello, глобальное представление уровня представления станции toohello hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-185">This panel displays alerts at each level of hello hierarchy, from hello station level view toohello global view.</span></span> <span data-ttu-id="d0346-186">Hello оповещения содержат описание предупреждения hello, даты, времени, расположение и количество вхождений.</span><span class="sxs-lookup"><span data-stu-id="d0346-186">hello alerts contain a description of hello alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="d0346-187">Можно получить подробные сведения об toohello данные, вызвавшие предупреждение hello hello аналитики времени рядов данных с помощью.</span><span class="sxs-lookup"><span data-stu-id="d0346-187">You can gain insights in toohello data that caused hello alert using hello Time Series Insights data.</span></span> <span data-ttu-id="d0346-188">ценных сведений Hello времени серии визуализации данных в hello оповещения, где это возможно.</span><span class="sxs-lookup"><span data-stu-id="d0346-188">hello Time Series Insights data is visualized in hello alerts where applicable.</span></span> <span data-ttu-id="d0346-189">Если вы являетесь администратором, можно предпринять действия по умолчанию hello оповещениями, такие как:</span><span class="sxs-lookup"><span data-stu-id="d0346-189">If you are an Administrator, you can take default actions on hello alerts such as:</span></span>

* <span data-ttu-id="d0346-190">Закрыть hello предупреждений.</span><span class="sxs-lookup"><span data-stu-id="d0346-190">Close hello alert.</span></span>
* <span data-ttu-id="d0346-191">Подтверждаете hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="d0346-191">Acknowledge hello alert.</span></span>

<span data-ttu-id="d0346-192">При необходимости можно предпринять действия посложнее.</span><span class="sxs-lookup"><span data-stu-id="d0346-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="d0346-193">Например для hello давление OPC UA узел hello сборку можно выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="d0346-193">For example, for hello Pressure OPC UA Node of hello Assembly you could:</span></span>

* <span data-ttu-id="d0346-194">Открыть веб-страницу в новом окне браузера, чтобы отобразить справочные сведения.</span><span class="sxs-lookup"><span data-stu-id="d0346-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="d0346-195">Устранить причину предупреждения hello hello путем вызова метода OPC UA на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-195">Mitigate hello cause of hello alert by calling an OPC UA method on hello device.</span></span>
* <span data-ttu-id="d0346-196">Отключение hello доступность действия по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-196">Suppress hello availability of hello default actions.</span></span>

    ![Оповещения предварительно настроенного решения для подключенной фабрики][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="d0346-198">Эти оповещения создаются правила, заданные в файле конфигурации в решении предварительно настроенных hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-198">These alerts are generated by rules that are specified in a configuration file in hello preconfigured solution.</span></span> <span data-ttu-id="d0346-199">Эти правила могут создавать оповещения при hello OEE ключевого показателя Эффективности фигуры или узел UA OPC значения превышают их пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="d0346-199">These rules can generate alerts when hello OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="d0346-200">Hello **панель предупреждения** показано hello предупреждения, созданные в этом решении.</span><span class="sxs-lookup"><span data-stu-id="d0346-200">hello **Alerts panel** shows hello alerts generated in this solution.</span></span>

2. <span data-ttu-id="d0346-201">tooview hello сведения об предупреждении щелкните предупреждение hello панели оповещений hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-201">tooview hello details of an alert, click hello alert in hello alerts panel.</span></span>

3. <span data-ttu-id="d0346-202">toofurther проанализируйте hello данных предупреждений, щелкните граф hello в обозревателе hello предупреждения панель tooopen hello аналитики ряда времени среде.</span><span class="sxs-lookup"><span data-stu-id="d0346-202">toofurther analyze hello alert data, click hello graph in hello alert panel tooopen hello Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="d0346-203">tooaddress Здравствуйте предупреждения, предупреждения панели hello доступны несколько действий.</span><span class="sxs-lookup"><span data-stu-id="d0346-203">tooaddress hello alert, several actions are available in hello alert panel.</span></span> <span data-ttu-id="d0346-204">Выберите соответствующий параметр hello для вас и нажмите кнопку hello выполнение действия кнопки.</span><span class="sxs-lookup"><span data-stu-id="d0346-204">Choose hello appropriate option for you and click hello execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="d0346-205">Просмотр общей эффективности оборудования</span><span class="sxs-lookup"><span data-stu-id="d0346-205">View overall equipment efficiency</span></span>

<span data-ttu-id="d0346-206">Тарифы OEE hello эффективность hello производственного процесса с помощью ключа производственной рабочие параметры.</span><span class="sxs-lookup"><span data-stu-id="d0346-206">OEE rates hello efficiency of hello manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="d0346-207">OEE — это отраслевой, стандартные измерения вычисляться путем умножения скорость доступности hello, частоты производительности и качества скорость: OEE = доступности x качество производительности x.</span><span class="sxs-lookup"><span data-stu-id="d0346-207">OEE is an industry standard measure calculated by multiplying hello availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![Общая эффективность оборудования предварительно настроенного решения для подключенной фабрики][cf-img-oee]

1. <span data-ttu-id="d0346-209">tooview OEE для любого уровня в иерархии hello перейдите toohello определенных представлений, потребуется.</span><span class="sxs-lookup"><span data-stu-id="d0346-209">tooview OEE for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="d0346-210">панели hello вместе с каждого из элементов hello, составляющих hello OEE процент отображает Hello OEE для этого представления.</span><span class="sxs-lookup"><span data-stu-id="d0346-210">hello OEE for that view displays in hello panel along with each of hello elements that make up hello OEE percentage.</span></span>

2. <span data-ttu-id="d0346-211">toofurther проанализируйте hello OEE для любого уровня в иерархии данных hello, щелкните hello OEE, доступности, производительности или процент качества.</span><span class="sxs-lookup"><span data-stu-id="d0346-211">toofurther analyze hello OEE for any level in hello hierarchy data, click either hello OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="d0346-212">Контекст в панель аналитики ряда времени энергопотреблением визуализации, представлены данные из hello последний час, последние 24 часа и за последние 7 дней.</span><span class="sxs-lookup"><span data-stu-id="d0346-212">A context panel appears with Time Series Insights powered visualizations that shows data from hello last hour, last 24 hours, and last 7 days.</span></span>

    ![Визуализация Time Series Insights предварительно настроенного решения для подключенной фабрики][cf-img-tsi-visualization]

3. <span data-ttu-id="d0346-214">toofurther анализ данных о предупреждениях hello, щелкните граф hello оповещения панели hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-214">toofurther analyze hello alert data, click hello graph in hello alert panel.</span></span> <span data-ttu-id="d0346-215">Это действие открывает hello аналитики ряда времени обозреватель среды.</span><span class="sxs-lookup"><span data-stu-id="d0346-215">This action opens hello Time Series Insights explorer environment.</span></span>

    ![Обозреватель Time Series Insights предварительно настроенного решения для подключенной фабрики][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="d0346-217">Просмотр ключевых показателей эффективности</span><span class="sxs-lookup"><span data-stu-id="d0346-217">View Key Performance Indicators</span></span>

<span data-ttu-id="d0346-218">решение Hello предоставляет два ключевых показателей эффективности, *единиц в час* и *кВт/ч Израсходованная энергия*.</span><span class="sxs-lookup"><span data-stu-id="d0346-218">hello solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![Ключевой показатель эффективности предварительно настроенного решения для подключенной фабрики][cf-img-kpi]

1. <span data-ttu-id="d0346-220">tooview единиц в час или энергии, используемый для любого уровня в иерархии hello перейдите toohello определенных представлений, потребуется.</span><span class="sxs-lookup"><span data-stu-id="d0346-220">tooview units per hour or energy used for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="d0346-221">единицы Hello час и энергии использовать отображения в панели «hello».</span><span class="sxs-lookup"><span data-stu-id="d0346-221">hello units per hour and energy used display in hello panel.</span></span>

2. <span data-ttu-id="d0346-222">tooanalyze единиц в час или энергии, используемый для любого уровня в иерархии hello, кроме того, щелкните датчик hello в hello **ключевые показатели эффективности** панель.</span><span class="sxs-lookup"><span data-stu-id="d0346-222">tooanalyze units per hour or energy used for any level in hello hierarchy further, click hello gauge in hello **Key Performance Indicators** panel.</span></span> <span data-ttu-id="d0346-223">Контекст в панель с визуализациями аналитики ряда времени на платформе, позволяя tooview данные из hello последний час hello последние 24 часа и за последние 7 дней.</span><span class="sxs-lookup"><span data-stu-id="d0346-223">A context panel appears with Time Series Insights powered visualizations enabling you tooview data from hello last hour, hello last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="d0346-224">Разбор сценария</span><span class="sxs-lookup"><span data-stu-id="d0346-224">Scenario review</span></span>

<span data-ttu-id="d0346-225">В этом сценарии мониторинга фабрики OEE и ключевые показатели эффективности значения, в панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-225">In this scenario, you monitored your factories OEE and KPIs values, in hello dashboard.</span></span> <span data-ttu-id="d0346-226">Затем использовалась tooprovide аналитики ряда времени Дополнительные сведения о toohelp Исследуйте дополнительные данные телеметрии hello toohelp OEE и ключевые показатели эффективности с обнаружение аномалий.</span><span class="sxs-lookup"><span data-stu-id="d0346-226">You then used Time Series Insights tooprovide more information toohelp drill further into hello telemetry data for OEE and KPIs toohelp with detecting anomalies.</span></span> <span data-ttu-id="d0346-227">Также используется hello предупреждения панель tooview проблем с вашей фабриками и использовать hello действия доступны tooyou tooresolve hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="d0346-227">You also used hello alert panel tooview issues with your factories and you used hello actions available tooyou tooresolve hello alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="d0346-228">Другие возможности</span><span class="sxs-lookup"><span data-stu-id="d0346-228">Other features</span></span>

<span data-ttu-id="d0346-229">Привет, в следующих разделах описаны некоторые дополнительные функции hello подключен фабрики решения, не описанные в предыдущем сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-229">hello following sections describe some additional features of hello connected factory solution that are not described in hello previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="d0346-230">Применение фильтров</span><span class="sxs-lookup"><span data-stu-id="d0346-230">Apply filters</span></span>

1. <span data-ttu-id="d0346-231">Нажмите кнопку hello **шеврона** toodisplay список доступных фильтров в hello фабрики расположения панели или панели оповещений hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-231">Click hello **chevron** toodisplay a list of available filters in either hello factory locations panel or hello alerts panel.</span></span>

2. <span data-ttu-id="d0346-232">автоматически отобразится панель фильтров Hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-232">hello filters panel is displayed for you.</span></span> 

    ![Фильтры предварительно настроенного решения для подключенной фабрики][cf-img-alert-filter]

3. <span data-ttu-id="d0346-234">Выберите фильтр hello, которые нужны.</span><span class="sxs-lookup"><span data-stu-id="d0346-234">Choose hello filter that you require.</span></span> <span data-ttu-id="d0346-235">Это также возможно tootype произвольный текст в поля фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-235">It is also possible tootype free text into hello filter fields.</span></span>

4. <span data-ttu-id="d0346-236">Hello фильтр будет применен для вас.</span><span class="sxs-lookup"><span data-stu-id="d0346-236">hello filter is then applied for you.</span></span> <span data-ttu-id="d0346-237">состояние фильтра Hello также отображается в панель hello с помощью Воронка, отображает hello фабрик и оповещает таблиц.</span><span class="sxs-lookup"><span data-stu-id="d0346-237">hello filter state is also shown in hello dashboard via a funnel that displays in hello factories and alerts tables.</span></span>

    ![Фильтры предварительно настроенного решения для подключенной фабрики][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="d0346-239">Активный фильтр не влияет на значения OEE и ключевого показателя Эффективности отображается hello, он только фильтрует список содержимого hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-239">An active filter does not affect hello displayed OEE and KPI values, it only filters hello list contents.</span></span>

5. <span data-ttu-id="d0346-240">tooclear фильтр, щелкните воронкообразной hello и выберите фильтр в панели контекст фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-240">tooclear a filter, click hello funnel and click filter in hello filter context panel.</span></span> <span data-ttu-id="d0346-241">текст Hello **все** отображается в фабрик hello и оповещает таблиц.</span><span class="sxs-lookup"><span data-stu-id="d0346-241">hello text **All** is displayed in hello factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="d0346-242">Просмотр сервера на основе унифицированной архитектуры OPC</span><span class="sxs-lookup"><span data-stu-id="d0346-242">Browse an OPC UA server</span></span>

<span data-ttu-id="d0346-243">При развертывании решения hello предварительно настроен, Автоматическая подготовка имитацию OPC UA серверов, можно просмотреть через обозреватель решений hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-243">When you deploy hello preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via hello solution browser.</span></span> <span data-ttu-id="d0346-244">Эти серверы являются *имитациями серверов на основе унифицированной архитектуры OPC*.</span><span class="sxs-lookup"><span data-stu-id="d0346-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="d0346-245">Имитации серверы упростить для вас tooexperiment hello предварительно настроенное решение без hello необходимость toodeploy real, физических серверов.</span><span class="sxs-lookup"><span data-stu-id="d0346-245">Simulated servers make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical servers.</span></span> <span data-ttu-id="d0346-246">Если требуется tooconnect реальное решение toohello server OPC UA см hello [подключение решения OPC UA toohello подключены устройства фабрики заранее] [ lnk-connect-cf] учебника.</span><span class="sxs-lookup"><span data-stu-id="d0346-246">If you do want tooconnect a real OPC UA server toohello solution, see hello [Connect your OPC UA device toohello connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="d0346-247">Нажмите кнопку hello **значок фабрики** hello панели навигации панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="d0346-247">Click hello **factory icon** in hello dashboard navigation bar.</span></span>

    ![Обозреватель сервера предварительно настроенного решения для подключенной фабрики][cf-img-server-browser]

2. <span data-ttu-id="d0346-249">Выберите один из серверов hello из стандартного списка hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-249">Choose one of hello servers from hello preconfigured list.</span></span> <span data-ttu-id="d0346-250">Этот список содержит hello серверов, которые развертываются в hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="d0346-250">This list shows hello servers that are deployed for you in hello preconfigured solution.</span></span>

    ![Выбор сервера предварительно настроенного решения для подключенной фабрики][cf-img-server-choice]

3. <span data-ttu-id="d0346-252">Щелкните **Подключиться**. Отобразится диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="d0346-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="d0346-253">Для имитации hello, это безопасное tooclick **продолжение**</span><span class="sxs-lookup"><span data-stu-id="d0346-253">For hello simulation, it is safe tooclick **Proceed**</span></span>

4. <span data-ttu-id="d0346-254">tooexpand hello узлов в дереве сервера hello, щелкните его.</span><span class="sxs-lookup"><span data-stu-id="d0346-254">tooexpand any of hello nodes in hello server tree, click it.</span></span> <span data-ttu-id="d0346-255">Рядом с узлами, публикующими данные телеметрии, отображаются деления.</span><span class="sxs-lookup"><span data-stu-id="d0346-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Дерево серверов предварительно настроенного решения для подключенной фабрики][cf-img-server-tree]

5. <span data-ttu-id="d0346-257">Щелкните правой кнопкой мыши элемент tooread, записи, публикации или вызова этого узла.</span><span class="sxs-lookup"><span data-stu-id="d0346-257">Right-click an item tooread, write, publish, or call that node.</span></span> <span data-ttu-id="d0346-258">Доступные tooyou Hello действия зависят от того, разрешения и атрибуты hello hello узла.</span><span class="sxs-lookup"><span data-stu-id="d0346-258">hello actions available tooyou depend on your permissions and hello attributes of hello node.</span></span> <span data-ttu-id="d0346-259">Hello чтения toodisplays параметр контекста панель, отображающая hello значение hello конкретного узла.</span><span class="sxs-lookup"><span data-stu-id="d0346-259">hello read option toodisplays a context panel showing hello value of hello specific node.</span></span> <span data-ttu-id="d0346-260">Hello записи отображает параметр контекста панель, где можно ввести новое значение.</span><span class="sxs-lookup"><span data-stu-id="d0346-260">hello write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="d0346-261">параметр вызова Hello отображает узел, где можно ввести параметры hello для вызова hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-261">hello call option displays a node where you can enter hello parameters for hello call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="d0346-262">Публикация узла</span><span class="sxs-lookup"><span data-stu-id="d0346-262">Publish a node</span></span>

<span data-ttu-id="d0346-263">При просмотре *имитацию OPC UA сервера*, вы также можете toopublish новых узлов.</span><span class="sxs-lookup"><span data-stu-id="d0346-263">When you browse a *simulated OPC UA server*, you can also choose toopublish new nodes.</span></span> <span data-ttu-id="d0346-264">Можно анализировать hello телеметрии с этих узлов в решении hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-264">You can analyze hello telemetry from these nodes in hello solution.</span></span> <span data-ttu-id="d0346-265">Эти *имитируемые OPC UA серверов* сделать легко tooexperiment hello предварительно настроенное решение без развертывания реальных физических устройств.</span><span class="sxs-lookup"><span data-stu-id="d0346-265">These *simulated OPC UA servers* make it easy tooexperiment with hello preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="d0346-266">Обзор tooa узла в дерево обозревателя сервера OPC UA, что вы хотите toopublish hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-266">Browse tooa node in hello OPC UA server browser tree that you wish toopublish.</span></span>

2. <span data-ttu-id="d0346-267">Щелкните правой кнопкой мыши узел hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-267">Right-click hello node.</span></span>

3. <span data-ttu-id="d0346-268">Выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="d0346-268">Choose **Publish**.</span></span>

    ![Публикация узла подключенной фабрики][cf-img-publish-node]

4. <span data-ttu-id="d0346-270">Появится панель контекста сообщает, что hello публикации завершен успешно.</span><span class="sxs-lookup"><span data-stu-id="d0346-270">A context panel appears which tells you that hello publish has succeeded.</span></span> <span data-ttu-id="d0346-271">в представление уровня hello станции с флажком рядом с ним появится узел Hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-271">hello node appears in hello station level view with a check mark beside it.</span></span>

    ![Успешная публикация предварительно настроенного решения для подключенной фабрики][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="d0346-273">Команды и управление</span><span class="sxs-lookup"><span data-stu-id="d0346-273">Command and control</span></span>

<span data-ttu-id="d0346-274">команды и управлять устройствами отрасли непосредственно из облака hello позволяет Hello подключенных фабрики.</span><span class="sxs-lookup"><span data-stu-id="d0346-274">hello connected factory allows you command and control your industry devices directly from hello cloud.</span></span> <span data-ttu-id="d0346-275">Можно использовать этот компонент tooalerts toorespond, формируемые hello устройством.</span><span class="sxs-lookup"><span data-stu-id="d0346-275">You can use this feature toorespond tooalerts generated by hello device.</span></span> <span data-ttu-id="d0346-276">Например можно отправлять команды toohello устройства из облака hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-276">For example, you could send a command toohello device from hello cloud.</span></span> <span data-ttu-id="d0346-277">Hello можно найти команды, доступные в hello **StationCommands** узла в дерево обозревателя серверов OPC UA hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-277">You can find hello available commands in hello **StationCommands** node in hello OPC UA servers browser tree.</span></span> <span data-ttu-id="d0346-278">В этом случае откройте вентиль выпуска нагрузку на станции сборки hello в Мюнхен строки производства.</span><span class="sxs-lookup"><span data-stu-id="d0346-278">In this scenario, you open a pressure release valve on hello assembly station of a production line in Munich.</span></span> <span data-ttu-id="d0346-279">toouse hello команда возможности управления, необходимо находиться в hello **администратора** роль для hello предварительно настроить развертывание решения.</span><span class="sxs-lookup"><span data-stu-id="d0346-279">toouse hello command and control functionality, you must be in hello **Administrator** role for hello preconfigured solution deployment.</span></span>

1. <span data-ttu-id="d0346-280">Обзор toohello **StationCommands** узла в дерево обозревателя сервера OPC UA hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-280">Browse toohello **StationCommands** node in hello OPC UA server browser tree.</span></span>

2. <span data-ttu-id="d0346-281">Выберите команду hello, что вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="d0346-281">Choose hello command that you wish use.</span></span>

3. <span data-ttu-id="d0346-282">Щелкните правой кнопкой мыши узел hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-282">Right-click hello node.</span></span>

4. <span data-ttu-id="d0346-283">Выберите **Вызов**.</span><span class="sxs-lookup"><span data-stu-id="d0346-283">Choose **Call**.</span></span>

    ![Вызов команды предварительно настроенного решения для подключенной фабрики][cf-img-call-command]

5. <span data-ttu-id="d0346-285">О том, какой метод вы собираетесь toocall и любые сведения о параметрах применяется в контексте панель.</span><span class="sxs-lookup"><span data-stu-id="d0346-285">A context panel appears informing you which method you are about toocall and any parameter details is applicable.</span></span>

6. <span data-ttu-id="d0346-286">Выберите **Вызов**.</span><span class="sxs-lookup"><span data-stu-id="d0346-286">Choose **Call**.</span></span>

    ![Контекстная панель вызова в предварительно настроенном решении для подключенной фабрики][cf-img-call-context]

7. <span data-ttu-id="d0346-288">панель Hello контекста — обновленных tooinform, hello вызова метода выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="d0346-288">hello context panel is updated tooinform you that hello method call succeeded.</span></span> <span data-ttu-id="d0346-289">Можно проверить, выполнено успешно, считывая значение hello hello давление узла, которое обновляется в результате вызова hello вызовов hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-289">You can verify hello call succeeded by reading hello value of hello pressure node that updated as a result of hello call.</span></span>

    ![Успешный вызов предварительно настроенного решения для подключенной фабрики][cf-img-call-success]


## <a name="behind-hello-scenes"></a><span data-ttu-id="d0346-291">Фоновом hello</span><span class="sxs-lookup"><span data-stu-id="d0346-291">Behind hello scenes</span></span>

<span data-ttu-id="d0346-292">При развертывании предварительно настроенных решений hello процесс развертывания создает несколько ресурсов в hello Azure подписку, которую вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="d0346-292">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="d0346-293">Эти ресурсы можно просмотреть в hello Azure [портала][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="d0346-293">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="d0346-294">процесс развертывания Hello создает **группы ресурсов** с именем, основываясь на имени hello, выберите для предварительно настроенного решения:</span><span class="sxs-lookup"><span data-stu-id="d0346-294">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Предварительно настроенных решений в hello портал Azure][img-cf-portal]

<span data-ttu-id="d0346-296">Параметры hello каждый ресурс можно просмотреть, выбрав его в список ресурсов в группе ресурсов hello hello.</span><span class="sxs-lookup"><span data-stu-id="d0346-296">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="d0346-297">Также можно просмотреть исходный код hello hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="d0346-297">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="d0346-298">Hello подключенных фабрики предварительно настроенное решение исходный код находится в hello [-iot подключен фабрики azure] [ lnk-cfgithub] репозитории GitHub:</span><span class="sxs-lookup"><span data-stu-id="d0346-298">hello connected factory preconfigured solution source code is in hello [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="d0346-299">После завершения, можно удалить hello предварительно настроенное решение из подписки Azure на hello [azureiotsuite.com] [ lnk-azureiotsuite] сайта.</span><span class="sxs-lookup"><span data-stu-id="d0346-299">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="d0346-300">Этот сайт обеспечивает delete tooeasily Здравствуйте, все ресурсы, которые были подготовлены при создании hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="d0346-300">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="d0346-301">toohello предварительно настроенных решений, связанных с tooensure, удалите весь код, удалите его на hello [azureiotsuite.com] [ lnk-azureiotsuite] сайта.</span><span class="sxs-lookup"><span data-stu-id="d0346-301">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="d0346-302">Не удаляйте группу ресурсов hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="d0346-302">Do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0346-303">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d0346-303">Next Steps</span></span>

<span data-ttu-id="d0346-304">Теперь, когда вы развернули предварительно настроенное рабочее решение, можно перейти, Приступая к работе с IoT Suite, считывая hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="d0346-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="d0346-305">[Пошаговое руководство по работе с настроенным решением для удаленного мониторинга][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="d0346-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="d0346-306">[Подключение решения подключенных фабрики заранее настроенные toohello устройства][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="d0346-306">[Connect your device toohello Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="d0346-307">[Разрешения на сайт azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="d0346-307">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md