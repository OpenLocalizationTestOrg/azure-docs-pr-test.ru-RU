---
title: "aaaConnect шлюза tooAzure IoT Suite, с помощью NUC Intel | Документы Microsoft"
description: "Используйте hello IoT коммерческих шлюза пакета и hello удаленного мониторинга предварительно настроенных решение. Используйте hello Azure IoT Edge tooconnect toohello удаленного мониторинга решение шлюза, отправить облака toohello имитацию телеметрии и реагировать toomethods вызывается из панели мониторинга hello решения."
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
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="ac0bc-104">Подключения вашей Azure IoT пограничного шлюза toohello удаленное наблюдение предварительно настроенных решений и отправки имитацию телеметрии</span><span class="sxs-lookup"><span data-stu-id="ac0bc-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="ac0bc-105">Этот учебник показывает, как toouse Azure IoT Edge toosimulate температуры и влажности toosend toohello удаленного мониторинга данных предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-105">This tutorial shows you how toouse Azure IoT Edge toosimulate temperature and humidity data toosend toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="ac0bc-106">Hello учебнике используется:</span><span class="sxs-lookup"><span data-stu-id="ac0bc-106">hello tutorial uses:</span></span>

- <span data-ttu-id="ac0bc-107">Azure IoT Edge tooimplement пример шлюза.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-107">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="ac0bc-108">удаленный мониторинг Hello IoT Suite предварительно настроить решение в hello облачной серверной части.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="ac0bc-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="ac0bc-109">Overview</span></span>

