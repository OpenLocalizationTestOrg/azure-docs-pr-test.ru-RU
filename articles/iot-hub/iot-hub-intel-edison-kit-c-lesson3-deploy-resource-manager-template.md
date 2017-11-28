---
title: "Подключение Intel Edison (C) к Интернету вещей Azure. Урок 3. Создание приложения-функции | Документация Майкрософт"
description: "Приложение-функция Azure ожидает передачи событий Центра Интернета вещей Azure, обрабатывает входящие сообщения и записывает их в хранилище таблиц Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "хранение данных в облаке, данные, хранящиеся в облаке, облачная служба Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 739b82e9-5d4e-4485-8971-f57cbb682faf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30018cc2d03fc19c13625ef066989a89f21800e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="c552a-104">Создание приложения-функции Azure и учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="c552a-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="c552a-105">[Функции Azure](../../articles/azure-functions/functions-overview.md) — это решение для быстрого запуска *функций* (фрагментов кода) в облаке.</span><span class="sxs-lookup"><span data-stu-id="c552a-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="c552a-106">Выполнение функций в Azure производится с помощью приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="c552a-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="c552a-107">Ваши действия</span><span class="sxs-lookup"><span data-stu-id="c552a-107">What will you do</span></span>
<span data-ttu-id="c552a-108">С помощью шаблона Azure Resource Manager создайте приложение-функцию Azure и учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="c552a-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="c552a-109">Приложение-функция Azure ожидает передачи событий Центра Интернета вещей Azure, обрабатывает входящие сообщения и записывает их в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="c552a-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="c552a-110">Учетная запись хранения используется для чтения сохраненных копий сообщений из таблицы Azure.</span><span class="sxs-lookup"><span data-stu-id="c552a-110">The storage account is used for reading the persisted copies of messages from Azure table.</span></span> <span data-ttu-id="c552a-111">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c552a-111">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="c552a-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="c552a-112">What will you learn</span></span>
<span data-ttu-id="c552a-113">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="c552a-113">In this article, you will learn:</span></span>
* <span data-ttu-id="c552a-114">Использование [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) для развертывания ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="c552a-114">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="c552a-115">Использование приложения-функции Azure для обработки сообщений Центра Интернета вещей и их записи в таблицу в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="c552a-115">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="c552a-116">Требования</span><span class="sxs-lookup"><span data-stu-id="c552a-116">What do you need</span></span>
<span data-ttu-id="c552a-117">Необходимо успешно выполнить инструкции, изложенные в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="c552a-117">You must have successfully completed:</span></span>
- <span data-ttu-id="c552a-118">[Начало работы с Intel Edison (Node.js)][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="c552a-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="c552a-119">[Create your Azure IoT hub][create-your-azure-iot-hub] (Создание Центра Интернета вещей Azure)</span><span class="sxs-lookup"><span data-stu-id="c552a-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="c552a-120">Открытие примера приложения</span><span class="sxs-lookup"><span data-stu-id="c552a-120">Open the sample app</span></span>
<span data-ttu-id="c552a-121">Откройте пример проекта в Visual Studio Code, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c552a-121">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Структура репозитория][repo-structure]

* <span data-ttu-id="c552a-123">Файл во вложенной папке `app` — ключевой файл исходного кода.</span><span class="sxs-lookup"><span data-stu-id="c552a-123">The file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="c552a-124">Этот исходный файл содержит код для отправки сообщения 20 раз в центр Интернета вещей и мигания светодиода с каждым отправляемым сообщением.</span><span class="sxs-lookup"><span data-stu-id="c552a-124">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="c552a-125">Файл `arm-template.json` — шаблон Azure Resource Manager, содержащий приложение-функцию Azure и учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="c552a-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="c552a-126">Файл `arm-template-param.json` — файл конфигурации, используемый в шаблоне Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c552a-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="c552a-127">Вложенная папка `ReceiveDeviceMessages` содержит код Node.js для функции Azure.</span><span class="sxs-lookup"><span data-stu-id="c552a-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="c552a-128">Настройка шаблонов Azure Resource Manager и создание ресурсов в Azure</span><span class="sxs-lookup"><span data-stu-id="c552a-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="c552a-129">Обновите файл `arm-template-param.json` в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c552a-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Параметры шаблона Azure Resource Manager][arm-template-parameters]

* <span data-ttu-id="c552a-131">Замените **[your IoT Hub name]** своим **{именем центра}**, которое вы указали при [создании Центра Интернета вещей и регистрации Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="c552a-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="c552a-132">Замените **[строку-префикс для новых ресурсов]** любым префиксом по вашему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="c552a-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="c552a-133">Префикс обеспечивает глобальную уникальность имени ресурса во избежание конфликта.</span><span class="sxs-lookup"><span data-stu-id="c552a-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="c552a-134">Префикс не должен начинаться с дефиса или цифры.</span><span class="sxs-lookup"><span data-stu-id="c552a-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="c552a-135">После обновления файла `arm-template-param.json` разверните ресурсы в Azure, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c552a-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="c552a-136">Создание этих ресурсов занимает около пяти минут.</span><span class="sxs-lookup"><span data-stu-id="c552a-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="c552a-137">Пока ресурсы создаются, можно перейти к следующей статье.</span><span class="sxs-lookup"><span data-stu-id="c552a-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="c552a-138">Сводка</span><span class="sxs-lookup"><span data-stu-id="c552a-138">Summary</span></span>
<span data-ttu-id="c552a-139">Вы создали приложение-функцию Azure для обработки сообщений Центра Интернета вещей и учетную запись хранения Azure для хранения этих сообщений.</span><span class="sxs-lookup"><span data-stu-id="c552a-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="c552a-140">Теперь можно развернуть и запустить на устройстве Edison пример приложения для отправки сообщений c устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="c552a-140">You can now deploy and run the sample to send device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c552a-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c552a-141">Next steps</span></span>
<span data-ttu-id="c552a-142">[Run a sample application to send device-to-cloud messages][send-device-to-cloud-messages] (Запуск примера приложения для отправки сообщений с устройства в облако).</span><span class="sxs-lookup"><span data-stu-id="c552a-142">[Run a sample application to send device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-c-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure_c.png
[arm-template-parameters]: /media/iot-hub-intel-edison-lessons/lesson3/arm_para_c.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md