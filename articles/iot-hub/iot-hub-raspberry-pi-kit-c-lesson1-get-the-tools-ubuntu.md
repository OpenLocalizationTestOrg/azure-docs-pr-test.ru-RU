---
title: "Connect Raspberry PI (C) tooAzure IoT — занятия 1: средства (Ubuntu) | Документы Microsoft"
description: "Загрузите и установите на Ubuntu hello необходимых средств и программного обеспечения для первого примера приложения hello пи."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git в ubuntu, gulp run, установка node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 794928b5da63521cb0a72cb54256f2ad9724ec84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Получить средства hello (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 или более поздние версии](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Выполняемая задача
Загрузите средства разработки hello и hello программное обеспечение для hello первый образец приложения для вашей Raspberry Pi 3. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Хотя язык основная логика hello hello C, Node.js tools используются в устройствах toodiscover занятиях hello и постройте и разверните образцы приложений.

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:

* Как tooinstall Git и Node.js
  * [Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом. Пример приложения Hello для данной статьи хранится на Git.
  * [Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.
* Как toouse NPM tooinstall дополнительных Node.js средства разработки.
  * Минимальная требуемая версия Hello Node.js — 4,5 LTS.
  * [NPM](https://www.npmjs.com) является одним из hello диспетчеров пакетов для Node.js.

## <a name="what-you-need"></a>Необходимые элементы
toocomplete этой операции вам потребуется:

* Toodownload подключения Internet hello средства разработки и hello программного обеспечения.
* Компьютер под управлением Ubuntu 16.04 или более поздней версии.

## <a name="install-git-nodejs-and-npm"></a>Установка Git, Node.js и NPM
Используйте сочетание клавиш hello `Ctrl + Alt + T` tooopen hello терминалов и выполнения следующих команд:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Установка дополнительных средств разработки для Node.js
Используйте [gulp.js](http://gulpjs.com) tooautomate развертывания hello tooPi приложения образец hello. Используйте hello [устройство обнаружения cli](https://github.com/Azure/device-discovery-cli) tooretrieve сети сведения об устройствах IoT.

Установка `gulp` и `device-discovery-cli` , выполнив следующую команду в терминале hello hello:

```bash
sudo npm install -g device-discovery-cli gulp
```

Если возникают проблемы с установкой Node.js и эти дополнительные средства разработки на Ubuntu разделе hello [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md) для решения проблемы toocommon.

## <a name="install-visual-studio-code"></a>Установка Visual Studio Code
[Скачайте](https://code.visualstudio.com/docs/setup/linux) и установите Visual Studio Code. Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS. Этот редактор используется далее в коде образец hello учебника tooedit hello.

## <a name="summary"></a>Сводка
Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello. Следующая задача Hello-toocreate, развернуть и запустить пример приложения hello на Pi.

## <a name="next-steps"></a>Дальнейшие действия
[Создание и развертывание приложения hello мерцания](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

