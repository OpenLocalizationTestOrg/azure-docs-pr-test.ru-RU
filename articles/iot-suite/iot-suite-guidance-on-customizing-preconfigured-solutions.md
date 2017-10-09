---
title: "aaaCustomizing предварительно настроенных решений | Документы Microsoft"
description: "Содержатся сведения о том, как toocustomize hello Azure IoT Suite предварительно настроенных решений."
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
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="34a20-103">Настройка предварительно настроенного решения</span><span class="sxs-lookup"><span data-stu-id="34a20-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="34a20-104">Hello предварительно настроенных решений, в состав hello Azure IoT Suite Демонстрация служб hello в hello suite рабочий вместе toodeliver решения начала до конца.</span><span class="sxs-lookup"><span data-stu-id="34a20-104">hello preconfigured solutions provided with hello Azure IoT Suite demonstrate hello services within hello suite working together toodeliver an end-to-end solution.</span></span> <span data-ttu-id="34a20-105">Из этой точки отсчета существуют в различных местах, в которых можно расширять и настраивать hello решения для конкретных сценариев.</span><span class="sxs-lookup"><span data-stu-id="34a20-105">From this starting point, there are various places in which you can extend and customize hello solution for specific scenarios.</span></span> <span data-ttu-id="34a20-106">Привет, в следующих разделах описаны эти общие настройки точки.</span><span class="sxs-lookup"><span data-stu-id="34a20-106">hello following sections describe these common customization points.</span></span>

## <a name="find-hello-source-code"></a><span data-ttu-id="34a20-107">Поиск исходного кода hello</span><span class="sxs-lookup"><span data-stu-id="34a20-107">Find hello source code</span></span>

<span data-ttu-id="34a20-108">Hello исходного кода для hello предварительно настроенных решений можно найти в GitHub в следующих репозиториев hello:</span><span class="sxs-lookup"><span data-stu-id="34a20-108">hello source code for hello preconfigured solutions is available on GitHub in hello following repositories:</span></span>

* <span data-ttu-id="34a20-109">Удаленный мониторинг: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="34a20-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="34a20-110">Прогнозируемое обслуживание: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="34a20-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="34a20-111">Подключенная фабрика: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="34a20-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="34a20-112">toodemonstrate hello шаблоны и методики используемым функциям конца в конец hello tooimplement IoT решения с помощью набора IoT Azure предоставляется Hello исходного кода для hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="34a20-112">hello source code for hello preconfigured solutions is provided toodemonstrate hello patterns and practices used tooimplement hello end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="34a20-113">Дополнительные сведения о том, как можно найти toobuild и развертывание решений hello в репозиториях GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-113">You can find more information about how toobuild and deploy hello solutions in hello GitHub repositories.</span></span>

## <a name="change-hello-preconfigured-rules"></a><span data-ttu-id="34a20-114">Изменение hello предварительно настроенных правил</span><span class="sxs-lookup"><span data-stu-id="34a20-114">Change hello preconfigured rules</span></span>

<span data-ttu-id="34a20-115">Hello удаленного мониторинга решение включает в себя три [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) задания сведений об устройстве toohandle, телеметрии и логики правил в решении hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-115">hello remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs toohandle device information, telemetry, and rules logic in hello solution.</span></span>

