---
title: "Connect Raspberry PI (C) tooAzure IoT — занятия 3: хранилище таблиц | Документы Microsoft"
description: "Они записываются в хранилище таблиц Azure tooyour наблюдать за сообщений hello устройства в облако."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "получить данные из облака, облачная служба Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8c5558bb-3c31-4445-90e6-b1a978738545
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 307ce2bc595339790db7379cc011fe262c2b8734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="68ec1-104">Чтение сообщений, сохраненных в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="68ec1-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="68ec1-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="68ec1-105">What you will do</span></span>
<span data-ttu-id="68ec1-106">Монитор hello устройства в облако сообщения, которые отправляются из центра IoT tooyour Raspberry Pi 3 в виде сообщений hello записываются tooyour хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="68ec1-106">Monitor hello device-to-cloud messages that are sent from Raspberry Pi 3 tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="68ec1-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="68ec1-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="68ec1-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="68ec1-108">What you will learn</span></span>
<span data-ttu-id="68ec1-109">В этой статье вы узнаете, как toouse hello gulp задачи чтения сообщений tooread сообщения сохраняются в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="68ec1-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="68ec1-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="68ec1-110">What you need</span></span>
<span data-ttu-id="68ec1-111">Прежде чем запустить этот процесс, необходимо успешно выполнить [Запустите пример приложения hello Azure blink на Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="68ec1-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="68ec1-112">Чтение новых сообщений из учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="68ec1-112">Read new messages from your storage account</span></span>
<span data-ttu-id="68ec1-113">В предыдущей статье hello запуска примера приложения на Pi.</span><span class="sxs-lookup"><span data-stu-id="68ec1-113">In hello previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="68ec1-114">Пример приложения Hello отправлено центр Azure IoT tooyour сообщений.</span><span class="sxs-lookup"><span data-stu-id="68ec1-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="68ec1-115">Центр IoT tooyour сообщения Hello хранятся в хранилище таблиц Azure через приложение Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="68ec1-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="68ec1-116">Вы должны сообщений tooread строку соединения хранения Azure hello от хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="68ec1-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="68ec1-117">tooread сообщения, хранящиеся в хранилище таблиц Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="68ec1-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="68ec1-118">Получите строку подключения hello, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="68ec1-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="68ec1-119">Первая команда Hello получает hello `storage name` , используемый в hello второй команды tooget hello строки подключения.</span><span class="sxs-lookup"><span data-stu-id="68ec1-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="68ec1-120">Используйте `iot-sample` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.</span><span class="sxs-lookup"><span data-stu-id="68ec1-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="68ec1-121">Привет открыть файл конфигурации `config-raspberrypi.json` в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="68ec1-121">Open hello configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="68ec1-122">Замените `[Azure storage connection string]` со строкой подключения hello, полученный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="68ec1-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="68ec1-123">Сохранить hello `config-raspberrypi.json` файла.</span><span class="sxs-lookup"><span data-stu-id="68ec1-123">Save hello `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="68ec1-124">Попытку отправки сообщений и их чтения из хранилища таблиц Azure, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="68ec1-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="68ec1-125">Hello логику для чтения из хранилища Azure таблицы находится в hello `azure-table.js` файла.</span><span class="sxs-lookup"><span data-stu-id="68ec1-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>
   
   ![gulp run --read-storage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a><span data-ttu-id="68ec1-127">Сводка</span><span class="sxs-lookup"><span data-stu-id="68ec1-127">Summary</span></span>
<span data-ttu-id="68ec1-128">Вы успешно подключен центра IoT tooyour Pi в облаке hello и использовать сообщения hello blink образец приложения toosend устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="68ec1-128">You've successfully connected Pi tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="68ec1-129">Можно также использовать hello Azure функция приложения toostore входящих IoT hub сообщения tooyour хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="68ec1-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="68ec1-130">Теперь можно отправлять сообщения облака на устройство из вашего tooPi концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="68ec1-130">You can now send cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68ec1-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68ec1-131">Next steps</span></span>
[<span data-ttu-id="68ec1-132">Запустите образец приложения tooreceive сообщений облака на устройство</span><span class="sxs-lookup"><span data-stu-id="68ec1-132">Run a sample application tooreceive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

