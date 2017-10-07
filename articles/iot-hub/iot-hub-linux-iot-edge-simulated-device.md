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
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a>Использовать сообщения из устройства в облако Azure IoT Edge toosend с имитированное устройство (Linux)

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Как toorun hello образца

Hello **build.sh** сценарий создает выходные данные в hello **построения** папки в локальной копии hello **iot edge** репозитория. Этот выход включает в себя четыре края IoT модули hello используемый в этом примере.

Здравствуйте местах скрипт построения:

* **liblogger.SO** в hello **сборки, модули/logger** папки.
* **libiothub.SO** в hello **сборки/модули/центром IOT** папки.
* **LIB\_удостоверение\_map.so** в hello **сборки, модули и identitymap** папки.
* **libsimulated\_device.so** в hello **сборки/модули/имитировать\_устройства** папки.

Эти пути можно использовать для hello **путь к модулю** значения, как показано в hello следующие параметры файл JSON:

Hello имитировать\_устройства\_облака\_отправить\_занимает образец файла конфигурации JSON tooa путь hello аргумент командной строки. Hello следующий файл JSON приведены в репозиторий SDK hello в **образцы\\имитацию\_устройства\_облака\_отправить\_пример\\src\\ Имитация\_устройства\_облака\_отправить\_пример\_lin.json**. Это работает файл конфигурации, если только не изменить hello построения hello tooplace сценария IoT Edge модули или образец исполняемые файлы в нестандартные расположения.

> [!NOTE]
> Hello модуля пути являются toohello относительный каталог, из которой запущена hello имитировать\_устройства\_облака\_отправить\_исполняемый файл образца, не hello каталог, где находится исполняемый файл hello. Образец Hello JSON файла конфигурации по умолчанию toowriting too'deviceCloudUploadGatewaylog.log "в текущий рабочий каталог.

В текстовом редакторе откройте файл hello **образцы и имитировать\_устройства\_облака\_отправить\_образец/src/имитировать\_устройства\_облака\_отправить\_lin.json** в локальной копии hello **iot edge** репозитория. Этот файл настраивает модули IoT Edge hello в пример hello шлюза:

* Hello **центром IOT** модуль подключается tooyour центр IoT. Можно настроить центр IoT tooyour toosend данных. В частности, набор hello **IoTHubName** toohello имя вашего центра IoT и задать hello **IoTHubSuffix** значение слишком**azure devices.net**. Набор hello **транспорта** tooone значение из: **HTTP**, **AMQP**, или **MQTT**. В настоящее время только **HTTP** использует одно TCP-подключение для всех сообщений с устройства. Если значение hello слишком**AMQP**, или **MQTT**, hello шлюз поддерживает отдельные TCP подключения tooIoT концентратора для каждого устройства.
* Hello **сопоставления** модуль сопоставляет hello MAC-адресов идентификатор устройства центра IoT tooyour имитации устройства. Убедитесь, что **deviceId** значения соответствия hello идентификаторы hello два устройства, вы добавили tooyour центр IoT и что hello **deviceKey** значения содержат ключи hello двух устройств.
* Hello **BLE1** и **BLE2** модули являются hello имитируемые устройства. Обратите внимание на то, как их MAC-адресов, соответствие hello адреса в hello **сопоставления** модуля.
* Hello **средства ведения журнала** модуль регистрирует файл tooa действия шлюза.
* Hello **путь к модулю** значения, как показано в примере hello предполагается запускать образец hello из hello **построения** папки в локальной копии hello **iot edge** репозитория.
* Hello **ссылки** массива внизу hello hello JSON-файл подключается hello **BLE1** и **BLE2** toohello модули **сопоставления** модуль и hello **сопоставления** toohello модуль **центром IOT** модуля. Это также гарантирует, что все сообщения регистрируются по hello **средства ведения журнала** модуля.

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

Сохранить hello изменения, сделанные toohello файла конфигурации.

Образец hello toorun:

1. Перейдите к оболочке toohello **iot — edge и сборки** папки.
2. Выполните следующую команду hello.
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. Можно использовать hello [обозреватель устройств] [ lnk-device-explorer] или [explorer центром IOT] [ lnk-iothub-explorer] средства toomonitor сообщений hello, назначенных hello центра IoT шлюз. Например с помощью обозревателя с центром IOT можно отслеживать сообщения устройства в облако, с помощью hello следующую команду:

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>Дальнейшие действия

toogain более глубоким пониманием Azure IoT Edge и поэкспериментировать с некоторые примеры кода, посетите следующие hello разработчика учебники и ресурсы:

* [Отправка сообщений с устройства в облако с помощью физического устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-physical-device]
* [Azure IoT Edge][lnk-iot-edge] (Edge Интернета вещей Azure).

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Руководство разработчика для Центра Интернета вещей][lnk-devguide]
* [Защита вашего решения IoT из hello основание,][lnk-securing]

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
