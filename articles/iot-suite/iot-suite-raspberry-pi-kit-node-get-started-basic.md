---
title: "aaaConnect tooAzure Raspberry Pi IoT Suite с помощью Node.js с реальными датчики | Документы Microsoft"
description: "Используйте hello Microsoft Azure IoT начального набора для hello Raspberry Pi 3 и Azure IoT Suite. Использовать Node.js tooconnect toohello вашей Raspberry Pi удаленного решением для мониторинга, отправка данных телеметрии с датчиками toohello облака и отвечать toomethods из панели мониторинга hello решения."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="f53c1-104">Подключения вашей Raspberry Pi 3 toohello удаленного решением для мониторинга и отправка данных телеметрии с реальными датчика с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="f53c1-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="f53c1-105">Этот учебник показывает, как toouse hello Microsoft Azure IoT начального набора для toodevelop Raspberry Pi 3 температуры и влажности чтения, которая может обмениваться данными с облаком hello.</span><span class="sxs-lookup"><span data-stu-id="f53c1-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="f53c1-106">Hello учебнике используется:</span><span class="sxs-lookup"><span data-stu-id="f53c1-106">hello tutorial uses:</span></span>

- <span data-ttu-id="f53c1-107">ОС Raspbian hello Node.js языка программирования и hello Microsoft Azure IoT SDK для Node.js tooimplement устройства образца.</span><span class="sxs-lookup"><span data-stu-id="f53c1-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="f53c1-108">удаленный мониторинг Hello IoT Suite предварительно настроить решение в hello облачной серверной части.</span><span class="sxs-lookup"><span data-stu-id="f53c1-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="f53c1-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="f53c1-109">Overview</span></span>

<span data-ttu-id="f53c1-110">В этом учебнике необходимо выполнить следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="f53c1-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="f53c1-111">Разверните экземпляр hello удаленного мониторинга предварительно настроенных решений tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="f53c1-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="f53c1-112">На этом шаге автоматически разворачивается и настраивается несколько служб Azure.</span><span class="sxs-lookup"><span data-stu-id="f53c1-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="f53c1-113">Настройка вашего устройства и датчики toocommunicate на компьютер и hello удаленного решением для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="f53c1-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="f53c1-114">Обновите hello образец кода tooconnect toohello удаленного мониторинга устройствами и отправлять данные телеметрии, можно просмотреть на панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="f53c1-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="f53c1-115">Hello удаленного мониторинга решения подготавливает набор служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="f53c1-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="f53c1-116">Развертывание Hello отражает реальные корпоративной архитектуре.</span><span class="sxs-lookup"><span data-stu-id="f53c1-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="f53c1-117">плата tooavoid ненужные использование Azure, удаление экземпляра hello предварительно настроенное решение в azureiotsuite.com после завершения с ним.</span><span class="sxs-lookup"><span data-stu-id="f53c1-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="f53c1-118">Если предварительно настроенных решений требуется hello еще раз, то ее можно легко восстановить.</span><span class="sxs-lookup"><span data-stu-id="f53c1-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="f53c1-119">Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="f53c1-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="f53c1-120">Загрузить и настроить образец hello</span><span class="sxs-lookup"><span data-stu-id="f53c1-120">Download and configure hello sample</span></span>

<span data-ttu-id="f53c1-121">Теперь можно загрузить и настроить hello удаленного мониторинга клиентского приложения на ваш Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f53c1-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="f53c1-122">Установка Node.js</span><span class="sxs-lookup"><span data-stu-id="f53c1-122">Install Node.js</span></span>

<span data-ttu-id="f53c1-123">Установите Node.js на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f53c1-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="f53c1-124">Hello IoT пакет SDK для Node.js требует 0.11.5 Node.js или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f53c1-124">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="f53c1-125">Hello следующие шаги показывают, как tooinstall v6.10.2 Node.js на ваш Pi Raspberry:</span><span class="sxs-lookup"><span data-stu-id="f53c1-125">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="f53c1-126">Используйте hello следующая команда tooupdate вашей Pi Raspberry:</span><span class="sxs-lookup"><span data-stu-id="f53c1-126">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="f53c1-127">Используйте следующие двоичные файлы Node.js tooyour Raspberry Pi команда toodownload hello hello.</span><span class="sxs-lookup"><span data-stu-id="f53c1-127">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="f53c1-128">Используйте следующие двоичные файлы hello tooinstall команда hello.</span><span class="sxs-lookup"><span data-stu-id="f53c1-128">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="f53c1-129">Используйте hello следующая команда tooverify установки Node.js v6.10.2 успешно:</span><span class="sxs-lookup"><span data-stu-id="f53c1-129">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="f53c1-130">Клонирование репозиториев hello</span><span class="sxs-lookup"><span data-stu-id="f53c1-130">Clone hello repositories</span></span>

<span data-ttu-id="f53c1-131">Если это еще не сделано, клон hello требуемые hello репозиториев, выполнив следующие команды на ваш Pi:</span><span class="sxs-lookup"><span data-stu-id="f53c1-131">If you haven't already done so, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="f53c1-132">Обновление строки подключения устройства hello</span><span class="sxs-lookup"><span data-stu-id="f53c1-132">Update hello device connection string</span></span>

<span data-ttu-id="f53c1-133">Привет открыть образец исходного файла в hello **nano** редактора с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f53c1-133">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="f53c1-134">Найдите строку hello:</span><span class="sxs-lookup"><span data-stu-id="f53c1-134">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="f53c1-135">Замените значения заполнителей hello и информации центр IoT был создан и сохранен в начале этого учебника hello hello устройства.</span><span class="sxs-lookup"><span data-stu-id="f53c1-135">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="f53c1-136">Сохранить изменения (**Ctrl-O**, **ввод**) и редактор hello выхода (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="f53c1-136">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="f53c1-137">Запуск образца hello</span><span class="sxs-lookup"><span data-stu-id="f53c1-137">Run hello sample</span></span>

<span data-ttu-id="f53c1-138">Выполнения hello следующими командами tooinstall hello пакеты необходимых компонентов для образца hello:</span><span class="sxs-lookup"><span data-stu-id="f53c1-138">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="f53c1-139">Теперь можно запустить образец hello программы для hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f53c1-139">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="f53c1-140">Введите команду hello:</span><span class="sxs-lookup"><span data-stu-id="f53c1-140">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="f53c1-141">Hello следующий результат приводится пример hello выходные данные, отображаемые на hello Raspberry Pi hello командной строке:</span><span class="sxs-lookup"><span data-stu-id="f53c1-141">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Выходные данные приложения Raspberry Pi][img-raspberry-output]

<span data-ttu-id="f53c1-143">Нажмите клавишу **Ctrl-C** tooexit программа hello в любое время.</span><span class="sxs-lookup"><span data-stu-id="f53c1-143">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="f53c1-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f53c1-144">Next steps</span></span>

<span data-ttu-id="f53c1-145">Посетите hello [Центр разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/) Дополнительные примеры и документация по Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="f53c1-145">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
