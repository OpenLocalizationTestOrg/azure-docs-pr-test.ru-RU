---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 3. Чтение сообщений | Документация Майкрософт"
description: "Запустите пример кода на главном компьютере для чтения сообщений из Центра Интернета вещей."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "данные в облаке, коллекция облачных данных, облачная служба Интернета вещей, данные Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 45f3595c4848d5c283cdf95604adf8d2c8d6a809
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="fc9b2-104">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="fc9b2-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="fc9b2-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="fc9b2-105">What you will do</span></span>

- <span data-ttu-id="fc9b2-106">Запустите пример кода на главном компьютере для чтения сообщений из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="fc9b2-107">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="fc9b2-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fc9b2-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="fc9b2-108">What you will learn</span></span>

<span data-ttu-id="fc9b2-109">Чтение сообщений из Центра Интернета вещей с использованием инструмента Gulp.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fc9b2-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="fc9b2-110">What you need</span></span>

- <span data-ttu-id="fc9b2-111">Пример приложения BLE, успешно запущенный на уроке 3.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-111">The BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="fc9b2-112">Получение строк подключения Центра Интернета вещей и устройства</span><span class="sxs-lookup"><span data-stu-id="fc9b2-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="fc9b2-113">Ваше устройство (TI SensorTag или имитация устройства) использует строку подключения для подключения к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-113">The device connection string is used by your device (TI SensorTag or simulated device) to connect to your IoT hub.</span></span> <span data-ttu-id="fc9b2-114">Строка подключения Центра Интернета вещей используется для подключения к реестру удостоверений в Центре Интернета вещей, чтобы управлять устройствами, которым разрешено подключаться к этому центру.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="fc9b2-115">Для вывода списка всех Центров Интернета вещей в группе ресурсов выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fc9b2-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="fc9b2-116">Используйте `iot-gateway` в качестве значения `{resource group name}`, если вы не меняли это значение.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value.</span></span>
- <span data-ttu-id="fc9b2-117">Для получения строки подключения Центра Интернета вещей выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fc9b2-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="fc9b2-118">`{my hub name}` — это имя, указанное в уроке 2.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="fc9b2-119">Настройка подключения устройства для примера кода</span><span class="sxs-lookup"><span data-stu-id="fc9b2-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="fc9b2-120">Обновите файл конфигурации устройства `config-azure.json` для чтения сообщений из Центра Интернета вещей на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-120">Update the device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="fc9b2-121">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-121">To do this, follow these steps:</span></span>

1. <span data-ttu-id="fc9b2-122">Откройте файл `config-azure.json` в Visual Studio Code, выполнив следующую команду в окне консоли:</span><span class="sxs-lookup"><span data-stu-id="fc9b2-122">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="fc9b2-123">В файле `config-azure.json` выполните следующие замены.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-123">Make the following replacements in the `config-azure.json` file:</span></span>

   ![снимок экрана настройки Azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="fc9b2-125">Замените `[IoT hub connection string]` полученной строкой подключения Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-125">Replace `[IoT hub connection string]` with the IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="fc9b2-126">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="fc9b2-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="fc9b2-127">Если у вас есть TI SensorTag, убедитесь, что устройство SensorTag включено.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="fc9b2-128">Запустите пример приложения шлюза и прочтите сообщения Центра Интернета вещей, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fc9b2-128">Run the gateway sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="fc9b2-129">Команда запускает пример приложения BLE, которое считывает данные температуры с SensorTag или имитации устройства и каждые 2 секунды отправляет сообщение в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-129">The command runs the BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends the message to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="fc9b2-130">Она также создает дочерний процесс получения сообщения.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-130">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="fc9b2-131">Все отправленные и полученные сообщения мгновенно появляются в том же окне консоли на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-131">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="fc9b2-132">Экземпляр примера приложения прекращает свое действие автоматически через 40 секунд.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-132">The sample application instance will terminate automatically in 40 seconds.</span></span>

![Пример приложения BLE с отправленными и полученными сообщениями](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="fc9b2-134">Сводка</span><span class="sxs-lookup"><span data-stu-id="fc9b2-134">Summary</span></span>

<span data-ttu-id="fc9b2-135">Вы запустили пример кода для чтения сообщений из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-135">You've run a sample code to read messages from your IoT hub.</span></span> <span data-ttu-id="fc9b2-136">Теперь можно приступить к чтению сообщений, которые хранятся в Хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="fc9b2-136">You're ready to read the messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc9b2-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc9b2-137">Next steps</span></span>
[<span data-ttu-id="fc9b2-138">Создание учетной записи хранения Azure и приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="fc9b2-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


