---
title: "Настройка предварительно настроенных решений | Документация Майкрософт"
description: "Руководство по настройке предварительно настроенных решений набора Azure IoT Suite."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: bdf4cd89d5ad0392337dfe761108608d506adf18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="122a5-103">Настройка предварительно настроенного решения</span><span class="sxs-lookup"><span data-stu-id="122a5-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="122a5-104">Предварительно настроенные решения, входящие в состав набора IoT Azure, показывают, какие службы работают вместе в составе набора, формируя комплексное решение.</span><span class="sxs-lookup"><span data-stu-id="122a5-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span></span> <span data-ttu-id="122a5-105">Начиная с этой стартовой точки, есть несколько мест, в которых можно выполнить настройку и расширение решений для их адаптации к конкретным сценариям.</span><span class="sxs-lookup"><span data-stu-id="122a5-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span></span> <span data-ttu-id="122a5-106">В следующих разделах описываются эти точки настройки.</span><span class="sxs-lookup"><span data-stu-id="122a5-106">The following sections describe these common customization points.</span></span>

## <a name="find-the-source-code"></a><span data-ttu-id="122a5-107">Поиск исходного кода</span><span class="sxs-lookup"><span data-stu-id="122a5-107">Find the source code</span></span>

<span data-ttu-id="122a5-108">Исходный код для предварительно настроенного решения можно найти в GitHub в следующих репозиториях:</span><span class="sxs-lookup"><span data-stu-id="122a5-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span></span>

* <span data-ttu-id="122a5-109">Удаленный мониторинг: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="122a5-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="122a5-110">Прогнозируемое обслуживание: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="122a5-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="122a5-111">Подключенная фабрика: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="122a5-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="122a5-112">Исходный код для предварительно настроенных решений предоставляется для демонстрации шаблонов и методов, используемых для реализации полной функциональности решения IoT с помощью Azure IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="122a5-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="122a5-113">Дополнительные сведения о том, как создавать и развертывать решения, можно найти в репозиториях GitHub.</span><span class="sxs-lookup"><span data-stu-id="122a5-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span></span>

## <a name="change-the-preconfigured-rules"></a><span data-ttu-id="122a5-114">Изменение предварительно настроенных правил</span><span class="sxs-lookup"><span data-stu-id="122a5-114">Change the preconfigured rules</span></span>

<span data-ttu-id="122a5-115">Решение удаленного мониторинга включает в себя три задания [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) для обработки логики сведений об устройстве, телеметрии и правил в решении.</span><span class="sxs-lookup"><span data-stu-id="122a5-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span></span>

