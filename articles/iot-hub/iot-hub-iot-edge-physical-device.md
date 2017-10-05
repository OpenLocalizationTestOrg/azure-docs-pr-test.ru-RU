---
title: "Использование физического устройства с Edge Интернета вещей Azure | Документация Майкрософт"
description: "Сведения об использовании устройства Texas Instruments SensorTag для отправки данных в Центр Интернета вещей через шлюз Edge Интернета вещей, работающий на устройстве Raspberry Pi 3. Шлюз создается с использованием Edge Интернета вещей Azure."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: 02962a91c739a53dfcf947bcc736e5c293b9384f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-to-forward-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="b1bda-104">Использование Azure IoT Edge в Raspberry Pi для переадресации отправки сообщений с устройства в облако в Центр Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="b1bda-104">Use Azure IoT Edge on a Raspberry Pi to forward device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="b1bda-105">В этом пошаговом руководстве по созданию [примера устройства Bluetooth с низким энергопотреблением][lnk-ble-samplecode] показано, как использовать [Edge Интернета вещей Azure][lnk-sdk], чтобы:</span><span class="sxs-lookup"><span data-stu-id="b1bda-105">This walkthrough of the [Bluetooth low energy sample][lnk-ble-samplecode] shows you how to use [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="b1bda-106">пересылать в Центр Интернета вещей данные телеметрии, передаваемые с устройства в облако;</span><span class="sxs-lookup"><span data-stu-id="b1bda-106">Forward device-to-cloud telemetry to IoT Hub from a physical device.</span></span>
* <span data-ttu-id="b1bda-107">маршрутизировать команды из Центра Интернета вещей на физическое устройство.</span><span class="sxs-lookup"><span data-stu-id="b1bda-107">Route commands from IoT Hub to a physical device.</span></span>

<span data-ttu-id="b1bda-108">В этом руководстве рассматриваются следующие темы.</span><span class="sxs-lookup"><span data-stu-id="b1bda-108">This walkthrough covers:</span></span>

* <span data-ttu-id="b1bda-109">**Архитектура**: важные данные об архитектуре в примере устройства Bluetooth с низким энергопотреблением.</span><span class="sxs-lookup"><span data-stu-id="b1bda-109">**Architecture**: important architectural information about the Bluetooth low energy sample.</span></span>
* <span data-ttu-id="b1bda-110">**Сборка и запуск**: шаги, необходимые для сборки и запуска примера.</span><span class="sxs-lookup"><span data-stu-id="b1bda-110">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="b1bda-111">Архитектура</span><span class="sxs-lookup"><span data-stu-id="b1bda-111">Architecture</span></span>

<span data-ttu-id="b1bda-112">В пошаговом руководстве показано, как выполнять сборку и запускать шлюз Edge Интернета вещей на плате Raspberry Pi 3, работающей под управлением ОС Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="b1bda-112">The walkthrough shows you how to build and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="b1bda-113">Шлюз создается с использованием Edge Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b1bda-113">The gateway is built using IoT Edge.</span></span> <span data-ttu-id="b1bda-114">Для сбора данных температуры в этом примере используется устройство Bluetooth с низким энергопотреблением (BLE) Texas Instruments SensorTag.</span><span class="sxs-lookup"><span data-stu-id="b1bda-114">The sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device to collect temperature data.</span></span>

<span data-ttu-id="b1bda-115">При запуске шлюз Edge Интернета вещей выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b1bda-115">When you run the IoT Edge gateway it:</span></span>

* <span data-ttu-id="b1bda-116">Подключается к устройству SensorTag с помощью протокола низкого энергопотребления Bluetooth (BLE).</span><span class="sxs-lookup"><span data-stu-id="b1bda-116">Connects to a SensorTag device using the Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="b1bda-117">Подключается к Центру Интернета вещей с помощью протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1bda-117">Connects to IoT Hub using the HTTP protocol.</span></span>
* <span data-ttu-id="b1bda-118">Пересылает данные телеметрии с устройства SensorTag в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="b1bda-118">Forwards telemetry from the SensorTag device to IoT Hub.</span></span>
* <span data-ttu-id="b1bda-119">Маршрутизирует команды из центра IoT на устройство SensorTag.</span><span class="sxs-lookup"><span data-stu-id="b1bda-119">Routes commands from IoT Hub to the SensorTag device.</span></span>

<span data-ttu-id="b1bda-120">Шлюз содержит следующие модули Edge Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="b1bda-120">The gateway contains the following IoT Edge modules:</span></span>

* <span data-ttu-id="b1bda-121">*Модуль BLE* , который взаимодействует с устройством BLE для получения от него данных температуры и отправки на него команд.</span><span class="sxs-lookup"><span data-stu-id="b1bda-121">A *BLE module* that interfaces with a BLE device to receive temperature data from the device and send commands to the device.</span></span>
* <span data-ttu-id="b1bda-122">*Модуль BLE "Из облака на устройство"*, который преобразовывает сообщения JSON, поступающие из Центра Интернета вещей, в инструкции BLE для *модуля BLE*.</span><span class="sxs-lookup"><span data-stu-id="b1bda-122">A *BLE cloud to device module* that translates JSON messages sent from IoT Hub into BLE instructions for the *BLE module*.</span></span>
* <span data-ttu-id="b1bda-123">*Модуль ведения журнала*, который регистрирует в локальном файле все сообщения шлюза.</span><span class="sxs-lookup"><span data-stu-id="b1bda-123">A *logger module* that logs all gateway messages to a local file.</span></span>
* <span data-ttu-id="b1bda-124">*Модуль сопоставления удостоверений* , который преобразовывает MAC-адреса устройств BLE и удостоверения устройств центра Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="b1bda-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="b1bda-125">*Модуль Центра Интернета вещей* , который передает в Центр Интернета вещей данные телеметрии и получает из него команды устройств.</span><span class="sxs-lookup"><span data-stu-id="b1bda-125">An *IoT Hub module* that uploads telemetry data to an IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="b1bda-126">*Модуль принтера BLE* интерпретирует данные телеметрии из устройства BLE и печатает форматированные данные в консоль, чтобы включить устранение неполадок и отладку.</span><span class="sxs-lookup"><span data-stu-id="b1bda-126">A *BLE printer module* that interprets telemetry from the BLE device and prints formatted data to the console to enable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-the-gateway"></a><span data-ttu-id="b1bda-127">Прохождение потока данных через шлюз</span><span class="sxs-lookup"><span data-stu-id="b1bda-127">How data flows through the gateway</span></span>

<span data-ttu-id="b1bda-128">На следующей блок-схеме показано, как работает конвейер отправки данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b1bda-128">The following block diagram illustrates the telemetry upload data flow pipeline:</span></span>

![Конвейер шлюза отправки данных телеметрии](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="b1bda-130">Элемент телеметрии на пути из устройства BLE в Центр Интернета вещей выполняет следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="b1bda-130">The steps that an item of telemetry takes traveling from a BLE device to IoT Hub are:</span></span>

1. <span data-ttu-id="b1bda-131">Устройство BLE создает пример данных температуры и отправляет его через Bluetooth на модуль BLE в шлюзе.</span><span class="sxs-lookup"><span data-stu-id="b1bda-131">The BLE device generates a temperature sample and sends it over Bluetooth to the BLE module in the gateway.</span></span>
1. <span data-ttu-id="b1bda-132">Модуль BLE получает этот пример и публикует его в брокер вместе с MAC-адресом устройства.</span><span class="sxs-lookup"><span data-stu-id="b1bda-132">The BLE module receives the sample and publishes it to the broker along with the MAC address of the device.</span></span>
1. <span data-ttu-id="b1bda-133">Модуль сопоставления удостоверений извлекает это сообщение и использует внутреннюю таблицу для преобразования MAC-адреса устройства в удостоверение устройства Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b1bda-133">The identity mapping module picks up this message and uses an internal table to translate the MAC address of the device into an IoT Hub device identity.</span></span> <span data-ttu-id="b1bda-134">Удостоверение устройства Центра Интернета вещей состоит из идентификатора и ключа устройства.</span><span class="sxs-lookup"><span data-stu-id="b1bda-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="b1bda-135">Модуль сопоставления удостоверений публикует новое сообщение, содержащее пример данных температуры, MAC-адрес, идентификатор и ключ устройства.</span><span class="sxs-lookup"><span data-stu-id="b1bda-135">The identity mapping module publishes a new message that contains the temperature sample data, the MAC address of the device, the device ID, and the device key.</span></span>
1. <span data-ttu-id="b1bda-136">Модуль Центра Интернета вещей получает это новое сообщение (созданное модулем сопоставления удостоверений) и публикует его в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b1bda-136">The IoT Hub module receives this new message (generated by the identity mapping module) and publishes it to IoT Hub.</span></span>
1. <span data-ttu-id="b1bda-137">Модуль ведения журнала регистрирует в локальном файле все сообщения из брокера.</span><span class="sxs-lookup"><span data-stu-id="b1bda-137">The logger module logs all messages from the broker to a local file.</span></span>

<span data-ttu-id="b1bda-138">На следующей блок-схеме показано, как работает конвейер обработки данных команд устройств.</span><span class="sxs-lookup"><span data-stu-id="b1bda-138">The following block diagram illustrates the device command data flow pipeline:</span></span>

![Конвейер шлюза команд устройства](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="b1bda-140">Модуль Центра Интернета вещей периодически опрашивает Центр Интернета вещей на наличие новых командных сообщений.</span><span class="sxs-lookup"><span data-stu-id="b1bda-140">The IoT Hub module periodically polls the IoT hub for new command messages.</span></span>
1. <span data-ttu-id="b1bda-141">Когда модуль Центра Интернета вещей получает новое командное сообщение, он публикует его в брокер.</span><span class="sxs-lookup"><span data-stu-id="b1bda-141">When the IoT Hub module receives a new command message, it publishes it to the broker.</span></span>
1. <span data-ttu-id="b1bda-142">Модуль сопоставления удостоверений извлекает это командное сообщение и использует внутреннюю таблицу для преобразования идентификатора устройства Центра Интернета вещей в MAC-адрес устройства.</span><span class="sxs-lookup"><span data-stu-id="b1bda-142">The identity mapping module picks up the command message and uses an internal table to translate the IoT Hub device ID to a device MAC address.</span></span> <span data-ttu-id="b1bda-143">Затем он публикует новое сообщение, содержащее MAC-адрес целевого устройства в схеме сопоставления свойств сообщения.</span><span class="sxs-lookup"><span data-stu-id="b1bda-143">It then publishes a new message that includes the MAC address of the target device in the properties map of the message.</span></span>
1. <span data-ttu-id="b1bda-144">Модуль BLE "Из облака на устройство" извлекает это сообщение и преобразовывает его в правильную инструкцию BLE для модуля BLE.</span><span class="sxs-lookup"><span data-stu-id="b1bda-144">The BLE Cloud-to-Device module picks up this message and translates it into the proper BLE instruction for the BLE module.</span></span> <span data-ttu-id="b1bda-145">Затем он публикует новое сообщение.</span><span class="sxs-lookup"><span data-stu-id="b1bda-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="b1bda-146">Модуль BLE извлекает это сообщение и выполняет инструкцию ввода-вывода, взаимодействуя с устройством BLE.</span><span class="sxs-lookup"><span data-stu-id="b1bda-146">The BLE module picks up this message and executes the I/O instruction by communicating with the BLE device.</span></span>
1. <span data-ttu-id="b1bda-147">Модуль ведения журнала регистрирует в журнале все сообщения из брокера в файл на диске.</span><span class="sxs-lookup"><span data-stu-id="b1bda-147">The logger module logs all messages from the broker to a disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1bda-148">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b1bda-148">Prerequisites</span></span>

<span data-ttu-id="b1bda-149">Для работы с этим руководством требуется активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="b1bda-149">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b1bda-150">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b1bda-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b1bda-151">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="b1bda-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="b1bda-152">На настольном компьютере необходимо установить клиент SSH, чтобы иметь удаленный доступ к командной строке Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b1bda-152">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="b1bda-153">Windows не предоставляет клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="b1bda-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="b1bda-154">Мы советуем использовать [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="b1bda-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="b1bda-155">Большинство дистрибутивов Linux и Mac OS содержат служебную программу командной строки SSH.</span><span class="sxs-lookup"><span data-stu-id="b1bda-155">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="b1bda-156">Дополнительные сведения см. в статье [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (Подключение по протоколу SSH с помощью Linux или Mac OS).</span><span class="sxs-lookup"><span data-stu-id="b1bda-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="b1bda-157">Подготовка оборудования</span><span class="sxs-lookup"><span data-stu-id="b1bda-157">Prepare your hardware</span></span>

<span data-ttu-id="b1bda-158">В этом учебнике предполагается, что вы используете устройство [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html), подключенное к плате Raspberry Pi 3 под управлением ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="b1bda-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected to a Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="b1bda-159">Установка Raspbian</span><span class="sxs-lookup"><span data-stu-id="b1bda-159">Install Raspbian</span></span>

<span data-ttu-id="b1bda-160">Воспользуйтесь одним из приведенных ниже вариантов установки Raspbian на устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="b1bda-160">You can use either of the following options to install Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="b1bda-161">Чтобы установить последнюю версию Raspbian, воспользуйтесь графическим пользовательским интерфейсом [NOOBS][lnk-noobs].</span><span class="sxs-lookup"><span data-stu-id="b1bda-161">To install the latest version of Raspbian, use the [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="b1bda-162">[Скачайте][lnk-raspbian] вручную и запишите новейший образ операционной системы Raspbian на SD-карту.</span><span class="sxs-lookup"><span data-stu-id="b1bda-162">Manually [download][lnk-raspbian] and write the latest image of the Raspbian operating system to an SD card.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="b1bda-163">Вход и доступ к терминалу</span><span class="sxs-lookup"><span data-stu-id="b1bda-163">Sign in and access the terminal</span></span>

<span data-ttu-id="b1bda-164">Существует два варианта получения доступа к среде терминала на Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b1bda-164">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="b1bda-165">Если клавиатура и монитор подключены к Raspberry Pi, вы можете использовать графический пользовательский интерфейс Raspbian, чтобы получить доступ к окну терминала.</span><span class="sxs-lookup"><span data-stu-id="b1bda-165">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

* <span data-ttu-id="b1bda-166">Получите доступ к командной строке на устройстве Raspberry Pi с настольного компьютера, используя SSH.</span><span class="sxs-lookup"><span data-stu-id="b1bda-166">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="b1bda-167">Использование окна терминала в графическом пользовательском интерфейсе</span><span class="sxs-lookup"><span data-stu-id="b1bda-167">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="b1bda-168">По умолчанию в качестве учетных данных для Raspbian используется имя пользователя **pi** и пароль **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-168">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="b1bda-169">На панели задач в графическом пользовательском интерфейсе можно запустить служебную программу **Terminal** с помощью значка в виде монитора.</span><span class="sxs-lookup"><span data-stu-id="b1bda-169">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="b1bda-170">Вход с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="b1bda-170">Sign in with SSH</span></span>

<span data-ttu-id="b1bda-171">Используйте SSH, чтобы получить доступ к Raspberry Pi с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="b1bda-171">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="b1bda-172">Сведения о настройке SSH на устройстве Raspberry Pi и о подключении из [Windows][lnk-ssh-windows], [Linux и Mac OS][lnk-ssh-linux] см. в руководстве по [SSH (SECURE SHELL)][lnk-pi-ssh].</span><span class="sxs-lookup"><span data-stu-id="b1bda-172">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="b1bda-173">Войдите, используя имя пользователя **pi** и пароль **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="b1bda-174">Установка BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="b1bda-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="b1bda-175">Модули BLE взаимодействуют с оборудованием Bluetooth через стек BlueZ.</span><span class="sxs-lookup"><span data-stu-id="b1bda-175">The BLE modules talk to the Bluetooth hardware via the BlueZ stack.</span></span> <span data-ttu-id="b1bda-176">Чтобы модули работали корректно, необходимо установить BlueZ версии 5.37.</span><span class="sxs-lookup"><span data-stu-id="b1bda-176">You need version 5.37 of BlueZ for the modules to work correctly.</span></span> <span data-ttu-id="b1bda-177">Эти инструкции помогут вам установить правильную версию BlueZ.</span><span class="sxs-lookup"><span data-stu-id="b1bda-177">These instructions make sure the correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="b1bda-178">Остановите работу текущей управляющей программы Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="b1bda-178">Stop the current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="b1bda-179">Установите зависимости BlueZ:</span><span class="sxs-lookup"><span data-stu-id="b1bda-179">Install the BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="b1bda-180">Скачайте исходный код BlueZ с сайта bluez.org:</span><span class="sxs-lookup"><span data-stu-id="b1bda-180">Download the BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="b1bda-181">Распакуйте исходный код:</span><span class="sxs-lookup"><span data-stu-id="b1bda-181">Unzip the source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="b1bda-182">Смените каталоги на вновь созданную папку:</span><span class="sxs-lookup"><span data-stu-id="b1bda-182">Change directories to the newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="b1bda-183">Настройте код BlueZ для выполнения сборки:</span><span class="sxs-lookup"><span data-stu-id="b1bda-183">Configure the BlueZ code to be built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="b1bda-184">Выполните сборку BlueZ:</span><span class="sxs-lookup"><span data-stu-id="b1bda-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="b1bda-185">По завершении сборки установите BlueZ:</span><span class="sxs-lookup"><span data-stu-id="b1bda-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="b1bda-186">В файле `/lib/systemd/system/bluetooth.service` измените конфигурацию службы systemd для Bluetooth, чтобы она указывала на новую управляющую программу Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="b1bda-186">Change systemd service configuration for bluetooth so it points to the new bluetooth daemon in the file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="b1bda-187">Замените строку ExecStart следующим текстом:</span><span class="sxs-lookup"><span data-stu-id="b1bda-187">Replace the 'ExecStart' line with the following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-to-the-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="b1bda-188">Подключение устройства Raspberry Pi 3 к устройству SensorTag</span><span class="sxs-lookup"><span data-stu-id="b1bda-188">Enable connectivity to the SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="b1bda-189">Перед запуском примера необходимо убедиться, что плата Raspberry Pi 3 имеет возможность подключаться к устройству SensorTag.</span><span class="sxs-lookup"><span data-stu-id="b1bda-189">Before running the sample, you need to verify that your Raspberry Pi 3 can connect to the SensorTag device.</span></span>

1. <span data-ttu-id="b1bda-190">Убедитесь, что служебная программа `rfkill` установлена:</span><span class="sxs-lookup"><span data-stu-id="b1bda-190">Ensure the `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="b1bda-191">Разблокируйте Bluetooth на устройстве Raspberry Pi 3 и убедитесь, что номер версии — **5.37**:</span><span class="sxs-lookup"><span data-stu-id="b1bda-191">Unblock bluetooth on the Raspberry Pi 3 and check that the version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="b1bda-192">Чтобы войти в интерактивную оболочку Bluetooth, запустите службу Bluetooth и выполните команду **bluetoothctl**:</span><span class="sxs-lookup"><span data-stu-id="b1bda-192">To enter the interactive bluetooth shell, start the bluetooth service and execute the **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="b1bda-193">Введите команду **power on** , чтобы включить питание контроллера Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="b1bda-193">Enter the command **power on** to power up the bluetooth controller.</span></span> <span data-ttu-id="b1bda-194">Команда вернет результат следующего вида:</span><span class="sxs-lookup"><span data-stu-id="b1bda-194">The command returns output similar to the following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="b1bda-195">В интерактивной оболочке Bluetooth введите команду **scan on** для поиска устройств Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="b1bda-195">In the interactive bluetooth shell, enter the command **scan on** to scan for bluetooth devices.</span></span> <span data-ttu-id="b1bda-196">Команда вернет результат следующего вида:</span><span class="sxs-lookup"><span data-stu-id="b1bda-196">The command returns output similar to the following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="b1bda-197">Сделайте устройство SensorTag доступным для обнаружения, нажав маленькую кнопку (должен загореться зеленый светодиодный индикатор).</span><span class="sxs-lookup"><span data-stu-id="b1bda-197">Make the SensorTag device discoverable by pressing the small button (the green LED should flash).</span></span> <span data-ttu-id="b1bda-198">Плата Raspberry Pi 3 должна обнаружить устройство SensorTag:</span><span class="sxs-lookup"><span data-stu-id="b1bda-198">The Raspberry Pi 3 should discover the SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="b1bda-199">В этом примере можно увидеть, что устройство SensorTag имеет MAC-адрес **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-199">In this example, you can see that the MAC address of the SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="b1bda-200">Отключите поиск, введя команду **scan off**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-200">Turn off scanning by entering the **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="b1bda-201">Подключитесь к устройству SensorTag, используя его MAC-адрес. Для этого введите команду **connect \<MAC-адрес\>**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-201">Connect to your SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="b1bda-202">Для большей ясности следующий пример выходных данных приведен в сокращенном виде.</span><span class="sxs-lookup"><span data-stu-id="b1bda-202">The following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting to connect to A0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > <span data-ttu-id="b1bda-203">Список характеристик GATT устройства можно получить повторно, используя команду **list-attributes**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-203">You can list the GATT characteristics of the device again using the **list-attributes** command.</span></span>

1. <span data-ttu-id="b1bda-204">Теперь можно отключиться от устройства с помощью команды **disconnect** и выйти из оболочки Bluetooth с помощью команды **quit**:</span><span class="sxs-lookup"><span data-stu-id="b1bda-204">You can now disconnect from the device using the **disconnect** command and then exit from the bluetooth shell using the **quit** command:</span></span>

    ```sh
    Attempting to disconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="b1bda-205">Теперь все готово для запуска примера Edge Интернета вещей BLE на устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="b1bda-205">You're now ready to run the BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-the-iot-edge-ble-sample"></a><span data-ttu-id="b1bda-206">Запуск примера Edge Интернета вещей BLE</span><span class="sxs-lookup"><span data-stu-id="b1bda-206">Run the IoT Edge BLE sample</span></span>

<span data-ttu-id="b1bda-207">Чтобы запустить пример шлюза Edge Интернета вещей BLE, необходимо выполнить три задачи:</span><span class="sxs-lookup"><span data-stu-id="b1bda-207">To run the IoT Edge BLE sample, you need to complete three tasks:</span></span>

* <span data-ttu-id="b1bda-208">Настроить два примера устройств в центре IoT.</span><span class="sxs-lookup"><span data-stu-id="b1bda-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="b1bda-209">Создать Edge Интернета вещей на устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="b1bda-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="b1bda-210">Настроить и запустить пример BLE на устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="b1bda-210">Configure and run the BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="b1bda-211">Во время записи IoT Edge поддерживает модули BLE только в шлюзах, запущенных на Linux.</span><span class="sxs-lookup"><span data-stu-id="b1bda-211">At the time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="b1bda-212">Настройка двух примеров устройств в центре IoT</span><span class="sxs-lookup"><span data-stu-id="b1bda-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="b1bda-213">[Создайте Центр Интернета вещей][lnk-create-hub] в подписке Azure (для выполнения указаний данного пошагового руководства необходимо имя центра).</span><span class="sxs-lookup"><span data-stu-id="b1bda-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="b1bda-214">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b1bda-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="b1bda-215">Добавьте в Центр Интернета вещей одно устройство с именем **SensorTag_01**, а затем запишите его идентификатор и ключ устройства.</span><span class="sxs-lookup"><span data-stu-id="b1bda-215">Add one device called **SensorTag_01** to your IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="b1bda-216">Чтобы добавить устройство в Центр Интернета вещей, созданный на предыдущем шаге, и получить его ключ, можно использовать такие инструменты, как [обозреватель устройств или iothub-explorer][lnk-explorer-tools].</span><span class="sxs-lookup"><span data-stu-id="b1bda-216">You can use the [device explorer or iothub-explorer][lnk-explorer-tools] tools to add this device to the IoT hub you created in the previous step and to retrieve its key.</span></span> <span data-ttu-id="b1bda-217">Сопоставление этого устройства с устройством SensorTag будет выполнено при настройке шлюза.</span><span class="sxs-lookup"><span data-stu-id="b1bda-217">You map this device to the SensorTag device when you configure the gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="b1bda-218">Создание Edge Интернета вещей Azure на устройстве Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="b1bda-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="b1bda-219">Установите зависимые компоненты Edge Интернета вещей Azure:</span><span class="sxs-lookup"><span data-stu-id="b1bda-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="b1bda-220">Выполните следующие команды, чтобы клонировать Edge Интернета вещей и все его подмодули в корневой каталог:</span><span class="sxs-lookup"><span data-stu-id="b1bda-220">Use the following commands to clone IoT Edge and all its submodules to your home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="b1bda-221">Когда репозиторий Edge Интернета вещей полностью скопирован на устройство Raspberry Pi 3, можно выполнить его сборку, выполнив следующую команду из папки, в которой содержится пакет SDK:</span><span class="sxs-lookup"><span data-stu-id="b1bda-221">When you have a complete copy of the IoT Edge repository on your Raspberry Pi 3, you can build it using the following command from the folder that contains the SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-the-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="b1bda-222">Настройка и запуск примера BLE на устройстве Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="b1bda-222">Configure and run the BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="b1bda-223">Для начальной загрузки и запуска примера необходимо настроить каждый модуль Edge Интернета вещей, который участвует в шлюзе.</span><span class="sxs-lookup"><span data-stu-id="b1bda-223">To bootstrap and run the sample, you must configure each IoT Edge module that participates in the gateway.</span></span> <span data-ttu-id="b1bda-224">Необходимая конфигурация предоставляется в файле JSON. Вам следует настроить все пять участвующих модулей Edge Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b1bda-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="b1bda-225">В репозитории есть пример JSON-файла с именем **gateway\_sample.json**, на основе которого вы можете создать собственный файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b1bda-225">There is a sample JSON file in the repository called **gateway\_sample.json** that you can use as the starting point for building your own configuration file.</span></span> <span data-ttu-id="b1bda-226">Этот файл находится в папке **samples/ble_gateway/src** в локальной копии репозитория Edge Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b1bda-226">This file is in the **samples/ble_gateway/src** folder in local copy of the IoT Edge repository.</span></span>

<span data-ttu-id="b1bda-227">В следующих разделах описывается, как изменить этот файл конфигурации для примера BLE. Кроме того, предполагается, что репозиторий Edge Интернета вещей находится в папке **/home/pi/iot-edge/** на устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="b1bda-227">The following sections describe how to edit this configuration file for the BLE sample and assume that the IoT Edge repository is in the **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="b1bda-228">Если репозиторий находится в другом месте, измените соответствующим образом пути.</span><span class="sxs-lookup"><span data-stu-id="b1bda-228">If the repository is elsewhere, adjust the paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="b1bda-229">Конфигурация средства ведения журнала</span><span class="sxs-lookup"><span data-stu-id="b1bda-229">Logger configuration</span></span>

<span data-ttu-id="b1bda-230">Убедившись, что репозиторий шлюза находится в папке **/home/pi/iot-edge/**, настройте модуль ведения журнала следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b1bda-230">Assuming the gateway repository is located in the **/home/pi/iot-edge/** folder, configure the logger module as follows:</span></span>

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a><span data-ttu-id="b1bda-231">Конфигурация модуля BLE</span><span class="sxs-lookup"><span data-stu-id="b1bda-231">BLE module configuration</span></span>

<span data-ttu-id="b1bda-232">В примере конфигурации для устройства BLE предполагается, что используется устройство Texas Instruments SensorTag.</span><span class="sxs-lookup"><span data-stu-id="b1bda-232">The sample configuration for the BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="b1bda-233">Любое стандартное устройство BLE, которое может функционировать как периферийное устройство GATT, должно работать, но для этого может потребоваться обновление идентификаторов характеристик и данных GATT.</span><span class="sxs-lookup"><span data-stu-id="b1bda-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need to update the GATT characteristic IDs and data.</span></span> <span data-ttu-id="b1bda-234">Добавьте MAC-адрес устройства SensorTag:</span><span class="sxs-lookup"><span data-stu-id="b1bda-234">Add the MAC address of your SensorTag device:</span></span>

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

<span data-ttu-id="b1bda-235">Если устройство SensorTag не используется, просмотрите документацию устройства BLE, чтобы определить, следует ли обновить идентификаторы характеристик GATT и значения данных.</span><span class="sxs-lookup"><span data-stu-id="b1bda-235">If you are not using a SensorTag device, review the documentation for your BLE device to determine whether you need to update the GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="b1bda-236">Модуль Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="b1bda-236">IoT Hub module</span></span>

<span data-ttu-id="b1bda-237">Добавьте имя центра IoT.</span><span class="sxs-lookup"><span data-stu-id="b1bda-237">Add the name of your IoT Hub.</span></span> <span data-ttu-id="b1bda-238">Значением суффикса обычно является **azure-devices.net**:</span><span class="sxs-lookup"><span data-stu-id="b1bda-238">The suffix value is typically **azure-devices.net**:</span></span>

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="b1bda-239">Конфигурация модуля сопоставления удостоверений</span><span class="sxs-lookup"><span data-stu-id="b1bda-239">Identity mapping module configuration</span></span>

<span data-ttu-id="b1bda-240">Добавьте MAC-адрес устройства SensorTag, а также идентификатор и ключ устройства **SensorTag_01**, которое вы добавили в Центр Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="b1bda-240">Add the MAC address of your SensorTag device and the device ID and key of the **SensorTag_01** device you added to your IoT Hub:</span></span>

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="b1bda-241">Конфигурация модуля принтера BLE</span><span class="sxs-lookup"><span data-stu-id="b1bda-241">BLE Printer module configuration</span></span>

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="b1bda-242">Конфигурация модуля BLEC2D</span><span class="sxs-lookup"><span data-stu-id="b1bda-242">BLEC2D Module Configuration</span></span>

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a><span data-ttu-id="b1bda-243">Конфигурация маршрутизации</span><span class="sxs-lookup"><span data-stu-id="b1bda-243">Routing Configuration</span></span>

<span data-ttu-id="b1bda-244">Указанные ниже параметры конфигурации гарантируют, что маршрутизация между модулями Edge Интернета вещей будет выполняться следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b1bda-244">The following configuration ensures the following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="b1bda-245">Модуль **ведения журнала** получает и регистрирует все сообщения.</span><span class="sxs-lookup"><span data-stu-id="b1bda-245">The **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="b1bda-246">Модуль **SensorTag** отправляет сообщения в модуль **mapping** и модуль **принтера BLE**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-246">The **SensorTag** module sends messages to both the **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="b1bda-247">Модуль **mapping** отправляет в модуль **IoTHub** сообщения, которые затем будут отправляться в ваш Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b1bda-247">The **mapping** module sends messages to the **IoTHub** module to be sent up to your IoT Hub.</span></span>
* <span data-ttu-id="b1bda-248">Модуль **IoTHub** отправляет сообщения обратно в модуль **mapping**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-248">The **IoTHub** module sends messages back to the **mapping** module.</span></span>
* <span data-ttu-id="b1bda-249">Модуль **mapping** отправляет сообщения в модуль **BLEC2D**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-249">The **mapping** module sends messages to the **BLEC2D** module.</span></span>
* <span data-ttu-id="b1bda-250">Модуль **BLEC2D** отправляет сообщения обратно в модуль **SensorTag**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-250">The **BLEC2D** module sends messages back to the **Sensor Tag** module.</span></span>

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

<span data-ttu-id="b1bda-251">Для запуска примера передайте в двоичный файл **ble\_gateway** путь к файлу конфигурации JSON в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="b1bda-251">To run the sample, pass the path to the JSON configuration file as a parameter to the **ble\_gateway** binary.</span></span> <span data-ttu-id="b1bda-252">В следующей команде предполагается, что вы используете файл конфигурации **gateway_sample.json**.</span><span class="sxs-lookup"><span data-stu-id="b1bda-252">The following command assumes you are using the **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="b1bda-253">Выполните эту команду из папки **iot-edge** на устройстве Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="b1bda-253">Execute this command from the **iot-edge** folder on the Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="b1bda-254">Перед запуском примера может потребоваться нажать маленькую кнопку на устройстве SensorTag, чтобы сделать его доступным для обнаружения.</span><span class="sxs-lookup"><span data-stu-id="b1bda-254">You may need to press the small button on the SensorTag device to make it discoverable before you run the sample.</span></span>

<span data-ttu-id="b1bda-255">При запуске примера можно использовать такие инструменты, как [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) или [обозреватель Центра Интернета вещей](https://github.com/Azure/iothub-explorer), для мониторинга сообщений, которые шлюз Edge Интернета вещей перенаправляет с устройства SensorTag.</span><span class="sxs-lookup"><span data-stu-id="b1bda-255">When you run the sample, you can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to monitor the messages the IoT Edge gateway forwards from the SensorTag device.</span></span> <span data-ttu-id="b1bda-256">Например, с помощью средства iothub-explorer вы можете отслеживать сообщения, отправляемые с устройства в облако, с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="b1bda-256">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="b1bda-257">Отправка сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="b1bda-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="b1bda-258">Модуль BLE также поддерживает отправку команд из Центра Интернета вещей на устройство.</span><span class="sxs-lookup"><span data-stu-id="b1bda-258">The BLE module also supports sending commands from IoT Hub to the device.</span></span> <span data-ttu-id="b1bda-259">Для отправки сообщений JSON, которые модуль шлюза BLE направляет на устройство BLE, можно использовать [обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) или [обозреватель Центра Интернета вещей (iothub-explorer)](https://github.com/Azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="b1bda-259">You can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to send JSON messages that the BLE gateway module forwards on to the BLE device.</span></span>

<span data-ttu-id="b1bda-260">При использовании устройства Texas Instruments SensorTag можно включить красный или зеленый светодиодные индикаторы или звуковой сигнал, отправив команды из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="b1bda-260">If you are using the Texas Instruments SensorTag device, you can turn on the red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="b1bda-261">Прежде чем отправлять команды из Центра Интернета вещей, необходимо сначала последовательно отправить два сообщения JSON, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="b1bda-261">Before you send commands from IoT Hub, first send the following two JSON messages in order.</span></span> <span data-ttu-id="b1bda-262">Затем можно будет отправить команды для включения светодиодных индикаторов или звукового сигнала.</span><span class="sxs-lookup"><span data-stu-id="b1bda-262">Then you can send any of the commands to turn on the lights or buzzer.</span></span>

1. <span data-ttu-id="b1bda-263">Выполните сброс всех светодиодных индикаторов и звуковых сигналов (отключите их).</span><span class="sxs-lookup"><span data-stu-id="b1bda-263">Reset all LEDs and the buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="b1bda-264">Настройте операции ввода-вывода как "удаленные".</span><span class="sxs-lookup"><span data-stu-id="b1bda-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="b1bda-265">Теперь можно будет отправить приведенные ниже команды для включения светодиодных индикаторов или звукового сигнала на устройстве SensorTag.</span><span class="sxs-lookup"><span data-stu-id="b1bda-265">Now you can send any of the following commands to turn on the lights or buzzer on the SensorTag device:</span></span>

* <span data-ttu-id="b1bda-266">Включение красного светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="b1bda-266">Turn on the red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="b1bda-267">Включение зеленого светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="b1bda-267">Turn on the green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="b1bda-268">Включение звукового сигнала.</span><span class="sxs-lookup"><span data-stu-id="b1bda-268">Turn on the buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="b1bda-269">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b1bda-269">Next Steps</span></span>

<span data-ttu-id="b1bda-270">Если вы хотите подробнее изучить возможности Edge Интернета вещей и поэкспериментировать с примерами кода, см. следующие руководства и ресурсы для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="b1bda-270">If you want to gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="b1bda-271">[Azure IoT Edge][lnk-sdk] (Edge Интернета вещей Azure).</span><span class="sxs-lookup"><span data-stu-id="b1bda-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="b1bda-272">Для дальнейшего изучения возможностей центра IoT см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="b1bda-272">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b1bda-273">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="b1bda-273">[IoT Hub developer guide][lnk-devguide]</span></span>

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
