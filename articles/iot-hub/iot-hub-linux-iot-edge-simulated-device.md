---
title: "aaaSimulate устройства Azure IoT границу (Linux) | Документы Microsoft"
description: "Как toouse Azure IoT Edge для Linux toocreate имитированное устройство, отправляет телеметрии через IoT граница центра IoT tooan шлюза."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 11e7bf28-ee3d-48d6-a386-eb506c7a31cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: 168fb8eda8671d02c63073bdf36dfcd88b397fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="70780-103">Использовать сообщения из устройства в облако Azure IoT Edge toosend с имитированное устройство (Linux)</span><span class="sxs-lookup"><span data-stu-id="70780-103">Use Azure IoT Edge toosend device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="70780-104">Как toorun hello образца</span><span class="sxs-lookup"><span data-stu-id="70780-104">How toorun hello sample</span></span>

<span data-ttu-id="70780-105">Hello **build.sh** сценарий создает выходные данные в hello **построения** папки в локальной копии hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="70780-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="70780-106">Этот выход включает в себя четыре края IoT модули hello используемый в этом примере.</span><span class="sxs-lookup"><span data-stu-id="70780-106">This output includes hello four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="70780-107">Здравствуйте местах скрипт построения:</span><span class="sxs-lookup"><span data-stu-id="70780-107">hello build script places the:</span></span>

* <span data-ttu-id="70780-108">**liblogger.SO** в hello **сборки, модули/logger** папки.</span><span class="sxs-lookup"><span data-stu-id="70780-108">**liblogger.so** in hello **build/modules/logger** folder.</span></span>
* <span data-ttu-id="70780-109">**libiothub.SO** в hello **сборки/модули/центром IOT** папки.</span><span class="sxs-lookup"><span data-stu-id="70780-109">**libiothub.so** in hello **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="70780-110">**LIB\_удостоверение\_map.so** в hello **сборки, модули и identitymap** папки.</span><span class="sxs-lookup"><span data-stu-id="70780-110">**lib\_identity\_map.so** in hello **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="70780-111">**libsimulated\_device.so** в hello **сборки/модули/имитировать\_устройства** папки.</span><span class="sxs-lookup"><span data-stu-id="70780-111">**libsimulated\_device.so** in hello **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="70780-112">Эти пути можно использовать для hello **путь к модулю** значения, как показано в hello следующие параметры файл JSON:</span><span class="sxs-lookup"><span data-stu-id="70780-112">Use these paths for hello **module path** values as shown in hello following JSON settings file:</span></span>

<span data-ttu-id="70780-113">Hello имитировать\_устройства\_облака\_отправить\_занимает образец файла конфигурации JSON tooa путь hello аргумент командной строки.</span><span class="sxs-lookup"><span data-stu-id="70780-113">hello simulated\_device\_cloud\_upload\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="70780-114">Hello следующий файл JSON приведены в репозиторий SDK hello в **образцы\\имитацию\_устройства\_облака\_отправить\_пример\\src\\ Имитация\_устройства\_облака\_отправить\_пример\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="70780-114">hello following example JSON file is provided in hello SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="70780-115">Это работает файл конфигурации, если только не изменить hello построения hello tooplace сценария IoT Edge модули или образец исполняемые файлы в нестандартные расположения.</span><span class="sxs-lookup"><span data-stu-id="70780-115">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="70780-116">Hello модуля пути являются toohello относительный каталог, из которой запущена hello имитировать\_устройства\_облака\_отправить\_исполняемый файл образца, не hello каталог, где находится исполняемый файл hello.</span><span class="sxs-lookup"><span data-stu-id="70780-116">hello module paths are relative toohello directory from where you run hello simulated\_device\_cloud\_upload\_sample executable, not hello directory where hello executable is located.</span></span> <span data-ttu-id="70780-117">Образец Hello JSON файла конфигурации по умолчанию toowriting too'deviceCloudUploadGatewaylog.log "в текущий рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="70780-117">hello sample JSON configuration file defaults toowriting too'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="70780-118">В текстовом редакторе откройте файл hello **образцы и имитировать\_устройства\_облака\_отправить\_образец/src/имитировать\_устройства\_облака\_отправить\_lin.json** в локальной копии hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="70780-118">In a text editor, open hello file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="70780-119">Этот файл настраивает модули IoT Edge hello в пример hello шлюза:</span><span class="sxs-lookup"><span data-stu-id="70780-119">This file configures hello IoT Edge modules in hello sample gateway:</span></span>

