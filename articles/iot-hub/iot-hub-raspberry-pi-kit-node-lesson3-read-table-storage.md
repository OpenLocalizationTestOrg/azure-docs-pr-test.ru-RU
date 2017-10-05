---
featureFlags: usabilla
title: "Подключение Raspberry Pi (Node) к Интернету вещей Azure. Урок 3. Хранилище таблиц | Документация Майкрософт"
description: "Отслеживайте сообщения, передаваемые с устройства в облако, по мере их записывания в хранилище таблиц Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "получить данные из облака, облачная служба Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 60084906c05ff9e5396f8e2378d73f7ac939d8df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="f59b8-104">Чтение сообщений, сохраненных в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="f59b8-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="f59b8-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="f59b8-105">What you will do</span></span>
<span data-ttu-id="f59b8-106">Отслеживание сообщений, передаваемых с устройства в облако (то есть с устройства Raspberry Pi 3 в центр Интернета вещей), по мере записывания сообщений в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="f59b8-106">Monitor the device-to-cloud messages that are sent from Raspberry Pi 3 to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="f59b8-107">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f59b8-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f59b8-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="f59b8-108">What you will learn</span></span>
<span data-ttu-id="f59b8-109">В этой статье вы узнаете, как использовать задачу gulp read-message для чтения сообщений, сохраненных в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="f59b8-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f59b8-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="f59b8-110">What you need</span></span>
<span data-ttu-id="f59b8-111">Прежде чем начинать, необходимо успешно выполнить инструкции статьи, посвященный [запуску на устройстве Raspberry Pi 3 примера приложения Azure для включения индикатора](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="f59b8-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="f59b8-112">Чтение новых сообщений из учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="f59b8-112">Read new messages from your storage account</span></span>
<span data-ttu-id="f59b8-113">В предыдущей статье вы запустили пример приложения на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="f59b8-113">In the previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="f59b8-114">Пример приложения отправлял сообщения в центр Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="f59b8-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="f59b8-115">Сообщения, отправленные в центр Интернета вещей, сохраняются в хранилище таблиц Azure с помощью приложения-функции Azure.</span><span class="sxs-lookup"><span data-stu-id="f59b8-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="f59b8-116">Для чтения сообщений из хранилища таблиц Azure потребуется строка подключения к хранилищу Azure.</span><span class="sxs-lookup"><span data-stu-id="f59b8-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="f59b8-117">Чтобы прочитать сообщения, сохраненные в хранилище таблиц Azure, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f59b8-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="f59b8-118">Получите строку подключения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f59b8-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="f59b8-119">Первая команда получает имя `storage name`, которое используется во второй команде для получения строки подключения.</span><span class="sxs-lookup"><span data-stu-id="f59b8-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="f59b8-120">Используйте `iot-sample` в качестве значения `{resource group name}`, если вы не меняли это значение.</span><span class="sxs-lookup"><span data-stu-id="f59b8-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="f59b8-121">Откройте файл конфигурации `config-raspberrypi.json` в Visual Studio Code, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f59b8-121">Open the configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="f59b8-122">Замените `[Azure storage connection string]` строкой подключения, полученной на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="f59b8-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="f59b8-123">Сохраните файл `config-raspberrypi.json`.</span><span class="sxs-lookup"><span data-stu-id="f59b8-123">Save the `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="f59b8-124">Отправьте сообщения еще раз и считайте их из хранилища таблиц Azure, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f59b8-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="f59b8-125">Логика чтения из хранилища таблиц Azure содержится в файле `azure-table.js`.</span><span class="sxs-lookup"><span data-stu-id="f59b8-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>
   
    ![gulp run --read-storage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a><span data-ttu-id="f59b8-127">Сводка</span><span class="sxs-lookup"><span data-stu-id="f59b8-127">Summary</span></span>
<span data-ttu-id="f59b8-128">Вы успешно подключили устройство Pi к Центру Интернета вещей в облаке и с помощью примера приложения для включения индикатора отправили сообщения с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="f59b8-128">You've successfully connected Pi to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="f59b8-129">Также вы использовали приложение-функцию Azure для сохранения входящих сообщений из Центра Интернета вещей в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="f59b8-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="f59b8-130">Теперь можно перейти к отправке сообщений из облака на устройство, т. е. из Центра Интернета вещей на устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="f59b8-130">You can now send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f59b8-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f59b8-131">Next steps</span></span>
<span data-ttu-id="f59b8-132">[Run the sample application to receive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md) (Запуск примера приложения для получения сообщений из облака на устройство)</span><span class="sxs-lookup"><span data-stu-id="f59b8-132">[Run the sample application to receive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)</span></span>

