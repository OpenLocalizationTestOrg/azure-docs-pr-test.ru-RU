---
title: "aaaConnect tooAzure Raspberry Pi IoT Suite с помощью C с реальными датчики | Документы Microsoft"
description: "Используйте hello Microsoft Azure IoT начального набора для hello Raspberry Pi 3 и Azure IoT Suite. Использовать C tooconnect вашей Raspberry Pi toohello удаленного решением для мониторинга, отправка данных телеметрии с датчиками toohello облака и отвечать toomethods из панели мониторинга hello решения."
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
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="edabe-104">Подключения вашей Raspberry Pi 3 toohello удаленного решением для мониторинга и отправка данных телеметрии с реальными датчика с помощью C</span><span class="sxs-lookup"><span data-stu-id="edabe-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="edabe-105">Этот учебник показывает, как toouse hello Microsoft Azure IoT начального набора для toodevelop Raspberry Pi 3 температуры и влажности чтения, которая может обмениваться данными с облаком hello.</span><span class="sxs-lookup"><span data-stu-id="edabe-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="edabe-106">Hello учебнике используется:</span><span class="sxs-lookup"><span data-stu-id="edabe-106">hello tutorial uses:</span></span>

- <span data-ttu-id="edabe-107">Raspbian ОС, язык программирования hello C и hello пакета SDK Microsoft Azure IoT для C tooimplement устройство образца.</span><span class="sxs-lookup"><span data-stu-id="edabe-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="edabe-108">удаленный мониторинг Hello IoT Suite предварительно настроить решение в hello облачной серверной части.</span><span class="sxs-lookup"><span data-stu-id="edabe-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="edabe-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="edabe-109">Overview</span></span>

<span data-ttu-id="edabe-110">В этом учебнике необходимо выполнить следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="edabe-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="edabe-111">Разверните экземпляр hello удаленного мониторинга предварительно настроенных решений tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="edabe-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="edabe-112">На этом шаге автоматически разворачивается и настраивается несколько служб Azure.</span><span class="sxs-lookup"><span data-stu-id="edabe-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="edabe-113">Настройка вашего устройства и датчики toocommunicate на компьютер и hello удаленного решением для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="edabe-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="edabe-114">Обновите hello образец кода tooconnect toohello удаленного мониторинга устройствами и отправлять данные телеметрии, можно просмотреть на панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="edabe-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="edabe-115">Hello удаленного мониторинга решения подготавливает набор служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="edabe-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="edabe-116">Развертывание Hello отражает реальные корпоративной архитектуре.</span><span class="sxs-lookup"><span data-stu-id="edabe-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="edabe-117">плата tooavoid ненужные использование Azure, удаление экземпляра hello предварительно настроенное решение в azureiotsuite.com после завершения с ним.</span><span class="sxs-lookup"><span data-stu-id="edabe-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="edabe-118">Если предварительно настроенных решений требуется hello еще раз, то ее можно легко восстановить.</span><span class="sxs-lookup"><span data-stu-id="edabe-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="edabe-119">Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="edabe-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="edabe-120">Загрузить и настроить образец hello</span><span class="sxs-lookup"><span data-stu-id="edabe-120">Download and configure hello sample</span></span>

<span data-ttu-id="edabe-121">Теперь можно загрузить и настроить hello удаленного мониторинга клиентского приложения на ваш Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="edabe-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="edabe-122">Клонирование репозиториев hello</span><span class="sxs-lookup"><span data-stu-id="edabe-122">Clone hello repositories</span></span>

<span data-ttu-id="edabe-123">Если это еще не сделано, клон hello требуемые hello репозиториев, выполнив следующие команды в конечном на ваш Pi:</span><span class="sxs-lookup"><span data-stu-id="edabe-123">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="edabe-124">Обновление строки подключения устройства hello</span><span class="sxs-lookup"><span data-stu-id="edabe-124">Update hello device connection string</span></span>

<span data-ttu-id="edabe-125">Привет открыть образец исходного файла в hello **nano** редактора с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="edabe-125">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="edabe-126">Найдите hello следующие строки:</span><span class="sxs-lookup"><span data-stu-id="edabe-126">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="edabe-127">Замените значения заполнителей hello и информации центр IoT был создан и сохранен в начале этого учебника hello hello устройства.</span><span class="sxs-lookup"><span data-stu-id="edabe-127">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="edabe-128">Сохранить изменения (**Ctrl-O**, **ввод**) и редактор hello выхода (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="edabe-128">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="edabe-129">Построение образца hello</span><span class="sxs-lookup"><span data-stu-id="edabe-129">Build hello sample</span></span>

<span data-ttu-id="edabe-130">Установите hello пакеты необходимых компонентов для hello IoT устройство Microsoft Azure SDK для C, выполнив следующие команды в конечном на hello Raspberry Pi hello:</span><span class="sxs-lookup"><span data-stu-id="edabe-130">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="edabe-131">Теперь можно построить образец hello обновление решения на hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="edabe-131">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="edabe-132">Теперь можно запустить образец hello программы для hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="edabe-132">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="edabe-133">Введите команду hello:</span><span class="sxs-lookup"><span data-stu-id="edabe-133">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="edabe-134">Hello следующий результат приводится пример hello выходные данные, отображаемые на hello Raspberry Pi hello командной строке:</span><span class="sxs-lookup"><span data-stu-id="edabe-134">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Выходные данные приложения Raspberry Pi][img-raspberry-output]

<span data-ttu-id="edabe-136">Нажмите клавишу **Ctrl-C** tooexit программа hello в любое время.</span><span class="sxs-lookup"><span data-stu-id="edabe-136">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="edabe-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="edabe-137">Next steps</span></span>

<span data-ttu-id="edabe-138">Посетите hello [Центр разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/) Дополнительные примеры и документация по Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="edabe-138">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
