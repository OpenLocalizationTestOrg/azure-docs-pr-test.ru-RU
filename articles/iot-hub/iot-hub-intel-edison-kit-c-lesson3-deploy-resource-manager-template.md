---
title: "Connect Intel Edison (C) tooAzure IoT — занятия 3: Создание приложения функции | Документы Microsoft"
description: "приложение Azure функции Hello прослушивает события концентратора IoT tooAzure, обрабатывает входящие сообщения и записывает их в хранилище таблиц tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "хранение данных в облаке hello, данные, хранящиеся в облаке, iot облачной службы"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 739b82e9-5d4e-4485-8971-f57cbb682faf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ef045ec2f44fe379a5e6c777d1bfb97de8b965a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Создание приложения-функции Azure и учетной записи хранения Azure
[Функции Azure](../../articles/azure-functions/functions-overview.md) — это решение для запуска легко *функции* (небольшие части кода) в облаке hello. Приложение Azure функция размещает hello выполнение функций в Azure.

## <a name="what-will-you-do"></a>Ваши действия
Используйте toocreate шаблона диспетчера ресурсов Azure, приложение Azure функции и учетная запись хранилища Azure. приложение Azure функции Hello прослушивает события концентратора IoT tooAzure, обрабатывает входящие сообщения и записывает их в хранилище таблиц tooAzure. Hello учетная запись хранения используется для чтения hello сохранения копии сообщений, из таблицы Azure. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-will-you-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Как toouse [диспетчера ресурсов Azure](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure ресурсы.
* Как toouse Azure функцией приложения tooprocess IoT hub сообщения и записывать их в таблице tooa в хранилище таблиц Azure.

## <a name="what-do-you-need"></a>Требования
Необходимо успешно выполнить инструкции, изложенные в следующих статьях:
- [Начало работы с Intel Edison (Node.js)][get-started-with-your-intel-edison]
- [Create your Azure IoT hub][create-your-azure-iot-hub] (Создание Центра Интернета вещей Azure)

## <a name="open-hello-sample-app"></a>Пример приложения Open hello
Откройте образец hello проекта в Visual Studio Code, выполнив следующие команды hello:

```bash
cd Lesson3
code .
```

![Структура репозитория][repo-structure]

* файл Hello в hello `app` подпапка является hello ключа исходного файла. Этот исходный файл содержит код hello toosend сообщение 20 раз tooyour IoT hub и blink hello Индикатора для каждого сообщения, он отправляет.
* Hello `arm-template.json` файла является шаблон hello диспетчера ресурсов Azure, который содержит приложение Azure функции и учетная запись хранилища Azure.
* Hello `arm-template-param.json` файл является файлом конфигурации hello, используемые hello шаблона диспетчера ресурсов Azure.
* Hello `ReceiveDeviceMessages` вложенная папка содержит код Node.js hello Azure функции hello.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Настройка шаблонов Azure Resource Manager и создание ресурсов в Azure
Обновление hello `arm-template-param.json` файл в Visual Studio Code.

![Параметры шаблона Azure Resource Manager][arm-template-parameters]

* Замените **[your IoT Hub name]** своим **{именем центра}**, которое вы указали при [создании Центра Интернета вещей и регистрации Intel Edison][created-your-iot-hub-and-registered-intel-edison].
* Замените **[строку-префикс для новых ресурсов]** любым префиксом по вашему усмотрению. префикс Hello гарантирует, что имя ресурса hello является глобально уникальным tooavoid конфликт. Не используйте символы дефиса или номер начальной hello префикса.

После обновления hello `arm-template-param.json` файлов, развертывание, выполнив следующую команду hello tooAzure ресурсы hello:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Занимает около пяти минут toocreate эти ресурсы. Во время создания ресурса hello можно переместить в следующей статье toohello.

## <a name="summary"></a>Сводка
Вы создали вашей tooprocess приложения Azure функция IoT hub сообщений и учетной записи хранилища Azure toostore эти сообщения. Теперь можно развернуть и запустить на Edison сообщения из устройства в облако toosend образец hello.

## <a name="next-steps"></a>Дальнейшие действия
[Запустите образец приложения toosend сообщения из устройства в облако на Intel Edison][send-device-to-cloud-messages].
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-c-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure_c.png
[arm-template-parameters]: /media/iot-hub-intel-edison-lessons/lesson3/arm_para_c.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md