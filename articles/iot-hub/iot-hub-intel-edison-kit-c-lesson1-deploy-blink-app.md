---
title: "Connect Intel Edison (C) tooAzure IoT — занятия 1: развертывание приложения | Документы Microsoft"
description: "Клонировать пример C приложения hello из GitHub и запуска этого приложения tooyour плата Intel Edison gulp toodeploy. В этом образце приложения мигает hello Индикатор подключен toohello плата каждые две секунды."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "проекты светодиодного индикатора Arduino, включение светодиодного индикатора Arduino, код включения индикатора Arduino, программа включения индикатора Arduino, пример включения индикатора Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="e21ee-105">Создание и развертывание приложения hello мерцания</span><span class="sxs-lookup"><span data-stu-id="e21ee-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e21ee-106">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="e21ee-106">What you will do</span></span>
<span data-ttu-id="e21ee-107">Клонировать пример C приложения hello из GitHub и использовать приложения образец tooIntel Edison hello gulp средство toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="e21ee-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="e21ee-108">Пример приложения Hello мигает hello Индикатор подключен toohello плата каждые две секунды.</span><span class="sxs-lookup"><span data-stu-id="e21ee-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="e21ee-109">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e21ee-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e21ee-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="e21ee-110">What you will learn</span></span>
* <span data-ttu-id="e21ee-111">Как toodeploy и выполнения hello образец приложения на Edison.</span><span class="sxs-lookup"><span data-stu-id="e21ee-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e21ee-112">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="e21ee-112">What you need</span></span>
<span data-ttu-id="e21ee-113">Необходимо успешно выполнить hello следующие операции:</span><span class="sxs-lookup"><span data-stu-id="e21ee-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="e21ee-114">[Настройка устройства][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="e21ee-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="e21ee-115">[Получить средства hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="e21ee-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="e21ee-116">Привет открыть образец приложения</span><span class="sxs-lookup"><span data-stu-id="e21ee-116">Open hello sample application</span></span>
<span data-ttu-id="e21ee-117">tooopen hello образец приложения, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e21ee-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="e21ee-118">Клонирование репозитория образец hello из GitHub, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e21ee-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="e21ee-119">Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="e21ee-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Структура репозитория][repo-structure]

<span data-ttu-id="e21ee-121">файл Hello в hello `app` подпапка является hello ключа исходного файла, содержащего hello toocontrol кода hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="e21ee-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="e21ee-122">Установка зависимостей приложения</span><span class="sxs-lookup"><span data-stu-id="e21ee-122">Install application dependencies</span></span>
<span data-ttu-id="e21ee-123">Установка библиотеки hello и другие модули, необходимые для образца приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e21ee-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="e21ee-124">Настройка подключения устройства hello</span><span class="sxs-lookup"><span data-stu-id="e21ee-124">Configure hello device connection</span></span>
<span data-ttu-id="e21ee-125">tooconfigure Здравствуйте подключения устройства, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e21ee-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="e21ee-126">Создайте файл конфигурации устройства hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e21ee-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="e21ee-127">файл конфигурации Hello `config-edison.json` содержит учетные данные пользователя hello использовать toolog в tooEdison.</span><span class="sxs-lookup"><span data-stu-id="e21ee-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="e21ee-128">tooavoid hello утечки учетных данных пользователя, создается файл конфигурации hello hello во вложенной папке `.iot-hub-getting-started` hello домашней папки на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e21ee-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="e21ee-129">Откройте файл конфигурации устройства hello в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e21ee-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="e21ee-130">Замените заполнитель hello `[device hostname or IP address]` и `[device password]` hello IP-адрес и пароль, который помечен на предыдущем занятии.</span><span class="sxs-lookup"><span data-stu-id="e21ee-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="e21ee-132">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="e21ee-132">Congratulations!</span></span> <span data-ttu-id="e21ee-133">Первый пример приложения hello для Edison успешно создана.</span><span class="sxs-lookup"><span data-stu-id="e21ee-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="e21ee-134">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="e21ee-134">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="e21ee-135">Установите пакет SDK Azure IoT Hub hello на Edison</span><span class="sxs-lookup"><span data-stu-id="e21ee-135">Install hello Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="e21ee-136">Установка hello Azure IoT Hub SDK на Edison при помощи hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e21ee-136">Install hello Azure IoT Hub SDK on Edison by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="e21ee-137">Эта задача может занять длительное время toocomplete, в зависимости от сетевого подключения.</span><span class="sxs-lookup"><span data-stu-id="e21ee-137">This task might take a long time toocomplete, depending on your network connection.</span></span> <span data-ttu-id="e21ee-138">Он нуждается toobe запустить только один раз для одного Edison.</span><span class="sxs-lookup"><span data-stu-id="e21ee-138">It needs toobe run only once for one Edison.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="e21ee-139">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="e21ee-139">Deploy and run hello sample app</span></span>
<span data-ttu-id="e21ee-140">Развертывание и запуск образца приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e21ee-140">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="e21ee-141">Проверки работы приложения hello</span><span class="sxs-lookup"><span data-stu-id="e21ee-141">Verify hello app works</span></span>
<span data-ttu-id="e21ee-142">Пример приложения Hello автоматически завершается после hello Индикатор мигает в течение 20 раз.</span><span class="sxs-lookup"><span data-stu-id="e21ee-142">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="e21ee-143">Если вы не видите hello Индикатор мигает, см. раздел hello [руководство по устранению неполадок] [ troubleshooting] для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="e21ee-143">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![Светодиодный индикатор мигает][led-blinking]

## <a name="summary"></a><span data-ttu-id="e21ee-145">Сводка</span><span class="sxs-lookup"><span data-stu-id="e21ee-145">Summary</span></span>
<span data-ttu-id="e21ee-146">Вы установили hello необходимые средства toowork с Edison и развернуть образец приложения tooEdison tooblink hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="e21ee-146">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="e21ee-147">Вы теперь можно создать, развернуть и выполнения другой пример приложения, которое подключается Edison tooAzure toosend центр IoT и получать сообщения.</span><span class="sxs-lookup"><span data-stu-id="e21ee-147">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e21ee-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e21ee-148">Next steps</span></span>
<span data-ttu-id="e21ee-149">[Получить инструменты Azure hello][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="e21ee-149">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
