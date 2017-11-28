---
title: "aaaGet к работе с предварительно настроенных решений | Документы Microsoft"
description: "Выполните этот учебник toolearn как toodeploy набор IoT Azure предварительно настроенных решений."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a><span data-ttu-id="89205-103">Приступая к работе с hello предварительно настроенных решений</span><span class="sxs-lookup"><span data-stu-id="89205-103">Get started with hello preconfigured solutions</span></span>

<span data-ttu-id="89205-104">Azure IoT Suite [предварительно настроенных решений] [ lnk-preconfigured-solutions] объединить несколько конца в конец решений toodeliver Azure IoT служб, реализующие общих деловых сценариях IoT.</span><span class="sxs-lookup"><span data-stu-id="89205-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="89205-105">Hello *удаленный мониторинг* предварительно настроенных решений подключается мониторы tooand устройств.</span><span class="sxs-lookup"><span data-stu-id="89205-105">hello *remote monitoring* preconfigured solution connects tooand monitors your devices.</span></span> <span data-ttu-id="89205-106">Можно использовать hello tooanalyze решения hello поток данных с устройств и результатов бизнеса tooimprove, делая процессы отвечать автоматически toothat поток данных.</span><span class="sxs-lookup"><span data-stu-id="89205-106">You can use hello solution tooanalyze hello stream of data from your devices and tooimprove business outcomes by making processes respond automatically toothat stream of data.</span></span>

<span data-ttu-id="89205-107">Этот учебник показывает, как удаленный мониторинг tooprovision hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="89205-107">This tutorial shows you how tooprovision hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="89205-108">Он также поможет выполнить основные функции hello hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="89205-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="89205-109">Многие из этих средств можно получить из решения hello *мониторинга* , которая выполняет развертывание в рамках hello предварительно настроенных решений:</span><span class="sxs-lookup"><span data-stu-id="89205-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Панель мониторинга предварительно настроенного решения для удаленного мониторинга][img-dashboard]

<span data-ttu-id="89205-111">toocomplete этого учебника требуется Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="89205-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="89205-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="89205-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="89205-113">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="89205-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="89205-114">Обзор сценария</span><span class="sxs-lookup"><span data-stu-id="89205-114">Scenario overview</span></span>

<span data-ttu-id="89205-115">При развертывании удаленного мониторинга предварительно настроенных решений hello заполнена ресурсов, позволяющих toostep через обычный сценарий удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="89205-115">When you deploy hello remote monitoring preconfigured solution, it is prepopulated with resources that enable you toostep through a common remote monitoring scenario.</span></span> <span data-ttu-id="89205-116">В этом сценарии несколько решений toohello подключенных устройств сообщаете температуры непредвиденные значения.</span><span class="sxs-lookup"><span data-stu-id="89205-116">In this scenario, several devices connected toohello solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="89205-117">Hello следующих разделах показано, как для:</span><span class="sxs-lookup"><span data-stu-id="89205-117">hello following sections show you how to:</span></span>

* <span data-ttu-id="89205-118">Определение устройств hello температуры непредвиденные значения.</span><span class="sxs-lookup"><span data-stu-id="89205-118">Identify hello devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="89205-119">Настройка этих устройств toosend более подробные данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="89205-119">Configure these devices toosend more detailed telemetry.</span></span>
* <span data-ttu-id="89205-120">Hello проблему можно устраните путем обновления встроенного по hello на этих устройствах.</span><span class="sxs-lookup"><span data-stu-id="89205-120">Fix hello problem by updating hello firmware on these devices.</span></span>
* <span data-ttu-id="89205-121">Проверка действия разрешения проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="89205-121">Verify that your action has resolved hello issue.</span></span>

<span data-ttu-id="89205-122">Ключевой особенностью этого сценария заключается в, можно выполнить все эти действия удаленно с панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="89205-122">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="89205-123">Не обязательно toohello физического доступа к устройствам.</span><span class="sxs-lookup"><span data-stu-id="89205-123">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="89205-124">Представление hello решений мониторинга</span><span class="sxs-lookup"><span data-stu-id="89205-124">View hello solution dashboard</span></span>

<span data-ttu-id="89205-125">панель мониторинга Hello решение позволяет toomanage hello развертывания решения.</span><span class="sxs-lookup"><span data-stu-id="89205-125">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="89205-126">Например, можно просматривать данные телеметрии, добавлять устройства и настраивать правила.</span><span class="sxs-lookup"><span data-stu-id="89205-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="89205-127">После подготовки hello завершения и указывает hello плитки для предварительно настроенного решения **готовности**, выберите **запуска** tooopen на новой вкладке портал удаленного мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="89205-127">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Запустите hello предварительно настроенных решений][img-launch-solution]

1. <span data-ttu-id="89205-129">По умолчанию hello решение портала отображает hello *мониторинга*.</span><span class="sxs-lookup"><span data-stu-id="89205-129">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="89205-130">Можно перемещаться tooother области портала hello решения, с помощью меню hello hello левой стороны страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="89205-130">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Панель мониторинга предварительно настроенного решения для удаленного мониторинга][img-menu]

