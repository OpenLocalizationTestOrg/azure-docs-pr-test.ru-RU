---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Урок 3. Запуск примера | Документация Майкрософт"
description: "Развертывание и запуск на устройстве Raspberry Pi 3 примера приложения, которое отправляет сообщения в Центр Интернета вещей и заставляет светодиодный индикатор мигать."
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
ms.openlocfilehash: e583ba455a94f9afcc7b31e49425b518d7968919
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="cdfa1-104">Запуск примера приложения для отправки сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="cdfa1-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="cdfa1-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="cdfa1-105">What you will do</span></span>
<span data-ttu-id="cdfa1-106">В этой статье показано, как развернуть и запустить на устройстве Raspberry Pi 3 пример приложения, которое отправляет сообщения в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="cdfa1-107">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cdfa1-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cdfa1-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="cdfa1-108">What you will learn</span></span>
<span data-ttu-id="cdfa1-109">Вы узнаете, как с помощью средства Gulp развернуть и запустить пример приложения Node.js на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cdfa1-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="cdfa1-110">What you need</span></span>
* <span data-ttu-id="cdfa1-111">К выполнению этой задачи следует приступать только после выполнения действий, описанных в статье [Create an Azure function app and an Azure Storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) (Создание приложения-функции Azure и учетной записи хранения Azure для обработки и хранения сообщений Центра Интернета вещей).</span><span class="sxs-lookup"><span data-stu-id="cdfa1-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="cdfa1-112">Получение строк подключения Центра Интернета вещей и устройства</span><span class="sxs-lookup"><span data-stu-id="cdfa1-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="cdfa1-113">Строка подключения устройства используется устройством Pi для подключения к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="cdfa1-114">Строка подключения Центра Интернета вещей используется для подключения к реестру удостоверений в Центре Интернета вещей, чтобы управлять устройствами, которым разрешено подключаться к этому центру.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="cdfa1-115">Для вывода списка всех Центров Интернета вещей в группе ресурсов выполните следующую команду Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="cdfa1-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="cdfa1-116">Используйте `iot-sample` в качестве значения `{resource group name}`, если вы не меняли это значение.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="cdfa1-117">Для получения строки подключения Центра Интернета вещей выполните следующую команду интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="cdfa1-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="cdfa1-118">`{my hub name}` — это имя, которое вы указали при создании Центра Интернета вещей и регистрации устройства Pi.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="cdfa1-119">Для получения строки подключения устройства выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cdfa1-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="cdfa1-120">Используйте `myraspberrypi` в качестве значения `{device id}`, если вы не меняли это значение.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="cdfa1-121">Настройка подключения устройства</span><span class="sxs-lookup"><span data-stu-id="cdfa1-121">Configure the device connection</span></span>
1. <span data-ttu-id="cdfa1-122">Запустите файл конфигурации, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="cdfa1-123">Выполните также **gulp install-tools**, если это не было сделано на уроке 1.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="cdfa1-124">Откройте файл конфигурации устройства `config-raspberrypi.json` в Visual Studio Code, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-124">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="cdfa1-126">В файле `config-raspberrypi.json` выполните следующие замены.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-126">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="cdfa1-127">Замените **[device hostname or IP address]** IP-адресом или именем узла устройства, полученным в результате выполнения команды `device-discovery-cli`, или значением, унаследованным из настроек устройства.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-127">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="cdfa1-128">Замените **[строка подключения устройства Интернета вещей]** на полученное значение `device connection string`.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-128">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="cdfa1-129">Замените **[IoT hub connection string]** (строка подключения Центра Интернета вещей) полученным значением `iot hub connection string`.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-129">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="cdfa1-130">В этой статье не требуется `azure_storage_connection_string`.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="cdfa1-131">Оставьте эту настройку без изменений.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-131">Keep it as is.</span></span>

<span data-ttu-id="cdfa1-132">Обновите файл `config-raspberrypi.json`, чтобы можно было развернуть пример приложения с компьютера.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-132">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="cdfa1-133">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="cdfa1-133">Deploy and run the sample application</span></span>
<span data-ttu-id="cdfa1-134">Разверните и запустите пример приложения на устройстве Pi, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-134">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="cdfa1-135">Проверка работы примера приложения</span><span class="sxs-lookup"><span data-stu-id="cdfa1-135">Verify that the sample application works</span></span>
<span data-ttu-id="cdfa1-136">Светодиодный индикатор, подключенный к устройству Pi, должен мигать с частотой в две секунды.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-136">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="cdfa1-137">Каждый раз, когда индикатор мигает, пример приложения отправляет сообщение в Центр Интернета вещей и проверяет, что сообщение успешно отправлено.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-137">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="cdfa1-138">Кроме того, каждое сообщение, полученное Центром Интернета вещей, выводится в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-138">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="cdfa1-139">Пример приложения автоматически завершает работу после отправки 20 сообщений.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-139">The sample application terminates automatically after sending 20 messages.</span></span>

![Пример приложения с отправленными и полученными сообщениями](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="cdfa1-141">Сводка</span><span class="sxs-lookup"><span data-stu-id="cdfa1-141">Summary</span></span>
<span data-ttu-id="cdfa1-142">Вы развернули и запустили новый пример приложения для включения индикатора на устройстве Pi для отправки сообщений с устройства в облако, то есть в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-142">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="cdfa1-143">Теперь можно отслеживать сообщения по мере их записывания в учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="cdfa1-143">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdfa1-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cdfa1-144">Next steps</span></span>
[<span data-ttu-id="cdfa1-145">Чтение сообщений, сохраненных в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="cdfa1-145">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

