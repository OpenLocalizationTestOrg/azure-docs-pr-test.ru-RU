---
title: "toocloud aaaESP8266 - tooAzure подключения Dev самое Sparkfun ESP8266 центр IoT | Документы Microsoft"
description: "Узнайте, как toosetup и подключите toosend данных toohello Azure облачной платформы разработки самое ESP8266 Sparkfun tooAzure центр IoT для него в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a>Подключение Dev самое ESP8266 Sparkfun tooAzure центр IoT в облаке hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Подключение DHT22 и Thing Dev к Центру Интернета вещей](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a>Выполняемая задача

Подключите центра IoT tooan Sparkfun ESP8266 самое разработки, вы создадите. Запустите образец приложения ESP8266 toocollect температуры и влажности данных с использованием DHT22 датчиков. Наконец отправьте центра IoT tooyour данных датчика hello.

> [!NOTE]
> При использовании других плат ESP8266 все равно можно выполнять эти действия tooconnect его tooyour центр IoT. В зависимости от hello ESP8266 Доска вы используете, может потребоваться tooreconfigure hello `LED_PIN`. Например, при использовании ESP8266 из AI-Thinker, можно изменить его из `0` слишком`2`. Нет начального набора? Щелкните [здесь](http://azure.com/iotstarterkits).

## <a name="what-you-will-learn"></a>Новые знания

* Как toocreate центр IoT и регистрация устройства для всего устройствам.
* Как tooconnect самое разработки с датчика hello и на компьютере.
* Как toocollect датчиков, выполнив пример приложения на самое устройствам.
* Как toosend hello центра IoT tooyour данных датчика.

## <a name="what-you-will-need"></a>Необходимые условия

![Детали, необходимые для работы с руководством hello](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete этой операции требуется hello следующую частей из начального набора разработки вещь:

* Здравствуйте, плата Sparkfun ESP8266 самое разработки.
* Micro USB tooType USB-кабель.

Следующие hello также необходим для среды разработки.

* Активная подписка Azure. Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.
* ПК или компьютер Mac под управлением Windows или Ubuntu;
* Беспроводной сети для разработки самое ESP8266 Sparkfun tooconnect для.
* Средство настройки hello toodownload подключения Интернета.
* [Интегрированная среда разработки Arduino](https://www.arduino.cc/en/main/software) версии 1.6.8 (или более поздней версии), более ранних версий не будет работать с hello AzureIoT библиотеки.

Hello следующие элементы являются необязательными случаю, когда не датчика. Также имеется возможность использовать имитацию датчиков hello.

* Датчик температуры и влажности Adafruit DHT22.
* Монтажная плата.
* Многомодовый оптоволоконный кабель с разъемами на обоих концах.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a>Связь ESP8266 самое разработки с датчика hello и компьютера

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a>Датчик температуры и влажности DHT22 подключения tooESP8266 самое разработки

Используйте hello breadboard и перемычки проводов toomake hello соединения следующим образом. Если у вас нет датчика, пропустите этот раздел, так как вместо него вы можете использовать симулированные данные.

![Справочные материалы по подключению](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

Для датчика ПИН-коды мы будем использовать следующие привязки hello:

| Начало (датчик)           | Конец (плата)           | Цвет кабеля   |
| -----------------------  | ---------------------- | ------------: |
| VDD (вывод 27F)            | 3V (вывод 8A)           | Красный кабель     |
| DATA (вывод 28F)           | GPIO 2 (вывод 9A)       | Белый кабель    |
| GND (вывод 30F)            | GND (вывод 7J)          | Черный кабель   |


- Дополнительные сведения см. в [документации по установке датчика DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) и в [спецификации Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711)

Теперь работающий датчик должен быть подключен к Sparkfun ESP8266 Thing Dev.

![Подключение dht22 к ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a>Подключите компьютер разработки самое ESP8266 Sparkfun tooyour

Используйте hello Micro USB tooType USB кабель tooconnect разработки самое ESP8266 Sparkfun tooyour компьютера следующим образом.

![Подключите компьютер tooyour huzzah Растушевка](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a>Добавление разрешений для последовательного порта (только в Ubuntu)

Если вы используете Ubuntu, убедитесь, что обычный пользователь имеет разрешения toooperate hello на hello USB порта из Sparkfun ESP8266 самое устройствам. разрешения tooadd последовательного порта для обычного пользователя, выполните следующие действия.

1. Выполните следующие команды в терминал hello.

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   При получении одного из hello следующие выходные данные:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Обратите внимание, в выходных данных hello, `uucp` или `dialout` , представляющим hello группы владельца имя hello USB-порту.

1. Добавление группы toohello hello пользователей, выполнив следующую команду hello:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`— Имя владельца группы hello, полученную на предыдущем шаге hello. `<username>` — это имя пользователя Ubuntu.

1. Выйдите из Ubuntu и снова войти в нем для hello изменение tootake эффекта.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Собирать данные датчиков и отправлять их tooyour центра IoT

В этом разделе вы развернете и запустите пример приложения на плате Sparkfun ESP8266 Thing Dev. Пример приложения Hello мигает hello Светодиод Sparkfun ESP8266 самое разработки и отправляет hello температуры и влажности собранные данные датчика tooyour hello DHT22 центр IoT.

### <a name="get-hello-sample-application-from-github"></a>Получение образца приложения hello из GitHub

Пример приложения Hello находится на GitHub. Клонирование репозитория образец hello, который содержит пример приложения hello из GitHub. репозиторий образец hello tooclone, выполните следующие действия:

1. Откройте окно командной строки или терминала.
1. Go tooa папку hello образец приложения toobe хранятся.
1. Выполните следующую команду hello.

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

Установка пакета hello для разработки самое ESP8266 Sparkfun в интегрированной среде разработки Arduino:

1. Откройте папку hello, где хранится пример приложения hello.
1. Откройте файл app.ino hello в папке приложения hello Arduino интегрированной среды разработки.

   ![Откройте пример приложения hello в интегрированной среде разработки arduino](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. В hello Arduino IDE, щелкните **файл** > **предпочтения**.
1. В hello **предпочтения** диалоговое окно, нажмите кнопку Далее toohello hello значок **дополнительные URL-адреса диспетчера досок** текстовое поле.
1. Во всплывающем окне приветствия, введите URL-адреса hello и нажмите кнопку **ОК**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![tooa точки URL-адреса пакета в интегрированной среде разработки arduino](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. В hello **предпочтения** диалоговое окно, нажмите кнопку **ОК**.
1. Щелкните **Инструменты** > **Платы** > **Менеджер плат**, а затем выполните поиск по esp8266.
   Должен быть установлен пакет ESP8266 версии 2.2.0 или более поздней.

   ![установлен пакет esp8266 Hello](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. Щелкните **Инструменты** > **Платы** > **Sparkfun ESP8266 Thing Dev**.

### <a name="install-necessary-libraries"></a>Установка необходимых библиотек

1. В hello Arduino IDE, щелкните **схематической** > **включают библиотеки** > **Управление библиотеками**.
1. Поиск hello следующие имена библиотек по одному. Для каждого из библиотеки hello, можно найти, установите **установить**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>У вас нет датчика DHT22?

Пример приложения Hello можно смоделировать температуры и влажности данных на случай реальные датчика DHT22 не нужно. tooenable hello образец приложения toouse моделирования данных, выполните следующие действия.

1. Откройте hello `config.h` файла в hello `app` папки.
1. Найдите следующие строки кода hello и измените значение hello из `false` слишком`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Настройка приложения toouse имитируемые hello примеров данных](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. Сохраните изменения с помощью `Control-s`.

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a>Развертывание hello образец приложения tooSparkfun ESP8266 самое разработки

1. В hello Arduino IDE, щелкните **средство** > **порт**и нажмите кнопку hello последовательного порта для устройствам Sparkfun ESP8266 вещь.
1. Нажмите кнопку **схематической** > **отправить** toobuild и развернуть tooSparkfun приложения образец hello устройствам ESP8266 вещь.

> [!Note]
> При использовании macOS, вероятно, могут быть hello следующие сообщения во время передачи данных. `warning: espcomm_sync failed`,`error: espcomm_open failed`. Откройте окно ternimal и Готово ниже toosolve действия этой проблемы.
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a>Ввод учетных данных

После успешного завершения передачи hello, выполните шаги tooenter hello учетные данные.

1. В hello Arduino IDE, щелкните **средства** > **последовательного монитор**.
1. В окне приветствия последовательного монитора Обратите внимание, hello двух раскрывающихся списках на hello нижнем правом углу.
1. Выберите **без завершения строк** для hello левом раскрывающемся списке.
1. Выберите **115200 бод** для hello правого раскрывающегося списка.
1. В hello входной расположенный вверху hello hello последовательного «монитор» введите следующую информацию в ответ на запрос tooprovide hello их, а затем нажмите кнопку **отправки**.
   * Идентификатор SSID для подключения Wi-Fi.
   * Пароль Wi-Fi.
   * Строка подключения к устройству.

> [!Note]
> Hello учетные данные хранятся в hello EEPROM из Sparkfun ESP8266 самое устройствам. При нажатии кнопки сброса hello на hello Dev самое ESP8266 Sparkfun плата пример приложения hello запрашивает Если интересующий вас tooerase hello. Введите `Y` удалены сведения hello toohave и предлагают tooprovide hello их еще раз.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Убедитесь, что успешно выполняется пример приложения hello

Если вы видите hello следующие выходные данные из окна последовательной монитор hello и hello мигающий Индикатор на ESP8266 самое Sparkfun разработки, пример приложения hello выполняется успешно.

![Окончательные выходные данные в Arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Дальнейшие действия

Успешно подключен концентратор IoT tooyour Sparkfun ESP8266 самое разработки и отправки центра IoT tooyour данных датчика захвачен hello. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
