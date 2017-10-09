---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 4. Хранилище таблиц | Документация Майкрософт"
description: "Сохранять сообщения из центра IoT tooyour Intel NUC, записывать их в хранилище таблиц tooAzure и затем прочитать их из облака hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "получить данные из облака, облачная служба Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 43e299d63bbbe10d4d867af25e700c3a7cc07c53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="825de-104">Чтение сообщений, сохраненных в Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="825de-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="825de-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="825de-105">What you will do</span></span>

- <span data-ttu-id="825de-106">Запустите образец приложения hello шлюза на шлюзе, отправляет сообщения tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="825de-106">Run hello gateway sample application on your gateway that sends messages tooyour IoT hub.</span></span>
- <span data-ttu-id="825de-107">Выполнение образца кода на узле компьютер tooread сообщения в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="825de-107">Run sample code on your host computer tooread messages in your Azure Table storage.</span></span>

<span data-ttu-id="825de-108">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="825de-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="825de-109">Новые знания</span><span class="sxs-lookup"><span data-stu-id="825de-109">What you will learn</span></span>

<span data-ttu-id="825de-110">Как toouse hello gulp средство toorun образец кода tooread сообщений hello в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="825de-110">How toouse hello gulp tool toorun hello sample code tooread messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="825de-111">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="825de-111">What you need</span></span>

<span data-ttu-id="825de-112">Будет иметь успешно hello следующие задания:</span><span class="sxs-lookup"><span data-stu-id="825de-112">You have have successfully done hello following tasks:</span></span>

- <span data-ttu-id="825de-113">[Создать приложение Azure функции hello и учетной записи хранилища Azure hello](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="825de-113">[Created hello Azure function app and hello Azure storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="825de-114">[Запустить образец приложения hello шлюза](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="825de-114">[Run hello gateway sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>
- <span data-ttu-id="825de-115">[Чтение сообщений из Центра Интернета вещей](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="825de-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="825de-116">Получение строк подключения службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="825de-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="825de-117">Раньше в ходе этого урока вы успешно создали учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="825de-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="825de-118">Строка подключения tooget hello учетной записи хранилища Azure hello, запуска hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="825de-118">tooget hello connection string of hello Azure storage account, run hello following commands:</span></span>

* <span data-ttu-id="825de-119">Выведите список всех учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="825de-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="825de-120">Получите строку подключения к службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="825de-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="825de-121">Используйте `iot-gateway` в качестве значения hello `{resource group name}` Если вы не изменили значение hello в занятии 2.</span><span class="sxs-lookup"><span data-stu-id="825de-121">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="825de-122">Настройка подключения устройства hello</span><span class="sxs-lookup"><span data-stu-id="825de-122">Configure hello device connection</span></span>

<span data-ttu-id="825de-123">Обновление hello `config-azure.json` так, чтобы hello образец кода, который выполняется на главном компьютере hello можно прочитать сообщение в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="825de-123">Update hello `config-azure.json` file so that hello sample code that runs on hello host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="825de-124">tooconfigure Здравствуйте подключения устройства, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="825de-124">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="825de-125">Файл конфигурации устройства Привет открыть `config-azure.json` , выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="825de-125">Open hello device configuration file `config-azure.json` by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![Конфигурация](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="825de-127">Замените `[Azure storage connection string]` с hello строка подключения хранилища Azure, который был получен.</span><span class="sxs-lookup"><span data-stu-id="825de-127">Replace `[Azure storage connection string]` with hello Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="825de-128">`[IoT hub connection string]` уже должна быть заменена в разделе [Чтение сообщений из Центра Интернета вещей Azure](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) в уроке 3.</span><span class="sxs-lookup"><span data-stu-id="825de-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="825de-129">Чтение сообщений в Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="825de-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="825de-130">Запустить образец приложения hello шлюза и чтения сообщений хранилища таблиц Azure, hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="825de-130">Run hello gateway sample application and read Azure Table storage messages by hello following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="825de-131">Сообщение toosave приложения Azure функция инициирует ваш центр IoT в хранилище таблиц Azure при поступлении нового сообщения.</span><span class="sxs-lookup"><span data-stu-id="825de-131">Your IoT hub triggers your Azure Function application toosave message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="825de-132">Hello `gulp run` команда выполняет шлюза образец приложения, который отправляет сообщения tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="825de-132">hello `gulp run` command runs gateway sample application that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="825de-133">С `table-storage` параметра, оно также создает hello tooreceive дочерних процесса, сохраненные сообщения в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="825de-133">With `table-storage` parameter, it also spawns a child process tooreceive hello saved message in your Azure Table storage.</span></span>

<span data-ttu-id="825de-134">сообщения приветствия, отправки и получения всех отображаемых мгновенно на hello же консоли окна в hello хост-компьютера.</span><span class="sxs-lookup"><span data-stu-id="825de-134">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="825de-135">экземпляр приложения Образец Hello нарушит автоматически в 40 секунд.</span><span class="sxs-lookup"><span data-stu-id="825de-135">hello sample application instance will terminate automatically in 40 seconds.</span></span>

   ![чтение Gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a><span data-ttu-id="825de-137">Сводка</span><span class="sxs-lookup"><span data-stu-id="825de-137">Summary</span></span>

<span data-ttu-id="825de-138">После выполнения сообщений hello tooread кода образца hello в хранилище таблиц Azure сохранен приложением Azure функции.</span><span class="sxs-lookup"><span data-stu-id="825de-138">You've run hello sample code tooread hello messages in your Azure Table storage saved by your Azure Function application.</span></span>
