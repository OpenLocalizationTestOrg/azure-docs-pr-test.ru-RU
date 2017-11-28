---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 4. Хранилище таблиц | Документация Майкрософт"
description: "Сохраняйте сообщения из Intel NUC в Центр Интернета вещей, записывайте их в Хранилище таблиц Azure, а затем читайте их из облака."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "получить данные из облака, облачная служба Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 72659ef3a7fd2f6011590d37176fd05503269aff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="2464a-104">Чтение сообщений, сохраненных в Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="2464a-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2464a-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="2464a-105">What you will do</span></span>

- <span data-ttu-id="2464a-106">Запуск примера приложения шлюза для шлюза, который отправляет сообщения в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="2464a-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span></span>
- <span data-ttu-id="2464a-107">Запустите пример кода на главном компьютере для чтения сообщений в Хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="2464a-107">Then run a sample code on your host computer to read the messages in your Azure Table storage.</span></span> 

<span data-ttu-id="2464a-108">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2464a-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2464a-109">Новые знания</span><span class="sxs-lookup"><span data-stu-id="2464a-109">What you will learn</span></span>

<span data-ttu-id="2464a-110">Использование инструмента Gulp для чтения сообщений в Хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="2464a-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2464a-111">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="2464a-111">What you need</span></span>

<span data-ttu-id="2464a-112">Вы успешно выполнили следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="2464a-112">You have have successfully done the following tasks:</span></span>

- <span data-ttu-id="2464a-113">[Создание приложения-функции Azure и учетной записи хранения Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="2464a-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="2464a-114">[Запуск примера приложения шлюза](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="2464a-114">[Run the gateway sample application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span></span>
- <span data-ttu-id="2464a-115">[Чтение сообщений из Центра Интернета вещей](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="2464a-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="2464a-116">Получение строк подключения службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="2464a-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="2464a-117">Раньше в ходе этого урока вы успешно создали учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="2464a-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="2464a-118">Чтобы получить строку подключения учетной записи хранения Azure, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="2464a-118">To get the connection string of the Azure storage account, run the following commands:</span></span>

* <span data-ttu-id="2464a-119">Выведите список всех учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="2464a-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="2464a-120">Получите строку подключения к службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="2464a-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="2464a-121">Используйте iot-gateway в качестве значения `{resource group name}`, если в уроке 2 значение не изменялось.</span><span class="sxs-lookup"><span data-stu-id="2464a-121">Use iot-gateway as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="2464a-122">Настройка подключения устройства</span><span class="sxs-lookup"><span data-stu-id="2464a-122">Configure the device connection</span></span>

<span data-ttu-id="2464a-123">Обновите файл `config-azure.json`, чтобы пример кода, который выполняется на главном компьютере, смог читать сообщения в Хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="2464a-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="2464a-124">Чтобы настроить подключение устройства, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2464a-124">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="2464a-125">Откройте файл конфигурации устройства `config-azure.json`, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="2464a-125">Open the device configuration file `config-azure.json` by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![Конфигурация](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="2464a-127">Замените `[Azure storage connection string]` полученной строкой подключения к службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="2464a-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="2464a-128">`[IoT hub connection string]` уже должна быть заменена в разделе [Чтение сообщений из Центра Интернета вещей Azure](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) в уроке 3.</span><span class="sxs-lookup"><span data-stu-id="2464a-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="2464a-129">Чтение сообщений в Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="2464a-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="2464a-130">Запустите пример приложения шлюза и прочтите сообщения Хранилища таблиц Azure, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2464a-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="2464a-131">Ваш Центр Интернета вещей активирует приложение-функцию Azure, чтобы сохранить сообщение в Хранилище таблиц Azure при поступлении нового сообщения.</span><span class="sxs-lookup"><span data-stu-id="2464a-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="2464a-132">Команда `gulp run` запускает пример приложения шлюза, который отправляет сообщения в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="2464a-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span></span> <span data-ttu-id="2464a-133">С помощью параметра `table-storage` она также создает дочерний процесс для получения сохраненного сообщения в Хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="2464a-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span></span>

<span data-ttu-id="2464a-134">Все отправленные и полученные сообщения мгновенно появляются в том же окне консоли на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="2464a-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="2464a-135">Экземпляр примера приложения прекращает свое действие автоматически через 40 секунд.</span><span class="sxs-lookup"><span data-stu-id="2464a-135">The sample application instance will terminate automatically in 40 seconds.</span></span>

   ![чтение Gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a><span data-ttu-id="2464a-137">Сводка</span><span class="sxs-lookup"><span data-stu-id="2464a-137">Summary</span></span>

<span data-ttu-id="2464a-138">Вы запустили пример кода для чтения сообщений в Хранилище таблиц Azure, сохраненных приложением-функцией Azure.</span><span class="sxs-lookup"><span data-stu-id="2464a-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span></span>