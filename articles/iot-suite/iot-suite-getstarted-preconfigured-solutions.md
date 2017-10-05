---
title: "Приступая к работе с предварительно настроенными решениями | Документация Майкрософт"
description: "Следуйте инструкциям этого учебника, чтобы научиться развертывать предварительно настроенные решения набора IoT Microsoft Azure"
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
ms.openlocfilehash: 466825ab78a5ac9773d8beff69cca90ff9db6c01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-preconfigured-solutions"></a><span data-ttu-id="e790e-103">Приступая к работе с предварительно настроенными решениями</span><span class="sxs-lookup"><span data-stu-id="e790e-103">Get started with the preconfigured solutions</span></span>

<span data-ttu-id="e790e-104">Набор [предварительно настроенных решений][lnk-preconfigured-solutions] Интернета вещей Azure включает несколько служб Интернета вещей Azure, используемых при создании комплексных решений для реализации распространенных бизнес-сценариев Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="e790e-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="e790e-105">Предварительно настроенное решение для *удаленного мониторинга* подключается к устройствам и отслеживает их работу.</span><span class="sxs-lookup"><span data-stu-id="e790e-105">The *remote monitoring* preconfigured solution connects to and monitors your devices.</span></span> <span data-ttu-id="e790e-106">Это решение можно использовать, чтобы анализировать поток данных, поступающих с устройств, и улучшать результаты работы компании, организовав автоматическое реагирование процессов на этот поток данных.</span><span class="sxs-lookup"><span data-stu-id="e790e-106">You can use the solution to analyze the stream of data from your devices and to improve business outcomes by making processes respond automatically to that stream of data.</span></span>

<span data-ttu-id="e790e-107">В этом руководстве показано, как подготовить предварительно настроенное решение для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="e790e-107">This tutorial shows you how to provision the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="e790e-108">Кроме того, здесь описываются основные функции этого решения.</span><span class="sxs-lookup"><span data-stu-id="e790e-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="e790e-109">Многие функции доступны на *панели мониторинга* решения, которая развертывается вместе с предварительно настроенным решением.</span><span class="sxs-lookup"><span data-stu-id="e790e-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Панель мониторинга предварительно настроенного решения для удаленного мониторинга][img-dashboard]

<span data-ttu-id="e790e-111">Для работы с этим руководством требуется активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="e790e-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e790e-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e790e-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e790e-113">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="e790e-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="e790e-114">Обзор сценария</span><span class="sxs-lookup"><span data-stu-id="e790e-114">Scenario overview</span></span>

<span data-ttu-id="e790e-115">Развертывание предварительно настроенного решения удаленного мониторинга уже содержит ресурсы, которые позволяют выполнять распространенный сценарий удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="e790e-115">When you deploy the remote monitoring preconfigured solution, it is prepopulated with resources that enable you to step through a common remote monitoring scenario.</span></span> <span data-ttu-id="e790e-116">В этом сценарии несколько устройств, подключенных к решению, передают непредвиденные значения температуры.</span><span class="sxs-lookup"><span data-stu-id="e790e-116">In this scenario, several devices connected to the solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="e790e-117">В следующих разделах описано, как:</span><span class="sxs-lookup"><span data-stu-id="e790e-117">The following sections show you how to:</span></span>

* <span data-ttu-id="e790e-118">определить устройства, которые отправляют непредвиденные значения температуры;</span><span class="sxs-lookup"><span data-stu-id="e790e-118">Identify the devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="e790e-119">настроить эти устройства для отправки подробных данных телеметрии;</span><span class="sxs-lookup"><span data-stu-id="e790e-119">Configure these devices to send more detailed telemetry.</span></span>
* <span data-ttu-id="e790e-120">устранять проблемы путем обновления встроенного ПО на этих устройствах;</span><span class="sxs-lookup"><span data-stu-id="e790e-120">Fix the problem by updating the firmware on these devices.</span></span>
* <span data-ttu-id="e790e-121">проверять устранение проблемы.</span><span class="sxs-lookup"><span data-stu-id="e790e-121">Verify that your action has resolved the issue.</span></span>

<span data-ttu-id="e790e-122">Ключевой особенностью этого сценария является возможность удаленно выполнять все эти действия с помощью панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="e790e-122">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="e790e-123">Физический доступ к устройствам не обязателен.</span><span class="sxs-lookup"><span data-stu-id="e790e-123">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="e790e-124">Просмотр панели мониторинга решения</span><span class="sxs-lookup"><span data-stu-id="e790e-124">View the solution dashboard</span></span>

<span data-ttu-id="e790e-125">Панель мониторинга решения позволяет управлять развернутым решением.</span><span class="sxs-lookup"><span data-stu-id="e790e-125">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="e790e-126">Например, можно просматривать данные телеметрии, добавлять устройства и настраивать правила.</span><span class="sxs-lookup"><span data-stu-id="e790e-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="e790e-127">Когда подготовка завершится и на плитке предварительно настроенного решения появится надпись **Готово**, нажмите кнопку **Запустить**. Панель мониторинга решения откроется в новой вкладке.</span><span class="sxs-lookup"><span data-stu-id="e790e-127">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Запуск предварительно настроенного решения][img-launch-solution]

1. <span data-ttu-id="e790e-129">По умолчанию на портале решения отображается *панель мониторинга*.</span><span class="sxs-lookup"><span data-stu-id="e790e-129">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="e790e-130">Вы можете перейти к другим областям портала решения с помощью меню в левой части страницы.</span><span class="sxs-lookup"><span data-stu-id="e790e-130">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Панель мониторинга предварительно настроенного решения для удаленного мониторинга][img-menu]

<span data-ttu-id="e790e-132">На панели мониторинга отображаются следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="e790e-132">The dashboard displays the following information:</span></span>

