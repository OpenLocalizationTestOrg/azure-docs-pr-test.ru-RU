---
title: "Подключение устройства Raspberry Pi со смоделированными данными телеметрии к Azure IoT Suite с помощью C | Документация Майкрософт"
description: "Используйте начальный набор Microsoft Azure IoT для Raspberry Pi 3, а также Azure IoT Suite. С помощью C вы можете подключать устройства Raspberry Pi к решению для удаленного мониторинга, отправлять смоделированные данные телеметрии в облако, а также реагировать на методы, вызываемые на панели мониторинга этого решения."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 43b82e5fb6a309283979f23d8c87af600595bc55
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="4d77a-104">Подключение устройства Raspberry Pi 3 к решению для удаленного мониторинга и отправка смоделированных данных телеметрии с помощью C</span><span class="sxs-lookup"><span data-stu-id="4d77a-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="4d77a-105">В этом руководстве показано, как использовать Raspberry Pi 3 для моделирования данных температуры и влажности для отправки в облако.</span><span class="sxs-lookup"><span data-stu-id="4d77a-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="4d77a-106">В руководстве используются следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="4d77a-106">The tutorial uses:</span></span>

- <span data-ttu-id="4d77a-107">ОС Raspbian, язык программирования C и пакет SDK для Microsoft Azure IoT для C для реализации примера устройства.</span><span class="sxs-lookup"><span data-stu-id="4d77a-107">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
- <span data-ttu-id="4d77a-108">Предварительно настроенное решение для удаленного мониторинга IoT Suite в качестве облачного сервера.</span><span class="sxs-lookup"><span data-stu-id="4d77a-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="4d77a-109">Решение для удаленного мониторинга подготавливает набор служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="4d77a-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="4d77a-110">Развертывание отражает реальную корпоративную архитектуру.</span><span class="sxs-lookup"><span data-stu-id="4d77a-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="4d77a-111">Чтобы избежать ненужных расходов на использование ресурсов Azure, удалите экземпляр предварительно настроенного решения на сайте azureiotsuite.com после завершения работы с ним.</span><span class="sxs-lookup"><span data-stu-id="4d77a-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="4d77a-112">Если предварительно настроенное решение понадобится снова, его можно легко восстановить.</span><span class="sxs-lookup"><span data-stu-id="4d77a-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="4d77a-113">Дополнительные сведения о сокращении затрат во время выполнения решения для удаленного мониторинга см. в статье [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Настройка предварительно настроенных решений Azure IoT Suite для демонстрационных целей).</span><span class="sxs-lookup"><span data-stu-id="4d77a-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="4d77a-114">Скачивание и настройка примера</span><span class="sxs-lookup"><span data-stu-id="4d77a-114">Download and configure the sample</span></span>

<span data-ttu-id="4d77a-115">Теперь можно скачать и настроить клиентское приложение для удаленного мониторинга на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4d77a-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="4d77a-116">Клонирование репозиториев</span><span class="sxs-lookup"><span data-stu-id="4d77a-116">Clone the repositories</span></span>

<span data-ttu-id="4d77a-117">Клонируйте необходимые репозитории (если вы еще не сделали это), выполнив следующие команды в терминале на устройстве Pi:</span><span class="sxs-lookup"><span data-stu-id="4d77a-117">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="4d77a-118">Обновление строки подключения устройства</span><span class="sxs-lookup"><span data-stu-id="4d77a-118">Update the device connection string</span></span>

<span data-ttu-id="4d77a-119">Откройте исходный файл примера в редакторе **nano**, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4d77a-119">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="4d77a-120">Найдите следующие строки:</span><span class="sxs-lookup"><span data-stu-id="4d77a-120">Locate the following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="4d77a-121">Замените значения заполнителей сведениями об устройстве и Центре Интернета вещей, созданными и сохраненными в начале этого руководства.</span><span class="sxs-lookup"><span data-stu-id="4d77a-121">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="4d77a-122">Сохраните изменения (клавиши **CTRL+O**, **ВВОД**) и закройте редактор (клавиши **CTRL+X**).</span><span class="sxs-lookup"><span data-stu-id="4d77a-122">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="4d77a-123">Сборка примера</span><span class="sxs-lookup"><span data-stu-id="4d77a-123">Build the sample</span></span>

<span data-ttu-id="4d77a-124">Установите пакеты необходимых компонентов пакет SDK для устройств Microsoft Azure IoT для C, выполнив следующие команды в окне терминала на устройстве Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="4d77a-124">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="4d77a-125">Теперь вы можете выполнить сборку обновленного примера решения на устройстве Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="4d77a-125">You can now build the updated sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="4d77a-126">Теперь вы можете запустить пример программы на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4d77a-126">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="4d77a-127">Введите команду:</span><span class="sxs-lookup"><span data-stu-id="4d77a-127">Enter the command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="4d77a-128">Следующий пример с выходными данными отобразится в командной строке на устройстве Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="4d77a-128">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Выходные данные приложения Raspberry Pi][img-raspberry-output]

<span data-ttu-id="4d77a-130">Вы можете в любое время нажать комбинацию клавиш **CTRL+C**, чтобы выйти из программы.</span><span class="sxs-lookup"><span data-stu-id="4d77a-130">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="4d77a-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d77a-131">Next steps</span></span>

<span data-ttu-id="4d77a-132">Дополнительные примеры и документацию по Azure IoT можно найти в [Центре разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/).</span><span class="sxs-lookup"><span data-stu-id="4d77a-132">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
