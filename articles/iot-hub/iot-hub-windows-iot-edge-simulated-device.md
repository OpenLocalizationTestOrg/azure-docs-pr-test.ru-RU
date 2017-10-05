---
title: "Имитация устройства с помощью Edge Интернета вещей Azure (Windows) | Документация Майкрософт"
description: "Сведения об использовании Edge Интернета вещей Azure в Windows для создания имитации устройства, отправляющего данные телеметрии через шлюз Интернета вещей Azure в Центр Интернета вещей."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 6a2aeda0-696a-4732-90e1-595d2e2fadc6
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: e7eb2931993daf3f0aecbd4a43d27ebd5adc10b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-to-send-device-to-cloud-messages-with-a-simulated-device-windows"></a><span data-ttu-id="3e88e-103">Отправка сообщений с устройства в облако с помощью имитации устройства (Windows) с использованием Edge Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="3e88e-103">Use Azure IoT Edge to send device-to-cloud messages with a simulated device (Windows)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="3e88e-104">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="3e88e-104">How to run the sample</span></span>

<span data-ttu-id="3e88e-105">Скрипт **build.cmd** создает выходные данные в папке **build** локальной копии репозитория **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="3e88e-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="3e88e-106">Выходные данные содержат четыре модуля IoT Edge, которые используются в данном примере.</span><span class="sxs-lookup"><span data-stu-id="3e88e-106">This output includes the four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="3e88e-107">Сценарий сборки помещает:</span><span class="sxs-lookup"><span data-stu-id="3e88e-107">The build script places the:</span></span>

* <span data-ttu-id="3e88e-108">**logger.dll** в папку **build\\modules\\logger\\Debug**;</span><span class="sxs-lookup"><span data-stu-id="3e88e-108">**logger.dll** in the **build\\modules\\logger\\Debug** folder.</span></span>
* <span data-ttu-id="3e88e-109">**iothub.dll** в папку **build\\modules\\iothub\\Debug**;</span><span class="sxs-lookup"><span data-stu-id="3e88e-109">**iothub.dll** in the **build\\modules\\iothub\\Debug** folder.</span></span>
* <span data-ttu-id="3e88e-110">**identity\_map.dll** в папку **build\\modules\\identitymap\\Debug**;</span><span class="sxs-lookup"><span data-stu-id="3e88e-110">**identity\_map.dll** in the **build\\modules\\identitymap\\Debug** folder.</span></span>
* <span data-ttu-id="3e88e-111">**simulated\_device.dll** в папку **build\\modules\\simulated\_device\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="3e88e-111">**simulated\_device.dll** in the **build\\modules\\simulated\_device\\Debug** folder.</span></span>

<span data-ttu-id="3e88e-112">Используйте эти пути для настройки значений **module path**, как указано в приведенном ниже файле параметров JSON.</span><span class="sxs-lookup"><span data-stu-id="3e88e-112">Use these paths for the **module path** values as shown in the following JSON settings file:</span></span>

<span data-ttu-id="3e88e-113">Процесс simulated\_device\_cloud\_upload\_sample принимает путь к JSON-файлу конфигурации в качестве аргумента командной строки.</span><span class="sxs-lookup"><span data-stu-id="3e88e-113">The simulated\_device\_cloud\_upload\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="3e88e-114">Следующий пример файла JSON предоставляется в репозитории SDK в расположении **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="3e88e-114">The following example JSON file is provided in the SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span></span> <span data-ttu-id="3e88e-115">Этот файл конфигурации работает так, как если бы вы не модифицировали сценарий сборки, чтобы разместить модули IoT Edge или образцы исполняемых файлов в местах, отличных от настроек по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3e88e-115">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="3e88e-116">Пути к модулям зависят от каталога, в котором находится файл simulated\_device\_cloud\_upload\_sample.exe.</span><span class="sxs-lookup"><span data-stu-id="3e88e-116">The module paths are relative to the directory where the simulated\_device\_cloud\_upload\_sample.exe is located.</span></span> <span data-ttu-id="3e88e-117">Образец файла конфигурации JSON по умолчанию используется для записи в deviceCloudUploadGatewaylog.log в вашей текущей рабочей папке.</span><span class="sxs-lookup"><span data-stu-id="3e88e-117">The sample JSON configuration file defaults to writing to 'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="3e88e-118">В текстовом редакторе откройте файл **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** в локальной копии репозитория **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="3e88e-118">In a text editor, open the file **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="3e88e-119">Этот файл настраивает модули Edge Интернета вещей в примере шлюза:</span><span class="sxs-lookup"><span data-stu-id="3e88e-119">This file configures the IoT Edge modules in the sample gateway:</span></span>

