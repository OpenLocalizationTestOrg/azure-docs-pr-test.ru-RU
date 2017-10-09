---
title: "Connect Intel Edison (C) tooAzure IoT — Lesson 2: инструменты Azure (macOS) | Документы Microsoft"
description: "Установка Python и интерфейса командной строки Azure (Azure CLI) на компьютер под управлением macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure CLI, облачная служба Интернета вещей, облако Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0dfc9ff90e879d5fd03040016ac71a9fe4f4a744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Получение инструментов Azure (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 и более поздние версии][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Выполняемая задача
Установите hello Azure командной строки (CLI Azure). Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Как tooinstall Azure CLI.
* Как tooadd IoT подгруппой hello Azure CLI.

## <a name="what-you-need"></a>Необходимые элементы
* Компьютер под управлением Mac с подключением к Интернету.
* Активная подписка Azure. Если у вас нет учетной записи Azure, можно создать [бесплатную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.

## <a name="install-python"></a>Установка Python
Несмотря на то, что macOS поставляется с Python 2.7 стандартной hello, рекомендуется установить Python через Homebrew. См. статью [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/) (Установка Python на Mac OS X).

Установите Python и pip, выполнив следующую команду hello:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Установка hello Azure CLI
Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure. Работа непосредственно из вашего tooprovision командной строки и управления ресурсами. 

tooinstall Здравствуйте последнюю Azure CLI, выполните следующие действия:

1. Выполните следующие команды в окне терминала hello. Может потребоваться пять минут tooinstall hello Azure CLI.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Проверка установки hello, выполнив следующую команду hello:

   ```bash
   az iot -h
   ```

Вы увидите следующее hello выходных данных, если hello успешно установлен.

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Сводка
После установки hello Azure CLI. Следующая задача — toocreate Azure IoT идентификаторов концентратора и устройств с помощью hello Azure CLI.

## <a name="next-steps"></a>Дальнейшие действия
[Создание Центра Интернета вещей и регистрация Intel Edison][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
