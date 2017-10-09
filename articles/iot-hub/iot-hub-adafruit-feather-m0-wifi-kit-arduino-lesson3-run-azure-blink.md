---
title: "Connect Arduino (C) tooAzure IoT — занятия 3: выполнение примера | Документы Microsoft"
description: "Развертывание и запуск образца приложения tooAdafruit Растушевка M0 Wi-Fi, отправляет сообщения центр IoT tooyour и hello Индикатор мигает."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT облачной службы, arduino отправки данных toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="84d0d-104">Запустите образец приложения toosend сообщения из устройства в облако</span><span class="sxs-lookup"><span data-stu-id="84d0d-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="84d0d-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="84d0d-105">What you will do</span></span>
<span data-ttu-id="84d0d-106">В этой статье показано, как toodeploy и выполнение примера приложения на ваш Adafruit Растушевка M0 Wi-Fi Arduino плата центра IoT tooyour, отправляет сообщения.</span><span class="sxs-lookup"><span data-stu-id="84d0d-106">This article will show you how toodeploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages tooyour IoT hub.</span></span>

<span data-ttu-id="84d0d-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="84d0d-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="84d0d-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="84d0d-108">What you will learn</span></span>
<span data-ttu-id="84d0d-109">Вы узнаете, как toouse hello gulp toodeploy средства и запустите приложение Arduino образец hello в Arduino на доске.</span><span class="sxs-lookup"><span data-stu-id="84d0d-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="84d0d-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="84d0d-110">What you need</span></span>
* <span data-ttu-id="84d0d-111">Прежде чем начать эту задачу, необходимо успешно выполнить [создания приложения Azure функции и концентратор IoT tooprocess и хранилище учетной записи хранилища сообщений][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="84d0d-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="84d0d-112">Получение строк подключения Центра Интернета вещей и устройства</span><span class="sxs-lookup"><span data-stu-id="84d0d-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="84d0d-113">Здравствуйте, строка подключения устройства является используется tooconnect ваш центр IoT Arduino tooyour платы.</span><span class="sxs-lookup"><span data-stu-id="84d0d-113">hello device connection string is used tooconnect your Arduino board tooyour IoT hub.</span></span> <span data-ttu-id="84d0d-114">Строка подключения концентратора IoT Hello — используется tooconnect вашей IoT hub toohello удостоверение устройства, представляющий вашей Arduino плата в центр IoT hello.</span><span class="sxs-lookup"><span data-stu-id="84d0d-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents your Arduino board in hello IoT hub.</span></span>

* <span data-ttu-id="84d0d-115">Перечислить все центры IoT в группе ресурсов, выполнив следующую команду Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="84d0d-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="84d0d-116">Используйте `iot-sample` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.</span><span class="sxs-lookup"><span data-stu-id="84d0d-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="84d0d-117">Получите строку подключения концентратора IoT hello, выполнив следующую команду Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="84d0d-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="84d0d-118">`{my hub name}`— hello имя, указанное при создании ваш центр IoT и зарегистрирован Arduino доске.</span><span class="sxs-lookup"><span data-stu-id="84d0d-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="84d0d-119">Получите строку подключения устройства hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="84d0d-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="84d0d-120">Используйте `mym0wifi` в качестве значения hello `{device id}` Если вы не изменили значение hello.</span><span class="sxs-lookup"><span data-stu-id="84d0d-120">Use `mym0wifi` as hello value of `{device id}` if you didn't change hello value.</span></span>
## <a name="configure-hello-device-connection"></a><span data-ttu-id="84d0d-121">Настройка подключения устройства hello</span><span class="sxs-lookup"><span data-stu-id="84d0d-121">Configure hello device connection</span></span>
<span data-ttu-id="84d0d-122">tooconfigure Здравствуйте подключения устройства, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="84d0d-122">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="84d0d-123">Получите hello последовательного порта hello устройства с cli обнаружения устройства hello.</span><span class="sxs-lookup"><span data-stu-id="84d0d-123">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="84d0d-124">Должны видеть выходные данные, аналогичные следующие toohello и найти COM-порт hello usb плата Arduino:</span><span class="sxs-lookup"><span data-stu-id="84d0d-124">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Обнаружение устройства][device-discovery]

