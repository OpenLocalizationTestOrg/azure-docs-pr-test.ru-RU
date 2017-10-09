---
title: "Connect Raspberry PI (C) tooAzure IoT — Lesson 2: инструменты Azure (Ubuntu) | Документы Microsoft"
description: "Установка Python и интерфейса командной строки Azure (Azure CLI) на компьютер под управлением Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "облачная служба Интернета вещей, azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a03512f2-fabe-40c5-8505-b93eef8e5bec
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1af4848f9fe0508e362c15b36eec8a35aea9ac5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Получение инструментов Azure (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 и более поздние версии](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Выполняемая задача
Установите hello Azure командной строки (CLI Azure). Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Как tooinstall hello Azure CLI.
* Как tooadd IoT подгруппой hello Azure CLI.

## <a name="what-you-need"></a>Необходимые элементы
* Компьютер под управлением Ubuntu с подключением к Интернету.
* Активная подписка Azure. Если у вас нет учетной записи, можно создать [бесплатную учетную запись](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.

## <a name="install-hello-azure-cli"></a>Установка hello Azure CLI
Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure, позволяя toowork непосредственно из вашего tooprovision командной строки и управлять ресурсами.

tooinstall Здравствуйте последнюю Azure CLI, выполните следующие действия:

1. Выполните следующие команды в окне терминала hello. Может потребоваться пять минут tooinstall hello Azure CLI.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Проверка установки hello, выполнив следующую команду hello:

   ```bash
   az iot -h
   ```

Вы увидите следующее hello выходных данных, если hello успешно установлен.

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a>Сводка
После установки hello Azure CLI. Следующая задача — toocreate центр Azure IoT и устройствами с помощью удостоверения hello Azure CLI.

## <a name="next-steps"></a>Дальнейшие действия
[Создание Центра Интернета вещей и регистрация Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

