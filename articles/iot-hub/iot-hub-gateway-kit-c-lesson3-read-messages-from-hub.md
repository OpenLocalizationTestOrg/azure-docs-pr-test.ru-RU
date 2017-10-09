---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 3. Чтение сообщений | Документация Майкрософт"
description: "Запустите образец кода на сообщения hello tooread компьютера узла из вашего центра IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "данные в облако hello, сбор данных облака, iot облачной службы, iot данных"
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
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="df6de-104">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="df6de-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="df6de-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="df6de-105">What you will do</span></span>

- <span data-ttu-id="df6de-106">Запустите образец кода на вашем узле компьютер tooread сообщения из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="df6de-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="df6de-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="df6de-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="df6de-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="df6de-108">What you will learn</span></span>

<span data-ttu-id="df6de-109">Как toouse hello gulp средство tooread сообщения от вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="df6de-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="df6de-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="df6de-110">What you need</span></span>

- <span data-ttu-id="df6de-111">Hello ЛЮЧИТЬ образец приложения, в занятии 3 выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="df6de-111">hello BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="df6de-112">Получение строк подключения Центра Интернета вещей и устройства</span><span class="sxs-lookup"><span data-stu-id="df6de-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="df6de-113">Строка подключения устройства Hello используется ваш центр IoT tooyour tooconnect устройства (TI SensorTag или имитированное устройство).</span><span class="sxs-lookup"><span data-stu-id="df6de-113">hello device connection string is used by your device (TI SensorTag or simulated device) tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="df6de-114">Строка подключения концентратора IoT Hello — реестра удостоверений toohello tooconnect используется в вашей IoT hub toomanage hello устройства, которым разрешен центра IoT tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="df6de-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="df6de-115">Перечислить все центры IoT в группе ресурсов, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="df6de-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="df6de-116">Используйте `iot-gateway` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.</span><span class="sxs-lookup"><span data-stu-id="df6de-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
- <span data-ttu-id="df6de-117">Получите строку подключения концентратора IoT hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="df6de-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="df6de-118">`{my hub name}`— Имя hello, указаны в занятии 2.</span><span class="sxs-lookup"><span data-stu-id="df6de-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="df6de-119">Настройка подключения устройства hello hello образец кода</span><span class="sxs-lookup"><span data-stu-id="df6de-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="df6de-120">Обновленный файл конфигурации устройства hello `config-azure.json` , могут читать сообщения из вашего центра IoT на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="df6de-120">Update hello device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="df6de-121">toodo это, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="df6de-121">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="df6de-122">Откройте `config-azure.json` в коде Visual Studio, выполнив следующую команду в окне консоли hello:</span><span class="sxs-lookup"><span data-stu-id="df6de-122">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="df6de-123">Сделать после замены в hello hello `config-azure.json` файла:</span><span class="sxs-lookup"><span data-stu-id="df6de-123">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![снимок экрана настройки Azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="df6de-125">Замените `[IoT hub connection string]` с строка подключения концентратора IoT, полученный hello.</span><span class="sxs-lookup"><span data-stu-id="df6de-125">Replace `[IoT hub connection string]` with hello IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="df6de-126">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="df6de-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="df6de-127">Если у вас есть TI SensorTag, убедитесь, что устройство SensorTag включено.</span><span class="sxs-lookup"><span data-stu-id="df6de-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="df6de-128">Запустить образец приложения hello шлюза и прочитаны центра IoT сообщений hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="df6de-128">Run hello gateway sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="df6de-129">Команда Hello выполняет hello ЛЮЧИТЬ образец приложения, считывает и упаковывает температур с имитации устройства или SensorTag и отправляет центр IoT tooyour сообщение hello каждые 2 секунды.</span><span class="sxs-lookup"><span data-stu-id="df6de-129">hello command runs hello BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends hello message tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="df6de-130">Оно также создает сообщение hello tooreceive дочерних процесса.</span><span class="sxs-lookup"><span data-stu-id="df6de-130">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="df6de-131">сообщения приветствия, отправки и получения всех отображаемых мгновенно на hello же консоли окна в hello хост-компьютера.</span><span class="sxs-lookup"><span data-stu-id="df6de-131">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="df6de-132">экземпляр приложения Образец Hello нарушит автоматически в 40 секунд.</span><span class="sxs-lookup"><span data-stu-id="df6de-132">hello sample application instance will terminate automatically in 40 seconds.</span></span>

![Пример приложения BLE с отправленными и полученными сообщениями](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="df6de-134">Сводка</span><span class="sxs-lookup"><span data-stu-id="df6de-134">Summary</span></span>

<span data-ttu-id="df6de-135">После выполнения tooread образец кода сообщения из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="df6de-135">You've run a sample code tooread messages from your IoT hub.</span></span> <span data-ttu-id="df6de-136">Теперь вы готовы tooread сообщений hello, которые хранятся в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="df6de-136">You're ready tooread hello messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df6de-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df6de-137">Next steps</span></span>
[<span data-ttu-id="df6de-138">Создание учетной записи хранения Azure и приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="df6de-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


