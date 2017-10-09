---
title: "Пошаговое руководство по решениям предварительно настроен мониторинг aaaRemote | Документы Microsoft"
description: "Описание удаленный мониторинг hello Azure IoT предварительно настроенное решение и его архитектуры."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="ebc01-103">Пошаговое руководство по работе с настроенным решением для удаленного мониторинга</span><span class="sxs-lookup"><span data-stu-id="ebc01-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="ebc01-104">Здравствуйте, удаленное наблюдение за IoT Suite [предварительно настроенное решение] [ lnk-preconfigured-solutions] является реализация end-to-end решением для мониторинга нескольких машинах в удаленных расположениях.</span><span class="sxs-lookup"><span data-stu-id="ebc01-104">hello IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="ebc01-105">решение Hello объединяет tooprovide ключа служб Azure универсальную реализацию hello бизнес-сценария.</span><span class="sxs-lookup"><span data-stu-id="ebc01-105">hello solution combines key Azure services tooprovide a generic implementation of hello business scenario.</span></span> <span data-ttu-id="ebc01-106">Hello решения можно использовать в качестве отправной точки для свою собственную реализацию и [настроить] [ lnk-customize] его toomeet требованиями бизнеса.</span><span class="sxs-lookup"><span data-stu-id="ebc01-106">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="ebc01-107">В этой статье поможет выполнить некоторые ключевые элементы hello hello удаленного мониторинга решения tooenable toounderstand ее работы.</span><span class="sxs-lookup"><span data-stu-id="ebc01-107">This article walks you through some of hello key elements of hello remote monitoring solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="ebc01-108">Эти знания помогут вам:</span><span class="sxs-lookup"><span data-stu-id="ebc01-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="ebc01-109">Устранение неполадок в решении hello.</span><span class="sxs-lookup"><span data-stu-id="ebc01-109">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="ebc01-110">Планирование как toocustomize toohello решения toomeet конкретным требованиям.</span><span class="sxs-lookup"><span data-stu-id="ebc01-110">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span> 
* <span data-ttu-id="ebc01-111">спроектировать собственное решение IoT, использующее службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ebc01-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="ebc01-112">Логическая архитектура</span><span class="sxs-lookup"><span data-stu-id="ebc01-112">Logical architecture</span></span>

