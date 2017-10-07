---
title: "toocloud aaaSimulated Raspberry Pi (Node.js) - tooAzure симулятор web Pi Raspberry подключения центр IoT | Документы Microsoft"
description: "Подключение web Raspberry Pi симулятор tooAzure центр IoT для Raspberry Pi toosend данные toohello облако Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "малиновая pi симулятор, azure iot малиновая pi, малиновая pi центра iot, малиновая pi отправки данных toocloud, малиновая pi toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a><span data-ttu-id="de5b3-104">Подключение tooAzure online симулятор Raspberry Pi центр IoT (Node.js)</span><span class="sxs-lookup"><span data-stu-id="de5b3-104">Connect Raspberry Pi online simulator tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="de5b3-105">В этом учебнике сначала обучения hello основы работы с симулятором online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="de5b3-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="de5b3-106">Затем вы узнаете, как tooseamlessly подключаться hello Pi симулятор toohello облака с помощью [центр IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="de5b3-106">You then learn how tooseamlessly connect hello Pi simulator toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="de5b3-107">При наличии физических устройств посетите [tooAzure подключения Pi Raspberry центр IoT](iot-hub-raspberry-pi-kit-node-get-started.md) tooget работы.</span><span class="sxs-lookup"><span data-stu-id="de5b3-107">If you have physical devices, visit [Connect Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="de5b3-108">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="de5b3-108">What you do</span></span>

* <span data-ttu-id="de5b3-109">Hello с основами online симулятор Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="de5b3-109">Learn hello basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="de5b3-110">Создайте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="de5b3-110">Create an IoT hub.</span></span>
* <span data-ttu-id="de5b3-111">Зарегистрируем устройство для Pi в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="de5b3-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="de5b3-112">Выполнение примера приложения на Pi toosend имитировать центра IoT tooyour данных датчика.</span><span class="sxs-lookup"><span data-stu-id="de5b3-112">Run a sample application on Pi toosend simulated sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="de5b3-113">Подключите имитацию центра IoT tooan Raspberry Pi, создаваемом.</span><span class="sxs-lookup"><span data-stu-id="de5b3-113">Connect simulated Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="de5b3-114">Тогда выполнение примера приложения с данными датчика toogenerate симулятор hello.</span><span class="sxs-lookup"><span data-stu-id="de5b3-114">Then you run a sample application with hello simulator toogenerate sensor data.</span></span> <span data-ttu-id="de5b3-115">Отправьте центра IoT tooyour данных датчика hello.</span><span class="sxs-lookup"><span data-stu-id="de5b3-115">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="de5b3-116">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="de5b3-116">What you learn</span></span>

