---
title: "Подключение шлюза к Azure IoT Suite с помощью Intel NUC | Документация Майкрософт"
description: "Использование набора для создания коммерческого шлюза Интернета вещей (Майкрософт) и предварительно настроенного решения для удаленного мониторинга. Подключайтесь к решению для удаленного мониторинга, отправляйте смоделированные данные телеметрии в облако, а также реагируйте на методы, вызываемые на панели мониторинга этого решения, с помощью шлюза Edge Интернета вещей Azure."
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
ms.openlocfilehash: 9ed57d3c23e2adbd42c054f33c8ed46e3d6c9792
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="a220f-104">Подключение шлюза Edge Интернета вещей Azure к предварительно настроенному решению для удаленного мониторинга и отправка смоделированной телеметрии</span><span class="sxs-lookup"><span data-stu-id="a220f-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="a220f-105">В этом учебнике показано, как использовать Azure IoT Edge для моделирования данных температуры и влажности, отправляемых в заранее настроенное удаленное решение для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a220f-105">This tutorial shows you how to use Azure IoT Edge to simulate temperature and humidity data to send to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="a220f-106">В руководстве используются следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="a220f-106">The tutorial uses:</span></span>

- <span data-ttu-id="a220f-107">Azure IoT Edge для реализации примера шлюза.</span><span class="sxs-lookup"><span data-stu-id="a220f-107">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="a220f-108">Предварительно настроенное решение для удаленного мониторинга IoT Suite в качестве облачного сервера.</span><span class="sxs-lookup"><span data-stu-id="a220f-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="a220f-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="a220f-109">Overview</span></span>

<span data-ttu-id="a220f-110">В этом руководстве выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="a220f-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="a220f-111">Развертывание экземпляра предварительно настроенного решения удаленного мониторинга в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="a220f-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="a220f-112">На этом шаге автоматически разворачивается и настраивается несколько служб Azure.</span><span class="sxs-lookup"><span data-stu-id="a220f-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="a220f-113">Настройка устройства шлюза Intel NUC для взаимодействия с компьютером и решением для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a220f-113">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="a220f-114">Настройка шлюза Edge Интернета вещей для отправки смоделированных данных телеметрии, которые можно просмотреть на панели мониторинга решений.</span><span class="sxs-lookup"><span data-stu-id="a220f-114">Configure the IoT Edge gateway to send simulated telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="a220f-115">Решение для удаленного мониторинга подготавливает набор служб Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="a220f-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="a220f-116">Развертывание отражает реальную корпоративную архитектуру.</span><span class="sxs-lookup"><span data-stu-id="a220f-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="a220f-117">Чтобы избежать ненужных расходов на использование ресурсов Azure, удалите экземпляр предварительно настроенного решения на сайте azureiotsuite.com после завершения работы с ним.</span><span class="sxs-lookup"><span data-stu-id="a220f-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="a220f-118">Если предварительно настроенное решение понадобится снова, его можно легко восстановить.</span><span class="sxs-lookup"><span data-stu-id="a220f-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="a220f-119">Дополнительные сведения о сокращении затрат во время выполнения решения для удаленного мониторинга см. в статье [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Настройка предварительно настроенных решений Azure IoT Suite для демонстрационных целей).</span><span class="sxs-lookup"><span data-stu-id="a220f-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="a220f-120">Повторите предыдущие шаги для добавления второго устройства с использованием идентификатора устройства, такого как **device02**.</span><span class="sxs-lookup"><span data-stu-id="a220f-120">Repeat the previous steps to add a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="a220f-121">Пример отправляет данные из двух виртуальных устройств в шлюзе решению для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a220f-121">The sample sends data from two simulated devices in the gateway to the remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="a220f-122">Создание пользовательского модуля Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="a220f-122">Build the custom IoT Edge module</span></span>

