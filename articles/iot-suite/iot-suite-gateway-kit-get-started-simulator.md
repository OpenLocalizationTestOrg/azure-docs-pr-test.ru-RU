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
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a>Подключения вашей Azure IoT пограничного шлюза toohello удаленное наблюдение предварительно настроенных решений и отправки имитацию телеметрии

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Этот учебник показывает, как toouse Azure IoT Edge toosimulate температуры и влажности toosend toohello удаленного мониторинга данных предварительно настроенных решений. Hello учебнике используется:

- Azure IoT Edge tooimplement пример шлюза.
- удаленный мониторинг Hello IoT Suite предварительно настроить решение в hello облачной серверной части.

## <a name="overview"></a>Обзор

В этом учебнике необходимо выполнить следующие шаги hello.

- Разверните экземпляр hello удаленного мониторинга предварительно настроенных решений tooyour подписки Azure. На этом шаге автоматически разворачивается и настраивается несколько служб Azure.
- Настройка toocommunicate устройства шлюза вашей Intel NUC, с компьютера и решение для удаленного мониторинга hello.
- Настройте hello IoT пограничного шлюза toosend смоделированные данные телеметрии, можно просмотреть на панели мониторинга hello решения.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hello удаленного мониторинга решения подготавливает набор служб Azure в подписке Azure. Развертывание Hello отражает реальные корпоративной архитектуре. плата tooavoid ненужные использование Azure, удаление экземпляра hello предварительно настроенное решение в azureiotsuite.com после завершения с ним. Если предварительно настроенных решений требуется hello еще раз, то ее можно легко восстановить. Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

Повторите предыдущие шаги tooadd hello второго устройства с помощью идентификатор устройства, например **device02**. Образец Hello отправляет данные из двух имитацию устройств в hello toohello удаленного мониторинга решение шлюза.

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

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
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

скрипт сборки Hello помещает пользовательский модуль IoT Edge hello libsimulator.so в папке построения hello.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Настройка и запуск hello IoT шлюз

Теперь можно настроить hello IoT пограничного шлюза toosend имитацию телеметрии tooyour удаленного мониторинга. Дополнительные сведения о настройке шлюза и модулей Edge Интернета вещей см. в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-gateway-concepts].

> [!TIP]
> В этом учебнике используется стандарт hello `vi` текстового редактора hello Intel NUC. Если вы не использовали `vi` ранее, следует выполнить Вводное руководство, такие как [Unix - hello vi учебник редактора] [ lnk-vi-tutorial] toofamiliarize самостоятельно с помощью этого редактора. Кроме того, можно установить более удобный hello [nano](https://www.nano-editor.org/) редактора с помощью команды hello `smart install nano -y`.

Привет открыть образец файла конфигурации в hello **vi** редактора с помощью hello следующую команду:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
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

Замените hello **deviceID** и **deviceKey** местозаполнителей hello идентификаторы и ключи для hello два устройства, вы создали в решение для удаленного мониторинга hello.

Сохраните изменения.

Теперь можно запускать приветствия IoT шлюз с помощью hello следующие команды:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

шлюз Hello начинается hello Intel NUC и отправляет имитацию телеметрии toohello удаленного мониторинга решения:

![Создание смоделированной телеметрии в шлюзе Edge Интернета вещей][img-simulated telemetry]

Нажмите клавишу **Ctrl-C** tooexit программа hello в любое время.

## <a name="view-hello-telemetry"></a>Представление hello телеметрии

Hello IoT шлюзом теперь отправляет имитацию телеметрии toohello удаленного решение для мониторинга. Hello телеметрии можно просмотреть на панели мониторинга hello решения.

- Перейдите в панель мониторинга toohello решения.
- Выберите одно из устройств hello двух, настроенного в шлюзе hello в hello **tooView устройства** раскрывающегося списка.
- Hello телеметрии из шлюзов hello отображаются на панели мониторинга hello.

![Отобразить данные телеметрии из шлюзов имитируемые hello][img-telemetry-display]

> [!WARNING]
> Если оставить hello удаленное наблюдение решение, работающее в учетной записи Azure, взимается плата за hello выполнения задания. Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config]. Удаление hello предварительно настроенное решение из учетной записи Azure, после завершения его использования.

## <a name="next-steps"></a>Дальнейшие действия

Посетите hello [Центр разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/) Дополнительные примеры и документация по Azure IoT.

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started