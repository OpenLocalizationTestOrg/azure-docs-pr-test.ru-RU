---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 3. Чтение сообщений | Документация Майкрософт"
description: "Запустите пример кода на главном компьютере для чтения сообщений из Центра Интернета вещей."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "данные в облаке, коллекция облачных данных, облачная служба Интернета вещей, данные Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fbf7958e2437d274f2692dbc235ac8147bdfa63
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="ce3b1-104">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="ce3b1-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ce3b1-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="ce3b1-105">What you will do</span></span>

- <span data-ttu-id="ce3b1-106">Запустите пример кода на главном компьютере для чтения сообщений из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="ce3b1-107">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ce3b1-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ce3b1-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="ce3b1-108">What you will learn</span></span>

<span data-ttu-id="ce3b1-109">Чтение сообщений из Центра Интернета вещей с использованием инструмента Gulp.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ce3b1-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="ce3b1-110">What you need</span></span>

- <span data-ttu-id="ce3b1-111">Пример имитации устройства можно найти в статье [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md) (Настройка и запуск примера приложения отправки в облако для имитации устройства).</span><span class="sxs-lookup"><span data-stu-id="ce3b1-111">The simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="ce3b1-112">Получение строк подключения Центра Интернета вещей и устройства</span><span class="sxs-lookup"><span data-stu-id="ce3b1-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="ce3b1-113">Строка подключения устройства используется имитацией устройства для подключения к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-113">The device connection string is used by your simulated device to connect to your IoT hub.</span></span> <span data-ttu-id="ce3b1-114">Строка подключения Центра Интернета вещей используется для подключения к реестру удостоверений в Центре Интернета вещей, чтобы управлять устройствами, которым разрешено подключаться к этому центру.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="ce3b1-115">Для вывода списка всех Центров Интернета вещей в группе ресурсов выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ce3b1-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="ce3b1-116">Используйте `iot-gateway` в качестве значения `{resource group name}`, если вы не меняли это значение.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="ce3b1-117">Для получения строки подключения Центра Интернета вещей выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ce3b1-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="ce3b1-118">`{my hub name}` — это имя, указанное в уроке 2.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="ce3b1-119">Настройка подключения устройства для примера кода</span><span class="sxs-lookup"><span data-stu-id="ce3b1-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="ce3b1-120">Обновите Центр Интернета вещей и конфигурации подключения устройства в `config-azure.json`, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="ce3b1-120">Update IoT hub and device connection configurations in `config-azure.json` by performing the following steps:</span></span>

1. <span data-ttu-id="ce3b1-121">Откройте файл `config-azure.json` в Visual Studio Code, выполнив следующую команду в окне консоли:</span><span class="sxs-lookup"><span data-stu-id="ce3b1-121">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="ce3b1-122">В файле `config-azure.json` выполните следующие замены.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-122">Make the following replacements in the `config-azure.json` file:</span></span>

   ![снимок экрана настройки Azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="ce3b1-124">Замените `[IoT hub connection string]` строкой подключения Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-124">Replace `[IoT hub connection string]` with the IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="ce3b1-125">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="ce3b1-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="ce3b1-126">Запустите пример приложения для имитации устройства и прочтите сообщения Центра Интернета вещей, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ce3b1-126">Run the simulated device sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="ce3b1-127">Команда запускает приложение, которое отправляет сообщения в Центр Интернета вещей каждые 2 секунды.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-127">The command runs the application that sends messages to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="ce3b1-128">Она также создает дочерний процесс получения сообщения.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-128">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="ce3b1-129">Все отправленные и полученные сообщения мгновенно появляются в том же окне консоли на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-129">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="ce3b1-130">Приложение завершит работу через 40 секунд.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-130">The application will exit in 40 seconds.</span></span>

![Имитация примера приложения с отправленными и полученными сообщениями](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="ce3b1-132">Сводка</span><span class="sxs-lookup"><span data-stu-id="ce3b1-132">Summary</span></span>

<span data-ttu-id="ce3b1-133">Вы успешно запустили пример приложения для отправки данных в Центр Интернета вещей с помощью имитации устройства.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-133">You've successfully run the sample application to send data to your IoT hub with simulated device.</span></span> <span data-ttu-id="ce3b1-134">Вы также прочли сообщения, отправленные в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ce3b1-134">You've also read the messages that have been sent to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce3b1-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ce3b1-135">Next steps</span></span>
[<span data-ttu-id="ce3b1-136">Создание учетной записи хранения Azure и приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="ce3b1-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