2. <span data-ttu-id="84d0d-126">Привет открыть файл `config.json` в hello папку занятия и добавьте значение hello hello, найти номер COM-порта:</span><span class="sxs-lookup"><span data-stu-id="84d0d-126">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="84d0d-128">Для порта hello COM, на платформе Windows, он имеет формат hello `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="84d0d-128">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="84d0d-129">На macOS или Ubuntu он начинается с `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="84d0d-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="84d0d-130">Инициализируйте hello файл конфигурации, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="84d0d-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="84d0d-131">Файл конфигурации устройства Привет открыть `config-arduino.json` в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="84d0d-131">Open hello device configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="84d0d-133">Сделать после замены в hello hello `config-arduino.json` файла:</span><span class="sxs-lookup"><span data-stu-id="84d0d-133">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   * <span data-ttu-id="84d0d-134">Замените **[Wi-Fi SSID]** с вашей SSID Wi-Fi, подключенный toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="84d0d-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="84d0d-135">Замените **[Wi-Fi password]** своим паролем Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="84d0d-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="84d0d-136">Удалите строку hello, если Wi-Fi не требует пароля.</span><span class="sxs-lookup"><span data-stu-id="84d0d-136">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="84d0d-137">Замените **[строка подключения устройств IoT]** с hello `device connection string` полученных.</span><span class="sxs-lookup"><span data-stu-id="84d0d-137">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="84d0d-138">Замените **[строка подключения концентратора IoT]** с hello `iot hub connection string` полученных.</span><span class="sxs-lookup"><span data-stu-id="84d0d-138">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="84d0d-139">В этой статье не требуется `azure_storage_connection_string`.</span><span class="sxs-lookup"><span data-stu-id="84d0d-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="84d0d-140">Оставьте эту настройку без изменений.</span><span class="sxs-lookup"><span data-stu-id="84d0d-140">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="84d0d-141">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="84d0d-141">Deploy and run hello sample application</span></span>
<span data-ttu-id="84d0d-142">Развертывание и запуск образца приложения hello на доске Arduino, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="84d0d-142">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="84d0d-143">Hello gulp задачи по умолчанию выполняется `install-tools` и `run` задачи последовательно.</span><span class="sxs-lookup"><span data-stu-id="84d0d-143">hello default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="84d0d-144">Когда вы [hello blink приложение развернуто][deployed-the-blink-app], выполнении этих задач отдельно.</span><span class="sxs-lookup"><span data-stu-id="84d0d-144">When you [deployed hello blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="84d0d-145">Проверка работы образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="84d0d-145">Verify that hello sample application works</span></span>
<span data-ttu-id="84d0d-146">Вы увидите hello объект групповой ПОЛИТИКИ #0 встроенный Индикатор мигает. каждые две секунды.</span><span class="sxs-lookup"><span data-stu-id="84d0d-146">You should see hello GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="84d0d-147">Каждый раз hello Индикатор мигает, пример приложения hello отправляет центр IoT tooyour сообщения и подтверждает, что это сообщение hello было успешно отправлено tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="84d0d-147">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="84d0d-148">Кроме того каждое сообщение, полученных центра IoT hello выводится в окне консоли hello.</span><span class="sxs-lookup"><span data-stu-id="84d0d-148">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="84d0d-149">Пример приложения Hello автоматически завершает после отправки 20 сообщений.</span><span class="sxs-lookup"><span data-stu-id="84d0d-149">hello sample application terminates automatically after sending 20 messages.</span></span>

![Пример приложения с отправленными и полученными сообщениями][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="84d0d-151">Сводка</span><span class="sxs-lookup"><span data-stu-id="84d0d-151">Summary</span></span>
<span data-ttu-id="84d0d-152">После развертывания и запустить hello новый blink пример приложения на концентратор IoT tooyour Arduino плата toosend сообщения из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="84d0d-152">You've deployed and run hello new blink sample application on your Arduino board toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="84d0d-153">Теперь отслеживать сообщения, записываемые toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="84d0d-153">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84d0d-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84d0d-154">Next steps</span></span>
<span data-ttu-id="84d0d-155">[Чтение сообщений, сохраненных в службе хранилища Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="84d0d-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md