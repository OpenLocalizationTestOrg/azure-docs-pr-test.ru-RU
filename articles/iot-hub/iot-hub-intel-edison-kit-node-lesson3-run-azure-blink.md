---
title: "Подключение Intel Edison (Node) к Интернету вещей Azure. Урок 3. Отправка сообщений | Документация Майкрософт"
description: "Развертывание и запуск на устройстве Intel Edison примера приложения, которое отправляет сообщения в Центр Интернета вещей и заставляет светодиодный индикатор мигать."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "облачная служба Интернета вещей, отправка данных в облако с помощью Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d4b520b9a1852a285b1e10b5b35447a54313af9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="b6f5c-104">Запуск примера приложения для отправки сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="b6f5c-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b6f5c-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="b6f5c-105">What you will do</span></span>
<span data-ttu-id="b6f5c-106">В этой статье показано, как развернуть и запустить на устройстве Intel Edison пример приложения, которое отправляет сообщения в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span></span> <span data-ttu-id="b6f5c-107">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="b6f5c-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b6f5c-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="b6f5c-108">What you will learn</span></span>
<span data-ttu-id="b6f5c-109">Вы узнаете, как с помощью инструмента Gulp развернуть и запустить пример приложения C на устройстве Edison.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b6f5c-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="b6f5c-110">What you need</span></span>
* <span data-ttu-id="b6f5c-111">К выполнению этой задачи следует приступать только после выполнения действий, описанных в статье [Создание приложения-функции Azure и учетной записи хранения Azure][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="b6f5c-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="b6f5c-112">Получение строк подключения Центра Интернета вещей и устройства</span><span class="sxs-lookup"><span data-stu-id="b6f5c-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="b6f5c-113">Строка подключения устройства используется для подключения устройства Edison к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-113">The device connection string is used to connect Edison to your IoT hub.</span></span> <span data-ttu-id="b6f5c-114">Строка подключения Центра Интернета вещей используется для его подключения к удостоверению устройства, которое представляет устройство Edison в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span></span>

* <span data-ttu-id="b6f5c-115">Для вывода списка всех Центров Интернета вещей в группе ресурсов выполните следующую команду Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="b6f5c-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="b6f5c-116">Используйте `iot-sample` в качестве значения `{resource group name}`, если вы не меняли это значение.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="b6f5c-117">Для получения строки подключения Центра Интернета вещей выполните следующую команду интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="b6f5c-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="b6f5c-118">`{my hub name}` — это имя, которое вы указали при создании Центра Интернета вещей и регистрации устройства Edison.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="b6f5c-119">Для получения строки подключения устройства выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b6f5c-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="b6f5c-120">Используйте `myinteledison` в качестве значения `{device id}`, если вы не меняли это значение.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="b6f5c-121">Настройка подключения устройства</span><span class="sxs-lookup"><span data-stu-id="b6f5c-121">Configure the device connection</span></span>
1. <span data-ttu-id="b6f5c-122">Запустите файл конфигурации, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-122">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="b6f5c-123">Откройте файл конфигурации устройства `config-edison.json` в Visual Studio Code, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-123">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="b6f5c-125">В файле `config-edison.json` выполните следующие замены.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-125">Make the following replacements in the `config-edison.json` file:</span></span>

   * <span data-ttu-id="b6f5c-126">Замените **[device hostname or IP address]** IP-адресом, указанным при настройке устройства.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-126">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="b6f5c-127">Замените **[строка подключения устройства Интернета вещей]** на полученное значение `device connection string`.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="b6f5c-128">Замените **[IoT hub connection string]** (строка подключения Центра Интернета вещей) полученным значением `iot hub connection string`.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b6f5c-129">В этой статье не требуется `azure_storage_connection_string`.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="b6f5c-130">Оставьте эту настройку без изменений.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-130">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="b6f5c-131">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="b6f5c-131">Deploy and run the sample application</span></span>
<span data-ttu-id="b6f5c-132">Разверните и запустите пример приложения в Edison, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b6f5c-132">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="b6f5c-133">Проверка работы примера приложения</span><span class="sxs-lookup"><span data-stu-id="b6f5c-133">Verify that the sample application works</span></span>
<span data-ttu-id="b6f5c-134">Светодиодный индикатор, подключенный к устройству Edison, должен мигать с частотой в две секунды.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-134">You should see the LED that is connected to Edison blinking every two seconds.</span></span> <span data-ttu-id="b6f5c-135">Каждый раз, когда индикатор мигает, пример приложения отправляет сообщение в Центр Интернета вещей и проверяет, что сообщение успешно отправлено.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-135">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="b6f5c-136">Кроме того, каждое сообщение, полученное Центром Интернета вещей, выводится в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-136">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="b6f5c-137">Пример приложения автоматически завершает работу после отправки 20 сообщений.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-137">The sample application terminates automatically after sending 20 messages.</span></span>

![Пример приложения с отправленными и полученными сообщениями][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="b6f5c-139">Сводка</span><span class="sxs-lookup"><span data-stu-id="b6f5c-139">Summary</span></span>
<span data-ttu-id="b6f5c-140">Вы развернули и запустили новый пример приложения для включения индикатора на устройстве Edison для отправки сообщений с устройства в облако, то есть в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-140">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="b6f5c-141">Теперь можно отслеживать сообщения по мере их записывания в учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="b6f5c-141">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6f5c-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6f5c-142">Next steps</span></span>
<span data-ttu-id="b6f5c-143">[Чтение сообщений, сохраненных в службе хранилища Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="b6f5c-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md