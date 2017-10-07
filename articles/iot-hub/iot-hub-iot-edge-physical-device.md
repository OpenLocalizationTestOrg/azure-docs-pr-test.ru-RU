---
title: "aaaUse физического устройства в Azure IoT Edge | Документы Microsoft"
description: "Как toouse SensorTag инструментов Техас устройства toosend данных tooan центр IoT через IoT шлюзом, запущенного на устройстве Raspberry Pi 3. шлюз Hello построен с использованием Azure IoT Edge."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a>Преимущества использования Azure IoT tooIoT сообщения из устройства в облако tooforward Raspberry Pi концентратора

В этом пошаговом руководстве для hello [образец низкого энергопотребления Bluetooth] [ lnk-ble-samplecode] показано, как toouse [Azure IoT Edge] [ lnk-sdk] для:

* Устройства в облако телеметрии tooIoT концентратора вперед от физического устройства.
* Команды маршрута из центра IoT tooa физического устройства.

В этом руководстве рассматриваются следующие темы.

* **Архитектура**: важные сведения об низкого энергопотребления образец hello Bluetooth.
* **Построение и запуск**: пример hello выполнения и toobuild необходимые шаги hello.

## <a name="architecture"></a>Архитектура

Hello пошаговом руководстве показано, как toobuild и выполнения IoT шлюз на Pi Raspberry 3, которое будет выполняться Raspbian Linux. шлюз Hello построен с использованием IoT Edge. Образец Hello использует данных температуры toocollect устройства энергии низкий Техас инструментов SensorTag Bluetooth (Разрешить).

При запуске hello IoT шлюзом его:

* Подключение устройства SensorTag tooa, с помощью протокола hello энергии низкий Bluetooth (Разрешить).
* TooIoT концентратора подключается с использованием протокола hello HTTP.
* Передает данные телеметрии из hello SensorTag устройства tooIoT концентратора.
* Направляет команды из центра IoT toohello SensorTag устройства.

шлюз Hello содержит следующие модули IoT Edge hello:

* Объект *ЛЮЧИТЬ модуль* , взаимодействующего с tooreceive температуры ЛЮЧИТЬ устройства данных из hello и устройством toohello команды send.
* Объект *ЛЮЧИТЬ облака toodevice модуль* , преобразующий сообщения JSON, отправленные из центра IoT в инструкции ЛЮЧИТЬ для hello *ЛЮЧИТЬ модуля*.
* Объект *модуль ведения журнала* , регистрирует все шлюза сообщений tooa локального файла.
* *Модуль сопоставления удостоверений* , который преобразовывает MAC-адреса устройств BLE и удостоверения устройств центра Azure IoT.
* *Центр IoT модуль* , отправляет центр IoT tooan данных телеметрии и получает команды от центра IoT.
* Объект *ЛЮЧИТЬ принтера модуль* , интерпретирует данные телеметрии с устройства ЛЮЧИТЬ hello и печатает форматированные данные toohello консоли tooenable неполадок и отладка.

### <a name="how-data-flows-through-hello-gateway"></a>Потоки данных через шлюз hello

Следующая блок-схема Hello показано конвейера потока данных передачи телеметрии hello.

