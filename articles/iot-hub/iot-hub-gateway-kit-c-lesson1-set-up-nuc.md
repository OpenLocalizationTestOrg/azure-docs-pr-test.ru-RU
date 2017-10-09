---
title: "Приступая к работе с устройством SensorTag и шлюзом Интернета вещей Azure. Урок 1. Настройка Intel NUC | Документация Майкрософт"
description: "Настройка toowork Intel NUC виде шлюза IoT между датчика и данных датчика toocollect центр IoT Azure и отправить его tooIoT концентратора."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "шлюз Интернета вещей, intel nuc, компьютер nuc, DE3815TYKE"
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Настройка Intel NUC в качестве шлюза Интернета вещей
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a>Выполняемая задача

- Настройте Intel NUC в качестве шлюза Интернета вещей.
- Установите пакет Azure IoT Edge hello на hello Intel NUC.
- Запустите пример приложения «hello_world» на hello функциональность шлюза hello tooverify Intel NUC.

  > Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания

Из этого урока вы узнаете:

- Как tooconnect Intel NUC с периферийные устройства.
- Как пакеты hello необходимые tooinstall и обновления на использование Intel NUC hello смарт-диспетчера пакетов.
- Как toorun hello» hello_world» образец функциональность шлюза hello tooverify приложения.

## <a name="what-you-need"></a>Необходимые элементы

- DE3815TYKE комплект Intel NUC с hello шлюза программного обеспечения Intel IoT Suite (р. воздушного Linux * 7.0.0.13) предварительно. [Щелкните здесь toopurchase Grove IoT коммерческих шлюза комплект](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).
- Кабель Ethernet.
- Клавиатура.
- Кабель HDMI или VGA.
- Монитор с портом HDMI или VGA.
- Необязательно: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)

![Комплект для шлюза](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Подключения Intel NUC hello периферийных устройств

изображение Hello ниже приведен пример NUC Intel, который связан с различными периферийные устройства:

1. Подключенный tooa клавиатуры.
2. Подключен монитор tooa кабель VGA или HDMI кабель.
3. Подключенный tooa проводной сети с помощью кабеля Ethernet.
4. Источник питания подключенных tooa кабеля питания.

![Tooperipherals подключен NUC Intel](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Подключение системы Intel NUC toohello от главного компьютера через Secure Shell (SSH)

Необходимо будет клавиатуру и монитор tooget hello IP-адрес устройства Intel NUC. Если вы уже знаете hello IP адрес, можно пропустить упреждающего toostep 3 в этом разделе.

1. Включите hello Intel NUC, нажав кнопку питания hello и войдите в систему.

   имя пользователя по умолчанию Hello и пароль указаны оба `root`.

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. Получить IP-адрес hello hello Intel NUC, выполнив hello `ifconfig` команду на устройстве Intel NUC hello.

   Ниже приведен пример выходных данных команды hello.

   ![Выходные данные ifconfig с IP-адресом Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   В этом примере hello значение, следующее за `inet addr:` hello IP-адрес, необходимый при подключении toohello Intel NUC от главного компьютера.

3. Используйте одну из следующую SSH клиентов из вашего узла компьютера tooconnect tooIntel NUC hello.

    - [PuTTY](http://www.putty.org/) для Windows.
    - Hello встроенный клиент SSH на Ubuntu или macOS.

   Это обеспечивает более эффективное и продуктивную toooperate NUC Intel от главного компьютера. Будет необходимо hello Intel NUC IP-адрес, пользователь имя и пароль tooit tooconnect через клиент SSH. Ниже приведен пример использования SSH-клиента в macOS.
   ![SSH-клиент, запущенный на macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Установите пакет Azure IoT Edge hello

пакет Azure IoT Edge Hello содержит hello заранее скомпилированные двоичные файлы IoT границей и его зависимости. Эти двоичные файлы являются Azure IoT Edge, hello IoT Azure SDK и соответствующих средств hello. Hello пакет также содержит «hello_world» приложение представляет функциональность шлюза используется toovalidate hello. Граница IoT является hello основной частью hello шлюза. 

Выполните эти шаги tooinstall hello пакета.

1. Добавьте hello облака IoT репозиторий, выполнив следующие команды в окне терминала hello:

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > Введите «y», при запросе too'Include этот канал? "
   
   При получении `import read failed(-1)` ошибку, используйте hello следующая проблема hello tooresolve команды:
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   Hello `rpm` команда импортирует hello ключ об/мин. Hello `smart channel` команда добавляет hello rpm канала toohello смарт-диспетчера пакетов. Перед запуском hello `smart update` команды, вы увидите выходные данные, аналогичные показанным ниже.

   ![результаты выполнения команд rpm и smart channel](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. Выполните команду hello смарт-обновления:

   ```bash
   smart update
   ```

3. Установите пакет шлюза Azure IoT hello, выполнив hello следующую команду:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`— Имя пакета hello hello. Hello `smart install` команды — пакет используется tooinstall hello.

    > Выполнения hello следующая команда, если вы видите эту ошибку: «открытый ключ недоступен»

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > Перезагрузить hello Intel NUC, если вы видите эту ошибку: «нет пакет предоставляет util-linux-dev»

   После установки пакета hello Intel NUC — Готово toofunction как шлюз.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Запустить hello Azure IoT края «hello_world» образец приложения

Следующий пример приложения Hello создает шлюз из `hello_world.json` файл и использует hello базовые компоненты архитектуры Azure IoT Edge toolog файл tooa сообщение hello world (log.txt) каждые 5 секунд.

Вы можете запустить пример Hello World hello, выполнив следующие команды hello:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Разрешить приложения hello Hello World работать несколько минут и нажмите клавишу hello ввод ключа toostop его.
![выходные данные приложения](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

> Вы можете игнорировать любые ошибки "Недопустимый дескриптор аргумента (NULL)", которые появляются после нажатия клавиши ВВОД.

Убедитесь, что шлюз hello выполнено успешно, открыв файл log.txt hello, которая теперь находится в папке hello_world ![log.txt представления каталога](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)

Откройте файл log.txt, с помощью hello следующую команду:

```bash
vim log.txt
```

Вы увидите содержимое hello log.txt, которой будет выводиться в формате JSON hello ведения журнала сообщений, которые были записаны каждые 5 секунд модулем Hello World hello шлюза.
![Представление каталога log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Сводка

Поздравляем! Итак, вы завершили настройку Intel NUC в качестве шлюза. Теперь вы готовы toomove на следующем занятии tooset toohello компьютера узла, создать центр IoT Azure и зарегистрировать логические устройства Azure IoT Hub.

## <a name="next-steps"></a>Дальнейшие действия
[Использовать tooconnect шлюза IoT tooAzure устройства центра IoT](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

