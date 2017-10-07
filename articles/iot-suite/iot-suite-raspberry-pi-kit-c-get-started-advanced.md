---
title: "обновляет IoT Suite, с помощью встроенного по toosupport C aaaConnect tooAzure Raspberry Pi | Документы Microsoft"
description: "Используйте hello Microsoft Azure IoT начального набора для hello Raspberry Pi 3 и Azure IoT Suite. Использовать C tooconnect вашей Raspberry Pi toohello удаленного решением для мониторинга, отправка данных телеметрии с датчиками toohello облака и обновления удаленного встроенного."
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
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a>Подключение toohello вашей Raspberry Pi 3 удаленного решением для мониторинга и включить обновление удаленного встроенного по, с помощью C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

В этом учебнике показано, как toouse hello Microsoft Azure IoT начального набора для 3 Raspberry Pi, чтобы:

* Разработка температуры и влажности чтения, которая может обмениваться данными с облаком hello.
* Включить и выполнять клиентское приложение hello tooupdate обновления удаленного встроенного по на hello Raspberry Pi.

Hello учебнике используется:

* Raspbian ОС, язык программирования hello C и hello пакета SDK Microsoft Azure IoT для C tooimplement устройство образца.
* удаленный мониторинг Hello IoT Suite предварительно настроить решение в hello облачной серверной части.

## <a name="overview"></a>Обзор

В этом учебнике необходимо выполнить следующие шаги hello.

* Разверните экземпляр hello удаленного мониторинга предварительно настроенных решений tooyour подписки Azure. На этом шаге автоматически разворачивается и настраивается несколько служб Azure.
* Настройка вашего устройства и датчики toocommunicate на компьютер и hello удаленного решением для мониторинга.
* Обновите hello образец кода tooconnect toohello удаленного мониторинга устройствами и отправлять данные телеметрии, можно просмотреть на панели мониторинга hello решения.
* Используйте hello образец кода устройства tooupdate hello клиентского приложения.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hello удаленного мониторинга решения подготавливает набор служб Azure в подписке Azure. Развертывание Hello отражает реальные корпоративной архитектуре. плата tooavoid ненужные использование Azure, удаление экземпляра hello предварительно настроенное решение в azureiotsuite.com после завершения с ним. Если предварительно настроенных решений требуется hello еще раз, то ее можно легко восстановить. Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Загрузить и настроить образец hello

Теперь можно загрузить и настроить hello удаленного мониторинга клиентского приложения на ваш Raspberry Pi.

### <a name="clone-hello-repositories"></a>Клонирование репозиториев hello

Если вы еще не сделали этого, клон hello необходимые hello репозиториев, выполнив следующие команды на ваш Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Обновление строки подключения устройства hello

Привет открыть образец файла конфигурации в hello **nano** редактора с помощью hello следующую команду:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

Замените значения заполнителей hello hello идентификатор и центр IoT сведений об устройстве был создан и сохранен в начале этого учебника hello.

Когда вы закончите, hello содержимое файла deviceinfo hello должен выглядеть hello в следующем примере:

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

Сохранить изменения (**Ctrl-O**, **ввод**) и редактор hello выхода (**Ctrl-X**).

## <a name="build-hello-sample"></a>Построение образца hello

Если вы еще не сделали установите hello пакеты необходимых компонентов для hello IoT устройство Microsoft Azure SDK для C, выполнив следующие команды в конечном на hello Raspberry Pi hello:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

Теперь можно построить образец решения hello на hello Raspberry Pi:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

Теперь можно запустить образец hello программы для hello Raspberry Pi. Введите команду hello:

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

Hello следующий результат приводится пример hello выходные данные, отображаемые на hello Raspberry Pi hello командной строке:

![Выходные данные приложения Raspberry Pi][img-raspberry-output]

Нажмите клавишу **Ctrl-C** tooexit программа hello в любое время.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. В панели мониторинга hello решение, нажмите кнопку **устройств** toovisit hello **устройств** страницы. Выберите ваш Pi Raspberry в hello **список устройств**. Затем выберите **Методы**:

    ![Список устройств на панели мониторинга][img-list-devices]

1. На hello **вызвать метод** выберите **InitiateFirmwareUpdate** в hello **метод** раскрывающегося списка.

1. В hello **FWPackageURI** введите **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**. Этот архив содержит реализацию hello версии 2.0 hello встроенного по.

1. Выберите **InvokeMethod**. приложение Hello на hello Raspberry Pi отправляет подтверждение задней toohello решений мониторинга. Затем она запускает процесс обновления встроенного по hello путем загрузки новой версии встроенного по hello hello:

    ![Просмотр журнала методов][img-method-history]

## <a name="observe-hello-firmware-update-process"></a>Контролировать процесс обновления встроенного по hello

Можно наблюдать hello процесс обновления встроенного по, во время их выполнения на устройстве hello и просмотрев hello сообщил свойств в панели мониторинга hello решения:

1. Можно просмотреть ход выполнения hello в процесс обновления hello на hello Raspberry Pi:

    ![Отображение хода выполнения обновления][img-update-progress]

    > [!NOTE]
    > удаленного мониторинга приложение Hello автоматически перезагружается после завершения обновления hello. Команда hello `ps -ef` tooverify его выполнения. Процесс tooterminate hello, используйте hello `kill` команду с идентификатором hello.

1. Состояние hello hello обновление встроенного по, можно просмотреть, сообщаемые hello устройства, на портале решения hello. Hello следующем снимке экрана показано состояние hello и длительность каждого этапа процесса обновления hello и hello новой версии встроенного по:

    ![Отображение состояния задания][img-job-status]

    При переходе назад toohello панели мониторинга можно убедитесь, что устройство hello продолжает посылать телеметрии следующее обновление встроенного по hello.

> [!WARNING]
> Если оставить hello удаленное наблюдение решение, работающее в учетной записи Azure, взимается плата за hello выполнения задания. Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config]. Удаление hello предварительно настроенное решение из учетной записи Azure, после завершения его использования.

## <a name="next-steps"></a>Дальнейшие действия

Посетите hello [Центр разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/) Дополнительные примеры и документация по Azure IoT.


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md