* <span data-ttu-id="e790e-133">Карта, на которой показано расположение каждого устройства, подключенного к решению.</span><span class="sxs-lookup"><span data-stu-id="e790e-133">A map that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="e790e-134">При первом запуске решения отобразятся 25 виртуальных устройств, реализованных в виде веб-заданий Azure.</span><span class="sxs-lookup"><span data-stu-id="e790e-134">When you first run the solution, there are 25 simulated devices.</span></span> <span data-ttu-id="e790e-135">Для отображения сведений на карте в решении используется интерфейс API для Карт Bing.</span><span class="sxs-lookup"><span data-stu-id="e790e-135">The simulated devices are implemented as Azure WebJobs, and the solution uses the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="e790e-136">В разделе [Часто задаваемые вопросы][lnk-faq] содержатся сведения о том, как сделать карту динамической.</span><span class="sxs-lookup"><span data-stu-id="e790e-136">See the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="e790e-137">На панели **Журнал телеметрии** отображаются графики влажности и температуры с выбранного устройства в близком к реальному времени, а также сводные данные, например максимальное, минимальное и среднее значения влажности.</span><span class="sxs-lookup"><span data-stu-id="e790e-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="e790e-138">На панели **Журнал оповещений** отображаются последние события, когда значение телеметрии превышает пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="e790e-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="e790e-139">В дополнение к оповещениям, созданным в предварительно настроенном решении, можно задать собственные оповещения.</span><span class="sxs-lookup"><span data-stu-id="e790e-139">You can define your own alarms in addition to the examples created by the preconfigured solution.</span></span>
* <span data-ttu-id="e790e-140">В области **Задания** отображаются сведения о запланированных заданиях.</span><span class="sxs-lookup"><span data-stu-id="e790e-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="e790e-141">Вы можете запланировать собственные задания на странице **заданий управления**.</span><span class="sxs-lookup"><span data-stu-id="e790e-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="e790e-142">Просмотр оповещений</span><span class="sxs-lookup"><span data-stu-id="e790e-142">View alarms</span></span>

<span data-ttu-id="e790e-143">На панели журнала оповещений показано, что пять устройств передают значения телеметрии, которые превышают ожидаемые.</span><span class="sxs-lookup"><span data-stu-id="e790e-143">The alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![TODO Журнал оповещений на панели мониторинга решения][img-alarms]

