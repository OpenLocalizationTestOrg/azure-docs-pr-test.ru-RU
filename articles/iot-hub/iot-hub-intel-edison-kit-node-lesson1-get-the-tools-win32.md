---
title: "Подключение Edison Intel (узел) tooAzure IoT — занятия 1: средства (Windows) | Документы Microsoft"
description: "Загрузите и установите необходимые средства hello и программное обеспечение для первый пример приложения hello для Edison в Windows 7 и более поздних версиях."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "инструменты для разработки Arduino, разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git в Windows, установка Node.js в Windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 933cc585d1b8b0236d76452f5c449ae9f2f3987b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="2ebe1-104">Получить средства hello (Windows 7 или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="2ebe1-104">Get hello tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2ebe1-105">[Windows 7 или более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="2ebe1-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="2ebe1-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="2ebe1-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="2ebe1-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="2ebe1-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2ebe1-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="2ebe1-108">What you will do</span></span>
<span data-ttu-id="2ebe1-109">Загрузите средства разработки hello и hello программное обеспечение для первый пример приложения hello для Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-109">Download hello development tools and hello software for hello first sample application for Intel Edison.</span></span> <span data-ttu-id="2ebe1-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2ebe1-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2ebe1-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="2ebe1-111">What you will learn</span></span>
<span data-ttu-id="2ebe1-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="2ebe1-112">In this article, you will learn:</span></span>

* <span data-ttu-id="2ebe1-113">Как tooinstall Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="2ebe1-114">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="2ebe1-115">Пример приложения Hello для данной статьи хранится на Git.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="2ebe1-116">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="2ebe1-117">Как toouse NPM tooinstall дополнительных Node.js средства разработки.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="2ebe1-118">Hello минимальное требование к версии Node.js — 4,5 LTS.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="2ebe1-119">[NPM](https://www.npmjs.com) является одним из hello диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2ebe1-120">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="2ebe1-120">What you need</span></span>

<span data-ttu-id="2ebe1-121">toocomplete этой операции вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="2ebe1-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="2ebe1-122">Toodownload подключения Internet hello средства разработки и hello программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="2ebe1-123">Компьютер под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="2ebe1-124">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="2ebe1-124">Install Git and Node.js</span></span>

<span data-ttu-id="2ebe1-125">Щелкните ссылки hello ниже toodownload и установите Git и LTS Node.js для Windows.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-125">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="2ebe1-126">Скачать Git для Windows</span><span class="sxs-lookup"><span data-stu-id="2ebe1-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="2ebe1-127">Скачать Node.js LTS для Windows</span><span class="sxs-lookup"><span data-stu-id="2ebe1-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="2ebe1-128">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="2ebe1-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="2ebe1-129">Используйте [gulp.js](http://gulpjs.com) tooautomate развертывания hello tooEdison приложения образец hello.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="2ebe1-130">Запустите командную строку от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="2ebe1-131">Установить `gulp` , выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="2ebe1-131">Install `gulp` by running hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="2ebe1-132">Если возникают проблемы с установкой Node.js и следующим дополнительным средствам разработки Node.js на компьютере, см. раздел hello [руководство по устранению неполадок] [ troubleshooting] для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="2ebe1-133">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2ebe1-133">Install Visual Studio Code</span></span>

<span data-ttu-id="2ebe1-134">[Скачайте](https://code.visualstudio.com/docs/setup/windows) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="2ebe1-135">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="2ebe1-136">Этот редактор используется далее в коде образец hello учебника tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-136">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="2ebe1-137">Сводка</span><span class="sxs-lookup"><span data-stu-id="2ebe1-137">Summary</span></span>

<span data-ttu-id="2ebe1-138">Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-138">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="2ebe1-139">Hello следующей задачей является toocreate, развернуть и запустить пример приложения hello на Edison.</span><span class="sxs-lookup"><span data-stu-id="2ebe1-139">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ebe1-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2ebe1-140">Next steps</span></span>

<span data-ttu-id="2ebe1-141">[Создание и развертывание приложения hello мерцания][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="2ebe1-141">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
