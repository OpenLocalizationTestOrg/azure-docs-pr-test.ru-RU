---
title: "aaaConnect шлюза tooAzure IoT Suite, с помощью NUC Intel | Документы Microsoft"
description: "Используйте hello IoT коммерческих шлюза пакета и hello удаленного мониторинга предварительно настроенных решение. Используйте hello Azure IoT пограничного шлюза tooenable tooconnect SensorTag устройства, toohello удаленного решением для мониторинга, отправки телеметрии toohello облака и отвечать toomethods из панели мониторинга hello решения."
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
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="6af07-104">Подключения вашей Azure IoT пограничного шлюза toohello удаленное наблюдение предварительно настроенных решений и отправки данных телеметрии из SensorTag</span><span class="sxs-lookup"><span data-stu-id="6af07-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="6af07-105">Этот учебник показывает, как toouse Azure IoT Edge toosend температуры и влажности данные из удаленного мониторинга SensorTag устройств toohello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="6af07-105">This tutorial shows you how toouse Azure IoT Edge toosend temperature and humidity data from SensorTag device toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="6af07-106">Hello SensorTag подключается toohello Intel NUC шлюза с помощью Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="6af07-106">hello SensorTag connects toohello Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="6af07-107">Hello учебнике используется:</span><span class="sxs-lookup"><span data-stu-id="6af07-107">hello tutorial uses:</span></span>

- <span data-ttu-id="6af07-108">Azure IoT Edge tooimplement пример шлюза.</span><span class="sxs-lookup"><span data-stu-id="6af07-108">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="6af07-109">удаленный мониторинг Hello IoT Suite предварительно настроить решение в hello облачной серверной части.</span><span class="sxs-lookup"><span data-stu-id="6af07-109">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="6af07-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="6af07-110">Overview</span></span>

<span data-ttu-id="6af07-111">В этом учебнике необходимо выполнить следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="6af07-111">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="6af07-112">Разверните экземпляр hello удаленного мониторинга предварительно настроенных решений tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="6af07-112">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="6af07-113">На этом шаге автоматически разворачивается и настраивается несколько служб Azure.</span><span class="sxs-lookup"><span data-stu-id="6af07-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="6af07-114">Настройка toocommunicate устройства шлюза вашей Intel NUC, с компьютера и решение для удаленного мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="6af07-114">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="6af07-115">Настройка шлюза tooreceive Intel NUC телеметрии из устройства SensorTag и отправьте ее toohello удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="6af07-115">Set up your Intel NUC gateway tooreceive telemetry from a SensorTag device and send it toohello remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="6af07-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="6af07-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="6af07-117">Этот учебник извлекает данные телеметрии через Bluetooth устройства SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="6af07-117">This tutorial retrieves telemetry data over Bluetooth from hello SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="6af07-118">Hello удаленного мониторинга решения подготавливает набор служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="6af07-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="6af07-119">Развертывание Hello отражает реальные корпоративной архитектуре.</span><span class="sxs-lookup"><span data-stu-id="6af07-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="6af07-120">плата tooavoid ненужные использование Azure, удаление экземпляра hello предварительно настроенное решение в azureiotsuite.com после завершения с ним.</span><span class="sxs-lookup"><span data-stu-id="6af07-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="6af07-121">Если предварительно настроенных решений требуется hello еще раз, то ее можно легко восстановить.</span><span class="sxs-lookup"><span data-stu-id="6af07-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="6af07-122">Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="6af07-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="6af07-123">Настройка подключения Bluetooth</span><span class="sxs-lookup"><span data-stu-id="6af07-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="6af07-124">Настроить Bluetooth на устройстве hello Intel NUC tooenable hello SensorTag tooconnect и отправка данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="6af07-124">Configure Bluetooth on hello Intel NUC tooenable hello SensorTag device tooconnect and send telemetry.</span></span>

### <a name="find-hello-mac-address-of-hello-sensortag"></a><span data-ttu-id="6af07-125">Найти hello MAC-адрес hello SensorTag</span><span class="sxs-lookup"><span data-stu-id="6af07-125">Find hello MAC address of hello SensorTag</span></span>

