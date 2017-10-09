---
title: "toocloud набор разработки aaaIoT - tooAzure подключения AZ3166 набор разработки IoT центр IoT | Документы Microsoft"
description: "Узнайте, как toosetup и подключите набор разработки AZ3166 IoT tooAzure центр IoT для него toosend данных toohello Azure облачной платформы в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a>Подключение AZ3166 набор разработки IoT tooAzure центр IoT в облаке hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Hello [набор разработки IoT MXChip](https://microsoft.github.io/azure-iot-developer-kit/) можно использовать toodevelop и прототип Интернета вещей (IoT) решения, использующие службы Microsoft Azure. Он содержит совместимую с Arduino плату со множеством периферийных устройств и датчиков, пакет ПО для платы с открытым кодом и расширяющийся [каталог проектов](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).

## <a name="what-you-do"></a>В рамках этого руководства мы:
Подключение [набор разработки](https://microsoft.github.io/azure-iot-developer-kit/) центр Azure IoT tooan создать сбор hello датчиков температуры и влажности данных и отправки hello данных tooIoT концентратора.

У вас еще нет платы DevKit? Вы можете новую плату DevKit [здесь](https://aka.ms/iot-devkit-purchase).

## <a name="what-you-learn"></a>Что вы узнаете

* Как tooconnect доступа tooWireless набор разработки IoT пункт и подготовить среду разработки.
* Как toocreate центр IoT и регистрация устройства для набор разработки MXChip IoT.
* Как toocollect датчиков, выполнив пример приложения на набор разработки MXChip IoT.
* Как toosend hello центра IoT tooyour данных датчика.

## <a name="what-you-need"></a>Необходимые элементы

* Плата MXChip IoT DevKit с кабелем micro USB. Вы можете [получить ее прямо сейчас](https://aka.ms/iot-devkit-purchase).
* Компьютер под управлением Windows 10 или macOS 10.10 (или более поздней версии).
* активная подписка Azure;
  * Вы можете активировать [бесплатную 30-дневную пробную учетную запись Microsoft Azure](https://azureinfo.microsoft.com/us-freetrial.html).

## <a name="prepare-your-hardware"></a>Подготовка оборудования

Подключить компьютер tooyour hello оборудования.

### <a name="hardware-you-need"></a>Необходимое оборудование

* Плата DevKit.
* Кабель micro USB.

![Приступая к работе: оборудование](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a>Подключите компьютер tooyour набор разработки

1. Подключение USB окончания tooyour ПК
2. Подключение Micro USB окончания toohello набор разработки
3. Далее toopower Hello зеленый Индикатор подтверждает подключения

![Приступая к работе: подключение](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>Настройка Wi-Fi

Для работы проектов Центра Интернета вещей требуется подключение к Интернету. Используйте следующие инструкции tooconfigure hello набор разработки tooconnect tooWiFi hello.

### <a name="enter-ap-mode"></a>Переключение в режим точки беспроводного доступа

Удерживая нажатой кнопку B, то push и отпустите кнопку "сбросить" hello, а затем кнопку выпуск б. Ваш набор разработки входит в режим доступа для настройки Wi-Fi. Hello отобразится экран приветствия Identifier(SSID) установите службы из hello набор разработки, а также hello конфигурации портала IP-адрес:

![Приступая к работе: настройка Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a>Подключение tooDevKit AP

Теперь использование другого Wi-Fi включена устройств (ПК или мобильный телефон) tooconnect toohello набор разработки SSID (выделены hello экрана выше), оставьте пустым паролем hello.

![Приступая к работе: идентификатор SSID](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>Настройка Wi-Fi для платы DevKit

Откройте hello IP-адрес, на экране приветствия набор разработки на ПК или в браузере мобильного телефона, выберите сеть Wi-Fi hello нужные hello tooconnect набор разработки для, а затем введите пароль hello. Нажмите кнопку **Connect** toocomplete:

![Приступая к работе: портал настройки Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

После успешного соединения hello hello набор разработки перезагрузится через несколько секунд. Если выполнено успешно, на экране приветствия появится hello Wi-Fi имя и IP-адрес:

![Приступая к работе: IP-адрес для Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
отображаемый в фото hello Hello IP-адрес может не соответствовать hello фактических IP назначается и отображается на экране приветствия набор разработки. Это нормально, как Wi-Fi использует DHCP toodynamically назначение IP-адресов.

После настройки Wi-Fi учетные данные останутся на hello устройства для этого соединения, даже если не подключен. Например, если вы настроили hello набор разработки для Wi-Fi дома и затем потребовалось hello набор разработки toohello office, необходимо будет tooreconfigure AP режим (начиная с шага **войти в режим AP**) tooconnect hello office tooyour набор разработки Wi-Fi. 

## <a name="start-using-devkit"></a>Начало использования платы DevKit

приложение по умолчанию Hello, работающих на набор разработки проверка hello последняя версия встроенного по hello и выводится некоторые данные диагностики датчика для вас.

### <a name="upgrade-toohello-latest-firmware"></a>Обновление toohello последняя версия встроенного по

Появится на экране приветствия, обе версии встроенного по последняя hello, при необходимости обновления. Выполните [обновления микропрограммы](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) руководство tooupgrade его.

![Приступая к работе: встроенное ПО](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
Это однократное усилия, после начала разработки на hello набор разработки и отправить приложение, вы получите последнюю версию встроенного по hello поставляются вместе с приложением.

### <a name="test-various-sensors"></a>Тестирование различных датчиков

Нажмите кнопку B tootest датчиков, продолжать, нажатие и отпускание кнопки toocycle hello B через каждого датчика.

![Приступая к работе: датчики](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>Подготовка среды разработки

Теперь настало время tooset hello среды разработки: средства и пакеты для toobuild привлекательных приложений IoT. Можно выбрать Windows или tooyour операционной системы в соответствии с версией macOS.


### <a name="windows"></a>Windows

Мы рекомендуем вам toouse hello установки пакета tooprepare hello среды разработки. Если возникли проблемы, можно выполнить hello [действия вручную](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget своей работы.

#### <a name="download-latest-package"></a>Скачивание последней версии пакета

Hello `.zip` загрузке файл содержит все необходимые средства и пакеты, необходимые для разработки набор разработки.

> [!div class="button"]
[Загрузить](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> Hello `.zip` файл содержит hello следующие средства и пакеты. Если уже установлены некоторые компоненты, скрипт hello обнаружит и пропустить их.
> * Node.js и Yarn: среда выполнения для сценария установки hello и автоматизированных задач
> * [Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -кросс платформенных взаимодействие с командной строки для управления ресурсами Azure, hello MSI-ФАЙЛ содержит зависимые Python и PIP-адрес.
> * [Visual Studio Code](https://code.visualstudio.com/): упрощенный редактор кода для разработки для платы DevKit.
> * [Расширение Visual Studio Code для Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): обеспечивает разработку для Arduino в VS Code.
> * [Интегрированная среда разработки Arduino](https://www.arduino.cc/en/Main/Software): hello расширение для Arduino зависит от этого средства
> * Пакет платы набор разработки: Средства цепочки, библиотеки и проекты для hello набор разработки
> * Служебная программа ST-Link: необходимые служебные программы и драйверы.

#### <a name="run-installation-script"></a>Запуск сценария установки

В проводнике Windows найдите hello `.zip` и извлеките его, найдите `install.cmd`, щелкните правой кнопкой мыши и выберите **«Запуск от имени администратора»** toostart.

![Приступая к работе: запуск от имени администратора](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

Во время установки вы увидите ход hello каждый инструмент или пакета.

![Приступая к работе: установка](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a>Подтвердите tooinstall драйверы

Hello VS Code для расширения Arduino использует hello Arduino интегрированной среды разработки. Если это hello впервые устанавливаете hello Arduino IDE, будут использоваться запрашиваемые tooinstall соответствующие драйверы:

![Приступая к работе: драйвер](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

Может потребоваться установка toofinish около 10 минут в зависимости от быстродействия Internet. После завершения установки hello, вы увидите кода Visual Studio и интегрированной среды разработки Arduino ярлыки на рабочем столе.

> [!NOTE] 
В некоторых случаях при запуске VS Code появляется сообщение об ошибке. В нем сообщается, что не удается найти интегрированную среду разработки Arduino или связанный пакет ПО для платы. toosolve его закрыть VS Code Arduino IDE запустить один раз и VS Code должна правильно определить путь Arduino IDE.


### <a name="macos-preview"></a>macOS (предварительная версия)

Выполните эти среды разработки tooprepare действия на macOS.

#### <a name="install-azure-cli-20"></a>Установка Azure CLI 2.0

Выполните hello [официальный руководство](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:

Azure CLI 2.0 можно установить с помощью одной команды `curl`.

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

И перезапустите вашей командной оболочки для изменения эффекта tootake:

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>Установка интегрированной среды разработки Arduino

Hello расширения Arduino кода Visual Studio использует hello Arduino интегрированной среды разработки. Загрузите и установите hello [Arduino интегрированную среду разработки для macOS](https://www.arduino.cc/en/Main/Software).

#### <a name="install-visual-studio-code"></a>Установка Visual Studio Code

Скачайте и установите [Visual Studio Code для macOS](https://code.visualstudio.com/). Это будет hello средство первичной разработки для создания IoT набор разработки приложений.

####  <a name="download-latest-package"></a>Скачивание последней версии пакета

1. Установите Node.js. Можно использовать диспетчер пакетов популярных macOS [Homebrew](https://brew.sh/) или [готовые установщика](https://nodejs.org/en/download/) tooinstall его.

2. Скачайте файл с расширением `.zip`, содержащий сценарии задач, необходимые для разработки для DevKit в VS Code.

   > [!div class="button"]
   [Загрузить](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   Найдите hello `.zip` и извлеките его. Затем запустите **терминалов** приложения и выполнения hello, следуя tooconfigure команды:

   Переместите папку пользователя macOS tooyour извлеченную папку:
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   Установите пакеты `npm`.
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>Расширение VS Code для Arduino

Код Visual Studio позволяет tooinstall Marketplace расширений непосредственно в средстве hello, просто щелкните значок расширения hello в левом меню области hello и найдите `Arduino` tooinstall:

![Установка: расширения](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>Установка пакета ПО для платы DevKit

Вам потребуется tooadd hello набор разработки доски с помощью hello Manager доски в коде Visual Studio.

1. Используйте `Cmd+Shift+P` tooinvoke команд палитры и тип **Arduino** затем найдите и выберите **Arduino: диспетчер плата**.

2. Нажмите кнопку **«Дополнительные URL-адреса»** внизу hello справа.
   ![Установка: дополнительные URL-адреса](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. В hello `settings.json` файл, добавьте строку внизу hello `USER SETTINGS` области и сохранить.
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![Установка: JSON-файл параметров](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. Теперь hello плата Manager для поиска «az3166» и установите последнюю версию hello.
   ![Установка: az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

Теперь у вас есть все необходимые средства hello и пакеты, установленные для macOS.


## <a name="open-project-folder"></a>Открытие папки проекта

### <a name="launch-vs-code"></a>Запустите VSCode.

Убедитесь, что плата DevKit не подключена. Сначала запустите VS Code и подключите компьютер tooyour набор разработки hello. VS Code автоматически найдет ее, и отобразится вводная страница.

![Минирешение: VS Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
В некоторых случаях при запуске VS Code появляется сообщение об ошибке. В нем сообщается, что не удается найти интегрированную среду разработки Arduino или связанный пакет ПО для платы. toosolve его закрыть VS Code еще раз запустите Arduino интегрированной среды разработки и VS Code должна правильно определить путь Arduino IDE.

### <a name="open-arduino-examples-folder"></a>Открытие папки с примерами Arduino

Переключение слишком**«Примеры Arduino»** вкладки, переходы слишком`Examples for MXCHIP AZ3166 > AzureIoT` и выберите команду `GetStarted`.

![Минирешение: примеры](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

Если вы столкнулись tooclose hello области tooreload его, используйте `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke команд палитры и тип **Arduino** toofind и выберите **Arduino: примеры**.

## <a name="provision-azure-services"></a>Подготовка служб Azure

Запустите задачу в окне решения hello, `Ctrl+P` (macOS: `Cmd+P`), введя «задача подготовки облако»:

В hello VS Code терминалов интерактивной командной строки поможет hello подготовки необходимых служб Azure:

![Минирешение: подготовка облачных служб](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>Создание и передача эскиза Arduino

### <a name="install-required-library"></a>Установка необходимой библиотеки

1. Нажмите клавишу `F1` или `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke команд палитры и тип **Arduino** затем найдите и выберите **Arduino: диспетчер библиотек**.

2. Найдите библиотеку `ArduinoJson` и щелкните **Install** (Установить).

### <a name="build-and-upload-hello-device-code"></a>Построение и загружать код устройства hello

Используйте `Ctrl+P` (macOS: `Cmd+P`) toorun «задачи устройства загрузки». Hello терминалов предложит вам tooenter режим конфигурации. toodo таким образом, удерживая нажатой кнопку A, а затем кнопки сброса hello принудительной отправки и выпуска. Hello отобразится экран «Конфигурация». Это строка подключения tooset hello, извлекает из шага «задачи облака подготовку к работе».

Затем он будет запущен, проверка и отправка эскиз Arduino hello:

![Минирешение: передача кода устройства](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

Hello набор разработки будет перезагрузить и начать выполнение кода hello.

## <a name="test-hello-project"></a>Hello тестовый проект

В VS Code щелкните значок подключаемых power hello строку hello tooopen последовательного монитор состояния hello.

Пример приложения Hello выполняется успешно при появлении hello следующие результаты:

* Hello последовательного монитор отображает hello же сведения, что содержимое hello hello снимке экрана ниже.
* мигает Hello Светодиод на набор разработки MXChip IoT.

![Окончательный результат в VS Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>Проблемы и обратная связь

Можно найти [часто задаваемые вопросы о](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) при возникновении проблем или достижения toous из каналов hello ниже.

## <a name="next-steps"></a>Дальнейшие действия

Вы успешно подключились набор разработки IoT MXChip tooyour центр IoT и отправленных hello захвачен центра IoT tooyour данных датчика.

Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:

- [Управление обменом сообщениями между устройством и облаком с помощью обозревателя Центра Интернета вещей](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [Сохранять сообщения центр IoT tooAzure хранилища данных](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [Использовать данные в режиме реального времени датчика toovisualize Power BI из центра IoT Azure](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [Использовать данные в режиме реального времени датчика toovisualize веб-приложения Azure из центр IoT Azure](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [Прогноз погоды, используя данные датчика hello из вашего центра IoT в машинном обучении Azure](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [Управление устройствами с помощью средства iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [Remote monitoring and notifications with Logic Apps](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps) (Удаленный мониторинг и уведомления Logic Apps)