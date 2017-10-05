---
title: "Подключение Intel Edison (C) к Интернету вещей Azure. Урок 3. Отслеживание сообщений | Документация Майкрософт"
description: "Отслеживайте сообщения, передаваемые с устройства в облако, по мере их записывания в хранилище таблиц Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "данные в облаке, коллекция облачных данных, облачная служба Интернета вещей, данные Интернета вещей"
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
ms.openlocfilehash: 249b5e0e96051fa2adeedfb9befd98fc939b4d40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="fe829-104">Чтение сообщений, сохраненных в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="fe829-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="fe829-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="fe829-105">What you will do</span></span>
<span data-ttu-id="fe829-106">Отслеживание сообщений, передаваемых с устройства в облако (то есть с устройства Intel Edison в центр Интернета вещей), по мере их записывания в Хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="fe829-106">Monitor the device-to-cloud messages that are sent from Intel Edison to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="fe829-107">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="fe829-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fe829-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="fe829-108">What you will learn</span></span>
<span data-ttu-id="fe829-109">В этой статье вы узнаете, как использовать задачу gulp read-message для чтения сообщений, сохраненных в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="fe829-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fe829-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="fe829-110">What you need</span></span>
<span data-ttu-id="fe829-111">Прежде чем начать, необходимо успешно выполнить инструкции, изложенные в статье [Run a sample application to send device-to-cloud messages][run-the-azure-blink-sample-application-on-intel-edison] (Запуск примера приложения для отправки сообщений с устройства в облако).</span><span class="sxs-lookup"><span data-stu-id="fe829-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="fe829-112">Чтение новых сообщений из учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="fe829-112">Read new messages from your storage account</span></span>
<span data-ttu-id="fe829-113">В предыдущей статье вы запустили пример приложения на устройстве Edison.</span><span class="sxs-lookup"><span data-stu-id="fe829-113">In the previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="fe829-114">Пример приложения отправлял сообщения в центр Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="fe829-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="fe829-115">Сообщения, отправленные в центр Интернета вещей, сохраняются в хранилище таблиц Azure с помощью приложения-функции Azure.</span><span class="sxs-lookup"><span data-stu-id="fe829-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="fe829-116">Для чтения сообщений из хранилища таблиц Azure потребуется строка подключения к хранилищу Azure.</span><span class="sxs-lookup"><span data-stu-id="fe829-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="fe829-117">Чтобы прочитать сообщения, сохраненные в хранилище таблиц Azure, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fe829-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="fe829-118">Получите строку подключения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fe829-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="fe829-119">Первая команда получает имя `storage name`, которое используется во второй команде для получения строки подключения.</span><span class="sxs-lookup"><span data-stu-id="fe829-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="fe829-120">Используйте `iot-sample` в качестве значения `{resource group name}`, если вы не меняли это значение.</span><span class="sxs-lookup"><span data-stu-id="fe829-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="fe829-121">Откройте файл конфигурации `config-edison.json` в Visual Studio Code, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="fe829-121">Open the configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="fe829-122">Замените `[Azure storage connection string]` строкой подключения, полученной на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="fe829-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="fe829-123">Сохраните файл `config-edison.json`.</span><span class="sxs-lookup"><span data-stu-id="fe829-123">Save the `config-edison.json` file.</span></span>
5. <span data-ttu-id="fe829-124">Отправьте сообщения еще раз и считайте их из хранилища таблиц Azure, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="fe829-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="fe829-125">Логика чтения из хранилища таблиц Azure содержится в файле `azure-table.js`.</span><span class="sxs-lookup"><span data-stu-id="fe829-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![gulp run --read-storage][gulp run]

## <a name="summary"></a><span data-ttu-id="fe829-127">Сводка</span><span class="sxs-lookup"><span data-stu-id="fe829-127">Summary</span></span>
<span data-ttu-id="fe829-128">Вы успешно подключили устройство Edison к Центру Интернета вещей в облаке и с помощью примера приложения для включения индикатора отправили сообщения с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="fe829-128">You've successfully connected Edison to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="fe829-129">Также вы использовали приложение-функцию Azure для сохранения входящих сообщений из Центра Интернета вещей в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="fe829-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="fe829-130">Теперь можно перейти к отправке сообщений из облака на устройство, т. е. из Центра Интернета вещей на устройство Edison.</span><span class="sxs-lookup"><span data-stu-id="fe829-130">You can now send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe829-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fe829-131">Next steps</span></span>
<span data-ttu-id="fe829-132">[Запуск примера приложения для получения сообщений из облака на устройство][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="fe829-132">[Run a sample application to receive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md