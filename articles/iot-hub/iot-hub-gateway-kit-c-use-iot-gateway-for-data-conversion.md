---
title: "Преобразование aaaData на шлюзе IoT Azure IoT границу | Документы Microsoft"
description: "Используйте формат hello tooconvert IoT шлюз данных датчика с помощью специализированный модуль Azure IoT края."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "преобразование данных в шлюзе Интернета вещей, преобразование данных в шлюзе IoT"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a>Использование шлюза Интернета вещей для преобразования данных датчиков с помощью Edge Интернета вещей

> [!NOTE]
> Перед началом этого учебника, убедитесь, что вы уже завершенной hello в следующих занятиях:
> * [Настройка Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [Использование облачного toohello действия tooconnect шлюза IoT - SensorTag tooAzure центра IoT](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

Один шлюз Iot предназначен tooprocess собранных данных перед их отправкой toohello облака. Azure IoT Edge вводит модули, которые могут быть созданы и собранный tooform hello обработки данных, рабочий процесс. Модуль получает сообщение, выполняет некоторые действия с его и затем переместить ее для других модулей tooprocess.

## <a name="what-you-learn"></a>Что вы узнаете

Вы узнаете, как toocreate tooconvert модуль сообщений hello SensorTag в другой формат.

## <a name="what-you-do"></a>В рамках этого руководства мы:

* Создание tooconvert модуль полученного сообщения в формате .json hello.
* Скомпилируйте модуль hello.
* Добавьте hello модуля toohello ЛЮЧИТЬ образец приложения Azure IoT края.
* Запустите образец приложения hello.

## <a name="what-you-need"></a>Необходимые элементы

* После завершения в последовательности учебники Hello:
  * [Настройка Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [Использование облачного toohello действия tooconnect шлюза IoT - SensorTag tooAzure центра IoT](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* Клиент SSH, который выполняется на главном компьютере. В Windows рекомендуется использовать PuTTY. Клиент SSH изначально входит в состав ОС Linux и Mac OS.
* Hello IP-адрес и hello имя пользователя и пароль tooaccess hello шлюза из клиента SSH hello.
* Подключение к Интернету.

## <a name="create-a-module"></a>Создание модуля

1. На главном компьютере hello запустите клиент SSH hello и шлюз IoT toohello подключения.
1. Клонирование hello исходные файлы hello преобразования модуля из GitHub toohello шлюза IoT hello в домашнем каталоге, выполнив следующие команды hello:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   Это собственный модуль Azure Edge на языке hello языка программирования. модуль Hello преобразует формат hello полученных сообщений в одном hello:

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a>Скомпилируйте модуль hello

hello модуль toocompile, запустите hello, следующие команды:

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

Вы получаете `libmy_module.so` файла после завершения компиляции hello. Запишите hello абсолютный путь этого файла.

## <a name="add-hello-module-toohello-ble-sample-application"></a>Добавить hello модуля toohello ЛЮЧИТЬ примера приложения

1. Папка образцов перейдите toohello, выполнив следующую команду hello:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. Откройте файл конфигурации hello, выполнив следующую команду hello:

   ```bash
   vi ble_gateway.json
   ```

1. Добавить модуль, вставив следующий код toohello hello `modules` раздела.

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. Замените `[Your libmy_module.so path]` в коде hello hello абсолютном пути hello libmy_module.so "файла.
1. Замените код hello в hello `links` раздел с hello, выполнив одно:

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. Нажмите клавишу `ESC`, а затем введите `:wq` toosave hello файла.

## <a name="run-hello-sample-application"></a>Запустить образец приложения hello

1. Включите hello SensorTag.
1. Задайте переменную среды SSL_CERT_FILE hello, выполнив hello следующую команду:

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. Выполните пример приложения hello с hello добавленный модуль, выполнив следующую команду hello:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Дальнейшие действия

Вы успешно использовать hello IoT шлюза tooconvert приветственных сообщений из SensorTag в формат .json hello.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
