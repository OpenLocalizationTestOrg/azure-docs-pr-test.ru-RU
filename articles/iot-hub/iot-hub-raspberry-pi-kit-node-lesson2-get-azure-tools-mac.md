---
title: "Подключение Raspberry Pi (Node) к Azure IoT. Урок 2. Получение инструментов (Ubuntu) | Документация Майкрософт"
description: "Установите Python и интерфейс командной строки Azure (Azure CLI) на компьютер под управлением macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "облачная служба Интернета вещей, azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 1814b703-2d81-45db-aff0-eb338c97f120
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 12a8c5b20724e747f3799960a0bd39b82d7fa6b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a>Получение инструментов Azure (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 и более поздние версии](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Выполняемая задача
Установка интерфейса командной строки Azure (Azure CLI). Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Как установить Azure CLI.
* Как добавить подгруппу команд интерфейса командной строки Azure для Интернета вещей.

## <a name="what-you-need"></a>Необходимые элементы
* Компьютер под управлением Mac с подключением к Интернету.
* Активная подписка Azure. Если у вас нет учетной записи Azure, можно создать [бесплатную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.

## <a name="install-python"></a>Установка Python
Несмотря на то, что macOS поставляется уже с установленной версией Python 2.7, рекомендуется установить Python через Homebrew. См. статью [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/) (Установка Python на Mac OS X).

Установите Python и pip, выполнив следующую команду:

```bash
brew install python
```

## <a name="install-the-azure-cli"></a>Установка Azure CLI
Azure CLI — это кроссплатформенное средство для работы с командной строкой. С его помощью можно подготавливать ресурсы для Azure и управлять ими непосредственно в командной строке. 

Чтобы установить последнюю версию Azure CLI, выполните следующие действия:

1. Выполните следующие команды в окне терминала. Установка интерфейса командной строки Azure может занять около пяти минут.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Выполните следующую команду, чтобы проверить установку:

   ```bash
   az iot -h
   ```

Если установка прошла успешно, отобразятся следующие сведения.

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Сводка
Вы установили интерфейс командной строки Azure. Перейдите к следующей задаче: создайте Центр Интернета вещей Azure и удостоверение устройства с помощью интерфейса командной строки Azure.

## <a name="next-steps"></a>Дальнейшие действия
[Создание Центра Интернета вещей и регистрация Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

