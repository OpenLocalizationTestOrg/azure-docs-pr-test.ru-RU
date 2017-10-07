---
featureFlags: usabilla
title: "Подключение Raspberry Pi (узел) tooAzure IoT — занятия 1: развертывание приложения | Документы Microsoft"
description: "Клонирование приложений Node.js образец hello из GitHub и gulp toodeploy tooyour Raspberry Pi 3 этого приложения плата. В этом образце приложения мигает hello Индикатор подключен toohello плата каждые две секунды."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "мигание светодиодного индикатора raspberry pi, включение индикатора с помощью raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9732df3009b8342d4872fe2318a975a6251e772b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="95d6a-105">Создание и развертывание приложения hello мерцания</span><span class="sxs-lookup"><span data-stu-id="95d6a-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="95d6a-106">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="95d6a-106">What you will do</span></span>
<span data-ttu-id="95d6a-107">Клонировать hello образец приложения Node.js из GitHub и использовать hello gulp средство toodeploy hello образец приложения tooyour Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="95d6a-107">Clone hello sample Node.js application from GitHub and use hello gulp tool toodeploy hello sample application tooyour Raspberry Pi 3.</span></span> <span data-ttu-id="95d6a-108">Пример приложения Hello мигает hello Индикатор подключен toohello плата каждые две секунды.</span><span class="sxs-lookup"><span data-stu-id="95d6a-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="95d6a-109">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="95d6a-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="95d6a-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="95d6a-110">What you will learn</span></span>
<span data-ttu-id="95d6a-111">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="95d6a-111">In this article, you will learn:</span></span>

* <span data-ttu-id="95d6a-112">Как toouse hello `device-discover-cli` tooretrieve средство сети сведения о Pi.</span><span class="sxs-lookup"><span data-stu-id="95d6a-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="95d6a-113">Как toodeploy и выполнения hello образец приложения на Pi.</span><span class="sxs-lookup"><span data-stu-id="95d6a-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="95d6a-114">Как toodeploy и отладки приложения, выполняющегося удаленно на Pi.</span><span class="sxs-lookup"><span data-stu-id="95d6a-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="95d6a-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="95d6a-115">What you need</span></span>
<span data-ttu-id="95d6a-116">Необходимо успешно выполнить hello следующие операции:</span><span class="sxs-lookup"><span data-stu-id="95d6a-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="95d6a-117">Настройка устройства</span><span class="sxs-lookup"><span data-stu-id="95d6a-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="95d6a-118">Получить средства hello</span><span class="sxs-lookup"><span data-stu-id="95d6a-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="95d6a-119">Получить hello IP адрес и имя узла Pi</span><span class="sxs-lookup"><span data-stu-id="95d6a-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="95d6a-120">В Windows или терминала в macOS или Ubuntu откройте командную строку и затем выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="95d6a-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="95d6a-121">Вы увидите выходные данные, аналогичные toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="95d6a-121">You should see an output that is similar toohello following:</span></span>

