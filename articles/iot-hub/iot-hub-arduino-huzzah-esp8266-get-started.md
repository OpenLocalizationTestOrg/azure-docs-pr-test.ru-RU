---
title: "toocloud aaaESP8266 - tooAzure подключения ESP8266 HUZZAH Растушевка центра IoT | Документы Microsoft"
description: "Узнайте, как toosetup и подключения tooAzure ESP8266 HUZZAH Adafruit Растушевка центр IoT для него toosend данных toohello Azure облачной платформы в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a>Подключение tooAzure ESP8266 HUZZAH Adafruit Растушевка центр IoT в облаке hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Подключение между DHT22, Feather HUZZAH ESP8266 и Центром Интернета вещей](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a>В рамках этого руководства мы:


Подключите центра IoT tooan ESP8266 HUZZAH Adafruit Растушевка созданного вами. Затем запустите пример приложения на ESP8266 toocollect hello температуры и влажности данных с использованием DHT22 датчиков. Отправьте центра IoT tooyour данных датчика hello.

> [!NOTE]
> При использовании других плат ESP8266 все равно можно выполнять эти действия tooconnect его tooyour центр IoT. В зависимости от hello ESP8266 Доска вы используете, может потребоваться tooreconfigure hello `LED_PIN`. Например, вы используете ESP8266 из Thinker аналитики Активов, может измениться из `0` слишком`2`. Нет начального набора? Получить его из hello [веб-сайте Azure](http://azure.com/iotstarterkits).




## <a name="what-you-learn"></a>Что вы узнаете

* Как toocreate центр IoT и регистрация устройства для ESP8266 HUZZAH Растушевка
* Как tooconnect ESP8266 HUZZAH Растушевка с датчика hello и компьютера
* Как toocollect датчиков, выполнив пример приложения на ESP8266 HUZZAH Растушевка
* Как toosend hello центра IoT tooyour данных датчика

## <a name="what-you-need"></a>Необходимые элементы

![Детали, необходимые для работы с руководством hello](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete этой операции требуется hello следующую частей из начального набора Растушевка HUZZAH ESP8266:

* плата ESP8266 HUZZAH Растушевка Hello
* Micro USB tooType USB-кабель

Также необходим hello следующие действия для среды разработки.

* Активная подписка Azure. Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.
* ПК или компьютер Mac под управлением Windows или Ubuntu;
* Tooconnect ESP8266 HUZZAH Растушевка для беспроводных сетей.
* Средство настройки hello toodownload подключения Интернета.
* [Arduino IDE](https://www.arduino.cc/en/main/software) версии 1.6.8 или более новой. Более ранних версий не работают с библиотекой AzureIoT hello.

Hello следующие элементы являются необязательными случаю, когда не датчика. Также имеется возможность использовать имитацию датчиков hello.

* Датчик температуры и влажности Adafruit DHT22.
* Монтажная плата.
* Многомодовый оптоволоконный кабель с разъемами на обоих концах


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a>Связь ESP8266 HUZZAH Растушевка с датчика hello и компьютера
В этом разделе подключиться hello датчики tooyour платы. Затем можно подключить компьютер tooyour устройство для использования в будущем.
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a>Подключение DHT22 температуры и влажности датчика tooFeather HUZZAH ESP8266

Используйте hello breadboard и перемычки проводов toomake hello соединения следующим образом. Если у вас нет датчика, пропустите этот раздел, так как вместо него вы можете использовать симулированные данные.

![Справочные материалы по подключению](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


Для датчика ПИН-коды используйте hello после подключения:


| Начало (датчик)           | Конец (плата)           | Цвет кабеля   |
| -----------------------  | ---------------------- | ------------: |
| VDD (вывод 31F)            | 3V (вывод 58H)           | Красный кабель     |
| DATA (вывод 32F)           | GPIO 2 (вывод 46A)       | Синий кабель    |
| GND (вывод 34F)            | GND (вывод 56I)          | Черный кабель   |

Дополнительные сведения см. в статьях о [подключении к датчику Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) и [выводах Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).



Теперь работающий датчик должен быть подключен к Feather HUZZAH ESP8266.

![Подключение DHT22 к Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a>Подключите компьютер tooyour ESP8266 HUZZAH Растушевка

Как показано далее, используйте hello Micro USB tooType USB кабель tooconnect ESP8266 HUZZAH Растушевка tooyour компьютера.

![Подключите компьютер tooyour Huzzah Растушевка](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Добавление разрешений для последовательного порта (только в Ubuntu)


Если вы используете Ubuntu, убедитесь, что имеется на hello USB порта из Растушевка HUZZAH ESP8266 toooperate разрешения hello. tooadd последовательный порт, выполните следующие действия:


1. Выполните следующие команды в терминал hello.

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   При получении одного из hello следующие выходные данные:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Обратите внимание, что в выходных данных hello `uucp` или `dialout` — имя владельца группы hello hello USB-порту.

1. Добавление группы toohello hello пользователей, выполнив следующую команду hello:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`— Имя владельца группы hello, полученную на предыдущем шаге hello. `<username>` — это имя пользователя Ubuntu.

1. Выйдите из Ubuntu и войдите в нее снова для tooappear изменение hello.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Собирать данные датчиков и отправлять их tooyour центра IoT

В этом разделе вы развернете и запустите пример приложения на плате Feather HUZZAH ESP8266. Пример приложения Hello мигает hello Светодиод Растушевка HUZZAH ESP8266 и отправляет hello температуры и влажности собранные данные датчика tooyour hello DHT22 центр IoT.

### <a name="get-hello-sample-application-from-github"></a>Получение образца приложения hello из GitHub

Пример приложения Hello находится на GitHub. Клонирование репозитория образец hello, который содержит пример приложения hello из GitHub. репозиторий образец hello tooclone, выполните следующие действия:

1. Откройте окно командной строки или терминала.
1. Go tooa папку hello образец приложения toobe хранятся.
1. Выполните следующую команду hello.

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

Установите пакет hello для ESP8266 HUZZAH Растушевка hello Arduino интегрированной среды разработки:

1. Откройте папку hello, где хранится пример приложения hello.
1. Откройте файл app.ino hello в папке приложения hello в hello Arduino интегрированной среды разработки.

   ![Откройте пример приложения hello в интегрированной среде разработки Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. В hello Arduino IDE, щелкните **файл** > **предпочтения**.
1. В hello **предпочтения** диалоговое окно, нажмите кнопку Далее toohello hello значок **дополнительные URL-адреса диспетчера досок** поле.
1. Во всплывающем окне приветствия, введите URL-адреса hello и нажмите кнопку **ОК**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Tooa точки URL-адреса пакета в интегрированной среде разработки Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. В hello **предпочтения** диалоговое окно, нажмите кнопку **ОК**.
1. Щелкните **Инструменты** > **Платы** > **Менеджер плат**, а затем выполните поиск по esp8266.

   Диспетчер плат показывает, что установлена плата ESP8266 2.2.0 или более поздней версии.

   ![установлен пакет esp8266 Hello](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. Щелкните **Инструменты** > **Платы** > **Adafruit HUZZAH ESP8266**.

### <a name="install-necessary-libraries"></a>Установка необходимых библиотек

1. В hello Arduino IDE, щелкните **схематической** > **включают библиотеки** > **Управление библиотеками**.
1. Поиск hello следующие имена библиотек по одному. Для каждой найденной библиотеки щелкните **Установить**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>У вас нет датчика DHT22?

Пример приложения Hello можно смоделировать температуры и влажности данных на случай реальные датчика DHT22 не нужно. tooset hello образец приложения toouse моделирования данных, выполните следующие действия.

1. Откройте hello `config.h` файла в hello `app` папки.
1. Найдите следующие строки кода hello и измените значение hello из `false` слишком`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Настройка приложения toouse имитируемые hello примеров данных](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. Сохраните файл hello с `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a>Развертывание hello образец приложения tooFeather HUZZAH ESP8266

1. В hello Arduino IDE, щелкните **средство** > **порт**и выберите для ESP8266 HUZZAH Растушевка hello последовательного порта.
1. Нажмите кнопку **схематической** > **отправить** toobuild и развертывание hello образец приложения tooFeather HUZZAH ESP8266.

### <a name="enter-your-credentials"></a>Ввод учетных данных

После успешного завершения передачи hello, выполните эти шаги tooenter учетные данные.

1. В hello Arduino IDE, щелкните **средства** > **последовательного монитор**.
1. В окне монитора последовательного hello Обратите внимание, hello два раскрывающихся списков в правом нижнем углу hello.
1. Выберите **без завершения строк** для hello левом раскрывающемся списке.
1. Выберите **115200 бод** для hello правого раскрывающегося списка.
1. В hello входной расположенный вверху hello hello последовательного «монитор» введите следующую информацию в ответ на запрос tooprovide hello их, а затем нажмите кнопку **отправки**.
   * Идентификатор SSID для подключения Wi-Fi.
   * Пароль Wi-Fi.
   * Строка подключения к устройству.

> [!Note]
> Hello учетные данные хранятся в hello EEPROM из Растушевка HUZZAH ESP8266. Если вы нажмете кнопку Сброс hello hello Растушевка HUZZAH ESP8266 платы, пример приложения hello запросом tooerase hello сведения. Введите `Y` toohave hello сведения удалены. Будет предложено сведения hello tooprovide еще раз.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Убедитесь, что успешно выполняется пример приложения hello

Если вы видите hello следующие выходные данные из окна последовательной монитор hello и hello мигающий Индикатор на ESP8266 HUZZAH Растушевка, пример приложения hello выполняется успешно.

![Окончательные выходные данные в интегрированной среде разработки Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Дальнейшие действия

Успешно подключен концентратор IoT tooyour ESP8266 HUZZAH Растушевка и отправляются центра IoT tooyour данных датчика захвачен hello. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

