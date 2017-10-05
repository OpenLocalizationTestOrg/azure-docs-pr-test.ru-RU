---
title: "Подключение веб-симулятора Raspberry Pi (Node.js) к Центру Интернета вещей для передачи данных в облако | Документация Майкрософт"
description: "Подключение веб-симулятора Raspberry Pi к Центру Интернета вещей для передачи данных с него в облако Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "симулятор raspberry pi, raspberry pi и центр интернета вещей azure, raspberry pi и центр интернета вещей, отправка данных с raspberry pi в облако, подключение raspberry pi к облаку"
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 3b80bf35d6af91d5bdb196d97668dc0f837b92cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-online-simulator-to-azure-iot-hub-nodejs"></a><span data-ttu-id="f7e14-104">Подключение онлайн-симулятора Raspberry Pi к Центру Интернета вещей Azure (Node.js)</span><span class="sxs-lookup"><span data-stu-id="f7e14-104">Connect Raspberry Pi online simulator to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="f7e14-105">В этом руководстве описано, как начать работу с онлайн-симулятором Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f7e14-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="f7e14-106">Кроме того, вы узнаете, как можно легко подключить симулятор Pi к облаку с помощью [Центра Интернета вещей Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="f7e14-106">You then learn how to seamlessly connect the Pi simulator to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="f7e14-107">Если вы используете физические устройства, ознакомьтесь со статьей [Подключение Raspberry Pi к Центру Интернета вещей Azure (Node.js)](iot-hub-raspberry-pi-kit-node-get-started.md), чтобы приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="f7e14-107">If you have physical devices, visit [Connect Raspberry Pi to Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) to get started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator to Azure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="f7e14-108">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="f7e14-108">What you do</span></span>

* <span data-ttu-id="f7e14-109">Изучим основы использования онлайн-симулятора Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f7e14-109">Learn the basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="f7e14-110">Создайте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f7e14-110">Create an IoT hub.</span></span>
* <span data-ttu-id="f7e14-111">Зарегистрируем устройство для Pi в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f7e14-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="f7e14-112">Запустим пример приложения на Pi для отправки симулированных данных датчика в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f7e14-112">Run a sample application on Pi to send simulated sensor data to your IoT hub.</span></span>

<span data-ttu-id="f7e14-113">Подключите виртуальное устройство Raspberry Pi к созданному Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f7e14-113">Connect simulated Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="f7e14-114">Затем запустите пример приложения с помощью симулятора, чтобы создать данные датчика.</span><span class="sxs-lookup"><span data-stu-id="f7e14-114">Then you run a sample application with the simulator to generate sensor data.</span></span> <span data-ttu-id="f7e14-115">После этого отправьте данные с датчика в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f7e14-115">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="f7e14-116">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="f7e14-116">What you learn</span></span>

* <span data-ttu-id="f7e14-117">Как создать Центр Интернета вещей Azure и получить строку подключения нового устройства.</span><span class="sxs-lookup"><span data-stu-id="f7e14-117">How to create an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="f7e14-118">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f7e14-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="f7e14-119">Как использовать онлайн-симулятор Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f7e14-119">How to work with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="f7e14-120">Как отправить данные датчика в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f7e14-120">How to send sensor data to your IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="f7e14-121">Общие сведения о веб-симуляторе Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="f7e14-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="f7e14-122">Нажмите кнопку, чтобы запустить онлайн-симулятор Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f7e14-122">Click the button to launch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
<span data-ttu-id="f7e14-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Запустить симулятор Raspberry Pi</a></span><span class="sxs-lookup"><span data-stu-id="f7e14-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Start Raspberry Pi Simulator</a></span></span>

