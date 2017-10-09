---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 4. Создание приложения-функции | Документация Майкрософт"
description: "Сохранять сообщения из центра IoT tooyour Intel NUC, записывать их в хранилище таблиц tooAzure и затем прочитать их из облака hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "хранение данных в облаке hello, данные, хранящиеся в облаке, iot облачной службы"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Создание приложения-функции Azure и учетной записи хранения Azure

Функции Azure — это решение для запуска легко _функции_ (небольшие части кода) в облаке hello. Приложение Azure функция размещает hello выполнение функций в Azure. 

## <a name="what-you-will-do"></a>Выполняемая задача

- Используйте toocreate шаблона диспетчера ресурсов Azure, приложение Azure функции и учетная запись хранилища Azure. приложение Azure функции Hello прослушивает события концентратора IoT tooAzure, обрабатывает входящие сообщения и записывает их в хранилище таблиц tooAzure.

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).


## <a name="what-you-will-learn"></a>Новые знания

Из этого урока вы узнаете:

- Как Azure Resource Manager toodeploy toouse ресурсов Azure.
- Как toouse Azure функцией tooprocess приложения центра IoT сообщения и записи таблицы tooa в хранилище таблиц Azure.

## <a name="what-you-need"></a>Необходимые элементы

Необходимо успешно выполнить предыдущие занятия hello:

- [Урок 1. Настройка Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [Урок 2. Подготовка главного компьютера и Центра Интернета вещей Azure](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [Урок 3. Получение сообщений из SensorTag и чтение сообщений из Центра Интернета вещей](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a>Открытие примера приложения

Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` репозитория папки, файлы конфигурации hello initialize и hello откройте образец проекта в Visual Studio Code, выполнив следующую команду hello:

```bash
cd Lesson4
npm install
gulp init
code .
```

![структура репозитория](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- Hello `arm-template.json` файла является шаблон hello диспетчера ресурсов Azure, который содержит приложение Azure функции и учетная запись хранилища Azure.
- Hello `arm-template-param.json` файл является файлом конфигурации hello, используемые hello шаблона диспетчера ресурсов Azure.
- Hello `ReceiveDeviceMessages` вложенная папка содержит код Node.js hello Azure функции hello.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Настройка шаблонов Azure Resource Manager и создание ресурсов в Azure

Обновление hello `arm-template-param.json` файл в Visual Studio Code.

![JSON-файл шаблона ARM](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Замените `[your IoT Hub name]` именем `{my hub name}`, указанным в уроке 2.

После обновления hello `arm-template-param.json` файлов, развертывание, выполнив следующую команду hello tooAzure ресурсы hello:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Используйте `iot-gateway` в качестве значения hello `{resource group name}` Если вы не изменили значение hello в занятии 2.

## <a name="summary"></a>Сводка

Вы создали вашей tooprocess приложения Azure функция IoT hub сообщений и учетной записи хранилища Azure toostore эти сообщения. Теперь можно считывать сообщения, отправляемые с вашего центра IoT tooyour шлюза.

## <a name="next-steps"></a>Дальнейшие действия
[Чтение сообщений, сохраненных в службе хранилища Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md)
