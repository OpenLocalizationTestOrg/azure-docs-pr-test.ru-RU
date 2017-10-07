---
title: "Connect Arduino (C) tooAzure IoT — занятия 3: хранилище таблиц | Документы Microsoft"
description: "Они записываются в хранилище таблиц Azure tooyour наблюдать за сообщений hello устройства в облако."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "данные в облако hello, сбор данных облака, iot облачной службы, iot данных"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="b6615-104">Чтение сообщений, сохраненных в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="b6615-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b6615-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="b6615-105">What you will do</span></span>
<span data-ttu-id="b6615-106">Монитор hello устройства в облако сообщений, отправляемых из вашего центра IoT Adafruit Растушевка M0 Wi-Fi Arduino tooyour плата как сообщений hello записываются tooyour хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="b6615-106">Monitor hello device-to-cloud messages that are sent from your Adafruit Feather M0 WiFi Arduino board tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span>

<span data-ttu-id="b6615-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="b6615-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b6615-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="b6615-108">What you will learn</span></span>
<span data-ttu-id="b6615-109">В этой статье вы узнаете, как toouse hello gulp задачи чтения сообщений tooread сообщения сохраняются в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="b6615-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b6615-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="b6615-110">What you need</span></span>
<span data-ttu-id="b6615-111">Прежде чем запустить этот процесс, необходимо успешно выполнить [запустить пример приложения hello Azure blink на доске Arduino][run-blink-application].</span><span class="sxs-lookup"><span data-stu-id="b6615-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on your Arduino board][run-blink-application].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="b6615-112">Чтение новых сообщений из учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="b6615-112">Read new messages from your storage account</span></span>
<span data-ttu-id="b6615-113">В предыдущей статье hello на доске Arduino запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="b6615-113">In hello previous article, you ran a sample application on your Arduino board.</span></span> <span data-ttu-id="b6615-114">Пример приложения Hello отправлено центр Azure IoT tooyour сообщений.</span><span class="sxs-lookup"><span data-stu-id="b6615-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="b6615-115">Центр IoT tooyour сообщения Hello хранятся в хранилище таблиц Azure через приложение Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="b6615-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="b6615-116">Вы должны сообщений tooread строку соединения хранения Azure hello от хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="b6615-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="b6615-117">tooread сообщения, хранящиеся в хранилище таблиц Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b6615-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="b6615-118">Получите строку подключения hello, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="b6615-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="b6615-119">Первая команда Hello получает hello `storage name` , используемый в hello второй команды tooget hello строки подключения.</span><span class="sxs-lookup"><span data-stu-id="b6615-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="b6615-120">Используйте `iot-sample` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.</span><span class="sxs-lookup"><span data-stu-id="b6615-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="b6615-121">Привет открыть файл конфигурации `config-arduino.json` в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="b6615-121">Open hello configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. <span data-ttu-id="b6615-122">Замените `[Azure storage connection string]` со строкой подключения hello, полученный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="b6615-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="b6615-123">Сохранить hello `config-arduino.json` файла.</span><span class="sxs-lookup"><span data-stu-id="b6615-123">Save hello `config-arduino.json` file.</span></span>
5. <span data-ttu-id="b6615-124">Попытку отправки сообщений и их чтения из хранилища таблиц Azure, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="b6615-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   <span data-ttu-id="b6615-125">Hello логику для чтения из хранилища Azure таблицы находится в hello `azure-table.js` файла.</span><span class="sxs-lookup"><span data-stu-id="b6615-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>

   ![gulp run --read-storage][gulp-run]

## <a name="summary"></a><span data-ttu-id="b6615-127">Сводка</span><span class="sxs-lookup"><span data-stu-id="b6615-127">Summary</span></span>
<span data-ttu-id="b6615-128">Вы успешно подключен концентратор IoT tooyour Arduino платы в облаке hello и использовать сообщения hello blink образец приложения toosend устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="b6615-128">You've successfully connected your Arduino board tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="b6615-129">Можно также использовать hello Azure функция приложения toostore входящих IoT hub сообщения tooyour хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="b6615-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="b6615-130">Теперь можно отправлять сообщения облака на устройство из вашего tooyour концентратора IoT Arduino платы.</span><span class="sxs-lookup"><span data-stu-id="b6615-130">You can now send cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6615-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6615-131">Next steps</span></span>
<span data-ttu-id="b6615-132">[Отправка сообщений из облака на устройство][send-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="b6615-132">[Send cloud-to-device messages][send-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md