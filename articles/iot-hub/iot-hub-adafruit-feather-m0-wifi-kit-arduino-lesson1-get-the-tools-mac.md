---
title: "Подключение Arduino tooAzure IoT — занятия 1: средства (macOS) | Документы Microsoft"
description: "Загрузите и установите необходимые средства hello и программное обеспечение для первый пример приложения hello для Wi-Fi M0 Растушевка Adafruit на macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "инструменты для разработки Arduino, разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git на компьютере Mac, установка Node.js на компьютере Mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5fd306fecd7259fb8f1e99d76282a1e464c4d4f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="81e20-104">Получить средства hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="81e20-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="81e20-105">[Windows 7 или более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="81e20-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="81e20-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="81e20-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="81e20-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="81e20-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="81e20-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="81e20-108">What you will do</span></span>

<span data-ttu-id="81e20-109">Загрузите средства разработки hello и hello программного обеспечения для первого примера приложения hello Adafruit Растушевка M0 Wi-Fi Arduino плата.</span><span class="sxs-lookup"><span data-stu-id="81e20-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="81e20-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="81e20-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="81e20-111">Хотя язык основная логика hello hello Arduino, Node.js tools используются в toobuild занятиях hello и развернуть образец приложения.</span><span class="sxs-lookup"><span data-stu-id="81e20-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="81e20-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="81e20-112">What you will learn</span></span>
<span data-ttu-id="81e20-113">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="81e20-113">In this article, you will learn:</span></span>

* <span data-ttu-id="81e20-114">Как tooinstall Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="81e20-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="81e20-115">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="81e20-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="81e20-116">Пример приложения Hello для данной статьи хранится на Git.</span><span class="sxs-lookup"><span data-stu-id="81e20-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="81e20-117">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="81e20-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="81e20-118">Как toouse NPM tooinstall дополнительных Node.js средства разработки.</span><span class="sxs-lookup"><span data-stu-id="81e20-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="81e20-119">Минимальная требуемая версия Hello Node.js — 4,5 LTS.</span><span class="sxs-lookup"><span data-stu-id="81e20-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="81e20-120">[NPM](https://www.npmjs.com) является одним из hello диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="81e20-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="81e20-121">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="81e20-121">What you need</span></span>
<span data-ttu-id="81e20-122">toocomplete этой операции вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="81e20-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="81e20-123">Toodownload подключения Internet hello средства разработки и hello программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="81e20-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="81e20-124">Компьютер Mac под управлением Yosemite macOS (10.10) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="81e20-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="81e20-125">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="81e20-125">Install Git and Node.js</span></span>
<span data-ttu-id="81e20-126">tooinstall Git и Node.js, использовать hello [Homebrew](http://brew.sh) пакета управления программы, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="81e20-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="81e20-127">Установите Homebrew.</span><span class="sxs-lookup"><span data-stu-id="81e20-127">Install Homebrew.</span></span> <span data-ttu-id="81e20-128">Если Homebrew уже установлен, воспользуйтесь toostep 2.</span><span class="sxs-lookup"><span data-stu-id="81e20-128">If you've already installed Homebrew, go toostep 2.</span></span>

   1. <span data-ttu-id="81e20-129">Нажмите клавишу `Cmd + Space` и введите `Terminal` tooopen терминала.</span><span class="sxs-lookup"><span data-stu-id="81e20-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="81e20-130">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="81e20-130">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="81e20-131">Установите Git и Node.js, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="81e20-131">Install Git and Node.js by running hello following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="81e20-132">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="81e20-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="81e20-133">Используйте [gulp.js](http://gulpjs.com) tooautomate развертывания hello hello образец приложения tooyour Arduino платы.</span><span class="sxs-lookup"><span data-stu-id="81e20-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="81e20-134">Установка `gulp`, `device-discovery-cli` , выполнив следующую команду в терминале hello hello:</span><span class="sxs-lookup"><span data-stu-id="81e20-134">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="81e20-135">Если возникают проблемы с установкой Node.js и эти дополнительные средства разработки на macOS. в разделе hello [руководство по устранению неполадок] [ troubleshooting] для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="81e20-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="81e20-136">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="81e20-136">Install Visual Studio Code</span></span>
<span data-ttu-id="81e20-137">[Скачайте](https://code.visualstudio.com/docs/setup/osx) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="81e20-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="81e20-138">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="81e20-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="81e20-139">Этот редактор используется далее в коде образец hello учебника tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="81e20-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="81e20-140">Сводка</span><span class="sxs-lookup"><span data-stu-id="81e20-140">Summary</span></span>
<span data-ttu-id="81e20-141">Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="81e20-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="81e20-142">Hello следующей задачей является toocreate, развернуть и запустить пример приложения hello в Arduino на доске.</span><span class="sxs-lookup"><span data-stu-id="81e20-142">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81e20-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="81e20-143">Next steps</span></span>
<span data-ttu-id="81e20-144">[Создание и развертывание приложения hello мерцания][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="81e20-144">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md