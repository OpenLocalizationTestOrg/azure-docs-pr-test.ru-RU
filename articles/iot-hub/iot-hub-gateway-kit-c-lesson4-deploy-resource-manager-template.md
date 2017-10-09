---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 4. Создание приложения-функции | Документация Майкрософт"
description: "Сохранять сообщения из центра IoT tooyour Intel NUC, записывать их в хранилище таблиц tooAzure и затем прочитать их из облака hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "хранение данных в облаке hello, данные, хранящиеся в облаке, iot облачной службы"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="57b67-104">Создание приложения-функции Azure и учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="57b67-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="57b67-105">Функции Azure — это решение для запуска легко _функции_ (небольшие части кода) в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="57b67-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="57b67-106">Приложение Azure функция размещает hello выполнение функций в Azure.</span><span class="sxs-lookup"><span data-stu-id="57b67-106">An Azure function app hosts hello execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="57b67-107">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="57b67-107">What you will do</span></span>

- <span data-ttu-id="57b67-108">Используйте toocreate шаблона диспетчера ресурсов Azure, приложение Azure функции и учетная запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="57b67-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="57b67-109">приложение Azure функции Hello прослушивает события концентратора IoT tooAzure, обрабатывает входящие сообщения и записывает их в хранилище таблиц tooAzure.</span><span class="sxs-lookup"><span data-stu-id="57b67-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="57b67-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="57b67-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="57b67-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="57b67-111">What you will learn</span></span>

<span data-ttu-id="57b67-112">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="57b67-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="57b67-113">Как Azure Resource Manager toodeploy toouse ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="57b67-113">How toouse Azure Resource Manager toodeploy Azure resources.</span></span>
- <span data-ttu-id="57b67-114">Как toouse Azure функцией tooprocess приложения центра IoT сообщения и записи таблицы tooa в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="57b67-114">How toouse an Azure function app tooprocess IoT Hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="57b67-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="57b67-115">What you need</span></span>

<span data-ttu-id="57b67-116">Необходимо успешно выполнить предыдущие занятия hello:</span><span class="sxs-lookup"><span data-stu-id="57b67-116">You must have successfully completed hello previous lessons:</span></span>

- [<span data-ttu-id="57b67-117">Урок 1. Настройка Intel NUC в качестве шлюза Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="57b67-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [<span data-ttu-id="57b67-118">Урок 2. Подготовка главного компьютера и Центра Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="57b67-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="57b67-119">Урок 3. Получение сообщений из SensorTag и чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="57b67-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="57b67-120">Открытие примера приложения</span><span class="sxs-lookup"><span data-stu-id="57b67-120">Open a sample app</span></span>

<span data-ttu-id="57b67-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` репозитория папки, файлы конфигурации hello initialize и hello откройте образец проекта в Visual Studio Code, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="57b67-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize hello configuration files, and then open hello sample project in Visual Studio Code by running hello following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![структура репозитория](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="57b67-123">Hello `arm-template.json` файла является шаблон hello диспетчера ресурсов Azure, который содержит приложение Azure функции и учетная запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="57b67-123">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="57b67-124">Hello `arm-template-param.json` файл является файлом конфигурации hello, используемые hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="57b67-124">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
- <span data-ttu-id="57b67-125">Hello `ReceiveDeviceMessages` вложенная папка содержит код Node.js hello Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="57b67-125">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="57b67-126">Настройка шаблонов Azure Resource Manager и создание ресурсов в Azure</span><span class="sxs-lookup"><span data-stu-id="57b67-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="57b67-127">Обновление hello `arm-template-param.json` файл в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="57b67-127">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![JSON-файл шаблона ARM](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="57b67-129">Замените `[your IoT Hub name]` именем `{my hub name}`, указанным в уроке 2.</span><span class="sxs-lookup"><span data-stu-id="57b67-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="57b67-130">После обновления hello `arm-template-param.json` файлов, развертывание, выполнив следующую команду hello tooAzure ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="57b67-130">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="57b67-131">Используйте `iot-gateway` в качестве значения hello `{resource group name}` Если вы не изменили значение hello в занятии 2.</span><span class="sxs-lookup"><span data-stu-id="57b67-131">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="57b67-132">Сводка</span><span class="sxs-lookup"><span data-stu-id="57b67-132">Summary</span></span>

<span data-ttu-id="57b67-133">Вы создали вашей tooprocess приложения Azure функция IoT hub сообщений и учетной записи хранилища Azure toostore эти сообщения.</span><span class="sxs-lookup"><span data-stu-id="57b67-133">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="57b67-134">Теперь можно считывать сообщения, отправляемые с вашего центра IoT tooyour шлюза.</span><span class="sxs-lookup"><span data-stu-id="57b67-134">You can now read messages that are sent by your gateway tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57b67-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="57b67-135">Next steps</span></span>
<span data-ttu-id="57b67-136">[Чтение сообщений, сохраненных в службе хранилища Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md)</span><span class="sxs-lookup"><span data-stu-id="57b67-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