* <span data-ttu-id="70780-120">Hello **центром IOT** модуль подключается tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="70780-120">hello **IoTHub** module connects tooyour IoT hub.</span></span> <span data-ttu-id="70780-121">Можно настроить центр IoT tooyour toosend данных.</span><span class="sxs-lookup"><span data-stu-id="70780-121">You configure it toosend data tooyour IoT hub.</span></span> <span data-ttu-id="70780-122">В частности, набор hello **IoTHubName** toohello имя вашего центра IoT и задать hello **IoTHubSuffix** значение слишком**azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="70780-122">Specifically, set hello **IoTHubName** value toohello name of your IoT hub and set hello **IoTHubSuffix** value too**azure-devices.net**.</span></span> <span data-ttu-id="70780-123">Набор hello **транспорта** tooone значение из: **HTTP**, **AMQP**, или **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="70780-123">Set hello **Transport** value tooone of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="70780-124">В настоящее время только **HTTP** использует одно TCP-подключение для всех сообщений с устройства.</span><span class="sxs-lookup"><span data-stu-id="70780-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="70780-125">Если значение hello слишком**AMQP**, или **MQTT**, hello шлюз поддерживает отдельные TCP подключения tooIoT концентратора для каждого устройства.</span><span class="sxs-lookup"><span data-stu-id="70780-125">If you set hello value too**AMQP**, or **MQTT**, hello gateway maintains a separate TCP connection tooIoT Hub for each device.</span></span>
* <span data-ttu-id="70780-126">Hello **сопоставления** модуль сопоставляет hello MAC-адресов идентификатор устройства центра IoT tooyour имитации устройства.</span><span class="sxs-lookup"><span data-stu-id="70780-126">hello **mapping** module maps hello MAC addresses of your simulated devices tooyour IoT Hub device ids.</span></span> <span data-ttu-id="70780-127">Убедитесь, что **deviceId** значения соответствия hello идентификаторы hello два устройства, вы добавили tooyour центр IoT и что hello **deviceKey** значения содержат ключи hello двух устройств.</span><span class="sxs-lookup"><span data-stu-id="70780-127">Make sure that **deviceId** values match hello ids of hello two devices you added tooyour IoT hub, and that hello **deviceKey** values contain hello keys of your two devices.</span></span>
* <span data-ttu-id="70780-128">Hello **BLE1** и **BLE2** модули являются hello имитируемые устройства.</span><span class="sxs-lookup"><span data-stu-id="70780-128">hello **BLE1** and **BLE2** modules are hello simulated devices.</span></span> <span data-ttu-id="70780-129">Обратите внимание на то, как их MAC-адресов, соответствие hello адреса в hello **сопоставления** модуля.</span><span class="sxs-lookup"><span data-stu-id="70780-129">Note how their MAC addresses match hello addresses in hello **mapping** module.</span></span>
* <span data-ttu-id="70780-130">Hello **средства ведения журнала** модуль регистрирует файл tooa действия шлюза.</span><span class="sxs-lookup"><span data-stu-id="70780-130">hello **Logger** module logs your gateway activity tooa file.</span></span>
* <span data-ttu-id="70780-131">Hello **путь к модулю** значения, как показано в примере hello предполагается запускать образец hello из hello **построения** папки в локальной копии hello **iot edge** репозитория.</span><span class="sxs-lookup"><span data-stu-id="70780-131">hello **module path** values shown in hello example assume that you run hello sample from hello **build** folder in your local copy of hello **iot-edge** repository.</span></span>
* <span data-ttu-id="70780-132">Hello **ссылки** массива внизу hello hello JSON-файл подключается hello **BLE1** и **BLE2** toohello модули **сопоставления** модуль и hello **сопоставления** toohello модуль **центром IOT** модуля.</span><span class="sxs-lookup"><span data-stu-id="70780-132">hello **links** array at hello bottom of hello JSON file connects hello **BLE1** and **BLE2** modules toohello **mapping** module, and hello **mapping** module toohello **IoTHub** module.</span></span> <span data-ttu-id="70780-133">Это также гарантирует, что все сообщения регистрируются по hello **средства ведения журнала** модуля.</span><span class="sxs-lookup"><span data-stu-id="70780-133">It also ensures that all messages are logged by hello **Logger** module.</span></span>

```json
{
    "modules": [
        {
            "name": "IotHub",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/iothub/libiothub.so"
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
              "module.path": "./modules/identitymap/libidentity_map.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args": {
              "filename": "deviceCloudUploadGatewaylog.log"
            }
          }
    ],
    "links": [
        {
            "source": "*",
            "sink": "Logger"
        },
        {
            "source": "BLE1",
            "sink": "mapping"
        },
        {
            "source": "BLE2",
            "sink": "mapping"
        },
        {
            "source": "mapping",
            "sink": "IotHub"
        }
    ]
}
```

<span data-ttu-id="70780-134">Сохранить hello изменения, сделанные toohello файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="70780-134">Save hello changes you made toohello configuration file.</span></span>

<span data-ttu-id="70780-135">Образец hello toorun:</span><span class="sxs-lookup"><span data-stu-id="70780-135">toorun hello sample:</span></span>

1. <span data-ttu-id="70780-136">Перейдите к оболочке toohello **iot — edge и сборки** папки.</span><span class="sxs-lookup"><span data-stu-id="70780-136">In your shell, navigate toohello **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="70780-137">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="70780-137">Run hello following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="70780-138">Можно использовать hello [обозреватель устройств] [ lnk-device-explorer] или [explorer центром IOT] [ lnk-iothub-explorer] средства toomonitor сообщений hello, назначенных hello центра IoT шлюз.</span><span class="sxs-lookup"><span data-stu-id="70780-138">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool toomonitor hello messages that IoT hub receives from hello gateway.</span></span> <span data-ttu-id="70780-139">Например с помощью обозревателя с центром IOT можно отслеживать сообщения устройства в облако, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="70780-139">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="70780-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="70780-140">Next steps</span></span>

<span data-ttu-id="70780-141">toogain более глубоким пониманием Azure IoT Edge и поэкспериментировать с некоторые примеры кода, посетите следующие hello разработчика учебники и ресурсы:</span><span class="sxs-lookup"><span data-stu-id="70780-141">toogain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="70780-142">[Отправка сообщений с устройства в облако с помощью физического устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="70780-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="70780-143">[Azure IoT Edge][lnk-iot-edge] (Edge Интернета вещей Azure).</span><span class="sxs-lookup"><span data-stu-id="70780-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="70780-144">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="70780-144">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="70780-145">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="70780-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="70780-146">[Защита вашего решения IoT из hello основание,][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="70780-146">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