1. <span data-ttu-id="6af07-126">В оболочке hello на hello Intel NUC выполните hello, следующая команда toounblock hello Bluetooth службы:</span><span class="sxs-lookup"><span data-stu-id="6af07-126">In hello shell on hello Intel NUC, run hello following command toounblock hello Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="6af07-127">Ниже hello выполнения команды службы Bluetooth hello toostart на hello Intel NUC и укажите оболочку hello Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="6af07-127">Run hello following commands toostart hello Bluetooth service on hello Intel NUC and enter hello Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="6af07-128">Выполните следующие команды toopower на контроллере Bluetooth hello hello.</span><span class="sxs-lookup"><span data-stu-id="6af07-128">Run hello following command toopower on hello Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="6af07-129">После на hello контроллера, вы увидите сообщение **изменение питания на успешно**.</span><span class="sxs-lookup"><span data-stu-id="6af07-129">When hello controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="6af07-130">Выполните hello, следующая команда tooscan для ближайших устройствами Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="6af07-130">Run hello following command tooscan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="6af07-131">Power приветствия нажмите кнопу hello SensorTag toomake ее доступной для обнаружения.</span><span class="sxs-lookup"><span data-stu-id="6af07-131">Press hello power button on hello SensorTag toomake it discoverable.</span></span> <span data-ttu-id="6af07-132">Hello зеленый Индикатор мигает.</span><span class="sxs-lookup"><span data-stu-id="6af07-132">hello green LED flashes.</span></span>

1. <span data-ttu-id="6af07-133">После появления сообщения в оболочке hello контроллера hello обнаружил hello SensorTag, запишите hello MAC-адрес устройства hello.</span><span class="sxs-lookup"><span data-stu-id="6af07-133">When you see a message in hello shell that hello controller has discovered hello SensorTag, make a note of hello MAC address of hello device.</span></span> <span data-ttu-id="6af07-134">Hello MAC-адрес выглядит как **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="6af07-134">hello MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="6af07-135">MAC-адрес hello далее в учебнике hello необходимо при настройке шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="6af07-135">You need hello MAC address later in hello tutorial when you configure hello gateway.</span></span>

1. <span data-ttu-id="6af07-136">Выполните hello, следующая команда tooturn off сканирование Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="6af07-136">Run hello following command tooturn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="6af07-137">Выполните следующие команды tooverify, возможность подключения устройства SensorTag toohello hello.</span><span class="sxs-lookup"><span data-stu-id="6af07-137">Run hello following command tooverify that you can connect toohello SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="6af07-138">Если подключение выполнено успешно, оболочка hello показывает сообщение hello **подключение выполнено успешно** и выводит на печать сведения об устройстве SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="6af07-138">If you connect successfully, hello shell shows hello message **Connection successful** and prints information about hello SensorTag device.</span></span> <span data-ttu-id="6af07-139">Если вы не можете подключиться, проверьте приветствия SensorTag по-прежнему не будет включено.</span><span class="sxs-lookup"><span data-stu-id="6af07-139">If you cannot connect, check hello SensorTag is still powered on.</span></span>

1. <span data-ttu-id="6af07-140">Теперь можно отключиться от hello SensorTag и выйти из оболочки Bluetooth hello, запустив hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="6af07-140">You can now disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="6af07-141">Построение настраиваемого модуля IoT Edge hello</span><span class="sxs-lookup"><span data-stu-id="6af07-141">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="6af07-142">Теперь можно построить hello пользовательский IoT Edge модуль, который позволяет hello toosend сообщения toohello удаленного мониторинга решение шлюза.</span><span class="sxs-lookup"><span data-stu-id="6af07-142">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="6af07-143">Дополнительные сведения о настройке шлюза и модулей Edge Интернета вещей см. в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="6af07-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="6af07-144">Загрузка исходного кода hello для пользовательских модулей IoT Edge hello из GitHub, используя hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="6af07-144">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="6af07-145">Сборки hello с помощью следующих команд hello пользовательский модуль IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="6af07-145">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="6af07-146">скрипт сборки Hello помещает пользовательский модуль IoT Edge hello libsensor2remotemonitoring.so в папке построения hello.</span><span class="sxs-lookup"><span data-stu-id="6af07-146">hello build script places hello libsensor2remotemonitoring.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="6af07-147">Настройка и запуск hello IoT шлюз</span><span class="sxs-lookup"><span data-stu-id="6af07-147">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="6af07-148">Теперь можно настроить hello IoT пограничного шлюза toosend телеметрии из вашего SensorTag устройства tooyour удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="6af07-148">You can now configure hello IoT Edge gateway toosend telemetry from your SensorTag device tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="6af07-149">Дополнительные сведения о настройке шлюза и модулей Edge Интернета вещей см. в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="6af07-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="6af07-150">В этом учебнике используется стандарт hello `vi` текстового редактора hello Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="6af07-150">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="6af07-151">Если вы не использовали `vi` ранее, следует выполнить Вводное руководство, такие как [Unix - hello vi учебник редактора] [ lnk-vi-tutorial] toofamiliarize самостоятельно с помощью этого редактора.</span><span class="sxs-lookup"><span data-stu-id="6af07-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="6af07-152">Кроме того, можно установить более удобный hello [nano](https://www.nano-editor.org/) редактора с помощью команды hello `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="6af07-152">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="6af07-153">Привет открыть образец файла конфигурации в hello **vi** редактора с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6af07-153">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="6af07-154">Найдите следующие строки в hello конфигурации для модуля центром IOT hello hello:</span><span class="sxs-lookup"><span data-stu-id="6af07-154">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="6af07-155">Замените заполнитель hello значениями hello сведения центр IoT был создан и сохранен в hello запуск этого учебника.</span><span class="sxs-lookup"><span data-stu-id="6af07-155">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="6af07-156">значение Hello IoTHubName выглядит как **yourrmsolution37e08**, а hello IoTSuffix равно обычно **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="6af07-156">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="6af07-157">Найдите следующие строки в hello конфигурации для модуля сопоставления hello hello:</span><span class="sxs-lookup"><span data-stu-id="6af07-157">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="6af07-158">Замените hello **macAddress** заполнитель hello MAC-адрес вашего SensorTag было сказано ранее.</span><span class="sxs-lookup"><span data-stu-id="6af07-158">Replace hello **macAddress** placeholder with hello MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="6af07-159">Замените hello **deviceID** и **deviceKey** местозаполнителей hello идентификаторы и ключи для hello два устройства, вы создали в решение для удаленного мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="6af07-159">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="6af07-160">Найдите следующие строки в hello конфигурации для модуля SensorTag hello hello:</span><span class="sxs-lookup"><span data-stu-id="6af07-160">Locate hello following lines in hello configuration for hello SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="6af07-161">Замените hello **устройства\_mac\_адрес** заполнитель hello MAC-адрес вашего SensorTag было сказано ранее.</span><span class="sxs-lookup"><span data-stu-id="6af07-161">Replace hello **device\_mac\_address** placeholder  with hello MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="6af07-162">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="6af07-162">Save your changes.</span></span>

