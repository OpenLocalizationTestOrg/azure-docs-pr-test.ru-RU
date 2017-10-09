---
title: "aaaConnect tooAzure Raspberry Pi IoT Suite с помощью Node.js с имитацию телеметрии | Документы Microsoft"
description: "Используйте hello Microsoft Azure IoT начального набора для hello Raspberry Pi 3 и Azure IoT Suite. Использовать Node.js tooconnect toohello вашей Raspberry Pi удаленного решением для мониторинга, отправить облака toohello имитацию телеметрии и отвечать toomethods из панели мониторинга hello решения."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="43388-104">Подключения вашей Raspberry Pi 3 toohello удаленного решением для мониторинга и отправки смоделированные данные телеметрии с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="43388-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="43388-105">Этом учебнике показано, как hello toouse Raspberry Pi 3 toosimulate температуры и влажности данных toosend toohello облако.</span><span class="sxs-lookup"><span data-stu-id="43388-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="43388-106">Hello учебнике используется:</span><span class="sxs-lookup"><span data-stu-id="43388-106">hello tutorial uses:</span></span>

- <span data-ttu-id="43388-107">ОС Raspbian hello Node.js языка программирования и hello Microsoft Azure IoT SDK для Node.js tooimplement устройства образца.</span><span class="sxs-lookup"><span data-stu-id="43388-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="43388-108">удаленный мониторинг Hello IoT Suite предварительно настроить решение в hello облачной серверной части.</span><span class="sxs-lookup"><span data-stu-id="43388-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="43388-109">Hello удаленного мониторинга решения подготавливает набор служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="43388-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="43388-110">Развертывание Hello отражает реальные корпоративной архитектуре.</span><span class="sxs-lookup"><span data-stu-id="43388-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="43388-111">плата tooavoid ненужные использование Azure, удаление экземпляра hello предварительно настроенное решение в azureiotsuite.com после завершения с ним.</span><span class="sxs-lookup"><span data-stu-id="43388-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="43388-112">Если предварительно настроенных решений требуется hello еще раз, то ее можно легко восстановить.</span><span class="sxs-lookup"><span data-stu-id="43388-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="43388-113">Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="43388-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="43388-114">Загрузить и настроить образец hello</span><span class="sxs-lookup"><span data-stu-id="43388-114">Download and configure hello sample</span></span>

<span data-ttu-id="43388-115">Теперь можно загрузить и настроить hello удаленного мониторинга клиентского приложения на ваш Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="43388-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="43388-116">Установка Node.js</span><span class="sxs-lookup"><span data-stu-id="43388-116">Install Node.js</span></span>

<span data-ttu-id="43388-117">Установите Node.js на устройстве Raspberry Pi, если вы это еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="43388-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="43388-118">Hello IoT пакет SDK для Node.js требует 0.11.5 Node.js или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="43388-118">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="43388-119">Hello следующие шаги показывают, как tooinstall v6.10.2 Node.js на ваш Pi Raspberry:</span><span class="sxs-lookup"><span data-stu-id="43388-119">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="43388-120">Используйте hello следующая команда tooupdate вашей Pi Raspberry:</span><span class="sxs-lookup"><span data-stu-id="43388-120">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="43388-121">Используйте следующие двоичные файлы Node.js tooyour Raspberry Pi команда toodownload hello hello.</span><span class="sxs-lookup"><span data-stu-id="43388-121">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="43388-122">Используйте следующие двоичные файлы hello tooinstall команда hello.</span><span class="sxs-lookup"><span data-stu-id="43388-122">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="43388-123">Используйте hello следующая команда tooverify установки Node.js v6.10.2 успешно:</span><span class="sxs-lookup"><span data-stu-id="43388-123">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="43388-124">Клонирование репозиториев hello</span><span class="sxs-lookup"><span data-stu-id="43388-124">Clone hello repositories</span></span>

<span data-ttu-id="43388-125">Если это еще не сделано, клон hello требуемые hello репозиториев, выполнив следующие команды в конечном на ваш Pi:</span><span class="sxs-lookup"><span data-stu-id="43388-125">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="43388-126">Обновление строки подключения устройства hello</span><span class="sxs-lookup"><span data-stu-id="43388-126">Update hello device connection string</span></span>

<span data-ttu-id="43388-127">Привет открыть образец исходного файла в hello **nano** редактора с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43388-127">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="43388-128">Найдите строку hello:</span><span class="sxs-lookup"><span data-stu-id="43388-128">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="43388-129">Замените значения заполнителей hello и информации центр IoT был создан и сохранен в начале этого учебника hello hello устройства.</span><span class="sxs-lookup"><span data-stu-id="43388-129">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="43388-130">Сохранить изменения (**Ctrl-O**, **ввод**) и редактор hello выхода (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="43388-130">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="43388-131">Запуск образца hello</span><span class="sxs-lookup"><span data-stu-id="43388-131">Run hello sample</span></span>

<span data-ttu-id="43388-132">Выполнения hello следующими командами tooinstall hello пакеты необходимых компонентов для образца hello:</span><span class="sxs-lookup"><span data-stu-id="43388-132">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="43388-133">Теперь можно запустить образец hello программы для hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="43388-133">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="43388-134">Введите команду hello:</span><span class="sxs-lookup"><span data-stu-id="43388-134">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="43388-135">Hello следующий результат приводится пример hello выходные данные, отображаемые на hello Raspberry Pi hello командной строке:</span><span class="sxs-lookup"><span data-stu-id="43388-135">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Выходные данные приложения Raspberry Pi][img-raspberry-output]

<span data-ttu-id="43388-137">Нажмите клавишу **Ctrl-C** tooexit программа hello в любое время.</span><span class="sxs-lookup"><span data-stu-id="43388-137">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="43388-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="43388-138">Next steps</span></span>

<span data-ttu-id="43388-139">Посетите hello [Центр разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/) Дополнительные примеры и документация по Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="43388-139">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