* <span data-ttu-id="3e88e-120">Модуль **IoTHub** подключается к центру IoT.</span><span class="sxs-lookup"><span data-stu-id="3e88e-120">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="3e88e-121">Его необходимо настроить для отправки данных в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="3e88e-121">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="3e88e-122">В частности, укажите в качестве значения **IoTHubName** имя своего Центра Интернета вещей, а в качестве значения **IoTHubSuffix** — **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="3e88e-122">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="3e88e-123">Для параметра **Transport** задайте одно из следующих значений: **HTTP**, **AMQP** или **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="3e88e-123">Set the **Transport** value to one of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="3e88e-124">В настоящее время только **HTTP** использует одно TCP-подключение для всех сообщений с устройства.</span><span class="sxs-lookup"><span data-stu-id="3e88e-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="3e88e-125">Если задать значение **AMQP** или **MQTT**, то шлюз будет поддерживать отдельное TCP-подключение к Центру Интернета вещей для каждого устройства.</span><span class="sxs-lookup"><span data-stu-id="3e88e-125">If you set the value to **AMQP**, or **MQTT**, the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="3e88e-126">Модуль **mapping** сопоставляет MAC-адреса имитаций устройств с идентификаторами устройств Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="3e88e-126">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="3e88e-127">Убедитесь в том, что значения **deviceId** совпадают с идентификаторами двух устройств, добавленных в Центр Интернета вещей, а значения **deviceKey** содержат ключи этих двух устройств.</span><span class="sxs-lookup"><span data-stu-id="3e88e-127">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="3e88e-128">Модули **BLE1** и **BLE2** — это имитации устройств.</span><span class="sxs-lookup"><span data-stu-id="3e88e-128">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="3e88e-129">Обратите внимание, что MAC-адреса модулей совпадают с адресами в модуле **mapping**.</span><span class="sxs-lookup"><span data-stu-id="3e88e-129">Note how the module MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="3e88e-130">Модуль **Logger** регистрирует активность вашего шлюза в файл.</span><span class="sxs-lookup"><span data-stu-id="3e88e-130">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="3e88e-131">Значения **путей модуля** в следующем примере зависят от каталога, в котором находится файл simulated\_device\_cloud\_upload\_sample.exe.</span><span class="sxs-lookup"><span data-stu-id="3e88e-131">The **module path** values shown in the following example are relative to the directory where the simulated\_device\_cloud\_upload\_sample.exe is located.</span></span>
* <span data-ttu-id="3e88e-132">Массив **links** в нижней части JSON-файла подключает модули **BLE1** и **BLE2** к модулю **mapping**, а модуль **mapping** — к модулю **IoTHub**.</span><span class="sxs-lookup"><span data-stu-id="3e88e-132">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="3e88e-133">Это также гарантирует, что все сообщения будут зарегистрированы модулем **Logger** .</span><span class="sxs-lookup"><span data-stu-id="3e88e-133">It also ensures that all messages are logged by the **Logger** module.</span></span>

```json
{
    "modules" :
    [
      {
        "name": "IotHub",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\iothub\\Debug\\iothub.dll"
          }
          },
          "args": {
            "IoTHubName": "<<insert here IoTHubName>>",
            "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
            "Transport": "HTTP"
          }
        },
      {
        "name": "mapping",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\identitymap\\Debug\\identity_map.dll"
          }
          },
          "args": [
            {
              "macAddress": "01:01:01:01:01:01",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            },
            {
              "macAddress": "02:02:02:02:02:02",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            }
          ]
        },
      {
        "name": "BLE1",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "01:01:01:01:01:01"
          }
        },
      {
        "name": "BLE2",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "02:02:02:02:02:02"
          }
        },
      {
        "name": "Logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
          }
        },
        "args": {
          "filename": "deviceCloudUploadGatewaylog.log"
        }
      }
    ],
    "links" : [
        { "source" : "*", "sink" : "Logger" },
        { "source" : "BLE1", "sink" : "mapping" },
        { "source" : "BLE2", "sink" : "mapping" },
        { "source" : "mapping", "sink" : "IotHub" }
    ]
}
```

<span data-ttu-id="3e88e-134">Сохраните все изменения, внесенные в файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3e88e-134">Save the changes you made to the configuration file.</span></span>

<span data-ttu-id="3e88e-135">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="3e88e-135">To run the sample:</span></span>

1. <span data-ttu-id="3e88e-136">В командной строке перейдите в папку **build** в локальной копии репозитория **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="3e88e-136">At a command prompt, navigate to the **build** folder in your local copy of the **iot-edge** repository.</span></span>
2. <span data-ttu-id="3e88e-137">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3e88e-137">Run the following command:</span></span>
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. <span data-ttu-id="3e88e-138">Для мониторинга сообщений, получаемых Центром Интернета вещей из шлюза, можно использовать такие средства, как [обозреватель устройств][lnk-device-explorer] или [iothub-explorer][lnk-iothub-explorer].</span><span class="sxs-lookup"><span data-stu-id="3e88e-138">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span> <span data-ttu-id="3e88e-139">Например, используя средство iothub-explorer, вы можете отслеживать сообщения, отправляемые с устройства в облако с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="3e88e-139">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="3e88e-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3e88e-140">Next steps</span></span>

<span data-ttu-id="3e88e-141">Чтобы подробнее изучить возможности IoT Edge и поэкспериментировать с примерами кода, см. следующие руководства и ресурсы для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="3e88e-141">To gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="3e88e-142">[Отправка сообщений с устройства в облако с помощью физического устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="3e88e-142">[Send device-to-cloud messages from a physical device with IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="3e88e-143">[Azure IoT Edge][lnk-iot-edge] (Edge Интернета вещей Azure).</span><span class="sxs-lookup"><span data-stu-id="3e88e-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="3e88e-144">Для дальнейшего изучения возможностей центра IoT см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="3e88e-144">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3e88e-145">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="3e88e-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="3e88e-146">[Комплексная защита в Интернете вещей][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="3e88e-146">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md