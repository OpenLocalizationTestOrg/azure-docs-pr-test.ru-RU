---
title: "Пошаговое руководство по предварительно настроенному решению удаленного мониторинга | Документация Майкрософт"
description: "Описание предварительно настроенного решения удаленного мониторинга Azure IoT и его архитектура."
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
ms.openlocfilehash: b28105f300723b542fa6d1aebc569439d5c73dc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="98d16-103">Пошаговое руководство по работе с настроенным решением для удаленного мониторинга</span><span class="sxs-lookup"><span data-stu-id="98d16-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="98d16-104">[Предварительно настроенное решение][lnk-preconfigured-solutions] удаленного мониторинга набора IoT Suite — это реализация решения комплексного мониторинга для сценария с использованием нескольких компьютеров в удаленных расположениях.</span><span class="sxs-lookup"><span data-stu-id="98d16-104">The IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="98d16-105">Это решение объединяет основные службы Azure, чтобы обеспечить универсальную реализацию бизнес-сценария.</span><span class="sxs-lookup"><span data-stu-id="98d16-105">The solution combines key Azure services to provide a generic implementation of the business scenario.</span></span> <span data-ttu-id="98d16-106">Его можно использовать в качестве отправной точки для собственной реализации и [настроить][lnk-customize] в соответствии с потребностями конкретной организации.</span><span class="sxs-lookup"><span data-stu-id="98d16-106">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span></span>

<span data-ttu-id="98d16-107">В этой статье рассматриваются некоторые основные компоненты решения для удаленного мониторинга, чтобы вы смогли представить, как оно работает.</span><span class="sxs-lookup"><span data-stu-id="98d16-107">This article walks you through some of the key elements of the remote monitoring solution to enable you to understand how it works.</span></span> <span data-ttu-id="98d16-108">Эти знания помогут вам:</span><span class="sxs-lookup"><span data-stu-id="98d16-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="98d16-109">устранить проблемы, возникшие с решением;</span><span class="sxs-lookup"><span data-stu-id="98d16-109">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="98d16-110">спланировать настройку решения в соответствии с определенными требованиями;</span><span class="sxs-lookup"><span data-stu-id="98d16-110">Plan how to customize to the solution to meet your own specific requirements.</span></span> 
* <span data-ttu-id="98d16-111">спроектировать собственное решение IoT, использующее службы Azure.</span><span class="sxs-lookup"><span data-stu-id="98d16-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="98d16-112">Логическая архитектура</span><span class="sxs-lookup"><span data-stu-id="98d16-112">Logical architecture</span></span>

