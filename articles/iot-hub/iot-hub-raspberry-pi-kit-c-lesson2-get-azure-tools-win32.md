---
title: "Connect Raspberry PI (C) tooAzure IoT — Lesson 2: инструменты Azure (Windows) | Документы Microsoft"
description: "Установите Python и hello Azure командной строки (CLI Azure) на Windows 7 и более поздних версиях."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "облачная служба Интернета вещей, azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a3c083b5-0d76-46af-bc77-2ad7d8aadc1e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1819d61fafbee6ac42a1bea5c16437cd8bf43af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Получение инструментов Azure (Windows 7 и более поздние версии)
> [!div class="op_single_selector"]
> * [Windows 7 и более поздние версии](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Выполняемая задача
Установите Python и hello Azure командной строки (CLI Azure). Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Как tooinstall Python.
* Как tooinstall hello Azure CLI.

## <a name="what-you-need"></a>Необходимые элементы
* Компьютер под управлением Windows с подключением к Интернету.
* Активная подписка Azure. Если ее нет, можно создать [бесплатную пробную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.

## <a name="install-python"></a>Установка Python
[Установите Python](https://www.python.org/downloads/) на компьютере под управлением Windows. Установить можно такие версии Python: 2.7, 3.4 или 3.5. Это руководство основано на версии Python 2.7. Если Python уже установлен, перейдите следующему разделу toohello и установите hello Azure CLI.

Необходимо также tooadd hello путь к папкам hello, где python.exe и pip.exe — установленных toohello системы `PATH` переменной среды. По умолчанию файл python.exe устанавливается в папку `C:\Python27`, а pip.exe — в `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Установка hello Azure CLI
Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure. Работа непосредственно из вашего tooprovision командной строки и управления ресурсами.

tooinstall hello Azure CLI, выполните следующие действия.

1. Откройте окно командной строки с правами администратора.
2. Выполните следующие команды hello.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Проверка установки hello, выполнив следующую команду hello:

   ```bash
   az iot -h
   ```

Вы увидите, что hello следующие выходные данные, если hello успешно установлен.

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>Сводка
После установки hello Azure CLI. Следующего задач toocreate вашу личность Azure IoT hub и устройств с помощью hello Azure CLI.

## <a name="next-steps"></a>Дальнейшие действия
[Создание Центра Интернета вещей и регистрация Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

