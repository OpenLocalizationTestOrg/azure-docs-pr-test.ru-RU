---
title: "Connect Intel Edison (C) tooAzure IoT — занятия 1: средства (macOS) | Документы Microsoft"
description: "Загрузите и установите необходимые средства hello и программное обеспечение для первый пример приложения hello для Edison на macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "инструменты для разработки Arduino, разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git на компьютере Mac, установка Node.js на компьютере Mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 3f764f2e-25fa-4dde-9e8d-d278453fccfd
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a53331b0dce73c3dd51de91f07df86e28cbb6b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Получить средства hello (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 или более поздние версии][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Выполняемая задача
Загрузите средства разработки hello и hello программное обеспечение для hello первый образец приложения для вашей Edison Intel. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

> [!NOTE]
> Хотя язык основная логика hello hello C, Node.js tools используются в toobuild занятиях hello и развернуть образец приложения.

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:

* Как tooinstall Git и Node.js.
  * [Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом. Пример приложения Hello для данной статьи хранится на Git.
  * [Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.
* Как toouse NPM tooinstall дополнительных Node.js средства разработки.
  * Минимальная требуемая версия Hello Node.js — 4,5 LTS.
  * [NPM](https://www.npmjs.com) является одним из hello диспетчеров пакетов для Node.js.

## <a name="what-you-need"></a>Необходимые элементы
toocomplete этой операции вам потребуется:
* Toodownload подключения Internet hello средства разработки и hello программного обеспечения.
* Компьютер Mac под управлением Yosemite macOS (10.10) или более поздней версии.

## <a name="install-git-and-nodejs"></a>Установка Git и Node.js
tooinstall Git и Node.js, использовать hello [Homebrew](http://brew.sh) пакета управления программы, выполните следующие действия:

1. Установите Homebrew. Если Homebrew уже установлен, воспользуйтесь toostep 2.

   1. Нажмите клавишу `Cmd + Space` и введите `Terminal` tooopen терминала.
   2. Выполните следующую команду hello.

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Установите Git и Node.js, выполнив следующую команду hello:

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Установка дополнительных средств разработки для Node.js
Используйте [gulp.js](http://gulpjs.com) tooautomate развертывания hello hello образец приложения tooyour Edison.

Установить `gulp` , выполнив следующую команду в терминале hello hello:

```bash
sudo npm install -g gulp
```

Если возникают проблемы с установкой Node.js и эти дополнительные средства разработки на macOS. в разделе hello [руководство по устранению неполадок] [ troubleshooting] для решения проблемы toocommon.

## <a name="install-visual-studio-code"></a>Установка Visual Studio Code
[Скачайте](https://code.visualstudio.com/docs/setup/osx) и установите Visual Studio Code. Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS. Этот редактор используется далее в коде образец hello учебника tooedit hello.

## <a name="summary"></a>Сводка
Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello. Hello следующей задачей является toocreate, развернуть и запустить пример приложения hello на Edison.

## <a name="next-steps"></a>Дальнейшие действия
[Создание и развертывание приложения hello мерцания][create-and-deploy-the-blink-application]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
