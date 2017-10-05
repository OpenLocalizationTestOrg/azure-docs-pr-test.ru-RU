---
title: "Подключение шлюза к Azure IoT Suite с помощью Intel NUC | Документация Майкрософт"
description: "Использование набора для создания коммерческого шлюза Интернета вещей (Майкрософт) и предварительно настроенного решения для удаленного мониторинга. Подключайтесь к решению для удаленного мониторинга, отправляйте смоделированные данные телеметрии в облако, а также реагируйте на методы, вызываемые на панели мониторинга этого решения, с помощью устройства SensorTag и шлюза Edge Интернета вещей Azure."
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
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: bda16be1094276fcecef1e708f9d7db307d94a89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="126a4-104">Подключение шлюза Edge Интернета вещей Azure к предварительно настроенному решению для удаленного мониторинга и отправка данных телеметрии из SensorTag</span><span class="sxs-lookup"><span data-stu-id="126a4-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="126a4-105">В этом руководстве показано, как отправлять данные температуры и влажности из устройства SensorTag предварительно настроенному решению для удаленного мониторинга с помощью шлюза Edge Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="126a4-105">This tutorial shows you how to use Azure IoT Edge to send temperature and humidity data from SensorTag device to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="126a4-106">SensorTag подключается к шлюзу Intel NUC с помощью Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="126a4-106">The SensorTag connects to the Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="126a4-107">В руководстве используются следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="126a4-107">The tutorial uses:</span></span>

- <span data-ttu-id="126a4-108">Azure IoT Edge для реализации примера шлюза.</span><span class="sxs-lookup"><span data-stu-id="126a4-108">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="126a4-109">Предварительно настроенное решение для удаленного мониторинга IoT Suite в качестве облачного сервера.</span><span class="sxs-lookup"><span data-stu-id="126a4-109">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="126a4-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="126a4-110">Overview</span></span>

<span data-ttu-id="126a4-111">В этом руководстве выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="126a4-111">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="126a4-112">Развертывание экземпляра предварительно настроенного решения удаленного мониторинга в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="126a4-112">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="126a4-113">На этом шаге автоматически разворачивается и настраивается несколько служб Azure.</span><span class="sxs-lookup"><span data-stu-id="126a4-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="126a4-114">Настройка устройства шлюза Intel NUC для взаимодействия с компьютером и решением для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="126a4-114">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="126a4-115">Настройка шлюза Intel NUC для получения данных телеметрии с устройства SensorTag и их отправки на панель удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="126a4-115">Set up your Intel NUC gateway to receive telemetry from a SensorTag device and send it to the remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="126a4-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="126a4-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="126a4-117">В этом руководстве данные телеметрии извлекаются с устройства SensorTag через Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="126a4-117">This tutorial retrieves telemetry data over Bluetooth from the SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="126a4-118">Решение для удаленного мониторинга подготавливает набор служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="126a4-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="126a4-119">Развертывание отражает реальную корпоративную архитектуру.</span><span class="sxs-lookup"><span data-stu-id="126a4-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="126a4-120">Чтобы избежать ненужных расходов на использование ресурсов Azure, удалите экземпляр предварительно настроенного решения на сайте azureiotsuite.com после завершения работы с ним.</span><span class="sxs-lookup"><span data-stu-id="126a4-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="126a4-121">Если предварительно настроенное решение понадобится снова, его можно легко восстановить.</span><span class="sxs-lookup"><span data-stu-id="126a4-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="126a4-122">Дополнительные сведения о сокращении затрат во время выполнения решения для удаленного мониторинга см. в статье [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Настройка предварительно настроенных решений Azure IoT Suite для демонстрационных целей).</span><span class="sxs-lookup"><span data-stu-id="126a4-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="126a4-123">Настройка подключения Bluetooth</span><span class="sxs-lookup"><span data-stu-id="126a4-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="126a4-124">Настройте Bluetooth на Intel NUC, чтобы включить устройство SensorTag для подключения и отправки данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="126a4-124">Configure Bluetooth on the Intel NUC to enable the SensorTag device to connect and send telemetry.</span></span>

### <a name="find-the-mac-address-of-the-sensortag"></a><span data-ttu-id="126a4-125">Поиск MAC-адреса устройства SensorTag</span><span class="sxs-lookup"><span data-stu-id="126a4-125">Find the MAC address of the SensorTag</span></span>

