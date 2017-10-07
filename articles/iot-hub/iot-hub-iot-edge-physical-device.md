---
title: "aaaUse физического устройства в Azure IoT Edge | Документы Microsoft"
description: "Как toouse SensorTag инструментов Техас устройства toosend данных tooan центр IoT через IoT шлюзом, запущенного на устройстве Raspberry Pi 3. шлюз Hello построен с использованием Azure IoT Edge."
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
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="068dd-104">Преимущества использования Azure IoT tooIoT сообщения из устройства в облако tooforward Raspberry Pi концентратора</span><span class="sxs-lookup"><span data-stu-id="068dd-104">Use Azure IoT Edge on a Raspberry Pi tooforward device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="068dd-105">В этом пошаговом руководстве для hello [образец низкого энергопотребления Bluetooth] [ lnk-ble-samplecode] показано, как toouse [Azure IoT Edge] [ lnk-sdk] для:</span><span class="sxs-lookup"><span data-stu-id="068dd-105">This walkthrough of hello [Bluetooth low energy sample][lnk-ble-samplecode] shows you how toouse [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="068dd-106">Устройства в облако телеметрии tooIoT концентратора вперед от физического устройства.</span><span class="sxs-lookup"><span data-stu-id="068dd-106">Forward device-to-cloud telemetry tooIoT Hub from a physical device.</span></span>
* <span data-ttu-id="068dd-107">Команды маршрута из центра IoT tooa физического устройства.</span><span class="sxs-lookup"><span data-stu-id="068dd-107">Route commands from IoT Hub tooa physical device.</span></span>

<span data-ttu-id="068dd-108">В этом руководстве рассматриваются следующие темы.</span><span class="sxs-lookup"><span data-stu-id="068dd-108">This walkthrough covers:</span></span>

* <span data-ttu-id="068dd-109">**Архитектура**: важные сведения об низкого энергопотребления образец hello Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="068dd-109">**Architecture**: important architectural information about hello Bluetooth low energy sample.</span></span>
* <span data-ttu-id="068dd-110">**Построение и запуск**: пример hello выполнения и toobuild необходимые шаги hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-110">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="068dd-111">Архитектура</span><span class="sxs-lookup"><span data-stu-id="068dd-111">Architecture</span></span>

<span data-ttu-id="068dd-112">Hello пошаговом руководстве показано, как toobuild и выполнения IoT шлюз на Pi Raspberry 3, которое будет выполняться Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="068dd-112">hello walkthrough shows you how toobuild and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="068dd-113">шлюз Hello построен с использованием IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="068dd-113">hello gateway is built using IoT Edge.</span></span> <span data-ttu-id="068dd-114">Образец Hello использует данных температуры toocollect устройства энергии низкий Техас инструментов SensorTag Bluetooth (Разрешить).</span><span class="sxs-lookup"><span data-stu-id="068dd-114">hello sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device toocollect temperature data.</span></span>

<span data-ttu-id="068dd-115">При запуске hello IoT шлюзом его:</span><span class="sxs-lookup"><span data-stu-id="068dd-115">When you run hello IoT Edge gateway it:</span></span>

* <span data-ttu-id="068dd-116">Подключение устройства SensorTag tooa, с помощью протокола hello энергии низкий Bluetooth (Разрешить).</span><span class="sxs-lookup"><span data-stu-id="068dd-116">Connects tooa SensorTag device using hello Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="068dd-117">TooIoT концентратора подключается с использованием протокола hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="068dd-117">Connects tooIoT Hub using hello HTTP protocol.</span></span>
* <span data-ttu-id="068dd-118">Передает данные телеметрии из hello SensorTag устройства tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="068dd-118">Forwards telemetry from hello SensorTag device tooIoT Hub.</span></span>
* <span data-ttu-id="068dd-119">Направляет команды из центра IoT toohello SensorTag устройства.</span><span class="sxs-lookup"><span data-stu-id="068dd-119">Routes commands from IoT Hub toohello SensorTag device.</span></span>

<span data-ttu-id="068dd-120">шлюз Hello содержит следующие модули IoT Edge hello:</span><span class="sxs-lookup"><span data-stu-id="068dd-120">hello gateway contains hello following IoT Edge modules:</span></span>

* <span data-ttu-id="068dd-121">Объект *ЛЮЧИТЬ модуль* , взаимодействующего с tooreceive температуры ЛЮЧИТЬ устройства данных из hello и устройством toohello команды send.</span><span class="sxs-lookup"><span data-stu-id="068dd-121">A *BLE module* that interfaces with a BLE device tooreceive temperature data from hello device and send commands toohello device.</span></span>
* <span data-ttu-id="068dd-122">Объект *ЛЮЧИТЬ облака toodevice модуль* , преобразующий сообщения JSON, отправленные из центра IoT в инструкции ЛЮЧИТЬ для hello *ЛЮЧИТЬ модуля*.</span><span class="sxs-lookup"><span data-stu-id="068dd-122">A *BLE cloud toodevice module* that translates JSON messages sent from IoT Hub into BLE instructions for hello *BLE module*.</span></span>
* <span data-ttu-id="068dd-123">Объект *модуль ведения журнала* , регистрирует все шлюза сообщений tooa локального файла.</span><span class="sxs-lookup"><span data-stu-id="068dd-123">A *logger module* that logs all gateway messages tooa local file.</span></span>
* <span data-ttu-id="068dd-124">*Модуль сопоставления удостоверений* , который преобразовывает MAC-адреса устройств BLE и удостоверения устройств центра Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="068dd-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="068dd-125">*Центр IoT модуль* , отправляет центр IoT tooan данных телеметрии и получает команды от центра IoT.</span><span class="sxs-lookup"><span data-stu-id="068dd-125">An *IoT Hub module* that uploads telemetry data tooan IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="068dd-126">Объект *ЛЮЧИТЬ принтера модуль* , интерпретирует данные телеметрии с устройства ЛЮЧИТЬ hello и печатает форматированные данные toohello консоли tooenable неполадок и отладка.</span><span class="sxs-lookup"><span data-stu-id="068dd-126">A *BLE printer module* that interprets telemetry from hello BLE device and prints formatted data toohello console tooenable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-hello-gateway"></a><span data-ttu-id="068dd-127">Потоки данных через шлюз hello</span><span class="sxs-lookup"><span data-stu-id="068dd-127">How data flows through hello gateway</span></span>

<span data-ttu-id="068dd-128">Следующая блок-схема Hello показано конвейера потока данных передачи телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-128">hello following block diagram illustrates hello telemetry upload data flow pipeline:</span></span>

![Конвейер шлюза отправки данных телеметрии](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="068dd-130">Привет, который принимает элемент телеметрии проходящих из tooIoT отключить устройство концентратора, необходимо:</span><span class="sxs-lookup"><span data-stu-id="068dd-130">hello steps that an item of telemetry takes traveling from a BLE device tooIoT Hub are:</span></span>

1. <span data-ttu-id="068dd-131">Отключить устройство Hello создает образец температуры и отправляет его по модуль ЛЮЧИТЬ toohello Bluetooth на шлюзе hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-131">hello BLE device generates a temperature sample and sends it over Bluetooth toohello BLE module in hello gateway.</span></span>
1. <span data-ttu-id="068dd-132">модуль ЛЮЧИТЬ Hello Получает образец hello и публикует его broker toohello вместе с hello MAC-адрес устройства hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-132">hello BLE module receives hello sample and publishes it toohello broker along with hello MAC address of hello device.</span></span>
1. <span data-ttu-id="068dd-133">модуль сопоставления удостоверений Hello принимает это сообщение и использует внутреннюю таблицу tootranslate hello MAC-адрес устройства hello в центр IoT удостоверение устройства.</span><span class="sxs-lookup"><span data-stu-id="068dd-133">hello identity mapping module picks up this message and uses an internal table tootranslate hello MAC address of hello device into an IoT Hub device identity.</span></span> <span data-ttu-id="068dd-134">Удостоверение устройства Центра Интернета вещей состоит из идентификатора и ключа устройства.</span><span class="sxs-lookup"><span data-stu-id="068dd-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="068dd-135">модуль сопоставления удостоверений Hello публикует новое сообщение, которое содержит образец hello температур, hello MAC-адрес устройства hello, идентификатор устройства hello и ключ устройства hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-135">hello identity mapping module publishes a new message that contains hello temperature sample data, hello MAC address of hello device, hello device ID, and hello device key.</span></span>
1. <span data-ttu-id="068dd-136">Hello центра IoT модуль получает это новое сообщение (создаваемые модулем сопоставления удостоверений hello) и публикует его tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="068dd-136">hello IoT Hub module receives this new message (generated by hello identity mapping module) and publishes it tooIoT Hub.</span></span>
1. <span data-ttu-id="068dd-137">модуль ведения журнала Hello заносит в журнал все сообщения из локального файла hello broker tooa.</span><span class="sxs-lookup"><span data-stu-id="068dd-137">hello logger module logs all messages from hello broker tooa local file.</span></span>

<span data-ttu-id="068dd-138">Следующая блок-схема Hello показано конвейера потока данных команда устройства hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-138">hello following block diagram illustrates hello device command data flow pipeline:</span></span>

![Конвейер шлюза команд устройства](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="068dd-140">Центр IoT модуль периодически опрашивает Hello hello центр IoT для новых командных сообщений.</span><span class="sxs-lookup"><span data-stu-id="068dd-140">hello IoT Hub module periodically polls hello IoT hub for new command messages.</span></span>
1. <span data-ttu-id="068dd-141">Получив команду новое сообщение hello центра IoT модуля он публикуется toohello broker.</span><span class="sxs-lookup"><span data-stu-id="068dd-141">When hello IoT Hub module receives a new command message, it publishes it toohello broker.</span></span>
1. <span data-ttu-id="068dd-142">модуль сопоставления удостоверений Hello сообщение hello команды и использование внутренней таблицы tootranslate hello центра IoT идентификатор tooa одноранговой MAC-адрес.</span><span class="sxs-lookup"><span data-stu-id="068dd-142">hello identity mapping module picks up hello command message and uses an internal table tootranslate hello IoT Hub device ID tooa device MAC address.</span></span> <span data-ttu-id="068dd-143">Затем он публикует новое сообщение, которое включает в себя hello MAC-адрес целевого устройства hello в карту приветственное сообщение hello свойства.</span><span class="sxs-lookup"><span data-stu-id="068dd-143">It then publishes a new message that includes hello MAC address of hello target device in hello properties map of hello message.</span></span>
1. <span data-ttu-id="068dd-144">модуль ЛЮЧИТЬ облака на устройство Hello воспринимает это сообщение и преобразует его в инструкции правильную ЛЮЧИТЬ hello hello ЛЮЧИТЬ модуля.</span><span class="sxs-lookup"><span data-stu-id="068dd-144">hello BLE Cloud-to-Device module picks up this message and translates it into hello proper BLE instruction for hello BLE module.</span></span> <span data-ttu-id="068dd-145">Затем он публикует новое сообщение.</span><span class="sxs-lookup"><span data-stu-id="068dd-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="068dd-146">модуль ЛЮЧИТЬ Hello принимает это сообщение и выполнение инструкции hello ввода-вывода в связи с устройством ЛЮЧИТЬ hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-146">hello BLE module picks up this message and executes hello I/O instruction by communicating with hello BLE device.</span></span>
1. <span data-ttu-id="068dd-147">модуль ведения журнала Hello заносит в журнал все сообщения из файла на диске tooa broker hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-147">hello logger module logs all messages from hello broker tooa disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="068dd-148">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="068dd-148">Prerequisites</span></span>

<span data-ttu-id="068dd-149">toocomplete этого учебника требуется Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="068dd-149">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="068dd-150">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="068dd-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="068dd-151">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="068dd-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="068dd-152">Требуется клиент SSH на tooenable на настольном компьютере, вы tooremotely доступ hello командную строку на hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="068dd-152">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="068dd-153">Windows не предоставляет клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="068dd-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="068dd-154">Мы советуем использовать [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="068dd-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="068dd-155">Большинство дистрибутивах Linux и Mac OS включают программу командной строки SSH hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-155">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="068dd-156">Дополнительные сведения см. в статье [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (Подключение по протоколу SSH с помощью Linux или Mac OS).</span><span class="sxs-lookup"><span data-stu-id="068dd-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="068dd-157">Подготовка оборудования</span><span class="sxs-lookup"><span data-stu-id="068dd-157">Prepare your hardware</span></span>

<span data-ttu-id="068dd-158">В этом учебнике предполагается, вы используете [SensorTag инструментов Техас](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) tooa Raspberry Pi 3 подключено устройство под управлением Raspbian.</span><span class="sxs-lookup"><span data-stu-id="068dd-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected tooa Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="068dd-159">Установка Raspbian</span><span class="sxs-lookup"><span data-stu-id="068dd-159">Install Raspbian</span></span>

<span data-ttu-id="068dd-160">Можно использовать либо hello следующие параметры tooinstall Raspbian на вашем устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="068dd-160">You can use either of hello following options tooinstall Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="068dd-161">tooinstall hello последнюю версию Raspbian hello используйте [NOOBS] [ lnk-noobs] графического интерфейса пользователя.</span><span class="sxs-lookup"><span data-stu-id="068dd-161">tooinstall hello latest version of Raspbian, use hello [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="068dd-162">Вручную [загрузки] [ lnk-raspbian] и записать образ последнюю hello hello Raspbian операционной системы tooan SD-карты.</span><span class="sxs-lookup"><span data-stu-id="068dd-162">Manually [download][lnk-raspbian] and write hello latest image of hello Raspbian operating system tooan SD card.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="068dd-163">Вход и доступ к терминалов hello</span><span class="sxs-lookup"><span data-stu-id="068dd-163">Sign in and access hello terminal</span></span>

<span data-ttu-id="068dd-164">У вас есть два tooaccess параметры терминалов среды с вашей пи Raspberry:</span><span class="sxs-lookup"><span data-stu-id="068dd-164">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="068dd-165">Если клавиатура и отслеживать подключенных tooyour Raspberry Pi, можно использовать tooaccess Raspbian GUI hello окно терминала.</span><span class="sxs-lookup"><span data-stu-id="068dd-165">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

* <span data-ttu-id="068dd-166">Командная строка hello доступа на ваш Raspberry Pi, с помощью SSH из настольном компьютере.</span><span class="sxs-lookup"><span data-stu-id="068dd-166">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="068dd-167">Использование окна терминала в hello графического пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="068dd-167">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="068dd-168">имя пользователя, учетные данные по умолчанию Hello для Raspbian **pi** и пароль **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="068dd-168">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="068dd-169">На панели задач hello в hello графического пользовательского интерфейса, можно запустить hello **терминалов** hello значок, который выглядит как монитор с помощью служебной программы.</span><span class="sxs-lookup"><span data-stu-id="068dd-169">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="068dd-170">Вход с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="068dd-170">Sign in with SSH</span></span>

<span data-ttu-id="068dd-171">Можно использовать SSH для командной строки доступ tooyour Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="068dd-171">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="068dd-172">статья Hello [SSH (Secure Shell)] [ lnk-pi-ssh] описывает как tooconfigure SSH с вашей пи Raspberry и как tooconnect из [Windows] [ lnk-ssh-windows] или [Linux и Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="068dd-172">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="068dd-173">Войдите, используя имя пользователя **pi** и пароль **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="068dd-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="068dd-174">Установка BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="068dd-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="068dd-175">модули ЛЮЧИТЬ Hello поговорим оборудования Bluetooth toohello через стек BlueZ hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-175">hello BLE modules talk toohello Bluetooth hardware via hello BlueZ stack.</span></span> <span data-ttu-id="068dd-176">Необходима версия 5.37 BlueZ для hello модули toowork правильно.</span><span class="sxs-lookup"><span data-stu-id="068dd-176">You need version 5.37 of BlueZ for hello modules toowork correctly.</span></span> <span data-ttu-id="068dd-177">Эти инструкции убедитесь, что установлена правильная версия BlueZ hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-177">These instructions make sure hello correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="068dd-178">Остановка текущего bluetooth демон hello:</span><span class="sxs-lookup"><span data-stu-id="068dd-178">Stop hello current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="068dd-179">Установка зависимостей BlueZ hello:</span><span class="sxs-lookup"><span data-stu-id="068dd-179">Install hello BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="068dd-180">Загрузите bluez.org hello BlueZ исходный код:</span><span class="sxs-lookup"><span data-stu-id="068dd-180">Download hello BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="068dd-181">Распакуйте hello исходный код:</span><span class="sxs-lookup"><span data-stu-id="068dd-181">Unzip hello source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="068dd-182">Изменить папку toohello вновь созданные каталоги:</span><span class="sxs-lookup"><span data-stu-id="068dd-182">Change directories toohello newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="068dd-183">Настройте hello BlueZ кода toobe построения:</span><span class="sxs-lookup"><span data-stu-id="068dd-183">Configure hello BlueZ code toobe built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="068dd-184">Выполните сборку BlueZ:</span><span class="sxs-lookup"><span data-stu-id="068dd-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="068dd-185">По завершении сборки установите BlueZ:</span><span class="sxs-lookup"><span data-stu-id="068dd-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="068dd-186">Изменение конфигурации службы systemd для bluetooth, теперь он указывает toohello новый демон bluetooth в файле hello `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="068dd-186">Change systemd service configuration for bluetooth so it points toohello new bluetooth daemon in hello file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="068dd-187">Замените строку «ExecStart» hello hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="068dd-187">Replace hello 'ExecStart' line with hello following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="068dd-188">Включить устройство SensorTag toohello подключения с устройства Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="068dd-188">Enable connectivity toohello SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="068dd-189">Для выполнения образца hello требуется tooverify, что ваш Pi 3 Raspberry подключить устройство SensorTag toohello.</span><span class="sxs-lookup"><span data-stu-id="068dd-189">Before running hello sample, you need tooverify that your Raspberry Pi 3 can connect toohello SensorTag device.</span></span>

1. <span data-ttu-id="068dd-190">Убедитесь, hello `rfkill` служебная программа устанавливается:</span><span class="sxs-lookup"><span data-stu-id="068dd-190">Ensure hello `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="068dd-191">Разблокировать bluetooth на hello Raspberry Pi 3 и проверьте номер версии hello **5.37**:</span><span class="sxs-lookup"><span data-stu-id="068dd-191">Unblock bluetooth on hello Raspberry Pi 3 and check that hello version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="068dd-192">оболочка интерактивный bluetooth tooenter hello, запустите службу hello bluetooth и выполнения hello **bluetoothctl** команды:</span><span class="sxs-lookup"><span data-stu-id="068dd-192">tooenter hello interactive bluetooth shell, start hello bluetooth service and execute hello **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="068dd-193">Введите команду hello **включения питания** toopower hello bluetooth контроллера.</span><span class="sxs-lookup"><span data-stu-id="068dd-193">Enter hello command **power on** toopower up hello bluetooth controller.</span></span> <span data-ttu-id="068dd-194">Команда Hello возвращает аналогичные toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="068dd-194">hello command returns output similar toohello following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="068dd-195">В оболочке интерактивный bluetooth hello, введите команду hello **сканирования на** tooscan для устройствами bluetooth.</span><span class="sxs-lookup"><span data-stu-id="068dd-195">In hello interactive bluetooth shell, enter hello command **scan on** tooscan for bluetooth devices.</span></span> <span data-ttu-id="068dd-196">Команда Hello возвращает аналогичные toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="068dd-196">hello command returns output similar toohello following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="068dd-197">Сделать доступной для обнаружения устройств SensorTag hello и нажав кнопку небольшой hello (приветствия мигания зеленый Индикатор).</span><span class="sxs-lookup"><span data-stu-id="068dd-197">Make hello SensorTag device discoverable by pressing hello small button (hello green LED should flash).</span></span> <span data-ttu-id="068dd-198">Hello Raspberry Pi 3 должны обнаруживать устройства SensorTag hello:</span><span class="sxs-lookup"><span data-stu-id="068dd-198">hello Raspberry Pi 3 should discover hello SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="068dd-199">В этом примере видно, hello MAC-адрес hello устройство SensorTag **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="068dd-199">In this example, you can see that hello MAC address of hello SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="068dd-200">Отключение сканирования, введя hello **сканирования** команды:</span><span class="sxs-lookup"><span data-stu-id="068dd-200">Turn off scanning by entering hello **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="068dd-201">Подключите устройство SensorTag tooyour с помощью его MAC-адрес, введя **подключения \<MAC-адрес\>**.</span><span class="sxs-lookup"><span data-stu-id="068dd-201">Connect tooyour SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="068dd-202">для ясности является сокращенным Hello следующий образец вывода:</span><span class="sxs-lookup"><span data-stu-id="068dd-202">hello following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
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

    > <span data-ttu-id="068dd-203">Вы можете вывести список характеристик GATT hello hello устройства, еще раз, используя hello **атрибуты списка** команды.</span><span class="sxs-lookup"><span data-stu-id="068dd-203">You can list hello GATT characteristics of hello device again using hello **list-attributes** command.</span></span>

1. <span data-ttu-id="068dd-204">Теперь можно отключить с помощью hello устройства hello **отключения** команды и выйдите из оболочки hello bluetooth, с помощью hello **quit** команды:</span><span class="sxs-lookup"><span data-stu-id="068dd-204">You can now disconnect from hello device using hello **disconnect** command and then exit from hello bluetooth shell using hello **quit** command:</span></span>

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="068dd-205">Теперь вы готовы toorun hello ЛЮЧИТЬ IoT Edge образец на Pi вашей Raspberry 3.</span><span class="sxs-lookup"><span data-stu-id="068dd-205">You're now ready toorun hello BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-hello-iot-edge-ble-sample"></a><span data-ttu-id="068dd-206">Запуск образца hello ЛЮЧИТЬ Edge IoT</span><span class="sxs-lookup"><span data-stu-id="068dd-206">Run hello IoT Edge BLE sample</span></span>

<span data-ttu-id="068dd-207">toorun hello IoT Edge ЛЮЧИТЬ образец необходимо toocomplete трех задач:</span><span class="sxs-lookup"><span data-stu-id="068dd-207">toorun hello IoT Edge BLE sample, you need toocomplete three tasks:</span></span>

* <span data-ttu-id="068dd-208">Настроить два примера устройств в центре IoT.</span><span class="sxs-lookup"><span data-stu-id="068dd-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="068dd-209">Создать Edge Интернета вещей на устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="068dd-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="068dd-210">Настройки и запуска образца ЛЮЧИТЬ hello на вашем устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="068dd-210">Configure and run hello BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="068dd-211">На момент написания статьи hello край IoT поддерживает только модули ЛЮЧИТЬ в шлюзы, выполняемым на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="068dd-211">At hello time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="068dd-212">Настройка двух примеров устройств в центре IoT</span><span class="sxs-lookup"><span data-stu-id="068dd-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="068dd-213">[Создать центр IoT] [ lnk-create-hub] в вашей подписке Azure необходимо имя вашей toocomplete концентратора hello в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="068dd-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="068dd-214">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="068dd-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="068dd-215">Добавьте одно устройство называется **SensorTag_01** tooyour центр IoT и запомните или запишите его идентификатор и устройства ключ.</span><span class="sxs-lookup"><span data-stu-id="068dd-215">Add one device called **SensorTag_01** tooyour IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="068dd-216">Можно использовать hello [обозреватель устройств или обозревателе центром IOT] [ lnk-explorer-tools] средств tooadd этот центр IoT toohello устройства, созданные в предыдущем шаге hello и tooretrieve его ключ.</span><span class="sxs-lookup"><span data-stu-id="068dd-216">You can use hello [device explorer or iothub-explorer][lnk-explorer-tools] tools tooadd this device toohello IoT hub you created in hello previous step and tooretrieve its key.</span></span> <span data-ttu-id="068dd-217">При настройке шлюза hello сопоставлении этого устройства SensorTag toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="068dd-217">You map this device toohello SensorTag device when you configure hello gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="068dd-218">Создание Edge Интернета вещей Azure на устройстве Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="068dd-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="068dd-219">Установите зависимые компоненты Edge Интернета вещей Azure:</span><span class="sxs-lookup"><span data-stu-id="068dd-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="068dd-220">Используйте hello следующими командами tooclone IoT края и все его подмодулей tooyour домашний каталог:</span><span class="sxs-lookup"><span data-stu-id="068dd-220">Use hello following commands tooclone IoT Edge and all its submodules tooyour home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="068dd-221">При наличии полную копию hello IoT Edge репозитория на Pi вашей Raspberry 3 можно создать ее с помощью hello следующую команду из папки hello, содержащий hello SDK:</span><span class="sxs-lookup"><span data-stu-id="068dd-221">When you have a complete copy of hello IoT Edge repository on your Raspberry Pi 3, you can build it using hello following command from hello folder that contains hello SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="068dd-222">Настройки и запуска образца hello ЛЮЧИТЬ на Pi вашей Raspberry 3</span><span class="sxs-lookup"><span data-stu-id="068dd-222">Configure and run hello BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="068dd-223">Пример выполнения hello и toobootstrap, необходимо настроить каждый модуль IoT Edge, участвующего в hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="068dd-223">toobootstrap and run hello sample, you must configure each IoT Edge module that participates in hello gateway.</span></span> <span data-ttu-id="068dd-224">Необходимая конфигурация предоставляется в файле JSON. Вам следует настроить все пять участвующих модулей Edge Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="068dd-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="068dd-225">Имеется пример JSON-файла в репозитории hello вызывается **шлюза\_sample.json** , можно использовать в качестве hello, начальной точкой для создания файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="068dd-225">There is a sample JSON file in hello repository called **gateway\_sample.json** that you can use as hello starting point for building your own configuration file.</span></span> <span data-ttu-id="068dd-226">Этот файл расположен в hello **образцы, ble_gateway/src** папки в локальной копии hello IoT Edge репозитория.</span><span class="sxs-lookup"><span data-stu-id="068dd-226">This file is in hello **samples/ble_gateway/src** folder in local copy of hello IoT Edge repository.</span></span>

<span data-ttu-id="068dd-227">Hello ниже описано, как tooedit этой конфигурации файла для образца hello ЛЮЧИТЬ и предполагается, hello репозитория IoT Edge возможности hello **/home/pi/iot-edge /** папку на Pi вашей Raspberry 3.</span><span class="sxs-lookup"><span data-stu-id="068dd-227">hello following sections describe how tooedit this configuration file for hello BLE sample and assume that hello IoT Edge repository is in hello **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="068dd-228">Если репозиторий hello в другом месте, соответствующим образом настройте hello пути.</span><span class="sxs-lookup"><span data-stu-id="068dd-228">If hello repository is elsewhere, adjust hello paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="068dd-229">Конфигурация средства ведения журнала</span><span class="sxs-lookup"><span data-stu-id="068dd-229">Logger configuration</span></span>

<span data-ttu-id="068dd-230">При условии, что репозитория hello шлюз находится в hello **/home/pi/iot-edge /** папки, настройте модуль ведения журнала hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="068dd-230">Assuming hello gateway repository is located in hello **/home/pi/iot-edge/** folder, configure hello logger module as follows:</span></span>

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

#### <a name="ble-module-configuration"></a><span data-ttu-id="068dd-231">Конфигурация модуля BLE</span><span class="sxs-lookup"><span data-stu-id="068dd-231">BLE module configuration</span></span>

<span data-ttu-id="068dd-232">Hello пример конфигурации для устройства ЛЮЧИТЬ hello предполагается SensorTag Техас инструментов устройства.</span><span class="sxs-lookup"><span data-stu-id="068dd-232">hello sample configuration for hello BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="068dd-233">Все стандартные отключить устройство, может работать как GATT периферийных устройств должны работать, но может потребоваться tooupdate hello GATT характеристика идентификаторов и данных.</span><span class="sxs-lookup"><span data-stu-id="068dd-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need tooupdate hello GATT characteristic IDs and data.</span></span> <span data-ttu-id="068dd-234">Добавьте hello MAC-адрес устройства SensorTag:</span><span class="sxs-lookup"><span data-stu-id="068dd-234">Add hello MAC address of your SensorTag device:</span></span>

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

<span data-ttu-id="068dd-235">Если устройство SensorTag не используются, документации hello вашей toodetermine отключить устройство, нужны ли вам tooupdate hello GATT характеристика идентификаторы и значения данных.</span><span class="sxs-lookup"><span data-stu-id="068dd-235">If you are not using a SensorTag device, review hello documentation for your BLE device toodetermine whether you need tooupdate hello GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="068dd-236">Модуль Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="068dd-236">IoT Hub module</span></span>

<span data-ttu-id="068dd-237">Добавьте имя вашего центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-237">Add hello name of your IoT Hub.</span></span> <span data-ttu-id="068dd-238">обычно является значение суффикса Hello **azure devices.net**:</span><span class="sxs-lookup"><span data-stu-id="068dd-238">hello suffix value is typically **azure-devices.net**:</span></span>

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

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="068dd-239">Конфигурация модуля сопоставления удостоверений</span><span class="sxs-lookup"><span data-stu-id="068dd-239">Identity mapping module configuration</span></span>

<span data-ttu-id="068dd-240">Добавить MAC-адрес hello SensorTag устройства, а идентификатор устройства hello и ключ hello **SensorTag_01** устройство, добавленное tooyour центр IoT:</span><span class="sxs-lookup"><span data-stu-id="068dd-240">Add hello MAC address of your SensorTag device and hello device ID and key of hello **SensorTag_01** device you added tooyour IoT Hub:</span></span>

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

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="068dd-241">Конфигурация модуля принтера BLE</span><span class="sxs-lookup"><span data-stu-id="068dd-241">BLE Printer module configuration</span></span>

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

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="068dd-242">Конфигурация модуля BLEC2D</span><span class="sxs-lookup"><span data-stu-id="068dd-242">BLEC2D Module Configuration</span></span>

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

#### <a name="routing-configuration"></a><span data-ttu-id="068dd-243">Конфигурация маршрутизации</span><span class="sxs-lookup"><span data-stu-id="068dd-243">Routing Configuration</span></span>

<span data-ttu-id="068dd-244">Hello ниже конфигурация обеспечивает следующие hello маршрутизации между модулями IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="068dd-244">hello following configuration ensures hello following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="068dd-245">Hello **средства ведения журнала** модуль получает и регистрирует все сообщения.</span><span class="sxs-lookup"><span data-stu-id="068dd-245">hello **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="068dd-246">Hello **SensorTag** модуль отправляет сообщения hello tooboth **сопоставления** и **принтера ЛЮЧИТЬ** модулей.</span><span class="sxs-lookup"><span data-stu-id="068dd-246">hello **SensorTag** module sends messages tooboth hello **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="068dd-247">Hello **сопоставления** модуль отправляет сообщения toohello **центром IOT** toobe модуль отправлялось tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="068dd-247">hello **mapping** module sends messages toohello **IoTHub** module toobe sent up tooyour IoT Hub.</span></span>
* <span data-ttu-id="068dd-248">Hello **центром IOT** модуль отправляет сообщений обратно toohello **сопоставления** модуля.</span><span class="sxs-lookup"><span data-stu-id="068dd-248">hello **IoTHub** module sends messages back toohello **mapping** module.</span></span>
* <span data-ttu-id="068dd-249">Hello **сопоставления** модуль отправляет сообщения toohello **BLEC2D** модуля.</span><span class="sxs-lookup"><span data-stu-id="068dd-249">hello **mapping** module sends messages toohello **BLEC2D** module.</span></span>
* <span data-ttu-id="068dd-250">Hello **BLEC2D** модуль отправляет сообщений обратно toohello **тег датчика** модуля.</span><span class="sxs-lookup"><span data-stu-id="068dd-250">hello **BLEC2D** module sends messages back toohello **Sensor Tag** module.</span></span>

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

<span data-ttu-id="068dd-251">Образец hello toorun, передайте hello путь toohello файл конфигурации JSON как toohello параметр **жбы\_шлюза** двоичный.</span><span class="sxs-lookup"><span data-stu-id="068dd-251">toorun hello sample, pass hello path toohello JSON configuration file as a parameter toohello **ble\_gateway** binary.</span></span> <span data-ttu-id="068dd-252">Hello следующая команда предполагает вы используете hello **gateway_sample.json** файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="068dd-252">hello following command assumes you are using hello **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="068dd-253">Выполните эту команду из hello **iot edge** папку на hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="068dd-253">Execute this command from hello **iot-edge** folder on hello Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="068dd-254">Может потребоваться toopress hello небольшой кнопку на устройстве toomake hello SensorTag ее доступной для обнаружения перед запуском образца hello.</span><span class="sxs-lookup"><span data-stu-id="068dd-254">You may need toopress hello small button on hello SensorTag device toomake it discoverable before you run hello sample.</span></span>

<span data-ttu-id="068dd-255">При запуске образца hello, можно использовать hello [обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) или hello [explorer центром IOT](https://github.com/Azure/iothub-explorer) средство toomonitor hello сообщений hello IoT шлюз пересылает hello SensorTag устройства.</span><span class="sxs-lookup"><span data-stu-id="068dd-255">When you run hello sample, you can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toomonitor hello messages hello IoT Edge gateway forwards from hello SensorTag device.</span></span> <span data-ttu-id="068dd-256">Например с помощью обозревателя с центром IOT можно отслеживать сообщения устройства в облако, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="068dd-256">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="068dd-257">Отправка сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="068dd-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="068dd-258">Hello ЛЮЧИТЬ модуль также поддерживает отправку команды из центра IoT toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="068dd-258">hello BLE module also supports sending commands from IoT Hub toohello device.</span></span> <span data-ttu-id="068dd-259">Можно использовать hello [обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) или hello [explorer центром IOT](https://github.com/Azure/iothub-explorer) сообщений JSON toosend средство модуля шлюза ЛЮЧИТЬ hello перенаправляет на устройстве ЛЮЧИТЬ toohello.</span><span class="sxs-lookup"><span data-stu-id="068dd-259">You can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toosend JSON messages that hello BLE gateway module forwards on toohello BLE device.</span></span>

<span data-ttu-id="068dd-260">Если вы используете устройство SensorTag инструментов Техас hello, можно включить Индикатор hello красный, зеленый Индикатор или звукового сигнала путем отправки команды из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="068dd-260">If you are using hello Texas Instruments SensorTag device, you can turn on hello red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="068dd-261">Прежде чем отправлять команды из центра IoT, сначала отправьте hello, следующие два сообщения JSON в порядке.</span><span class="sxs-lookup"><span data-stu-id="068dd-261">Before you send commands from IoT Hub, first send hello following two JSON messages in order.</span></span> <span data-ttu-id="068dd-262">Затем можно отправить hello tooturn команды на индикаторы hello или звукового сигнала.</span><span class="sxs-lookup"><span data-stu-id="068dd-262">Then you can send any of hello commands tooturn on hello lights or buzzer.</span></span>

1. <span data-ttu-id="068dd-263">Сбросьте все индикаторы и звукового сигнала hello (отключены):</span><span class="sxs-lookup"><span data-stu-id="068dd-263">Reset all LEDs and hello buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="068dd-264">Настройте операции ввода-вывода как "удаленные".</span><span class="sxs-lookup"><span data-stu-id="068dd-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="068dd-265">Теперь можно отправить после команды tooturn на индикаторы hello и звукового сигнала на устройстве SensorTag hello hello:</span><span class="sxs-lookup"><span data-stu-id="068dd-265">Now you can send any of hello following commands tooturn on hello lights or buzzer on hello SensorTag device:</span></span>

* <span data-ttu-id="068dd-266">Включите hello красный Индикатор.</span><span class="sxs-lookup"><span data-stu-id="068dd-266">Turn on hello red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="068dd-267">Включите hello зеленый Индикатор:</span><span class="sxs-lookup"><span data-stu-id="068dd-267">Turn on hello green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="068dd-268">Включите hello звукового сигнала.</span><span class="sxs-lookup"><span data-stu-id="068dd-268">Turn on hello buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="068dd-269">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="068dd-269">Next Steps</span></span>

<span data-ttu-id="068dd-270">Toogain более глубоким пониманием IoT края и поэкспериментировать с примерами кода, посетите следующие hello разработчика учебники и ресурсы:</span><span class="sxs-lookup"><span data-stu-id="068dd-270">If you want toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="068dd-271">[Azure IoT Edge][lnk-sdk] (Edge Интернета вещей Azure).</span><span class="sxs-lookup"><span data-stu-id="068dd-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="068dd-272">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="068dd-272">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="068dd-273">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="068dd-273">[IoT Hub developer guide][lnk-devguide]</span></span>

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
