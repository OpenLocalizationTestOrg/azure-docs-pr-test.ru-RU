---
title: "Подключение Arduino tooAzure IoT — занятия 1: средства (Windows) | Документы Microsoft"
description: "Загрузите и установите необходимые средства hello и программное обеспечение для первый пример приложения hello для Wi-Fi M0 Растушевка Adafruit в Windows 7 и более поздних версиях."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "инструменты для разработки Arduino, разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git в Windows, установка Node.js в Windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9cfb8cd2-eafb-4ba2-b23e-d94e114ff3a6
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4dd946da6c84293987e166fd1d17fac117e94e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a>Получить средства hello (Windows 7 или более поздней версии)

> [!div class="op_single_selector"]
> * [Windows 7 или более поздние версии][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Выполняемая задача

Загрузите средства разработки hello и hello программного обеспечения для первого примера приложения hello Adafruit Растушевка M0 Wi-Fi Arduino плата.

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

> [!NOTE]
> Хотя язык основная логика hello hello Arduino, Node.js tools используются в toobuild занятиях hello и развернуть образец приложения.

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:

* Как tooinstall Git и Node.js.
  * [Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом. Пример приложения Hello для данной статьи хранится на Git.
  * [Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.
* Как toouse NPM tooinstall дополнительных Node.js средства разработки.
  * Hello минимальное требование к версии Node.js — 4,5 LTS.
  * [NPM](https://www.npmjs.com) является одним из hello диспетчеров пакетов для Node.js.

## <a name="what-you-need"></a>Необходимые элементы

toocomplete этой операции вам потребуется:

* Toodownload подключения Internet hello средства разработки и hello программного обеспечения.
* Компьютер под управлением Windows.

## <a name="install-git-and-nodejs"></a>Установка Git и Node.js

Щелкните ссылки hello ниже toodownload и установите Git и LTS Node.js для Windows.

* [Скачать Git для Windows](https://git-scm.com/download/win/)
* [Скачать Node.js LTS для Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Установка дополнительных средств разработки для Node.js

Используйте [gulp.js](http://gulpjs.com) tooautomate развертывания hello hello образец приложения tooyour Arduino платы.

Запустите командную строку от имени администратора. Установка `gulp`, `device-discovery-cli` , выполнив следующую команду в терминале hello hello:

```bash
npm install -g gulp device-discovery-cli
```

Если возникают проблемы с установкой Node.js и следующим дополнительным средствам разработки Node.js на компьютере, см. раздел hello [руководство по устранению неполадок] [ troubleshooting] для решения проблемы toocommon.

## <a name="install-visual-studio-code"></a>Установка Visual Studio Code

[Скачайте](https://code.visualstudio.com/docs/setup/windows) и установите Visual Studio Code. Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS. Этот редактор используется далее в коде образец hello учебника tooedit hello.

## <a name="summary"></a>Сводка

Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello. Hello следующей задачей является toocreate, развернуть и запустить пример приложения hello в Arduino на доске.

## <a name="next-steps"></a>Дальнейшие действия

[Создание и развертывание образца приложения hello мерцания][create-and-deploy-the-blink-sample-application]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md