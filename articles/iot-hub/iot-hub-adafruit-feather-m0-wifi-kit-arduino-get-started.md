---
title: "M0 toocloud: подключение Wi-Fi M0 Растушевка tooAzure центр IoT | Документы Microsoft"
description: "Узнайте, как tooset Настройка и подключение Wi-Fi M0 Растушевка Adafruit tooAzure центр IoT toosend данные toohello Azure облачной платформы в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a>Подключения Wi-Fi M0 Растушевка Adafruit tooAzure центр IoT в облаке hello
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Подключение между датчиком BME280, платой Feather M0 WiFi и Центром Интернета вещей](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

В этом учебнике сначала обучения hello основы работы с Arduino доске. Затем вы узнаете, как tooseamlessly подключаться toohello облачных устройств с помощью [центр IoT Azure](iot-hub-what-is-iot-hub.md).

## <a name="what-you-do"></a>В рамках этого руководства мы:

Подключите центра IoT tooan Adafruit Растушевка M0 WiFi, создаваемом. Затем запустите пример приложения на M0 Wi-Fi toocollect hello температуры и влажности данных из BME280. Отправьте центра IoT tooyour данных датчика hello.


## <a name="what-you-learn"></a>Что вы узнаете

* Как toocreate центр IoT и регистрация устройства для Растушевка M0 Wi-Fi
* Как tooconnect Растушевка M0 Wi-Fi с датчика hello и компьютера
* Как toocollect датчиков, выполнив пример приложения на Растушевка M0 Wi-Fi
* Как toosend hello центра IoT tooyour данных датчика

## <a name="what-you-need"></a>Необходимые элементы

![Детали, необходимые для работы с руководством hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete этой операции требуется hello следующую частей из начального набора Растушевка M0 Wi-Fi:

* Hello плата Растушевка M0 Wi-Fi
* Micro USB tooType USB-кабель

Также необходим hello следующие действия для среды разработки.

* Активная подписка Azure. Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.
* ПК или компьютер Mac под управлением Windows или Ubuntu;
* Беспроводная сеть Wi-Fi M0 Растушевка tooconnect для.
* Подключение toodownload hello конфигурации средств Интернета.
* [Arduino IDE](https://www.arduino.cc/en/main/software) версии 1.6.8 или более новой. Более ранних версий не работают с библиотекой hello центр IoT Azure.

Если у вас нет датчика, hello следующие элементы являются необязательными. Также имеется возможность использовать имитацию датчиков hello:

* Датчик температуры и влажности BME280
* Монтажная плата
* Многомодовый оптоволоконный кабель с разъемами на обоих концах

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a>Подключения Wi-Fi M0 Растушевка датчика hello и компьютера
В этом разделе подключиться hello датчики tooyour платы. Затем можно подключить компьютер tooyour устройство для использования в будущем.

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a>Подключение DHT22 температуры и влажности датчика tooFeather M0 Wi-Fi

Используйте hello breadboard и перемычки проводов toomake hello подключение. Если у вас нет датчика, пропустите этот раздел, так как вместо него вы можете использовать симулированные данные.

![Справочные материалы по подключению](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


Для датчика ПИН-коды используйте hello после подключения:


| Начало (датчик)           | Конец (плата)            | Цвет кабеля   |
| -----------------------  | ---------------------- | ------------: |
| VDD (вывод 27A)            | 3V (вывод 3A)            | Красный кабель     |
| GND (вывод 29A)            | GND (вывод 6A)           | Черный кабель   |
| SCK (вывод 30A)            | SCK (вывод 12A)          | Желтый кабель  |
| SDO (вывод 31A)            | MI (вывод 14A)           | Белый кабель   |
| SDI (вывод 32A)            | M0 (вывод 13A)           | Синий кабель    |
| CS (вывод 33A)             | GPIO 5 (вывод 15J)       | Оранжевый кабель  |

Дополнительные сведения см. в статье [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) (Выходы датчика влажности, атмосферного давления и температуры Adafruit BME280) и [Adafruit Feather M0 WiFi Pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts) (Выводы платы Adafruit Feather M0 WiFi).



Теперь работающий датчик должен быть подключен к Feather M0 WiFi.

![Подключение DHT22 к Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a>Подключения Wi-Fi M0 Растушевка tooyour компьютера

Используется hello Micro USB tooType USB кабель tooconnect Wi-Fi M0 Растушевка tooyour компьютеров, как показано:

![Подключите компьютер tooyour Huzzah Растушевка](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Добавление разрешений для последовательного порта (только в Ubuntu)

Если вы используете Ubuntu, убедитесь, что у вас разрешения toooperate hello на hello USB порта из Растушевка M0 Wi-Fi. tooadd последовательный порт, выполните следующие действия:


1. В терминалов выполните следующие команды hello:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   При получении одного из hello следующие выходные данные:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Обратите внимание, что в выходных данных hello `uucp` или `dialout` — имя владельца группы hello hello USB-порту.

2. tooadd hello toohello группы пользователей, запустите hello следующую команду:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   В предыдущем шаге hello, получения имени владельца группы hello `<group-owner-name>`. `<username>` — это имя пользователя Ubuntu.

3. Для tooappear изменение hello выйдите из Ubuntu и снова войдите в нее.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Собирать данные датчиков и отправлять их tooyour центра IoT

В этом разделе рассказывается о том, как развернуть и запустить пример приложения на плате Feather M0 WiFi. Пример приложения Hello делает hello мигающий Индикатор на Растушевка M0 Wi-Fi. После этого он отправляет hello температуры и влажности собранные данные датчика tooyour hello BME280 центр IoT.

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a>Пример приложения hello из GitHub и подготовка hello Arduino интегрированной среды разработки

Пример приложения Hello находится на GitHub. Клонирование репозитория образец hello, который содержит пример приложения hello из GitHub. репозиторий образец hello tooclone, выполните следующие действия:

1. Откройте окно командной строки или терминала.

2. Go tooa папку hello образец приложения toobe хранятся.
3. Выполните следующую команду hello.

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a>Установить пакет hello для Растушевка M0 Wi-Fi в hello Arduino интегрированной среды разработки

1. Откройте папку hello, где хранится пример приложения hello.

2. Откройте файл app.ino hello в папке приложения hello в hello Arduino интегрированной среды разработки.

   ![Откройте пример приложения hello в интегрированной среде разработки Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. Нажмите кнопку **файл** > **предпочтения** (Windows или Linux) или **Arduino** > **предпочтения** (Mac) и скопируйте ее и Вставить hello следующую ссылку в hello **дополнительные URL-адреса диспетчера досок** в диалоговом окне приветствия предпочтения Arduino интегрированной среды разработки.
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. Нажмите кнопку **средства** > **плата** > **досок Manager**и установите hello `Arduino SAMD Boards` версии `1.6.2` или более поздней версии. 

1. Затем в том же окне hello, установите `Adafruit SAMD Boards` tooadd hello плата файл определения пакета.

   ![установлен пакет esp8266 Hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. Щелкните **Инструменты** > **Платы** > **Adafruit M0 WiFi**.

5. Установите драйверы (только для Windows). После подключения Wi-Fi M0 Растушевка, может потребоваться tooinstall драйвера. Нажмите кнопку [hello ссылку на веб-странице hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) установщик драйвера toodownload hello. Выполните hello действия tooinstall hello драйверы.

### <a name="install-necessary-libraries"></a>Установка необходимых библиотек

1. В hello Arduino IDE, щелкните **схематической** > **включают библиотеки** > **Управление библиотеками**.

2. Поиск hello следующие имена библиотек по одному. Для каждой найденной библиотеки щелкните **Установить**.

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. Вручную установите `Adafruit_WINC1500`. Go слишком[этот веб-сайт](https://github.com/adafruit/Adafruit_WINC1500) и нажмите кнопку **клон или загрузки** > **загрузить ZIP**. В вашей СРЕДЕ Arduino перейдите слишком**схематической** > **включают библиотеки** > **добавьте .zip библиотеки** и добавьте hello ZIP-файл.

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a>Используйте пример приложения hello, при отсутствии реальных BME280 датчика

При отсутствии реальных датчика BME280 пример приложения hello можно смоделировать температуры и влажности данных. tooset hello образец приложения toouse моделирования данных, выполните следующие действия.

1. Откройте hello `config.h` файла в hello `app` папки.

2. Найдите следующие строки кода hello и измените значение hello из `false` слишком`true`:

   ```c
   define SIMULATED_DATA true
   ```
   ![Настройка приложения toouse имитируемые hello примеров данных](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. Сохраните файл hello с `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a>Развертывание tooFeather приложения образец hello M0 Wi-Fi

1. В hello Arduino IDE, щелкните **средство** > **порт**и нажмите кнопку hello последовательного порта для Растушевка M0 Wi-Fi.

2. Нажмите кнопку **схематической** > **отправить** toobuild и развернуть tooFeather приложения образец hello M0 Wi-Fi.

### <a name="enter-your-credentials"></a>Ввод учетных данных

После успешного завершения передачи hello, выполните эти шаги tooenter учетные данные.

1. В hello Arduino IDE, щелкните **средства** > **последовательного монитор**.

2. В hello нижнем правом углу окна последовательной монитор hello, выберите **без завершения строк** в раскрывающемся списке hello слева hello.
3. Выберите **115200 бод** в hello раскрывающегося списка в правом hello.
4. В поле ввода hello вверху hello, введите hello следующую информацию, если вы задаваемые tooprovide и нажмите кнопку **отправки**:

   * Идентификатор SSID для подключения Wi-Fi.
   * Пароль Wi-Fi.
   * Строка подключения к устройству.

> [!Note]
> Hello учетные данные хранятся в hello EEPROM из Растушевка M0 Wi-Fi. Если вы нажмете кнопку Сброс hello hello плата Растушевка M0 Wi-Fi, пример приложения hello запросом tooerase hello сведения. Введите `Y` tooerase hello сведения. Появится сообщение hello tooprovide сведения еще раз.

### <a name="verify-that-hello-sample-application-is-running-successfully"></a>Убедитесь, что пример приложения hello успешно запущен

Если вы видите hello следующие выходные данные из окна последовательной монитор hello и hello мигающий Индикатор на M0 Растушевка Wi-Fi, пример приложения hello выполняется успешно:

![Окончательные выходные данные в интегрированной среде разработки Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a>Дальнейшие действия

Успешно подключен центра IoT tooyour Растушевка M0 Wi-Fi и отправленных центра IoT tooyour данных датчика захвачен hello. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