1. <span data-ttu-id="126a4-126">В оболочке Intel NUC выполните следующую команду, чтобы разблокировать службу Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="126a4-126">In the shell on the Intel NUC, run the following command to unblock the Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="126a4-127">Выполните следующие команды, чтобы запустить службу Bluetooth на Intel NUC и выполнить вход в оболочку Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="126a4-127">Run the following commands to start the Bluetooth service on the Intel NUC and enter the Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="126a4-128">Выполните следующую команду, чтобы включить контроллер Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="126a4-128">Run the following command to power on the Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="126a4-129">При включении контроллера появится сообщение **Changing power on succeeded** (Питание успешно включено).</span><span class="sxs-lookup"><span data-stu-id="126a4-129">When the controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="126a4-130">Выполните следующую команду для поиска находящихся поблизости устройств Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="126a4-130">Run the following command to scan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="126a4-131">Нажмите кнопку питания на устройстве SensorTag, чтобы его можно было обнаружить.</span><span class="sxs-lookup"><span data-stu-id="126a4-131">Press the power button on the SensorTag to make it discoverable.</span></span> <span data-ttu-id="126a4-132">Начнет мигать зеленый индикатор.</span><span class="sxs-lookup"><span data-stu-id="126a4-132">The green LED flashes.</span></span>

1. <span data-ttu-id="126a4-133">Когда в оболочке появится сообщение о том, что контроллер обнаружил SensorTag, запишите MAC-адрес устройства.</span><span class="sxs-lookup"><span data-stu-id="126a4-133">When you see a message in the shell that the controller has discovered the SensorTag, make a note of the MAC address of the device.</span></span> <span data-ttu-id="126a4-134">MAC-адрес выглядит примерно так: **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="126a4-134">The MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="126a4-135">Он понадобится вам позже в этом руководстве при настройке шлюза.</span><span class="sxs-lookup"><span data-stu-id="126a4-135">You need the MAC address later in the tutorial when you configure the gateway.</span></span>

1. <span data-ttu-id="126a4-136">Выполните следующую команду, чтобы отключить сканирование Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="126a4-136">Run the following command to turn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="126a4-137">Выполните следующую команду, чтобы убедиться, что вы можете подключиться к устройству SensorTag:</span><span class="sxs-lookup"><span data-stu-id="126a4-137">Run the following command to verify that you can connect to the SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="126a4-138">Если подключение выполнено успешно, в оболочке отобразится сообщение **Подключение успешно выполнено** и будут выведены сведения об устройстве SensorTag.</span><span class="sxs-lookup"><span data-stu-id="126a4-138">If you connect successfully, the shell shows the message **Connection successful** and prints information about the SensorTag device.</span></span> <span data-ttu-id="126a4-139">Если вы не можете подключиться, убедитесь, что устройство SensorTag включено.</span><span class="sxs-lookup"><span data-stu-id="126a4-139">If you cannot connect, check the SensorTag is still powered on.</span></span>

1. <span data-ttu-id="126a4-140">Теперь вы можете отключиться от SensorTag и выйти из оболочки Bluetooth, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="126a4-140">You can now disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="126a4-141">Создание пользовательского модуля Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="126a4-141">Build the custom IoT Edge module</span></span>

<span data-ttu-id="126a4-142">Теперь вы можете создать пользовательский модуль Edge Интернета вещей, который включает шлюз для отправки сообщений решению для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="126a4-142">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="126a4-143">Дополнительные сведения о настройке шлюза и модулей Edge Интернета вещей см. в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="126a4-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="126a4-144">Скачайте исходный код для модулей Edge Интернета вещей с GitHub с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="126a4-144">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="126a4-145">Создайте пользовательский модуль Edge Интернета вещей с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="126a4-145">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="126a4-146">Сценарий сборки помещает пользовательский модуль Edge Интернета вещей libsensor2remotemonitoring.so в папку со сборкой.</span><span class="sxs-lookup"><span data-stu-id="126a4-146">The build script places the libsensor2remotemonitoring.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="126a4-147">Настройка шлюза Edge Интернета вещей и его выполнение</span><span class="sxs-lookup"><span data-stu-id="126a4-147">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="126a4-148">Теперь вы можете настроить шлюз Edge Интернета вещей для отправки данных телеметрии с устройства SensorTag решению для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="126a4-148">You can now configure the IoT Edge gateway to send telemetry from your SensorTag device to your remote monitoring dashboard.</span></span> <span data-ttu-id="126a4-149">Дополнительные сведения о настройке шлюза и модулей Edge Интернета вещей см. в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="126a4-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="126a4-150">В этом руководстве используется стандартный текстовый редактор `vi` для Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="126a4-150">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="126a4-151">Если вы не использовали `vi` ранее, вам необходимо завершить вводное руководство, например [Unix — The vi Editor Tutorial][lnk-vi-tutorial] (Руководство по редактору vi в UNIX), для ознакомления с редактором.</span><span class="sxs-lookup"><span data-stu-id="126a4-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="126a4-152">Кроме того, с помощью команды `smart install nano -y` можно установить более удобный редактор [nano](https://www.nano-editor.org/).</span><span class="sxs-lookup"><span data-stu-id="126a4-152">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="126a4-153">Откройте пример файла конфигурации в редакторе **vi**, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="126a4-153">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="126a4-154">Найдите следующие строки в конфигурации для модуля Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="126a4-154">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="126a4-155">Замените значения заполнителей сведениями о Центре Интернета вещей, созданными и сохраненными в начале этого руководства.</span><span class="sxs-lookup"><span data-stu-id="126a4-155">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="126a4-156">Обычно для IoTHubName используется значение **yourrmsolution37e08**, а для IoTSuffix — **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="126a4-156">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="126a4-157">Найдите следующие строки в конфигурации для модуля сопоставления:</span><span class="sxs-lookup"><span data-stu-id="126a4-157">Locate the following lines in the configuration for the mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="126a4-158">Замените заполнитель **macAddress** MAC-адресом устройства SensorTag, записанным ранее.</span><span class="sxs-lookup"><span data-stu-id="126a4-158">Replace the **macAddress** placeholder with the MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="126a4-159">Замените заполнители **deviceID** и **deviceKey** идентификаторами и ключами двух устройств, созданными ранее для решения удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="126a4-159">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="126a4-160">Найдите следующие строки в конфигурации для модуля SensorTag:</span><span class="sxs-lookup"><span data-stu-id="126a4-160">Locate the following lines in the configuration for the SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="126a4-161">Замените заполнитель **device\_mac\_address** MAC-адресом устройства SensorTag, записанным ранее.</span><span class="sxs-lookup"><span data-stu-id="126a4-161">Replace the **device\_mac\_address** placeholder  with the MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="126a4-162">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="126a4-162">Save your changes.</span></span>

