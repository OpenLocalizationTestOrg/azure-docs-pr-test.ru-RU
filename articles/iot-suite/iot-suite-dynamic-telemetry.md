---
title: "динамические данные телеметрии aaaUse | Документы Microsoft"
description: "Выполните этот учебник toolearn как toouse динамические данные телеметрии с удаленного мониторинга hello Azure IoT Suite предварительно настроенных решений."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="e0583-103">Используйте динамические данные телеметрии с hello удаленное наблюдение предварительно настроенных решений</span><span class="sxs-lookup"><span data-stu-id="e0583-103">Use dynamic telemetry with hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="e0583-104">Динамические данные телеметрии позволяет вы toovisualize все отправленные данные телеметрии toohello удаленное наблюдение предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="e0583-104">Dynamic telemetry enables you toovisualize any telemetry sent toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="e0583-105">Hello имитируемые устройства, развертываемые hello предварительно настроенное решение отправляют температуры и влажности для телеметрии, то можно отобразить на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="e0583-105">hello simulated devices that deploy with hello preconfigured solution send temperature and humidity telemetry, which you can visualize on hello dashboard.</span></span> <span data-ttu-id="e0583-106">При настройке существующих устройств, имитация создания новых устройств, имитация или физических устройств toohello предварительно настроенных решений можно отправить другим значениям телеметрии, например hello температура, RPM или windspeed подключения.</span><span class="sxs-lookup"><span data-stu-id="e0583-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices toohello preconfigured solution you can send other telemetry values such as hello external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="e0583-107">Затем можно отобразить дополнительные данные телеметрии на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="e0583-107">You can then visualize this additional telemetry on hello dashboard.</span></span>

<span data-ttu-id="e0583-108">В этом учебнике используется простой Node.js имитированное устройство, можно легко изменить tooexperiment с динамической телеметрии.</span><span class="sxs-lookup"><span data-stu-id="e0583-108">This tutorial uses a simple Node.js simulated device that you can easily modify tooexperiment with dynamic telemetry.</span></span>

<span data-ttu-id="e0583-109">toocomplete этого учебника вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e0583-109">toocomplete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="e0583-110">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="e0583-110">An active Azure subscription.</span></span> <span data-ttu-id="e0583-111">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e0583-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e0583-112">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="e0583-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="e0583-113">[Node.js][lnk-node] версии 0.12.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e0583-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="e0583-114">Этот учебник подходит для любой операционной системы, например Windows или Linux, в которой можно установить Node.js.</span><span class="sxs-lookup"><span data-stu-id="e0583-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="e0583-115">Добавление типа данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="e0583-115">Add a telemetry type</span></span>

<span data-ttu-id="e0583-116">Hello следующим шагом является tooreplace hello телеметрии, созданные hello Node.js имитированное устройство с новым набором значений:</span><span class="sxs-lookup"><span data-stu-id="e0583-116">hello next step is tooreplace hello telemetry generated by hello Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="e0583-117">Остановка hello Node.js имитированное устройство, введя **Ctrl + C** в командной строке или оболочки.</span><span class="sxs-lookup"><span data-stu-id="e0583-117">Stop hello Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="e0583-118">В файле remote_monitoring.js hello вы увидите hello основные значения данных для существующих температуры hello, влажность и температура телеметрии.</span><span class="sxs-lookup"><span data-stu-id="e0583-118">In hello remote_monitoring.js file, you can see hello base data values for hello existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="e0583-119">Добавьте базовое значение данных для **rpm** следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e0583-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="e0583-120">Hello Node.js имитированное устройство использует hello **generateRandomIncrement** функционировать в hello remote_monitoring.js файл tooadd toohello случайных приращения основные значения данных.</span><span class="sxs-lookup"><span data-stu-id="e0583-120">hello Node.js simulated device uses hello **generateRandomIncrement** function in hello remote_monitoring.js file tooadd a random increment toohello base data values.</span></span> <span data-ttu-id="e0583-121">Случайный выбор hello **rpm** значение, добавив строку кода после существующего метода рандомизации hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e0583-121">Randomize hello **rpm** value by adding a line of code after hello existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="e0583-122">Добавьте hello новый rpm значение toohello JSON полезных данных hello устройство отправляет tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="e0583-122">Add hello new rpm value toohello JSON payload hello device sends tooIoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="e0583-123">Запустите имитированное устройство hello Node.js с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e0583-123">Run hello Node.js simulated device using hello following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="e0583-124">Изучите hello новый RPM телеметрии тип, который отображается на диаграмме hello в панели мониторинга hello:</span><span class="sxs-lookup"><span data-stu-id="e0583-124">Observe hello new RPM telemetry type that displays on hello chart in hello dashboard:</span></span>