<span data-ttu-id="ac0bc-110">В этом учебнике необходимо выполнить следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="ac0bc-111">Разверните экземпляр hello удаленного мониторинга предварительно настроенных решений tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="ac0bc-112">На этом шаге автоматически разворачивается и настраивается несколько служб Azure.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="ac0bc-113">Настройка toocommunicate устройства шлюза вашей Intel NUC, с компьютера и решение для удаленного мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-113">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="ac0bc-114">Настройте hello IoT пограничного шлюза toosend смоделированные данные телеметрии, можно просмотреть на панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-114">Configure hello IoT Edge gateway toosend simulated telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="ac0bc-115">Hello удаленного мониторинга решения подготавливает набор служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="ac0bc-116">Развертывание Hello отражает реальные корпоративной архитектуре.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="ac0bc-117">плата tooavoid ненужные использование Azure, удаление экземпляра hello предварительно настроенное решение в azureiotsuite.com после завершения с ним.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="ac0bc-118">Если предварительно настроенных решений требуется hello еще раз, то ее можно легко восстановить.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="ac0bc-119">Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="ac0bc-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="ac0bc-120">Повторите предыдущие шаги tooadd hello второго устройства с помощью идентификатор устройства, например **device02**.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-120">Repeat hello previous steps tooadd a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="ac0bc-121">Образец Hello отправляет данные из двух имитацию устройств в hello toohello удаленного мониторинга решение шлюза.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-121">hello sample sends data from two simulated devices in hello gateway toohello remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="ac0bc-122">Построение настраиваемого модуля IoT Edge hello</span><span class="sxs-lookup"><span data-stu-id="ac0bc-122">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="ac0bc-123">Теперь можно построить hello пользовательский IoT Edge модуль, который позволяет hello toosend сообщения toohello удаленного мониторинга решение шлюза.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-123">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="ac0bc-124">Дополнительные сведения о настройке шлюза и модулей Edge Интернета вещей см. в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="ac0bc-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="ac0bc-125">Загрузка исходного кода hello для пользовательских модулей IoT Edge hello из GitHub, используя hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ac0bc-125">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="ac0bc-126">Сборки hello с помощью следующих команд hello пользовательский модуль IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="ac0bc-126">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="ac0bc-127">скрипт сборки Hello помещает пользовательский модуль IoT Edge hello libsimulator.so в папке построения hello.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-127">hello build script places hello libsimulator.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="ac0bc-128">Настройка и запуск hello IoT шлюз</span><span class="sxs-lookup"><span data-stu-id="ac0bc-128">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="ac0bc-129">Теперь можно настроить hello IoT пограничного шлюза toosend имитацию телеметрии tooyour удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-129">You can now configure hello IoT Edge gateway toosend simulated telemetry tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="ac0bc-130">Дополнительные сведения о настройке шлюза и модулей Edge Интернета вещей см. в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="ac0bc-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="ac0bc-131">В этом учебнике используется стандарт hello `vi` текстового редактора hello Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-131">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="ac0bc-132">Если вы не использовали `vi` ранее, следует выполнить Вводное руководство, такие как [Unix - hello vi учебник редактора] [ lnk-vi-tutorial] toofamiliarize самостоятельно с помощью этого редактора.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="ac0bc-133">Кроме того, можно установить более удобный hello [nano](https://www.nano-editor.org/) редактора с помощью команды hello `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-133">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="ac0bc-134">Привет открыть образец файла конфигурации в hello **vi** редактора с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ac0bc-134">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="ac0bc-135">Найдите следующие строки в hello конфигурации для модуля центром IOT hello hello:</span><span class="sxs-lookup"><span data-stu-id="ac0bc-135">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="ac0bc-136">Замените заполнитель hello значениями hello сведения центр IoT был создан и сохранен в hello запуск этого учебника.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-136">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="ac0bc-137">значение Hello IoTHubName выглядит как **yourrmsolution37e08**, а hello IoTSuffix равно обычно **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-137">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="ac0bc-138">Найдите следующие строки в hello конфигурации для модуля сопоставления hello hello:</span><span class="sxs-lookup"><span data-stu-id="ac0bc-138">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="ac0bc-139">Замените hello **deviceID** и **deviceKey** местозаполнителей hello идентификаторы и ключи для hello два устройства, вы создали в решение для удаленного мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-139">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="ac0bc-140">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-140">Save your changes.</span></span>

<span data-ttu-id="ac0bc-141">Теперь можно запускать приветствия IoT шлюз с помощью hello следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ac0bc-141">You can now run hello IoT Edge gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="ac0bc-142">шлюз Hello начинается hello Intel NUC и отправляет имитацию телеметрии toohello удаленного мониторинга решения:</span><span class="sxs-lookup"><span data-stu-id="ac0bc-142">hello gateway starts on hello Intel NUC and sends simulated telemetry toohello remote monitoring solution:</span></span>

![Создание смоделированной телеметрии в шлюзе Edge Интернета вещей][img-simulated telemetry]

<span data-ttu-id="ac0bc-144">Нажмите клавишу **Ctrl-C** tooexit программа hello в любое время.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-144">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="ac0bc-145">Представление hello телеметрии</span><span class="sxs-lookup"><span data-stu-id="ac0bc-145">View hello telemetry</span></span>

<span data-ttu-id="ac0bc-146">Hello IoT шлюзом теперь отправляет имитацию телеметрии toohello удаленного решение для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-146">hello IoT Edge gateway is now sending simulated telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="ac0bc-147">Hello телеметрии можно просмотреть на панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-147">You can view hello telemetry on hello solution dashboard.</span></span>

- <span data-ttu-id="ac0bc-148">Перейдите в панель мониторинга toohello решения.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-148">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="ac0bc-149">Выберите одно из устройств hello двух, настроенного в шлюзе hello в hello **tooView устройства** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-149">Select one of hello two devices you configured in hello gateway in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="ac0bc-150">Hello телеметрии из шлюзов hello отображаются на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-150">hello telemetry from hello gateway devices displays on hello dashboard.</span></span>

![Отобразить данные телеметрии из шлюзов имитируемые hello][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="ac0bc-152">Если оставить hello удаленное наблюдение решение, работающее в учетной записи Azure, взимается плата за hello выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-152">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="ac0bc-153">Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="ac0bc-153">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="ac0bc-154">Удаление hello предварительно настроенное решение из учетной записи Azure, после завершения его использования.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-154">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac0bc-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac0bc-155">Next steps</span></span>

<span data-ttu-id="ac0bc-156">Посетите hello [Центр разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/) Дополнительные примеры и документация по Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="ac0bc-156">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started