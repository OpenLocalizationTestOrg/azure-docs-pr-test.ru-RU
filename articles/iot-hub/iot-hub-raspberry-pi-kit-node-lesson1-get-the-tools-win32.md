---
title: "Подключение Raspberry Pi (узел) tooAzure IoT — занятия 1: средства (Windows) | Документы Microsoft"
description: "Загрузите и установите необходимые средства hello и программное обеспечение для hello первый образец приложения для платформы на Windows 7 и более поздних версиях."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git в Windows, gulp run, установка node js в Windows, установка npm в Windows, установка python в Windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ea7f77cc79c70c8c7952b63462b926471fcf71cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a>Получить средства hello (Windows 7 или более поздней версии)

> [!div class="op_single_selector"]
> * [Windows 7 или более поздние версии](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a>Выполняемая задача
Загрузите средства разработки hello и hello программное обеспечение для первый пример приложения hello для Raspberry Pi 3. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

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
Щелкните следующие ссылки toodownload hello и установите Git и LTS Node.js для Windows.

* [Скачать Git для Windows](https://git-scm.com/download/win/)
* [Скачать Node.js LTS для Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Установка дополнительных средств разработки для Node.js
Используйте [gulp.js](http://gulpjs.com) tooautomate развертывания hello tooPi приложения образец hello. Можно также использовать hello [устройство обнаружения cli](https://github.com/Azure/device-discovery-cli) tooretrieve сети сведения об устройствах IoT.

Запустите командную строку от имени администратора. Установка `gulp` и `device-discovery-cli` , выполнив следующую команду hello:

```bash
npm install -g device-discovery-cli gulp
```

Если возникают проблемы с установкой Node.js и следующим дополнительным средствам разработки Node.js на компьютере, см. раздел hello [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md) для решения проблемы toocommon.

## <a name="install-visual-studio-code"></a>Установка Visual Studio Code
[Скачайте](https://code.visualstudio.com/docs/setup/windows) и установите Visual Studio Code. Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS. Этот редактор используется далее в коде образец hello учебника tooedit hello.

## <a name="summary"></a>Сводка
Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello. Следующая задача Hello-toocreate, развернуть и запустить пример приложения hello на Pi.

## <a name="next-steps"></a>Дальнейшие действия
[Создание и развертывание образца приложения hello мерцания](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