<span data-ttu-id="126a4-163">Теперь можно запускать шлюз с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="126a4-163">You can now run the gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="126a4-164">Шлюз Edge Интернета вещей запускается на Intel NUC и отправляет данные телеметрии из SensorTag решению для удаленного мониторинга:</span><span class="sxs-lookup"><span data-stu-id="126a4-164">The IoT Edge gateway starts on the Intel NUC and sends telemetry from the SensorTag to the remote monitoring solution:</span></span>

![Отправка данных телеметрии с SensorTag шлюзом Edge Интернета вещей][img-telemetry]

<span data-ttu-id="126a4-166">Вы можете в любое время нажать комбинацию клавиш **CTRL+C**, чтобы выйти из программы.</span><span class="sxs-lookup"><span data-stu-id="126a4-166">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="126a4-167">Просмотр телеметрии</span><span class="sxs-lookup"><span data-stu-id="126a4-167">View the telemetry</span></span>

<span data-ttu-id="126a4-168">Теперь шлюз отправляет данные телеметрии с устройства SensorTag решению для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="126a4-168">The gateway is now sending telemetry from the SensorTag device to the remote monitoring solution.</span></span> <span data-ttu-id="126a4-169">Эти данные можно просмотреть на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="126a4-169">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="126a4-170">Вы также можете отправлять команды на устройство SensorTag через шлюз с панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="126a4-170">You can also send commands to your SensorTag device through the gateway from the solution dashboard.</span></span>

- <span data-ttu-id="126a4-171">Перейдите к панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="126a4-171">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="126a4-172">В раскрывающемся списке **Device to View** (Устройство для просмотра) выберите настроенное в шлюзе устройство, которое представляет SensorTag.</span><span class="sxs-lookup"><span data-stu-id="126a4-172">Select the device you configured in the gateway that represents the SensorTag in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="126a4-173">Данные телеметрии с устройства SensorTag отобразятся на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="126a4-173">The telemetry from the SensorTag device displays on the dashboard.</span></span>

![Отображение телеметрии с устройства SensorTag][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="126a4-175">Если не завершить выполнение решения удаленного мониторинга в учетной записи Azure, вам будет выставлен счет.</span><span class="sxs-lookup"><span data-stu-id="126a4-175">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="126a4-176">Дополнительные сведения о сокращении затрат во время выполнения решения для удаленного мониторинга см. в статье [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Настройка предварительно настроенных решений Azure IoT Suite для демонстрационных целей).</span><span class="sxs-lookup"><span data-stu-id="126a4-176">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="126a4-177">Прекратив использовать предварительно настроенное решение, удалите его из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="126a4-177">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="126a4-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="126a4-178">Next steps</span></span>

<span data-ttu-id="126a4-179">Дополнительные примеры и документацию по Azure IoT можно найти в [Центре разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/).</span><span class="sxs-lookup"><span data-stu-id="126a4-179">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started