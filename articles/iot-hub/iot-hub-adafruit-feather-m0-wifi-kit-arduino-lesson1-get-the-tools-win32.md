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
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="13c9c-104">Получить средства hello (Windows 7 или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="13c9c-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="13c9c-105">[Windows 7 или более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="13c9c-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="13c9c-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="13c9c-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="13c9c-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="13c9c-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="13c9c-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="13c9c-108">What you will do</span></span>

<span data-ttu-id="13c9c-109">Загрузите средства разработки hello и hello программного обеспечения для первого примера приложения hello Adafruit Растушевка M0 Wi-Fi Arduino плата.</span><span class="sxs-lookup"><span data-stu-id="13c9c-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="13c9c-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="13c9c-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="13c9c-111">Хотя язык основная логика hello hello Arduino, Node.js tools используются в toobuild занятиях hello и развернуть образец приложения.</span><span class="sxs-lookup"><span data-stu-id="13c9c-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="13c9c-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="13c9c-112">What you will learn</span></span>
<span data-ttu-id="13c9c-113">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="13c9c-113">In this article, you will learn:</span></span>

* <span data-ttu-id="13c9c-114">Как tooinstall Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="13c9c-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="13c9c-115">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="13c9c-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="13c9c-116">Пример приложения Hello для данной статьи хранится на Git.</span><span class="sxs-lookup"><span data-stu-id="13c9c-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="13c9c-117">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="13c9c-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="13c9c-118">Как toouse NPM tooinstall дополнительных Node.js средства разработки.</span><span class="sxs-lookup"><span data-stu-id="13c9c-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="13c9c-119">Hello минимальное требование к версии Node.js — 4,5 LTS.</span><span class="sxs-lookup"><span data-stu-id="13c9c-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="13c9c-120">[NPM](https://www.npmjs.com) является одним из hello диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="13c9c-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="13c9c-121">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="13c9c-121">What you need</span></span>

<span data-ttu-id="13c9c-122">toocomplete этой операции вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="13c9c-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="13c9c-123">Toodownload подключения Internet hello средства разработки и hello программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="13c9c-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="13c9c-124">Компьютер под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="13c9c-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="13c9c-125">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="13c9c-125">Install Git and Node.js</span></span>

<span data-ttu-id="13c9c-126">Щелкните ссылки hello ниже toodownload и установите Git и LTS Node.js для Windows.</span><span class="sxs-lookup"><span data-stu-id="13c9c-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="13c9c-127">Скачать Git для Windows</span><span class="sxs-lookup"><span data-stu-id="13c9c-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="13c9c-128">Скачать Node.js LTS для Windows</span><span class="sxs-lookup"><span data-stu-id="13c9c-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="13c9c-129">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="13c9c-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="13c9c-130">Используйте [gulp.js](http://gulpjs.com) tooautomate развертывания hello hello образец приложения tooyour Arduino платы.</span><span class="sxs-lookup"><span data-stu-id="13c9c-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="13c9c-131">Запустите командную строку от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="13c9c-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="13c9c-132">Установка `gulp`, `device-discovery-cli` , выполнив следующую команду в терминале hello hello:</span><span class="sxs-lookup"><span data-stu-id="13c9c-132">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g gulp device-discovery-cli
```

<span data-ttu-id="13c9c-133">Если возникают проблемы с установкой Node.js и следующим дополнительным средствам разработки Node.js на компьютере, см. раздел hello [руководство по устранению неполадок] [ troubleshooting] для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="13c9c-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="13c9c-134">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="13c9c-134">Install Visual Studio Code</span></span>

<span data-ttu-id="13c9c-135">[Скачайте](https://code.visualstudio.com/docs/setup/windows) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="13c9c-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="13c9c-136">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="13c9c-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="13c9c-137">Этот редактор используется далее в коде образец hello учебника tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="13c9c-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="13c9c-138">Сводка</span><span class="sxs-lookup"><span data-stu-id="13c9c-138">Summary</span></span>

<span data-ttu-id="13c9c-139">Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="13c9c-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="13c9c-140">Hello следующей задачей является toocreate, развернуть и запустить пример приложения hello в Arduino на доске.</span><span class="sxs-lookup"><span data-stu-id="13c9c-140">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13c9c-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="13c9c-141">Next steps</span></span>

<span data-ttu-id="13c9c-142">[Создание и развертывание образца приложения hello мерцания][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="13c9c-142">[Create and deploy hello blink sample application][create-and-deploy-the-blink-sample-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md