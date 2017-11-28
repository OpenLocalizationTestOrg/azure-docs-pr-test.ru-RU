---
title: "Подключение Raspberry Pi (узел) tooAzure IoT — занятия 3: шаблон-развертывание | Документы Microsoft"
description: "приложение Azure функции Hello прослушивает события концентратора IoT tooAzure, обрабатывает входящие сообщения и записывает их в хранилище таблиц tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "хранение данных в облаке hello, данные, хранящиеся в облаке, iot облачной службы"
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
ms.openlocfilehash: b6c0a9530cb80e3f78c0e96037f6f3942b602aea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="e1bbb-104">Создание приложения-функции Azure и учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="e1bbb-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="e1bbb-105">[Функции Azure](../azure-functions/functions-overview.md) — это решение для запуска легко *функции* (небольшие части кода) в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="e1bbb-106">Приложение Azure функция размещает hello выполнение функций в Azure.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e1bbb-107">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="e1bbb-107">What you will do</span></span>
<span data-ttu-id="e1bbb-108">Используйте toocreate шаблона диспетчера ресурсов Azure, приложение Azure функции и учетная запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="e1bbb-109">приложение Azure функции Hello прослушивает события концентратора IoT tooAzure, обрабатывает входящие сообщения и записывает их в хранилище таблиц tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="e1bbb-110">Если у вас возникнут проблемы, поиска решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e1bbb-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e1bbb-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="e1bbb-111">What you will learn</span></span>
<span data-ttu-id="e1bbb-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="e1bbb-112">In this article, you will learn:</span></span>

* <span data-ttu-id="e1bbb-113">Как toouse [диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md) toodeploy Azure ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-113">How toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="e1bbb-114">Как toouse Azure функцией приложения tooprocess IoT hub сообщения и записывать их в таблице tooa в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e1bbb-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="e1bbb-115">What you need</span></span>
<span data-ttu-id="e1bbb-116">Необходимо успешно выполнить инструкции, изложенные в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="e1bbb-116">You must have successfully completed:</span></span>
* <span data-ttu-id="e1bbb-117">[Get started with Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md) (Приступая к работе с Raspberry Pi 3)</span><span class="sxs-lookup"><span data-stu-id="e1bbb-117">[Get started with Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md)</span></span>
* <span data-ttu-id="e1bbb-118">[Create your Azure IoT hub](iot-hub-raspberry-pi-kit-node-get-started.md) (Создание Центра Интернета вещей Azure)</span><span class="sxs-lookup"><span data-stu-id="e1bbb-118">[Create your Azure IoT hub](iot-hub-raspberry-pi-kit-node-get-started.md)</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="e1bbb-119">Пример приложения Open hello</span><span class="sxs-lookup"><span data-stu-id="e1bbb-119">Open hello sample app</span></span>
<span data-ttu-id="e1bbb-120">Откройте образец hello проекта в Visual Studio Code, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="e1bbb-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Структура репозитория](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="e1bbb-122">Hello `app.js` файла в hello `app` подпапка является hello ключа исходного файла.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-122">hello `app.js` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="e1bbb-123">Этот исходный файл содержит код hello toosend сообщение 20 раз tooyour IoT hub и blink hello Индикатора для каждого сообщения, он отправляет.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="e1bbb-124">Hello `arm-template.json` файла является шаблон hello диспетчера ресурсов Azure, который содержит приложение Azure функции и учетная запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-124">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="e1bbb-125">Hello `arm-template-param.json` файл является файлом конфигурации hello, используемые hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-125">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="e1bbb-126">Hello `ReceiveDeviceMessages` вложенная папка содержит код Node.js hello Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-126">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="e1bbb-127">Настройка шаблонов Azure Resource Manager и создание ресурсов в Azure</span><span class="sxs-lookup"><span data-stu-id="e1bbb-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="e1bbb-128">Обновление hello `arm-template-param.json` файл в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-128">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Параметры шаблона Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="e1bbb-130">Замените **[your IoT Hub name]** своим **{именем центра}**, которое вы указали при [создании Центра Интернета вещей и регистрации Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="e1bbb-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="e1bbb-131">Замените **[строку-префикс для новых ресурсов]** любым префиксом по вашему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="e1bbb-132">префикс Hello гарантирует, что имя ресурса hello является глобально уникальным tooavoid конфликт.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-132">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="e1bbb-133">Не используйте символы дефиса или номер начальной hello префикса.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-133">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="e1bbb-134">После обновления hello `arm-template-param.json` файлов, развертывание, выполнив следующую команду hello tooAzure ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="e1bbb-134">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="e1bbb-135">Занимает около пяти минут toocreate эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-135">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="e1bbb-136">Во время создания ресурса hello можно переместить в следующей статье toohello.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-136">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="e1bbb-137">Сводка</span><span class="sxs-lookup"><span data-stu-id="e1bbb-137">Summary</span></span>
<span data-ttu-id="e1bbb-138">Вы создали вашей tooprocess приложения Azure функция IoT hub сообщений и учетной записи хранилища Azure toostore эти сообщения.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-138">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="e1bbb-139">Теперь можно развернуть и запустить сообщения из устройства в облако toosend образец hello на Pi.</span><span class="sxs-lookup"><span data-stu-id="e1bbb-139">You can now deploy and run hello sample toosend device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1bbb-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1bbb-140">Next steps</span></span>
[<span data-ttu-id="e1bbb-141">Запустите образец приложения toosend сообщения из устройства в облако на Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="e1bbb-141">Run a sample application toosend device-to-cloud messages on Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