<span data-ttu-id="89205-132">панель мониторинга Hello отображает hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="89205-132">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="89205-133">Карта, отображающая hello расположение каждого устройства подключены toohello решения.</span><span class="sxs-lookup"><span data-stu-id="89205-133">A map that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="89205-134">При первом запуске hello решение, есть 25 имитации устройства.</span><span class="sxs-lookup"><span data-stu-id="89205-134">When you first run hello solution, there are 25 simulated devices.</span></span> <span data-ttu-id="89205-135">Hello устройств, имитация реализованы в виде веб-заданий Azure и hello решение использует hello Bing Maps API tooplot сведения на карте hello.</span><span class="sxs-lookup"><span data-stu-id="89205-135">hello simulated devices are implemented as Azure WebJobs, and hello solution uses hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="89205-136">В разделе hello [часто задаваемые вопросы о] [ lnk-faq] toolearn как toomake hello динамической карты.</span><span class="sxs-lookup"><span data-stu-id="89205-136">See hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="89205-137">На панели **Журнал телеметрии** отображаются графики влажности и температуры с выбранного устройства в близком к реальному времени, а также сводные данные, например максимальное, минимальное и среднее значения влажности.</span><span class="sxs-lookup"><span data-stu-id="89205-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="89205-138">На панели **Журнал оповещений** отображаются последние события, когда значение телеметрии превышает пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="89205-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="89205-139">Можно определить собственные сигналы в примерах toohello сложения, созданные hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="89205-139">You can define your own alarms in addition toohello examples created by hello preconfigured solution.</span></span>
* <span data-ttu-id="89205-140">В области **Задания** отображаются сведения о запланированных заданиях.</span><span class="sxs-lookup"><span data-stu-id="89205-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="89205-141">Вы можете запланировать собственные задания на странице **заданий управления**.</span><span class="sxs-lookup"><span data-stu-id="89205-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="89205-142">Просмотр оповещений</span><span class="sxs-lookup"><span data-stu-id="89205-142">View alarms</span></span>

<span data-ttu-id="89205-143">«Журнал» звуковых сигналов Hello показано выше, чем ожидаемое телеметрии значения Подотчетные пять устройства.</span><span class="sxs-lookup"><span data-stu-id="89205-143">hello alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Журнал TODO сигнала на панели мониторинга решения hello][img-alarms]

