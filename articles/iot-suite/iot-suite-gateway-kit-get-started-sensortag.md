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
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a>Подключения вашей Azure IoT пограничного шлюза toohello удаленное наблюдение предварительно настроенных решений и отправки данных телеметрии из SensorTag

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Этот учебник показывает, как toouse Azure IoT Edge toosend температуры и влажности данные из удаленного мониторинга SensorTag устройств toohello предварительно настроенных решений. Hello SensorTag подключается toohello Intel NUC шлюза с помощью Bluetooth. Hello учебнике используется:

- Azure IoT Edge tooimplement пример шлюза.
- удаленный мониторинг Hello IoT Suite предварительно настроить решение в hello облачной серверной части.

## <a name="overview"></a>Обзор

В этом учебнике необходимо выполнить следующие шаги hello.

- Разверните экземпляр hello удаленного мониторинга предварительно настроенных решений tooyour подписки Azure. На этом шаге автоматически разворачивается и настраивается несколько служб Azure.
- Настройка toocommunicate устройства шлюза вашей Intel NUC, с компьютера и решение для удаленного мониторинга hello.
- Настройка шлюза tooreceive Intel NUC телеметрии из устройства SensorTag и отправьте ее toohello удаленного мониторинга.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[Texas Instruments BLE SensorTag][lnk-sensortag]. Этот учебник извлекает данные телеметрии через Bluetooth устройства SensorTag hello.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hello удаленного мониторинга решения подготавливает набор служб Azure в подписке Azure. Развертывание Hello отражает реальные корпоративной архитектуре. плата tooavoid ненужные использование Azure, удаление экземпляра hello предварительно настроенное решение в azureiotsuite.com после завершения с ним. Если предварительно настроенных решений требуется hello еще раз, то ее можно легко восстановить. Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a>Настройка подключения Bluetooth

Настроить Bluetooth на устройстве hello Intel NUC tooenable hello SensorTag tooconnect и отправка данных телеметрии.

### <a name="find-hello-mac-address-of-hello-sensortag"></a>Найти hello MAC-адрес hello SensorTag

1. В оболочке hello на hello Intel NUC выполните hello, следующая команда toounblock hello Bluetooth службы:

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. Ниже hello выполнения команды службы Bluetooth hello toostart на hello Intel NUC и укажите оболочку hello Bluetooth:

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Выполните следующие команды toopower на контроллере Bluetooth hello hello.

    ```bash
    power on
    ```

    После на hello контроллера, вы увидите сообщение **изменение питания на успешно**.

1. Выполните hello, следующая команда tooscan для ближайших устройствами Bluetooth.

    ```bash
    scan on
    ```

1. Power приветствия нажмите кнопу hello SensorTag toomake ее доступной для обнаружения. Hello зеленый Индикатор мигает.

1. После появления сообщения в оболочке hello контроллера hello обнаружил hello SensorTag, запишите hello MAC-адрес устройства hello. Hello MAC-адрес выглядит как **A0:E6:F8:B5:F6:00**. MAC-адрес hello далее в учебнике hello необходимо при настройке шлюза hello.

1. Выполните hello, следующая команда tooturn off сканирование Bluetooth:

    ```bash
    scan off
    ```

1. Выполните следующие команды tooverify, возможность подключения устройства SensorTag toohello hello.

    ```bash
    connect <SensorTag MAC address>
    ```

    Если подключение выполнено успешно, оболочка hello показывает сообщение hello **подключение выполнено успешно** и выводит на печать сведения об устройстве SensorTag hello. Если вы не можете подключиться, проверьте приветствия SensorTag по-прежнему не будет включено.

1. Теперь можно отключиться от hello SensorTag и выйти из оболочки Bluetooth hello, запустив hello, следующие команды:

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a>Построение настраиваемого модуля IoT Edge hello

Теперь можно построить hello пользовательский IoT Edge модуль, который позволяет hello toosend сообщения toohello удаленного мониторинга решение шлюза. Дополнительные сведения о настройке шлюза и модулей Edge Интернета вещей см. в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-gateway-concepts].

Загрузка исходного кода hello для пользовательских модулей IoT Edge hello из GitHub, используя hello, следующие команды:

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

Сборки hello с помощью следующих команд hello пользовательский модуль IoT Edge:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

скрипт сборки Hello помещает пользовательский модуль IoT Edge hello libsensor2remotemonitoring.so в папке построения hello.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Настройка и запуск hello IoT шлюз

Теперь можно настроить hello IoT пограничного шлюза toosend телеметрии из вашего SensorTag устройства tooyour удаленного мониторинга. Дополнительные сведения о настройке шлюза и модулей Edge Интернета вещей см. в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-gateway-concepts].

> [!TIP]
> В этом учебнике используется стандарт hello `vi` текстового редактора hello Intel NUC. Если вы не использовали `vi` ранее, следует выполнить Вводное руководство, такие как [Unix - hello vi учебник редактора] [ lnk-vi-tutorial] toofamiliarize самостоятельно с помощью этого редактора. Кроме того, можно установить более удобный hello [nano](https://www.nano-editor.org/) редактора с помощью команды hello `smart install nano -y`.

Привет открыть образец файла конфигурации в hello **vi** редактора с помощью hello следующую команду:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

Найдите следующие строки в hello конфигурации для модуля центром IOT hello hello:

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

Замените заполнитель hello значениями hello сведения центр IoT был создан и сохранен в hello запуск этого учебника. значение Hello IoTHubName выглядит как **yourrmsolution37e08**, а hello IoTSuffix равно обычно **azure devices.net**.

Найдите следующие строки в hello конфигурации для модуля сопоставления hello hello:

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Замените hello **macAddress** заполнитель hello MAC-адрес вашего SensorTag было сказано ранее. Замените hello **deviceID** и **deviceKey** местозаполнителей hello идентификаторы и ключи для hello два устройства, вы создали в решение для удаленного мониторинга hello.

Найдите следующие строки в hello конфигурации для модуля SensorTag hello hello:

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

Замените hello **устройства\_mac\_адрес** заполнитель hello MAC-адрес вашего SensorTag было сказано ранее.

Сохраните изменения.

Теперь можно выполнить с помощью следующих команд hello шлюза hello:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

Hello IoT шлюзом начинается hello Intel NUC и отправляет данные телеметрии из hello SensorTag toohello удаленного мониторинга решения:

![IoT шлюз отправляет данные телеметрии из hello SensorTag][img-telemetry]

Нажмите клавишу **Ctrl-C** tooexit программа hello в любое время.

## <a name="view-hello-telemetry"></a>Представление hello телеметрии

шлюз Hello теперь отправляет данные телеметрии из hello SensorTag toohello удаленного мониторинга устройствами. Hello телеметрии можно просмотреть на панели мониторинга hello решения. Можно также отправлять команды tooyour SensorTag устройства через шлюз hello из панели мониторинга hello решения.

- Перейдите в панель мониторинга toohello решения.
- Выберите hello устройства, настроенные в hello шлюза, который представляет hello SensorTag в hello **tooView устройства** раскрывающегося списка.
- Hello телеметрии с hello SensorTag устройства отображаются на панели мониторинга hello.

![Отобразить данные телеметрии с устройств SensorTag hello][img-telemetry-display]

> [!WARNING]
> Если оставить hello удаленное наблюдение решение, работающее в учетной записи Azure, взимается плата за hello выполнения задания. Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config]. Удаление hello предварительно настроенное решение из учетной записи Azure, после завершения его использования.


## <a name="next-steps"></a>Дальнейшие действия

Посетите hello [Центр разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/) Дополнительные примеры и документация по Azure IoT.

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started