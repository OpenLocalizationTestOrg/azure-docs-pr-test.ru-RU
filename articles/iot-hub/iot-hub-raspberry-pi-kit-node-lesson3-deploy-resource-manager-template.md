---
title: "Подключение Raspberry Pi (Node) к Интернету вещей Azure. Урок 3. Развертывание шаблона | Документация Майкрософт"
description: "Приложение-функция Azure ожидает передачи событий Центра Интернета вещей Azure, обрабатывает входящие сообщения и записывает их в хранилище таблиц Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "хранение данных в облаке, данные, хранящиеся в облаке, облачная служба Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44901faea37a847a418e6d2b4097302cdb610495
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="17b57-104">Создание приложения-функции Azure и учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="17b57-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="17b57-105">[Функции Azure](../azure-functions/functions-overview.md) — это решение для быстрого запуска *функций* (фрагментов кода) в облаке.</span><span class="sxs-lookup"><span data-stu-id="17b57-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="17b57-106">Выполнение функций в Azure производится с помощью приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="17b57-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="17b57-107">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="17b57-107">What you will do</span></span>
<span data-ttu-id="17b57-108">С помощью шаблона Azure Resource Manager создайте приложение-функцию Azure и учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="17b57-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="17b57-109">Приложение-функция Azure ожидает передачи событий Центра Интернета вещей Azure, обрабатывает входящие сообщения и записывает их в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="17b57-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="17b57-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="17b57-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="17b57-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="17b57-111">What you will learn</span></span>
<span data-ttu-id="17b57-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="17b57-112">In this article, you will learn:</span></span>

* <span data-ttu-id="17b57-113">Использование [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) для развертывания ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="17b57-113">How to use [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="17b57-114">Использование приложения-функции Azure для обработки сообщений Центра Интернета вещей и их записи в таблицу в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="17b57-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="17b57-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="17b57-115">What you need</span></span>
<span data-ttu-id="17b57-116">Необходимо успешно выполнить инструкции, изложенные в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="17b57-116">You must have successfully completed:</span></span>
* <span data-ttu-id="17b57-117">[Get started with Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md) (Приступая к работе с Raspberry Pi 3)</span><span class="sxs-lookup"><span data-stu-id="17b57-117">[Get started with Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md)</span></span>
* <span data-ttu-id="17b57-118">[Create your Azure IoT hub](iot-hub-raspberry-pi-kit-node-get-started.md) (Создание Центра Интернета вещей Azure)</span><span class="sxs-lookup"><span data-stu-id="17b57-118">[Create your Azure IoT hub](iot-hub-raspberry-pi-kit-node-get-started.md)</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="17b57-119">Открытие примера приложения</span><span class="sxs-lookup"><span data-stu-id="17b57-119">Open the sample app</span></span>
<span data-ttu-id="17b57-120">Откройте пример проекта в Visual Studio Code, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="17b57-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Структура репозитория](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="17b57-122">Файл `app.js` во вложенной папке `app` — ключевой файл исходного кода.</span><span class="sxs-lookup"><span data-stu-id="17b57-122">The `app.js` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="17b57-123">Этот исходный файл содержит код для отправки сообщения 20 раз в центр Интернета вещей и мигания светодиода с каждым отправляемым сообщением.</span><span class="sxs-lookup"><span data-stu-id="17b57-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="17b57-124">Файл `arm-template.json` — шаблон Azure Resource Manager, содержащий приложение-функцию Azure и учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="17b57-124">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="17b57-125">Файл `arm-template-param.json` — файл конфигурации, используемый в шаблоне Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="17b57-125">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="17b57-126">Вложенная папка `ReceiveDeviceMessages` содержит код Node.js для функции Azure.</span><span class="sxs-lookup"><span data-stu-id="17b57-126">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="17b57-127">Настройка шаблонов Azure Resource Manager и создание ресурсов в Azure</span><span class="sxs-lookup"><span data-stu-id="17b57-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="17b57-128">Обновите файл `arm-template-param.json` в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="17b57-128">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Параметры шаблона Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="17b57-130">Замените **[your IoT Hub name]** своим **{именем центра}**, которое вы указали при [создании Центра Интернета вещей и регистрации Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="17b57-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="17b57-131">Замените **[строку-префикс для новых ресурсов]** любым префиксом по вашему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="17b57-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="17b57-132">Префикс обеспечивает глобальную уникальность имени ресурса во избежание конфликта.</span><span class="sxs-lookup"><span data-stu-id="17b57-132">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="17b57-133">Префикс не должен начинаться с дефиса или цифры.</span><span class="sxs-lookup"><span data-stu-id="17b57-133">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="17b57-134">После обновления файла `arm-template-param.json` разверните ресурсы в Azure, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="17b57-134">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="17b57-135">Создание этих ресурсов занимает около пяти минут.</span><span class="sxs-lookup"><span data-stu-id="17b57-135">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="17b57-136">Пока ресурсы создаются, можно перейти к следующей статье.</span><span class="sxs-lookup"><span data-stu-id="17b57-136">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="17b57-137">Сводка</span><span class="sxs-lookup"><span data-stu-id="17b57-137">Summary</span></span>
<span data-ttu-id="17b57-138">Вы создали приложение-функцию Azure для обработки сообщений Центра Интернета вещей и учетную запись хранения Azure для хранения этих сообщений.</span><span class="sxs-lookup"><span data-stu-id="17b57-138">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="17b57-139">Теперь можно развернуть и запустить на устройстве Pi пример приложения для отправки сообщений c устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="17b57-139">You can now deploy and run the sample to send device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17b57-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17b57-140">Next steps</span></span>
<span data-ttu-id="17b57-141">[Run a sample application to send device-to-cloud messages on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md) (Запуск примера приложения для отправки сообщений с устройства в облако на Raspberry Pi 3)</span><span class="sxs-lookup"><span data-stu-id="17b57-141">[Run a sample application to send device-to-cloud messages on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)</span></span>

