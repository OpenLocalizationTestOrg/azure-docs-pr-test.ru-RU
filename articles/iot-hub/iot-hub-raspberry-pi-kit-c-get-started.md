---
title: "toocloud aaaRaspberry Pi (C) - подключения Pi Raspberry tooAzure центр IoT | Документы Microsoft"
description: "Узнайте, как toosetup и подключите Raspberry Pi tooAzure центр IoT для Raspberry Pi toosend данные toohello Azure облачной платформы в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot малиновая pi малиновая pi iot hub, малиновая pi отправки данных toocloud, малиновая pi toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a>Подключение Raspberry Pi tooAzure IoT Hub (C)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

В этом учебнике сначала hello основы работы с Raspberry Pi, на котором выполняется Raspbian обучения. Затем вы узнаете, как tooseamlessly подключаться toohello облачных устройств с помощью [центр IoT Azure](iot-hub-what-is-iot-hub.md). Примеры Windows 10 IoT базовая go toohello [центра разработчиков Windows](http://www.windowsondevices.com/).

Нет начального набора? Используйте [онлайн-симулятор Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md). Или купите новый комплект [здесь](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>В рамках этого руководства мы:

* Создайте Центр Интернета вещей.
* Зарегистрируем устройство для Pi в Центре Интернета вещей.
* Настроим Raspberry Pi.
* Запустите образец приложения на Pi toosend датчиков данных tooyour центр IoT.

Подключение центра IoT tooan Raspberry Pi созданного вами. Затем запустите пример приложения на Pi toocollect температуры и влажности данных с использованием BME280 датчиков. Отправьте центра IoT tooyour данных датчика hello.

## <a name="what-you-learn"></a>Что вы узнаете

* Как toocreate центр Azure IoT и получить новые строки подключения устройства.
* Как tooconnect числа пи с BME280 датчика.
* Как toocollect датчиков, выполнив пример приложения на Pi.
* Как центр IoT tooyour данных датчика toosend.

## <a name="what-you-need"></a>Необходимые элементы

![Необходимые элементы](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* Здравствуйте, Raspberry Pi 2 или Raspberry Pi 3 на доске.
* Активная подписка Azure. Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.
* Монитор, USB-клавиатуры и мыши подключаются tooPi.
* ПК или компьютер Mac под управлением Windows или Linux.
* Подключение к Интернету.
* Карта microSD емкостью 16 ГБ или больше.
* USB-SD адаптер или microSD карты tooburn hello образа операционной системы на карту microSD, hello.
* Питания 2 amp 5В с hello 6 фут micro USB-кабель.

Привет, следующие элементы являются необязательными.

* Датчик температуры, давления и влажности Adafruit BME280 в сборе.
* Монтажная плата.
* 6 оптоволоконных кабелей с разъемом на одном конце и гнездом на другом.
* Светодиодный индикатор 10 мм с рассеянным освещением.


> [!NOTE] 
Эти элементы являются необязательными, поскольку поддержка образец кода hello смоделированные данные датчиков.


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Настройка Raspberry Pi

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Установка операционной системы Raspbian hello для Pi

Подготовьте карта microSD hello для установки образа Raspbian hello.

1. Скачайте ОС Raspbian.
   1. [Загрузите детском Raspbian с рабочим столом](https://www.raspberrypi.org/downloads/raspbian/) (hello ZIP-файл).
   1. Извлеките hello Raspbian изображения tooa папку на локальном компьютере.
1. Установите карту microSD toohello Raspbian.
   1. [Загрузите и установите программу записи карты SD гравировальная hello](https://etcher.io/).
   1. Запустите гравировальная и выберите изображение Raspbian hello, извлеченный на шаге 1.
   1. Выберите диск, карту microSD hello. Обратите внимание, что гравировальная может уже выбран правильный диск hello.
   1. Щелкните карту microSD toohello Raspbian tooinstall флэш-памяти.
   1. Удаление карта microSD hello с компьютера после завершения установки. Это карта microSD безопасные tooremove hello непосредственно из-за гравировальная автоматически извлечение или отключение карта microSD hello после завершения.
   1. Вставьте карту microSD hello в Pi.

### <a name="enable-ssh-and-spi"></a>Включение SSH и SPI

1. Подключение Pi toohello монитора, клавиатуры и мыши, запустите Pi и затем войдите Raspbian с помощью `pi` имени пользователя hello и `raspberry` hello паролем.
1. Щелкните значок малиновая hello > **предпочтения** > **Raspberry Pi конфигурации**.

   ![меню настройки Raspbian Hello](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. На hello **интерфейсы** установите **SPI** и **SSH** слишком**включить**, а затем нажмите кнопку **ОК**. Если нет физических датчиков и toouse смоделированные данные датчика, этот шаг является необязательным.

   ![Включение SPI и SSH на Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH и SPI, можно найти дополнительные справочные документы на [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) и [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).

### <a name="connect-hello-sensor-toopi"></a>Подключение tooPi датчик hello

Используйте hello breadboard и перемычки проводов tooconnect Светодиодный индикатор и BME280 tooPi. Если у вас нет датчик hello [пропустите этот раздел](#connect-pi-to-the-network).

![Hello Raspberry Pi и датчик подключения](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

Датчик Hello BME280 можно собирать данные, температуры и влажности. И hello Индикатор мигает, при наличии связи между локальными устройствами и hello. 

Для датчика ПИН-коды используйте hello после подключения:

| Начало (датчик и светодиодный индикатор)     | Конец (плата)            | Цвет кабеля   |
| -----------------------  | ---------------------- | ------------: |
| LED VDD (вывод 5G)         | GPIO 4 (вывод 7)         | Белый кабель   |
| LED GND (вывод 6G)         | GND (вывод 6)            | Черный кабель   |
| VDD (вывод 18F)            | 3.3V PWR (вывод 17)      | Белый кабель   |
| GND (вывод 20F)            | GND (вывод 20)           | Черный кабель   |
| SCK (вывод 21F)            | SPI0 SCLK (вывод 23)     | Оранжевый кабель  |
| SDO (вывод 22F)            | SPI0 MISO (вывод 21)     | Желтый кабель  |
| SDI (вывод 23F)            | SPI0 MOSI (вывод 19)     | Зеленый кабель   |
| CS (вывод 24F)             | SPI0 CS (вывод 24)       | Синий кабель    |

Нажмите кнопку tooview [Raspberry Pi 2 и 3 ПИН-код сопоставления](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) для справки.

После успешного соединения BME280 tooyour Raspberry Pi должно быть как под изображением.

![Подключенный компьютер Pi и датчик BME280](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Подключение к сети toohello Pi

Включите Pi при помощи micro USB-кабель hello и hello питания. Используйте hello Ethernet кабель tooconnect Pi tooyour проводной сети, или выполните hello [инструкции hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour беспроводной сети. После вашей Pi было успешно выполнено подключение toohello сети, необходимо tootake заметку hello [IP-адрес вашего Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Toowired подключенной сети](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a>Запуск примера приложения на Pi

### <a name="install-hello-prerequisite-packages"></a>Установите пакеты необходимых компонентов hello

1. Используйте одну из hello следующую SSH клиентов из вашего узла компьютера tooconnect tooyour Raspberry Pi.
   
   **Пользователи Windows**
   1. Скачайте и установите [PuTTY](http://www.putty.org/) для Windows. 
   1. Скопируйте hello IP-адрес раздела Pi в hello узел имя (или IP-адрес) и выберите в качестве типа соединения hello SSH.
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   **Пользователи MAC и Ubuntu**
   
   Используйте встроенный клиент SSH hello Ubuntu или macOS. Может потребоваться toorun `ssh pi@<ip address of pi>` tooconnect Pi по протоколу SSH.
   > [!NOTE] 
   имя пользователя по умолчанию Hello `pi` , и пароль hello `raspberry`.

1. Установите пакеты необходимых компонентов hello для hello IoT устройство Microsoft Azure SDK для C и Cmake, выполнив hello, следующие команды:

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-hello-sample-application"></a>Настройка образца приложения hello

1. Пример приложения hello клона, выполнив следующую команду hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. Откройте файл конфигурации hello, запустив hello, следующие команды:

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Файл конфигурации](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   В этом файле можно настроить два макроса. Hello сначала он `INTERVAL`, который определяет hello временной интервал (в миллисекундах) между двумя сообщений, передаваемых toocloud. Здравствуйте, вторая — `SIMULATED_DATA`, — логическое значение для ли toouse смоделированные данные датчиков или нет.

   Если вы **нет hello датчика**, задайте hello `SIMULATED_DATA` значение слишком`1` пример приложения hello toomake создать и использовать имитацию датчиков.

1. Сохраните изменения и закройте окно, нажав клавиши Control-O > ВВОД > Control-X.

### <a name="build-and-run-hello-sample-application"></a>Построение и запуск образца приложения hello

1. Построение образца приложения hello, выполнив следующую команду hello:

   ```bash
   cmake . && make
   ```
   ![Выходные данные при создании](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. Выполните пример приложения hello, выполнив следующую команду hello:

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   Убедитесь, что вы скопированные и вставленные строки подключения устройств hello в одинарных кавычках hello.


Вы увидите следующее hello выходных данных, показано hello датчик данных и hello сообщений, отправляемых tooyour центр IoT.

![Вывод — данные датчика, отправленные из центра IoT tooyour Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a>Дальнейшие действия

Вы впервые запускаете в образце данных датчика toocollect приложения и отправьте его центр IoT tooyour. сообщения приветствия toosee, Pi вашей Raspberry отправленных IoT tooyour концентратор или отправки tooyour сообщений Raspberry Pi в интерфейс командной строки, в разделе hello [управление облака устройство обмен сообщениями с центром IOT учебнике](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