![Добавление панели мониторинга toohello об/мин][image3]

> [!NOTE]
> <span data-ttu-id="e0583-126">Может требуется toodisable и затем включите устройство Node.js hello hello **устройств** страницу изменения hello toosee мониторинга hello немедленно.</span><span class="sxs-lookup"><span data-stu-id="e0583-126">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="customize-hello-dashboard-display"></a><span data-ttu-id="e0583-127">Настройте отображение панели мониторинга hello</span><span class="sxs-lookup"><span data-stu-id="e0583-127">Customize hello dashboard display</span></span>

<span data-ttu-id="e0583-128">Hello **сведения об устройстве** сообщение может содержать метаданные о телеметрии hello hello устройство может отправлять tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="e0583-128">hello **Device-Info** message can include metadata about hello telemetry hello device can send tooIoT Hub.</span></span> <span data-ttu-id="e0583-129">Эти метаданные можно указать типы телеметрии hello, отправляемую hello устройства.</span><span class="sxs-lookup"><span data-stu-id="e0583-129">This metadata can specify hello telemetry types hello device sends.</span></span> <span data-ttu-id="e0583-130">Изменение hello **deviceMetaData** значения в файл tooinclude hello remote_monitoring.js **телеметрии** hello после определения **команды** определения.</span><span class="sxs-lookup"><span data-stu-id="e0583-130">Modify hello **deviceMetaData** value in hello remote_monitoring.js file tooinclude a **Telemetry** definition following hello **Commands** definition.</span></span> <span data-ttu-id="e0583-131">Hello следующий фрагмент кода показывает hello **команды** определение (быть убедиться, что tooadd `,` после hello **команды** определение):</span><span class="sxs-lookup"><span data-stu-id="e0583-131">hello following code snippet shows hello **Commands** definition (be sure tooadd a `,` after hello **Commands** definition):</span></span>

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> <span data-ttu-id="e0583-132">решение для удаленного мониторинга Hello используется определение метаданных hello toocompare сравнение без учета регистра с данными в потоке данных телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="e0583-132">hello remote monitoring solution uses a case-insensitive match toocompare hello metadata definition with data in hello telemetry stream.</span></span>


<span data-ttu-id="e0583-133">Добавление **телеметрии** определения, как показано в предыдущем hello фрагмент кода hello поведение мониторинга hello не меняется.</span><span class="sxs-lookup"><span data-stu-id="e0583-133">Adding a **Telemetry** definition as shown in hello preceding code snippet does not change hello behavior of hello dashboard.</span></span> <span data-ttu-id="e0583-134">Тем не менее, может также включать метаданные hello **DisplayName** атрибута toocustomize hello, отображаются в панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="e0583-134">However, hello metadata can also include a **DisplayName** attribute toocustomize hello display in hello dashboard.</span></span> <span data-ttu-id="e0583-135">Обновление hello **телеметрии** определение метаданных, как показано в hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="e0583-135">Update hello **Telemetry** metadata definition as shown in hello following snippet:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

<span data-ttu-id="e0583-136">Hello следующем снимке экрана показано это изменение изменение hello условные обозначения диаграммы на панели мониторинга hello:</span><span class="sxs-lookup"><span data-stu-id="e0583-136">hello following screenshot shows how this change modifies hello chart legend on hello dashboard:</span></span>

![Настройка условных обозначений диаграммы hello][image4]

