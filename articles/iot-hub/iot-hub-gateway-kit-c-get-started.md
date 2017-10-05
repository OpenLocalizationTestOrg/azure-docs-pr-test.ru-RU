---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT | Документация Майкрософт"
description: "Приступая к работе с начальным набором для шлюза Azure IoT, создание Центра Интернета вещей Azure и подключение шлюза и SensorTag к Центру Интернета вещей"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Центр Интернета вещей Azure, шлюз Интернета вещей, приступая к работе с Интернетом вещей, инструментарий Интернета вещей"
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
ms.openlocfilehash: 624bdc7877d5048da08897f868272fd8e8f3f7b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="8ddd1-104">Приступая к работе с начальным набором шлюза Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="8ddd1-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ddd1-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="8ddd1-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="8ddd1-106">Имитация устройства</span><span class="sxs-lookup"><span data-stu-id="8ddd1-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="8ddd1-107">В этом руководстве вы начнете с того, что узнаете основы работы с [начальным набором для шлюза Интернета вещей](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="8ddd1-108">Вы будете работать с Intel NUC под управлением Wind River Linux и устройством [SensorTag от Texas Instruments](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-108">You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="8ddd1-109">Кроме того, вы узнаете, как можно легко подключать устройства к облаку с помощью Центра Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="8ddd1-110">**Нет начального набора?** Щелкните [здесь](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="8ddd1-111">**Нет SensorTag?** [Начните имитацию устройства](iot-hub-gateway-kit-c-sim-get-started.md) или [купите SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="8ddd1-112">Урок 1. Настройка NUC</span><span class="sxs-lookup"><span data-stu-id="8ddd1-112">Lesson 1: Configure your NUC</span></span>
![Урок 1. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="8ddd1-114">На этом уроке вы настроите Intel NUC (Next Unit of Computing) из набора в качестве шлюза Интернета вещей Azure, установите пакет Edge Интернета вещей Azure на NUC и запустите пример приложения, чтобы проверить работоспособность шлюза.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="8ddd1-115">*Предполагаемое время выполнения: 15 минут.*</span><span class="sxs-lookup"><span data-stu-id="8ddd1-115">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="8ddd1-116">Перейдите к статье [Настройка Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-116">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="8ddd1-117">Урок 2. Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="8ddd1-117">Lesson 2: Create your IoT Hub</span></span>
![Урок 2. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="8ddd1-119">В ходе этого урока вы установите инструменты и программное обеспечение на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-119">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="8ddd1-120">Затем создадите бесплатную учетную запись Azure, подготовите Центр Интернета вещей Azure и создадите в нем первое устройство.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="8ddd1-121">Прежде чем продолжать, завершите урок 1.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="8ddd1-122">Получить инструменты</span><span class="sxs-lookup"><span data-stu-id="8ddd1-122">Get the tools</span></span>
<span data-ttu-id="8ddd1-123">Установите инструменты и программное обеспечение на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-123">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="8ddd1-124">*Предполагаемое время выполнения: 20 минут*</span><span class="sxs-lookup"><span data-stu-id="8ddd1-124">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="8ddd1-125">Ознакомьтесь со статьей [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md) (Получение инструментов).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-125">Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="8ddd1-126">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="8ddd1-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="8ddd1-127">Создайте группу ресурсов, подготовьте Центр Интернета вещей Azure и добавьте в него первое устройство, используя Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-127">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="8ddd1-128">*Предполагаемое время выполнения: 10 минут*</span><span class="sxs-lookup"><span data-stu-id="8ddd1-128">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="8ddd1-129">Перейдите к разделу [Создание Центра Интернета вещей и регистрация устройства](iot-hub-gateway-kit-c-lesson2-register-device.md).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-129">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="8ddd1-130">Урок 3. Получение сообщений из SensorTag и чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="8ddd1-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="8ddd1-131">На этом уроке вы будете использовать сценарии для автоматизации настройки и выполнения примера приложения BLE в шлюзе.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-131">In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="8ddd1-132">Такие приложения используют коллекцию модулей для агрегации и преобразования данных, обработки команд или для выполнения любого количества связанных задач.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-132">Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="8ddd1-133">Модули взаимодействуют друг с другом через брокер сообщений.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="8ddd1-134">Пример приложения содержит модуль BLE и Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-134">The sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="8ddd1-135">Модуль BLE получает данные из SensorTag BLE.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-135">The BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="8ddd1-136">Модуль Центра Интернета вещей упаковывает полученные данные и отправляет их в Центр Интернета вещей через платформу шлюза, предоставленную в Edge Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-136">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Урок 3. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-the-ble-sample-app"></a><span data-ttu-id="8ddd1-138">Настройка и запуск примера приложения BLE</span><span class="sxs-lookup"><span data-stu-id="8ddd1-138">Configure and run the BLE sample app</span></span>
<span data-ttu-id="8ddd1-139">Настройте подключение между SensorTag и шлюзом.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-139">Set up the connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="8ddd1-140">Затем завершите настройку и запустите пример приложения BLE.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-140">Then finish the configuration and run the BLE sample application.</span></span>

<span data-ttu-id="8ddd1-141">*Предполагаемое время выполнения: 15 минут.*</span><span class="sxs-lookup"><span data-stu-id="8ddd1-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="8ddd1-142">Перейдите к статье [Настройка и запуск примера приложения BLE](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-142">Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="8ddd1-143">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="8ddd1-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="8ddd1-144">Запустите пример кода на главном компьютере для чтения сообщений из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-144">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="8ddd1-145">*Предполагаемое время выполнения: 15 минут.*</span><span class="sxs-lookup"><span data-stu-id="8ddd1-145">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="8ddd1-146">Перейдите к статье [Чтение сообщений из Центра Интернета вещей](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-146">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="8ddd1-147">Урок 4. Сохранение сообщений в Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="8ddd1-147">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="8ddd1-148">Создайте приложение-функцию Azure, которое получает входящие сообщения из Центра Интернета вещей и записывает их в Хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Урок 4. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="8ddd1-150">Создание учетной записи хранения Azure и приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="8ddd1-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="8ddd1-151">С помощью шаблона Azure Resource Manager создайте приложение-функцию Azure и учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-151">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="8ddd1-152">*Предполагаемое время выполнения: 10 минут*</span><span class="sxs-lookup"><span data-stu-id="8ddd1-152">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="8ddd1-153">Перейдите к статье [Создание приложения-функции Azure и учетной записи хранения Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-153">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="8ddd1-154">Чтение сообщений, сохраненных в Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="8ddd1-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="8ddd1-155">Отслеживайте сообщения, передаваемые из шлюза в облако, по мере их записывания в Хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="8ddd1-155">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="8ddd1-156">*Предполагаемое время выполнения: 5 минут*</span><span class="sxs-lookup"><span data-stu-id="8ddd1-156">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="8ddd1-157">Ознакомьтесь со статьей [Чтение сообщений, сохраненных в Хранилище таблиц Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-157">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8ddd1-158">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="8ddd1-158">Troubleshooting</span></span>
<span data-ttu-id="8ddd1-159">Если в ходе какого-либо урока у вас возникнут проблемы, то решение можно найти в статье [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) (Устранение неполадок).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-159">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="8ddd1-160">Изучить подробнее</span><span class="sxs-lookup"><span data-stu-id="8ddd1-160">Explore more</span></span>
<span data-ttu-id="8ddd1-161">Дополнительные сведения см. на странице сообщества [Developer Zone комплекта Intel IoT Gateway](http://software.intel.com/iot/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="8ddd1-161">Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.</span></span>