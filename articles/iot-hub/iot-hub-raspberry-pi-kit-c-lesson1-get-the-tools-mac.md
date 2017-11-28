---
title: "Connect Raspberry PI (C) tooAzure IoT — занятия 1: средства (macOS) | Документы Microsoft"
description: "Загрузите и установите необходимые инструменты hello и программного обеспечения для первого примера приложения hello пи на macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git на компьютере Mac, запуск Gulp, установка Node.js на компьютере Mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="e56d2-104">Получить средства hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="e56d2-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e56d2-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="e56d2-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="e56d2-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="e56d2-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="e56d2-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="e56d2-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="e56d2-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="e56d2-108">What you will do</span></span>
<span data-ttu-id="e56d2-109">Загрузите средства разработки hello и hello программное обеспечение для hello первый образец приложения для вашей Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="e56d2-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="e56d2-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e56d2-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e56d2-111">Хотя язык основная логика hello hello C, Node.js tools используются в устройствах toodiscover занятиях hello и постройте и разверните образцы приложений.</span><span class="sxs-lookup"><span data-stu-id="e56d2-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e56d2-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="e56d2-112">What you will learn</span></span>
<span data-ttu-id="e56d2-113">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="e56d2-113">In this article, you will learn:</span></span>

* <span data-ttu-id="e56d2-114">Как tooinstall Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="e56d2-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="e56d2-115">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="e56d2-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="e56d2-116">Пример приложения Hello для данной статьи хранится на Git.</span><span class="sxs-lookup"><span data-stu-id="e56d2-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="e56d2-117">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="e56d2-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="e56d2-118">Как toouse NPM tooinstall дополнительных Node.js средства разработки.</span><span class="sxs-lookup"><span data-stu-id="e56d2-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="e56d2-119">Минимальная требуемая версия Hello Node.js — 4,5 LTS.</span><span class="sxs-lookup"><span data-stu-id="e56d2-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="e56d2-120">[NPM](https://www.npmjs.com) является одним из hello диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="e56d2-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e56d2-121">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="e56d2-121">What you need</span></span>
<span data-ttu-id="e56d2-122">toocomplete этой операции вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e56d2-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="e56d2-123">Toodownload подключения Internet hello средства разработки и hello программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="e56d2-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="e56d2-124">Компьютер Mac под управлением Yosemite macOS (10.10) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e56d2-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="e56d2-125">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="e56d2-125">Install Git and Node.js</span></span>
<span data-ttu-id="e56d2-126">tooinstall Git и Node.js, использовать hello [Homebrew](http://brew.sh) пакета управления программы, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e56d2-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="e56d2-127">Установите Homebrew.</span><span class="sxs-lookup"><span data-stu-id="e56d2-127">Install Homebrew.</span></span> <span data-ttu-id="e56d2-128">Если Homebrew уже установлен, воспользуйтесь toostep 2.</span><span class="sxs-lookup"><span data-stu-id="e56d2-128">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="e56d2-129">Нажмите клавишу `Cmd + Space` и введите `Terminal` tooopen терминала.</span><span class="sxs-lookup"><span data-stu-id="e56d2-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="e56d2-130">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="e56d2-130">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="e56d2-131">Установите Git и Node.js, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e56d2-131">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="e56d2-132">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="e56d2-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="e56d2-133">Используйте [gulp.js](http://gulpjs.com) tooautomate развертывания hello tooyour приложения образец hello Pi.</span><span class="sxs-lookup"><span data-stu-id="e56d2-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Pi.</span></span> <span data-ttu-id="e56d2-134">Используйте hello [устройство обнаружения cli](https://github.com/Azure/device-discovery-cli) tooretrieve сети сведения об устройствах IoT.</span><span class="sxs-lookup"><span data-stu-id="e56d2-134">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="e56d2-135">Установка `gulp` и `device-discovery-cli` , выполнив следующую команду в терминале hello hello:</span><span class="sxs-lookup"><span data-stu-id="e56d2-135">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="e56d2-136">Если возникают проблемы с установкой Node.js и эти дополнительные средства разработки на macOS. в разделе hello [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md) для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="e56d2-136">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="e56d2-137">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e56d2-137">Install Visual Studio Code</span></span>
<span data-ttu-id="e56d2-138">[Скачайте](https://code.visualstudio.com/docs/setup/osx) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e56d2-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="e56d2-139">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="e56d2-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="e56d2-140">Этот редактор используется далее в коде образец hello учебника tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="e56d2-140">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="e56d2-141">Сводка</span><span class="sxs-lookup"><span data-stu-id="e56d2-141">Summary</span></span>
<span data-ttu-id="e56d2-142">Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e56d2-142">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="e56d2-143">Следующая задача Hello-toocreate, развернуть и запустить пример приложения hello на Pi.</span><span class="sxs-lookup"><span data-stu-id="e56d2-143">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e56d2-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e56d2-144">Next steps</span></span>
[<span data-ttu-id="e56d2-145">Создание и развертывание приложения hello мерцания</span><span class="sxs-lookup"><span data-stu-id="e56d2-145">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