<span data-ttu-id="f7e14-124">В веб-симуляторе есть 3 области.</span><span class="sxs-lookup"><span data-stu-id="f7e14-124">There are three areas in the web simulator.</span></span>
1. <span data-ttu-id="f7e14-125">Область сборки. В стандартной схеме Pi соединяется с датчиком BME280 и светодиодным индикатором.</span><span class="sxs-lookup"><span data-stu-id="f7e14-125">Assembly area - The default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="f7e14-126">В предварительной версии эта область заблокирована, поэтому вы не можете выполнить настройку.</span><span class="sxs-lookup"><span data-stu-id="f7e14-126">The area is locked in preview version so currently you cannot do customization.</span></span>
2. <span data-ttu-id="f7e14-127">Область кодирования. Интерактивный редактор кода, позволяющий писать код, используя Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f7e14-127">Coding area - An online code editor for you to code with Raspberry Pi.</span></span> <span data-ttu-id="f7e14-128">Стандартный пример приложения позволяет выполнить сбор данных датчика BME280 и отправить их в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f7e14-128">The default sample application helps to collect sensor data from BME280 sensor and sends to your Azure IoT Hub.</span></span> <span data-ttu-id="f7e14-129">Приложение полностью совместимо с реальными устройствами Pi.</span><span class="sxs-lookup"><span data-stu-id="f7e14-129">The application is fully compatible with real Pi devices.</span></span> 
3. <span data-ttu-id="f7e14-130">Встроенное окно консоли. Показывает выходные данные вашего кода.</span><span class="sxs-lookup"><span data-stu-id="f7e14-130">Integrated console window - It shows the output of your code.</span></span> <span data-ttu-id="f7e14-131">В верхней части этого окна есть 3 кнопки.</span><span class="sxs-lookup"><span data-stu-id="f7e14-131">At the top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="f7e14-132">**Запуск.** Запуск приложения в области кодирования.</span><span class="sxs-lookup"><span data-stu-id="f7e14-132">**Run** - Run the application in the coding area.</span></span>
   * <span data-ttu-id="f7e14-133">**Сброс.** Сброс параметров области кодирования до стандартных параметров примера приложения.</span><span class="sxs-lookup"><span data-stu-id="f7e14-133">**Reset** - Reset the coding area to the default sample application.</span></span>
   * <span data-ttu-id="f7e14-134">**Fold/Expand** (Свернуть или развернуть). В правой части расположена кнопка, с помощью которой можно свернуть или развернуть окно консоли.</span><span class="sxs-lookup"><span data-stu-id="f7e14-134">**Fold/Expand** - On the right side there is a button for you to fold/expand the console window.</span></span>

> [!NOTE] 
<span data-ttu-id="f7e14-135">Веб-симулятор Raspberry Pi доступен в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="f7e14-135">The Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="f7e14-136">Оставляйте свои комментарии в [чате Gitter](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="f7e14-136">We'd like to hear your voice in the [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="f7e14-137">Исходный код доступен на сайте [GitHub](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="f7e14-137">The source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Общие сведения об онлайн-симуляторе Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="f7e14-139">Запуск примера приложения на веб-симуляторе Pi</span><span class="sxs-lookup"><span data-stu-id="f7e14-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="f7e14-140">В области кодирования убедитесь, что вы работаете над стандартным примером приложения.</span><span class="sxs-lookup"><span data-stu-id="f7e14-140">In coding area, make sure you are working on the default sample application.</span></span> <span data-ttu-id="f7e14-141">Замените значения заполнителя в 15 строке на строку подключения устройства Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f7e14-141">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="f7e14-142">![Замена строки подключения устройства](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="f7e14-142">![Replace the device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="f7e14-143">Щелкните **Запуск** или введите `npm start`, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f7e14-143">Click **Run** or type `npm start` to run the application.</span></span>


<span data-ttu-id="f7e14-144">Должны отобразиться следующие результаты, содержащие данные датчика и сообщения, которые отправляются в Центр Интернета вещей: ![Выходные данные — данные датчика, отправленные с Raspberry Pi в Центр Интернета вещей](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="f7e14-144">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub ![Output - sensor data sent from Raspberry Pi to your IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="f7e14-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7e14-145">Next steps</span></span>

<span data-ttu-id="f7e14-146">Вы запустили пример приложения, чтобы собрать данные датчика и отправить их в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f7e14-146">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
