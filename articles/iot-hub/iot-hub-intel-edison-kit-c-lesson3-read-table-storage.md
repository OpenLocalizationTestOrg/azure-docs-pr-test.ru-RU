---
title: "Connect Intel Edison (C) tooAzure IoT — занятия 3: наблюдения за сообщениями | Документы Microsoft"
description: "Они записываются в хранилище таблиц Azure tooyour наблюдать за сообщений hello устройства в облако."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "данные в облако hello, сбор данных облака, iot облачной службы, iot данных"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: cad545c3-dd88-486c-a663-d587a924ccd4
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2679b22f2987f77ecd1eea03044ed8ea03bf73f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="c57ad-104">Чтение сообщений, сохраненных в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c57ad-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c57ad-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="c57ad-105">What you will do</span></span>
<span data-ttu-id="c57ad-106">Монитор hello устройства в облако сообщения, которые отправляются из центра IoT tooyour Intel Edison в виде сообщений hello записываются tooyour хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="c57ad-106">Monitor hello device-to-cloud messages that are sent from Intel Edison tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="c57ad-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c57ad-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c57ad-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="c57ad-108">What you will learn</span></span>
<span data-ttu-id="c57ad-109">В этой статье вы узнаете, как toouse hello gulp задачи чтения сообщений tooread сообщения сохраняются в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="c57ad-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c57ad-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="c57ad-110">What you need</span></span>
<span data-ttu-id="c57ad-111">Прежде чем запустить этот процесс, необходимо успешно выполнить [проведение пример приложения hello Azure blink Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="c57ad-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="c57ad-112">Чтение новых сообщений из учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="c57ad-112">Read new messages from your storage account</span></span>
<span data-ttu-id="c57ad-113">В предыдущей статье hello выполнена образец приложения для Edison.</span><span class="sxs-lookup"><span data-stu-id="c57ad-113">In hello previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="c57ad-114">Пример приложения Hello отправлено центр Azure IoT tooyour сообщений.</span><span class="sxs-lookup"><span data-stu-id="c57ad-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="c57ad-115">Центр IoT tooyour сообщения Hello хранятся в хранилище таблиц Azure через приложение Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="c57ad-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="c57ad-116">Вы должны сообщений tooread строку соединения хранения Azure hello от хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="c57ad-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="c57ad-117">tooread сообщения, хранящиеся в хранилище таблиц Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c57ad-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="c57ad-118">Получите строку подключения hello, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="c57ad-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="c57ad-119">Первая команда Hello получает hello `storage name` , используемый в hello второй команды tooget hello строки подключения.</span><span class="sxs-lookup"><span data-stu-id="c57ad-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="c57ad-120">Используйте `iot-sample` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.</span><span class="sxs-lookup"><span data-stu-id="c57ad-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="c57ad-121">Привет открыть файл конфигурации `config-edison.json` в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c57ad-121">Open hello configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="c57ad-122">Замените `[Azure storage connection string]` со строкой подключения hello, полученный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="c57ad-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="c57ad-123">Сохранить hello `config-edison.json` файла.</span><span class="sxs-lookup"><span data-stu-id="c57ad-123">Save hello `config-edison.json` file.</span></span>
5. <span data-ttu-id="c57ad-124">Попытку отправки сообщений и их чтения из хранилища таблиц Azure, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c57ad-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="c57ad-125">Hello логику для чтения из хранилища Azure таблицы находится в hello `azure-table.js` файла.</span><span class="sxs-lookup"><span data-stu-id="c57ad-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>

   ![gulp run --read-storage][gulp run]

## <a name="summary"></a><span data-ttu-id="c57ad-127">Сводка</span><span class="sxs-lookup"><span data-stu-id="c57ad-127">Summary</span></span>
<span data-ttu-id="c57ad-128">Вы успешно подключен центра IoT tooyour Edison в облаке hello и использовать сообщения hello blink образец приложения toosend устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="c57ad-128">You've successfully connected Edison tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="c57ad-129">Можно также использовать hello Azure функция приложения toostore входящих IoT hub сообщения tooyour хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="c57ad-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="c57ad-130">Теперь можно отправлять сообщения облака на устройство из вашего tooEdison концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="c57ad-130">You can now send cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c57ad-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c57ad-131">Next steps</span></span>
<span data-ttu-id="c57ad-132">[Запустите образец приложения tooreceive сообщений облака на устройство][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="c57ad-132">[Run a sample application tooreceive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md