<span data-ttu-id="98d16-113">На следующей диаграмме показаны логические компоненты предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="98d16-113">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![Логическая архитектура](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="98d16-115">Виртуальные устройства</span><span class="sxs-lookup"><span data-stu-id="98d16-115">Simulated devices</span></span>

<span data-ttu-id="98d16-116">В настроенном решении виртуальное устройство представляет собой устройство охлаждения (например, кондиционер воздуха в помещении или установку кондиционирования воздуха объекта).</span><span class="sxs-lookup"><span data-stu-id="98d16-116">In the preconfigured solution, the simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="98d16-117">При развертывании предварительно настроенного решения вы также автоматически подготавливаете четыре имитации устройств, которые выполняются в [веб-задании Azure][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="98d16-117">When you deploy the preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="98d16-118">Эти устройства упрощают изучение поведения решения, не требуя развертывания физических устройств.</span><span class="sxs-lookup"><span data-stu-id="98d16-118">The simulated devices make it easy for you to explore the behavior of the solution without the need to deploy any physical devices.</span></span> <span data-ttu-id="98d16-119">Сведения о развертывании физического устройства см. в статье [Подключение устройства к предварительно настроенному решению для удаленного мониторинга (Windows)][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="98d16-119">To deploy a real physical device, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="98d16-120">Отправка сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="98d16-120">Device-to-cloud messages</span></span>

<span data-ttu-id="98d16-121">Каждое виртуальное устройство может отправлять следующие типы сообщений в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="98d16-121">Each simulated device can send the following message types to IoT Hub:</span></span>

| <span data-ttu-id="98d16-122">Сообщение</span><span class="sxs-lookup"><span data-stu-id="98d16-122">Message</span></span> | <span data-ttu-id="98d16-123">Описание</span><span class="sxs-lookup"><span data-stu-id="98d16-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="98d16-124">Запуск</span><span class="sxs-lookup"><span data-stu-id="98d16-124">Startup</span></span> |<span data-ttu-id="98d16-125">При запуске устройство отправляет в серверную часть сообщение со **сведениями об устройстве** .</span><span class="sxs-lookup"><span data-stu-id="98d16-125">When the device starts, it sends a **device-info** message containing information about itself to the back end.</span></span> <span data-ttu-id="98d16-126">Например, идентификатор устройства и список команд и методов, поддерживаемых устройством.</span><span class="sxs-lookup"><span data-stu-id="98d16-126">This data includes the device id and a list of the commands and methods the device supports.</span></span> |
| <span data-ttu-id="98d16-127">Присутствие</span><span class="sxs-lookup"><span data-stu-id="98d16-127">Presence</span></span> |<span data-ttu-id="98d16-128">Устройство периодически отправляет сообщение о **присутствии** , чтобы сообщить, может ли оно определить присутствие датчика.</span><span class="sxs-lookup"><span data-stu-id="98d16-128">A device periodically sends a **presence** message to report whether the device can sense the presence of a sensor.</span></span> |
| <span data-ttu-id="98d16-129">Телеметрия</span><span class="sxs-lookup"><span data-stu-id="98d16-129">Telemetry</span></span> |<span data-ttu-id="98d16-130">Устройство периодически отправляет сообщение **телеметрии** со значениями температуры и влажности, полученными от виртуальных датчиков.</span><span class="sxs-lookup"><span data-stu-id="98d16-130">A device periodically sends a **telemetry** message that reports simulated values for the temperature and humidity collected from the device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="98d16-131">Решение сохраняет список команд, поддерживаемых устройством, в базе данных Cosmos DB, а не в двойнике устройства.</span><span class="sxs-lookup"><span data-stu-id="98d16-131">The solution stores the list of commands supported by the device in a Cosmos DB database and not in the device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="98d16-132">Свойства и двойники устройств</span><span class="sxs-lookup"><span data-stu-id="98d16-132">Properties and device twins</span></span>

<span data-ttu-id="98d16-133">Имитации устройств отправляют следующие свойства устройств [двойнику][lnk-device-twins] в Центре Интернета вещей в виде *сообщаемых свойств*.</span><span class="sxs-lookup"><span data-stu-id="98d16-133">The simulated devices send the following device properties to the [twin][lnk-device-twins] in the IoT hub as *reported properties*.</span></span> <span data-ttu-id="98d16-134">Устройство отправляет сообщаемые свойства при запуске и в ответ на метод или команду **изменения состояния устройства**.</span><span class="sxs-lookup"><span data-stu-id="98d16-134">The device sends reported properties at startup and in response to a **Change Device State** command or method.</span></span>

| <span data-ttu-id="98d16-135">Свойство</span><span class="sxs-lookup"><span data-stu-id="98d16-135">Property</span></span> | <span data-ttu-id="98d16-136">Назначение</span><span class="sxs-lookup"><span data-stu-id="98d16-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="98d16-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="98d16-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="98d16-138">Частота (в секундах), с которой устройство отправляет данные телеметрии</span><span class="sxs-lookup"><span data-stu-id="98d16-138">Frequency (seconds) the device sends telemetry</span></span> |
| <span data-ttu-id="98d16-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="98d16-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="98d16-140">Указывает среднее значение имитированных данных телеметрии (температуры)</span><span class="sxs-lookup"><span data-stu-id="98d16-140">Specifies the mean value for the simulated temperature telemetry</span></span> |
| <span data-ttu-id="98d16-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="98d16-141">Device.DeviceID</span></span> |<span data-ttu-id="98d16-142">Идентификатор, предоставленный или назначенный при создании устройства в решении</span><span class="sxs-lookup"><span data-stu-id="98d16-142">Id that is either provided or assigned when a device is created in the solution</span></span> |
| <span data-ttu-id="98d16-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="98d16-143">Device.DeviceState</span></span> | <span data-ttu-id="98d16-144">Состояние, сообщаемое устройством</span><span class="sxs-lookup"><span data-stu-id="98d16-144">State reported by the device</span></span> |
| <span data-ttu-id="98d16-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="98d16-145">Device.CreatedTime</span></span> |<span data-ttu-id="98d16-146">Время создания устройства в решении</span><span class="sxs-lookup"><span data-stu-id="98d16-146">Time the device was created in the solution</span></span> |
| <span data-ttu-id="98d16-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="98d16-147">Device.StartupTime</span></span> |<span data-ttu-id="98d16-148">Время запуска устройства</span><span class="sxs-lookup"><span data-stu-id="98d16-148">Time the device was started</span></span> |
| <span data-ttu-id="98d16-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="98d16-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="98d16-150">Номер версии последнего изменения требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="98d16-150">The version number of the last desired property change</span></span> |
| <span data-ttu-id="98d16-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="98d16-151">Device.Location.Latitude</span></span> |<span data-ttu-id="98d16-152">Широта расположения устройства</span><span class="sxs-lookup"><span data-stu-id="98d16-152">Latitude location of the device</span></span> |
| <span data-ttu-id="98d16-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="98d16-153">Device.Location.Longitude</span></span> |<span data-ttu-id="98d16-154">Долгота расположения устройства</span><span class="sxs-lookup"><span data-stu-id="98d16-154">Longitude location of the device</span></span> |
| <span data-ttu-id="98d16-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="98d16-155">System.Manufacturer</span></span> |<span data-ttu-id="98d16-156">Производитель устройства</span><span class="sxs-lookup"><span data-stu-id="98d16-156">Device manufacturer</span></span> |
| <span data-ttu-id="98d16-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="98d16-157">System.ModelNumber</span></span> |<span data-ttu-id="98d16-158">Номер модели устройства</span><span class="sxs-lookup"><span data-stu-id="98d16-158">Model number of the device</span></span> |
| <span data-ttu-id="98d16-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="98d16-159">System.SerialNumber</span></span> |<span data-ttu-id="98d16-160">Серийный номер устройства</span><span class="sxs-lookup"><span data-stu-id="98d16-160">Serial number of the device</span></span> |
| <span data-ttu-id="98d16-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="98d16-161">System.FirmwareVersion</span></span> |<span data-ttu-id="98d16-162">Текущая версия встроенного ПО на устройстве</span><span class="sxs-lookup"><span data-stu-id="98d16-162">Current version of firmware on the device</span></span> |
| <span data-ttu-id="98d16-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="98d16-163">System.Platform</span></span> |<span data-ttu-id="98d16-164">Архитектура платформы устройства</span><span class="sxs-lookup"><span data-stu-id="98d16-164">Platform architecture of the device</span></span> |
| <span data-ttu-id="98d16-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="98d16-165">System.Processor</span></span> |<span data-ttu-id="98d16-166">Процессор, управляющий устройством</span><span class="sxs-lookup"><span data-stu-id="98d16-166">Processor running the device</span></span> |
| <span data-ttu-id="98d16-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="98d16-167">System.InstalledRAM</span></span> |<span data-ttu-id="98d16-168">Объем ОЗУ, установленного на устройстве</span><span class="sxs-lookup"><span data-stu-id="98d16-168">Amount of RAM installed on the device</span></span> |

<span data-ttu-id="98d16-169">Симулятор заполняет эти свойства в виртуальных устройствах образцами данных.</span><span class="sxs-lookup"><span data-stu-id="98d16-169">The simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="98d16-170">Каждый раз, когда симулятор инициализирует имитацию устройства, устройство отправляет предварительно определенные метаданные в Центр Интернета вещей в виде сообщаемых свойств.</span><span class="sxs-lookup"><span data-stu-id="98d16-170">Each time the simulator initializes a simulated device, the device reports the pre-defined metadata to IoT Hub as reported properties.</span></span> <span data-ttu-id="98d16-171">Сообщаемые свойства могут обновляться только устройством.</span><span class="sxs-lookup"><span data-stu-id="98d16-171">Reported properties can only be updated by the device.</span></span> <span data-ttu-id="98d16-172">Чтобы изменить сообщаемое свойство, задайте на портале решения требуемое свойство.</span><span class="sxs-lookup"><span data-stu-id="98d16-172">To change a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="98d16-173">Устройство отвечает за следующие действия:</span><span class="sxs-lookup"><span data-stu-id="98d16-173">It is the responsibility of the device to:</span></span>

1. <span data-ttu-id="98d16-174">Периодическое получение требуемых свойств из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="98d16-174">Periodically retrieve desired properties from the IoT hub.</span></span>
2. <span data-ttu-id="98d16-175">Обновление своей конфигурации с помощью значения требуемого свойства.</span><span class="sxs-lookup"><span data-stu-id="98d16-175">Update its configuration with the desired property value.</span></span>
3. <span data-ttu-id="98d16-176">Отправка нового значения обратно в центр в виде сообщаемого свойства.</span><span class="sxs-lookup"><span data-stu-id="98d16-176">Send the new value back to the hub as a reported property.</span></span>

<span data-ttu-id="98d16-177">На панели мониторинга решения можно воспользоваться *требуемыми свойствами*, чтобы задать значения свойств устройства с помощью [двойника устройства][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="98d16-177">From the solution dashboard, you can use *desired properties* to set properties on a device by using the [device twin][lnk-device-twins].</span></span> <span data-ttu-id="98d16-178">Как правило, устройство считывает в центре значение требуемого свойства для обновления своего внутреннего состояния и сообщает об изменении в виде сообщаемого свойства.</span><span class="sxs-lookup"><span data-stu-id="98d16-178">Typically, a device reads a desired property value from the hub to update its internal state and report the change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="98d16-179">Код имитации устройства использует только требуемые свойства **Desired.Config.TemperatureMeanValue** и **Desired.Config.TelemetryInterval**, чтобы обновить сообщаемые свойства, отправляемые обратно в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="98d16-179">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="98d16-180">Все прочие запросы на изменение требуемых свойств в имитации устройства игнорируются.</span><span class="sxs-lookup"><span data-stu-id="98d16-180">All other desired property change requests are ignored in the simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="98d16-181">Методы</span><span class="sxs-lookup"><span data-stu-id="98d16-181">Methods</span></span>

<span data-ttu-id="98d16-182">Имитации устройств могут обрабатывать следующие методы ([прямые методы][lnk-direct-methods]), вызываемые из портала решения через Центр Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="98d16-182">The simulated devices can handle the following methods ([direct methods][lnk-direct-methods]) invoked from the solution portal through the IoT hub:</span></span>

| <span data-ttu-id="98d16-183">Метод</span><span class="sxs-lookup"><span data-stu-id="98d16-183">Method</span></span> | <span data-ttu-id="98d16-184">Описание</span><span class="sxs-lookup"><span data-stu-id="98d16-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="98d16-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="98d16-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="98d16-186">Сообщает устройству о выполнении обновления встроенного ПО</span><span class="sxs-lookup"><span data-stu-id="98d16-186">Instructs the device to perform a firmware update</span></span> |
| <span data-ttu-id="98d16-187">Reboot</span><span class="sxs-lookup"><span data-stu-id="98d16-187">Reboot</span></span> |<span data-ttu-id="98d16-188">Сообщает устройству о перезагрузке</span><span class="sxs-lookup"><span data-stu-id="98d16-188">Instructs the device to reboot</span></span> |
| <span data-ttu-id="98d16-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="98d16-189">FactoryReset</span></span> |<span data-ttu-id="98d16-190">Сообщает устройству о выполнении сброса до заводских настроек</span><span class="sxs-lookup"><span data-stu-id="98d16-190">Instructs the device to perform a factory reset</span></span> |

<span data-ttu-id="98d16-191">Некоторые методы используют сообщаемые свойства для продолжения процесса.</span><span class="sxs-lookup"><span data-stu-id="98d16-191">Some methods use reported properties to report on progress.</span></span> <span data-ttu-id="98d16-192">Например, метод **InitiateFirmwareUpdate** имитирует на устройстве асинхронное выполнение обновления.</span><span class="sxs-lookup"><span data-stu-id="98d16-192">For example, the **InitiateFirmwareUpdate** method simulates running the update asynchronously on the device.</span></span> <span data-ttu-id="98d16-193">Метод немедленно возвращается на устройстве, в то время как асинхронная задача продолжает отправлять обновления состояния обратно на панель мониторинга решения, используя сообщаемые свойства.</span><span class="sxs-lookup"><span data-stu-id="98d16-193">The method returns immediately on the device, while the asynchronous task continues to send status updates back to the solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="98d16-194">Команды</span><span class="sxs-lookup"><span data-stu-id="98d16-194">Commands</span></span>

<span data-ttu-id="98d16-195">Имитации устройств могут обрабатывать следующие команды (сообщения, отправляемые из облака на устройство), отправляемые из портала решения через Центр Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="98d16-195">The simulated devices can handle the following commands (cloud-to-device messages) sent from the solution portal through the IoT hub:</span></span>

| <span data-ttu-id="98d16-196">Команда</span><span class="sxs-lookup"><span data-stu-id="98d16-196">Command</span></span> | <span data-ttu-id="98d16-197">Описание</span><span class="sxs-lookup"><span data-stu-id="98d16-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="98d16-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="98d16-198">PingDevice</span></span> |<span data-ttu-id="98d16-199">Отправляет на устройство *ping-запрос* для проверки его активности</span><span class="sxs-lookup"><span data-stu-id="98d16-199">Sends a *ping* to the device to check it is alive</span></span> |
| <span data-ttu-id="98d16-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="98d16-200">StartTelemetry</span></span> |<span data-ttu-id="98d16-201">Запускает отправку данных телеметрии устройством</span><span class="sxs-lookup"><span data-stu-id="98d16-201">Starts the device sending telemetry</span></span> |
| <span data-ttu-id="98d16-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="98d16-202">StopTelemetry</span></span> |<span data-ttu-id="98d16-203">Останавливает отправку данных телеметрии устройством</span><span class="sxs-lookup"><span data-stu-id="98d16-203">Stops the device from sending telemetry</span></span> |
| <span data-ttu-id="98d16-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="98d16-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="98d16-205">Изменяет значение заданной точки, вокруг которой формируются случайные данные</span><span class="sxs-lookup"><span data-stu-id="98d16-205">Changes the set point value around which the random data is generated</span></span> |
| <span data-ttu-id="98d16-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="98d16-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="98d16-207">Вызывает отправку симулятором устройства дополнительного значения телеметрии (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="98d16-207">Triggers the device simulator to send an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="98d16-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="98d16-208">ChangeDeviceState</span></span> |<span data-ttu-id="98d16-209">Изменяет свойство расширенного состояния устройства и отправляет с устройства сообщение со сведениями об устройстве</span><span class="sxs-lookup"><span data-stu-id="98d16-209">Changes an extended state property for the device and sends the device info message from the device</span></span> |

> [!NOTE]
> <span data-ttu-id="98d16-210">Сравнение этих команд (сообщений, отправляемых из облака на устройство) и методов (прямых методов) см. в статье [Руководство по обмену данными между облаком и устройством][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="98d16-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="98d16-211">Центр IoT</span><span class="sxs-lookup"><span data-stu-id="98d16-211">IoT Hub</span></span>

<span data-ttu-id="98d16-212">[Центр Интернета вещей][lnk-iothub] принимает данные, отправленные с устройств в облако, и предоставляет к ним доступ заданиям Azure Stream Analytics (ASA).</span><span class="sxs-lookup"><span data-stu-id="98d16-212">The [IoT hub][lnk-iothub] ingests data sent from the devices into the cloud and makes it available to the Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="98d16-213">Каждый поток заданий ASA использует отдельную группу потребителей центра IoT для считывания потока сообщений с устройств.</span><span class="sxs-lookup"><span data-stu-id="98d16-213">Each stream ASA job uses a separate IoT Hub consumer group to read the stream of messages from your devices.</span></span>

<span data-ttu-id="98d16-214">Центр Интернета вещей также выполняет в решении следующие функции:</span><span class="sxs-lookup"><span data-stu-id="98d16-214">The IoT hub in the solution also:</span></span>

- <span data-ttu-id="98d16-215">Поддерживает реестр удостоверений, в котором хранятся идентификаторы и ключи аутентификации всех устройств с разрешением на подключение к порталу.</span><span class="sxs-lookup"><span data-stu-id="98d16-215">Maintains an identity registry that stores the ids and authentication keys of all the devices permitted to connect to the portal.</span></span> <span data-ttu-id="98d16-216">С помощью реестра удостоверений можно включать и отключать устройства.</span><span class="sxs-lookup"><span data-stu-id="98d16-216">You can enable and disable devices through the identity registry.</span></span>
- <span data-ttu-id="98d16-217">Отправляет устройствам команды от имени портала устройства.</span><span class="sxs-lookup"><span data-stu-id="98d16-217">Sends commands to your devices on behalf of the solution portal.</span></span>
- <span data-ttu-id="98d16-218">Вызывает на устройствах методы от имени портала устройства.</span><span class="sxs-lookup"><span data-stu-id="98d16-218">Invokes methods on your devices on behalf of the solution portal.</span></span>
- <span data-ttu-id="98d16-219">Поддерживает двойники устройств для всех зарегистрированных устройств.</span><span class="sxs-lookup"><span data-stu-id="98d16-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="98d16-220">Двойник устройства хранит значения свойств, сообщаемые устройством.</span><span class="sxs-lookup"><span data-stu-id="98d16-220">A device twin stores the property values reported by a device.</span></span> <span data-ttu-id="98d16-221">Двойник устройства также хранит требуемые свойства, заданные на портале решения, которые извлекаются устройством при следующем подключении.</span><span class="sxs-lookup"><span data-stu-id="98d16-221">A device twin also stores desired properties, set in the solution portal, for the device to retrieve when it next connects.</span></span>
- <span data-ttu-id="98d16-222">Планирует задания, чтобы задать значения свойств для нескольких устройств или вызвать методы на нескольких устройствах.</span><span class="sxs-lookup"><span data-stu-id="98d16-222">Schedules jobs to set properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="98d16-223">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="98d16-223">Azure Stream Analytics</span></span>

<span data-ttu-id="98d16-224">В решении удаленного мониторинга [Azure Stream Analytics][lnk-asa] (ASA) отправляет сообщения, полученные с устройств в Центре Интернета вещей, другим компонентам серверной части для обработки или хранения.</span><span class="sxs-lookup"><span data-stu-id="98d16-224">In the remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by the IoT hub to other back-end components for processing or storage.</span></span> <span data-ttu-id="98d16-225">Каждое задание ASA выполняет определенные функции в зависимости от содержимого сообщений.</span><span class="sxs-lookup"><span data-stu-id="98d16-225">Different ASA jobs perform specific functions based on the content of the messages.</span></span>

<span data-ttu-id="98d16-226">**Задание 1. Сведения об устройстве.** Фильтрует сообщения со сведениями об устройстве из входящего потока сообщений и отправляет их в конечную точку концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="98d16-226">**Job 1: Device Info** filters device information messages from the incoming message stream and sends them to an Event Hub endpoint.</span></span> <span data-ttu-id="98d16-227">Устройство отправляет сообщения с информацией об устройстве при запуске и в ответ на команду **SendDeviceInfo**.</span><span class="sxs-lookup"><span data-stu-id="98d16-227">A device sends device information messages at startup and in response to a **SendDeviceInfo** command.</span></span> <span data-ttu-id="98d16-228">Чтобы определить сообщения со **сведениями об устройстве**, задание использует следующее определение запроса.</span><span class="sxs-lookup"><span data-stu-id="98d16-228">This job uses the following query definition to identify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="98d16-229">Это задание отправляет выходные данные в концентратор событий для дальнейшей обработки.</span><span class="sxs-lookup"><span data-stu-id="98d16-229">This job sends its output to an Event Hub for further processing.</span></span>

<span data-ttu-id="98d16-230">**Задание 2. Правила.** Оценивает входящие телеметрические значения температуры и влажности и сравнивает с пороговым значением для устройства.</span><span class="sxs-lookup"><span data-stu-id="98d16-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="98d16-231">Пороговые значения задаются в редакторе правил, доступном на портале решения.</span><span class="sxs-lookup"><span data-stu-id="98d16-231">Threshold values are set in the rules editor available in the solution portal.</span></span> <span data-ttu-id="98d16-232">Каждая пара "устройство/значение" хранится с меткой времени в большом двоичном объекте, который обработчик Stream Analytics считывает как **ссылочные данные**.</span><span class="sxs-lookup"><span data-stu-id="98d16-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="98d16-233">Задание сравнивает все непустые значения с заданным пороговым значением для устройства.</span><span class="sxs-lookup"><span data-stu-id="98d16-233">The job compares any non-empty value against the set threshold for the device.</span></span> <span data-ttu-id="98d16-234">Если значение превышает условие ">", задание выводит событие **оповещения**, которое сигнализирует, что пороговое значение превышено, и указывает устройство, значение и метку времени.</span><span class="sxs-lookup"><span data-stu-id="98d16-234">If it exceeds the '>' condition, the job outputs an **alarm** event that indicates that the threshold is exceeded and provides the device, value, and timestamp values.</span></span> <span data-ttu-id="98d16-235">Чтобы определить сообщения телеметрии, которые должны активировать оповещение, задание использует следующее определение запроса:</span><span class="sxs-lookup"><span data-stu-id="98d16-235">This job uses the following query definition to identify telemetry messages that should trigger an alarm:</span></span>

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

<span data-ttu-id="98d16-236">Задание отправляет выходные данные в концентратор событий для дальнейшей обработки и сохраняет сведения о каждом оповещении в хранилище BLOB-объектов, откуда их может считывать портал решения.</span><span class="sxs-lookup"><span data-stu-id="98d16-236">The job sends its output to an Event Hub for further processing and saves details of each alert to blob storage from where the solution portal can read the alert information.</span></span>

<span data-ttu-id="98d16-237">**Задание 3. Телеметрия.** Работает на входящем потоке телеметрии устройства, используя два метода.</span><span class="sxs-lookup"><span data-stu-id="98d16-237">**Job 3: Telemetry** operates on the incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="98d16-238">Первый отправляет все сообщения телеметрии с устройств в постоянное хранилище BLOB-объектов для долгосрочного хранения.</span><span class="sxs-lookup"><span data-stu-id="98d16-238">The first sends all telemetry messages from the devices to persistent blob storage for long-term storage.</span></span> <span data-ttu-id="98d16-239">Второй вычисляет среднее, минимальное и максимальное значения влажности в течение пятиминутного скользящего окна, а потом отправляет эти данные в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="98d16-239">The second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data to blob storage.</span></span> <span data-ttu-id="98d16-240">Портал решения считывает данные телеметрии из хранилища BLOB-объектов, чтобы заполнить диаграммы.</span><span class="sxs-lookup"><span data-stu-id="98d16-240">The solution portal reads the telemetry data from blob storage to populate the charts.</span></span> <span data-ttu-id="98d16-241">Это задание использует следующее определение запроса:</span><span class="sxs-lookup"><span data-stu-id="98d16-241">This job uses the following query definition:</span></span>

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

## <a name="event-hubs"></a><span data-ttu-id="98d16-242">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="98d16-242">Event Hubs</span></span>

<span data-ttu-id="98d16-243">Задания ASA **Сведения об устройстве** и **Правила** выводят данные в концентраторы событий, чтобы надежно перенаправить их в **обработчик событий**, запущенный в веб-задании.</span><span class="sxs-lookup"><span data-stu-id="98d16-243">The **device info** and **rules** ASA jobs output their data to Event Hubs to reliably forward on to the **Event Processor** running in the WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="98d16-244">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="98d16-244">Azure storage</span></span>

<span data-ttu-id="98d16-245">Решение использует хранилище BLOB-объектов Azure, чтобы сохранять все необработанные и сводные данные телеметрии с устройств в решении.</span><span class="sxs-lookup"><span data-stu-id="98d16-245">The solution uses Azure blob storage to persist all the raw and summarized telemetry data from the devices in the solution.</span></span> <span data-ttu-id="98d16-246">Портал считывает данные телеметрии из хранилища BLOB-объектов, чтобы заполнить диаграммы.</span><span class="sxs-lookup"><span data-stu-id="98d16-246">The portal reads the telemetry data from blob storage to populate the charts.</span></span> <span data-ttu-id="98d16-247">Чтобы отобразить оповещения, портал решения считывает данные из хранилища BLOB-объектов, регистрирующего события превышения настроенных пороговых значений телеметрии.</span><span class="sxs-lookup"><span data-stu-id="98d16-247">To display alerts, the solution portal reads the data from blob storage that records when telemetry values exceeded the configured threshold values.</span></span> <span data-ttu-id="98d16-248">Решение также использует хранилище BLOB-объектов для записи пороговых значений, которые пользователь задал на портале решения.</span><span class="sxs-lookup"><span data-stu-id="98d16-248">The solution also uses blob storage to record the threshold values you set in the solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="98d16-249">Веб-задания</span><span class="sxs-lookup"><span data-stu-id="98d16-249">WebJobs</span></span>

<span data-ttu-id="98d16-250">В дополнение к размещению имитаций устройств в веб-заданиях решения также размещается **обработчик событий**, работающий в веб-задании Azure, который обрабатывает ответы команд.</span><span class="sxs-lookup"><span data-stu-id="98d16-250">In addition to hosting the device simulators, the WebJobs in the solution also host the **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="98d16-251">Он использует сообщения об ответе на команды для обновления журнала команд устройства (хранится в базе данных Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="98d16-251">It uses command response messages to update the device command history (stored in the Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="98d16-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="98d16-252">Cosmos DB</span></span>

<span data-ttu-id="98d16-253">Решение использует базу данных Cosmos DB для хранения сведений о подключенных к нему устройствах,</span><span class="sxs-lookup"><span data-stu-id="98d16-253">The solution uses a Cosmos DB database to store information about the devices connected to the solution.</span></span> <span data-ttu-id="98d16-254">например журнала команд, отправленных на устройства с портала решения, и методов, вызванных с портала решения.</span><span class="sxs-lookup"><span data-stu-id="98d16-254">This information includes the history of commands sent to devices from the solution portal and of methods invoked from the solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="98d16-255">Портал решения</span><span class="sxs-lookup"><span data-stu-id="98d16-255">Solution portal</span></span>

<span data-ttu-id="98d16-256">Портал решения представляет собой веб-приложение, разворачиваемое в составе предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="98d16-256">The solution portal is a web app deployed as part of the preconfigured solution.</span></span> <span data-ttu-id="98d16-257">Основными страницами на портале решения являются панель мониторинга и список устройств.</span><span class="sxs-lookup"><span data-stu-id="98d16-257">The key pages in the solution portal are the dashboard and the device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="98d16-258">Панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="98d16-258">Dashboard</span></span>

<span data-ttu-id="98d16-259">Эта страница в веб-приложении использует элементы управления JavaScript PowerBI (см. в [репозитории визуальных элементов PowerBI](https://www.github.com/Microsoft/PowerBI-visuals)) для визуализации данных телеметрии с устройств.</span><span class="sxs-lookup"><span data-stu-id="98d16-259">This page in the web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) to visualize the telemetry data from the devices.</span></span> <span data-ttu-id="98d16-260">Решение использует задание телеметрии ASA для записи данных телеметрии в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="98d16-260">The solution uses the ASA telemetry job to write the telemetry data to blob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="98d16-261">Список устройств</span><span class="sxs-lookup"><span data-stu-id="98d16-261">Device list</span></span>

<span data-ttu-id="98d16-262">На этой странице портала решения можно выполнить перечисленные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="98d16-262">From this page in the solution portal you can:</span></span>

* <span data-ttu-id="98d16-263">Подготовка нового устройства.</span><span class="sxs-lookup"><span data-stu-id="98d16-263">Provision a new device.</span></span> <span data-ttu-id="98d16-264">Это действие задает уникальный идентификатор устройства и создает ключ проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="98d16-264">This action sets the unique device id and generates the authentication key.</span></span> <span data-ttu-id="98d16-265">Сведения об устройстве записываются в реестр удостоверений центра IoT и базу данных Cosmos DB определенного решения.</span><span class="sxs-lookup"><span data-stu-id="98d16-265">It writes information about the device to both the IoT Hub identity registry and the solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="98d16-266">Управление свойствами устройства.</span><span class="sxs-lookup"><span data-stu-id="98d16-266">Manage device properties.</span></span> <span data-ttu-id="98d16-267">Это действие выполняет просмотр имеющихся свойств и их обновление.</span><span class="sxs-lookup"><span data-stu-id="98d16-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="98d16-268">Отправка команд на устройство.</span><span class="sxs-lookup"><span data-stu-id="98d16-268">Send commands to a device.</span></span>
* <span data-ttu-id="98d16-269">Просмотр журнала команд для устройства.</span><span class="sxs-lookup"><span data-stu-id="98d16-269">View the command history for a device.</span></span>
* <span data-ttu-id="98d16-270">Включение и отключение устройств.</span><span class="sxs-lookup"><span data-stu-id="98d16-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98d16-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98d16-271">Next steps</span></span>

<span data-ttu-id="98d16-272">В записях блога на сайте TechNet приведены дополнительные сведения о предварительно настроенном решении удаленного мониторинга:</span><span class="sxs-lookup"><span data-stu-id="98d16-272">The following TechNet blog posts provide more detail about the remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="98d16-273">IoT Suite - Under The Hood - Remote Monitoring (IoT Suite. Как работает удаленный мониторинг).</span><span class="sxs-lookup"><span data-stu-id="98d16-273">IoT Suite - Under The Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="98d16-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (IoT Suite. Удаленный мониторинг: добавление реальных и виртуальных устройств).</span><span class="sxs-lookup"><span data-stu-id="98d16-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="98d16-275">Дополнительные сведения об IoT Suite см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="98d16-275">You can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="98d16-276">[Подключение устройства к предварительно настроенному решению для удаленного мониторинга][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="98d16-276">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="98d16-277">[Разрешения на сайте azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="98d16-277">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

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