> [!NOTE]
> <span data-ttu-id="e790e-145">Эти оповещения создаются правилом, которое содержится в предварительно настроенном решении.</span><span class="sxs-lookup"><span data-stu-id="e790e-145">These alarms are generated by a rule that is included in the preconfigured solution.</span></span> <span data-ttu-id="e790e-146">Это правило создает оповещение, когда значение температуры, передаваемое устройством, превышает 60.</span><span class="sxs-lookup"><span data-stu-id="e790e-146">This rule generates an alert when the temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="e790e-147">Вы можете определить собственные правила и действия, выбрав элементы [Правила](#add-a-rule) и [Действия](#add-an-action) в меню слева.</span><span class="sxs-lookup"><span data-stu-id="e790e-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in the left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="e790e-148">Просмотр устройств</span><span class="sxs-lookup"><span data-stu-id="e790e-148">View devices</span></span>

<span data-ttu-id="e790e-149">В *списке устройств* показаны все зарегистрированные устройства в решении.</span><span class="sxs-lookup"><span data-stu-id="e790e-149">The *devices* list shows all the registered devices in the solution.</span></span> <span data-ttu-id="e790e-150">Там вы можете просматривать и изменять метаданные устройств, добавлять или удалять их, а также вызывать методы на устройствах.</span><span class="sxs-lookup"><span data-stu-id="e790e-150">From the device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="e790e-151">Этот список можно фильтровать и сортировать.</span><span class="sxs-lookup"><span data-stu-id="e790e-151">You can filter and sort the list of devices in the device list.</span></span> <span data-ttu-id="e790e-152">Можно также настроить столбцы, которые отображаются в списке устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-152">You can also customize the columns shown in the device list.</span></span>

1. <span data-ttu-id="e790e-153">Выберите **Устройства** для отображения списка устройств этого решения.</span><span class="sxs-lookup"><span data-stu-id="e790e-153">Choose **Devices** to show the device list for this solution.</span></span>

   ![Просмотр списка устройств на портале решения][img-devicelist]

1. <span data-ttu-id="e790e-155">Изначально список устройств отображает 25 виртуальных устройств, созданных в ходе подготовки.</span><span class="sxs-lookup"><span data-stu-id="e790e-155">The device list initially shows 25 simulated devices created by the provisioning process.</span></span> <span data-ttu-id="e790e-156">Вы можете добавить в решение дополнительные виртуальные и физические устройства.</span><span class="sxs-lookup"><span data-stu-id="e790e-156">You can add additional simulated and physical devices to the solution.</span></span>

1. <span data-ttu-id="e790e-157">Чтобы просмотреть сведения об устройстве, щелкните его в списке устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-157">To view the details of a device, choose a device in the device list.</span></span>

   ![Просмотр дополнительных сведений об устройствах на портале решения][img-devicedetails]

<span data-ttu-id="e790e-159">Область **Сведения об устройстве** содержит шесть разделов.</span><span class="sxs-lookup"><span data-stu-id="e790e-159">The **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="e790e-160">Коллекция ссылок, позволяющих настроить значок устройства, отключить устройство, добавить правило, вызвать метод или отправить команду.</span><span class="sxs-lookup"><span data-stu-id="e790e-160">A collection of links that enable you to customize the device icon, disable the device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="e790e-161">Сведения о сравнении команд (сообщения из устройства в облако) и методов (прямые методы) см. в [руководстве о связи между облаком и устройством][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="e790e-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="e790e-162">Раздел **Device Twin - Tags** (Двойник устройства — Теги) позволяет изменять значения тегов для устройства.</span><span class="sxs-lookup"><span data-stu-id="e790e-162">The **Device Twin - Tags** section enables you to edit tag values for the device.</span></span> <span data-ttu-id="e790e-163">Вы можете отобразить значения тегов в списке устройств и использовать их для фильтрации этого списка.</span><span class="sxs-lookup"><span data-stu-id="e790e-163">You can display tag values in the device list and use tag values to filter the device list.</span></span>
* <span data-ttu-id="e790e-164">Раздел **Device Twin - Desired Properties** (Двойник устройства — Требуемые свойства) позволяет задавать значения свойств, отправляемые на устройство.</span><span class="sxs-lookup"><span data-stu-id="e790e-164">The **Device Twin - Desired Properties** section enables you to set property values to be sent to the device.</span></span>
* <span data-ttu-id="e790e-165">В разделе **Device Twin - Reported Properties** (Двойник устройства — Переданные свойства) отображаются значения свойств, отправляемые из устройства.</span><span class="sxs-lookup"><span data-stu-id="e790e-165">The **Device Twin - Reported Properties** section shows property values sent from the device.</span></span>
* <span data-ttu-id="e790e-166">В разделе **Свойства устройства** отображаются сведения из реестра удостоверений, например идентификатор устройства и ключи проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e790e-166">The **Device Properties** section shows information from the identity registry such as the device id and authentication keys.</span></span>
* <span data-ttu-id="e790e-167">В разделе **Последние задания** отображаются сведения обо всех заданиях, недавно назначенных этому устройству.</span><span class="sxs-lookup"><span data-stu-id="e790e-167">The **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-the-device-list"></a><span data-ttu-id="e790e-168">Фильтрация списка устройств</span><span class="sxs-lookup"><span data-stu-id="e790e-168">Filter the device list</span></span>

<span data-ttu-id="e790e-169">С помощью фильтра можно отобразить только те устройства, которые передают непредвиденные значения температуры.</span><span class="sxs-lookup"><span data-stu-id="e790e-169">You can use a filter to display only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="e790e-170">Предварительно настроенное решение удаленного мониторинга содержит фильтр **Неработоспособные устройства**, отображающий устройства, передающие среднее значение температуры выше 60.</span><span class="sxs-lookup"><span data-stu-id="e790e-170">The remote monitoring preconfigured solution includes the **Unhealthy devices** filter to show devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="e790e-171">Также можно [создать собственные фильтры](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="e790e-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="e790e-172">Выберите **Открыть сохраненный фильтр**, чтобы отобразить список доступных фильтров.</span><span class="sxs-lookup"><span data-stu-id="e790e-172">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="e790e-173">Выберите **Неработоспособные устройства**, чтобы применить фильтр:</span><span class="sxs-lookup"><span data-stu-id="e790e-173">Then choose **Unhealthy devices** to apply the filter:</span></span>

    ![Отображение списка фильтров][img-unhealthy-filter]

1. <span data-ttu-id="e790e-175">В списке устройств теперь отображаются только те устройства, которые передают среднее значение температуры выше 60.</span><span class="sxs-lookup"><span data-stu-id="e790e-175">The device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Просмотр отфильтрованного списка устройств, в котором отображаются неработоспособные устройства][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="e790e-177">Обновление требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="e790e-177">Update desired properties</span></span>

<span data-ttu-id="e790e-178">Вы определили набор устройств, которые необходимо исправить.</span><span class="sxs-lookup"><span data-stu-id="e790e-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="e790e-179">Предположим, что 15-секундного интервала обновления данных недостаточно для точной диагностики проблемы.</span><span class="sxs-lookup"><span data-stu-id="e790e-179">However, you decide that the data frequency of 15 seconds is not sufficient for a clear diagnosis of the issue.</span></span> <span data-ttu-id="e790e-180">Увеличение частоты телеметрии до пяти секунд для получения дополнительных данных поможет лучше определить проблему.</span><span class="sxs-lookup"><span data-stu-id="e790e-180">Changing the telemetry frequency to five seconds to provide you with more data points to better diagnose the issue.</span></span> <span data-ttu-id="e790e-181">Вы можете применить это изменение конфигурации к удаленным устройствам с помощью портала решения.</span><span class="sxs-lookup"><span data-stu-id="e790e-181">You can push this configuration change to your remote devices from the solution portal.</span></span> <span data-ttu-id="e790e-182">Можно применить изменение, оценить его влияние, а затем действовать в соответствии с полученными результатами.</span><span class="sxs-lookup"><span data-stu-id="e790e-182">You can make the change once, evaluate the impact, and then act on the results.</span></span>

<span data-ttu-id="e790e-183">Выполните следующие действия, чтобы запустить задание, которое изменяет требуемое свойство **TelemetryInterval** для затрагиваемых устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-183">Follow these steps to run a job that changes the **TelemetryInterval** desired property for the affected devices.</span></span> <span data-ttu-id="e790e-184">При получении нового значения свойства **TelemetryInterval** устройства изменят свою конфигурацию и будут передавать данные телеметрии каждые пять секунд вместо 15.</span><span class="sxs-lookup"><span data-stu-id="e790e-184">When the devices receive the new **TelemetryInterval** property value, they change their configuration to send telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="e790e-185">Когда в списке устройств отображаются неработоспособные устройства, выберите **Планировщик заданий**, а затем **Изменить двойник устройства**.</span><span class="sxs-lookup"><span data-stu-id="e790e-185">While you are showing the list of unhealthy devices in the device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="e790e-186">Вызовите задание **изменения интервала телеметрии**.</span><span class="sxs-lookup"><span data-stu-id="e790e-186">Call the job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="e790e-187">Задайте для значения **требуемого свойства** **desired.Config.TelemetryInterva** пять секунд.</span><span class="sxs-lookup"><span data-stu-id="e790e-187">Change the value of the **Desired Property** name **desired.Config.TelemetryInterval** to five seconds.</span></span>

1. <span data-ttu-id="e790e-188">Выберите **Расписание**.</span><span class="sxs-lookup"><span data-stu-id="e790e-188">Choose **Schedule**.</span></span>

    ![Изменение значения свойства TelemetryInterval на пять секунд][img-change-interval]

1. <span data-ttu-id="e790e-190">Вы можете отслеживать ход выполнения заданий на странице **Задания управления** на портале.</span><span class="sxs-lookup"><span data-stu-id="e790e-190">You can monitor the progress of the job on the **Management Jobs** page in the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="e790e-191">Если вы хотите изменить значение требуемого свойства для отдельных устройств, вместо выполнения задания используйте раздел **Требуемые свойства** на панели **Сведения об устройстве**.</span><span class="sxs-lookup"><span data-stu-id="e790e-191">If you want to change a desired property value for an individual device, use the **Desired Properties** section in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="e790e-192">Это задание задает значение требуемого свойства **TelemetryInterval** на двойнике устройства для всех устройств, выбранных с помощью фильтра.</span><span class="sxs-lookup"><span data-stu-id="e790e-192">This job sets the value of the **TelemetryInterval** desired property in the device twin for all the devices selected by the filter.</span></span> <span data-ttu-id="e790e-193">Устройства получают это значение от двойника устройства и обновляют свое поведение.</span><span class="sxs-lookup"><span data-stu-id="e790e-193">The devices retrieve this value from the device twin and update their behavior.</span></span> <span data-ttu-id="e790e-194">Когда устройство получает от двойника устройства требуемое свойство и обрабатывает его, оно задает соответствующее значение сообщаемого свойства.</span><span class="sxs-lookup"><span data-stu-id="e790e-194">When a device retrieves and processes a desired property from a device twin, it sets the corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="e790e-195">Вызов методов</span><span class="sxs-lookup"><span data-stu-id="e790e-195">Invoke methods</span></span>

<span data-ttu-id="e790e-196">Во время выполнения задания в списке неработоспособных устройств вы заметите, что эти устройства работают под управлением старой версии встроенного ПО (ниже версии 1.6).</span><span class="sxs-lookup"><span data-stu-id="e790e-196">While the job runs, you notice in the list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Просмотр версии сообщаемого встроенного ПО неработоспособных устройств][img-old-firmware]

<span data-ttu-id="e790e-198">Устаревшая версия встроенного ПО может стать основной причиной получения непредвиденных значений температуры, так как известно, что ПО других работоспособных устройств было недавно обновлено до версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="e790e-198">This firmware version may be the root cause of the unexpected temperature values because you know that other healthy devices were recently updated to version 2.0.</span></span> <span data-ttu-id="e790e-199">Можно воспользоваться встроенным фильтром **Old firmware devices** (Устройства с устаревшим встроенным ПО), чтобы определить все устройства с устаревшими версиями встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="e790e-199">You can use the built-in **Old firmware devices** filter to identify any devices with old firmware versions.</span></span> <span data-ttu-id="e790e-200">На портале можно удаленно обновить все устройства, которые продолжают работать под управлением старых версий встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="e790e-200">From the portal, you can then remotely update all the devices still running old firmware versions:</span></span>

1. <span data-ttu-id="e790e-201">Выберите **Открыть сохраненный фильтр**, чтобы отобразить список доступных фильтров.</span><span class="sxs-lookup"><span data-stu-id="e790e-201">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="e790e-202">Выберите **Old firmware devices** (Устройства с устаревшим встроенным ПО) для применения фильтра:</span><span class="sxs-lookup"><span data-stu-id="e790e-202">Then choose **Old firmware devices** to apply the filter:</span></span>

    ![Отображение списка фильтров][img-old-filter]

1. <span data-ttu-id="e790e-204">Теперь в списке устройств отображаются только устройства со старыми версиями встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="e790e-204">The device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="e790e-205">Этот список содержит пять устройств, определенных с помощью фильтра **Неработоспособные устройства**, и три дополнительных устройства.</span><span class="sxs-lookup"><span data-stu-id="e790e-205">This list includes the five devices identified by the **Unhealthy devices** filter and three additional devices:</span></span>

    ![Просмотр отфильтрованного списка устройств, в котором отображаются устройства с устаревшими версиями встроенного ПО][img-filtered-old-list]

1. <span data-ttu-id="e790e-207">Выберите **Планировщик заданий**, а затем — **Вызвать метод**.</span><span class="sxs-lookup"><span data-stu-id="e790e-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="e790e-208">В качестве **имени задания** введите **Обновление встроенного ПО до версии 2.0**.</span><span class="sxs-lookup"><span data-stu-id="e790e-208">Set **Job Name** to **Firmware update to version 2.0**.</span></span>

1. <span data-ttu-id="e790e-209">Выберите **InitiateFirmwareUpdate** в качестве **метода**.</span><span class="sxs-lookup"><span data-stu-id="e790e-209">Choose **InitiateFirmwareUpdate** as the **Method**.</span></span>

1. <span data-ttu-id="e790e-210">Для параметра **FwPackageUri** задайте значение **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="e790e-210">Set the **FwPackageUri** parameter to **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="e790e-211">Выберите **Расписание**.</span><span class="sxs-lookup"><span data-stu-id="e790e-211">Choose **Schedule**.</span></span> <span data-ttu-id="e790e-212">По умолчанию для задания используется значение "Запустить сейчас".</span><span class="sxs-lookup"><span data-stu-id="e790e-212">The default is for the job to run now.</span></span>

    ![Создание задания для обновления встроенного ПО выбранных устройств][img-method-update]

> [!NOTE]
> <span data-ttu-id="e790e-214">Если вы хотите вызвать метод для отдельного устройства, вместо выполнения задания на панели **Сведения об устройстве** выберите **Методы**.</span><span class="sxs-lookup"><span data-stu-id="e790e-214">If you want to invoke a method on an individual device, choose **Methods** in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="e790e-215">Это задание вызывает прямой метод **InitiateFirmwareUpdate** на всех устройствах, выбранных с помощью фильтра.</span><span class="sxs-lookup"><span data-stu-id="e790e-215">This job invokes the **InitiateFirmwareUpdate** direct method on all the devices selected by the filter.</span></span> <span data-ttu-id="e790e-216">Устройства немедленно отвечают Центру Интернета вещей и асинхронно инициируют процесс обновления встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="e790e-216">Devices respond immediately to IoT Hub and then initiate the firmware update process asynchronously.</span></span> <span data-ttu-id="e790e-217">Устройства предоставляют сведения о ходе процесса обновления встроенного ПО с помощью значений сообщаемых свойств, как показано на следующих снимках экрана.</span><span class="sxs-lookup"><span data-stu-id="e790e-217">The devices provide status information about the firmware update process through reported property values, as shown in the following screenshots.</span></span> <span data-ttu-id="e790e-218">Щелкните значок **Обновить**, чтобы обновить данные в списках устройств и заданий.</span><span class="sxs-lookup"><span data-stu-id="e790e-218">Choose the **Refresh** icon to update the information in the device and job lists:</span></span>

<span data-ttu-id="e790e-219">![Список заданий, отображающий выполнение обновления встроенного ПО][img-update-1]
![Список устройств, отображающий состояние обновления встроенного ПО][img-update-2]
![Список заданий, отображающий завершение обновления встроенного ПО][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="e790e-219">![Job list showing the firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing the firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="e790e-220">В рабочей среде можно запланировать выполнение заданий во время периода планового обслуживания.</span><span class="sxs-lookup"><span data-stu-id="e790e-220">In a production environment, you can schedule jobs to run during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="e790e-221">Разбор сценария</span><span class="sxs-lookup"><span data-stu-id="e790e-221">Scenario review</span></span>

<span data-ttu-id="e790e-222">В этом сценарии вы определили потенциальную проблему с некоторыми удаленными устройствами, используя фильтр и журнал оповещений на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="e790e-222">In this scenario, you identified a potential issue with some of your remote devices using the alarm history on the dashboard and a filter.</span></span> <span data-ttu-id="e790e-223">Затем с помощью фильтра и задания вы удаленно выполнили настройку устройств, чтобы получить дополнительные сведения для диагностики проблемы.</span><span class="sxs-lookup"><span data-stu-id="e790e-223">You then used the filter and a job to remotely configure the devices to provide more information to help diagnose the issue.</span></span> <span data-ttu-id="e790e-224">Наконец, вы использовали фильтр и задание, чтобы запланировать обслуживание затрагиваемых устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-224">Finally, you used a filter and a job to schedule maintenance on the affected devices.</span></span> <span data-ttu-id="e790e-225">На панели мониторинга можно проверить, что от устройств в решении оповещения больше не поступают.</span><span class="sxs-lookup"><span data-stu-id="e790e-225">If you return to the dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="e790e-226">Вы можете использовать фильтр, чтобы проверить актуальность встроенного ПО на всех устройствах в решении, а также чтобы убедиться в отсутствии неработоспособных устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-226">You can use a filter to verify that the firmware is up-to-date on all the devices in your solution and that there are no more unhealthy devices:</span></span>

![Фильтр, показывающий, что все устройства имеют актуальную версию встроенного ПО][img-updated]

![Фильтр, показывающий, что все устройства работоспособны][img-healthy]

## <a name="other-features"></a><span data-ttu-id="e790e-229">Другие возможности</span><span class="sxs-lookup"><span data-stu-id="e790e-229">Other features</span></span>

<span data-ttu-id="e790e-230">В следующих разделах приведены некоторые дополнительные возможности предварительно настроенного решения удаленного мониторинга, которые не описаны в предыдущем сценарии.</span><span class="sxs-lookup"><span data-stu-id="e790e-230">The following sections describe some additional features of the remote monitoring preconfigured solution that are not described as part of the previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="e790e-231">Настройка столбцов</span><span class="sxs-lookup"><span data-stu-id="e790e-231">Customize columns</span></span>

<span data-ttu-id="e790e-232">Вы можете настроить сведения, отображающиеся в списке устройств, щелкнув **Редактор столбцов**.</span><span class="sxs-lookup"><span data-stu-id="e790e-232">You can customize the information shown in the device list by choosing **Column editor**.</span></span> <span data-ttu-id="e790e-233">Кроме того, можно добавлять и удалять столбцы, отображающие полученные значения тегов и свойств,</span><span class="sxs-lookup"><span data-stu-id="e790e-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="e790e-234">а также изменять порядок столбцов и переименовывать их.</span><span class="sxs-lookup"><span data-stu-id="e790e-234">You can also reorder and rename columns:</span></span>

   ![Редактор столбцов в списке устройств][img-columneditor]

### <a name="customize-the-device-icon"></a><span data-ttu-id="e790e-236">Настройка значка устройства</span><span class="sxs-lookup"><span data-stu-id="e790e-236">Customize the device icon</span></span>

<span data-ttu-id="e790e-237">Вы можете настроить значок устройства, отображающийся в списке устройств, в области **Сведения об устройстве**.</span><span class="sxs-lookup"><span data-stu-id="e790e-237">You can customize the device icon displayed in the device list from the **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="e790e-238">Щелкните значок карандаша, чтобы открыть для устройства область **Изменить изображение**.</span><span class="sxs-lookup"><span data-stu-id="e790e-238">Choose the pencil icon to open the **Edit image** panel for a device:</span></span>

   ![Открытие редактора изображений устройств][img-startimageedit]

1. <span data-ttu-id="e790e-240">Отправьте новое изображение или используйте одно из существующих и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e790e-240">Either upload a new image or use one of the existing images and then choose **Save**:</span></span>

   ![Редактор изменения изображений устройства][img-imageedit]

1. <span data-ttu-id="e790e-242">Теперь в столбце **Значок** для устройства отображается изображение, которое вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="e790e-242">The image you selected now displays in the **Icon** column for the device.</span></span>

> [!NOTE]
> <span data-ttu-id="e790e-243">Изображение хранится в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="e790e-243">The image is stored in blob storage.</span></span> <span data-ttu-id="e790e-244">Тег в двойнике устройства содержит ссылку на изображение в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="e790e-244">A tag in the device twin contains a link to the image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="e790e-245">Добавление устройства</span><span class="sxs-lookup"><span data-stu-id="e790e-245">Add a device</span></span>

<span data-ttu-id="e790e-246">При развертывании предварительно настроенного решения автоматически подготавливаются 25 примеров устройств, которые вы можете увидеть в списке устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-246">When you deploy the preconfigured solution, you automatically provision 25 sample devices that you can see in the device list.</span></span> <span data-ttu-id="e790e-247">Это *виртуальные устройства*, работающие в веб-задании Azure.</span><span class="sxs-lookup"><span data-stu-id="e790e-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="e790e-248">Виртуальные устройства позволяют легко экспериментировать с предварительно настроенным решением без развертывания физических устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-248">Simulated devices make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical devices.</span></span> <span data-ttu-id="e790e-249">Если вы хотите подключить к решению физическое устройство, см. руководство [Подключение устройства к предварительно настроенному решению для удаленного мониторинга (Windows)][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="e790e-249">If you do want to connect a real device to the solution, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="e790e-250">Далее объясняется, как добавить виртуальное устройство к решению.</span><span class="sxs-lookup"><span data-stu-id="e790e-250">The following steps show you how to add a simulated device to the solution:</span></span>

1. <span data-ttu-id="e790e-251">Вернитесь к списку устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-251">Navigate back to the device list.</span></span>

1. <span data-ttu-id="e790e-252">В левом нижнем углу щелкните **+ Add a Device** (+ Добавить устройство), чтобы добавить устройство.</span><span class="sxs-lookup"><span data-stu-id="e790e-252">To add a device, choose **+ Add A Device** in the bottom left corner.</span></span>

   ![Добавление устройства в предварительно настроенное решение][img-adddevice]

1. <span data-ttu-id="e790e-254">На плитке **Имитированное устройство** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e790e-254">Choose **Add New** on the **Simulated Device** tile.</span></span>

   ![Настройка сведений о новом устройстве на панели мониторинга][img-addnew]

   <span data-ttu-id="e790e-256">Помимо создания виртуального устройства, можно также добавить физическое устройство на панели **Custom Device** (Пользовательское устройство).</span><span class="sxs-lookup"><span data-stu-id="e790e-256">In addition to creating a new simulated device, you can also add a physical device if you choose to create a **Custom Device**.</span></span> <span data-ttu-id="e790e-257">Дополнительные сведения о подключении к решению физических устройств см. в статье [Подключение устройства к предварительно настроенному решению для удаленного мониторинга (Windows)][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="e790e-257">To learn more about connecting physical devices to the solution, see [Connect your device to the IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="e790e-258">Выберите пункт **Let me define my own Device ID** (Задать идентификатор устройства самостоятельно) и укажите имя уникального идентификатора устройства: **mydevice_01**.</span><span class="sxs-lookup"><span data-stu-id="e790e-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="e790e-259">Выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e790e-259">Choose **Create**.</span></span>

   ![Сохранение нового устройства][img-definedevice]

1. <span data-ttu-id="e790e-261">На шаге 3 действия **Add a simulated device** (Добавить имитированное устройство) щелкните **Готово**, чтобы вернуться к списку устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-261">In step 3 of **Add a simulated device**, choose **Done** to return to the device list.</span></span>

1. <span data-ttu-id="e790e-262">В списке устройств состояние устройства изменится на **Работает** .</span><span class="sxs-lookup"><span data-stu-id="e790e-262">You can view your device **Running** in the device list.</span></span>

    ![Просмотр нового устройства в списке устройств][img-runningnew]

1. <span data-ttu-id="e790e-264">На панели мониторинга можно просмотреть данные телеметрии нового виртуального устройства:</span><span class="sxs-lookup"><span data-stu-id="e790e-264">You can also view the simulated telemetry from your new device on the dashboard:</span></span>

    ![Просмотр данных телеметрии с нового устройства][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="e790e-266">Отключение и удаление устройства</span><span class="sxs-lookup"><span data-stu-id="e790e-266">Disable and delete a device</span></span>

<span data-ttu-id="e790e-267">Можно отключить устройство, а после отключения его можно удалить.</span><span class="sxs-lookup"><span data-stu-id="e790e-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Отключение и удаление устройства][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="e790e-269">Добавление правила</span><span class="sxs-lookup"><span data-stu-id="e790e-269">Add a rule</span></span>

<span data-ttu-id="e790e-270">Только что созданное устройство пока не регулируется никакими правилами.</span><span class="sxs-lookup"><span data-stu-id="e790e-270">There are no rules for the new device you just added.</span></span> <span data-ttu-id="e790e-271">В этом разделе описано, как добавить правило, которое активирует оповещение, если значение температуры, сообщаемое новым устройством, превышает 47 градусов.</span><span class="sxs-lookup"><span data-stu-id="e790e-271">In this section, you add a rule that triggers an alarm when the temperature reported by the new device exceeds 47 degrees.</span></span> <span data-ttu-id="e790e-272">Прежде чем добавить правило, зайдите в раздел истории телеметрии на панели мониторинга и убедитесь, что температура нового устройства никогда не превышает 45 градусов.</span><span class="sxs-lookup"><span data-stu-id="e790e-272">Before you start, notice that the telemetry history for the new device on the dashboard shows the device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="e790e-273">Вернитесь к списку устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-273">Navigate back to the device list.</span></span>

1. <span data-ttu-id="e790e-274">Чтобы добавить для устройства правило, выберите новое устройство в **списке устройств**, а затем щелкните **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="e790e-274">To add a rule for the device, select your new device in the **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="e790e-275">В окне создания правила в поле данных выберите значение **Температура** и укажите **AlarmTemp** в качестве выходных данных правила при превышении 47 градусов:</span><span class="sxs-lookup"><span data-stu-id="e790e-275">Create a rule that uses **Temperature** as the data field and uses **AlarmTemp** as the output when the temperature exceeds 47 degrees:</span></span>

    ![Добавление правила устройства][img-adddevicerule]

1. <span data-ttu-id="e790e-277">Чтобы сохранить изменения, нажмите кнопку **Сохранить и просмотреть правила**.</span><span class="sxs-lookup"><span data-stu-id="e790e-277">To save your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="e790e-278">В области сведений о новом устройстве щелкните **Команды**.</span><span class="sxs-lookup"><span data-stu-id="e790e-278">Choose **Commands** in the device details pane for the new device.</span></span>

    ![Добавление правила устройства][img-adddevicerule2]

1. <span data-ttu-id="e790e-280">В списке команд выберите **ChangeSetPointTemp** и укажите в поле **SetPointTemp** значение 45.</span><span class="sxs-lookup"><span data-stu-id="e790e-280">Select **ChangeSetPointTemp** from the command list and set **SetPointTemp** to 45.</span></span> <span data-ttu-id="e790e-281">Выберите **Отправить команду**.</span><span class="sxs-lookup"><span data-stu-id="e790e-281">Then choose **Send Command**:</span></span>

    ![Добавление правила устройства][img-adddevicerule3]

1. <span data-ttu-id="e790e-283">Вернитесь на панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="e790e-283">Navigate back to the dashboard.</span></span> <span data-ttu-id="e790e-284">Вскоре, когда температура, сообщаемая новым устройством, превысит пороговое значение в 47 градусов, на панели **Журнал оповещений** появится новая запись.</span><span class="sxs-lookup"><span data-stu-id="e790e-284">After a short time, you will see a new entry in the **Alarm History** pane when the temperature reported by your new device exceeds the 47-degree threshold:</span></span>

    ![Добавление правила устройства][img-adddevicerule4]

1. <span data-ttu-id="e790e-286">На странице **Правила** панели мониторинга можно просматривать и изменять все правила.</span><span class="sxs-lookup"><span data-stu-id="e790e-286">You can review and edit all your rules on the **Rules** page of the dashboard:</span></span>

    ![Список правил устройства][img-rules]

1. <span data-ttu-id="e790e-288">На странице **Действия** панели мониторинга можно просматривать и изменять все действия, которые могут быть предприняты при выполнении условия, заданного правилом.</span><span class="sxs-lookup"><span data-stu-id="e790e-288">You can review and edit all the actions that can be taken in response to a rule on the **Actions** page of the dashboard:</span></span>

    ![Список действий с устройством][img-actions]

> [!NOTE]
> <span data-ttu-id="e790e-290">Вы можете определить действия, при которых будут отправляться сообщения или SMS в случае выполнения условия, заданного правилом. Кроме того, действия можно интегрировать с бизнес-системой с помощью [приложения логики][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="e790e-290">It is possible to define actions that can send an email message or SMS in response to a rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="e790e-291">Дополнительные сведения см. в статье [Руководство. Подключение приложения логики к предварительно настроенному решению для удаленного мониторинга Azure IoT Suite][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="e790e-291">For more information, see the [Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="e790e-292">Управление фильтрами</span><span class="sxs-lookup"><span data-stu-id="e790e-292">Manage filters</span></span>

<span data-ttu-id="e790e-293">В списке устройств вы можете создавать, сохранять и обновлять фильтры, чтобы отобразить настраиваемый список устройств, подключенных к центру.</span><span class="sxs-lookup"><span data-stu-id="e790e-293">In the device list, you can create, save, and reload filters to display a customized list of devices connected to your hub.</span></span> <span data-ttu-id="e790e-294">Чтобы создать фильтр, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e790e-294">To create a filter:</span></span>

1. <span data-ttu-id="e790e-295">Щелкните значок изменения фильтра, расположенный над списком устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-295">Choose the edit filter icon above the list of devices:</span></span>

    ![Открытие редактора фильтров][img-editfiltericon]

1. <span data-ttu-id="e790e-297">В разделе **Редактор фильтров** можно добавить поля, операторы и значения для фильтрации списка устройств.</span><span class="sxs-lookup"><span data-stu-id="e790e-297">In the **Filter editor**, add the fields, operators, and values to filter the device list.</span></span> <span data-ttu-id="e790e-298">Вы можете добавить несколько предложений для уточнения фильтра.</span><span class="sxs-lookup"><span data-stu-id="e790e-298">You can add multiple clauses to refine your filter.</span></span> <span data-ttu-id="e790e-299">Щелкните параметр **Фильтр**, чтобы применить фильтр.</span><span class="sxs-lookup"><span data-stu-id="e790e-299">Choose **Filter** to apply the filter:</span></span>

    ![Создание фильтра][img-filtereditor]

1. <span data-ttu-id="e790e-301">В этом примере список фильтруется по изготовителю и номеру модели.</span><span class="sxs-lookup"><span data-stu-id="e790e-301">In this example, the list is filtered by manufacturer and model number:</span></span>

    ![Фильтрованный список][img-filterelist]

1. <span data-ttu-id="e790e-303">Чтобы сохранить фильтр с пользовательским именем, щелкните значок **Сохранить как**.</span><span class="sxs-lookup"><span data-stu-id="e790e-303">To save your filter with a custom name, choose the **Save as** icon:</span></span>

    ![Сохранение фильтра][img-savefilter]

1. <span data-ttu-id="e790e-305">Чтобы повторно применить ранее сохраненный фильтр, щелкните значок **Открыть сохраненный фильтр**.</span><span class="sxs-lookup"><span data-stu-id="e790e-305">To reapply a filter you saved previously, choose the **Open saved filter** icon:</span></span>

    ![Открытие фильтра][img-openfilter]

<span data-ttu-id="e790e-307">Вы можете создавать фильтры на основе идентификатора устройства, его состояния, требуемых или переданных свойств и тегов.</span><span class="sxs-lookup"><span data-stu-id="e790e-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="e790e-308">Добавьте собственные настраиваемые теги для устройства в разделе **Теги** панели **Сведения об устройстве** или выполните задание, которое обновит теги на нескольких устройствах.</span><span class="sxs-lookup"><span data-stu-id="e790e-308">You add your own custom tags to a device in the **Tags** section of the **Device Details** panel, or run a job to update tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="e790e-309">Если вам необходимо изменить текст запроса, это можно сделать непосредственно, использовав **расширенное представление** в **редакторе фильтров**.</span><span class="sxs-lookup"><span data-stu-id="e790e-309">In the **Filter editor**, you can use the **Advanced view** to edit the query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="e790e-310">Команды</span><span class="sxs-lookup"><span data-stu-id="e790e-310">Commands</span></span>

<span data-ttu-id="e790e-311">В области **Сведения об устройстве** можно отправить команды на устройство.</span><span class="sxs-lookup"><span data-stu-id="e790e-311">From the **Device Details** panel, you can send commands to the device.</span></span> <span data-ttu-id="e790e-312">При первом запуске устройство отправляет решению сведения о командах, которые оно поддерживает.</span><span class="sxs-lookup"><span data-stu-id="e790e-312">When a device first starts, it sends information about the commands it supports to the solution.</span></span> <span data-ttu-id="e790e-313">Описание различий между командами и методами см. в статье [Параметры отправки сообщений из облака на устройство с помощью Центра Интернета вещей Azure][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="e790e-313">For a discussion of the differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="e790e-314">В области **Сведения об устройстве** выбранного устройства щелкните **Команды**.</span><span class="sxs-lookup"><span data-stu-id="e790e-314">Choose **Commands** in the **Device Details** panel for the selected device:</span></span>

   ![Команды устройств на панели мониторинга][img-devicecommands]

1. <span data-ttu-id="e790e-316">В списке команд выберите **PingDevice** .</span><span class="sxs-lookup"><span data-stu-id="e790e-316">Select **PingDevice** from the command list.</span></span>

1. <span data-ttu-id="e790e-317">Щелкните **Отправить команду**.</span><span class="sxs-lookup"><span data-stu-id="e790e-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="e790e-318">В журнале команд отобразится состояние команды.</span><span class="sxs-lookup"><span data-stu-id="e790e-318">You can see the status of the command in the command history.</span></span>

   ![Состояние команды на панели мониторинга][img-pingcommand]

<span data-ttu-id="e790e-320">Решение отслеживает состояние каждой отправляемой команды.</span><span class="sxs-lookup"><span data-stu-id="e790e-320">The solution tracks the status of each command it sends.</span></span> <span data-ttu-id="e790e-321">Изначальное состояние команды — **Ожидание**.</span><span class="sxs-lookup"><span data-stu-id="e790e-321">Initially the result is **Pending**.</span></span> <span data-ttu-id="e790e-322">Когда устройство сообщает о выполнении команды, значение состояния изменяется на **Успешно**.</span><span class="sxs-lookup"><span data-stu-id="e790e-322">When the device reports that it has executed the command, the result is set to **Success**.</span></span>

## <a name="behind-the-scenes"></a><span data-ttu-id="e790e-323">Сопутствующие ресурсы</span><span class="sxs-lookup"><span data-stu-id="e790e-323">Behind the scenes</span></span>

<span data-ttu-id="e790e-324">При развертывании предварительно настроенного решения создается несколько ресурсов в выбранной подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="e790e-324">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="e790e-325">Эти ресурсы можно просмотреть на [портале Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="e790e-325">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="e790e-326">Имя **группы ресурсов** , создаваемой при развертывании, зависит от имени, выбранного для предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="e790e-326">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Предварительно настроенное решение на портале Azure][img-portal]

<span data-ttu-id="e790e-328">Параметры каждого ресурса можно просмотреть, выбрав его в списке в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e790e-328">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="e790e-329">Можно также просмотреть исходный код предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="e790e-329">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="e790e-330">Исходный код предварительно настроенного решения для удаленного мониторинга находится в репозитории GitHub [azure-iot-remote-monitoring][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="e790e-330">The remote monitoring preconfigured solution source code is in the [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="e790e-331">В папке **DeviceAdministration** содержится исходный код для панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="e790e-331">The **DeviceAdministration** folder contains the source code for the dashboard.</span></span>
* <span data-ttu-id="e790e-332">В папке **Simulator** содержится исходный код для виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="e790e-332">The **Simulator** folder contains the source code for the simulated device.</span></span>
* <span data-ttu-id="e790e-333">В папке **EventProcessor** содержится исходный код для фонового процесса, который обрабатывает входящие данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="e790e-333">The **EventProcessor** folder contains the source code for the back-end process that handles the incoming telemetry.</span></span>

<span data-ttu-id="e790e-334">Завершив работу, можно удалить предварительно настроенное решение из подписки Azure на сайте [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="e790e-334">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="e790e-335">На этом сайте можно легко удалить все ресурсы, подготовленные при создании предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="e790e-335">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="e790e-336">Чтобы полностью удалить все ресурсы, связанные с предварительно настроенным решением, а не группу ресурсов на портале, удалите эти ресурсы на сайте [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="e790e-336">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site and do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e790e-337">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e790e-337">Next Steps</span></span>

<span data-ttu-id="e790e-338">Теперь, когда вы развернули рабочее предварительно настроенное решение, вы можете продолжить знакомство с IoT Suite. См. следующие статьи.</span><span class="sxs-lookup"><span data-stu-id="e790e-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="e790e-339">[Пошаговое руководство по работе с настроенным решением для удаленного мониторинга][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="e790e-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="e790e-340">[Подключение устройства к предварительно настроенному решению для удаленного мониторинга][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="e790e-340">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="e790e-341">[Разрешения на сайте azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="e790e-341">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

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