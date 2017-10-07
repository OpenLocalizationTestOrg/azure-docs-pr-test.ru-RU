---
title: "обновляет IoT Suite, с помощью встроенного по toosupport C aaaConnect tooAzure Raspberry Pi | Документы Microsoft"
description: "Используйте hello Microsoft Azure IoT начального набора для hello Raspberry Pi 3 и Azure IoT Suite. Использовать C tooconnect вашей Raspberry Pi toohello удаленного решением для мониторинга, отправка данных телеметрии с датчиками toohello облака и обновления удаленного встроенного."
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
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="0c520-104">Подключение toohello вашей Raspberry Pi 3 удаленного решением для мониторинга и включить обновление удаленного встроенного по, с помощью C</span><span class="sxs-lookup"><span data-stu-id="0c520-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="0c520-105">В этом учебнике показано, как toouse hello Microsoft Azure IoT начального набора для 3 Raspberry Pi, чтобы:</span><span class="sxs-lookup"><span data-stu-id="0c520-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="0c520-106">Разработка температуры и влажности чтения, которая может обмениваться данными с облаком hello.</span><span class="sxs-lookup"><span data-stu-id="0c520-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="0c520-107">Включить и выполнять клиентское приложение hello tooupdate обновления удаленного встроенного по на hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0c520-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="0c520-108">Hello учебнике используется:</span><span class="sxs-lookup"><span data-stu-id="0c520-108">hello tutorial uses:</span></span>

* <span data-ttu-id="0c520-109">Raspbian ОС, язык программирования hello C и hello пакета SDK Microsoft Azure IoT для C tooimplement устройство образца.</span><span class="sxs-lookup"><span data-stu-id="0c520-109">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
* <span data-ttu-id="0c520-110">удаленный мониторинг Hello IoT Suite предварительно настроить решение в hello облачной серверной части.</span><span class="sxs-lookup"><span data-stu-id="0c520-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="0c520-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="0c520-111">Overview</span></span>

<span data-ttu-id="0c520-112">В этом учебнике необходимо выполнить следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="0c520-112">In this tutorial, you complete hello following steps:</span></span>

* <span data-ttu-id="0c520-113">Разверните экземпляр hello удаленного мониторинга предварительно настроенных решений tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="0c520-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="0c520-114">На этом шаге автоматически разворачивается и настраивается несколько служб Azure.</span><span class="sxs-lookup"><span data-stu-id="0c520-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="0c520-115">Настройка вашего устройства и датчики toocommunicate на компьютер и hello удаленного решением для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="0c520-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
* <span data-ttu-id="0c520-116">Обновите hello образец кода tooconnect toohello удаленного мониторинга устройствами и отправлять данные телеметрии, можно просмотреть на панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="0c520-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
* <span data-ttu-id="0c520-117">Используйте hello образец кода устройства tooupdate hello клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="0c520-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="0c520-118">Hello удаленного мониторинга решения подготавливает набор служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="0c520-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="0c520-119">Развертывание Hello отражает реальные корпоративной архитектуре.</span><span class="sxs-lookup"><span data-stu-id="0c520-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="0c520-120">плата tooavoid ненужные использование Azure, удаление экземпляра hello предварительно настроенное решение в azureiotsuite.com после завершения с ним.</span><span class="sxs-lookup"><span data-stu-id="0c520-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="0c520-121">Если предварительно настроенных решений требуется hello еще раз, то ее можно легко восстановить.</span><span class="sxs-lookup"><span data-stu-id="0c520-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="0c520-122">Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="0c520-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="0c520-123">Загрузить и настроить образец hello</span><span class="sxs-lookup"><span data-stu-id="0c520-123">Download and configure hello sample</span></span>

<span data-ttu-id="0c520-124">Теперь можно загрузить и настроить hello удаленного мониторинга клиентского приложения на ваш Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0c520-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="0c520-125">Клонирование репозиториев hello</span><span class="sxs-lookup"><span data-stu-id="0c520-125">Clone hello repositories</span></span>

<span data-ttu-id="0c520-126">Если вы еще не сделали этого, клон hello необходимые hello репозиториев, выполнив следующие команды на ваш Pi:</span><span class="sxs-lookup"><span data-stu-id="0c520-126">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="0c520-127">Обновление строки подключения устройства hello</span><span class="sxs-lookup"><span data-stu-id="0c520-127">Update hello device connection string</span></span>

<span data-ttu-id="0c520-128">Привет открыть образец файла конфигурации в hello **nano** редактора с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0c520-128">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="0c520-129">Замените значения заполнителей hello hello идентификатор и центр IoT сведений об устройстве был создан и сохранен в начале этого учебника hello.</span><span class="sxs-lookup"><span data-stu-id="0c520-129">Replace hello placeholder values with hello device ID and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="0c520-130">Когда вы закончите, hello содержимое файла deviceinfo hello должен выглядеть hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="0c520-130">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="0c520-131">Сохранить изменения (**Ctrl-O**, **ввод**) и редактор hello выхода (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="0c520-131">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="0c520-132">Построение образца hello</span><span class="sxs-lookup"><span data-stu-id="0c520-132">Build hello sample</span></span>

