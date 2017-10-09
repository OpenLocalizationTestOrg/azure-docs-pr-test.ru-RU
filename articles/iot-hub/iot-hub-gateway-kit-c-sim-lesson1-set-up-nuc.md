---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 1. Настройка NUC | Документация Майкрософт"
description: "Настройка toowork Intel NUC виде шлюза IoT между датчика и данных датчика toocollect центр IoT Azure и отправить его tooIoT концентратора."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: "шлюз Интернета вещей, intel nuc, компьютер nuc, DE3815TYKE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Настройка Intel NUC в качестве шлюза Интернета вещей

## <a name="what-you-will-do"></a>Выполняемая задача

- Настройте Intel NUC в качестве шлюза Интернета вещей.
- Установите пакет Azure IoT Edge hello на Intel NUC.
- Запустите пример приложения «hello_world» на функциональность шлюза hello tooverify Intel NUC.
Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания

Из этого урока вы узнаете:

- Как tooconnect Intel NUC с периферийные устройства.
- Как пакеты hello необходимые tooinstall и обновления на использование Intel NUC hello смарт-диспетчера пакетов.
- Как toorun hello» hello_world» образец функциональность шлюза hello tooverify приложения.

## <a name="what-you-need"></a>Необходимые элементы

- DE3815TYKE комплект Intel NUC с hello шлюза программного обеспечения Intel IoT Suite (р. воздушного Linux * 7.0.0.13) предварительно.
- Кабель Ethernet.
- Клавиатура.
- Кабель HDMI или VGA.
- Монитор с портом HDMI или VGA.

![Комплект для шлюза](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Подключения Intel NUC hello периферийных устройств

изображение Hello ниже приведен пример NUC Intel, который связан с различными периферийные устройства:

1. Подключенный tooa клавиатуры.
2. Подключен монитор toohello кабель VGA или HDMI кабель.
3. Подключенный tooa проводной сети с помощью кабеля Ethernet.
4. Источник питания подключенных toohello кабеля питания.

![Tooperipherals подключен NUC Intel](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Подключение системы Intel NUC toohello от главного компьютера через Secure Shell (SSH)

Здесь требуется клавиатуру и монитор tooget hello IP-адрес устройства NUC. Если вы уже знаете hello IP адрес, можно пропустить toostep 3 в этом разделе.

1. Включите Intel NUC, нажав кнопку питания hello и журналов в системе hello.

   имя пользователя по умолчанию Hello и пароль указаны оба `root`.

2. Получить IP-адрес NUC hello, выполнив hello `ifconfig` команды. Эта процедура выполняется на устройстве NUC hello.

   Ниже приведен пример выходных данных команды hello.

   ![Выходные данные ifconfig с IP-адресом NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   В этом примере hello значение, следующее за `inet addr:` hello IP-адрес, необходимый при планировании tooconnect удаленно с tooIntel компьютера узла NUC.

3. Используйте одну из следующую SSH клиентов из вашего узла машины tooconnect tooIntel NUC hello.

   - [PuTTY](http://www.putty.org/) для Windows.
   - Hello сборки в клиент SSH на Ubuntu или macOS.

   Это обеспечивает более эффективное и продуктивную toooperate на Intel NUC от главного компьютера. Требуется hello hello IP-адрес, имя пользователя и пароль hello tooconnect NUC через клиент SSH. Ниже приведен пример использования hello SSH-клиента на macOS.
   ![SSH-клиент, запущенный на macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Установите пакет Azure IoT Edge hello

пакет Azure IoT Edge Hello содержит hello заранее скомпилированные двоичные файлы hello SDK и его зависимости. Эти двоичные файлы являются Azure IoT Edge, hello IoT Azure SDK и соответствующих средств hello. Hello пакет также содержит пример приложения «hello_world», используется toovalidate функциональность шлюза hello. Граница IoT является hello основной частью hello шлюза. tooinstall hello пакет, выполните следующие действия:

1. Добавьте репозиторий облака IoT hello, выполнив следующие команды в окне терминала hello:

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   Hello `rpm` команда импортирует hello ключ об/мин. Hello `smart channel` команда добавляет hello rpm канала toohello смарт-диспетчера пакетов. Перед запуском hello `smart update` команду, вы видите вывод как ниже.

   ![результаты выполнения команд rpm и smart channel](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Установка пакета hello, выполнив следующую команду hello:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`— Имя пакета hello hello. Hello `smart install` команды — пакет используется tooinstall hello.

   После установки пакета hello Intel NUC является ожидаемым toowork как шлюз.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Запустить hello Azure IoT края «hello_world» образец приложения

Go слишком`azureiotgatewaysdk/samples` и запуск приложения образец «hello_world» образец hello. В этом образце приложения создает шлюз из hello `hello_world.json` файл и использует базовые компоненты hello Azure IoT Edge архитектура toolog файл tooa сообщение hello world hello каждые 5 секунд.

Можно запустить «hello_world» образец hello образец приложения, запустив hello следующую команду:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Пример приложения Hello создает следующие hello, выходные данные при правильной работе функции hello шлюза:

![выходные данные приложения](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Сводка

Поздравляем! Итак, вы завершили настройку Intel NUC в качестве шлюза. Теперь вы готовы toomove на следующем занятии tooset toohello компьютера узла, создать центр Azure IoT и зарегистрируйте логическое устройство концентратора Azure IoT.

## <a name="next-steps"></a>Дальнейшие действия
[Подготовка главного компьютера и Центра Интернета вещей Azure](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
