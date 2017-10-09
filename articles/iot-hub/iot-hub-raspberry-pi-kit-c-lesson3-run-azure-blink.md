---
title: "Connect Raspberry PI (C) tooAzure IoT — занятия 3: выполнение примера | Документы Microsoft"
description: "Развертывание и запуск образца приложения tooRaspberry Pi 3, отправляет сообщения центр IoT tooyour и hello Индикатор мигает."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "мигающий светодиодный индикатор облако pi, мигающий индикатор из облака"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c484beb2e2d3a3cf19f071f2ba87b9a4fe41c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="10757-104">Запустите образец приложения toosend сообщения из устройства в облако</span><span class="sxs-lookup"><span data-stu-id="10757-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="10757-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="10757-105">What you will do</span></span>
<span data-ttu-id="10757-106">В этой статье показано, как toodeploy и выполнение примера приложения на 3 Raspberry Pi, который отправляет сообщения tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="10757-106">This article will show you how toodeploy and run a sample application on Raspberry Pi 3 that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="10757-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="10757-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="10757-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="10757-108">What you will learn</span></span>
<span data-ttu-id="10757-109">Вы узнаете, как toouse hello gulp toodeploy средства и запустите приложение Node.js образец hello на Pi.</span><span class="sxs-lookup"><span data-stu-id="10757-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="10757-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="10757-110">What you need</span></span>
* <span data-ttu-id="10757-111">Прежде чем начать эту задачу, необходимо успешно выполнить [создания приложения Azure функции и концентратор IoT tooprocess и хранилище учетной записи хранилища сообщений](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="10757-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="10757-112">Получение строк подключения Центра Интернета вещей и устройства</span><span class="sxs-lookup"><span data-stu-id="10757-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="10757-113">Строка подключения устройства Hello используется ваш центр IoT tooyour tooconnect Pi.</span><span class="sxs-lookup"><span data-stu-id="10757-113">hello device connection string is used by your Pi tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="10757-114">Строка подключения концентратора IoT Hello — реестра удостоверений toohello tooconnect используется в вашей IoT hub toomanage hello устройства, которым разрешен центра IoT tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="10757-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span> 

* <span data-ttu-id="10757-115">Перечислить все центры IoT в группе ресурсов, выполнив следующую команду Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="10757-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="10757-116">Используйте `iot-sample` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.</span><span class="sxs-lookup"><span data-stu-id="10757-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="10757-117">Получите строку подключения концентратора IoT hello, выполнив следующую команду Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="10757-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="10757-118">`{my hub name}`— Имя hello, указанный вами создали концентратор IoT при регистрации Pi.</span><span class="sxs-lookup"><span data-stu-id="10757-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="10757-119">Получите строку подключения устройства hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="10757-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="10757-120">Используйте `myraspberrypi` в качестве значения hello `{device id}` Если вы не изменили значение hello.</span><span class="sxs-lookup"><span data-stu-id="10757-120">Use `myraspberrypi` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="10757-121">Настройка подключения устройства hello</span><span class="sxs-lookup"><span data-stu-id="10757-121">Configure hello device connection</span></span>
1. <span data-ttu-id="10757-122">Инициализируйте hello файл конфигурации, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="10757-122">Initialize hello configuration file by running hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="10757-123">Выполните также **gulp install-tools**, если это не было сделано на уроке 1.</span><span class="sxs-lookup"><span data-stu-id="10757-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="10757-124">Файл конфигурации устройства Привет открыть `config-raspberrypi.json` в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="10757-124">Open hello device configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="10757-126">Сделать после замены в hello hello `config-raspberrypi.json` файла:</span><span class="sxs-lookup"><span data-stu-id="10757-126">Make hello following replacements in hello `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="10757-127">Замените **[устройства имя узла или IP-адрес]** hello IP адрес или имя устройства, полученный из `device-discovery-cli` или со значением hello наследуется при настройке устройства.</span><span class="sxs-lookup"><span data-stu-id="10757-127">Replace **[device hostname or IP address]** with hello device IP address or host name you got from `device-discovery-cli` or with hello value inherited when you configured your device.</span></span>
   * <span data-ttu-id="10757-128">Замените **[строка подключения устройств IoT]** с hello `device connection string` полученных.</span><span class="sxs-lookup"><span data-stu-id="10757-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="10757-129">Замените **[строка подключения концентратора IoT]** с hello `iot hub connection string` полученных.</span><span class="sxs-lookup"><span data-stu-id="10757-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="10757-130">В этой статье не требуется `azure_storage_connection_string`.</span><span class="sxs-lookup"><span data-stu-id="10757-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="10757-131">Оставьте эту настройку без изменений.</span><span class="sxs-lookup"><span data-stu-id="10757-131">Keep it as is.</span></span>

<span data-ttu-id="10757-132">Обновление hello `config-raspberrypi.json` так, можно развернуть пример приложения hello с вашего компьютера.</span><span class="sxs-lookup"><span data-stu-id="10757-132">Update hello `config-raspberrypi.json` file so that you can deploy hello sample application from your computer.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="10757-133">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="10757-133">Deploy and run hello sample application</span></span>
<span data-ttu-id="10757-134">Развертывание и запуск образца приложения hello на Pi, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="10757-134">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="10757-135">Проверка работы образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="10757-135">Verify that hello sample application works</span></span>
<span data-ttu-id="10757-136">Вы увидите hello Индикатор, подключенных tooPi мигает каждые две секунды.</span><span class="sxs-lookup"><span data-stu-id="10757-136">You should see hello LED that is connected tooPi blinking every two seconds.</span></span> <span data-ttu-id="10757-137">Каждый раз hello Индикатор мигает, пример приложения hello отправляет центр IoT tooyour сообщения и подтверждает, что это сообщение hello было успешно отправлено tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="10757-137">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="10757-138">Кроме того каждое сообщение, полученных центра IoT hello выводится в окне консоли hello.</span><span class="sxs-lookup"><span data-stu-id="10757-138">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="10757-139">Пример приложения Hello автоматически завершает после отправки 20 сообщений.</span><span class="sxs-lookup"><span data-stu-id="10757-139">hello sample application terminates automatically after sending 20 messages.</span></span>

![Пример приложения с отправленными и полученными сообщениями](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="10757-141">Сводка</span><span class="sxs-lookup"><span data-stu-id="10757-141">Summary</span></span>
<span data-ttu-id="10757-142">Вы развертывания и запуска hello новый blink образца приложения-концентратора IoT tooyour Pi toosend сообщения из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="10757-142">You've deployed and run hello new blink sample application on Pi toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="10757-143">Теперь отслеживать сообщения, записываемые toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="10757-143">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10757-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="10757-144">Next steps</span></span>
[<span data-ttu-id="10757-145">Чтение сообщений, сохраненных в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="10757-145">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

