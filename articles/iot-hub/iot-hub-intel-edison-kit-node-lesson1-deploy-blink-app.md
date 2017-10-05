---
title: "Подключение Intel Edison (Node) к Интернету вещей Azure. Урок 1. Развертывание приложения | Документация Майкрософт"
description: "Клонируйте пример приложения C c GitHub и разверните его с помощью инструмента Gulp на плате Intel Edison. Это приложение будет каждые две секунды включать и выключать светодиодный индикатор на компьютере."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "проекты светодиодного индикатора Arduino, включение светодиодного индикатора Arduino, код включения индикатора Arduino, программа включения индикатора Arduino, пример включения индикатора Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8490fbbf14183432c665165412f00955d6323580
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="e16ab-105">Создание и развертывание приложения для включения индикатора</span><span class="sxs-lookup"><span data-stu-id="e16ab-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e16ab-106">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="e16ab-106">What you will do</span></span>
<span data-ttu-id="e16ab-107">Клонирование примера приложения C из GitHub и его развертывание с помощью инструмента Gulp на устройстве Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="e16ab-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="e16ab-108">Этот пример приложения будет каждые две секунды включать светодиодный индикатор, подключенный к плате.</span><span class="sxs-lookup"><span data-stu-id="e16ab-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="e16ab-109">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e16ab-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e16ab-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="e16ab-110">What you will learn</span></span>
* <span data-ttu-id="e16ab-111">Как развертывать и запускать пример приложения в Edison.</span><span class="sxs-lookup"><span data-stu-id="e16ab-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e16ab-112">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="e16ab-112">What you need</span></span>
<span data-ttu-id="e16ab-113">Необходимо успешно выполнить следующие операции:</span><span class="sxs-lookup"><span data-stu-id="e16ab-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="e16ab-114">[Настройка устройства][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="e16ab-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="e16ab-115">[Get the tools][get-the-tools] (Получение инструментов)</span><span class="sxs-lookup"><span data-stu-id="e16ab-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="e16ab-116">Открытие примера приложения</span><span class="sxs-lookup"><span data-stu-id="e16ab-116">Open the sample application</span></span>
<span data-ttu-id="e16ab-117">Чтобы открыть пример приложения, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e16ab-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="e16ab-118">Клонируйте пример репозитория из GitHub, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e16ab-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="e16ab-119">Откройте пример приложения в Visual Studio Code, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e16ab-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Структура репозитория][repo-structure]

<span data-ttu-id="e16ab-121">Файл в подпапке `app` — это ключевой исходный файл, содержащий код для управления светодиодным индикатором.</span><span class="sxs-lookup"><span data-stu-id="e16ab-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="e16ab-122">Установка зависимостей приложения</span><span class="sxs-lookup"><span data-stu-id="e16ab-122">Install application dependencies</span></span>
<span data-ttu-id="e16ab-123">Установите библиотеки и другие модули, необходимые для примера приложения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e16ab-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="e16ab-124">Настройка подключения устройства</span><span class="sxs-lookup"><span data-stu-id="e16ab-124">Configure the device connection</span></span>
<span data-ttu-id="e16ab-125">Чтобы настроить подключение устройства, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e16ab-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="e16ab-126">Создайте файл конфигурации устройства, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="e16ab-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="e16ab-127">Файл конфигурации `config-edison.json` содержит учетные данные пользователя для входа в Edison.</span><span class="sxs-lookup"><span data-stu-id="e16ab-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="e16ab-128">Чтобы избежать утечки учетных данных пользователя, файл конфигурации создается в подпапке `.iot-hub-getting-started` домашней папки на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e16ab-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="e16ab-129">Откройте файл конфигурации устройства в Visual Studio Code, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="e16ab-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="e16ab-130">Замените заполнитель `[device hostname or IP address]` и `[device password]` на IP-адрес и пароль, указанный на предыдущем уроке.</span><span class="sxs-lookup"><span data-stu-id="e16ab-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="e16ab-132">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="e16ab-132">Congratulations!</span></span> <span data-ttu-id="e16ab-133">Вы успешно создали пример приложения для платы Edison.</span><span class="sxs-lookup"><span data-stu-id="e16ab-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="e16ab-134">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="e16ab-134">Deploy and run the sample application</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="e16ab-135">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="e16ab-135">Deploy and run the sample app</span></span>
<span data-ttu-id="e16ab-136">Разверните и запустите пример приложения, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e16ab-136">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="e16ab-137">Проверка работы приложения</span><span class="sxs-lookup"><span data-stu-id="e16ab-137">Verify the app works</span></span>
<span data-ttu-id="e16ab-138">После того, как светодиодный индикатор мигнет 20 раз, пример приложения завершит работу автоматически.</span><span class="sxs-lookup"><span data-stu-id="e16ab-138">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="e16ab-139">Если светодиодный индикатор не мигает, см. способы решения распространенных проблем в [руководстве по устранению неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e16ab-139">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![Светодиодный индикатор мигает][led-blinking]

## <a name="summary"></a><span data-ttu-id="e16ab-141">Сводка</span><span class="sxs-lookup"><span data-stu-id="e16ab-141">Summary</span></span>
<span data-ttu-id="e16ab-142">Вы установили необходимые инструменты для работы с устройством Edison и развернули пример приложения, заставляющего светодиодный индикатор мигать.</span><span class="sxs-lookup"><span data-stu-id="e16ab-142">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="e16ab-143">Теперь можно приступать к созданию, развертыванию и запуску другого примера приложения, которое подключает устройство Edison к Центру Интернета вещей Azure для отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="e16ab-143">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e16ab-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e16ab-144">Next steps</span></span>
<span data-ttu-id="e16ab-145">[Get the Azure tools][get-the-azure-tools] (Получение инструментов Azure)</span><span class="sxs-lookup"><span data-stu-id="e16ab-145">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