<span data-ttu-id="6af07-163">Теперь можно выполнить с помощью следующих команд hello шлюза hello:</span><span class="sxs-lookup"><span data-stu-id="6af07-163">You can now run hello gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="6af07-164">Hello IoT шлюзом начинается hello Intel NUC и отправляет данные телеметрии из hello SensorTag toohello удаленного мониторинга решения:</span><span class="sxs-lookup"><span data-stu-id="6af07-164">hello IoT Edge gateway starts on hello Intel NUC and sends telemetry from hello SensorTag toohello remote monitoring solution:</span></span>

![IoT шлюз отправляет данные телеметрии из hello SensorTag][img-telemetry]

<span data-ttu-id="6af07-166">Нажмите клавишу **Ctrl-C** tooexit программа hello в любое время.</span><span class="sxs-lookup"><span data-stu-id="6af07-166">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="6af07-167">Представление hello телеметрии</span><span class="sxs-lookup"><span data-stu-id="6af07-167">View hello telemetry</span></span>

<span data-ttu-id="6af07-168">шлюз Hello теперь отправляет данные телеметрии из hello SensorTag toohello удаленного мониторинга устройствами.</span><span class="sxs-lookup"><span data-stu-id="6af07-168">hello gateway is now sending telemetry from hello SensorTag device toohello remote monitoring solution.</span></span> <span data-ttu-id="6af07-169">Hello телеметрии можно просмотреть на панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="6af07-169">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="6af07-170">Можно также отправлять команды tooyour SensorTag устройства через шлюз hello из панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="6af07-170">You can also send commands tooyour SensorTag device through hello gateway from hello solution dashboard.</span></span>

- <span data-ttu-id="6af07-171">Перейдите в панель мониторинга toohello решения.</span><span class="sxs-lookup"><span data-stu-id="6af07-171">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="6af07-172">Выберите hello устройства, настроенные в hello шлюза, который представляет hello SensorTag в hello **tooView устройства** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="6af07-172">Select hello device you configured in hello gateway that represents hello SensorTag in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="6af07-173">Hello телеметрии с hello SensorTag устройства отображаются на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="6af07-173">hello telemetry from hello SensorTag device displays on hello dashboard.</span></span>

![Отобразить данные телеметрии с устройств SensorTag hello][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="6af07-175">Если оставить hello удаленное наблюдение решение, работающее в учетной записи Azure, взимается плата за hello выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="6af07-175">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="6af07-176">Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="6af07-176">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="6af07-177">Удаление hello предварительно настроенное решение из учетной записи Azure, после завершения его использования.</span><span class="sxs-lookup"><span data-stu-id="6af07-177">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6af07-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6af07-178">Next steps</span></span>

<span data-ttu-id="6af07-179">Посетите hello [Центр разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/) Дополнительные примеры и документация по Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="6af07-179">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started