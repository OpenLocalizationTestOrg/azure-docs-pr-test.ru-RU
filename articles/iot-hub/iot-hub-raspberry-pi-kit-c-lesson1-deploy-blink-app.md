---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Урок 1. Развертывание приложения | Документация Майкрософт"
description: "Клонируйте пример приложения C из Github и разверните его с помощью инструмента Gulp на устройстве Raspberry Pi 3. Это приложение будет каждые две секунды включать и выключать светодиодный индикатор на компьютере."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "мигание светодиодного индикатора raspberry pi, включение индикатора с помощью raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2ae409c6a39521711777ec329d2507a2801cc985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="1bf7f-105">Создание и развертывание приложения для включения индикатора</span><span class="sxs-lookup"><span data-stu-id="1bf7f-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1bf7f-106">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="1bf7f-106">What you will do</span></span>
<span data-ttu-id="1bf7f-107">Клонирование примера приложения C из GitHub и его развертывание с помощью инструмента Gulp на устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Raspberry Pi 3.</span></span> <span data-ttu-id="1bf7f-108">Этот пример приложения будет каждые две секунды включать светодиодный индикатор, подключенный к плате.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="1bf7f-109">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1bf7f-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1bf7f-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="1bf7f-110">What you will learn</span></span>
<span data-ttu-id="1bf7f-111">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="1bf7f-111">In this article, you will learn:</span></span>

* <span data-ttu-id="1bf7f-112">Как использовать средство `device-discover-cli` для получения сетевых сведений о плате Pi.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="1bf7f-113">Как развертывать и запускать пример приложения на плате Pi.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="1bf7f-114">Как развертывать и отлаживать приложения, работающие удаленно на плате Pi.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1bf7f-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="1bf7f-115">What you need</span></span>
<span data-ttu-id="1bf7f-116">Необходимо успешно выполнить следующие операции:</span><span class="sxs-lookup"><span data-stu-id="1bf7f-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="1bf7f-117">Настройка устройства</span><span class="sxs-lookup"><span data-stu-id="1bf7f-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="1bf7f-118">Получение инструментов</span><span class="sxs-lookup"><span data-stu-id="1bf7f-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="1bf7f-119">Получение IP-адреса и имени узла для платы Pi</span><span class="sxs-lookup"><span data-stu-id="1bf7f-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="1bf7f-120">В командной строке Windows или в окне терминала на устройстве под управлением macOS или Ubuntu выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="1bf7f-121">Должен отобразиться результат, аналогичный приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="1bf7f-121">You should see an output that is similar to the following:</span></span>

![Обнаружение устройства](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="1bf7f-123">Запишите значения `IP address` и `hostname` для платы Pi.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="1bf7f-124">Эти сведения потребуются позже в данной статье.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf7f-125">Убедитесь, что плата Pi подключена к той же сети, что и компьютер.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="1bf7f-126">Например, если компьютер подключен к беспроводной сети, а плата Pi подключена к проводной сети, то IP-адрес может не отобразиться в выходных данных devdisco.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="1bf7f-127">Открытие примера приложения</span><span class="sxs-lookup"><span data-stu-id="1bf7f-127">Open the sample application</span></span>
<span data-ttu-id="1bf7f-128">Чтобы открыть пример приложения, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1bf7f-128">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="1bf7f-129">Клонируйте пример репозитория из GitHub, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="1bf7f-130">Откройте пример приложения в Visual Studio Code, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="1bf7f-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Структура репозитория](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="1bf7f-132">Файл `main.c` в подпапке `app` — это ключевой исходный файл, содержащий код для управления светодиодным индикатором.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-132">The `main.c` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="1bf7f-133">Установка зависимостей приложения</span><span class="sxs-lookup"><span data-stu-id="1bf7f-133">Install application dependencies</span></span>
<span data-ttu-id="1bf7f-134">Установите библиотеки и другие модули, необходимые для примера приложения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1bf7f-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="1bf7f-135">Настройка подключения устройства</span><span class="sxs-lookup"><span data-stu-id="1bf7f-135">Configure the device connection</span></span>
<span data-ttu-id="1bf7f-136">Чтобы настроить подключение устройства, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="1bf7f-137">Создайте файл конфигурации устройства, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="1bf7f-138">Файл конфигурации `config-raspberrypi.json` содержит учетные данные пользователя для входа в Pi.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="1bf7f-139">Чтобы избежать утечки учетных данных пользователя, файл конфигурации создается в подпапке `.iot-hub-getting-started` домашней папки на компьютере.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="1bf7f-140">Откройте файл конфигурации устройства в Visual Studio Code, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="1bf7f-141">Замените заполнитель `[device hostname or IP address]` IP-адресом или именем узла, которые вы записали ранее в разделе "Получение IP-адреса и имени узла для платы Pi".</span><span class="sxs-lookup"><span data-stu-id="1bf7f-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="1bf7f-143">При подключении к устройству Raspberry Pi вместо имени пользователя и пароля можно использовать ключ SSH.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="1bf7f-144">Чтобы сделать это необходимо для создания ключа с помощью **ssh-keygen** и **pi ssh-copy-id @\<адрес устройства\>**.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="1bf7f-145">В Windows эти команды доступны следующие в **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="1bf7f-146">В MacOS необходимо выполнить команду **brew install ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="1bf7f-147">После успешной отправки ключа на устройство Raspberry Pi замените **device_password** свойством **device_key_path** в файле **config-raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="1bf7f-148">Обновленные строки должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1bf7f-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="1bf7f-149">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="1bf7f-149">Congratulations!</span></span> <span data-ttu-id="1bf7f-150">Вы успешно создали первый пример приложения для платы Pi.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="1bf7f-151">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="1bf7f-151">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="1bf7f-152">Установка пакета SDK для Центра Интернета вещей на устройстве Pi</span><span class="sxs-lookup"><span data-stu-id="1bf7f-152">Install the Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="1bf7f-153">Установите пакет SDK для Центра Интернета вещей на устройстве Pi, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1bf7f-153">Install the Azure IoT Hub SDK on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="1bf7f-154">При первом выполнении этой задачи на ее завершение может уйти несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-154">This task might take a few minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="1bf7f-155">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="1bf7f-155">Deploy and run the sample app</span></span>
<span data-ttu-id="1bf7f-156">Разверните и запустите пример приложения, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="1bf7f-157">Проверка работы приложения</span><span class="sxs-lookup"><span data-stu-id="1bf7f-157">Verify the app works</span></span>
<span data-ttu-id="1bf7f-158">После того, как светодиодный индикатор мигнет 20 раз, пример приложения завершит работу автоматически.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-158">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="1bf7f-159">Если индикатор не мигает, см. способы решения распространенных проблем в [руководстве по устранению неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1bf7f-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="1bf7f-160">![Индикатор мигает](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="1bf7f-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="1bf7f-161">Сводка</span><span class="sxs-lookup"><span data-stu-id="1bf7f-161">Summary</span></span>
<span data-ttu-id="1bf7f-162">Вы установили необходимые средства для работы с платой Pi и развернули пример приложения, заставляющего светодиодный индикатор мигать.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="1bf7f-163">Теперь можно приступать к созданию, развертыванию и запуску другого примера приложения, которое подключает плату Pi к Центру Интернета вещей Azure для отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="1bf7f-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bf7f-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1bf7f-164">Next steps</span></span>
<span data-ttu-id="1bf7f-165">[Get Azure tools](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md) (Получение инструментов Azure)</span><span class="sxs-lookup"><span data-stu-id="1bf7f-165">[Get Azure tools](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)</span></span>

