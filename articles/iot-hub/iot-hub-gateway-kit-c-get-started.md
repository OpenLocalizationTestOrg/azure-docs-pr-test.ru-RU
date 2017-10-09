---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT | Документация Майкрософт"
description: "Приступая к работе с IoT шлюза начального набора, создать ваш центр Azure IoT Подключите концентратор IoT toohello SensorTag и шлюза"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure iot hub, шлюз iot, Приступая к работе с hello Интернет вещей, набор средств iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="ec878-104">Приступая к работе с начальным набором шлюза Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="ec878-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec878-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="ec878-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="ec878-106">Имитация устройства</span><span class="sxs-lookup"><span data-stu-id="ec878-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="ec878-107">В этом учебнике, начните с изучения hello основы работы с [IoT шлюза начального набора](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="ec878-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="ec878-108">Вы будете работать с Intel NUC под управлением Linux воздушного р. и hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="ec878-108">You will be working with Intel NUC that's running Wind River Linux and hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="ec878-109">Вы узнаете, как tooseamleesly подключаться toohello облачных устройств с помощью центра IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="ec878-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="ec878-110">**Нет начального набора?** Щелкните [здесь](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="ec878-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="ec878-111">**Нет SensorTag?** [Начните имитацию устройства](iot-hub-gateway-kit-c-sim-get-started.md) или [купите SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag).</span><span class="sxs-lookup"><span data-stu-id="ec878-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="ec878-112">Урок 1. Настройка NUC</span><span class="sxs-lookup"><span data-stu-id="ec878-112">Lesson 1: Configure your NUC</span></span>
![Урок 1. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="ec878-114">На этом занятии настроить NUC Intel (Далее единицы для вычисления) в hello Kit виде шлюза Azure IoT, установите пакет Azure IoT Edge hello на NUC и запуска шлюза функциональность tooverify hello образца приложения.</span><span class="sxs-lookup"><span data-stu-id="ec878-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="ec878-115">*Предполагаемое время toocomplete: 15 минут*</span><span class="sxs-lookup"><span data-stu-id="ec878-115">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="ec878-116">Go слишком[Настройка NUC Intel виде шлюза IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="ec878-116">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="ec878-117">Урок 2. Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="ec878-117">Lesson 2: Create your IoT Hub</span></span>
![Урок 2. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="ec878-119">На этом занятии устанавливается hello средств и программного обеспечения на компьютере узла.</span><span class="sxs-lookup"><span data-stu-id="ec878-119">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="ec878-120">Затем можно создать бесплатную учетную запись Azure, подготовки ваш центр Azure IoT и создания своим первым устройством в центр IoT hello.</span><span class="sxs-lookup"><span data-stu-id="ec878-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="ec878-121">Прежде чем продолжать, завершите урок 1.</span><span class="sxs-lookup"><span data-stu-id="ec878-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="ec878-122">Получить средства hello</span><span class="sxs-lookup"><span data-stu-id="ec878-122">Get hello tools</span></span>
<span data-ttu-id="ec878-123">На главном компьютере установите hello средств и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="ec878-123">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="ec878-124">*Предполагаемое время toocomplete: 20 минут*</span><span class="sxs-lookup"><span data-stu-id="ec878-124">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="ec878-125">Go слишком[средства hello](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="ec878-125">Go too[Get hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="ec878-126">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="ec878-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="ec878-127">Создание группы ресурсов, подготовки к первой центр Azure IoT и добавить вашего первого устройства toohello центр IoT с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ec878-127">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="ec878-128">*Предполагаемое время toocomplete: 10 минут*</span><span class="sxs-lookup"><span data-stu-id="ec878-128">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="ec878-129">Go слишком[создать центр IoT и регистрация устройства](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="ec878-129">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="ec878-130">Урок 3. Получение сообщений из SensorTag и чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="ec878-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="ec878-131">На этом занятии будет использовать конфигурации hello tooautomate сценарии и выполнение примера приложения ЛЮЧИТЬ шлюза.</span><span class="sxs-lookup"><span data-stu-id="ec878-131">In this lesson, you will use scripts tooautomate hello configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="ec878-132">Такие приложения использовать коллекцию модулей tooaggregate и преобразования данных, обработки команд и выполнять любое количество связанных задач.</span><span class="sxs-lookup"><span data-stu-id="ec878-132">Such applications use a collection of modules tooaggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="ec878-133">Модули взаимодействуют друг с другом через брокер сообщений.</span><span class="sxs-lookup"><span data-stu-id="ec878-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="ec878-134">Пример приложения Hello имеет ЛЮЧИТЬ модуля и модуль концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="ec878-134">hello sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="ec878-135">Hello ЛЮЧИТЬ модуль получает данные из SensorTag отключить.</span><span class="sxs-lookup"><span data-stu-id="ec878-135">hello BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="ec878-136">Здравствуйте, пакеты модуля концентратора IoT данных hello полученных и отправляет его центр IoT tooyour через шлюз платформы hello в Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="ec878-136">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Урок 3. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a><span data-ttu-id="ec878-138">Настройка и выполнение примера приложения hello ЛЮЧИТЬ</span><span class="sxs-lookup"><span data-stu-id="ec878-138">Configure and run hello BLE sample app</span></span>
<span data-ttu-id="ec878-139">Настройте подключение hello между SensorTag и шлюза.</span><span class="sxs-lookup"><span data-stu-id="ec878-139">Set up hello connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="ec878-140">Затем завершите настройку hello и запустить пример приложения hello отключить.</span><span class="sxs-lookup"><span data-stu-id="ec878-140">Then finish hello configuration and run hello BLE sample application.</span></span>

<span data-ttu-id="ec878-141">*Предполагаемое время toocomplete: 15 минут*</span><span class="sxs-lookup"><span data-stu-id="ec878-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="ec878-142">Go слишком[настройки и выполнения hello ЛЮЧИТЬ пример приложения](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="ec878-142">Go too[Configure and run hello BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="ec878-143">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="ec878-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="ec878-144">Запустите образец кода на вашем узле компьютер tooread сообщения из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="ec878-144">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="ec878-145">*Предполагаемое время toocomplete: 15 минут*</span><span class="sxs-lookup"><span data-stu-id="ec878-145">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="ec878-146">Go слишком[чтения сообщений из вашего центра IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="ec878-146">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="ec878-147">Урок 4: Сохранить сообщения tooAzure хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="ec878-147">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="ec878-148">Создайте приложение Azure функции, которое получает входящие сообщения от вашего центра IoT и записывает их в хранилище таблиц tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ec878-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Урок 4. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="ec878-150">Создание учетной записи хранения Azure и приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="ec878-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="ec878-151">Используйте toocreate шаблона диспетчера ресурсов Azure, приложение Azure функции и учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ec878-151">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="ec878-152">*Предполагаемое время toocomplete: 10 минут*</span><span class="sxs-lookup"><span data-stu-id="ec878-152">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="ec878-153">Go слишком[создать учетную запись хранилища Azure и Azure функции приложения](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="ec878-153">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="ec878-154">Чтение сообщений, сохраненных в Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="ec878-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="ec878-155">Они записываются в хранилище таблиц tooAzure наблюдать за сообщений hello шлюза в облако.</span><span class="sxs-lookup"><span data-stu-id="ec878-155">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="ec878-156">*Предполагаемое время toocomplete: 5 минут*</span><span class="sxs-lookup"><span data-stu-id="ec878-156">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="ec878-157">Go слишком[чтения сообщения сохраняются в хранилище таблиц Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ec878-157">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ec878-158">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="ec878-158">Troubleshooting</span></span>
<span data-ttu-id="ec878-159">Если у вас возникнут проблемы во время занятия hello поиск решений в hello [Устранение неполадок](iot-hub-gateway-kit-c-troubleshooting.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="ec878-159">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="ec878-160">Изучить подробнее</span><span class="sxs-lookup"><span data-stu-id="ec878-160">Explore more</span></span>
<span data-ttu-id="ec878-161">Посетите hello [Intel IoT шлюза для разработчика зоны](http://software.intel.com/iot/microsoft-azure) toolearn дополнительные.</span><span class="sxs-lookup"><span data-stu-id="ec878-161">Visit hello [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) toolearn more.</span></span>
