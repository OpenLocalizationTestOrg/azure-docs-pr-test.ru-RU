---
title: "Подключение Raspberry Pi (узел) tooAzure IoT — занятия 1: средства (macOS) | Документы Microsoft"
description: "Загрузите и установите необходимые инструменты hello и программного обеспечения для первого примера приложения hello пи на macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка python mac, установка git в mac, gulp run, установка node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 382b066cb7ece7ffdeb22b162b725727b22e5fac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="a92bf-104">Получить средства hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="a92bf-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a92bf-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="a92bf-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="a92bf-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="a92bf-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="a92bf-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="a92bf-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="a92bf-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="a92bf-108">What you will do</span></span>
<span data-ttu-id="a92bf-109">Загрузите средства разработки hello и hello программное обеспечение для hello первый образец приложения для вашей Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a92bf-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="a92bf-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a92bf-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a92bf-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="a92bf-111">What you will learn</span></span>
<span data-ttu-id="a92bf-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="a92bf-112">In this article, you will learn:</span></span>

* <span data-ttu-id="a92bf-113">Как tooinstall Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="a92bf-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="a92bf-114">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="a92bf-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="a92bf-115">Пример приложения Hello для данной статьи хранится на Git.</span><span class="sxs-lookup"><span data-stu-id="a92bf-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="a92bf-116">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="a92bf-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="a92bf-117">Как toouse NPM tooinstall дополнительных Node.js средства разработки.</span><span class="sxs-lookup"><span data-stu-id="a92bf-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="a92bf-118">Минимальная требуемая версия Hello Node.js — 4,5 LTS.</span><span class="sxs-lookup"><span data-stu-id="a92bf-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="a92bf-119">[NPM](https://www.npmjs.com) является одним из hello диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="a92bf-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a92bf-120">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="a92bf-120">What you need</span></span>
<span data-ttu-id="a92bf-121">toocomplete этой операции вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a92bf-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="a92bf-122">Toodownload подключения Internet hello средства разработки и hello программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="a92bf-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="a92bf-123">Компьютер Mac под управлением Yosemite macOS (10.10) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a92bf-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="a92bf-124">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="a92bf-124">Install Git and Node.js</span></span>
<span data-ttu-id="a92bf-125">tooinstall Git и Node.js, использовать hello [Homebrew](http://brew.sh) пакета управления программы, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a92bf-125">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="a92bf-126">Установите Homebrew.</span><span class="sxs-lookup"><span data-stu-id="a92bf-126">Install Homebrew.</span></span> <span data-ttu-id="a92bf-127">Если Homebrew уже установлен, воспользуйтесь toostep 2.</span><span class="sxs-lookup"><span data-stu-id="a92bf-127">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="a92bf-128">Нажмите клавишу `Cmd + Space` и введите `Terminal` tooopen терминала.</span><span class="sxs-lookup"><span data-stu-id="a92bf-128">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="a92bf-129">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="a92bf-129">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="a92bf-130">Установите Git и Node.js, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="a92bf-130">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="a92bf-131">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="a92bf-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="a92bf-132">Используйте [gulp.js](http://gulpjs.com) tooautomate развертывания hello tooPi приложения образец hello.</span><span class="sxs-lookup"><span data-stu-id="a92bf-132">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="a92bf-133">Используйте hello [устройство обнаружения cli](https://github.com/Azure/device-discovery-cli) tooretrieve сети сведения об устройствах IoT.</span><span class="sxs-lookup"><span data-stu-id="a92bf-133">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="a92bf-134">Установка `gulp` и `device-discovery-cli` , выполнив следующую команду в терминале hello hello:</span><span class="sxs-lookup"><span data-stu-id="a92bf-134">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="a92bf-135">Если возникают проблемы с установкой Node.js и эти дополнительные средства разработки на macOS. в разделе hello [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md) для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="a92bf-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="a92bf-136">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a92bf-136">Install Visual Studio Code</span></span>
<span data-ttu-id="a92bf-137">[Скачайте](https://code.visualstudio.com/docs/setup/osx) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a92bf-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="a92bf-138">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="a92bf-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="a92bf-139">Этот редактор используется далее в коде образец hello учебника tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="a92bf-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="a92bf-140">Сводка</span><span class="sxs-lookup"><span data-stu-id="a92bf-140">Summary</span></span>
<span data-ttu-id="a92bf-141">Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a92bf-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="a92bf-142">Следующая задача Hello-toocreate, развернуть и запустить пример приложения hello на Pi.</span><span class="sxs-lookup"><span data-stu-id="a92bf-142">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a92bf-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a92bf-143">Next steps</span></span>
[<span data-ttu-id="a92bf-144">Создание и развертывание образца приложения hello мерцания</span><span class="sxs-lookup"><span data-stu-id="a92bf-144">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

