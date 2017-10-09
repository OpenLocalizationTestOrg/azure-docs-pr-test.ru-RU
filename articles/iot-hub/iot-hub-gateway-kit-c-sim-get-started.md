---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT | Документация Майкрософт"
description: "Приступая к работе с IoT шлюза начального набора, создать ваш центр Azure IoT Подключите концентратор IoT toohello шлюза"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure iot hub, шлюз iot, Приступая к работе с hello Интернет вещей, набор средств iot"
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
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="f4bbe-104">Приступая к работе с начальным набором шлюза Интернета вещей с имитацией устройства</span><span class="sxs-lookup"><span data-stu-id="f4bbe-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4bbe-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="f4bbe-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="f4bbe-106">Имитация устройства</span><span class="sxs-lookup"><span data-stu-id="f4bbe-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="f4bbe-107">В этом учебнике, начните с изучения hello основы работы с [IoT шлюза начального набора](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="f4bbe-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="f4bbe-108">Вы будете работать с Intel NUC под управлением Wind River Linux.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="f4bbe-109">Вы узнаете, как tooseamleesly подключаться toohello облачных устройств с помощью центра IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="f4bbe-110">**Нет начального набора?** Щелкните [здесь](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="f4bbe-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="f4bbe-111">Урок 1. Настройка NUC</span><span class="sxs-lookup"><span data-stu-id="f4bbe-111">Lesson 1: Configure your NUC</span></span>
![Урок 1. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="f4bbe-113">На этом занятии настроить NUC Intel (Далее единицы для вычисления) в hello Kit виде шлюза Azure IoT, установите пакет Azure IoT Edge hello на NUC и запуска шлюза функциональность tooverify hello образца приложения.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="f4bbe-114">*Предполагаемое время toocomplete: 15 минут*</span><span class="sxs-lookup"><span data-stu-id="f4bbe-114">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="f4bbe-115">Go слишком[Настройка NUC Intel виде шлюза IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="f4bbe-115">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="f4bbe-116">Урок 2. Создание Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f4bbe-116">Lesson 2: Create your IoT Hub</span></span>
![Урок 2. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="f4bbe-118">На этом занятии устанавливается hello средств и программного обеспечения на компьютере узла.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-118">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="f4bbe-119">Затем можно создать бесплатную учетную запись Azure, подготовки ваш центр Azure IoT и создания своим первым устройством в центр IoT hello.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="f4bbe-120">Прежде чем продолжать, завершите урок 1.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="f4bbe-121">Получить средства hello</span><span class="sxs-lookup"><span data-stu-id="f4bbe-121">Get hello tools</span></span>
<span data-ttu-id="f4bbe-122">На главном компьютере установите hello средств и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-122">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="f4bbe-123">*Предполагаемое время toocomplete: 20 минут*</span><span class="sxs-lookup"><span data-stu-id="f4bbe-123">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="f4bbe-124">Go слишком[средства hello](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="f4bbe-124">Go too[Get hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="f4bbe-125">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="f4bbe-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="f4bbe-126">Создание группы ресурсов, подготовки к первой центр Azure IoT и добавить вашего первого устройства toohello центр IoT с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-126">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="f4bbe-127">*Предполагаемое время toocomplete: 10 минут*</span><span class="sxs-lookup"><span data-stu-id="f4bbe-127">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="f4bbe-128">Go слишком[создать центр IoT и регистрация устройства](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="f4bbe-128">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="f4bbe-129">Занятие 3: Получение сообщений от устройств, имитация hello и чтение сообщений в концентратор IoT</span><span class="sxs-lookup"><span data-stu-id="f4bbe-129">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="f4bbe-130">На этом занятии будет использовать конфигурации hello tooautomate сценариев и выполнением приложения имитированное устройство шлюза.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-130">In this lesson, you will use scripts tooautomate hello configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="f4bbe-131">приложение Hello имитированное устройство создает температуры образец данных и отправляет его tooan IoT hub модуля.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-131">hello simulated device app generates sample temperature data and sends it tooan IoT hub module.</span></span> <span data-ttu-id="f4bbe-132">Здравствуйте, пакеты модуля концентратора IoT данных hello полученных и отправляет его центр IoT tooyour через шлюз платформы hello в Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-132">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Урок 3. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="f4bbe-134">Настройка и запуск имитации устройства</span><span class="sxs-lookup"><span data-stu-id="f4bbe-134">Configure and run a simulated device</span></span>
<span data-ttu-id="f4bbe-135">Подготовьте коды образец hello.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-135">Prepare hello sample codes.</span></span> <span data-ttu-id="f4bbe-136">Затем настроить и запустить пример приложения hello имитируемые устройства.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-136">Then configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="f4bbe-137">*Предполагаемое время toocomplete: 15 минут*</span><span class="sxs-lookup"><span data-stu-id="f4bbe-137">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="f4bbe-138">Go слишком[настроить и запустить имитированное устройство](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="f4bbe-138">Go too[Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="f4bbe-139">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f4bbe-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="f4bbe-140">Запустите образец кода на сообщения hello tooread компьютера узла из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-140">Run a sample code on your host computer tooread hello messages from your IoT hub.</span></span>

<span data-ttu-id="f4bbe-141">*Предполагаемое время toocomplete: 15 минут*</span><span class="sxs-lookup"><span data-stu-id="f4bbe-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="f4bbe-142">Go слишком[чтения сообщений из вашего центра IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="f4bbe-142">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="f4bbe-143">Урок 4: Сохранить сообщения tooAzure хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="f4bbe-143">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="f4bbe-144">Создайте приложение Azure функции, которое получает входящие сообщения от вашего центра IoT и записывает их в хранилище таблиц tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Урок 4. Сквозная схема](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="f4bbe-146">Создание учетной записи хранения Azure и приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="f4bbe-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="f4bbe-147">Используйте toocreate шаблона диспетчера ресурсов Azure, приложение Azure функции и учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-147">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="f4bbe-148">*Предполагаемое время toocomplete: 10 минут*</span><span class="sxs-lookup"><span data-stu-id="f4bbe-148">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="f4bbe-149">Go слишком[создать учетную запись хранилища Azure и Azure функции приложения](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="f4bbe-149">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="f4bbe-150">Чтение сообщений, сохраненных в Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="f4bbe-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="f4bbe-151">Они записываются в хранилище таблиц tooAzure наблюдать за сообщений hello шлюза в облако.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-151">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="f4bbe-152">*Предполагаемое время toocomplete: 5 минут*</span><span class="sxs-lookup"><span data-stu-id="f4bbe-152">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="f4bbe-153">Go слишком[чтения сообщения сохраняются в хранилище таблиц Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f4bbe-153">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f4bbe-154">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f4bbe-154">Troubleshooting</span></span>
<span data-ttu-id="f4bbe-155">Если у вас возникнут проблемы во время занятия hello поиск решений в hello [Устранение неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-155">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="f4bbe-156">Изучить подробнее</span><span class="sxs-lookup"><span data-stu-id="f4bbe-156">Explore more</span></span>
<span data-ttu-id="f4bbe-157">Посетите hello [Intel IoT шлюза для разработчика зоны](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn дополнительные.</span><span class="sxs-lookup"><span data-stu-id="f4bbe-157">Visit hello [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn more.</span></span>
