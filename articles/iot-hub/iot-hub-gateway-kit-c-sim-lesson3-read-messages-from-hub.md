---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 3. Чтение сообщений | Документация Майкрософт"
description: "Запустите образец кода на сообщения hello tooread компьютера узла из вашего центра IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "данные в облако hello, сбор данных облака, iot облачной службы, iot данных"
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
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="ab894-104">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="ab894-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ab894-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="ab894-105">What you will do</span></span>

- <span data-ttu-id="ab894-106">Запустите образец кода на вашем узле компьютер tooread сообщения из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="ab894-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="ab894-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ab894-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ab894-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="ab894-108">What you will learn</span></span>

<span data-ttu-id="ab894-109">Как toouse hello gulp средство tooread сообщения от вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="ab894-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ab894-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="ab894-110">What you need</span></span>

- <span data-ttu-id="ab894-111">Образец Hello имитированное устройство в [настроить и запустить имитированное устройство облака отправить образец приложения](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="ab894-111">hello simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="ab894-112">Получение строк подключения Центра Интернета вещей и устройства</span><span class="sxs-lookup"><span data-stu-id="ab894-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="ab894-113">Строка подключения устройства Hello используется ваш центр IoT tooyour tooconnect имитированное устройство.</span><span class="sxs-lookup"><span data-stu-id="ab894-113">hello device connection string is used by your simulated device tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="ab894-114">Строка подключения концентратора IoT Hello — реестра удостоверений toohello tooconnect используется в вашей IoT hub toomanage hello устройства, которым разрешен центра IoT tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="ab894-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="ab894-115">Перечислить все центры IoT в группе ресурсов, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ab894-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="ab894-116">Используйте `iot-gateway` в качестве значения hello `{resource group name}` Если вы не были изменены.</span><span class="sxs-lookup"><span data-stu-id="ab894-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="ab894-117">Получите строку подключения концентратора IoT hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ab894-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="ab894-118">`{my hub name}`— Имя hello, указаны в занятии 2.</span><span class="sxs-lookup"><span data-stu-id="ab894-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="ab894-119">Настройка подключения устройства hello hello образец кода</span><span class="sxs-lookup"><span data-stu-id="ab894-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="ab894-120">Обновить IoT hub устройства подключения конфигураций и в `config-azure.json` , выполнив следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ab894-120">Update IoT hub and device connection configurations in `config-azure.json` by performing hello following steps:</span></span>

1. <span data-ttu-id="ab894-121">Откройте `config-azure.json` в коде Visual Studio, выполнив следующую команду в окне консоли hello:</span><span class="sxs-lookup"><span data-stu-id="ab894-121">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="ab894-122">Сделать после замены в hello hello `config-azure.json` файла:</span><span class="sxs-lookup"><span data-stu-id="ab894-122">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![снимок экрана настройки Azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="ab894-124">Замените `[IoT hub connection string]` с hello строка подключения концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="ab894-124">Replace `[IoT hub connection string]` with hello IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="ab894-125">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="ab894-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="ab894-126">Запустить образец приложения hello имитируемые устройства и прочитаны центра IoT сообщений hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ab894-126">Run hello simulated device sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="ab894-127">Команда Hello выполняет приложение hello, отправляет сообщения центр IoT tooyour каждые 2 секунды.</span><span class="sxs-lookup"><span data-stu-id="ab894-127">hello command runs hello application that sends messages tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="ab894-128">Оно также создает сообщение hello tooreceive дочерних процесса.</span><span class="sxs-lookup"><span data-stu-id="ab894-128">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="ab894-129">сообщения приветствия, отправки и получения всех отображаемых мгновенно на hello же консоли окна в hello хост-компьютера.</span><span class="sxs-lookup"><span data-stu-id="ab894-129">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="ab894-130">приложение Hello завершит работу в 40 секунд.</span><span class="sxs-lookup"><span data-stu-id="ab894-130">hello application will exit in 40 seconds.</span></span>

![Имитация примера приложения с отправленными и полученными сообщениями](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="ab894-132">Сводка</span><span class="sxs-lookup"><span data-stu-id="ab894-132">Summary</span></span>

<span data-ttu-id="ab894-133">После успешного выполнения tooyour центр IoT приложений toosend hello образец данных с устройств, имитация.</span><span class="sxs-lookup"><span data-stu-id="ab894-133">You've successfully run hello sample application toosend data tooyour IoT hub with simulated device.</span></span> <span data-ttu-id="ab894-134">Также прочтения сообщений hello, которые были отправлены tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="ab894-134">You've also read hello messages that have been sent tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab894-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ab894-135">Next steps</span></span>
[<span data-ttu-id="ab894-136">Создание учетной записи хранения Azure и приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="ab894-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


