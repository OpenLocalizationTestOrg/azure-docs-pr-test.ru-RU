---
title: "aaaConnect tooAzure Raspberry Pi IoT Suite с помощью C с реальными датчики | Документы Microsoft"
description: "Используйте hello Microsoft Azure IoT начального набора для hello Raspberry Pi 3 и Azure IoT Suite. Использовать C tooconnect вашей Raspberry Pi toohello удаленного решением для мониторинга, отправка данных телеметрии с датчиками toohello облака и отвечать toomethods из панели мониторинга hello решения."
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
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a>Подключения вашей Raspberry Pi 3 toohello удаленного решением для мониторинга и отправка данных телеметрии с реальными датчика с помощью C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Этот учебник показывает, как toouse hello Microsoft Azure IoT начального набора для toodevelop Raspberry Pi 3 температуры и влажности чтения, которая может обмениваться данными с облаком hello. Hello учебнике используется:

- Raspbian ОС, язык программирования hello C и hello пакета SDK Microsoft Azure IoT для C tooimplement устройство образца.
- удаленный мониторинг Hello IoT Suite предварительно настроить решение в hello облачной серверной части.

## <a name="overview"></a>Обзор

В этом учебнике необходимо выполнить следующие шаги hello.

- Разверните экземпляр hello удаленного мониторинга предварительно настроенных решений tooyour подписки Azure. На этом шаге автоматически разворачивается и настраивается несколько служб Azure.
- Настройка вашего устройства и датчики toocommunicate на компьютер и hello удаленного решением для мониторинга.
- Обновите hello образец кода tooconnect toohello удаленного мониторинга устройствами и отправлять данные телеметрии, можно просмотреть на панели мониторинга hello решения.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hello удаленного мониторинга решения подготавливает набор служб Azure в подписке Azure. Развертывание Hello отражает реальные корпоративной архитектуре. плата tooavoid ненужные использование Azure, удаление экземпляра hello предварительно настроенное решение в azureiotsuite.com после завершения с ним. Если предварительно настроенных решений требуется hello еще раз, то ее можно легко восстановить. Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Загрузить и настроить образец hello

Теперь можно загрузить и настроить hello удаленного мониторинга клиентского приложения на ваш Raspberry Pi.

### <a name="clone-hello-repositories"></a>Клонирование репозиториев hello

Если это еще не сделано, клон hello требуемые hello репозиториев, выполнив следующие команды в конечном на ваш Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a>Обновление строки подключения устройства hello

Привет открыть образец исходного файла в hello **nano** редактора с помощью hello следующую команду:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

Найдите hello следующие строки:

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

Замените значения заполнителей hello и информации центр IoT был создан и сохранен в начале этого учебника hello hello устройства. Сохранить изменения (**Ctrl-O**, **ввод**) и редактор hello выхода (**Ctrl-X**).

## <a name="build-hello-sample"></a>Построение образца hello

Установите hello пакеты необходимых компонентов для hello IoT устройство Microsoft Azure SDK для C, выполнив следующие команды в конечном на hello Raspberry Pi hello:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

Теперь можно построить образец hello обновление решения на hello Raspberry Pi:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

Теперь можно запустить образец hello программы для hello Raspberry Pi. Введите команду hello:

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

Hello следующий результат приводится пример hello выходные данные, отображаемые на hello Raspberry Pi hello командной строке:

![Выходные данные приложения Raspberry Pi][img-raspberry-output]

Нажмите клавишу **Ctrl-C** tooexit программа hello в любое время.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a>Дальнейшие действия

Посетите hello [Центр разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/) Дополнительные примеры и документация по Azure IoT.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