> [!NOTE]
> <span data-ttu-id="e0583-138">Может требуется toodisable и затем включите устройство Node.js hello hello **устройств** страницу изменения hello toosee мониторинга hello немедленно.</span><span class="sxs-lookup"><span data-stu-id="e0583-138">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="filter-hello-telemetry-types"></a><span data-ttu-id="e0583-139">Фильтровать типы телеметрии hello</span><span class="sxs-lookup"><span data-stu-id="e0583-139">Filter hello telemetry types</span></span>

<span data-ttu-id="e0583-140">По умолчанию hello диаграммы на панели мониторинга hello отображает каждого ряда данных в потоке данных телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="e0583-140">By default, hello chart on hello dashboard shows every data series in hello telemetry stream.</span></span> <span data-ttu-id="e0583-141">Можно использовать hello **сведения об устройстве** toosuppress метаданных hello Отображение типов определенной телеметрии на диаграмме hello.</span><span class="sxs-lookup"><span data-stu-id="e0583-141">You can use hello **Device-Info** metadata toosuppress hello display of specific telemetry types on hello chart.</span></span> 

<span data-ttu-id="e0583-142">Диаграмма hello toomake Показать только температуры и влажности телеметрии, опустить **ExternalTemperature** из hello **сведения об устройстве** **телеметрии** метаданных следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e0583-142">toomake hello chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from hello **Device-Info** **Telemetry** metadata as follows:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

<span data-ttu-id="e0583-143">Hello **наружной температуры** больше не отображается на диаграмме hello:</span><span class="sxs-lookup"><span data-stu-id="e0583-143">hello **Outdoor Temperature** no longer displays on hello chart:</span></span>

![Данные телеметрии hello фильтра на панели мониторинга hello][image5]

<span data-ttu-id="e0583-145">Это изменение влияет только на отображение диаграммы hello.</span><span class="sxs-lookup"><span data-stu-id="e0583-145">This change only affects hello chart display.</span></span> <span data-ttu-id="e0583-146">Hello **ExternalTemperature** значение данных по-прежнему сохраняются и становятся доступными для обработки базы данных.</span><span class="sxs-lookup"><span data-stu-id="e0583-146">hello **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="e0583-147">Может требуется toodisable и затем включите устройство Node.js hello hello **устройств** страницу изменения hello toosee мониторинга hello немедленно.</span><span class="sxs-lookup"><span data-stu-id="e0583-147">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="e0583-148">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="e0583-148">Handle errors</span></span>

<span data-ttu-id="e0583-149">Для toodisplay потока данных на диаграмме hello его **тип** в hello **сведения об устройстве** метаданных должен соответствовать типу данных hello hello телеметрии значений.</span><span class="sxs-lookup"><span data-stu-id="e0583-149">For a data stream toodisplay on hello chart, its **Type** in hello **Device-Info** metadata must match hello data type of hello telemetry values.</span></span> <span data-ttu-id="e0583-150">Например, если hello метаданные указывают, hello **тип** влажности является данных **int** и **двойные** найден в потоке данных телеметрии hello телеметрии влажности hello не не отображать на диаграмме hello.</span><span class="sxs-lookup"><span data-stu-id="e0583-150">For example, if hello metadata specifies that hello **Type** of humidity data is **int** and a **double** is found in hello telemetry stream then hello humidity telemetry does not display on hello chart.</span></span> <span data-ttu-id="e0583-151">Здравствуйте, однако **влажность** значения по-прежнему сохраняются и становятся доступными для внутренней обработки.</span><span class="sxs-lookup"><span data-stu-id="e0583-151">However, hello **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0583-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0583-152">Next steps</span></span>

<span data-ttu-id="e0583-153">Теперь, когда вы знаете, как toouse динамические данные телеметрии, можно узнать больше о том, как hello предварительно настроенных решений использовать сведения об устройстве: [метаданных сведения устройства в удаленный мониторинг hello предварительно настроенное решение] [ lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="e0583-153">Now that you've seen how toouse dynamic telemetry, you can learn more about how hello preconfigured solutions use device information: [Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
