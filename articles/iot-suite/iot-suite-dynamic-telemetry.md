---
title: "Использование динамической телеметрии | Документация Майкрософт"
description: "Ознакомьтесь с этим руководством, чтобы узнать, как использовать динамическую телеметрию с предварительно настроенным решением для удаленного мониторинга Azure IoT Suite."
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
ms.openlocfilehash: 0114f27f9b8ae76e1170d04ddf66e2c4bf20686a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-dynamic-telemetry-with-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="de040-103">Использование динамической телеметрии с предварительно настроенным решением для удаленного мониторинга</span><span class="sxs-lookup"><span data-stu-id="de040-103">Use dynamic telemetry with the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="de040-104">Динамическая телеметрия позволяют визуализировать любые данные телеметрии, отправленные в предварительно настроенное решение для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="de040-104">Dynamic telemetry enables you to visualize any telemetry sent to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="de040-105">Имитации устройств, развертываемые вместе с предварительно настроенным решением, отправляют данные телеметрии температуры и влажности, которые можно отобразить на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="de040-105">The simulated devices that deploy with the preconfigured solution send temperature and humidity telemetry, which you can visualize on the dashboard.</span></span> <span data-ttu-id="de040-106">Если настроить существующие имитации устройств, создать имитации устройств или подключить физические устройства к предварительно настроенному решению, то это позволит отправлять другие значения телеметрии, такие как внешняя температура, число оборотов в минуту или скорость ветра.</span><span class="sxs-lookup"><span data-stu-id="de040-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices to the preconfigured solution you can send other telemetry values such as the external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="de040-107">Затем эти дополнительные данные телеметрии можно будет визуализировать на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="de040-107">You can then visualize this additional telemetry on the dashboard.</span></span>

<span data-ttu-id="de040-108">В этом учебнике используется простая имитация устройства Node.js, которую можно легко изменить для экспериментов с динамической телеметрией.</span><span class="sxs-lookup"><span data-stu-id="de040-108">This tutorial uses a simple Node.js simulated device that you can easily modify to experiment with dynamic telemetry.</span></span>

<span data-ttu-id="de040-109">Чтобы завершить этот учебник, потребуется следующее.</span><span class="sxs-lookup"><span data-stu-id="de040-109">To complete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="de040-110">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="de040-110">An active Azure subscription.</span></span> <span data-ttu-id="de040-111">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="de040-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="de040-112">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="de040-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="de040-113">[Node.js][lnk-node] версии 0.12.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="de040-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="de040-114">Этот учебник подходит для любой операционной системы, например Windows или Linux, в которой можно установить Node.js.</span><span class="sxs-lookup"><span data-stu-id="de040-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="de040-115">Добавление типа данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="de040-115">Add a telemetry type</span></span>

<span data-ttu-id="de040-116">Следующий шаг — заменить данные телеметрии, созданные имитацией устройства Node.js, новым набором значений.</span><span class="sxs-lookup"><span data-stu-id="de040-116">The next step is to replace the telemetry generated by the Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="de040-117">Остановите имитацию устройства Node.js, нажав клавиши **Ctrl+C** в командной строке или оболочке.</span><span class="sxs-lookup"><span data-stu-id="de040-117">Stop the Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="de040-118">В файле remote_monitoring.js можно увидеть базовые значения для существующих данных телеметрии температуры, влажности и внешней температуры.</span><span class="sxs-lookup"><span data-stu-id="de040-118">In the remote_monitoring.js file, you can see the base data values for the existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="de040-119">Добавьте базовое значение данных для **rpm** следующим образом.</span><span class="sxs-lookup"><span data-stu-id="de040-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="de040-120">Имитированное устройство Node.js добавляет случайное приращение базовых значений данных с помощью функции **generateRandomIncrement**, определенной в файле remote_monitoring.js.</span><span class="sxs-lookup"><span data-stu-id="de040-120">The Node.js simulated device uses the **generateRandomIncrement** function in the remote_monitoring.js file to add a random increment to the base data values.</span></span> <span data-ttu-id="de040-121">Рандомизируйте значение **rpm** , добавив строку кода после существующего кода рандомизации следующим образом.</span><span class="sxs-lookup"><span data-stu-id="de040-121">Randomize the **rpm** value by adding a line of code after the existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="de040-122">Добавьте новое значение rpm в полезные данные JSON, которые устройство отправляет в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="de040-122">Add the new rpm value to the JSON payload the device sends to IoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="de040-123">Запустите имитацию устройства Node.js с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="de040-123">Run the Node.js simulated device using the following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="de040-124">Вы увидите новый тип данных телеметрии RPM на диаграмме на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="de040-124">Observe the new RPM telemetry type that displays on the chart in the dashboard:</span></span>

![Добавление значения оборотов в секунду на панель мониторинга][image3]

> [!NOTE]
> <span data-ttu-id="de040-126">Может потребоваться отключить и снова включить устройство Node.js на странице **Устройства** на панели мониторинга, чтобы немедленно отобразить изменения.</span><span class="sxs-lookup"><span data-stu-id="de040-126">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="customize-the-dashboard-display"></a><span data-ttu-id="de040-127">Настройка отображения панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="de040-127">Customize the dashboard display</span></span>

