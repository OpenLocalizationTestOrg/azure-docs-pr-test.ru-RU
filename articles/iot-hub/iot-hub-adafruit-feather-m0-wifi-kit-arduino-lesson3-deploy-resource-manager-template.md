---
title: "Connect Arduino (C) tooAzure IoT — занятия 3: шаблон-развертывание | Документы Microsoft"
description: "приложение Azure функции Hello прослушивает события концентратора IoT tooAzure, обрабатывает входящие сообщения и записывает их в хранилище таблиц tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "хранение данных в облаке hello, данные, хранящиеся в облаке, iot облачной службы"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9c8f4cd1-9511-4601-ad7e-51761a986753
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6a84a6d3c5263a85c8997cf69fe446d73ab7a5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="ca01f-104">Создание приложения-функции Azure и учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="ca01f-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="ca01f-105">[Функции Azure](../../articles/azure-functions/functions-overview.md) — это решение для запуска легко *функции* (небольшие части кода) в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="ca01f-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="ca01f-106">Приложение Azure функция размещает hello выполнение функций в Azure.</span><span class="sxs-lookup"><span data-stu-id="ca01f-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="ca01f-107">Ваши действия</span><span class="sxs-lookup"><span data-stu-id="ca01f-107">What will you do</span></span>
<span data-ttu-id="ca01f-108">Используйте toocreate шаблона диспетчера ресурсов Azure, приложение Azure функции и учетная запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ca01f-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="ca01f-109">приложение Azure функции Hello прослушивает события концентратора IoT tooAzure, обрабатывает входящие сообщения и записывает их в хранилище таблиц tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ca01f-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="ca01f-110">Если у вас возникнут проблемы, искать решения на hello [страницу плата Adafruit Растушевка M0 Wi-Fi Arduino устранения неполадок](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ca01f-110">If you have any problems, look for solutions on hello [troubleshooting page for your Adafruit Feather M0 WiFi Arduino board](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="ca01f-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="ca01f-111">What will you learn</span></span>
<span data-ttu-id="ca01f-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="ca01f-112">In this article, you will learn:</span></span>
* <span data-ttu-id="ca01f-113">Как toouse [диспетчера ресурсов Azure](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ca01f-113">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="ca01f-114">Как toouse Azure функцией приложения tooprocess IoT hub сообщения и записывать их в таблице tooa в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="ca01f-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="ca01f-115">Требования</span><span class="sxs-lookup"><span data-stu-id="ca01f-115">What do you need</span></span>
<span data-ttu-id="ca01f-116">Необходимо успешно выполнить инструкции, изложенные в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="ca01f-116">You must have successfully completed:</span></span>
- <span data-ttu-id="ca01f-117">[Приступая к работе с платой Arduino: Adafruit Feather M0 Wi-Fi][get-started]</span><span class="sxs-lookup"><span data-stu-id="ca01f-117">[Get started with your Arduino board][get-started]</span></span>
- <span data-ttu-id="ca01f-118">[Create your Azure IoT hub][create-iot-hub] (Создание Центра Интернета вещей Azure)</span><span class="sxs-lookup"><span data-stu-id="ca01f-118">[Create your Azure IoT hub][create-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="ca01f-119">Пример приложения Open hello</span><span class="sxs-lookup"><span data-stu-id="ca01f-119">Open hello sample app</span></span>
<span data-ttu-id="ca01f-120">Откройте образец hello проекта в Visual Studio Code, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="ca01f-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Структура репозитория][repo-structure]

* <span data-ttu-id="ca01f-122">Hello `app.ino` файла в hello `app` подпапка является hello ключа исходного файла.</span><span class="sxs-lookup"><span data-stu-id="ca01f-122">hello `app.ino` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="ca01f-123">Этот исходный файл содержит код hello toosend сообщение 20 раз tooyour IoT hub и blink hello Индикатора для каждого сообщения, он отправляет.</span><span class="sxs-lookup"><span data-stu-id="ca01f-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="ca01f-124">Hello `config.json` содержит необходимые параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ca01f-124">hello `config.json` contains required configuration settings.</span></span>
* <span data-ttu-id="ca01f-125">Hello `arm-template.json` файла является шаблон hello диспетчера ресурсов Azure, который содержит приложение Azure функции и учетная запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ca01f-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="ca01f-126">Hello `arm-template-param.json` файл является файлом конфигурации hello, используемые hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ca01f-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="ca01f-127">Hello `ReceiveDeviceMessages` вложенная папка содержит код Node.js hello Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="ca01f-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="ca01f-128">Настройка шаблонов Azure Resource Manager и создание ресурсов в Azure</span><span class="sxs-lookup"><span data-stu-id="ca01f-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="ca01f-129">Обновление hello `arm-template-param.json` файл в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ca01f-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Параметры шаблона Azure Resource Manager][arm-template-params]

* <span data-ttu-id="ca01f-131">Замените **[your IoT Hub name]** своим именем Центра Интернета вещей (это значение **{my hub name}**, которое вы указали при [создании Центра Интернета вещей и регистрации платы Arduino][created-iot-hub-and-registered-arduino-board]).</span><span class="sxs-lookup"><span data-stu-id="ca01f-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered your Arduino board][created-iot-hub-and-registered-arduino-board].</span></span>
* <span data-ttu-id="ca01f-132">Замените **[строку-префикс для новых ресурсов]** любым префиксом по вашему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="ca01f-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="ca01f-133">префикс Hello гарантирует, что имя ресурса hello является глобально уникальным tooavoid конфликт.</span><span class="sxs-lookup"><span data-stu-id="ca01f-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="ca01f-134">Не используйте символы дефиса или номер начальной hello префикса.</span><span class="sxs-lookup"><span data-stu-id="ca01f-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="ca01f-135">После обновления hello `arm-template-param.json` файлов, развертывание, выполнив следующую команду hello tooAzure ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="ca01f-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="ca01f-136">Занимает около пяти минут toocreate эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ca01f-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="ca01f-137">Во время создания ресурса hello можно переместить в следующей статье toohello.</span><span class="sxs-lookup"><span data-stu-id="ca01f-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="ca01f-138">Сводка</span><span class="sxs-lookup"><span data-stu-id="ca01f-138">Summary</span></span>
<span data-ttu-id="ca01f-139">Вы создали вашей tooprocess приложения Azure функция IoT hub сообщений и учетной записи хранилища Azure toostore эти сообщения.</span><span class="sxs-lookup"><span data-stu-id="ca01f-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="ca01f-140">Теперь можно развернуть и запустить сообщения из устройства в облако toosend образец hello в Arduino на доске.</span><span class="sxs-lookup"><span data-stu-id="ca01f-140">You can now deploy and run hello sample toosend device-to-cloud messages on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca01f-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca01f-141">Next steps</span></span>
<span data-ttu-id="ca01f-142">[Запустите образец приложения toosend сообщения из устройства в облако на доске Arduino][send-device-to-cloud-messages]</span><span class="sxs-lookup"><span data-stu-id="ca01f-142">[Run a sample application toosend device-to-cloud messages on your Arduino board][send-device-to-cloud-messages]</span></span>

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md