<span data-ttu-id="34a20-116">Hello три потока analytics заданий и их синтаксиса описаны в глубину в hello [удаленный мониторинг заранее настроенные Пошаговое руководство по решениям](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="34a20-116">hello three stream analytics jobs and their syntax are described in depth in hello [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="34a20-117">Эти задания можно изменить напрямую tooalter hello логики или добавьте логику tooyour конкретного сценария.</span><span class="sxs-lookup"><span data-stu-id="34a20-117">You can edit these jobs directly tooalter hello logic, or add logic specific tooyour scenario.</span></span> <span data-ttu-id="34a20-118">Можно найти hello заданий Stream Analytics следующим образом:</span><span class="sxs-lookup"><span data-stu-id="34a20-118">You can find hello Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="34a20-119">Go слишком[портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="34a20-119">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="34a20-120">Перейдите в группу ресурсов toohello hello точно такое же имя в качестве вашего решения IoT.</span><span class="sxs-lookup"><span data-stu-id="34a20-120">Navigate toohello resource group with hello same name as your IoT solution.</span></span> 
3. <span data-ttu-id="34a20-121">Выберите задание Azure Stream Analytics hello хотелось бы toomodify.</span><span class="sxs-lookup"><span data-stu-id="34a20-121">Select hello Azure Stream Analytics job you'd like toomodify.</span></span> 
4. <span data-ttu-id="34a20-122">Остановка задания hello, выбрав **остановить** hello набора команд.</span><span class="sxs-lookup"><span data-stu-id="34a20-122">Stop hello job by selecting **Stop** in hello set of commands.</span></span> 
5. <span data-ttu-id="34a20-123">Измените входные данные hello, запрос и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="34a20-123">Edit hello inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="34a20-124">Простое изменение — запрос hello toochange для hello **правила** toouse задания **«<»** вместо **» > «**.</span><span class="sxs-lookup"><span data-stu-id="34a20-124">A simple modification is toochange hello query for hello **Rules** job toouse a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="34a20-125">портал Hello решение по-прежнему показывает **» > «** при изменении правил, но Обратите внимание на то, как поведение hello отражается из-за изменения toohello hello базового задания.</span><span class="sxs-lookup"><span data-stu-id="34a20-125">hello solution portal still shows **">"** when you edit a rule, but notice how hello behavior is flipped due toohello change in hello underlying job.</span></span>
6. <span data-ttu-id="34a20-126">Запустить задание hello</span><span class="sxs-lookup"><span data-stu-id="34a20-126">Start hello job</span></span>

> [!NOTE]
> <span data-ttu-id="34a20-127">Hello удаленного мониторинга зависит от конкретных данных, поэтому изменение hello задания может привести к toofail hello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="34a20-127">hello remote monitoring dashboard depends on specific data, so altering hello jobs can cause hello dashboard toofail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="34a20-128">Добавление собственных правил</span><span class="sxs-lookup"><span data-stu-id="34a20-128">Add your own rules</span></span>

<span data-ttu-id="34a20-129">В дополнение к этому toochanging hello заранее настроенные задания Azure Stream Analytics, можно использовать новые задания hello Azure портала tooadd или добавлять новые задания tooexisting запросов.</span><span class="sxs-lookup"><span data-stu-id="34a20-129">In addition toochanging hello preconfigured Azure Stream Analytics jobs, you can use hello Azure portal tooadd new jobs or add new queries tooexisting jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="34a20-130">Настройка устройств</span><span class="sxs-lookup"><span data-stu-id="34a20-130">Customize devices</span></span>

<span data-ttu-id="34a20-131">Одним из наиболее распространенных действий расширения hello работает со сценарием tooyour конкретного устройства.</span><span class="sxs-lookup"><span data-stu-id="34a20-131">One of hello most common extension activities is working with devices specific tooyour scenario.</span></span> <span data-ttu-id="34a20-132">Существует несколько способов работы с устройствами.</span><span class="sxs-lookup"><span data-stu-id="34a20-132">There are several methods for working with devices.</span></span> <span data-ttu-id="34a20-133">Это может быть изменение сценария toomatch имитированное устройство или с помощью hello [SDK устройств IoT] [ IoT Device SDK] tooconnect toohello решения физического устройства.</span><span class="sxs-lookup"><span data-stu-id="34a20-133">These methods include altering a simulated device toomatch your scenario, or using hello [IoT Device SDK][IoT Device SDK] tooconnect your physical device toohello solution.</span></span>

<span data-ttu-id="34a20-134">Пошаговое руководство по tooadding устройств, в разделе hello [Iot Suite подключение устройств](iot-suite-connecting-devices.md) статьи и hello [удаленного мониторинга образца пакета SDK C](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="34a20-134">For a step-by-step guide tooadding devices, see hello [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and hello [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="34a20-135">Этот образец является спроектированный toowork с hello удаленное наблюдение предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="34a20-135">This sample is designed toowork with hello remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="34a20-136">Создание собственного виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="34a20-136">Create your own simulated device</span></span>

<span data-ttu-id="34a20-137">Включенные в hello [удаленное наблюдение исходного кода решения](https://github.com/Azure/azure-iot-remote-monitoring), является симулятор .NET.</span><span class="sxs-lookup"><span data-stu-id="34a20-137">Included in hello [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="34a20-138">Это симулятор является hello один подготовить как часть решения hello и можно изменить его toosend различные метаданные, телеметрии и реагирования на команды toodifferent и методы.</span><span class="sxs-lookup"><span data-stu-id="34a20-138">This simulator is hello one provisioned as part of hello solution and you can alter it toosend different metadata, telemetry, and respond toodifferent commands and methods.</span></span>

<span data-ttu-id="34a20-139">предварительно настроенный симулятор Hello в удаленное наблюдение предварительно настроенных решений hello имитирует охлаждающего устройства, которое выдает температуры и влажности телеметрии.</span><span class="sxs-lookup"><span data-stu-id="34a20-139">hello preconfigured simulator in hello remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="34a20-140">Вы можете изменить симулятор hello в hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) проекта при разделенными репозитории GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-140">You can modify hello simulator in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked hello GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="34a20-141">Доступные расположения для виртуальных устройств</span><span class="sxs-lookup"><span data-stu-id="34a20-141">Available locations for simulated devices</span></span>

<span data-ttu-id="34a20-142">набор по умолчанию Hello расположения — Сиэтл и Редмонд, штат Вашингтон, США.</span><span class="sxs-lookup"><span data-stu-id="34a20-142">hello default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="34a20-143">Эти расположения можно изменить в файле [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="34a20-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a><span data-ttu-id="34a20-144">Добавьте обработчик toohello нужного свойства обновления симулятора</span><span class="sxs-lookup"><span data-stu-id="34a20-144">Add a desired property update handler toohello simulator</span></span>

<span data-ttu-id="34a20-145">Можно задать значение для нужного свойства для устройства на портале решения hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-145">You can set a value for a desired property for a device in hello solution portal.</span></span> <span data-ttu-id="34a20-146">Ответственность hello запроса на изменение hello устройства toohandle hello свойство состоит в том случае, когда устройство hello извлекает значение свойства hello требуемого.</span><span class="sxs-lookup"><span data-stu-id="34a20-146">It is hello responsibility of hello device toohandle hello property change request when hello device retrieves hello desired property value.</span></span> <span data-ttu-id="34a20-147">Поддержка tooadd для изменения значения свойства через нужное свойство, необходимо tooadd симулятора toohello обработчика.</span><span class="sxs-lookup"><span data-stu-id="34a20-147">tooadd support for a property value change through a desired property, you need tooadd a handler toohello simulator.</span></span>

<span data-ttu-id="34a20-148">Имитатор Hello содержит обработчики для hello **SetPointTemp** и **TelemetryInterval** свойства, которые можно обновить, установив требуемого значения hello решение портала.</span><span class="sxs-lookup"><span data-stu-id="34a20-148">hello simulator contains handlers for hello **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in hello solution portal.</span></span>

<span data-ttu-id="34a20-149">Hello примере показан обработчик hello hello **SetPointTemp** требуемого свойства в hello **CoolerDevice** класса:</span><span class="sxs-lookup"><span data-stu-id="34a20-149">hello following example shows hello handler for hello **SetPointTemp** desired property in hello **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="34a20-150">Этот метод обновляет точки данных телеметрии hello температуры, а затем отчеты hello изменить задней tooIoT концентратора, задав свойство отчета.</span><span class="sxs-lookup"><span data-stu-id="34a20-150">This method updates hello telemetry point temperature and then reports hello change back tooIoT Hub by setting a reported property.</span></span>

<span data-ttu-id="34a20-151">Можно добавить собственные обработчики для собственные свойства по следующему шаблону hello в предшествующих пример hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-151">You can add your own handlers for your own properties by following hello pattern in hello preceding example.</span></span>

<span data-ttu-id="34a20-152">Необходимо также привязать обработчик toohello hello нужное свойство, как показано в следующий пример из hello hello **CoolerDevice** конструктор:</span><span class="sxs-lookup"><span data-stu-id="34a20-152">You must also bind hello desired property toohello handler as shown in hello following example from hello **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="34a20-153">Обратите внимание, что **SetPointTempPropertyName** — это константа, определенная как Config.SetPointTemp.</span><span class="sxs-lookup"><span data-stu-id="34a20-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-toohello-simulator"></a><span data-ttu-id="34a20-154">Добавить поддержку нового симулятор toohello метод</span><span class="sxs-lookup"><span data-stu-id="34a20-154">Add support for a new method toohello simulator</span></span>

<span data-ttu-id="34a20-155">Вы можете настроить hello симулятор tooadd поддержка новый [(прямой) метод][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="34a20-155">You can customize hello simulator tooadd support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="34a20-156">Нужно выполнить два основных действия.</span><span class="sxs-lookup"><span data-stu-id="34a20-156">There are two key steps required:</span></span>

- <span data-ttu-id="34a20-157">Имитатор Hello необходимо уведомить центра IoT hello в решении hello предварительно настроен с данные метода hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-157">hello simulator must notify hello IoT hub in hello preconfigured solution with details of hello method.</span></span>
- <span data-ttu-id="34a20-158">Имитатор Hello должен включать вызов метода hello toohandle кода, при вызове из hello **сведений об устройстве** панель в обозревателе решений hello или с помощью задания.</span><span class="sxs-lookup"><span data-stu-id="34a20-158">hello simulator must include code toohandle hello method call when you invoke it from hello **Device details** panel in hello solution explorer or through a job.</span></span>

<span data-ttu-id="34a20-159">Hello удаленный мониторинг предварительно настроенное решение использует *сообщил свойства* toosend подробные сведения о поддерживаемых методах tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="34a20-159">hello remote monitoring preconfigured solution uses *reported properties* toosend details of supported methods tooIoT hub.</span></span> <span data-ttu-id="34a20-160">серверной части решения Hello поддерживает список всех методов hello, поддерживаемые для каждого устройства, а также журнал вызовов методов.</span><span class="sxs-lookup"><span data-stu-id="34a20-160">hello solution back end maintains a list of all hello methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="34a20-161">Можно просмотреть эти сведения об устройствах и вызывать методы в портал hello решения.</span><span class="sxs-lookup"><span data-stu-id="34a20-161">You can view this information about devices and invoke methods in hello solution portal.</span></span>

<span data-ttu-id="34a20-162">Центр IoT hello toonotify, устройство поддерживает метод, hello устройства необходимо добавить сведения о hello метод toohello **SupportedMethods** узел в hello сообщил свойства:</span><span class="sxs-lookup"><span data-stu-id="34a20-162">toonotify hello IoT hub that a device supports a method, hello device must add details of hello method toohello **SupportedMethods** node in hello reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="34a20-163">Hello сигнатура метода имеет следующий формат hello: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="34a20-163">hello method signature has hello following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="34a20-164">Например, hello toospecify **InitiateFirmwareUpdate** методе ожидается строковый параметр с именем **FwPackageURI**, использовать hello, следуя сигнатуру метода:</span><span class="sxs-lookup"><span data-stu-id="34a20-164">For example, toospecify hello **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use hello following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="34a20-165">Список поддерживаемых типов параметров см. в разделе hello **CommandTypes** класса в проекте инфраструктуры hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-165">For a list of supported parameter types, see hello **CommandTypes** class in hello Infrastructure project.</span></span>

<span data-ttu-id="34a20-166">метод toodelete задать подпись метода hello слишком`null` включается в hello свойства.</span><span class="sxs-lookup"><span data-stu-id="34a20-166">toodelete a method, set hello method signature too`null` in hello reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="34a20-167">Hello серверной части решения обновляет только сведения о поддерживаемых методах при получении *сведений об устройстве* сообщение hello устройства.</span><span class="sxs-lookup"><span data-stu-id="34a20-167">hello solution back end only updates information about supported methods when it receives a *device information* message from hello device.</span></span>

<span data-ttu-id="34a20-168">Следующий образец кода из hello Hello **SampleDeviceFactory** класса в hello общего проекта показано, как tooadd список toohello метод из **SupportedMethods** включается в hello свойства отправленных hello устройство:</span><span class="sxs-lookup"><span data-stu-id="34a20-168">hello following code sample from hello **SampleDeviceFactory** class in hello Common project shows how tooadd a method toohello list of **SupportedMethods** in hello reported properties sent by hello device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="34a20-169">Этот фрагмент кода добавляет сведения о hello **InitiateFirmwareUpdate** метода, включая текст toodisplay портале решения hello и подробные сведения о hello необходимые параметры метода.</span><span class="sxs-lookup"><span data-stu-id="34a20-169">This code snippet adds details of hello **InitiateFirmwareUpdate** method including text toodisplay in hello solution portal and details of hello required method parameters.</span></span>

<span data-ttu-id="34a20-170">Имитатор Hello отправляет выводятся свойства, включая hello список поддерживаемых методов tooIoT концентратора при запуске симулятор hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-170">hello simulator sends reported properties, including hello list of supported methods, tooIoT Hub when hello simulator starts.</span></span>

<span data-ttu-id="34a20-171">Добавьте код обработчика toohello имитатор для каждого метода, который он поддерживает.</span><span class="sxs-lookup"><span data-stu-id="34a20-171">Add a handler toohello simulator code for each method it supports.</span></span> <span data-ttu-id="34a20-172">Вы увидите hello существующих обработчиков в hello **CoolerDevice** класса в проекте Simulator.WebJob hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-172">You can see hello existing handlers in hello **CoolerDevice** class in hello Simulator.WebJob project.</span></span> <span data-ttu-id="34a20-173">Hello примере показан обработчик hello **InitiateFirmwareUpdate** метод:</span><span class="sxs-lookup"><span data-stu-id="34a20-173">hello following example shows hello handler for **InitiateFirmwareUpdate** method:</span></span>

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

<span data-ttu-id="34a20-174">Метод обработчика имена должны начинаться с `On` следуют hello имя метода hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-174">Method handler names must start with `On` followed by hello name of hello method.</span></span> <span data-ttu-id="34a20-175">Hello **methodRequest** параметр содержит все передаваемые с помощью вызова метода hello из серверной части решения hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-175">hello **methodRequest** parameter contains any parameters passed with hello method invocation from hello solution back end.</span></span> <span data-ttu-id="34a20-176">Hello возвращаемое значение должно быть типа **задачи&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="34a20-176">hello return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="34a20-177">Hello **BuildMethodResponse** вспомогательный метод служит для создания hello возвращаемое значение.</span><span class="sxs-lookup"><span data-stu-id="34a20-177">hello **BuildMethodResponse** utility method helps you create hello return value.</span></span>

<span data-ttu-id="34a20-178">В обработчике метод hello можно выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="34a20-178">Inside hello method handler, you could:</span></span>

- <span data-ttu-id="34a20-179">Запустить асинхронную задачу.</span><span class="sxs-lookup"><span data-stu-id="34a20-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="34a20-180">Загрузить нужные свойства из hello *двойных устройства* в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="34a20-180">Retrieve desired properties from hello *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="34a20-181">Обновления одного свойства отчета с помощью hello **SetReportedPropertyAsync** метод в hello **CoolerDevice** класса.</span><span class="sxs-lookup"><span data-stu-id="34a20-181">Update a single reported property using hello **SetReportedPropertyAsync** method in hello **CoolerDevice** class.</span></span>
- <span data-ttu-id="34a20-182">Обновить несколько свойств отчета, создав **TwinCollection** экземпляра и вызова hello **Transport.UpdateReportedPropertiesAsync** метод.</span><span class="sxs-lookup"><span data-stu-id="34a20-182">Update multiple reported properties by creating a **TwinCollection** instance and calling hello **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="34a20-183">Hello предыдущий пример обновления встроенного по выполняет следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-183">hello preceding firmware update example performs hello following steps:</span></span>

- <span data-ttu-id="34a20-184">Проверяет hello устройство является запрос на обновление встроенного по может tooaccept hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-184">Checks hello device is able tooaccept hello firmware update request.</span></span>
- <span data-ttu-id="34a20-185">Асинхронно запускает операцию обновления встроенного по hello и сбрасывает данные телеметрии hello после завершения операции hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-185">Asynchronously initiates hello firmware update operation and resets hello telemetry when hello operation is complete.</span></span>
- <span data-ttu-id="34a20-186">Сразу же возвращает Здравствуйте «FirmwareUpdate принято» сообщения tooindicate hello запрос принят устройством hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-186">Immediately returns hello "FirmwareUpdate accepted" message tooindicate hello request was accepted by hello device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="34a20-187">Построение и использование собственного (физического) устройства</span><span class="sxs-lookup"><span data-stu-id="34a20-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="34a20-188">Hello [пакеты SDK Azure IoT](https://github.com/Azure/azure-iot-sdks) предоставляют библиотеки для подключения различных типов устройств (языков и операционных систем) в решения IoT.</span><span class="sxs-lookup"><span data-stu-id="34a20-188">hello [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="34a20-189">Изменение ограничений панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="34a20-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="34a20-190">Количество устройств, отображаемых в раскрывающемся списке панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="34a20-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="34a20-191">по умолчанию Hello — 200.</span><span class="sxs-lookup"><span data-stu-id="34a20-191">hello default is 200.</span></span> <span data-ttu-id="34a20-192">Это количество можно изменить в файле [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="34a20-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a><span data-ttu-id="34a20-193">Количество toodisplay ПИН-кодов в элементе управления карты Bing</span><span class="sxs-lookup"><span data-stu-id="34a20-193">Number of pins toodisplay in Bing Map control</span></span>

<span data-ttu-id="34a20-194">по умолчанию Hello — 200.</span><span class="sxs-lookup"><span data-stu-id="34a20-194">hello default is 200.</span></span> <span data-ttu-id="34a20-195">Это количество можно изменить в файле [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="34a20-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="34a20-196">Период времени графика телеметрии</span><span class="sxs-lookup"><span data-stu-id="34a20-196">Time period of telemetry graph</span></span>

<span data-ttu-id="34a20-197">по умолчанию Hello — 10 минут.</span><span class="sxs-lookup"><span data-stu-id="34a20-197">hello default is 10 minutes.</span></span> <span data-ttu-id="34a20-198">Это значение можно изменить в файле [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="34a20-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="34a20-199">Настройка ролей приложений вручную</span><span class="sxs-lookup"><span data-stu-id="34a20-199">Manually set up application roles</span></span>

<span data-ttu-id="34a20-200">Hello ниже описано, как tooadd **администратора** и **ReadOnly** tooa ролей приложения предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="34a20-200">hello following procedure describes how tooadd **Admin** and **ReadOnly** application roles tooa preconfigured solution.</span></span> <span data-ttu-id="34a20-201">Обратите внимание, что предварительно настроенных решений, которые уже подготовлены с сайта azureiotsuite.com hello включает hello **администратора** и **ReadOnly** ролей.</span><span class="sxs-lookup"><span data-stu-id="34a20-201">Note that preconfigured solutions provisioned from hello azureiotsuite.com site already include hello **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="34a20-202">Члены hello **ReadOnly** роли можно увидеть панели мониторинга hello и hello список устройств, но не допускаются tooadd устройств, изменение атрибутов устройства или команд отправки.</span><span class="sxs-lookup"><span data-stu-id="34a20-202">Members of hello **ReadOnly** role can see hello dashboard and hello device list, but are not allowed tooadd devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="34a20-203">Члены hello **администратора** роль имеет полный доступ tooall hello функциональность в решении hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-203">Members of hello **Admin** role have full access tooall hello functionality in hello solution.</span></span>

1. <span data-ttu-id="34a20-204">Go toohello [классический портал Azure][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="34a20-204">Go toohello [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="34a20-205">Выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="34a20-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="34a20-206">Щелкните имя hello клиента AAD hello, которая использовалась при подготовке решения.</span><span class="sxs-lookup"><span data-stu-id="34a20-206">Click hello name of hello AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="34a20-207">Щелкните **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="34a20-207">Click **Applications**.</span></span>
5. <span data-ttu-id="34a20-208">Щелкните имя приложения hello, совпадающим с именем предварительно настроенных решений hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-208">Click hello name of hello application that matches your preconfigured solution name.</span></span> <span data-ttu-id="34a20-209">Если вы не видите в списке hello приложения, выберите **приложений, которыми владеет Моя компания** в hello **Показать** раскрывающегося списка и нажмите кнопку hello флажок.</span><span class="sxs-lookup"><span data-stu-id="34a20-209">If you don't see your application in hello list, select **Applications my company owns** in hello **Show** dropdown and click hello check mark.</span></span>
6. <span data-ttu-id="34a20-210">Внизу hello страницы приветствия щелкните **управление манифеста** и затем **загрузки манифеста**.</span><span class="sxs-lookup"><span data-stu-id="34a20-210">At hello bottom of hello page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="34a20-211">Эта процедура загружает файл .json tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="34a20-211">This procedure downloads a .json file tooyour local machine.</span></span> <span data-ttu-id="34a20-212">Откройте этот файл для редактирования в любом текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="34a20-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="34a20-213">В hello третья строка hello JSON-файл можно увидеть:</span><span class="sxs-lookup"><span data-stu-id="34a20-213">On hello third line of hello .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="34a20-214">Замените эту строку hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="34a20-214">Replace this line with hello following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="34a20-215">Сохраните Обновленный JSON-файл hello (можно перезаписать существующий файл hello).</span><span class="sxs-lookup"><span data-stu-id="34a20-215">Save hello updated .json file (you can overwrite hello existing file).</span></span>
10. <span data-ttu-id="34a20-216">В hello классический портал Azure, hello нижней части страницы приветствия выберите **управление манифеста** затем **отправить манифест** tooupload hello JSON-файл был сохранен на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="34a20-216">In hello Azure classic portal, at hello bottom of hello page, select **Manage Manifest** then **Upload Manifest** tooupload hello .json file you saved in hello previous step.</span></span>
11. <span data-ttu-id="34a20-217">Теперь вы добавили hello **администратора** и **ReadOnly** ролей tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="34a20-217">You have now added hello **Admin** and **ReadOnly** roles tooyour application.</span></span>
12. <span data-ttu-id="34a20-218">tooassign один пользователь tooa эти роли в каталоге, в разделе [разрешения на сайт hello azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="34a20-218">tooassign one of these roles tooa user in your directory, see [Permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="34a20-219">Отзыв</span><span class="sxs-lookup"><span data-stu-id="34a20-219">Feedback</span></span>

<span data-ttu-id="34a20-220">У вас есть настройки хотелось бы toosee, рассматриваемые в данном документе?</span><span class="sxs-lookup"><span data-stu-id="34a20-220">Do you have a customization you'd like toosee covered in this document?</span></span> <span data-ttu-id="34a20-221">Добавление предложения функция слишком[User Voice](https://feedback.azure.com/forums/321918-azure-iot), или оставьте комментарий для этой статьи.</span><span class="sxs-lookup"><span data-stu-id="34a20-221">Add feature suggestions too[User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="34a20-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="34a20-222">Next steps</span></span>

<span data-ttu-id="34a20-223">toolearn Дополнительные сведения о hello варианты настройки hello предварительно настроенных решений, см.:</span><span class="sxs-lookup"><span data-stu-id="34a20-223">toolearn more about hello options for customizing hello preconfigured solutions, see:</span></span>

* <span data-ttu-id="34a20-224">[Подключение приложения логики tooyour IoT Suite удаленного мониторинга Azure предварительно настроенных решения][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="34a20-224">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="34a20-225">[Используйте динамические данные телеметрии с hello удаленное наблюдение предварительно настроенных решений][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="34a20-225">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="34a20-226">[Устройство сведения метаданных в удаленное наблюдение предварительно настроенных решений hello][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="34a20-226">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="34a20-227">[Настроить способ hello подключения фабрики решений отображает данные с серверов OPC UA][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="34a20-227">[Customize how hello connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

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