> [!NOTE]
> <span data-ttu-id="89205-145">Эти предупреждения создаются правилом, включенный в hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="89205-145">These alarms are generated by a rule that is included in hello preconfigured solution.</span></span> <span data-ttu-id="89205-146">Это правило создает оповещение, когда значение температуры hello, отправляемый устройством превышает 60.</span><span class="sxs-lookup"><span data-stu-id="89205-146">This rule generates an alert when hello temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="89205-147">Можно определить собственные правила и действия, выбрав [правила](#add-a-rule) и [действия](#add-an-action) в левом меню hello.</span><span class="sxs-lookup"><span data-stu-id="89205-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in hello left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="89205-148">Просмотр устройств</span><span class="sxs-lookup"><span data-stu-id="89205-148">View devices</span></span>

<span data-ttu-id="89205-149">Hello *устройств* список содержит все устройства, зарегистрированные hello в решении hello.</span><span class="sxs-lookup"><span data-stu-id="89205-149">hello *devices* list shows all hello registered devices in hello solution.</span></span> <span data-ttu-id="89205-150">Из списка устройств hello можно просматривать и изменять метаданные устройства добавьте или удалите устройства и вызова методов на устройствах.</span><span class="sxs-lookup"><span data-stu-id="89205-150">From hello device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="89205-151">Можно фильтровать и сортировать список устройств в списке устройств hello hello.</span><span class="sxs-lookup"><span data-stu-id="89205-151">You can filter and sort hello list of devices in hello device list.</span></span> <span data-ttu-id="89205-152">Можно также настроить hello столбцов, показанных в списке устройств hello.</span><span class="sxs-lookup"><span data-stu-id="89205-152">You can also customize hello columns shown in hello device list.</span></span>

1. <span data-ttu-id="89205-153">Выберите **устройств** список устройств hello tooshow для этого решения.</span><span class="sxs-lookup"><span data-stu-id="89205-153">Choose **Devices** tooshow hello device list for this solution.</span></span>

   ![Просмотр списка устройств hello hello решение портала][img-devicelist]

1. <span data-ttu-id="89205-155">Список устройств Hello первоначально показывает 25 имитации устройства, созданные по подготовке hello.</span><span class="sxs-lookup"><span data-stu-id="89205-155">hello device list initially shows 25 simulated devices created by hello provisioning process.</span></span> <span data-ttu-id="89205-156">Можно добавить решение toohello дополнительных имитацию и физических устройств.</span><span class="sxs-lookup"><span data-stu-id="89205-156">You can add additional simulated and physical devices toohello solution.</span></span>

1. <span data-ttu-id="89205-157">сведения о hello tooview устройства, выберите устройство в список устройств hello.</span><span class="sxs-lookup"><span data-stu-id="89205-157">tooview hello details of a device, choose a device in hello device list.</span></span>

   ![Просмотр сведений об устройстве hello hello решение портала][img-devicedetails]

<span data-ttu-id="89205-159">Hello **сведений об устройстве** панель содержит шесть разделы:</span><span class="sxs-lookup"><span data-stu-id="89205-159">hello **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="89205-160">Коллекция ссылок, включения вы toocustomize hello значок устройства, отключите устройство hello, добавить правило, вызвать метод или отправить команду.</span><span class="sxs-lookup"><span data-stu-id="89205-160">A collection of links that enable you toocustomize hello device icon, disable hello device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="89205-161">Сведения о сравнении команд (сообщения из устройства в облако) и методов (прямые методы) см. в [руководстве о связи между облаком и устройством][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="89205-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="89205-162">Hello **устройства двойных - теги** раздел позволяет tooedit значения тега для hello устройства.</span><span class="sxs-lookup"><span data-stu-id="89205-162">hello **Device Twin - Tags** section enables you tooedit tag values for hello device.</span></span> <span data-ttu-id="89205-163">Можно отобразить значения тега в список устройств hello и использовать список устройств hello toofilter значения тега.</span><span class="sxs-lookup"><span data-stu-id="89205-163">You can display tag values in hello device list and use tag values toofilter hello device list.</span></span>
* <span data-ttu-id="89205-164">Hello **устройства двойных - требуемого свойства** раздел позволяет tooset свойство значения toobe отправлено toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="89205-164">hello **Device Twin - Desired Properties** section enables you tooset property values toobe sent toohello device.</span></span>
* <span data-ttu-id="89205-165">Hello **устройства двойных - сообщил свойства** разделе показаны значения свойств, отправляемых с устройства hello.</span><span class="sxs-lookup"><span data-stu-id="89205-165">hello **Device Twin - Reported Properties** section shows property values sent from hello device.</span></span>
* <span data-ttu-id="89205-166">Hello **свойства устройства** разделе отображаются сведения из реестра удостоверение hello, например hello устройства идентификатор и проверки подлинности ключи.</span><span class="sxs-lookup"><span data-stu-id="89205-166">hello **Device Properties** section shows information from hello identity registry such as hello device id and authentication keys.</span></span>
* <span data-ttu-id="89205-167">Hello **последних заданий** разделе приводятся сведения о все задания, которые недавно предназначены этого устройства.</span><span class="sxs-lookup"><span data-stu-id="89205-167">hello **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-hello-device-list"></a><span data-ttu-id="89205-168">Фильтровать список устройств hello</span><span class="sxs-lookup"><span data-stu-id="89205-168">Filter hello device list</span></span>

<span data-ttu-id="89205-169">Можно использовать только те устройства, которые отправляют значения температуры Непредвиденная toodisplay фильтра.</span><span class="sxs-lookup"><span data-stu-id="89205-169">You can use a filter toodisplay only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="89205-170">удаленный мониторинг предварительно настроенных решений Hello включает hello **неработоспособности устройства** фильтрации tooshow устройствами с помощью температуры среднее значение, большее, чем 60.</span><span class="sxs-lookup"><span data-stu-id="89205-170">hello remote monitoring preconfigured solution includes hello **Unhealthy devices** filter tooshow devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="89205-171">Также можно [создать собственные фильтры](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="89205-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="89205-172">Выберите **открыть сохраненный фильтр** toodisplay список доступных фильтров.</span><span class="sxs-lookup"><span data-stu-id="89205-172">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="89205-173">Выберите **неработоспособности устройства** tooapply hello фильтра:</span><span class="sxs-lookup"><span data-stu-id="89205-173">Then choose **Unhealthy devices** tooapply hello filter:</span></span>

    ![Отображение списка фильтров hello][img-unhealthy-filter]

1. <span data-ttu-id="89205-175">Hello устройство теперь перечислены только устройства с температуры среднее значение больше 60.</span><span class="sxs-lookup"><span data-stu-id="89205-175">hello device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Просмотр списка отфильтрованных устройств hello отображает неработоспособен][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="89205-177">Обновление требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="89205-177">Update desired properties</span></span>

<span data-ttu-id="89205-178">Вы определили набор устройств, которые необходимо исправить.</span><span class="sxs-lookup"><span data-stu-id="89205-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="89205-179">Однако принято hello периодичность данных составляет 15 секунд недостаточно для очистки диагностики проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="89205-179">However, you decide that hello data frequency of 15 seconds is not sufficient for a clear diagnosis of hello issue.</span></span> <span data-ttu-id="89205-180">Изменение hello телеметрии частоты toofive секунд tooprovide вам toobetter точек дополнительные данные диагностики проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="89205-180">Changing hello telemetry frequency toofive seconds tooprovide you with more data points toobetter diagnose hello issue.</span></span> <span data-ttu-id="89205-181">Это изменение конфигурации tooyour удаленных устройств можно передать через портал hello решения.</span><span class="sxs-lookup"><span data-stu-id="89205-181">You can push this configuration change tooyour remote devices from hello solution portal.</span></span> <span data-ttu-id="89205-182">Необходимо будет внести изменение hello один раз, оценивать влияние hello и выполнить действия с hello результаты.</span><span class="sxs-lookup"><span data-stu-id="89205-182">You can make hello change once, evaluate hello impact, and then act on hello results.</span></span>

<span data-ttu-id="89205-183">Выполните эти шаги toorun задание, которое изменяет hello **TelemetryInterval** требуемого свойства для затронутых hello устройств.</span><span class="sxs-lookup"><span data-stu-id="89205-183">Follow these steps toorun a job that changes hello **TelemetryInterval** desired property for hello affected devices.</span></span> <span data-ttu-id="89205-184">Когда hello устройства будут получать новый hello **TelemetryInterval** значения свойства, они изменяют свои данные телеметрии toosend конфигурации каждые пять секунд, а не через каждые 15 секунд:</span><span class="sxs-lookup"><span data-stu-id="89205-184">When hello devices receive hello new **TelemetryInterval** property value, they change their configuration toosend telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="89205-185">Хотя список hello неработоспособное устройств отображаются в списке устройств hello, **планировщик заданий**, затем **изменить двойных устройства**.</span><span class="sxs-lookup"><span data-stu-id="89205-185">While you are showing hello list of unhealthy devices in hello device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="89205-186">Вызов задания hello **интервала изменений телеметрии**.</span><span class="sxs-lookup"><span data-stu-id="89205-186">Call hello job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="89205-187">Измените значение hello hello **нужное свойство** имя **требуемой. Config.TelemetryInterval** toofive секунд.</span><span class="sxs-lookup"><span data-stu-id="89205-187">Change hello value of hello **Desired Property** name **desired.Config.TelemetryInterval** toofive seconds.</span></span>

1. <span data-ttu-id="89205-188">Выберите **Расписание**.</span><span class="sxs-lookup"><span data-stu-id="89205-188">Choose **Schedule**.</span></span>

    ![Изменить свойства toofive hello TelemetryInterval секунд][img-change-interval]

1. <span data-ttu-id="89205-190">Отследить ход выполнения hello hello задания на hello **управления заданиями** портале hello.</span><span class="sxs-lookup"><span data-stu-id="89205-190">You can monitor hello progress of hello job on hello **Management Jobs** page in hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="89205-191">Toochange значению свойства для отдельных устройств, используйте hello **нужными свойствами** раздела hello **сведений об устройстве** панель вместо запуска задания.</span><span class="sxs-lookup"><span data-stu-id="89205-191">If you want toochange a desired property value for an individual device, use hello **Desired Properties** section in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="89205-192">Это задание задает значение hello hello **TelemetryInterval** требуемого свойства в двойных hello устройства для всех hello выбранных фильтром hello устройств.</span><span class="sxs-lookup"><span data-stu-id="89205-192">This job sets hello value of hello **TelemetryInterval** desired property in hello device twin for all hello devices selected by hello filter.</span></span> <span data-ttu-id="89205-193">Hello устройств это значение получалось из устройства двойных hello и обновите их поведения.</span><span class="sxs-lookup"><span data-stu-id="89205-193">hello devices retrieve this value from hello device twin and update their behavior.</span></span> <span data-ttu-id="89205-194">Когда устройство получает и обрабатывает нужные свойства из двойных устройства, его свойству hello соответствующего значение по отчету.</span><span class="sxs-lookup"><span data-stu-id="89205-194">When a device retrieves and processes a desired property from a device twin, it sets hello corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="89205-195">Вызов методов</span><span class="sxs-lookup"><span data-stu-id="89205-195">Invoke methods</span></span>

<span data-ttu-id="89205-196">Во время выполнения задания hello замечаете в списке hello неработоспособное устройств, все эти устройства микропрограмма старого (меньше, чем версии 1.6) версии.</span><span class="sxs-lookup"><span data-stu-id="89205-196">While hello job runs, you notice in hello list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Представление hello сообщила о версии встроенного по для устройств неработоспособное hello][img-old-firmware]

<span data-ttu-id="89205-198">Эта версия встроенного по может быть hello первопричину hello Непредвиденная значения температуры, поскольку известно, что другие работоспособных устройств были недавно обновленного tooversion 2.0.</span><span class="sxs-lookup"><span data-stu-id="89205-198">This firmware version may be hello root cause of hello unexpected temperature values because you know that other healthy devices were recently updated tooversion 2.0.</span></span> <span data-ttu-id="89205-199">Можно использовать встроенные hello **старые встроенного по устройства** фильтрации tooidentify все устройства со старыми версиями встроенного по.</span><span class="sxs-lookup"><span data-stu-id="89205-199">You can use hello built-in **Old firmware devices** filter tooidentify any devices with old firmware versions.</span></span> <span data-ttu-id="89205-200">Из портала hello можно удаленно обновить все устройства hello, по-прежнему под управлением старых версий встроенного по:</span><span class="sxs-lookup"><span data-stu-id="89205-200">From hello portal, you can then remotely update all hello devices still running old firmware versions:</span></span>

1. <span data-ttu-id="89205-201">Выберите **открыть сохраненный фильтр** toodisplay список доступных фильтров.</span><span class="sxs-lookup"><span data-stu-id="89205-201">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="89205-202">Выберите **старые встроенного по устройства** tooapply hello фильтра:</span><span class="sxs-lookup"><span data-stu-id="89205-202">Then choose **Old firmware devices** tooapply hello filter:</span></span>

    ![Отображение списка фильтров hello][img-old-filter]

1. <span data-ttu-id="89205-204">Список устройств Hello теперь отображаются только устройства с помощью старых версий встроенного по.</span><span class="sxs-lookup"><span data-stu-id="89205-204">hello device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="89205-205">Этот список включает пять устройств hello, определенных hello **неработоспособности устройства** фильтр и трех дополнительных устройств:</span><span class="sxs-lookup"><span data-stu-id="89205-205">This list includes hello five devices identified by hello **Unhealthy devices** filter and three additional devices:</span></span>

    ![Просмотр списка отфильтрованных устройств hello отображаются старые устройства][img-filtered-old-list]

1. <span data-ttu-id="89205-207">Выберите **Планировщик заданий**, а затем — **Вызвать метод**.</span><span class="sxs-lookup"><span data-stu-id="89205-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="89205-208">Задать **имя задания** слишком**tooversion обновление встроенного по 2.0**.</span><span class="sxs-lookup"><span data-stu-id="89205-208">Set **Job Name** too**Firmware update tooversion 2.0**.</span></span>

1. <span data-ttu-id="89205-209">Выберите **InitiateFirmwareUpdate** как hello **метод**.</span><span class="sxs-lookup"><span data-stu-id="89205-209">Choose **InitiateFirmwareUpdate** as hello **Method**.</span></span>

1. <span data-ttu-id="89205-210">Набор hello **FwPackageUri** параметр слишком**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="89205-210">Set hello **FwPackageUri** parameter too**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="89205-211">Выберите **Расписание**.</span><span class="sxs-lookup"><span data-stu-id="89205-211">Choose **Schedule**.</span></span> <span data-ttu-id="89205-212">по умолчанию Hello сейчас для задания toorun hello.</span><span class="sxs-lookup"><span data-stu-id="89205-212">hello default is for hello job toorun now.</span></span>

    ![Создание задания tooupdate hello встроенное по устройств выбран hello][img-method-update]

> [!NOTE]
> <span data-ttu-id="89205-214">Tooinvoke метод отдельные устройства, выберите **методы** в hello **сведений об устройстве** панель вместо запуска задания.</span><span class="sxs-lookup"><span data-stu-id="89205-214">If you want tooinvoke a method on an individual device, choose **Methods** in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="89205-215">Это задание вызывает hello **InitiateFirmwareUpdate** прямой метод на всех устройствах hello выбранных фильтром hello.</span><span class="sxs-lookup"><span data-stu-id="89205-215">This job invokes hello **InitiateFirmwareUpdate** direct method on all hello devices selected by hello filter.</span></span> <span data-ttu-id="89205-216">Устройства ответить немедленно tooIoT концентратора и асинхронной инициации процесса обновления встроенного по hello.</span><span class="sxs-lookup"><span data-stu-id="89205-216">Devices respond immediately tooIoT Hub and then initiate hello firmware update process asynchronously.</span></span> <span data-ttu-id="89205-217">устройства Hello предоставляют сведения о состоянии процесса обновления встроенного по hello через значения свойств отчета, как показано на следующих снимках экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="89205-217">hello devices provide status information about hello firmware update process through reported property values, as shown in hello following screenshots.</span></span> <span data-ttu-id="89205-218">Выберите hello **обновление** значок tooupdate hello сведения в списки устройств и задание hello:</span><span class="sxs-lookup"><span data-stu-id="89205-218">Choose hello **Refresh** icon tooupdate hello information in hello device and job lists:</span></span>

<span data-ttu-id="89205-219">![Список заданий, показывающий выполнение списка обновления встроенного по hello][img-update-1]
![список устройств, показывающий состояние обновления встроенного по][img-update-2]
![задания списка Отображение hello встроенного по обновления списка завершения][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="89205-219">![Job list showing hello firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing hello firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="89205-220">В рабочей среде можно запланировать toorun задания во время заданного периода.</span><span class="sxs-lookup"><span data-stu-id="89205-220">In a production environment, you can schedule jobs toorun during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="89205-221">Разбор сценария</span><span class="sxs-lookup"><span data-stu-id="89205-221">Scenario review</span></span>

<span data-ttu-id="89205-222">В этом сценарии определить потенциальные проблемы с некоторыми из удаленного устройства с помощью журнала hello звуковых сигналов на панель мониторинга hello и фильтр.</span><span class="sxs-lookup"><span data-stu-id="89205-222">In this scenario, you identified a potential issue with some of your remote devices using hello alarm history on hello dashboard and a filter.</span></span> <span data-ttu-id="89205-223">Вы затем фильтра используется hello и tooremotely задания настройки устройств tooprovide hello дополнительные toohelp сведения диагностики проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="89205-223">You then used hello filter and a job tooremotely configure hello devices tooprovide more information toohelp diagnose hello issue.</span></span> <span data-ttu-id="89205-224">Наконец вы использовали фильтр и задания обслуживания tooschedule на устройствах затронуты hello.</span><span class="sxs-lookup"><span data-stu-id="89205-224">Finally, you used a filter and a job tooschedule maintenance on hello affected devices.</span></span> <span data-ttu-id="89205-225">Если возвращается toohello панели мониторинга можно проверить, что больше не существует любой сигналы поступают от устройств в решении.</span><span class="sxs-lookup"><span data-stu-id="89205-225">If you return toohello dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="89205-226">Можно использовать фильтр актуален tooverify, hello встроенного по на всех устройствах hello в решении и больше нет неработоспособности устройства:</span><span class="sxs-lookup"><span data-stu-id="89205-226">You can use a filter tooverify that hello firmware is up-to-date on all hello devices in your solution and that there are no more unhealthy devices:</span></span>

![Фильтр, показывающий, что все устройства имеют актуальную версию встроенного ПО][img-updated]

![Фильтр, показывающий, что все устройства работоспособны][img-healthy]

## <a name="other-features"></a><span data-ttu-id="89205-229">Другие возможности</span><span class="sxs-lookup"><span data-stu-id="89205-229">Other features</span></span>

<span data-ttu-id="89205-230">Hello следующих разделах описаны некоторые дополнительные функции hello удаленное наблюдение предварительно настроенного решения, описанные в предыдущем сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="89205-230">hello following sections describe some additional features of hello remote monitoring preconfigured solution that are not described as part of hello previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="89205-231">Настройка столбцов</span><span class="sxs-lookup"><span data-stu-id="89205-231">Customize columns</span></span>

<span data-ttu-id="89205-232">Можно настроить hello сведения отображаются в списке устройств hello, выбрав **редактор столбец**.</span><span class="sxs-lookup"><span data-stu-id="89205-232">You can customize hello information shown in hello device list by choosing **Column editor**.</span></span> <span data-ttu-id="89205-233">Кроме того, можно добавлять и удалять столбцы, отображающие полученные значения тегов и свойств,</span><span class="sxs-lookup"><span data-stu-id="89205-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="89205-234">а также изменять порядок столбцов и переименовывать их.</span><span class="sxs-lookup"><span data-stu-id="89205-234">You can also reorder and rename columns:</span></span>

   ![Список столбцов редактор ion hello устройства][img-columneditor]

### <a name="customize-hello-device-icon"></a><span data-ttu-id="89205-236">Настройка значок устройства hello</span><span class="sxs-lookup"><span data-stu-id="89205-236">Customize hello device icon</span></span>

<span data-ttu-id="89205-237">Вы можете настроить hello устройства значка, отображаемого в списке устройств hello из hello **сведений об устройстве** панели следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89205-237">You can customize hello device icon displayed in hello device list from hello **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="89205-238">Выберите значок tooopen hello карандаша hello **редактирование изображения** панель для устройства:</span><span class="sxs-lookup"><span data-stu-id="89205-238">Choose hello pencil icon tooopen hello **Edit image** panel for a device:</span></span>

   ![Открытие редактора изображений устройств][img-startimageedit]

1. <span data-ttu-id="89205-240">Отправить новый образ или использовать один из существующих образов hello и выберите **Сохранить**:</span><span class="sxs-lookup"><span data-stu-id="89205-240">Either upload a new image or use one of hello existing images and then choose **Save**:</span></span>

   ![Редактор изменения изображений устройства][img-imageedit]

1. <span data-ttu-id="89205-242">Hello образа, выбранного теперь отображаются в hello **значок** столбца для hello устройства.</span><span class="sxs-lookup"><span data-stu-id="89205-242">hello image you selected now displays in hello **Icon** column for hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="89205-243">Hello изображение хранится в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="89205-243">hello image is stored in blob storage.</span></span> <span data-ttu-id="89205-244">Тег в двойных устройства hello содержит изображение toohello ссылку в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="89205-244">A tag in hello device twin contains a link toohello image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="89205-245">Добавление устройства</span><span class="sxs-lookup"><span data-stu-id="89205-245">Add a device</span></span>

<span data-ttu-id="89205-246">При развертывании решения hello предварительно настроен, Автоматическая подготовка 25 образец устройств, которые отображаются в списке устройств hello.</span><span class="sxs-lookup"><span data-stu-id="89205-246">When you deploy hello preconfigured solution, you automatically provision 25 sample devices that you can see in hello device list.</span></span> <span data-ttu-id="89205-247">Это *виртуальные устройства*, работающие в веб-задании Azure.</span><span class="sxs-lookup"><span data-stu-id="89205-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="89205-248">Устройств, имитация упростить для вас tooexperiment hello предварительно настроенное решение без hello необходимость toodeploy реальных физических устройств.</span><span class="sxs-lookup"><span data-stu-id="89205-248">Simulated devices make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical devices.</span></span> <span data-ttu-id="89205-249">Если вы хотите tooconnect решения toohello реального устройства, см. раздел hello [подключения вашего устройства toohello удаленное наблюдение предварительно настроенных решений] [ lnk-connect-rm] учебника.</span><span class="sxs-lookup"><span data-stu-id="89205-249">If you do want tooconnect a real device toohello solution, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="89205-250">Hello следующие шаги показывают, как tooadd имитацию toohello устройствами:</span><span class="sxs-lookup"><span data-stu-id="89205-250">hello following steps show you how tooadd a simulated device toohello solution:</span></span>

1. <span data-ttu-id="89205-251">Перейдите назад toohello список устройств.</span><span class="sxs-lookup"><span data-stu-id="89205-251">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="89205-252">Выберите tooadd устройством, **+ добавить устройство** в левом нижнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="89205-252">tooadd a device, choose **+ Add A Device** in hello bottom left corner.</span></span>

   ![Добавление решения toohello предварительно настроенных устройств][img-adddevice]

1. <span data-ttu-id="89205-254">Выберите **добавить новое** на hello **имитируемые устройства** плитки.</span><span class="sxs-lookup"><span data-stu-id="89205-254">Choose **Add New** on hello **Simulated Device** tile.</span></span>

   ![Настройка сведений о новом устройстве на панели мониторинга][img-addnew]

   <span data-ttu-id="89205-256">В добавление toocreating имитацию новое устройство, можно также добавить физическое устройство при выборе toocreate **пользовательских устройств**.</span><span class="sxs-lookup"><span data-stu-id="89205-256">In addition toocreating a new simulated device, you can also add a physical device if you choose toocreate a **Custom Device**.</span></span> <span data-ttu-id="89205-257">toolearn Дополнительные сведения о подключении решения toohello физических устройств, в разделе [подключиться к toohello устройств IoT Suite удаленное наблюдение предварительно настроенных решений][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="89205-257">toolearn more about connecting physical devices toohello solution, see [Connect your device toohello IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="89205-258">Выберите пункт **Let me define my own Device ID** (Задать идентификатор устройства самостоятельно) и укажите имя уникального идентификатора устройства: **mydevice_01**.</span><span class="sxs-lookup"><span data-stu-id="89205-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="89205-259">Выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="89205-259">Choose **Create**.</span></span>

   ![Сохранение нового устройства][img-definedevice]

1. <span data-ttu-id="89205-261">На шаге 3 **добавить имитированное устройство**, выберите **сделать** список устройств toohello tooreturn.</span><span class="sxs-lookup"><span data-stu-id="89205-261">In step 3 of **Add a simulated device**, choose **Done** tooreturn toohello device list.</span></span>

1. <span data-ttu-id="89205-262">Можно просматривать устройства **под управлением** в список устройств hello.</span><span class="sxs-lookup"><span data-stu-id="89205-262">You can view your device **Running** in hello device list.</span></span>

    ![Просмотр нового устройства в списке устройств][img-runningnew]

1. <span data-ttu-id="89205-264">Можно также просмотреть hello смоделированные данные телеметрии с нового устройства на панели мониторинга hello:</span><span class="sxs-lookup"><span data-stu-id="89205-264">You can also view hello simulated telemetry from your new device on hello dashboard:</span></span>

    ![Просмотр данных телеметрии с нового устройства][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="89205-266">Отключение и удаление устройства</span><span class="sxs-lookup"><span data-stu-id="89205-266">Disable and delete a device</span></span>

<span data-ttu-id="89205-267">Можно отключить устройство, а после отключения его можно удалить.</span><span class="sxs-lookup"><span data-stu-id="89205-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Отключение и удаление устройства][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="89205-269">Добавление правила</span><span class="sxs-lookup"><span data-stu-id="89205-269">Add a rule</span></span>

<span data-ttu-id="89205-270">Нет правил для hello новое устройство только что добавлен.</span><span class="sxs-lookup"><span data-stu-id="89205-270">There are no rules for hello new device you just added.</span></span> <span data-ttu-id="89205-271">В этом разделе добавьте правило, которое запускает оповещение, когда температуры hello сообщили hello нового устройства превышает 47 градусов.</span><span class="sxs-lookup"><span data-stu-id="89205-271">In this section, you add a rule that triggers an alarm when hello temperature reported by hello new device exceeds 47 degrees.</span></span> <span data-ttu-id="89205-272">Прежде чем начать, обратите внимание, журнал телеметрии hello hello новое устройство, на панели мониторинга hello показывают температура устройства hello никогда не превышает 45 градусов.</span><span class="sxs-lookup"><span data-stu-id="89205-272">Before you start, notice that hello telemetry history for hello new device on hello dashboard shows hello device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="89205-273">Перейдите назад toohello список устройств.</span><span class="sxs-lookup"><span data-stu-id="89205-273">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="89205-274">tooadd правило для hello устройства, выберите новое устройство в hello **список устройств**, а затем выберите **добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="89205-274">tooadd a rule for hello device, select your new device in hello **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="89205-275">Создать правило, которое использует **температуры** как поле данных hello и использует **AlarmTemp** как hello выходных данных, если температуры hello превышает 47 градусов:</span><span class="sxs-lookup"><span data-stu-id="89205-275">Create a rule that uses **Temperature** as hello data field and uses **AlarmTemp** as hello output when hello temperature exceeds 47 degrees:</span></span>

    ![Добавление правила устройства][img-adddevicerule]

1. <span data-ttu-id="89205-277">Выберите изменения, toosave **сохранение и Просмотр правил**.</span><span class="sxs-lookup"><span data-stu-id="89205-277">toosave your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="89205-278">Выберите **команды** в области сведений hello устройства для hello новое устройство.</span><span class="sxs-lookup"><span data-stu-id="89205-278">Choose **Commands** in hello device details pane for hello new device.</span></span>

    ![Добавление правила устройства][img-adddevicerule2]

1. <span data-ttu-id="89205-280">Выберите **ChangeSetPointTemp** из списка команд hello и набор **SetPointTemp** too45.</span><span class="sxs-lookup"><span data-stu-id="89205-280">Select **ChangeSetPointTemp** from hello command list and set **SetPointTemp** too45.</span></span> <span data-ttu-id="89205-281">Выберите **Отправить команду**.</span><span class="sxs-lookup"><span data-stu-id="89205-281">Then choose **Send Command**:</span></span>

    ![Добавление правила устройства][img-adddevicerule3]

1. <span data-ttu-id="89205-283">Перейдите назад toohello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="89205-283">Navigate back toohello dashboard.</span></span> <span data-ttu-id="89205-284">Через некоторое время, вы увидите новую запись в hello **журнал сигнала** панели при температуры hello сообщили новое устройство превышает пороговое значение степени 47 hello:</span><span class="sxs-lookup"><span data-stu-id="89205-284">After a short time, you will see a new entry in hello **Alarm History** pane when hello temperature reported by your new device exceeds hello 47-degree threshold:</span></span>

    ![Добавление правила устройства][img-adddevicerule4]

1. <span data-ttu-id="89205-286">Можно просмотреть и изменить все правила на hello **правила** hello панели мониторинга:</span><span class="sxs-lookup"><span data-stu-id="89205-286">You can review and edit all your rules on hello **Rules** page of hello dashboard:</span></span>

    ![Список правил устройства][img-rules]

1. <span data-ttu-id="89205-288">Можно просмотреть и изменить все hello действия, которые могут быть предприняты в правиле tooa ответа на hello **действия** hello панели мониторинга:</span><span class="sxs-lookup"><span data-stu-id="89205-288">You can review and edit all hello actions that can be taken in response tooa rule on hello **Actions** page of hello dashboard:</span></span>

    ![Список действий с устройством][img-actions]

> [!NOTE]
> <span data-ttu-id="89205-290">Это toodefine возможные действия, которые можно отправить сообщение электронной почты или SMS в ответ tooa правило или интегрировать бизнес-системе с помощью [приложения логики][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="89205-290">It is possible toodefine actions that can send an email message or SMS in response tooa rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="89205-291">Дополнительные сведения см. в разделе hello [tooyour подключения приложения логики Azure IoT Suite удаленный мониторинг предварительно настроенное решение][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="89205-291">For more information, see hello [Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="89205-292">Управление фильтрами</span><span class="sxs-lookup"><span data-stu-id="89205-292">Manage filters</span></span>

<span data-ttu-id="89205-293">В списке устройств hello создания, сохранения и перезагрузить toodisplay фильтры список концентратора tooyour подключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="89205-293">In hello device list, you can create, save, and reload filters toodisplay a customized list of devices connected tooyour hub.</span></span> <span data-ttu-id="89205-294">toocreate фильтра:</span><span class="sxs-lookup"><span data-stu-id="89205-294">toocreate a filter:</span></span>

1. <span data-ttu-id="89205-295">Выберите значок фильтра hello редактирования над списком hello устройств:</span><span class="sxs-lookup"><span data-stu-id="89205-295">Choose hello edit filter icon above hello list of devices:</span></span>

    ![Привет открыть редактор фильтров][img-editfiltericon]

1. <span data-ttu-id="89205-297">В hello **редактор фильтров**, добавьте hello поля, операторы и список значений toofilter hello устройств.</span><span class="sxs-lookup"><span data-stu-id="89205-297">In hello **Filter editor**, add hello fields, operators, and values toofilter hello device list.</span></span> <span data-ttu-id="89205-298">Можно добавить несколько toorefine предложения фильтра.</span><span class="sxs-lookup"><span data-stu-id="89205-298">You can add multiple clauses toorefine your filter.</span></span> <span data-ttu-id="89205-299">Выберите **фильтра** tooapply hello фильтра:</span><span class="sxs-lookup"><span data-stu-id="89205-299">Choose **Filter** tooapply hello filter:</span></span>

    ![Создание фильтра][img-filtereditor]

1. <span data-ttu-id="89205-301">В этом примере hello список фильтруется по производителю и номер модели:</span><span class="sxs-lookup"><span data-stu-id="89205-301">In this example, hello list is filtered by manufacturer and model number:</span></span>

    ![Фильтрованный список][img-filterelist]

1. <span data-ttu-id="89205-303">toosave фильтра с пользовательским именем выберите hello **сохранение** значок:</span><span class="sxs-lookup"><span data-stu-id="89205-303">toosave your filter with a custom name, choose hello **Save as** icon:</span></span>

    ![Сохранение фильтра][img-savefilter]

1. <span data-ttu-id="89205-305">tooreapply фильтр, сохраненный ранее, выберите hello **открыть сохраненный фильтр** значок:</span><span class="sxs-lookup"><span data-stu-id="89205-305">tooreapply a filter you saved previously, choose hello **Open saved filter** icon:</span></span>

    ![Открытие фильтра][img-openfilter]

<span data-ttu-id="89205-307">Вы можете создавать фильтры на основе идентификатора устройства, его состояния, требуемых или переданных свойств и тегов.</span><span class="sxs-lookup"><span data-stu-id="89205-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="89205-308">Добавление устройства tooa настраиваемые теги в hello **теги** раздел hello **сведений об устройстве** панели или запустить теги tooupdate заданий на нескольких устройствах.</span><span class="sxs-lookup"><span data-stu-id="89205-308">You add your own custom tags tooa device in hello **Tags** section of hello **Device Details** panel, or run a job tooupdate tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="89205-309">В hello **редактор фильтров**, можно использовать hello **расширенное представление** текст запроса hello tooedit напрямую.</span><span class="sxs-lookup"><span data-stu-id="89205-309">In hello **Filter editor**, you can use hello **Advanced view** tooedit hello query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="89205-310">Команды</span><span class="sxs-lookup"><span data-stu-id="89205-310">Commands</span></span>

<span data-ttu-id="89205-311">Из hello **сведений об устройстве** панель, можно отправлять команды toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="89205-311">From hello **Device Details** panel, you can send commands toohello device.</span></span> <span data-ttu-id="89205-312">При первом запуске устройство отправляет сведения о hello команд, что он поддерживает toohello решения.</span><span class="sxs-lookup"><span data-stu-id="89205-312">When a device first starts, it sends information about hello commands it supports toohello solution.</span></span> <span data-ttu-id="89205-313">Обсуждение hello различия между командами и методов см. в разделе [параметры облака на устройство Azure IoT Hub][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="89205-313">For a discussion of hello differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="89205-314">Выберите **команды** в hello **сведений об устройстве** панель для выбранного устройства hello:</span><span class="sxs-lookup"><span data-stu-id="89205-314">Choose **Commands** in hello **Device Details** panel for hello selected device:</span></span>

   ![Команды устройств на панели мониторинга][img-devicecommands]

1. <span data-ttu-id="89205-316">Выберите **PingDevice** из списка команд hello.</span><span class="sxs-lookup"><span data-stu-id="89205-316">Select **PingDevice** from hello command list.</span></span>

1. <span data-ttu-id="89205-317">Щелкните **Отправить команду**.</span><span class="sxs-lookup"><span data-stu-id="89205-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="89205-318">Вы увидите состояние hello hello команды в журнале команды hello.</span><span class="sxs-lookup"><span data-stu-id="89205-318">You can see hello status of hello command in hello command history.</span></span>

   ![Состояние команды на панели мониторинга][img-pingcommand]

<span data-ttu-id="89205-320">решение Hello отслеживает состояние hello каждой команды, которую он отправляет.</span><span class="sxs-lookup"><span data-stu-id="89205-320">hello solution tracks hello status of each command it sends.</span></span> <span data-ttu-id="89205-321">Изначально hello результатом является **ожидающие**.</span><span class="sxs-lookup"><span data-stu-id="89205-321">Initially hello result is **Pending**.</span></span> <span data-ttu-id="89205-322">Если устройство hello сообщает, что она выполнена команда hello, hello результирующий набор слишком**успешно**.</span><span class="sxs-lookup"><span data-stu-id="89205-322">When hello device reports that it has executed hello command, hello result is set too**Success**.</span></span>

## <a name="behind-hello-scenes"></a><span data-ttu-id="89205-323">Фоновом hello</span><span class="sxs-lookup"><span data-stu-id="89205-323">Behind hello scenes</span></span>

<span data-ttu-id="89205-324">При развертывании предварительно настроенных решений hello процесс развертывания создает несколько ресурсов в hello Azure подписку, которую вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="89205-324">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="89205-325">Эти ресурсы можно просмотреть в hello Azure [портала][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="89205-325">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="89205-326">процесс развертывания Hello создает **группы ресурсов** с именем, основываясь на имени hello, выберите для предварительно настроенного решения:</span><span class="sxs-lookup"><span data-stu-id="89205-326">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Предварительно настроенных решений в hello портал Azure][img-portal]

<span data-ttu-id="89205-328">Параметры hello каждый ресурс можно просмотреть, выбрав его в список ресурсов в группе ресурсов hello hello.</span><span class="sxs-lookup"><span data-stu-id="89205-328">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="89205-329">Также можно просмотреть исходный код hello hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="89205-329">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="89205-330">Hello удаленное наблюдение предварительно настроенных решений исходный код находится в hello [azure iot удаленного мониторинга] [ lnk-rmgithub] репозитории GitHub:</span><span class="sxs-lookup"><span data-stu-id="89205-330">hello remote monitoring preconfigured solution source code is in hello [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="89205-331">Hello **DeviceAdministration** папка содержит hello исходный код для мониторинга "hello".</span><span class="sxs-lookup"><span data-stu-id="89205-331">hello **DeviceAdministration** folder contains hello source code for hello dashboard.</span></span>
* <span data-ttu-id="89205-332">Hello **симулятор** папка содержит hello исходного кода для имитации устройства hello.</span><span class="sxs-lookup"><span data-stu-id="89205-332">hello **Simulator** folder contains hello source code for hello simulated device.</span></span>
* <span data-ttu-id="89205-333">Hello **EventProcessor** папка содержит hello исходного кода для серверной части процесса hello, который обрабатывает входящие данные телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="89205-333">hello **EventProcessor** folder contains hello source code for hello back-end process that handles hello incoming telemetry.</span></span>

<span data-ttu-id="89205-334">После завершения, можно удалить hello предварительно настроенное решение из подписки Azure на hello [azureiotsuite.com] [ lnk-azureiotsuite] сайта.</span><span class="sxs-lookup"><span data-stu-id="89205-334">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="89205-335">Этот сайт обеспечивает delete tooeasily Здравствуйте, все ресурсы, которые были подготовлены при создании hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="89205-335">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="89205-336">toohello предварительно настроенных решений, связанных с tooensure, удалите весь код, удалите его на hello [azureiotsuite.com] [ lnk-azureiotsuite] сайта, а также не удаляйте группу ресурсов hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="89205-336">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site and do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89205-337">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89205-337">Next Steps</span></span>

<span data-ttu-id="89205-338">Теперь, когда вы развернули предварительно настроенное рабочее решение, можно перейти, Приступая к работе с IoT Suite, считывая hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="89205-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="89205-339">[Пошаговое руководство по работе с настроенным решением для удаленного мониторинга][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="89205-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="89205-340">[Подключиться с вашего устройства toohello удаленное наблюдение предварительно настроенных решений][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="89205-340">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="89205-341">[Разрешения на сайт azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="89205-341">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md