<span data-ttu-id="ebc01-113">Следующая схема Hello представлен краткий обзор hello логические компоненты hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="ebc01-113">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Логическая архитектура](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="ebc01-115">Виртуальные устройства</span><span class="sxs-lookup"><span data-stu-id="ebc01-115">Simulated devices</span></span>

<span data-ttu-id="ebc01-116">В решении предварительно настроенных hello hello имитированное устройство представляет устройство охлаждения (например, здания кондиционер или единица обработки воздуху территории).</span><span class="sxs-lookup"><span data-stu-id="ebc01-116">In hello preconfigured solution, hello simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="ebc01-117">При развертывании решения hello предварительно настроен, также автоматически подготовить четыре имитацию устройствами под управлением в [веб-задания Azure][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="ebc01-117">When you deploy hello preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="ebc01-118">Hello имитируемые устройства облегчают вы tooexplore hello поведение hello решения без необходимости toodeploy hello все физические устройства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-118">hello simulated devices make it easy for you tooexplore hello behavior of hello solution without hello need toodeploy any physical devices.</span></span> <span data-ttu-id="ebc01-119">toodeploy физического устройства в разделе hello [подключения вашего устройства toohello удаленное наблюдение предварительно настроенных решений] [ lnk-connect-rm] учебника.</span><span class="sxs-lookup"><span data-stu-id="ebc01-119">toodeploy a real physical device, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="ebc01-120">Отправка сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="ebc01-120">Device-to-cloud messages</span></span>

<span data-ttu-id="ebc01-121">Каждый имитированное устройство может отправлять hello следующие типы сообщений tooIoT концентратора:</span><span class="sxs-lookup"><span data-stu-id="ebc01-121">Each simulated device can send hello following message types tooIoT Hub:</span></span>

| <span data-ttu-id="ebc01-122">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ebc01-122">Message</span></span> | <span data-ttu-id="ebc01-123">Описание</span><span class="sxs-lookup"><span data-stu-id="ebc01-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ebc01-124">Запуск</span><span class="sxs-lookup"><span data-stu-id="ebc01-124">Startup</span></span> |<span data-ttu-id="ebc01-125">При запуске hello устройство отправляет **сведения об устройстве** сообщение, содержащее сведения о себе toohello серверной части.</span><span class="sxs-lookup"><span data-stu-id="ebc01-125">When hello device starts, it sends a **device-info** message containing information about itself toohello back end.</span></span> <span data-ttu-id="ebc01-126">Эти данные включают идентификатор устройства hello и список команд hello и методы hello поддерживает устройства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-126">This data includes hello device id and a list of hello commands and methods hello device supports.</span></span> |
| <span data-ttu-id="ebc01-127">Присутствие</span><span class="sxs-lookup"><span data-stu-id="ebc01-127">Presence</span></span> |<span data-ttu-id="ebc01-128">Устройство периодически отправляет **наличие** сообщений tooreport ли hello устройства могут быть наличие hello датчика.</span><span class="sxs-lookup"><span data-stu-id="ebc01-128">A device periodically sends a **presence** message tooreport whether hello device can sense hello presence of a sensor.</span></span> |
| <span data-ttu-id="ebc01-129">Телеметрия</span><span class="sxs-lookup"><span data-stu-id="ebc01-129">Telemetry</span></span> |<span data-ttu-id="ebc01-130">Устройство периодически отправляет **телеметрии** сообщение, уведомляющее имитацию значения для hello температуры и влажности, собранных с устройств hello смоделированные датчиков.</span><span class="sxs-lookup"><span data-stu-id="ebc01-130">A device periodically sends a **telemetry** message that reports simulated values for hello temperature and humidity collected from hello device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="ebc01-131">решение Hello хранит hello список команд, поддерживаемых устройств hello Cosmos DB базы данных, а не в двойных устройства hello.</span><span class="sxs-lookup"><span data-stu-id="ebc01-131">hello solution stores hello list of commands supported by hello device in a Cosmos DB database and not in hello device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="ebc01-132">Свойства и двойники устройств</span><span class="sxs-lookup"><span data-stu-id="ebc01-132">Properties and device twins</span></span>

<span data-ttu-id="ebc01-133">Hello имитации устройства отправляют hello следующие устройства свойства toohello [двойных] [ lnk-device-twins] в центр IoT hello как *сообщил свойства*.</span><span class="sxs-lookup"><span data-stu-id="ebc01-133">hello simulated devices send hello following device properties toohello [twin][lnk-device-twins] in hello IoT hub as *reported properties*.</span></span> <span data-ttu-id="ebc01-134">Hello устройство отправляет отчет свойства во время запуска, а также в ответ tooa **изменение состояния устройства** команды или метода.</span><span class="sxs-lookup"><span data-stu-id="ebc01-134">hello device sends reported properties at startup and in response tooa **Change Device State** command or method.</span></span>

| <span data-ttu-id="ebc01-135">Свойство</span><span class="sxs-lookup"><span data-stu-id="ebc01-135">Property</span></span> | <span data-ttu-id="ebc01-136">Назначение</span><span class="sxs-lookup"><span data-stu-id="ebc01-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="ebc01-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="ebc01-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="ebc01-138">Частота (в секундах) hello устройство отправляет данные телеметрии</span><span class="sxs-lookup"><span data-stu-id="ebc01-138">Frequency (seconds) hello device sends telemetry</span></span> |
| <span data-ttu-id="ebc01-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="ebc01-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="ebc01-140">Указывает среднее значение hello имитируемые температуры телеметрии hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-140">Specifies hello mean value for hello simulated temperature telemetry</span></span> |
| <span data-ttu-id="ebc01-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="ebc01-141">Device.DeviceID</span></span> |<span data-ttu-id="ebc01-142">Идентификатор, который будет предоставлен или назначенный при создании устройства в решении hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-142">Id that is either provided or assigned when a device is created in hello solution</span></span> |
| <span data-ttu-id="ebc01-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="ebc01-143">Device.DeviceState</span></span> | <span data-ttu-id="ebc01-144">Состояние устройства hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-144">State reported by hello device</span></span> |
| <span data-ttu-id="ebc01-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="ebc01-145">Device.CreatedTime</span></span> |<span data-ttu-id="ebc01-146">Время hello устройства был создан в решении hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-146">Time hello device was created in hello solution</span></span> |
| <span data-ttu-id="ebc01-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="ebc01-147">Device.StartupTime</span></span> |<span data-ttu-id="ebc01-148">Время hello устройство было запущено</span><span class="sxs-lookup"><span data-stu-id="ebc01-148">Time hello device was started</span></span> |
| <span data-ttu-id="ebc01-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="ebc01-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="ebc01-150">изменить номер версии последнего нужное свойство hello Hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-150">hello version number of hello last desired property change</span></span> |
| <span data-ttu-id="ebc01-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="ebc01-151">Device.Location.Latitude</span></span> |<span data-ttu-id="ebc01-152">Широта местоположение устройства hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-152">Latitude location of hello device</span></span> |
| <span data-ttu-id="ebc01-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="ebc01-153">Device.Location.Longitude</span></span> |<span data-ttu-id="ebc01-154">Долгота местоположение устройства hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-154">Longitude location of hello device</span></span> |
| <span data-ttu-id="ebc01-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="ebc01-155">System.Manufacturer</span></span> |<span data-ttu-id="ebc01-156">Производитель устройства</span><span class="sxs-lookup"><span data-stu-id="ebc01-156">Device manufacturer</span></span> |
| <span data-ttu-id="ebc01-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="ebc01-157">System.ModelNumber</span></span> |<span data-ttu-id="ebc01-158">Номер модели устройства hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-158">Model number of hello device</span></span> |
| <span data-ttu-id="ebc01-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="ebc01-159">System.SerialNumber</span></span> |<span data-ttu-id="ebc01-160">Серийный номер устройства hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-160">Serial number of hello device</span></span> |
| <span data-ttu-id="ebc01-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="ebc01-161">System.FirmwareVersion</span></span> |<span data-ttu-id="ebc01-162">Текущая версия встроенного по на устройстве hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-162">Current version of firmware on hello device</span></span> |
| <span data-ttu-id="ebc01-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="ebc01-163">System.Platform</span></span> |<span data-ttu-id="ebc01-164">Архитектура платформы устройства hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-164">Platform architecture of hello device</span></span> |
| <span data-ttu-id="ebc01-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="ebc01-165">System.Processor</span></span> |<span data-ttu-id="ebc01-166">Процессор работающего устройства hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-166">Processor running hello device</span></span> |
| <span data-ttu-id="ebc01-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="ebc01-167">System.InstalledRAM</span></span> |<span data-ttu-id="ebc01-168">Объем ОЗУ, установленного на устройстве hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-168">Amount of RAM installed on hello device</span></span> |

<span data-ttu-id="ebc01-169">Имитатор Hello начальные значения этих свойств в имитации устройствами с помощью образцов значений.</span><span class="sxs-lookup"><span data-stu-id="ebc01-169">hello simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="ebc01-170">Каждый раз, симулятор hello инициализирует имитации устройства, устройства hello tooIoT предварительно определенных метаданных hello концентратора отчеты в виде отчета свойства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-170">Each time hello simulator initializes a simulated device, hello device reports hello pre-defined metadata tooIoT Hub as reported properties.</span></span> <span data-ttu-id="ebc01-171">Свойства отчета можно обновлять только hello устройства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-171">Reported properties can only be updated by hello device.</span></span> <span data-ttu-id="ebc01-172">toochange свойство отчета, необходимо задать нужное свойство в решение портала.</span><span class="sxs-lookup"><span data-stu-id="ebc01-172">toochange a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="ebc01-173">Он несет hello hello устройства:</span><span class="sxs-lookup"><span data-stu-id="ebc01-173">It is hello responsibility of hello device to:</span></span>

1. <span data-ttu-id="ebc01-174">Периодически загрузить нужные свойства из центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="ebc01-174">Periodically retrieve desired properties from hello IoT hub.</span></span>
2. <span data-ttu-id="ebc01-175">Обновите конфигурацию с значение hello требуемого свойства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-175">Update its configuration with hello desired property value.</span></span>
3. <span data-ttu-id="ebc01-176">Отправьте hello новый концентратор задней toohello значение как свойство отчета.</span><span class="sxs-lookup"><span data-stu-id="ebc01-176">Send hello new value back toohello hub as a reported property.</span></span>

<span data-ttu-id="ebc01-177">На панели мониторинга решения hello, можно использовать *требуемого свойства* tooset свойства на устройстве с помощью hello [двойных устройства][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="ebc01-177">From hello solution dashboard, you can use *desired properties* tooset properties on a device by using hello [device twin][lnk-device-twins].</span></span> <span data-ttu-id="ebc01-178">Как правило устройство считывает значению свойства из tooupdate концентратора hello, его внутреннее состояние и hello отчета изменения обратно в качестве свойства отчета.</span><span class="sxs-lookup"><span data-stu-id="ebc01-178">Typically, a device reads a desired property value from hello hub tooupdate its internal state and report hello change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="ebc01-179">Hello имитированное устройство код использует только hello **Desired.Config.TemperatureMeanValue** и **Desired.Config.TelemetryInterval** hello tooupdate нужными свойствами сообщил отправил обратно свойства tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="ebc01-179">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="ebc01-180">Имитированное устройство hello пропускаются все остальные запросы на изменение нужного свойства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-180">All other desired property change requests are ignored in hello simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="ebc01-181">Методы</span><span class="sxs-lookup"><span data-stu-id="ebc01-181">Methods</span></span>

<span data-ttu-id="ebc01-182">Hello имитации устройства можно обрабатывать следующие методы hello ([прямой методы][lnk-direct-methods]) из портала решения hello через Центр IoT hello:</span><span class="sxs-lookup"><span data-stu-id="ebc01-182">hello simulated devices can handle hello following methods ([direct methods][lnk-direct-methods]) invoked from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="ebc01-183">Метод</span><span class="sxs-lookup"><span data-stu-id="ebc01-183">Method</span></span> | <span data-ttu-id="ebc01-184">Описание</span><span class="sxs-lookup"><span data-stu-id="ebc01-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ebc01-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="ebc01-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="ebc01-186">Указывает, что устройство hello tooperform обновление встроенного по</span><span class="sxs-lookup"><span data-stu-id="ebc01-186">Instructs hello device tooperform a firmware update</span></span> |
| <span data-ttu-id="ebc01-187">Reboot</span><span class="sxs-lookup"><span data-stu-id="ebc01-187">Reboot</span></span> |<span data-ttu-id="ebc01-188">Указывает, что устройство tooreboot hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-188">Instructs hello device tooreboot</span></span> |
| <span data-ttu-id="ebc01-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="ebc01-189">FactoryReset</span></span> |<span data-ttu-id="ebc01-190">Указывает, что tooperform устройство hello сброса</span><span class="sxs-lookup"><span data-stu-id="ebc01-190">Instructs hello device tooperform a factory reset</span></span> |

<span data-ttu-id="ebc01-191">Некоторые методы используют tooreport свойства отчета о ходе выполнения.</span><span class="sxs-lookup"><span data-stu-id="ebc01-191">Some methods use reported properties tooreport on progress.</span></span> <span data-ttu-id="ebc01-192">Например, hello **InitiateFirmwareUpdate** метод Моделирует выполнение обновления hello асинхронно на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="ebc01-192">For example, hello **InitiateFirmwareUpdate** method simulates running hello update asynchronously on hello device.</span></span> <span data-ttu-id="ebc01-193">метод Hello немедленно возвращает на устройстве hello прерывая toosend обратно обновления состояния асинхронной задачи hello toohello решений мониторинга с помощью команды сообщил свойства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-193">hello method returns immediately on hello device, while hello asynchronous task continues toosend status updates back toohello solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="ebc01-194">Команды</span><span class="sxs-lookup"><span data-stu-id="ebc01-194">Commands</span></span>

<span data-ttu-id="ebc01-195">Hello имитируемые устройства можно обрабатывать следующие команды (облака на устройство сообщений), отправляемые из портала решения hello через Центр IoT hello hello.</span><span class="sxs-lookup"><span data-stu-id="ebc01-195">hello simulated devices can handle hello following commands (cloud-to-device messages) sent from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="ebc01-196">Команда</span><span class="sxs-lookup"><span data-stu-id="ebc01-196">Command</span></span> | <span data-ttu-id="ebc01-197">Описание</span><span class="sxs-lookup"><span data-stu-id="ebc01-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ebc01-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="ebc01-198">PingDevice</span></span> |<span data-ttu-id="ebc01-199">Отправляет *ping* toocheck toohello устройство, он работоспособен</span><span class="sxs-lookup"><span data-stu-id="ebc01-199">Sends a *ping* toohello device toocheck it is alive</span></span> |
| <span data-ttu-id="ebc01-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="ebc01-200">StartTelemetry</span></span> |<span data-ttu-id="ebc01-201">Запускает hello устройство, отправляющее телеметрии</span><span class="sxs-lookup"><span data-stu-id="ebc01-201">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="ebc01-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="ebc01-202">StopTelemetry</span></span> |<span data-ttu-id="ebc01-203">Останавливает отправку телеметрии hello устройстве</span><span class="sxs-lookup"><span data-stu-id="ebc01-203">Stops hello device from sending telemetry</span></span> |
| <span data-ttu-id="ebc01-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="ebc01-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="ebc01-205">Изменения hello пороговое значение значение, вокруг которой hello случайные данные</span><span class="sxs-lookup"><span data-stu-id="ebc01-205">Changes hello set point value around which hello random data is generated</span></span> |
| <span data-ttu-id="ebc01-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="ebc01-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="ebc01-207">Триггеры hello toosend симулятор устройства значение дополнительных телеметрии (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="ebc01-207">Triggers hello device simulator toosend an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="ebc01-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="ebc01-208">ChangeDeviceState</span></span> |<span data-ttu-id="ebc01-209">Изменяет свойство расширенном состоянии для устройства hello и отправляет информационное сообщение hello устройства с устройства hello</span><span class="sxs-lookup"><span data-stu-id="ebc01-209">Changes an extended state property for hello device and sends hello device info message from hello device</span></span> |

> [!NOTE]
> <span data-ttu-id="ebc01-210">Сравнение этих команд (сообщений, отправляемых из облака на устройство) и методов (прямых методов) см. в статье [Руководство по обмену данными между облаком и устройством][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="ebc01-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="ebc01-211">Центр IoT</span><span class="sxs-lookup"><span data-stu-id="ebc01-211">IoT Hub</span></span>

<span data-ttu-id="ebc01-212">Hello [центр IoT] [ lnk-iothub] принимает данные, отправленные с устройств hello в облаке hello и делает ее доступной toohello задания Azure Stream Analytics (ASA).</span><span class="sxs-lookup"><span data-stu-id="ebc01-212">hello [IoT hub][lnk-iothub] ingests data sent from hello devices into hello cloud and makes it available toohello Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="ebc01-213">Каждое задание ASA поток использует отдельный центр IoT потребителя группы tooread hello поток сообщений из устройства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-213">Each stream ASA job uses a separate IoT Hub consumer group tooread hello stream of messages from your devices.</span></span>

<span data-ttu-id="ebc01-214">Здравствуйте центр IoT в решении hello также:</span><span class="sxs-lookup"><span data-stu-id="ebc01-214">hello IoT hub in hello solution also:</span></span>

- <span data-ttu-id="ebc01-215">Хранит в реестре удостоверений, сохраняет идентификаторы hello и ключей проверки подлинности всех устройств hello допускается tooconnect toohello портала.</span><span class="sxs-lookup"><span data-stu-id="ebc01-215">Maintains an identity registry that stores hello ids and authentication keys of all hello devices permitted tooconnect toohello portal.</span></span> <span data-ttu-id="ebc01-216">Можно включить и отключить устройствами с помощью реестра удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="ebc01-216">You can enable and disable devices through hello identity registry.</span></span>
- <span data-ttu-id="ebc01-217">Отправляет команды tooyour устройства от имени hello решение портала.</span><span class="sxs-lookup"><span data-stu-id="ebc01-217">Sends commands tooyour devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="ebc01-218">Вызывает методы на устройствах, от имени hello решение портала.</span><span class="sxs-lookup"><span data-stu-id="ebc01-218">Invokes methods on your devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="ebc01-219">Поддерживает двойники устройств для всех зарегистрированных устройств.</span><span class="sxs-lookup"><span data-stu-id="ebc01-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="ebc01-220">Двойных устройство сохраняет значения свойств hello, сообщаемые устройства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-220">A device twin stores hello property values reported by a device.</span></span> <span data-ttu-id="ebc01-221">Двойных устройства также хранит нужный набор hello решение портала для hello tooretrieve устройства при подключении рядом свойств.</span><span class="sxs-lookup"><span data-stu-id="ebc01-221">A device twin also stores desired properties, set in hello solution portal, for hello device tooretrieve when it next connects.</span></span>
- <span data-ttu-id="ebc01-222">Расписания заданий tooset свойства для нескольких устройств или вызвать методы на нескольких устройствах.</span><span class="sxs-lookup"><span data-stu-id="ebc01-222">Schedules jobs tooset properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="ebc01-223">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ebc01-223">Azure Stream Analytics</span></span>

<span data-ttu-id="ebc01-224">В удаленное наблюдение решения, hello [Azure Stream Analytics] [ lnk-asa] (ASA) отправляет устройства сообщений, полученных hello IoT hub tooother внутренней компонентов для обработки или хранения.</span><span class="sxs-lookup"><span data-stu-id="ebc01-224">In hello remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by hello IoT hub tooother back-end components for processing or storage.</span></span> <span data-ttu-id="ebc01-225">Разные задания ASA выполнения конкретных функций на основе содержимого hello сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="ebc01-225">Different ASA jobs perform specific functions based on hello content of hello messages.</span></span>

<span data-ttu-id="ebc01-226">**Задания 1: Сведения об устройстве** фильтрует сообщения сведения устройства из входящего потока сообщений hello и отправляет их конечной точки tooan концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="ebc01-226">**Job 1: Device Info** filters device information messages from hello incoming message stream and sends them tooan Event Hub endpoint.</span></span> <span data-ttu-id="ebc01-227">Устройство отправляет устройства информационных сообщений во время запуска и в ответ tooa **SendDeviceInfo** команды.</span><span class="sxs-lookup"><span data-stu-id="ebc01-227">A device sends device information messages at startup and in response tooa **SendDeviceInfo** command.</span></span> <span data-ttu-id="ebc01-228">Это задание использует следующий запрос определения tooidentify hello **сведения об устройстве** сообщения:</span><span class="sxs-lookup"><span data-stu-id="ebc01-228">This job uses hello following query definition tooidentify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="ebc01-229">Эта задача отправляет его выходные данные tooan концентратор событий для дальнейшей обработки.</span><span class="sxs-lookup"><span data-stu-id="ebc01-229">This job sends its output tooan Event Hub for further processing.</span></span>

<span data-ttu-id="ebc01-230">**Задание 2. Правила.** Оценивает входящие телеметрические значения температуры и влажности и сравнивает с пороговым значением для устройства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="ebc01-231">Пороговые значения задаются в редакторе правил hello доступна на портале hello решения.</span><span class="sxs-lookup"><span data-stu-id="ebc01-231">Threshold values are set in hello rules editor available in hello solution portal.</span></span> <span data-ttu-id="ebc01-232">Каждая пара "устройство/значение" хранится с меткой времени в большом двоичном объекте, который обработчик Stream Analytics считывает как **ссылочные данные**.</span><span class="sxs-lookup"><span data-stu-id="ebc01-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="ebc01-233">Задание Hello сравнивает значение любой непустой hello заданное пороговое значение для hello устройства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-233">hello job compares any non-empty value against hello set threshold for hello device.</span></span> <span data-ttu-id="ebc01-234">При превышении hello ">" условие выходных задания hello **сигнала** событие, указывающее hello пороговое значение превышено и предоставляет hello устройства, значения и значения отметок времени.</span><span class="sxs-lookup"><span data-stu-id="ebc01-234">If it exceeds hello '>' condition, hello job outputs an **alarm** event that indicates that hello threshold is exceeded and provides hello device, value, and timestamp values.</span></span> <span data-ttu-id="ebc01-235">Это задание использует следующий запрос определения tooidentify телеметрии сообщений, которые должны запускать оповещение hello:</span><span class="sxs-lookup"><span data-stu-id="ebc01-235">This job uses hello following query definition tooidentify telemetry messages that should trigger an alarm:</span></span>

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

<span data-ttu-id="ebc01-236">Hello задания отправляет его выходные данные tooan концентратора событий для дальнейшей обработки и сохраняет сведения о каждой предупреждения tooblob хранилища из портала hello решения могут быть прочитаны hello сведений о предупреждениях.</span><span class="sxs-lookup"><span data-stu-id="ebc01-236">hello job sends its output tooan Event Hub for further processing and saves details of each alert tooblob storage from where hello solution portal can read hello alert information.</span></span>

<span data-ttu-id="ebc01-237">**Задание 3: Телеметрии** обрабатывает входящий поток телеметрии устройства hello двумя способами.</span><span class="sxs-lookup"><span data-stu-id="ebc01-237">**Job 3: Telemetry** operates on hello incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="ebc01-238">Hello сначала отправляет все сообщения телеметрии из хранилища больших двоичных объектов toopersistent hello устройств для долговременного хранения.</span><span class="sxs-lookup"><span data-stu-id="ebc01-238">hello first sends all telemetry messages from hello devices toopersistent blob storage for long-term storage.</span></span> <span data-ttu-id="ebc01-239">Во-вторых, Hello вычисляет влажности среднее, минимальное и максимальное значения для скользящего окна каждые пять минут и отправляет этот tooblob хранения данных.</span><span class="sxs-lookup"><span data-stu-id="ebc01-239">hello second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data tooblob storage.</span></span> <span data-ttu-id="ebc01-240">портал решения Hello считывает данные телеметрии hello из диаграммы hello toopopulate хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="ebc01-240">hello solution portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="ebc01-241">Это задание использует hello после определения запроса:</span><span class="sxs-lookup"><span data-stu-id="ebc01-241">This job uses hello following query definition:</span></span>

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a><span data-ttu-id="ebc01-242">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="ebc01-242">Event Hubs</span></span>

<span data-ttu-id="ebc01-243">Hello **сведения об устройстве** и **правила** задания ASA выводят их данных tooEvent концентраторов tooreliably вперед на toohello **обработчик событий** в hello веб-задания.</span><span class="sxs-lookup"><span data-stu-id="ebc01-243">hello **device info** and **rules** ASA jobs output their data tooEvent Hubs tooreliably forward on toohello **Event Processor** running in hello WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="ebc01-244">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="ebc01-244">Azure storage</span></span>

<span data-ttu-id="ebc01-245">Hello решение использует все данные телеметрии необработанные и сводных данных о hello из устройств hello toopersist хранилища BLOB-объектов Azure в решении hello.</span><span class="sxs-lookup"><span data-stu-id="ebc01-245">hello solution uses Azure blob storage toopersist all hello raw and summarized telemetry data from hello devices in hello solution.</span></span> <span data-ttu-id="ebc01-246">портал Hello считывает данные телеметрии hello из диаграммы hello toopopulate хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="ebc01-246">hello portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="ebc01-247">оповещения toodisplay hello решение портала считывает hello данные из хранилища больших двоичных объектов, записываемых при телеметрии превысил значения hello настроить пороговые значения.</span><span class="sxs-lookup"><span data-stu-id="ebc01-247">toodisplay alerts, hello solution portal reads hello data from blob storage that records when telemetry values exceeded hello configured threshold values.</span></span> <span data-ttu-id="ebc01-248">решение Hello также использует больших двоичных объектов хранилища toorecord hello пороговые значения, заданные в портал hello решения.</span><span class="sxs-lookup"><span data-stu-id="ebc01-248">hello solution also uses blob storage toorecord hello threshold values you set in hello solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="ebc01-249">Веб-задания</span><span class="sxs-lookup"><span data-stu-id="ebc01-249">WebJobs</span></span>

<span data-ttu-id="ebc01-250">Кроме эмуляторах устройств toohosting hello, hello веб-заданий в решение hello также hello узла **обработчик событий** работает в веб-задания Azure, обрабатывающему команду ответов.</span><span class="sxs-lookup"><span data-stu-id="ebc01-250">In addition toohosting hello device simulators, hello WebJobs in hello solution also host hello **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="ebc01-251">Он использует команду ответа сообщения tooupdate hello устройства команда журнала (хранятся в базе данных Cosmos DB hello).</span><span class="sxs-lookup"><span data-stu-id="ebc01-251">It uses command response messages tooupdate hello device command history (stored in hello Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="ebc01-252">База данных Cosmos</span><span class="sxs-lookup"><span data-stu-id="ebc01-252">Cosmos DB</span></span>

<span data-ttu-id="ebc01-253">Hello решение использует сведения о toostore Cosmos DB базы данных о решении toohello подключенных устройств hello.</span><span class="sxs-lookup"><span data-stu-id="ebc01-253">hello solution uses a Cosmos DB database toostore information about hello devices connected toohello solution.</span></span> <span data-ttu-id="ebc01-254">Эти сведения включают hello журнала команды, отправляемые toodevices из портала решения hello и методы, вызываемые из портала hello решения.</span><span class="sxs-lookup"><span data-stu-id="ebc01-254">This information includes hello history of commands sent toodevices from hello solution portal and of methods invoked from hello solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="ebc01-255">Портал решения</span><span class="sxs-lookup"><span data-stu-id="ebc01-255">Solution portal</span></span>

<span data-ttu-id="ebc01-256">портал Hello решение — веб-приложения, развернутые как часть hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="ebc01-256">hello solution portal is a web app deployed as part of hello preconfigured solution.</span></span> <span data-ttu-id="ebc01-257">Hello ключа страницы портала решения hello: hello панели мониторинга и hello список устройств.</span><span class="sxs-lookup"><span data-stu-id="ebc01-257">hello key pages in hello solution portal are hello dashboard and hello device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="ebc01-258">Панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="ebc01-258">Dashboard</span></span>

<span data-ttu-id="ebc01-259">Эта страница в веб-приложения hello использует элементы управления javascript PowerBI (см. [репозитория визуальных элементов PowerBI](https://www.github.com/Microsoft/PowerBI-visuals)) данные телеметрии hello toovisualize с устройств hello.</span><span class="sxs-lookup"><span data-stu-id="ebc01-259">This page in hello web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetry data from hello devices.</span></span> <span data-ttu-id="ebc01-260">Hello решение использует hello ASA телеметрии задания toowrite hello телеметрии tooblob хранения данных.</span><span class="sxs-lookup"><span data-stu-id="ebc01-260">hello solution uses hello ASA telemetry job toowrite hello telemetry data tooblob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="ebc01-261">Список устройств</span><span class="sxs-lookup"><span data-stu-id="ebc01-261">Device list</span></span>

<span data-ttu-id="ebc01-262">На этой странице hello решение портала можно:</span><span class="sxs-lookup"><span data-stu-id="ebc01-262">From this page in hello solution portal you can:</span></span>

* <span data-ttu-id="ebc01-263">Подготовка нового устройства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-263">Provision a new device.</span></span> <span data-ttu-id="ebc01-264">Это действие задает hello уникальный идентификатор устройства и приводит к возникновению ошибки hello ключ проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ebc01-264">This action sets hello unique device id and generates hello authentication key.</span></span> <span data-ttu-id="ebc01-265">Записывает сведения о hello устройства tooboth hello реестра удостоверений центр IoT и базы данных Cosmos DB конкретного решения hello.</span><span class="sxs-lookup"><span data-stu-id="ebc01-265">It writes information about hello device tooboth hello IoT Hub identity registry and hello solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="ebc01-266">Управление свойствами устройства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-266">Manage device properties.</span></span> <span data-ttu-id="ebc01-267">Это действие выполняет просмотр имеющихся свойств и их обновление.</span><span class="sxs-lookup"><span data-stu-id="ebc01-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="ebc01-268">Отправка команд tooa устройства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-268">Send commands tooa device.</span></span>
* <span data-ttu-id="ebc01-269">Просмотр журнала hello команд для устройства.</span><span class="sxs-lookup"><span data-stu-id="ebc01-269">View hello command history for a device.</span></span>
* <span data-ttu-id="ebc01-270">Включение и отключение устройств.</span><span class="sxs-lookup"><span data-stu-id="ebc01-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebc01-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ebc01-271">Next steps</span></span>

<span data-ttu-id="ebc01-272">Hello следующих записях блога TechNet содержат более подробные сведения о hello удаленное наблюдение предварительно настроенных решений:</span><span class="sxs-lookup"><span data-stu-id="ebc01-272">hello following TechNet blog posts provide more detail about hello remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="ebc01-273">Удаленный мониторинг IoT Suite - в разделе hello изнутри-</span><span class="sxs-lookup"><span data-stu-id="ebc01-273">IoT Suite - Under hello Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="ebc01-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (IoT Suite. Удаленный мониторинг: добавление реальных и виртуальных устройств).</span><span class="sxs-lookup"><span data-stu-id="ebc01-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="ebc01-275">Вы можете продолжить, Приступая к работе с IoT Suite, считывая hello следующих статей.</span><span class="sxs-lookup"><span data-stu-id="ebc01-275">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="ebc01-276">[Подключиться с вашего устройства toohello удаленное наблюдение предварительно настроенных решений][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="ebc01-276">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="ebc01-277">[Разрешения на сайт azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="ebc01-277">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