* <span data-ttu-id="de5b3-117">Как toocreate центр Azure IoT и получить новые строки подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="de5b3-117">How toocreate an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="de5b3-118">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="de5b3-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="de5b3-119">Как toowork с имитатором online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="de5b3-119">How toowork with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="de5b3-120">Как центр IoT tooyour данных датчика toosend.</span><span class="sxs-lookup"><span data-stu-id="de5b3-120">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="de5b3-121">Общие сведения о веб-симуляторе Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="de5b3-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="de5b3-122">Щелкните online симулятор toolaunch кнопку Raspberry Pi hello.</span><span class="sxs-lookup"><span data-stu-id="de5b3-122">Click hello button toolaunch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
[<span data-ttu-id="de5b3-123">Запустить симулятор Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="de5b3-123">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

<span data-ttu-id="de5b3-124">В симуляторе hello web имеется три области.</span><span class="sxs-lookup"><span data-stu-id="de5b3-124">There are three areas in hello web simulator.</span></span>
* <span data-ttu-id="de5b3-125">Область сборки - схемы по умолчанию hello — что Pi подключается с BME280 датчика и Индикатора.</span><span class="sxs-lookup"><span data-stu-id="de5b3-125">Assembly area - hello default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="de5b3-126">область Hello заблокирован в предварительной версии таким образом, в настоящее время не удается выполнить настройку.</span><span class="sxs-lookup"><span data-stu-id="de5b3-126">hello area is locked in preview version so currently you cannot do customization.</span></span>
* <span data-ttu-id="de5b3-127">Кодирование область - toocode с Raspberry Pi редактора кода в Интернете.</span><span class="sxs-lookup"><span data-stu-id="de5b3-127">Coding area - An online code editor for you toocode with Raspberry Pi.</span></span> <span data-ttu-id="de5b3-128">Образец приложения по умолчанию Hello помогает toocollect датчиков с BME280 датчиков и отправляет tooyour центр IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="de5b3-128">hello default sample application helps toocollect sensor data from BME280 sensor and sends tooyour Azure IoT Hub.</span></span> <span data-ttu-id="de5b3-129">приложение Hello полностью совместима с реальными Pi устройств.</span><span class="sxs-lookup"><span data-stu-id="de5b3-129">hello application is fully compatible with real Pi devices.</span></span> 
* <span data-ttu-id="de5b3-130">Окно интегрированной консоли - показывает hello вывода кода.</span><span class="sxs-lookup"><span data-stu-id="de5b3-130">Integrated console window - It shows hello output of your code.</span></span> <span data-ttu-id="de5b3-131">Hello верхней части окна имеются три кнопки.</span><span class="sxs-lookup"><span data-stu-id="de5b3-131">At hello top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="de5b3-132">**Запустите** -запустите приложение hello в область кода hello.</span><span class="sxs-lookup"><span data-stu-id="de5b3-132">**Run** - Run hello application in hello coding area.</span></span>
   * <span data-ttu-id="de5b3-133">**Сброс** -кодирования области toohello по умолчанию образец приложения hello сброса.</span><span class="sxs-lookup"><span data-stu-id="de5b3-133">**Reset** - Reset hello coding area toohello default sample application.</span></span>
   * <span data-ttu-id="de5b3-134">**Свертки/расширение** — в правой стороне существует — кнопка для вас toofold или свернут hello окна консоли hello.</span><span class="sxs-lookup"><span data-stu-id="de5b3-134">**Fold/Expand** - On hello right side there is a button for you toofold/expand hello console window.</span></span>

> [!NOTE] 
<span data-ttu-id="de5b3-135">Имитатор web Raspberry Pi Hello теперь доступна в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="de5b3-135">hello Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="de5b3-136">Мы хотели бы toohear голоса в hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="de5b3-136">We'd like toohear your voice in hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="de5b3-137">исходный код Hello public на [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="de5b3-137">hello source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Общие сведения об онлайн-симуляторе Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="de5b3-139">Запуск примера приложения на веб-симуляторе Pi</span><span class="sxs-lookup"><span data-stu-id="de5b3-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="de5b3-140">В программировании области, убедитесь, что вы работаете в пример приложения hello по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="de5b3-140">In coding area, make sure you are working on hello default sample application.</span></span> <span data-ttu-id="de5b3-141">Подставьте вместо приветствия в строке 15 hello строки подключения устройства Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="de5b3-141">Replace hello placeholder in Line 15 with hello Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="de5b3-142">![Замените строку подключения устройства hello](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="de5b3-142">![Replace hello device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="de5b3-143">Нажмите кнопку **запуска** или тип `npm start` toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="de5b3-143">Click **Run** or type `npm start` toorun hello application.</span></span>


<span data-ttu-id="de5b3-144">Вы увидите hello следующие выходные данные, показаны hello датчиков и hello сообщений, отправленных центра IoT tooyour ![вывод — данные датчика, отправленные из центра IoT tooyour Raspberry Pi](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="de5b3-144">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub ![Output - sensor data sent from Raspberry Pi tooyour IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="de5b3-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de5b3-145">Next steps</span></span>

<span data-ttu-id="de5b3-146">Вы впервые запускаете в образце данных датчика toocollect приложения и отправьте его центр IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="de5b3-146">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
