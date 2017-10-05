---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 4. Создание приложения-функции | Документация Майкрософт"
description: "Сохраняйте сообщения из Intel NUC в Центр Интернета вещей, записывайте их в Хранилище таблиц Azure, а затем читайте их из облака."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "хранение данных в облаке, данные, хранящиеся в облаке, облачная служба Интернета вещей"
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
ms.openlocfilehash: 717c91e8332660f19d596c05a8a23afd8df1d51c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="8d27c-104">Создание приложения-функции Azure и учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="8d27c-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="8d27c-105">Функции Azure — это решение для быстрого запуска _функций_ (фрагментов кода) в облаке.</span><span class="sxs-lookup"><span data-stu-id="8d27c-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span></span> <span data-ttu-id="8d27c-106">Выполнение функций в Azure производится с помощью приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="8d27c-106">An Azure function app hosts the execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="8d27c-107">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="8d27c-107">What you will do</span></span>

- <span data-ttu-id="8d27c-108">С помощью шаблона Azure Resource Manager создайте приложение-функцию Azure и учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="8d27c-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="8d27c-109">Приложение-функция Azure ожидает передачи событий Центра Интернета вещей Azure, обрабатывает входящие сообщения и записывает их в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="8d27c-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="8d27c-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8d27c-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="8d27c-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="8d27c-111">What you will learn</span></span>

<span data-ttu-id="8d27c-112">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="8d27c-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="8d27c-113">как использовать Azure Resource Manager для развертывания ресурсов в Azure;</span><span class="sxs-lookup"><span data-stu-id="8d27c-113">How to use Azure Resource Manager to deploy Azure resources.</span></span>
- <span data-ttu-id="8d27c-114">как использовать приложение-функцию Azure для обработки сообщений Центра Интернета вещей и их записи в таблицу в Хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="8d27c-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8d27c-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="8d27c-115">What you need</span></span>

<span data-ttu-id="8d27c-116">Необходимо успешно пройти следующие уроки:</span><span class="sxs-lookup"><span data-stu-id="8d27c-116">You must have successfully completed the previous lessons:</span></span>

- [<span data-ttu-id="8d27c-117">Урок 1. Настройка Intel NUC в качестве шлюза Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="8d27c-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [<span data-ttu-id="8d27c-118">Урок 2. Подготовка главного компьютера и Центра Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="8d27c-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="8d27c-119">Урок 3. Получение сообщений из SensorTag и чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="8d27c-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="8d27c-120">Открытие примера приложения</span><span class="sxs-lookup"><span data-stu-id="8d27c-120">Open a sample app</span></span>

<span data-ttu-id="8d27c-121">Перейдите в папку репозитория `iot-hub-c-intel-nuc-gateway-getting-started`, выполните инициализацию файлов конфигурации, а затем откройте пример проекта в Visual Studio Code, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8d27c-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![структура репозитория](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="8d27c-123">Файл `arm-template.json` — шаблон Azure Resource Manager, содержащий приложение-функцию Azure и учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="8d27c-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="8d27c-124">Файл `arm-template-param.json` — файл конфигурации, используемый в шаблоне Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8d27c-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
- <span data-ttu-id="8d27c-125">Вложенная папка `ReceiveDeviceMessages` содержит код Node.js для функции Azure.</span><span class="sxs-lookup"><span data-stu-id="8d27c-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="8d27c-126">Настройка шаблонов Azure Resource Manager и создание ресурсов в Azure</span><span class="sxs-lookup"><span data-stu-id="8d27c-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="8d27c-127">Обновите файл `arm-template-param.json` в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8d27c-127">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![JSON-файл шаблона ARM](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="8d27c-129">Замените `[your IoT Hub name]` именем `{my hub name}`, указанным в уроке 2.</span><span class="sxs-lookup"><span data-stu-id="8d27c-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="8d27c-130">После обновления файла `arm-template-param.json` разверните ресурсы в Azure, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8d27c-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="8d27c-131">Используйте `iot-gateway` в качестве значения `{resource group name}`, если в уроке 2 значение не изменялось.</span><span class="sxs-lookup"><span data-stu-id="8d27c-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="8d27c-132">Сводка</span><span class="sxs-lookup"><span data-stu-id="8d27c-132">Summary</span></span>

<span data-ttu-id="8d27c-133">Вы создали приложение-функцию Azure для обработки сообщений Центра Интернета вещей и учетную запись хранения Azure для хранения этих сообщений.</span><span class="sxs-lookup"><span data-stu-id="8d27c-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="8d27c-134">Теперь можно читать сообщения, отправленные шлюзом в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8d27c-134">You can now read messages that are sent by your gateway to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d27c-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d27c-135">Next steps</span></span>
<span data-ttu-id="8d27c-136">[Чтение сообщений, сохраненных в службе хранилища Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md)</span><span class="sxs-lookup"><span data-stu-id="8d27c-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
