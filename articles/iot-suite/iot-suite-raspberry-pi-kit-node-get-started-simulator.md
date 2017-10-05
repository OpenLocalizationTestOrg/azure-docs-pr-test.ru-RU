---
title: "Подключение устройства Raspberry Pi с имитированными данными телеметрии к Azure IoT Suite с помощью Node.js | Документация Майкрософт"
description: "Используйте начальный набор Microsoft Azure IoT для Raspberry Pi 3, а также Azure IoT Suite. С помощью Node.js вы можете подключать устройства Raspberry Pi к решению для удаленного мониторинга, отправлять имитированные данные телеметрии в облако, а также реагировать на методы, вызываемые на панели мониторинга этого решения."
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
ms.openlocfilehash: 43fbfe2f2c5fb86e496c4419f9565365cf89830a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="0cae5-104">Подключение устройства Raspberry Pi 3 к решению для удаленного мониторинга и отправка имитированных данных телеметрии с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="0cae5-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="0cae5-105">В этом руководстве показано, как использовать Raspberry Pi 3 для моделирования данных температуры и влажности для отправки в облако.</span><span class="sxs-lookup"><span data-stu-id="0cae5-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="0cae5-106">В руководстве используются следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="0cae5-106">The tutorial uses:</span></span>

- <span data-ttu-id="0cae5-107">Операционная система Raspbian, язык программирования Node.js и пакет SDK Microsoft Azure IoT для Node.js для реализации примера устройства.</span><span class="sxs-lookup"><span data-stu-id="0cae5-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="0cae5-108">Предварительно настроенное решение для удаленного мониторинга IoT Suite в качестве облачного сервера.</span><span class="sxs-lookup"><span data-stu-id="0cae5-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="0cae5-109">Решение для удаленного мониторинга подготавливает набор служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="0cae5-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="0cae5-110">Развертывание отражает реальную корпоративную архитектуру.</span><span class="sxs-lookup"><span data-stu-id="0cae5-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="0cae5-111">Чтобы избежать ненужных расходов на использование ресурсов Azure, удалите экземпляр предварительно настроенного решения на сайте azureiotsuite.com после завершения работы с ним.</span><span class="sxs-lookup"><span data-stu-id="0cae5-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="0cae5-112">Если предварительно настроенное решение понадобится снова, его можно легко восстановить.</span><span class="sxs-lookup"><span data-stu-id="0cae5-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="0cae5-113">Дополнительные сведения о сокращении затрат во время выполнения решения для удаленного мониторинга см. в статье [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Настройка предварительно настроенных решений Azure IoT Suite для демонстрационных целей).</span><span class="sxs-lookup"><span data-stu-id="0cae5-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="0cae5-114">Скачивание и настройка примера</span><span class="sxs-lookup"><span data-stu-id="0cae5-114">Download and configure the sample</span></span>

<span data-ttu-id="0cae5-115">Теперь можно скачать и настроить клиентское приложение для удаленного мониторинга на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0cae5-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="0cae5-116">Установка Node.js</span><span class="sxs-lookup"><span data-stu-id="0cae5-116">Install Node.js</span></span>

<span data-ttu-id="0cae5-117">Установите Node.js на устройстве Raspberry Pi, если вы это еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="0cae5-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="0cae5-118">Для пакета SDK IoT для Node.js требуется версия Node.js 0.11.5 или более поздняя.</span><span class="sxs-lookup"><span data-stu-id="0cae5-118">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="0cae5-119">Ниже описывается установка Node.js версии 6.10.2 на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0cae5-119">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="0cae5-120">Чтобы обновить устройство Raspberry Pi, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0cae5-120">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="0cae5-121">Чтобы скачать двоичные файлы Node.js на устройство Raspberry Pi, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0cae5-121">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="0cae5-122">Чтобы установить эти двоичные файлы, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0cae5-122">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="0cae5-123">Чтобы убедиться в успешной установке Node.js версии 6.10.2, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0cae5-123">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="0cae5-124">Клонирование репозиториев</span><span class="sxs-lookup"><span data-stu-id="0cae5-124">Clone the repositories</span></span>

<span data-ttu-id="0cae5-125">Клонируйте необходимые репозитории (если вы еще не сделали это), выполнив следующие команды в терминале на устройстве Pi:</span><span class="sxs-lookup"><span data-stu-id="0cae5-125">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="0cae5-126">Обновление строки подключения устройства</span><span class="sxs-lookup"><span data-stu-id="0cae5-126">Update the device connection string</span></span>

<span data-ttu-id="0cae5-127">Откройте исходный файл примера в редакторе **nano**, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0cae5-127">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="0cae5-128">Найдите следующую строку:</span><span class="sxs-lookup"><span data-stu-id="0cae5-128">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="0cae5-129">Замените значения заполнителей сведениями об устройстве и Центре Интернета вещей, созданными и сохраненными в начале этого руководства.</span><span class="sxs-lookup"><span data-stu-id="0cae5-129">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="0cae5-130">Сохраните изменения (клавиши **CTRL+O**, **ВВОД**) и закройте редактор (клавиши **CTRL+X**).</span><span class="sxs-lookup"><span data-stu-id="0cae5-130">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="0cae5-131">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="0cae5-131">Run the sample</span></span>

<span data-ttu-id="0cae5-132">Чтобы установить пакеты необходимых компонентов для примера, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="0cae5-132">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="0cae5-133">Теперь вы можете запустить пример программы на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0cae5-133">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="0cae5-134">Введите команду:</span><span class="sxs-lookup"><span data-stu-id="0cae5-134">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="0cae5-135">Следующий пример с выходными данными отобразится в командной строке на устройстве Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0cae5-135">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Выходные данные приложения Raspberry Pi][img-raspberry-output]

<span data-ttu-id="0cae5-137">Вы можете в любое время нажать комбинацию клавиш **CTRL+C**, чтобы выйти из программы.</span><span class="sxs-lookup"><span data-stu-id="0cae5-137">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="0cae5-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0cae5-138">Next steps</span></span>

<span data-ttu-id="0cae5-139">Дополнительные примеры и документацию по Azure IoT можно найти в [Центре разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/).</span><span class="sxs-lookup"><span data-stu-id="0cae5-139">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
