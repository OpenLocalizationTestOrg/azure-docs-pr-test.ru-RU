---
title: "Приступая к работе с устройством SensorTag и шлюзом Интернета вещей Azure. Урок 1. Настройка Intel NUC | Документация Майкрософт"
description: "Настройка Intel NUC в качестве шлюза Интернета вещей, который собирает данные из датчиков и передает их в Центр Интернета вещей Azure."
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
ms.openlocfilehash: 1a3a92ab8d08c6ed6f047208217c46022027157e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Настройка Intel NUC в качестве шлюза Интернета вещей
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a>Выполняемая задача

- Настройте Intel NUC в качестве шлюза Интернета вещей.
- Установите пакет Edge Интернета вещей Azure на Intel NUC.
- Запустите пример приложения hello_world на Intel NUC для проверки работоспособности шлюза.

  > Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания

Из этого урока вы узнаете:

- как подключить периферийные устройства к Intel NUC;
- как установить и обновить требуемые пакеты на Intel NUC с помощью Smart Package Manager;
- как запустить пример приложения hello_world на Intel NUC для проверки работоспособности шлюза.

## <a name="what-you-need"></a>Необходимые элементы

- Предварительно установленный пакет DE3815TYKE для Intel NUC с набором программного обеспечения Intel для шлюза Интернета вещей (Wind River Linux *7.0.0.13). [Щелкните здесь, чтобы приобрести набор для создания коммерческого шлюза Интернета вещей Grove](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).
- Кабель Ethernet.
- Клавиатура.
- Кабель HDMI или VGA.
- Монитор с портом HDMI или VGA.
- Необязательно: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)

![Комплект для шлюза](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a>Подключение периферийных устройств к Intel NUC

На следующем рисунке показана конфигурация Intel NUC с подключением к разным периферийным устройствам.

1. Подключение к клавиатуре.
2. Подключение к монитору через кабель VGA или HDMI.
3. Подключение к проводной сети с помощью кабеля Ethernet.
4. Подключение питания с помощью кабеля питания.

![Intel NUC с подключением к периферийным устройствам](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Подключение к системе Intel NUC с главного компьютера через Secure Shell (SSH)

Вам потребуются клавиатура и монитор, чтобы узнать IP-адрес устройства Intel NUC. Если вы уже знаете IP-адрес, можете сразу перейти к шагу 3 в этом разделе.

1. Включите Intel NUC, нажав кнопку питания, и войдите в систему.

   По умолчанию имя пользователя и пароль имеют одинаковые значения: `root`.

       > Hit the enter key on your keyboard if you see either of the following errors when you boot: 'A TPM error (7) occurred attempting to read a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. Получите IP-адрес Intel NUC, выполнив команду `ifconfig` на устройстве Intel NUC.

   Вот пример результата выполнения такой команды:

   ![Выходные данные ifconfig с IP-адресом Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   В этом примере значение IP-адреса указано после символов `inet addr:`. Этот адрес понадобится вам для удаленного подключения к Intel NUC с главного компьютера.

3. Используйте один из следующих SSH-клиентов для подключения к Intel NUC с главного компьютера.

    - [PuTTY](http://www.putty.org/) для Windows.
    - Встроенный SSH-клиент ОС Ubuntu или macOS.

   Работа с Intel NUC будет более эффективной, если подключиться к нему через SSH-клиент с главного компьютера. Для этого вам нужны IP-адрес Intel NUC, имя пользователя и пароль. Ниже приведен пример использования SSH-клиента в macOS.
   ![SSH-клиент, запущенный на macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-the-azure-iot-edge-package"></a>Установка пакета Edge Интернета вещей Azure

Пакет Edge Интернета вещей Azure содержит предварительно скомпилированные двоичные файлы самого пакета Edge Интернета вещей и его зависимостей. В список этих файлов входят Edge Интернета вещей Azure, пакет SDK для Интернета вещей Azure и соответствующие средства. Пакет также содержит пример приложения hello_world, который используется для проверки работоспособности шлюза. Edge Интернета вещей является основой шлюза. 

Для установки пакета выполните следующие действия.

1. Добавьте репозиторий облака Интернета вещей, выполнив в окне терминала следующие команды:

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > Введите "y", получив запрос "Include this channel?" (Включить этот канал?).
   
   Если произошла ошибка `import read failed(-1)`, можно решить эту проблему, выполнив следующие команды:
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   Команда `rpm` импортирует ключ RPM. Команда `smart channel` добавляет канал RPM в Smart Package Manager. Перед запуском команды `smart update` вы должны увидеть примерно такие результаты, как показано ниже.

   ![результаты выполнения команд rpm и smart channel](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. Выполните команду smart update:

   ```bash
   smart update
   ```

3. Установите пакет для шлюза Интернета вещей Azure, выполнив следующую команду:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   Здесь `packagegroup-cloud-azure` — это имя пакета. Команда `smart install` используется для установки пакета.

    > Если вы увидите ошибку "Открытый ключ недоступен", выполните следующую команду:

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > Перезагрузите Intel NUC, если отображается сообщение об ошибке "no package provides util-linux-dev" (нет пакета, предоставляющего util-linux-dev)

   Когда установка пакета завершится, Intel NUC будет готово выполнять функции шлюза.

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a>Запуск примера приложения hello_world из Edge Интернета вещей Azure

Этот пример приложения создает шлюз из файла `hello_world.json` и использует базовые компоненты архитектуры Edge Интернета вещей Azure, чтобы каждые 5 секунд записывать в журнал (log.txt) сообщение Hello World.

Чтобы запустить наш пример "Hello World", выполните следующие команды:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Оставьте приложение "Hello World" работать в течение нескольких минут, а затем остановите его, нажав клавишу ВВОД.
![выходные данные приложения](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

> Вы можете игнорировать любые ошибки "Недопустимый дескриптор аргумента (NULL)", которые появляются после нажатия клавиши ВВОД.

Убедитесь, что шлюз успешно работал, открыв файл log.txt, который был создан в папке приложения hello_world. ![Представление каталога с файлом log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)

Откройте файл log.txt с помощью следующей команды:

```bash
vim log.txt
```

Вы увидите содержимое log.txt, который содержит сообщения в формате JSON, создаваемые каждые 5 секунд нашим модулем шлюза "Hello World".
![Представление каталога log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)

Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Сводка

Поздравляем! Итак, вы завершили настройку Intel NUC в качестве шлюза. Теперь можно переходить к следующему уроку, в котором вы настроите главный компьютер, настроите Центр Интернета вещей Azure и зарегистрируете логическое устройство Центра Интернета вещей Azure.

## <a name="next-steps"></a>Дальнейшие действия
[Использование шлюза Интернета вещей для подключения устройства к Центру Интернета вещей Azure](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