<span data-ttu-id="de040-128">Сообщение **Device-Info** может содержать метаданные о данных телеметрии, которые устройство может отправлять в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="de040-128">The **Device-Info** message can include metadata about the telemetry the device can send to IoT Hub.</span></span> <span data-ttu-id="de040-129">В этих метаданных могут быть указаны типы данных телеметрии, отправляемых устройством.</span><span class="sxs-lookup"><span data-stu-id="de040-129">This metadata can specify the telemetry types the device sends.</span></span> <span data-ttu-id="de040-130">Измените значение **deviceMetaData** в файле remote_monitoring.js, чтобы добавить определение **Telemetry** после определения **Commands**.</span><span class="sxs-lookup"><span data-stu-id="de040-130">Modify the **deviceMetaData** value in the remote_monitoring.js file to include a **Telemetry** definition following the **Commands** definition.</span></span> <span data-ttu-id="de040-131">Определение **Commands** показано в следующем фрагменте кода (не забудьте добавить `,` после определения **Commands**).</span><span class="sxs-lookup"><span data-stu-id="de040-131">The following code snippet shows the **Commands** definition (be sure to add a `,` after the **Commands** definition):</span></span>

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
> <span data-ttu-id="de040-132">Решение для удаленного мониторинга проверяет соответствие регистра при сравнении определения метаданных с информацией в потоке данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="de040-132">The remote monitoring solution uses a case-insensitive match to compare the metadata definition with data in the telemetry stream.</span></span>


<span data-ttu-id="de040-133">Добавление определения **Telemetry** , показанное в предыдущем фрагменте кода, не изменяет поведение панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="de040-133">Adding a **Telemetry** definition as shown in the preceding code snippet does not change the behavior of the dashboard.</span></span> <span data-ttu-id="de040-134">Тем не менее метаданные также могут содержать атрибут **DisplayName** для настройки отображения на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="de040-134">However, the metadata can also include a **DisplayName** attribute to customize the display in the dashboard.</span></span> <span data-ttu-id="de040-135">Измените определение метаданных **Telemetry** , как показано во фрагменте кода ниже.</span><span class="sxs-lookup"><span data-stu-id="de040-135">Update the **Telemetry** metadata definition as shown in the following snippet:</span></span>

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

<span data-ttu-id="de040-136">На следующем снимке экрана показано, как это изменение меняет легенду диаграммы на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="de040-136">The following screenshot shows how this change modifies the chart legend on the dashboard:</span></span>

![Настройка легенды диаграммы][image4]

> [!NOTE]
> <span data-ttu-id="de040-138">Может потребоваться отключить и снова включить устройство Node.js на странице **Устройства** на панели мониторинга, чтобы немедленно отобразить изменения.</span><span class="sxs-lookup"><span data-stu-id="de040-138">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="filter-the-telemetry-types"></a><span data-ttu-id="de040-139">Фильтрация типов данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="de040-139">Filter the telemetry types</span></span>

<span data-ttu-id="de040-140">По умолчанию диаграмма на панели мониторинга отображает каждый ряд данных в потоке данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="de040-140">By default, the chart on the dashboard shows every data series in the telemetry stream.</span></span> <span data-ttu-id="de040-141">Можно использовать метаданные **Device-Info** , чтобы подавить вывод определенных типов данных телеметрии на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="de040-141">You can use the **Device-Info** metadata to suppress the display of specific telemetry types on the chart.</span></span> 

<span data-ttu-id="de040-142">Чтобы на диаграмме отображались только данные телеметрии температуры и влажности, опустите **ExternalTemperature** в метаданных **Telemetry** для **Device-Info**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="de040-142">To make the chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from the **Device-Info** **Telemetry** metadata as follows:</span></span>

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

<span data-ttu-id="de040-143">**Outdoor Temperature** (Наружная температура) больше не отображается на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="de040-143">The **Outdoor Temperature** no longer displays on the chart:</span></span>

![Фильтрация данных телеметрии на панели мониторинга][image5]

<span data-ttu-id="de040-145">Это изменение влияет только на отображение диаграммы.</span><span class="sxs-lookup"><span data-stu-id="de040-145">This change only affects the chart display.</span></span> <span data-ttu-id="de040-146">Значения данных **ExternalTemperature** по-прежнему сохраняются и остаются доступными для внутренней обработки.</span><span class="sxs-lookup"><span data-stu-id="de040-146">The **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="de040-147">Может потребоваться отключить и снова включить устройство Node.js на странице **Устройства** на панели мониторинга, чтобы немедленно отобразить изменения.</span><span class="sxs-lookup"><span data-stu-id="de040-147">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="de040-148">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="de040-148">Handle errors</span></span>

<span data-ttu-id="de040-149">Чтобы поток данных можно было отобразить на диаграмме, его значение **Type** в метаданных **Device-Info** должно соответствовать типу данных значений телеметрии.</span><span class="sxs-lookup"><span data-stu-id="de040-149">For a data stream to display on the chart, its **Type** in the **Device-Info** metadata must match the data type of the telemetry values.</span></span> <span data-ttu-id="de040-150">Например, если в метаданных указано, что **Type** данных влажности — **int**, а в потоке данных телеметрии обнаружен тип **double**, то данные телеметрии влажности не отображаются на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="de040-150">For example, if the metadata specifies that the **Type** of humidity data is **int** and a **double** is found in the telemetry stream then the humidity telemetry does not display on the chart.</span></span> <span data-ttu-id="de040-151">Тем не менее значения **Humidity** по-прежнему сохраняются и остаются доступными для внутренней обработки.</span><span class="sxs-lookup"><span data-stu-id="de040-151">However, the **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de040-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de040-152">Next steps</span></span>

<span data-ttu-id="de040-153">Теперь, когда вы узнали, как использовать динамическую телеметрию, ознакомьтесь также со статьей о том, как с помощью предварительно настроенных решений применять сведения об устройстве: [Метаданные сведений об устройстве в предварительно настроенном решении для удаленного мониторинга][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="de040-153">Now that you've seen how to use dynamic telemetry, you can learn more about how the preconfigured solutions use device information: [Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
