---
title: "Connect Raspberry PI (C) tooAzure IoT — занятия 1: средства (Windows) | Документы Microsoft"
description: "Загрузите и установите необходимые средства hello и программное обеспечение для hello первый образец приложения для платформы на Windows 7 и более поздних версиях."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git в Windows, установка Node.js в Windows, установка npm в Windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: bd765ddd-65b7-4241-a391-dc77cb3af1c0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 70ae6d15f9d6af116ff065a79a30d99afc67bffd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="41486-104">Получить средства hello (Windows 7 или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="41486-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="41486-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="41486-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="41486-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="41486-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="41486-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="41486-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="41486-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="41486-108">What you will do</span></span>
<span data-ttu-id="41486-109">Загрузите средства разработки hello и hello программное обеспечение для первый пример приложения hello для Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="41486-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="41486-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="41486-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="41486-111">Хотя язык основная логика hello hello C, Node.js tools используются в устройствах toodiscover занятиях hello и постройте и разверните образцы приложений.</span><span class="sxs-lookup"><span data-stu-id="41486-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="41486-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="41486-112">What you will learn</span></span>
<span data-ttu-id="41486-113">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="41486-113">In this article, you will learn:</span></span>

* <span data-ttu-id="41486-114">Как tooinstall Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="41486-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="41486-115">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="41486-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="41486-116">Пример приложения Hello для данной статьи хранится на Git.</span><span class="sxs-lookup"><span data-stu-id="41486-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="41486-117">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="41486-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="41486-118">Как toouse NPM tooinstall дополнительных Node.js средства разработки.</span><span class="sxs-lookup"><span data-stu-id="41486-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="41486-119">Hello минимальное требование к версии Node.js — 4,5 LTS.</span><span class="sxs-lookup"><span data-stu-id="41486-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="41486-120">[NPM](https://www.npmjs.com) является одним из hello диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="41486-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="41486-121">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="41486-121">What you need</span></span>

<span data-ttu-id="41486-122">toocomplete этой операции вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="41486-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="41486-123">Toodownload подключения Internet hello средства разработки и hello программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="41486-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="41486-124">Компьютер под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="41486-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="41486-125">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="41486-125">Install Git and Node.js</span></span>

<span data-ttu-id="41486-126">Щелкните ссылки hello ниже toodownload и установите Git и LTS Node.js для Windows.</span><span class="sxs-lookup"><span data-stu-id="41486-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="41486-127">Скачать Git для Windows</span><span class="sxs-lookup"><span data-stu-id="41486-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="41486-128">Скачать Node.js LTS для Windows</span><span class="sxs-lookup"><span data-stu-id="41486-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="41486-129">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="41486-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="41486-130">Используйте [gulp.js](http://gulpjs.com) tooautomate развертывания hello tooPi приложения образец hello.</span><span class="sxs-lookup"><span data-stu-id="41486-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="41486-131">Используйте hello [устройство обнаружения cli](https://github.com/Azure/device-discovery-cli) tooretrieve сети сведения об устройствах IoT.</span><span class="sxs-lookup"><span data-stu-id="41486-131">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="41486-132">Запустите командную строку от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="41486-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="41486-133">Установка `gulp` и `device-discovery-cli` , выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="41486-133">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="41486-134">Если возникают проблемы с установкой Node.js и следующим дополнительным средствам разработки Node.js на компьютере, см. раздел hello [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md) для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="41486-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="41486-135">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="41486-135">Install Visual Studio Code</span></span>

<span data-ttu-id="41486-136">[Скачайте](https://code.visualstudio.com/docs/setup/windows) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="41486-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="41486-137">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="41486-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="41486-138">Этот редактор используется далее в коде образец hello учебника tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="41486-138">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="41486-139">Сводка</span><span class="sxs-lookup"><span data-stu-id="41486-139">Summary</span></span>

<span data-ttu-id="41486-140">Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="41486-140">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="41486-141">Следующая задача Hello-toocreate, развернуть и запустить пример приложения hello на Pi.</span><span class="sxs-lookup"><span data-stu-id="41486-141">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41486-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41486-142">Next steps</span></span>

[<span data-ttu-id="41486-143">Создание и развертывание приложения hello мерцания</span><span class="sxs-lookup"><span data-stu-id="41486-143">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