<span data-ttu-id="a220f-123">Теперь вы можете создать пользовательский модуль Edge Интернета вещей, который включает шлюз для отправки сообщений решению для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a220f-123">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="a220f-124">Дополнительные сведения о настройке шлюза и модулей Edge Интернета вещей см. в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="a220f-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="a220f-125">Скачайте исходный код для модулей Edge Интернета вещей с GitHub с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="a220f-125">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="a220f-126">Создайте пользовательский модуль Edge Интернета вещей с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="a220f-126">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="a220f-127">Сценарий сборки помещает пользовательский модуль Edge Интернета вещей libsimulator.so в папку со сборкой.</span><span class="sxs-lookup"><span data-stu-id="a220f-127">The build script places the libsimulator.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="a220f-128">Настройка шлюза Edge Интернета вещей и его выполнение</span><span class="sxs-lookup"><span data-stu-id="a220f-128">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="a220f-129">Теперь вы можете настраивать шлюз Edge Интернета вещей для отправки смоделированных данных телеметрии решению для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a220f-129">You can now configure the IoT Edge gateway to send simulated telemetry to your remote monitoring dashboard.</span></span> <span data-ttu-id="a220f-130">Дополнительные сведения о настройке шлюза и модулей Edge Интернета вещей см. в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="a220f-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="a220f-131">В этом руководстве используется стандартный текстовый редактор `vi` для Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a220f-131">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="a220f-132">Если вы не использовали `vi` ранее, вам необходимо завершить вводное руководство, например [Unix — The vi Editor Tutorial][lnk-vi-tutorial] (Руководство по редактору vi в UNIX), для ознакомления с редактором.</span><span class="sxs-lookup"><span data-stu-id="a220f-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="a220f-133">Кроме того, с помощью команды `smart install nano -y` можно установить более удобный редактор [nano](https://www.nano-editor.org/).</span><span class="sxs-lookup"><span data-stu-id="a220f-133">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="a220f-134">Откройте пример файла конфигурации в редакторе **vi**, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a220f-134">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="a220f-135">Найдите следующие строки в конфигурации для модуля Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="a220f-135">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="a220f-136">Замените значения заполнителей сведениями о Центре Интернета вещей, созданными и сохраненными в начале этого руководства.</span><span class="sxs-lookup"><span data-stu-id="a220f-136">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="a220f-137">Обычно для IoTHubName используется значение **yourrmsolution37e08**, а для IoTSuffix — **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="a220f-137">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="a220f-138">Найдите следующие строки в конфигурации для модуля сопоставления:</span><span class="sxs-lookup"><span data-stu-id="a220f-138">Locate the following lines in the configuration for the mapping module:</span></span>

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

<span data-ttu-id="a220f-139">Замените заполнители **deviceID** и **deviceKey** идентификаторами и ключами двух устройств, созданными ранее для решения удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a220f-139">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="a220f-140">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="a220f-140">Save your changes.</span></span>

<span data-ttu-id="a220f-141">Теперь можно запускать шлюз Edge Интернета вещей с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="a220f-141">You can now run the IoT Edge gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="a220f-142">Шлюз запускается на Intel NUC и отправляет смоделированные данные телеметрии решению для удаленного мониторинга:</span><span class="sxs-lookup"><span data-stu-id="a220f-142">The gateway starts on the Intel NUC and sends simulated telemetry to the remote monitoring solution:</span></span>

![Создание смоделированной телеметрии в шлюзе Edge Интернета вещей][img-simulated telemetry]

<span data-ttu-id="a220f-144">Вы можете в любое время нажать комбинацию клавиш **CTRL+C**, чтобы выйти из программы.</span><span class="sxs-lookup"><span data-stu-id="a220f-144">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="a220f-145">Просмотр телеметрии</span><span class="sxs-lookup"><span data-stu-id="a220f-145">View the telemetry</span></span>

<span data-ttu-id="a220f-146">Теперь шлюз Edge Интернета вещей может отправлять смоделированные данные телеметрии в удаленное решение мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a220f-146">The IoT Edge gateway is now sending simulated telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="a220f-147">Эти данные можно просмотреть на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="a220f-147">You can view the telemetry on the solution dashboard.</span></span>

- <span data-ttu-id="a220f-148">Перейдите к панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="a220f-148">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="a220f-149">В раскрывающемся списке **Device to View** (Устройство для просмотра) выберите одно из двух устройств, настроенных в шлюзе.</span><span class="sxs-lookup"><span data-stu-id="a220f-149">Select one of the two devices you configured in the gateway in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="a220f-150">Данные телеметрии из устройств шлюза отобразятся на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a220f-150">The telemetry from the gateway devices displays on the dashboard.</span></span>

![Отображение данных телеметрии из устройств имитации шлюза][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="a220f-152">Если не завершить выполнение решения удаленного мониторинга в учетной записи Azure, вам будет выставлен счет.</span><span class="sxs-lookup"><span data-stu-id="a220f-152">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="a220f-153">Дополнительные сведения о сокращении затрат во время выполнения решения для удаленного мониторинга см. в статье [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Настройка предварительно настроенных решений Azure IoT Suite для демонстрационных целей).</span><span class="sxs-lookup"><span data-stu-id="a220f-153">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="a220f-154">Прекратив использовать предварительно настроенное решение, удалите его из учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="a220f-154">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a220f-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a220f-155">Next steps</span></span>

<span data-ttu-id="a220f-156">Дополнительные примеры и документацию по Azure IoT можно найти в [Центре разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/).</span><span class="sxs-lookup"><span data-stu-id="a220f-156">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started