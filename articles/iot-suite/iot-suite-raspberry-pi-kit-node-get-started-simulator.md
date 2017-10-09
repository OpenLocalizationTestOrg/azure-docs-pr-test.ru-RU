---
title: "aaaConnect tooAzure Raspberry Pi IoT Suite с помощью Node.js с имитацию телеметрии | Документы Microsoft"
description: "Используйте hello Microsoft Azure IoT начального набора для hello Raspberry Pi 3 и Azure IoT Suite. Использовать Node.js tooconnect toohello вашей Raspberry Pi удаленного решением для мониторинга, отправить облака toohello имитацию телеметрии и отвечать toomethods из панели мониторинга hello решения."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a>Подключения вашей Raspberry Pi 3 toohello удаленного решением для мониторинга и отправки смоделированные данные телеметрии с помощью Node.js

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Этом учебнике показано, как hello toouse Raspberry Pi 3 toosimulate температуры и влажности данных toosend toohello облако. Hello учебнике используется:

- ОС Raspbian hello Node.js языка программирования и hello Microsoft Azure IoT SDK для Node.js tooimplement устройства образца.
- удаленный мониторинг Hello IoT Suite предварительно настроить решение в hello облачной серверной части.

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hello удаленного мониторинга решения подготавливает набор служб Azure в подписке Azure. Развертывание Hello отражает реальные корпоративной архитектуре. плата tooavoid ненужные использование Azure, удаление экземпляра hello предварительно настроенное решение в azureiotsuite.com после завершения с ним. Если предварительно настроенных решений требуется hello еще раз, то ее можно легко восстановить. Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a>Загрузить и настроить образец hello

Теперь можно загрузить и настроить hello удаленного мониторинга клиентского приложения на ваш Raspberry Pi.

### <a name="install-nodejs"></a>Установка Node.js

Установите Node.js на устройстве Raspberry Pi, если вы это еще не сделали. Hello IoT пакет SDK для Node.js требует 0.11.5 Node.js или более поздней версии. Hello следующие шаги показывают, как tooinstall v6.10.2 Node.js на ваш Pi Raspberry:

1. Используйте hello следующая команда tooupdate вашей Pi Raspberry:

    ```sh
    sudo apt-get update
    ```

1. Используйте следующие двоичные файлы Node.js tooyour Raspberry Pi команда toodownload hello hello.

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Используйте следующие двоичные файлы hello tooinstall команда hello.

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Используйте hello следующая команда tooverify установки Node.js v6.10.2 успешно:

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a>Клонирование репозиториев hello

Если это еще не сделано, клон hello требуемые hello репозиториев, выполнив следующие команды в конечном на ваш Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Обновление строки подключения устройства hello

Привет открыть образец исходного файла в hello **nano** редактора с помощью hello следующую команду:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

Найдите строку hello:

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

Замените значения заполнителей hello и информации центр IoT был создан и сохранен в начале этого учебника hello hello устройства. Сохранить изменения (**Ctrl-O**, **ввод**) и редактор hello выхода (**Ctrl-X**).

## <a name="run-hello-sample"></a>Запуск образца hello

Выполнения hello следующими командами tooinstall hello пакеты необходимых компонентов для образца hello:

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

Теперь можно запустить образец hello программы для hello Raspberry Pi. Введите команду hello:

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

Hello следующий результат приводится пример hello выходные данные, отображаемые на hello Raspberry Pi hello командной строке:

![Выходные данные приложения Raspberry Pi][img-raspberry-output]

Нажмите клавишу **Ctrl-C** tooexit программа hello в любое время.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a>Дальнейшие действия

Посетите hello [Центр разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/) Дополнительные примеры и документация по Azure IoT.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