![Конвейер шлюза отправки данных телеметрии](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

Привет, который принимает элемент телеметрии проходящих из tooIoT отключить устройство концентратора, необходимо:

1. Отключить устройство Hello создает образец температуры и отправляет его по модуль ЛЮЧИТЬ toohello Bluetooth на шлюзе hello.
1. модуль ЛЮЧИТЬ Hello Получает образец hello и публикует его broker toohello вместе с hello MAC-адрес устройства hello.
1. модуль сопоставления удостоверений Hello принимает это сообщение и использует внутреннюю таблицу tootranslate hello MAC-адрес устройства hello в центр IoT удостоверение устройства. Удостоверение устройства Центра Интернета вещей состоит из идентификатора и ключа устройства.
1. модуль сопоставления удостоверений Hello публикует новое сообщение, которое содержит образец hello температур, hello MAC-адрес устройства hello, идентификатор устройства hello и ключ устройства hello.
1. Hello центра IoT модуль получает это новое сообщение (создаваемые модулем сопоставления удостоверений hello) и публикует его tooIoT концентратора.
1. модуль ведения журнала Hello заносит в журнал все сообщения из локального файла hello broker tooa.

Следующая блок-схема Hello показано конвейера потока данных команда устройства hello.

![Конвейер шлюза команд устройства](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. Центр IoT модуль периодически опрашивает Hello hello центр IoT для новых командных сообщений.
1. Получив команду новое сообщение hello центра IoT модуля он публикуется toohello broker.
1. модуль сопоставления удостоверений Hello сообщение hello команды и использование внутренней таблицы tootranslate hello центра IoT идентификатор tooa одноранговой MAC-адрес. Затем он публикует новое сообщение, которое включает в себя hello MAC-адрес целевого устройства hello в карту приветственное сообщение hello свойства.
1. модуль ЛЮЧИТЬ облака на устройство Hello воспринимает это сообщение и преобразует его в инструкции правильную ЛЮЧИТЬ hello hello ЛЮЧИТЬ модуля. Затем он публикует новое сообщение.
1. модуль ЛЮЧИТЬ Hello принимает это сообщение и выполнение инструкции hello ввода-вывода в связи с устройством ЛЮЧИТЬ hello.
1. модуль ведения журнала Hello заносит в журнал все сообщения из файла на диске tooa broker hello.

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника требуется Активная подписка Azure.

> [!NOTE]
> Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk-free-trial].

Требуется клиент SSH на tooenable на настольном компьютере, вы tooremotely доступ hello командную строку на hello Raspberry Pi.

- Windows не предоставляет клиент SSH. Мы советуем использовать [PuTTY](http://www.putty.org/).
- Большинство дистрибутивах Linux и Mac OS включают программу командной строки SSH hello. Дополнительные сведения см. в статье [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (Подключение по протоколу SSH с помощью Linux или Mac OS).

## <a name="prepare-your-hardware"></a>Подготовка оборудования

В этом учебнике предполагается, вы используете [SensorTag инструментов Техас](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) tooa Raspberry Pi 3 подключено устройство под управлением Raspbian.

### <a name="install-raspbian"></a>Установка Raspbian

Можно использовать либо hello следующие параметры tooinstall Raspbian на вашем устройстве Raspberry Pi 3.

* tooinstall hello последнюю версию Raspbian hello используйте [NOOBS] [ lnk-noobs] графического интерфейса пользователя.
* Вручную [загрузки] [ lnk-raspbian] и записать образ последнюю hello hello Raspbian операционной системы tooan SD-карты.

### <a name="sign-in-and-access-hello-terminal"></a>Вход и доступ к терминалов hello

У вас есть два tooaccess параметры терминалов среды с вашей пи Raspberry:

* Если клавиатура и отслеживать подключенных tooyour Raspberry Pi, можно использовать tooaccess Raspbian GUI hello окно терминала.

* Командная строка hello доступа на ваш Raspberry Pi, с помощью SSH из настольном компьютере.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Использование окна терминала в hello графического пользовательского интерфейса

имя пользователя, учетные данные по умолчанию Hello для Raspbian **pi** и пароль **raspberry**. На панели задач hello в hello графического пользовательского интерфейса, можно запустить hello **терминалов** hello значок, который выглядит как монитор с помощью служебной программы.

#### <a name="sign-in-with-ssh"></a>Вход с помощью SSH

Можно использовать SSH для командной строки доступ tooyour Raspberry Pi. статья Hello [SSH (Secure Shell)] [ lnk-pi-ssh] описывает как tooconfigure SSH с вашей пи Raspberry и как tooconnect из [Windows] [ lnk-ssh-windows] или [Linux и Mac OS][lnk-ssh-linux].

Войдите, используя имя пользователя **pi** и пароль **raspberry**.

### <a name="install-bluez-537"></a>Установка BlueZ 5.37

модули ЛЮЧИТЬ Hello поговорим оборудования Bluetooth toohello через стек BlueZ hello. Необходима версия 5.37 BlueZ для hello модули toowork правильно. Эти инструкции убедитесь, что установлена правильная версия BlueZ hello.

1. Остановка текущего bluetooth демон hello:

    ```sh
    sudo systemctl stop bluetooth
    ```

1. Установка зависимостей BlueZ hello:

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. Загрузите bluez.org hello BlueZ исходный код:

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. Распакуйте hello исходный код:

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. Изменить папку toohello вновь созданные каталоги:

    ```sh
    cd bluez-5.37
    ```

1. Настройте hello BlueZ кода toobe построения:

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. Выполните сборку BlueZ:

    ```sh
    make
    ```

1. По завершении сборки установите BlueZ:

    ```sh
    sudo make install
    ```

1. Изменение конфигурации службы systemd для bluetooth, теперь он указывает toohello новый демон bluetooth в файле hello `/lib/systemd/system/bluetooth.service`. Замените строку «ExecStart» hello hello следующий текст:

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a>Включить устройство SensorTag toohello подключения с устройства Raspberry Pi 3

Для выполнения образца hello требуется tooverify, что ваш Pi 3 Raspberry подключить устройство SensorTag toohello.

1. Убедитесь, hello `rfkill` служебная программа устанавливается:

    ```sh
    sudo apt-get install rfkill
    ```

1. Разблокировать bluetooth на hello Raspberry Pi 3 и проверьте номер версии hello **5.37**:

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. оболочка интерактивный bluetooth tooenter hello, запустите службу hello bluetooth и выполнения hello **bluetoothctl** команды:

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Введите команду hello **включения питания** toopower hello bluetooth контроллера. Команда Hello возвращает аналогичные toohello следующие выходные данные:

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. В оболочке интерактивный bluetooth hello, введите команду hello **сканирования на** tooscan для устройствами bluetooth. Команда Hello возвращает аналогичные toohello следующие выходные данные:

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. Сделать доступной для обнаружения устройств SensorTag hello и нажав кнопку небольшой hello (приветствия мигания зеленый Индикатор). Hello Raspberry Pi 3 должны обнаруживать устройства SensorTag hello:

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    В этом примере видно, hello MAC-адрес hello устройство SensorTag **A0:E6:F8:B5:F6:00**.

1. Отключение сканирования, введя hello **сканирования** команды:

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. Подключите устройство SensorTag tooyour с помощью его MAC-адрес, введя **подключения \<MAC-адрес\>**. для ясности является сокращенным Hello следующий образец вывода:

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > Вы можете вывести список характеристик GATT hello hello устройства, еще раз, используя hello **атрибуты списка** команды.

1. Теперь можно отключить с помощью hello устройства hello **отключения** команды и выйдите из оболочки hello bluetooth, с помощью hello **quit** команды:

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

Теперь вы готовы toorun hello ЛЮЧИТЬ IoT Edge образец на Pi вашей Raspberry 3.

## <a name="run-hello-iot-edge-ble-sample"></a>Запуск образца hello ЛЮЧИТЬ Edge IoT

toorun hello IoT Edge ЛЮЧИТЬ образец необходимо toocomplete трех задач:

* Настроить два примера устройств в центре IoT.
* Создать Edge Интернета вещей на устройстве Raspberry Pi 3.
* Настройки и запуска образца ЛЮЧИТЬ hello на вашем устройстве Raspberry Pi 3.

На момент написания статьи hello край IoT поддерживает только модули ЛЮЧИТЬ в шлюзы, выполняемым на платформе Linux.

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>Настройка двух примеров устройств в центре IoT

* [Создать центр IoT] [ lnk-create-hub] в вашей подписке Azure необходимо имя вашей toocomplete концентратора hello в данном пошаговом руководстве. Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.
* Добавьте одно устройство называется **SensorTag_01** tooyour центр IoT и запомните или запишите его идентификатор и устройства ключ. Можно использовать hello [обозреватель устройств или обозревателе центром IOT] [ lnk-explorer-tools] средств tooadd этот центр IoT toohello устройства, созданные в предыдущем шаге hello и tooretrieve его ключ. При настройке шлюза hello сопоставлении этого устройства SensorTag toohello устройства.

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>Создание Edge Интернета вещей Azure на устройстве Raspberry Pi 3

Установите зависимые компоненты Edge Интернета вещей Azure:

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

Используйте hello следующими командами tooclone IoT края и все его подмодулей tooyour домашний каталог:

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

При наличии полную копию hello IoT Edge репозитория на Pi вашей Raspberry 3 можно создать ее с помощью hello следующую команду из папки hello, содержащий hello SDK:

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a>Настройки и запуска образца hello ЛЮЧИТЬ на Pi вашей Raspberry 3

Пример выполнения hello и toobootstrap, необходимо настроить каждый модуль IoT Edge, участвующего в hello шлюза. Необходимая конфигурация предоставляется в файле JSON. Вам следует настроить все пять участвующих модулей Edge Интернета вещей. Имеется пример JSON-файла в репозитории hello вызывается **шлюза\_sample.json** , можно использовать в качестве hello, начальной точкой для создания файла конфигурации. Этот файл расположен в hello **образцы, ble_gateway/src** папки в локальной копии hello IoT Edge репозитория.

Hello ниже описано, как tooedit этой конфигурации файла для образца hello ЛЮЧИТЬ и предполагается, hello репозитория IoT Edge возможности hello **/home/pi/iot-edge /** папку на Pi вашей Raspberry 3. Если репозиторий hello в другом месте, соответствующим образом настройте hello пути.

#### <a name="logger-configuration"></a>Конфигурация средства ведения журнала

При условии, что репозитория hello шлюз находится в hello **/home/pi/iot-edge /** папки, настройте модуль ведения журнала hello следующим образом:

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a>Конфигурация модуля BLE

Hello пример конфигурации для устройства ЛЮЧИТЬ hello предполагается SensorTag Техас инструментов устройства. Все стандартные отключить устройство, может работать как GATT периферийных устройств должны работать, но может потребоваться tooupdate hello GATT характеристика идентификаторов и данных. Добавьте hello MAC-адрес устройства SensorTag:

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

Если устройство SensorTag не используются, документации hello вашей toodetermine отключить устройство, нужны ли вам tooupdate hello GATT характеристика идентификаторы и значения данных.

#### <a name="iot-hub-module"></a>Модуль Центра Интернета вещей

Добавьте имя вашего центра IoT hello. обычно является значение суффикса Hello **azure devices.net**:

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a>Конфигурация модуля сопоставления удостоверений

Добавить MAC-адрес hello SensorTag устройства, а идентификатор устройства hello и ключ hello **SensorTag_01** устройство, добавленное tooyour центр IoT:

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a>Конфигурация модуля принтера BLE

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a>Конфигурация модуля BLEC2D

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a>Конфигурация маршрутизации

Hello ниже конфигурация обеспечивает следующие hello маршрутизации между модулями IoT Edge:

* Hello **средства ведения журнала** модуль получает и регистрирует все сообщения.
* Hello **SensorTag** модуль отправляет сообщения hello tooboth **сопоставления** и **принтера ЛЮЧИТЬ** модулей.
* Hello **сопоставления** модуль отправляет сообщения toohello **центром IOT** toobe модуль отправлялось tooyour центр IoT.
* Hello **центром IOT** модуль отправляет сообщений обратно toohello **сопоставления** модуля.
* Hello **сопоставления** модуль отправляет сообщения toohello **BLEC2D** модуля.
* Hello **BLEC2D** модуль отправляет сообщений обратно toohello **тег датчика** модуля.

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

Образец hello toorun, передайте hello путь toohello файл конфигурации JSON как toohello параметр **жбы\_шлюза** двоичный. Hello следующая команда предполагает вы используете hello **gateway_sample.json** файла конфигурации. Выполните эту команду из hello **iot edge** папку на hello Raspberry Pi:

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

Может потребоваться toopress hello небольшой кнопку на устройстве toomake hello SensorTag ее доступной для обнаружения перед запуском образца hello.

При запуске образца hello, можно использовать hello [обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) или hello [explorer центром IOT](https://github.com/Azure/iothub-explorer) средство toomonitor hello сообщений hello IoT шлюз пересылает hello SensorTag устройства. Например с помощью обозревателя с центром IOT можно отслеживать сообщения устройства в облако, с помощью hello следующую команду:

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>Отправка сообщений из облака на устройство

Hello ЛЮЧИТЬ модуль также поддерживает отправку команды из центра IoT toohello устройства. Можно использовать hello [обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) или hello [explorer центром IOT](https://github.com/Azure/iothub-explorer) сообщений JSON toosend средство модуля шлюза ЛЮЧИТЬ hello перенаправляет на устройстве ЛЮЧИТЬ toohello.

Если вы используете устройство SensorTag инструментов Техас hello, можно включить Индикатор hello красный, зеленый Индикатор или звукового сигнала путем отправки команды из центра IoT. Прежде чем отправлять команды из центра IoT, сначала отправьте hello, следующие два сообщения JSON в порядке. Затем можно отправить hello tooturn команды на индикаторы hello или звукового сигнала.

1. Сбросьте все индикаторы и звукового сигнала hello (отключены):

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. Настройте операции ввода-вывода как "удаленные".

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

Теперь можно отправить после команды tooturn на индикаторы hello и звукового сигнала на устройстве SensorTag hello hello:

* Включите hello красный Индикатор.

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* Включите hello зеленый Индикатор:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* Включите hello звукового сигнала.

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>Дальнейшие действия

Toogain более глубоким пониманием IoT края и поэкспериментировать с примерами кода, посетите следующие hello разработчика учебники и ресурсы:

* [Azure IoT Edge][lnk-sdk] (Edge Интернета вещей Azure).

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Руководство разработчика для Центра Интернета вещей][lnk-devguide]

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
