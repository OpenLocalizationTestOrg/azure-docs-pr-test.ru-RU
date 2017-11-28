---
title: "Подключение Edison Intel (узел) tooAzure IoT — занятия 1: средства (Ubuntu) | Документы Microsoft"
description: "Загрузите и установите необходимые средства hello и программное обеспечение для первый пример приложения hello для Edison на Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "инструменты для разработки Arduino, разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git в Ubuntu, установка Node.js в Ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 9ab5b161-7ec5-41a6-9c5f-4456e4882752
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ad1a48708bd74bcc07d09f105f597f18c3f9d2b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="df916-104">Получить средства hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="df916-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="df916-105">[Windows 7 или более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="df916-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="df916-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="df916-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="df916-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="df916-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="df916-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="df916-108">What you will do</span></span>
<span data-ttu-id="df916-109">Загрузите средства разработки hello и hello программное обеспечение для hello первый образец приложения для вашей Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="df916-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="df916-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="df916-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="df916-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="df916-111">What you will learn</span></span>
<span data-ttu-id="df916-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="df916-112">In this article, you will learn:</span></span>

* <span data-ttu-id="df916-113">Как tooinstall Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="df916-113">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="df916-114">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="df916-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="df916-115">Пример приложения Hello для данной статьи хранится на Git.</span><span class="sxs-lookup"><span data-stu-id="df916-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="df916-116">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="df916-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="df916-117">Как toouse NPM tooinstall дополнительных Node.js средства разработки.</span><span class="sxs-lookup"><span data-stu-id="df916-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="df916-118">Минимальная требуемая версия Hello Node.js — 4,5 LTS.</span><span class="sxs-lookup"><span data-stu-id="df916-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="df916-119">[NPM](https://www.npmjs.com) является одним из hello диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="df916-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="df916-120">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="df916-120">What you need</span></span>
<span data-ttu-id="df916-121">toocomplete этой операции вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="df916-121">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="df916-122">Toodownload подключения Internet hello средства разработки и hello программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="df916-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="df916-123">Компьютер под управлением Ubuntu 16.04 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="df916-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="df916-124">Установка Git, Node.js и NPM</span><span class="sxs-lookup"><span data-stu-id="df916-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="df916-125">Используйте сочетание клавиш hello `Ctrl + Alt + T` tooopen hello терминалов и выполнения следующих команд:</span><span class="sxs-lookup"><span data-stu-id="df916-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="df916-126">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="df916-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="df916-127">Используйте [gulp.js](http://gulpjs.com) tooautomate развертывания hello tooEdison приложения образец hello.</span><span class="sxs-lookup"><span data-stu-id="df916-127">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="df916-128">Установить `gulp` , выполнив следующую команду в терминале hello hello:</span><span class="sxs-lookup"><span data-stu-id="df916-128">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="df916-129">Если возникают проблемы с установкой Node.js и эти дополнительные средства разработки на Ubuntu разделе hello [руководство по устранению неполадок] [ troubleshooting] для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="df916-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="df916-130">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="df916-130">Install Visual Studio Code</span></span>
<span data-ttu-id="df916-131">[Скачайте](https://code.visualstudio.com/docs/setup/linux) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="df916-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="df916-132">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="df916-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="df916-133">Этот редактор используется далее в коде образец hello учебника tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="df916-133">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="df916-134">Сводка</span><span class="sxs-lookup"><span data-stu-id="df916-134">Summary</span></span>
<span data-ttu-id="df916-135">Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="df916-135">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="df916-136">Hello следующей задачей является toocreate, развернуть и запустить пример приложения hello на Edison.</span><span class="sxs-lookup"><span data-stu-id="df916-136">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df916-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df916-137">Next steps</span></span>
<span data-ttu-id="df916-138">[Создание и развертывание образца приложения hello мерцания][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="df916-138">[Create and deploy hello blink sample application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
