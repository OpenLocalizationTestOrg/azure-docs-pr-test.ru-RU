---
title: "Подключение Edison Intel (узел) tooAzure IoT — занятия 3: отправка сообщений | Документы Microsoft"
description: "Развертывание и запуск образца приложения tooIntel Edison, отправляет сообщения центр IoT tooyour и hello Индикатор мигает."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT облачной службы, arduino отправки данных toocloud"
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
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="c7ec9-104">Запустите образец приложения toosend сообщения из устройства в облако</span><span class="sxs-lookup"><span data-stu-id="c7ec9-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c7ec9-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="c7ec9-105">What you will do</span></span>
<span data-ttu-id="c7ec9-106">В этой статье показано, как toodeploy и выполнение примера приложения на Edison Intel, который отправляет сообщения tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-106">This article will show you how toodeploy and run a sample application on Intel Edison that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="c7ec9-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c7ec9-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c7ec9-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="c7ec9-108">What you will learn</span></span>
<span data-ttu-id="c7ec9-109">Будет узнать, как toouse hello gulp toodeploy средства и запустите приложение C образец hello на Edison.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-109">You will learn how toouse hello gulp tool toodeploy and run hello sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c7ec9-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="c7ec9-110">What you need</span></span>
* <span data-ttu-id="c7ec9-111">Прежде чем начать эту задачу, необходимо успешно выполнить [создания приложения Azure функции и концентратор IoT tooprocess и хранилище учетной записи хранилища сообщений][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="c7ec9-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="c7ec9-112">Получение строк подключения Центра Интернета вещей и устройства</span><span class="sxs-lookup"><span data-stu-id="c7ec9-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="c7ec9-113">Строка подключения устройства Hello — используется tooconnect Edison tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-113">hello device connection string is used tooconnect Edison tooyour IoT hub.</span></span> <span data-ttu-id="c7ec9-114">Здравствуйте, строка подключения концентратора IoT является используется tooconnect вашей IoT hub toohello удостоверение устройства, представляющий Edison в центр IoT hello.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents Edison in hello IoT hub.</span></span>

* <span data-ttu-id="c7ec9-115">Перечислить все центры IoT в группе ресурсов, выполнив следующую команду Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="c7ec9-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="c7ec9-116">Используйте `iot-sample` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="c7ec9-117">Получите строку подключения концентратора IoT hello, выполнив следующую команду Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="c7ec9-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="c7ec9-118">`{my hub name}`— Имя hello, указанный вами создали концентратор IoT при регистрации Edison.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="c7ec9-119">Получите строку подключения устройства hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c7ec9-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="c7ec9-120">Используйте `myinteledison` в качестве значения hello `{device id}` Если вы не изменили значение hello.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-120">Use `myinteledison` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="c7ec9-121">Настройка подключения устройства hello</span><span class="sxs-lookup"><span data-stu-id="c7ec9-121">Configure hello device connection</span></span>
1. <span data-ttu-id="c7ec9-122">Инициализируйте hello файл конфигурации, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="c7ec9-122">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="c7ec9-123">Файл конфигурации устройства Привет открыть `config-edison.json` в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c7ec9-123">Open hello device configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="c7ec9-125">Сделать после замены в hello hello `config-edison.json` файла:</span><span class="sxs-lookup"><span data-stu-id="c7ec9-125">Make hello following replacements in hello `config-edison.json` file:</span></span>

   * <span data-ttu-id="c7ec9-126">Замените **[устройства имя узла или IP-адрес]** с IP-адрес устройства hello помечен работу при настройке устройства.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-126">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="c7ec9-127">Замените **[строка подключения устройств IoT]** с hello `device connection string` полученных.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-127">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="c7ec9-128">Замените **[строка подключения концентратора IoT]** с hello `iot hub connection string` полученных.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-128">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c7ec9-129">В этой статье не требуется `azure_storage_connection_string`.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="c7ec9-130">Оставьте эту настройку без изменений.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-130">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="c7ec9-131">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="c7ec9-131">Deploy and run hello sample application</span></span>
<span data-ttu-id="c7ec9-132">Развертывание и запуск образца приложения hello на Edison, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c7ec9-132">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="c7ec9-133">Проверка работы образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="c7ec9-133">Verify that hello sample application works</span></span>
<span data-ttu-id="c7ec9-134">Вы увидите hello Индикатор, подключенных tooEdison мигает каждые две секунды.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-134">You should see hello LED that is connected tooEdison blinking every two seconds.</span></span> <span data-ttu-id="c7ec9-135">Каждый раз hello Индикатор мигает, пример приложения hello отправляет центр IoT tooyour сообщения и подтверждает, что это сообщение hello было успешно отправлено tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-135">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="c7ec9-136">Кроме того каждое сообщение, полученных центра IoT hello выводится в окне консоли hello.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-136">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="c7ec9-137">Пример приложения Hello автоматически завершает после отправки 20 сообщений.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-137">hello sample application terminates automatically after sending 20 messages.</span></span>

![Пример приложения с отправленными и полученными сообщениями][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="c7ec9-139">Сводка</span><span class="sxs-lookup"><span data-stu-id="c7ec9-139">Summary</span></span>
<span data-ttu-id="c7ec9-140">Развертывания и запустите hello новый образец приложения blink Edison центр IoT tooyour toosend сообщения из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-140">You've deployed and run hello new blink sample application on Edison toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="c7ec9-141">Теперь отслеживать сообщения, записываемые toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="c7ec9-141">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7ec9-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c7ec9-142">Next steps</span></span>
<span data-ttu-id="c7ec9-143">[Чтение сообщений, сохраненных в службе хранилища Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="c7ec9-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md