![Обнаружение устройства](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="95d6a-123">Запишите hello `IP address` и `hostname` числа пи.</span><span class="sxs-lookup"><span data-stu-id="95d6a-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="95d6a-124">Эти сведения потребуются позже в данной статье.</span><span class="sxs-lookup"><span data-stu-id="95d6a-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="95d6a-125">Убедитесь, что Pi подключенных toohello сетевых как на компьютере.</span><span class="sxs-lookup"><span data-stu-id="95d6a-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="95d6a-126">Например, если компьютер находится подключенных tooa беспроводной сети при подключенном tooa проводной сети Pi, могут отображаться не hello IP адрес в выходных данных devdisco hello.</span><span class="sxs-lookup"><span data-stu-id="95d6a-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="95d6a-127">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="95d6a-127">Clone hello sample application</span></span>
<span data-ttu-id="95d6a-128">Привет tooopen пример кода, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="95d6a-128">tooopen hello sample code, follow these steps:</span></span>

1. <span data-ttu-id="95d6a-129">Клонирование репозитория образец hello из GitHub, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="95d6a-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="95d6a-130">Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="95d6a-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Структура репозитория](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="95d6a-132">Hello `app.js` файла в hello `app` подпапка является hello ключа исходного файла, содержащего hello toocontrol кода hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="95d6a-132">hello `app.js` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="95d6a-133">Установка зависимостей приложения</span><span class="sxs-lookup"><span data-stu-id="95d6a-133">Install application dependencies</span></span>
<span data-ttu-id="95d6a-134">Установка библиотеки hello и другие модули, необходимые для образца приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="95d6a-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="95d6a-135">Настройка подключения устройства hello</span><span class="sxs-lookup"><span data-stu-id="95d6a-135">Configure hello device connection</span></span>
<span data-ttu-id="95d6a-136">tooconfigure Здравствуйте подключения устройства, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="95d6a-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="95d6a-137">Создайте файл конфигурации устройства hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="95d6a-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="95d6a-138">файл конфигурации Hello `config-raspberrypi.json` содержит учетные данные пользователя hello использовать toolog в tooPi.</span><span class="sxs-lookup"><span data-stu-id="95d6a-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="95d6a-139">tooavoid hello утечки учетных данных пользователя, создается файл конфигурации hello hello во вложенной папке `.iot-hub-getting-started` hello домашней папки на компьютере.</span><span class="sxs-lookup"><span data-stu-id="95d6a-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="95d6a-140">Откройте файл конфигурации устройства hello в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="95d6a-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="95d6a-141">Замените заполнитель hello `[device hostname or IP address]` с hello IP-адрес или имя узла hello, полученный ранее на «Получение hello IP адрес и имя узла пи.»</span><span class="sxs-lookup"><span data-stu-id="95d6a-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="95d6a-143">SSH-ключ можно использовать вместо имени пользователя и пароль при подключении tooRaspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="95d6a-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="95d6a-144">Чтобы toodo это будет иметь toogenerate hello ключ при помощи **ssh-keygen** и **pi ssh-copy-id @\<адрес устройства\>**.</span><span class="sxs-lookup"><span data-stu-id="95d6a-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="95d6a-145">В Windows эти команды доступны следующие в **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="95d6a-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="95d6a-146">На MacOS необходимо toorun **brew установить ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="95d6a-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="95d6a-147">После успешной отправки hello ключа toohello Raspberry Pi, замените **device_password** с **device_key_path** свойство в **raspberrypi.json конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="95d6a-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="95d6a-148">Обновленные строки должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="95d6a-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="95d6a-149">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="95d6a-149">Congratulations!</span></span> <span data-ttu-id="95d6a-150">Первый пример приложения hello для Pi успешно создана.</span><span class="sxs-lookup"><span data-stu-id="95d6a-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="95d6a-151">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="95d6a-151">Deploy and run hello sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="95d6a-152">Установка Node.js и NPM на устройстве Pi</span><span class="sxs-lookup"><span data-stu-id="95d6a-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="95d6a-153">Установите Node.js и NPM на Pi, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="95d6a-153">Install Node.js and NPM on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="95d6a-154">Эта задача может занять 10 минут toocomplete hello первый раз при запуске.</span><span class="sxs-lookup"><span data-stu-id="95d6a-154">This task might take 10 minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="95d6a-155">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="95d6a-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="95d6a-156">Развертывание и запуск образца приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="95d6a-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="95d6a-157">Проверки работы приложения hello</span><span class="sxs-lookup"><span data-stu-id="95d6a-157">Verify hello app works</span></span>
<span data-ttu-id="95d6a-158">Теперь вы увидите hello Светодиод на Pi мигает каждые две секунды.</span><span class="sxs-lookup"><span data-stu-id="95d6a-158">You should now see hello LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="95d6a-159">Если вы не видите hello Индикатор мигает, см. раздел hello [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md) для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="95d6a-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="95d6a-160">![Индикатор мигает](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="95d6a-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="95d6a-161">Сводка</span><span class="sxs-lookup"><span data-stu-id="95d6a-161">Summary</span></span>
<span data-ttu-id="95d6a-162">Вы установили hello необходимые средства toowork с Pi и развернуть образец приложения tooPi tooblink hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="95d6a-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="95d6a-163">Вы теперь можно создать, развернуть и выполнения другой пример приложения, которое подключается Pi tooAzure toosend центр IoT и получать сообщения.</span><span class="sxs-lookup"><span data-stu-id="95d6a-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95d6a-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="95d6a-164">Next steps</span></span>
[<span data-ttu-id="95d6a-165">Получить инструменты Azure hello</span><span class="sxs-lookup"><span data-stu-id="95d6a-165">Get hello Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