<span data-ttu-id="122a5-116">Три задания Stream Analytics и их синтаксис подробно описаны в [пошаговом руководстве по работе с настроенным решением для удаленного мониторинга](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="122a5-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="122a5-117">Эти задания можно редактировать напрямую, изменяя или добавляя логику для своего сценария.</span><span class="sxs-lookup"><span data-stu-id="122a5-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span></span> <span data-ttu-id="122a5-118">Задания Stream Analytics можно найти следующим образом:</span><span class="sxs-lookup"><span data-stu-id="122a5-118">You can find the Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="122a5-119">Перейдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="122a5-119">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="122a5-120">Перейдите к группе ресурсов, имя которой совпадает с именем вашего решения IoT.</span><span class="sxs-lookup"><span data-stu-id="122a5-120">Navigate to the resource group with the same name as your IoT solution.</span></span> 
3. <span data-ttu-id="122a5-121">Выберите задание Azure Stream Analytics, которое вы хотите изменить.</span><span class="sxs-lookup"><span data-stu-id="122a5-121">Select the Azure Stream Analytics job you'd like to modify.</span></span> 
4. <span data-ttu-id="122a5-122">Остановите задание, выбрав **Остановить** в наборе команд.</span><span class="sxs-lookup"><span data-stu-id="122a5-122">Stop the job by selecting **Stop** in the set of commands.</span></span> 
5. <span data-ttu-id="122a5-123">Измените входные данные, запрос и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="122a5-123">Edit the inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="122a5-124">В качестве простого изменения запроса для задания **Правила** можно изменить **">"** на **"<"**.</span><span class="sxs-lookup"><span data-stu-id="122a5-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="122a5-125">При изменении правила на портале в запросе по-прежнему отображается **">"**, но вы видите, как изменилось поведение из-за изменения базового задания.</span><span class="sxs-lookup"><span data-stu-id="122a5-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span></span>
6. <span data-ttu-id="122a5-126">Запустите задание</span><span class="sxs-lookup"><span data-stu-id="122a5-126">Start the job</span></span>

> [!NOTE]
> <span data-ttu-id="122a5-127">Панель удаленного мониторинга зависит от конкретных данных, поэтому изменение задания потенциально может вызвать сбой панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="122a5-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="122a5-128">Добавление собственных правил</span><span class="sxs-lookup"><span data-stu-id="122a5-128">Add your own rules</span></span>

<span data-ttu-id="122a5-129">Наряду с изменением предварительно настроенных заданий Stream Analytics на портале Azure можно добавлять новые задания или новые запросы для существующих заданий.</span><span class="sxs-lookup"><span data-stu-id="122a5-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="122a5-130">Настройка устройств</span><span class="sxs-lookup"><span data-stu-id="122a5-130">Customize devices</span></span>

<span data-ttu-id="122a5-131">Одно из наиболее распространенных действий расширения — работа с устройствами, относящимися к вашему сценарию.</span><span class="sxs-lookup"><span data-stu-id="122a5-131">One of the most common extension activities is working with devices specific to your scenario.</span></span> <span data-ttu-id="122a5-132">Существует несколько способов работы с устройствами.</span><span class="sxs-lookup"><span data-stu-id="122a5-132">There are several methods for working with devices.</span></span> <span data-ttu-id="122a5-133">В число этих методов входят изменение виртуального устройства для соответствия вашему сценарию или подключение физического устройства к решению с помощью [пакета SDK устройства Интернета вещей][IoT Device SDK].</span><span class="sxs-lookup"><span data-stu-id="122a5-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span></span>

<span data-ttu-id="122a5-134">Пошаговые инструкции по добавлению устройств см. в статье [Подключение устройства к предварительно настроенному решению для удаленного мониторинга (Windows)](iot-suite-connecting-devices.md). Также вы можете использовать [пример пакета SDK для удаленного мониторинга](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="122a5-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="122a5-135">Этот пример предназначен для работы с предварительно настроенным решением для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="122a5-135">This sample is designed to work with the remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="122a5-136">Создание собственного виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="122a5-136">Create your own simulated device</span></span>

<span data-ttu-id="122a5-137">В [исходный код решения удаленного мониторинга](https://github.com/Azure/azure-iot-remote-monitoring) включен симулятор .NET.</span><span class="sxs-lookup"><span data-stu-id="122a5-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="122a5-138">Этот симулятор подготавливается как часть решения, и его можно настроить для отправки разных метаданных и данных телеметрии, а также для реагирования на разные команды и методы.</span><span class="sxs-lookup"><span data-stu-id="122a5-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span></span>

<span data-ttu-id="122a5-139">Симулятор предварительно настроенного решения удаленного мониторинга имитирует устройство охлаждения, которое выдает данные телеметрии о температуре и влажности.</span><span class="sxs-lookup"><span data-stu-id="122a5-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="122a5-140">Изменить симулятор можно в проекте [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) при создании разветвления в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="122a5-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="122a5-141">Доступные расположения для виртуальных устройств</span><span class="sxs-lookup"><span data-stu-id="122a5-141">Available locations for simulated devices</span></span>

<span data-ttu-id="122a5-142">Расположения по умолчанию находятся в Редмонде (Сиэтле), штат Вашингтон, США.</span><span class="sxs-lookup"><span data-stu-id="122a5-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="122a5-143">Эти расположения можно изменить в файле [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="122a5-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a><span data-ttu-id="122a5-144">Добавление обработчика изменения для требуемого свойства в симуляторе</span><span class="sxs-lookup"><span data-stu-id="122a5-144">Add a desired property update handler to the simulator</span></span>

<span data-ttu-id="122a5-145">На портале решения вы можете задать значение для требуемого свойства устройства.</span><span class="sxs-lookup"><span data-stu-id="122a5-145">You can set a value for a desired property for a device in the solution portal.</span></span> <span data-ttu-id="122a5-146">Обработку запроса на изменение свойства должно выполнять само устройство, получая новое значение требуемого свойства.</span><span class="sxs-lookup"><span data-stu-id="122a5-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span></span> <span data-ttu-id="122a5-147">Чтобы добавить поддержку для изменения значений свойства через требуемое свойство, необходимо добавить в симулятор соответствующий обработчик.</span><span class="sxs-lookup"><span data-stu-id="122a5-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span></span>

<span data-ttu-id="122a5-148">Симулятор содержит обработчики для свойств **SetPointTemp** и **TelemetryInterval**, для изменения которых можно установить нужные значения на портале решения.</span><span class="sxs-lookup"><span data-stu-id="122a5-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span></span>

<span data-ttu-id="122a5-149">В следующем примере представлен обработчик требуемого свойства **SetPointTemp** в классе **CoolerDevice**:</span><span class="sxs-lookup"><span data-stu-id="122a5-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="122a5-150">Этот метод изменяет температуру для точки телеметрии и передает информацию об изменении в Центр Интернета вещей, устанавливая значение сообщаемого свойства.</span><span class="sxs-lookup"><span data-stu-id="122a5-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span></span>

<span data-ttu-id="122a5-151">Вы можете добавить собственные обработчики для требуемых свойств, используя шаблон из предыдущего примера.</span><span class="sxs-lookup"><span data-stu-id="122a5-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span></span>

<span data-ttu-id="122a5-152">Также следует привязать требуемое свойство к обработчику, как показано в следующем примере из конструктора **CoolerDevice**:</span><span class="sxs-lookup"><span data-stu-id="122a5-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="122a5-153">Обратите внимание, что **SetPointTempPropertyName** — это константа, определенная как Config.SetPointTemp.</span><span class="sxs-lookup"><span data-stu-id="122a5-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-to-the-simulator"></a><span data-ttu-id="122a5-154">Добавление в симулятор поддержки для нового метода</span><span class="sxs-lookup"><span data-stu-id="122a5-154">Add support for a new method to the simulator</span></span>

<span data-ttu-id="122a5-155">Вы можете изменить симулятор, добавив поддержку нового [метода (прямой метод)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="122a5-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="122a5-156">Нужно выполнить два основных действия.</span><span class="sxs-lookup"><span data-stu-id="122a5-156">There are two key steps required:</span></span>

- <span data-ttu-id="122a5-157">Симулятор должен уведомлять Центр Интернета вещей в предварительно настроенном решении, передавая сведения о методе.</span><span class="sxs-lookup"><span data-stu-id="122a5-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span></span>
- <span data-ttu-id="122a5-158">Симулятор должен содержать код для обработки вызова метода, запускаемого из панели **Сведения об устройстве** в обозревателе решений или с помощью задания.</span><span class="sxs-lookup"><span data-stu-id="122a5-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span></span>

<span data-ttu-id="122a5-159">Удаленный мониторинг предварительно настроенного решения использует *сообщаемые свойства* для передачи в Центр Интернета вещей подробных сведений о поддерживаемых методах.</span><span class="sxs-lookup"><span data-stu-id="122a5-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span></span> <span data-ttu-id="122a5-160">Серверная часть решения сохраняет список всех методов, поддерживаемых для каждого устройства, а также журнал вызовов этих методов.</span><span class="sxs-lookup"><span data-stu-id="122a5-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="122a5-161">Эти сведения об устройствах и вызовах методов можно посмотреть на портале решения.</span><span class="sxs-lookup"><span data-stu-id="122a5-161">You can view this information about devices and invoke methods in the solution portal.</span></span>

<span data-ttu-id="122a5-162">Чтобы уведомить Центр Интернета вещей о поддержке метода, устройство добавляет сведения о методе в узел **SupportedMethods** в сообщаемых свойствах:</span><span class="sxs-lookup"><span data-stu-id="122a5-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="122a5-163">Подпись метода имеет следующий формат: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="122a5-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="122a5-164">Например, если метод **InitiateFirmwareUpdate** ожидает строковый параметр с именем **FwPackageURI**, сообщить об этом можно с помощью такой подписи метода:</span><span class="sxs-lookup"><span data-stu-id="122a5-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="122a5-165">Список поддерживаемых типов параметров см. в описании класса **CommandTypes** в проекте инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="122a5-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span></span>

<span data-ttu-id="122a5-166">Чтобы удалить метод, установите в сообщаемых свойствах значение `null` для подписи метода.</span><span class="sxs-lookup"><span data-stu-id="122a5-166">To delete a method, set the method signature to `null` in the reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="122a5-167">Серверная часть решения обновляет сведения о поддерживаемых методах только при получении от устройства сообщений типа *сведения об устройстве*.</span><span class="sxs-lookup"><span data-stu-id="122a5-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span></span>

<span data-ttu-id="122a5-168">В следующем примере кода из класса **SampleDeviceFactory**, реализованного в проекте Common, демонстрируется добавление метода в список поддерживаемых методов **SupportedMethods** в сообщаемых свойствах, отправленных устройством:</span><span class="sxs-lookup"><span data-stu-id="122a5-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="122a5-169">Этот фрагмент кода добавляет сведения о методе **InitiateFirmwareUpdate**, в том числе текст, отображаемый на портале решения, и подробные сведения о параметрах метода.</span><span class="sxs-lookup"><span data-stu-id="122a5-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span></span>

<span data-ttu-id="122a5-170">При запуске симулятор отправляет сообщаемые свойства, включая список поддерживаемых методов, в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="122a5-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span></span>

<span data-ttu-id="122a5-171">Добавьте в симулятор обработчик для каждого поддерживаемого метода.</span><span class="sxs-lookup"><span data-stu-id="122a5-171">Add a handler to the simulator code for each method it supports.</span></span> <span data-ttu-id="122a5-172">Существующие обработчики можно увидеть в классе **CoolerDevice** в проекте Simulator.WebJob.</span><span class="sxs-lookup"><span data-stu-id="122a5-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span></span> <span data-ttu-id="122a5-173">В следующем примере представлен обработчик для метода **InitiateFirmwareUpdate**:</span><span class="sxs-lookup"><span data-stu-id="122a5-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span></span>

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

<span data-ttu-id="122a5-174">Имя для метода обработчика должно состоять из строки `On`, за которой следует имя метода.</span><span class="sxs-lookup"><span data-stu-id="122a5-174">Method handler names must start with `On` followed by the name of the method.</span></span> <span data-ttu-id="122a5-175">Параметр **methodRequest** содержит все параметры, передаваемые при вызове этого метода из серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="122a5-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span></span> <span data-ttu-id="122a5-176">Возвращаемое значение должно иметь тип **Task&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="122a5-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="122a5-177">Вспомогательный метод **BuildMethodResponse** служит для создания возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="122a5-177">The **BuildMethodResponse** utility method helps you create the return value.</span></span>

<span data-ttu-id="122a5-178">В методе обработчика можно выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="122a5-178">Inside the method handler, you could:</span></span>

- <span data-ttu-id="122a5-179">Запустить асинхронную задачу.</span><span class="sxs-lookup"><span data-stu-id="122a5-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="122a5-180">Получить требуемые свойства от *двойника устройства*, хранящегося в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="122a5-180">Retrieve desired properties from the *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="122a5-181">Обновить одно сообщаемое свойство с помощью метода **SetReportedPropertyAsync** из класса **CoolerDevice**.</span><span class="sxs-lookup"><span data-stu-id="122a5-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span></span>
- <span data-ttu-id="122a5-182">Обновить несколько сообщаемых свойств, создав экземпляр **TwinCollection** и вызвав для него метод **Transport.UpdateReportedPropertiesAsync**.</span><span class="sxs-lookup"><span data-stu-id="122a5-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="122a5-183">Предыдущий пример обновления микропрограммы выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="122a5-183">The preceding firmware update example performs the following steps:</span></span>

- <span data-ttu-id="122a5-184">Проверяет, что устройство способно принимать запрос на обновление микропрограммы.</span><span class="sxs-lookup"><span data-stu-id="122a5-184">Checks the device is able to accept the firmware update request.</span></span>
- <span data-ttu-id="122a5-185">Асинхронно запускает операцию обновления микропрограммы и сбрасывает данные телеметрии по завершении этой операции.</span><span class="sxs-lookup"><span data-stu-id="122a5-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span></span>
- <span data-ttu-id="122a5-186">Немедленно возвращает сообщение "Принято обновление микропрограммы", подтверждая получение запроса устройством.</span><span class="sxs-lookup"><span data-stu-id="122a5-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="122a5-187">Построение и использование собственного (физического) устройства</span><span class="sxs-lookup"><span data-stu-id="122a5-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="122a5-188">[Пакеты SDK для IoT Azure](https://github.com/Azure/azure-iot-sdks) предоставляют библиотеки для подключения различных типов устройств (языков и операционных систем) к решениям IoT.</span><span class="sxs-lookup"><span data-stu-id="122a5-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="122a5-189">Изменение ограничений панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="122a5-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="122a5-190">Количество устройств, отображаемых в раскрывающемся списке панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="122a5-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="122a5-191">Количество по умолчанию — 200.</span><span class="sxs-lookup"><span data-stu-id="122a5-191">The default is 200.</span></span> <span data-ttu-id="122a5-192">Это количество можно изменить в файле [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="122a5-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-to-display-in-bing-map-control"></a><span data-ttu-id="122a5-193">Количество маркеров, отображаемых в элементе управления карты Bing</span><span class="sxs-lookup"><span data-stu-id="122a5-193">Number of pins to display in Bing Map control</span></span>

<span data-ttu-id="122a5-194">Количество по умолчанию — 200.</span><span class="sxs-lookup"><span data-stu-id="122a5-194">The default is 200.</span></span> <span data-ttu-id="122a5-195">Это количество можно изменить в файле [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="122a5-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="122a5-196">Период времени графика телеметрии</span><span class="sxs-lookup"><span data-stu-id="122a5-196">Time period of telemetry graph</span></span>

<span data-ttu-id="122a5-197">Значение по умолчанию — 10 минут.</span><span class="sxs-lookup"><span data-stu-id="122a5-197">The default is 10 minutes.</span></span> <span data-ttu-id="122a5-198">Это значение можно изменить в файле [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="122a5-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="122a5-199">Настройка ролей приложений вручную</span><span class="sxs-lookup"><span data-stu-id="122a5-199">Manually set up application roles</span></span>

<span data-ttu-id="122a5-200">В следующей процедуре описывается, как добавлять роли приложения **Admin** и **ReadOnly** в предварительно настроенное решение.</span><span class="sxs-lookup"><span data-stu-id="122a5-200">The following procedure describes how to add **Admin** and **ReadOnly** application roles to a preconfigured solution.</span></span> <span data-ttu-id="122a5-201">Обратите внимание, что такие решения, подготовленные на сайте azureiotsuite.com, уже включают роли **Admin** и **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="122a5-201">Note that preconfigured solutions provisioned from the azureiotsuite.com site already include the **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="122a5-202">Члены роли **ReadOnly** могут просматривать панель мониторинга и список устройств, но им не разрешено добавлять устройства, изменять атрибуты устройств и отправлять команды.</span><span class="sxs-lookup"><span data-stu-id="122a5-202">Members of the **ReadOnly** role can see the dashboard and the device list, but are not allowed to add devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="122a5-203">Члены роли **Admin** имеют полный доступ ко всем функциям в решении.</span><span class="sxs-lookup"><span data-stu-id="122a5-203">Members of the **Admin** role have full access to all the functionality in the solution.</span></span>

1. <span data-ttu-id="122a5-204">Войдите на [классический портал Azure][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="122a5-204">Go to the [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="122a5-205">Выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="122a5-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="122a5-206">Щелкните имя клиента AAD, который вы использовали при подготовке решения.</span><span class="sxs-lookup"><span data-stu-id="122a5-206">Click the name of the AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="122a5-207">Щелкните **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="122a5-207">Click **Applications**.</span></span>
5. <span data-ttu-id="122a5-208">Щелкните имя приложения, совпадающее с именем предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="122a5-208">Click the name of the application that matches your preconfigured solution name.</span></span> <span data-ttu-id="122a5-209">Если приложение отсутствует в списке, выберите в раскрывающемся списке **Показать** пункт **Приложения, которыми владеет моя компания** и установите флажок.</span><span class="sxs-lookup"><span data-stu-id="122a5-209">If you don't see your application in the list, select **Applications my company owns** in the **Show** dropdown and click the check mark.</span></span>
6. <span data-ttu-id="122a5-210">Внизу страницы щелкните **Управление манифестом**, а затем — **Скачать манифест**.</span><span class="sxs-lookup"><span data-stu-id="122a5-210">At the bottom of the page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="122a5-211">Эта процедура загружает JSON-файл на ваш локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="122a5-211">This procedure downloads a .json file to your local machine.</span></span> <span data-ttu-id="122a5-212">Откройте этот файл для редактирования в любом текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="122a5-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="122a5-213">В третьей строке JSON-файла вы можете видеть следующее:</span><span class="sxs-lookup"><span data-stu-id="122a5-213">On the third line of the .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="122a5-214">Замените эту строку следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="122a5-214">Replace this line with the following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access to the application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access to device information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="122a5-215">Сохраните обновленный JSON-файл (можно перезаписать существующий файл).</span><span class="sxs-lookup"><span data-stu-id="122a5-215">Save the updated .json file (you can overwrite the existing file).</span></span>
10. <span data-ttu-id="122a5-216">На классическом портале Azure внизу страницы выберите **Управление манифестом**, а затем — **Отправить манифест**, чтобы отправить JSON-файл, сохраненный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="122a5-216">In the Azure classic portal, at the bottom of the page, select **Manage Manifest** then **Upload Manifest** to upload the .json file you saved in the previous step.</span></span>
11. <span data-ttu-id="122a5-217">Теперь вы добавили роли **Admin** и **ReadOnly** в свое приложение.</span><span class="sxs-lookup"><span data-stu-id="122a5-217">You have now added the **Admin** and **ReadOnly** roles to your application.</span></span>
12. <span data-ttu-id="122a5-218">Чтобы назначить одну из этих ролей пользователю в каталоге, ознакомьтесь со статьей [Разрешения на сайте azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="122a5-218">To assign one of these roles to a user in your directory, see [Permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="122a5-219">Отзыв</span><span class="sxs-lookup"><span data-stu-id="122a5-219">Feedback</span></span>

<span data-ttu-id="122a5-220">У вас есть предложение по настройке, которое не описано в этом документе?</span><span class="sxs-lookup"><span data-stu-id="122a5-220">Do you have a customization you'd like to see covered in this document?</span></span> <span data-ttu-id="122a5-221">Оставьте его на сайте [User Voice](https://feedback.azure.com/forums/321918-azure-iot) или в комментариях к этой статье.</span><span class="sxs-lookup"><span data-stu-id="122a5-221">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="122a5-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="122a5-222">Next steps</span></span>

<span data-ttu-id="122a5-223">Дополнительные сведения о настройке решений с предварительно заданными параметрами см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="122a5-223">To learn more about the options for customizing the preconfigured solutions, see:</span></span>

* <span data-ttu-id="122a5-224">[Руководство. Подключение приложения логики к предварительно настроенному решению для удаленного мониторинга Azure IoT Suite][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="122a5-224">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="122a5-225">[Использование динамической телеметрии с предварительно настроенным решением для удаленного мониторинга][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="122a5-225">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="122a5-226">[Метаданные сведений об устройстве в предварительно настроенном решении для удаленного мониторинга][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="122a5-226">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="122a5-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize] (Настройка отображения данных серверов OPC UA решением подключенной фабрики)</span><span class="sxs-lookup"><span data-stu-id="122a5-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md