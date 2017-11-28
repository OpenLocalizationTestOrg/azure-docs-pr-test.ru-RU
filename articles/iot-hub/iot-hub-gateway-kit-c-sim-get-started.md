---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT | Документация Майкрософт"
description: "Приступите к работе с начальным набором для шлюза Azure IoT, создайте Центр Интернета вещей Azure и подключите шлюз к нему"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Центр Интернета вещей Azure, шлюз Интернета вещей, приступая к работе с Интернетом вещей, инструментарий Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 916fa40d9ac857dfa72197b40c232834593d3891
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="bc09f-104">Приступая к работе с начальным набором шлюза Интернета вещей с имитацией устройства</span><span class="sxs-lookup"><span data-stu-id="bc09f-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc09f-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="bc09f-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="bc09f-106">Имитация устройства</span><span class="sxs-lookup"><span data-stu-id="bc09f-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="bc09f-107">В этом руководстве вы начнете с того, что узнаете основы работы с [начальным набором для шлюза Интернета вещей](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="bc09f-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="bc09f-108">Вы будете работать с Intel NUC под управлением Wind River Linux.</span><span class="sxs-lookup"><span data-stu-id="bc09f-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="bc09f-109">Кроме того, вы узнаете, как можно легко подключать устройства к облаку с помощью Центра Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="bc09f-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="bc09f-110">**Нет начального набора?** Щелкните [здесь](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="bc09f-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="bc09f-111">Урок 1. Настройка NUC</span><span class="sxs-lookup"><span data-stu-id="bc09f-111">Lesson 1: Configure your NUC</span></span>
![Урок 1. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="bc09f-113">На этом уроке вы настроите Intel NUC (Next Unit of Computing) из набора в качестве шлюза Интернета вещей Azure, установите пакет Edge Интернета вещей Azure на NUC и запустите пример приложения, чтобы проверить работоспособность шлюза.</span><span class="sxs-lookup"><span data-stu-id="bc09f-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="bc09f-114">*Предполагаемое время выполнения: 15 минут.*</span><span class="sxs-lookup"><span data-stu-id="bc09f-114">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="bc09f-115">Перейдите к статье [Настройка Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="bc09f-115">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="bc09f-116">Урок 2. Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="bc09f-116">Lesson 2: Create your IoT Hub</span></span>
![Урок 2. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="bc09f-118">В ходе этого урока вы установите инструменты и программное обеспечение на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="bc09f-118">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="bc09f-119">Затем создадите бесплатную учетную запись Azure, подготовите Центр Интернета вещей Azure и создадите в нем первое устройство.</span><span class="sxs-lookup"><span data-stu-id="bc09f-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="bc09f-120">Прежде чем продолжать, завершите урок 1.</span><span class="sxs-lookup"><span data-stu-id="bc09f-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="bc09f-121">Получить инструменты</span><span class="sxs-lookup"><span data-stu-id="bc09f-121">Get the tools</span></span>
<span data-ttu-id="bc09f-122">Установите инструменты и программное обеспечение на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="bc09f-122">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="bc09f-123">*Предполагаемое время выполнения: 20 минут*</span><span class="sxs-lookup"><span data-stu-id="bc09f-123">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="bc09f-124">Ознакомьтесь со статьей [Get the tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md) (Получение инструментов).</span><span class="sxs-lookup"><span data-stu-id="bc09f-124">Go to [Get the tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="bc09f-125">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="bc09f-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="bc09f-126">Создайте группу ресурсов, подготовьте Центр Интернета вещей Azure и добавьте в него первое устройство, используя Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bc09f-126">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="bc09f-127">*Предполагаемое время выполнения: 10 минут*</span><span class="sxs-lookup"><span data-stu-id="bc09f-127">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="bc09f-128">Перейдите к разделу [Создание Центра Интернета вещей и регистрация устройства](iot-hub-gateway-kit-c-sim-lesson2-register-device.md).</span><span class="sxs-lookup"><span data-stu-id="bc09f-128">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-the-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="bc09f-129">Урок 3. Получение сообщений из имитации устройства и чтение сообщений из вашего Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="bc09f-129">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="bc09f-130">В ходе этого урока вы используете сценарии для автоматизации настройки и выполнения приложения для имитации устройства в шлюзе.</span><span class="sxs-lookup"><span data-stu-id="bc09f-130">In this lesson, you will use scripts to automate the configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="bc09f-131">Приложение для имитации устройства создает пример данных температуры и отправляет его в модуль Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="bc09f-131">The simulated device app generates sample temperature data and sends it to an IoT hub module.</span></span> <span data-ttu-id="bc09f-132">Модуль Центра Интернета вещей упаковывает полученные данные и отправляет их в Центр Интернета вещей через платформу шлюза, предоставленную в Edge Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="bc09f-132">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Урок 3. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="bc09f-134">Настройка и запуск имитации устройства</span><span class="sxs-lookup"><span data-stu-id="bc09f-134">Configure and run a simulated device</span></span>
<span data-ttu-id="bc09f-135">Подготовьте примеры кодов.</span><span class="sxs-lookup"><span data-stu-id="bc09f-135">Prepare the sample codes.</span></span> <span data-ttu-id="bc09f-136">Затем настройте и запустите пример приложения для имитации устройства.</span><span class="sxs-lookup"><span data-stu-id="bc09f-136">Then configure and run the simulated device sample application.</span></span>

<span data-ttu-id="bc09f-137">*Предполагаемое время выполнения: 15 минут.*</span><span class="sxs-lookup"><span data-stu-id="bc09f-137">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="bc09f-138">Перейдите к статье [Настройка и запуск имитации устройства](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="bc09f-138">Go to [Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="bc09f-139">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="bc09f-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="bc09f-140">Запустите пример кода на главном компьютере для чтения сообщений из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="bc09f-140">Run a sample code on your host computer to read the messages from your IoT hub.</span></span>

<span data-ttu-id="bc09f-141">*Предполагаемое время выполнения: 15 минут.*</span><span class="sxs-lookup"><span data-stu-id="bc09f-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="bc09f-142">Перейдите к статье [Чтение сообщений из Центра Интернета вещей](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="bc09f-142">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="bc09f-143">Урок 4. Сохранение сообщений в Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="bc09f-143">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="bc09f-144">Создайте приложение-функцию Azure, которое получает входящие сообщения из Центра Интернета вещей и записывает их в Хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="bc09f-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Урок 4. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="bc09f-146">Создание учетной записи хранения Azure и приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="bc09f-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="bc09f-147">С помощью шаблона Azure Resource Manager создайте приложение-функцию Azure и учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="bc09f-147">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="bc09f-148">*Предполагаемое время выполнения: 10 минут*</span><span class="sxs-lookup"><span data-stu-id="bc09f-148">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="bc09f-149">Перейдите к статье [Создание приложения-функции Azure и учетной записи хранения Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="bc09f-149">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="bc09f-150">Чтение сообщений, сохраненных в Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="bc09f-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="bc09f-151">Отслеживайте сообщения, передаваемые из шлюза в облако, по мере их записывания в Хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="bc09f-151">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="bc09f-152">*Предполагаемое время выполнения: 5 минут*</span><span class="sxs-lookup"><span data-stu-id="bc09f-152">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="bc09f-153">Ознакомьтесь со статьей [Чтение сообщений, сохраненных в Хранилище таблиц Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="bc09f-153">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bc09f-154">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="bc09f-154">Troubleshooting</span></span>
<span data-ttu-id="bc09f-155">Если в ходе какого-либо урока у вас возникнут проблемы, то решение можно найти в статье [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) (Устранение неполадок).</span><span class="sxs-lookup"><span data-stu-id="bc09f-155">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="bc09f-156">Изучить подробнее</span><span class="sxs-lookup"><span data-stu-id="bc09f-156">Explore more</span></span>
<span data-ttu-id="bc09f-157">Дополнительные сведения см. на странице сообщества [Developer Zone комплекта Intel IoT Gateway](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit).</span><span class="sxs-lookup"><span data-stu-id="bc09f-157">Visit the [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) to learn more.</span></span>