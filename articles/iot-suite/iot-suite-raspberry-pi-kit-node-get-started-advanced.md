---
title: "Подключение устройства Raspberry Pi к Azure IoT Suite с помощью Node.js для поддержки обновлений встроенного ПО | Документация Майкрософт"
description: "Используйте начальный набор Microsoft Azure IoT для Raspberry Pi 3, а также Azure IoT Suite. Используйте Node.js для подключения устройства Raspberry Pi к решению для удаленного мониторинга, отправляйте данные телеметрии с датчиков в облако, а также выполняйте удаленное обновление встроенного ПО."
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
ms.openlocfilehash: 54503d5d6a636239d240509d7d09cf334234bac7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="7e303-104">Подключение устройства Raspberry Pi 3 к решению для удаленного мониторинга и включение удаленных обновлений встроенного ПО с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="7e303-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="7e303-105">В этом руководстве показано, как можно получить следующие возможности, используя начальный набор Интернета вещей Microsoft Azure для Raspberry Pi 3:</span><span class="sxs-lookup"><span data-stu-id="7e303-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="7e303-106">Разработка средства чтения данных о температуре и влажности, которое может взаимодействовать с облаком.</span><span class="sxs-lookup"><span data-stu-id="7e303-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="7e303-107">Включение и выполнение удаленного обновления встроенного ПО для обновления клиентского приложения на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7e303-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="7e303-108">В руководстве используются следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="7e303-108">The tutorial uses:</span></span>

- <span data-ttu-id="7e303-109">Операционная система Raspbian, язык программирования Node.js и пакет SDK Microsoft Azure IoT для Node.js для реализации примера устройства.</span><span class="sxs-lookup"><span data-stu-id="7e303-109">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="7e303-110">Предварительно настроенное решение для удаленного мониторинга IoT Suite в качестве облачного сервера.</span><span class="sxs-lookup"><span data-stu-id="7e303-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="7e303-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="7e303-111">Overview</span></span>

<span data-ttu-id="7e303-112">В этом руководстве выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7e303-112">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="7e303-113">Развертывание экземпляра предварительно настроенного решения удаленного мониторинга в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="7e303-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="7e303-114">На этом шаге автоматически разворачивается и настраивается несколько служб Azure.</span><span class="sxs-lookup"><span data-stu-id="7e303-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="7e303-115">Настройка устройства и датчиков для взаимодействия с компьютером и решением для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="7e303-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="7e303-116">Обновление кода примера устройства для подключения к решению для удаленного мониторинга и отправка данных телеметрии, которые можно просмотреть на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="7e303-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
- <span data-ttu-id="7e303-117">Обновление клиентского приложения с помощью примера кода устройства.</span><span class="sxs-lookup"><span data-stu-id="7e303-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="7e303-118">Решение для удаленного мониторинга подготавливает набор служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="7e303-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="7e303-119">Развертывание отражает реальную корпоративную архитектуру.</span><span class="sxs-lookup"><span data-stu-id="7e303-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="7e303-120">Чтобы избежать ненужных расходов на использование ресурсов Azure, удалите экземпляр предварительно настроенного решения на сайте azureiotsuite.com после завершения работы с ним.</span><span class="sxs-lookup"><span data-stu-id="7e303-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="7e303-121">Если предварительно настроенное решение понадобится снова, его можно легко восстановить.</span><span class="sxs-lookup"><span data-stu-id="7e303-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="7e303-122">Дополнительные сведения о сокращении затрат во время выполнения решения для удаленного мониторинга см. в статье [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Настройка предварительно настроенных решений Azure IoT Suite для демонстрационных целей).</span><span class="sxs-lookup"><span data-stu-id="7e303-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="7e303-123">Скачивание и настройка примера</span><span class="sxs-lookup"><span data-stu-id="7e303-123">Download and configure the sample</span></span>

<span data-ttu-id="7e303-124">Теперь можно скачать и настроить клиентское приложение для удаленного мониторинга на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7e303-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="7e303-125">Установка Node.js</span><span class="sxs-lookup"><span data-stu-id="7e303-125">Install Node.js</span></span>

<span data-ttu-id="7e303-126">Установите Node.js на устройстве Raspberry Pi, если вы это еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="7e303-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="7e303-127">Для пакета SDK IoT для Node.js требуется версия Node.js 0.11.5 или более поздняя.</span><span class="sxs-lookup"><span data-stu-id="7e303-127">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="7e303-128">Ниже описывается установка Node.js версии 6.10.2 на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7e303-128">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="7e303-129">Чтобы обновить устройство Raspberry Pi, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7e303-129">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="7e303-130">Чтобы скачать двоичные файлы Node.js на устройство Raspberry Pi, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7e303-130">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="7e303-131">Чтобы установить эти двоичные файлы, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7e303-131">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="7e303-132">Чтобы убедиться в успешной установке Node.js версии 6.10.2, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7e303-132">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="7e303-133">Клонирование репозиториев</span><span class="sxs-lookup"><span data-stu-id="7e303-133">Clone the repositories</span></span>

<span data-ttu-id="7e303-134">Клонируйте необходимые репозитории (если вы еще не сделали этого), выполнив следующие команды на устройстве Pi:</span><span class="sxs-lookup"><span data-stu-id="7e303-134">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="7e303-135">Обновление строки подключения устройства</span><span class="sxs-lookup"><span data-stu-id="7e303-135">Update the device connection string</span></span>