<span data-ttu-id="0c520-133">Если вы еще не сделали установите hello пакеты необходимых компонентов для hello IoT устройство Microsoft Azure SDK для C, выполнив следующие команды в конечном на hello Raspberry Pi hello:</span><span class="sxs-lookup"><span data-stu-id="0c520-133">If you have not already done so, install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="0c520-134">Теперь можно построить образец решения hello на hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0c520-134">You can now build hello sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="0c520-135">Теперь можно запустить образец hello программы для hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0c520-135">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="0c520-136">Введите команду hello:</span><span class="sxs-lookup"><span data-stu-id="0c520-136">Enter hello command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="0c520-137">Hello следующий результат приводится пример hello выходные данные, отображаемые на hello Raspberry Pi hello командной строке:</span><span class="sxs-lookup"><span data-stu-id="0c520-137">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Выходные данные приложения Raspberry Pi][img-raspberry-output]

<span data-ttu-id="0c520-139">Нажмите клавишу **Ctrl-C** tooexit программа hello в любое время.</span><span class="sxs-lookup"><span data-stu-id="0c520-139">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="0c520-140">В панели мониторинга hello решение, нажмите кнопку **устройств** toovisit hello **устройств** страницы.</span><span class="sxs-lookup"><span data-stu-id="0c520-140">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="0c520-141">Выберите ваш Pi Raspberry в hello **список устройств**.</span><span class="sxs-lookup"><span data-stu-id="0c520-141">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="0c520-142">Затем выберите **Методы**:</span><span class="sxs-lookup"><span data-stu-id="0c520-142">Then choose **Methods**:</span></span>

    ![Список устройств на панели мониторинга][img-list-devices]

1. <span data-ttu-id="0c520-144">На hello **вызвать метод** выберите **InitiateFirmwareUpdate** в hello **метод** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="0c520-144">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="0c520-145">В hello **FWPackageURI** введите **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="0c520-145">In hello **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="0c520-146">Этот архив содержит реализацию hello версии 2.0 hello встроенного по.</span><span class="sxs-lookup"><span data-stu-id="0c520-146">This archive file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="0c520-147">Выберите **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="0c520-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="0c520-148">приложение Hello на hello Raspberry Pi отправляет подтверждение задней toohello решений мониторинга.</span><span class="sxs-lookup"><span data-stu-id="0c520-148">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="0c520-149">Затем она запускает процесс обновления встроенного по hello путем загрузки новой версии встроенного по hello hello:</span><span class="sxs-lookup"><span data-stu-id="0c520-149">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Просмотр журнала методов][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="0c520-151">Контролировать процесс обновления встроенного по hello</span><span class="sxs-lookup"><span data-stu-id="0c520-151">Observe hello firmware update process</span></span>

<span data-ttu-id="0c520-152">Можно наблюдать hello процесс обновления встроенного по, во время их выполнения на устройстве hello и просмотрев hello сообщил свойств в панели мониторинга hello решения:</span><span class="sxs-lookup"><span data-stu-id="0c520-152">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="0c520-153">Можно просмотреть ход выполнения hello в процесс обновления hello на hello Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0c520-153">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Отображение хода выполнения обновления][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="0c520-155">удаленного мониторинга приложение Hello автоматически перезагружается после завершения обновления hello.</span><span class="sxs-lookup"><span data-stu-id="0c520-155">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="0c520-156">Команда hello `ps -ef` tooverify его выполнения.</span><span class="sxs-lookup"><span data-stu-id="0c520-156">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="0c520-157">Процесс tooterminate hello, используйте hello `kill` команду с идентификатором hello.</span><span class="sxs-lookup"><span data-stu-id="0c520-157">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="0c520-158">Состояние hello hello обновление встроенного по, можно просмотреть, сообщаемые hello устройства, на портале решения hello.</span><span class="sxs-lookup"><span data-stu-id="0c520-158">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="0c520-159">Hello следующем снимке экрана показано состояние hello и длительность каждого этапа процесса обновления hello и hello новой версии встроенного по:</span><span class="sxs-lookup"><span data-stu-id="0c520-159">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![Отображение состояния задания][img-job-status]

    <span data-ttu-id="0c520-161">При переходе назад toohello панели мониторинга можно убедитесь, что устройство hello продолжает посылать телеметрии следующее обновление встроенного по hello.</span><span class="sxs-lookup"><span data-stu-id="0c520-161">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="0c520-162">Если оставить hello удаленное наблюдение решение, работающее в учетной записи Azure, взимается плата за hello выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="0c520-162">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="0c520-163">Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="0c520-163">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="0c520-164">Удаление hello предварительно настроенное решение из учетной записи Azure, после завершения его использования.</span><span class="sxs-lookup"><span data-stu-id="0c520-164">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c520-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0c520-165">Next steps</span></span>

<span data-ttu-id="0c520-166">Посетите hello [Центр разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/) Дополнительные примеры и документация по Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="0c520-166">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md