<span data-ttu-id="7e303-136">Откройте пример файла конфигурации в редакторе **nano**, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7e303-136">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="7e303-137">Замените значения заполнителей идентификатором устройства и сведениями о Центре Интернета вещей, созданном и сохраненном в начале этого руководства.</span><span class="sxs-lookup"><span data-stu-id="7e303-137">Replace the placeholder values with the device id and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="7e303-138">По завершении содержимое файла deviceinfo должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7e303-138">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="7e303-139">Сохраните изменения (клавиши **CTRL+O**, **ВВОД**) и закройте редактор (клавиши **CTRL+X**).</span><span class="sxs-lookup"><span data-stu-id="7e303-139">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="7e303-140">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="7e303-140">Run the sample</span></span>

<span data-ttu-id="7e303-141">Чтобы установить пакеты необходимых компонентов для примера, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="7e303-141">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="7e303-142">Теперь вы можете запустить пример программы на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7e303-142">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="7e303-143">Введите команду:</span><span class="sxs-lookup"><span data-stu-id="7e303-143">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="7e303-144">Следующий пример с выходными данными отобразится в командной строке на устройстве Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="7e303-144">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Выходные данные приложения Raspberry Pi][img-raspberry-output]

<span data-ttu-id="7e303-146">Вы можете в любое время нажать комбинацию клавиш **CTRL+C**, чтобы выйти из программы.</span><span class="sxs-lookup"><span data-stu-id="7e303-146">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="7e303-147">На панели мониторинга решения щелкните **Устройства**, чтобы перейти на страницу **устройств**.</span><span class="sxs-lookup"><span data-stu-id="7e303-147">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="7e303-148">Выберите Raspberry Pi в **списке устройств**.</span><span class="sxs-lookup"><span data-stu-id="7e303-148">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="7e303-149">Затем выберите **Методы**:</span><span class="sxs-lookup"><span data-stu-id="7e303-149">Then choose **Methods**:</span></span>

    ![Список устройств на панели мониторинга][img-list-devices]

1. <span data-ttu-id="7e303-151">На странице **Вызвать метод** в раскрывающемся списке **методов** выберите **InitiateFirmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="7e303-151">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="7e303-152">В поле **FWPackageURI** введите **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="7e303-152">In the **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="7e303-153">Этот файл содержит реализацию встроенного ПО версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="7e303-153">This file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="7e303-154">Выберите **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="7e303-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="7e303-155">Приложение на устройстве Raspberry Pi отправляет подтверждение обратно на панель мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="7e303-155">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="7e303-156">Затем запускается процесс обновления встроенного ПО путем скачивания новой версии встроенного ПО:</span><span class="sxs-lookup"><span data-stu-id="7e303-156">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Просмотр журнала методов][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="7e303-158">Просмотр процесса обновления встроенного ПО</span><span class="sxs-lookup"><span data-stu-id="7e303-158">Observe the firmware update process</span></span>

<span data-ttu-id="7e303-159">Вы можете наблюдать за выполнением процесса обновления встроенного ПО на устройстве и просматривая сообщенные свойства на панели мониторинга решения:</span><span class="sxs-lookup"><span data-stu-id="7e303-159">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="7e303-160">Ход выполнения процесса обновления можно просмотреть на устройстве Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="7e303-160">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Отображение хода выполнения обновления][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="7e303-162">После обновления приложение для удаленного мониторинга автоматически перезапускается.</span><span class="sxs-lookup"><span data-stu-id="7e303-162">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="7e303-163">Используйте команду `ps -ef`, чтобы проверить, выполняется ли процесс.</span><span class="sxs-lookup"><span data-stu-id="7e303-163">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="7e303-164">Если вы хотите завершить процесс, используйте команду `kill` с идентификатором процесса.</span><span class="sxs-lookup"><span data-stu-id="7e303-164">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="7e303-165">Данные о состоянии обновления встроенного ПО, сообщаемые устройством, можно просмотреть на портале решения.</span><span class="sxs-lookup"><span data-stu-id="7e303-165">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="7e303-166">На следующем снимке экрана показаны сведения о состоянии и продолжительности каждого этапа процесса обновления, а также сведения о новой версии встроенного ПО:</span><span class="sxs-lookup"><span data-stu-id="7e303-166">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![Отображение состояния задания][img-job-status]

    <span data-ttu-id="7e303-168">При переходе к панели мониторинга можно проверить, отправляет ли устройство данные телеметрии после обновления встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="7e303-168">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="7e303-169">Если не завершить выполнение решения удаленного мониторинга в учетной записи Azure, вам будет выставлен счет.</span><span class="sxs-lookup"><span data-stu-id="7e303-169">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="7e303-170">Дополнительные сведения о сокращении затрат во время выполнения решения для удаленного мониторинга см. в статье [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Настройка предварительно настроенных решений Azure IoT Suite для демонстрационных целей).</span><span class="sxs-lookup"><span data-stu-id="7e303-170">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="7e303-171">Прекратив использовать предварительно настроенное решение, удалите его из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="7e303-171">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e303-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7e303-172">Next steps</span></span>

<span data-ttu-id="7e303-173">Дополнительные примеры и документацию по Azure IoT можно найти в [Центре разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/).</span><span class="sxs-lookup"><span data-stu-id="7e303-173">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
