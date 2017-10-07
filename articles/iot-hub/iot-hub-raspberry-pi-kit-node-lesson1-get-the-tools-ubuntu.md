---
title: "Подключение Raspberry Pi (узел) tooAzure IoT — занятия 1: средства (Ubuntu) | Документы Microsoft"
description: "Загрузите и установите на Ubuntu hello необходимых средств и программного обеспечения для первого примера приложения hello пи."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git в ubuntu, gulp run, установка node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f566fa0d1faf8b2321707145f675e3d87f0bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="942d6-104">Получить средства hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="942d6-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="942d6-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="942d6-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="942d6-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="942d6-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="942d6-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="942d6-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="942d6-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="942d6-108">What you will do</span></span>
<span data-ttu-id="942d6-109">Загрузите средства разработки hello и hello программное обеспечение для первый пример приложения hello для Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="942d6-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="942d6-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="942d6-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="942d6-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="942d6-111">What you will learn</span></span>
<span data-ttu-id="942d6-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="942d6-112">In this article, you will learn:</span></span>

* <span data-ttu-id="942d6-113">Как tooinstall Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="942d6-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="942d6-114">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="942d6-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="942d6-115">Пример приложения Hello для данной статьи хранится на Git.</span><span class="sxs-lookup"><span data-stu-id="942d6-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="942d6-116">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="942d6-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="942d6-117">Как toouse NPM tooinstall дополнительных Node.js средства разработки.</span><span class="sxs-lookup"><span data-stu-id="942d6-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="942d6-118">Минимальная требуемая версия Hello Node.js — 4,5 LTS.</span><span class="sxs-lookup"><span data-stu-id="942d6-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="942d6-119">[NPM](https://www.npmjs.com) является одним из hello диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="942d6-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="942d6-120">Требования</span><span class="sxs-lookup"><span data-stu-id="942d6-120">What do you need</span></span>
<span data-ttu-id="942d6-121">toocomplete этой операции вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="942d6-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="942d6-122">Toodownload подключения Internet hello средства разработки и hello программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="942d6-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="942d6-123">Компьютер под управлением Ubuntu 16.04 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="942d6-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="942d6-124">Установка Git, Node.js и NPM</span><span class="sxs-lookup"><span data-stu-id="942d6-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="942d6-125">Используйте сочетание клавиш hello `Ctrl + Alt + T` tooopen hello терминалов и выполнения следующих команд:</span><span class="sxs-lookup"><span data-stu-id="942d6-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="942d6-126">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="942d6-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="942d6-127">Вы используете [gulp.js](http://gulpjs.com) tooautomate развертывания hello tooPi приложения образец hello.</span><span class="sxs-lookup"><span data-stu-id="942d6-127">You use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="942d6-128">Можно также использовать hello [устройство обнаружения cli](https://github.com/Azure/device-discovery-cli) tooretrieve сети сведения об устройствах IoT.</span><span class="sxs-lookup"><span data-stu-id="942d6-128">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="942d6-129">Установка `gulp` и `device-discovery-cli` , выполнив следующую команду в терминале hello hello:</span><span class="sxs-lookup"><span data-stu-id="942d6-129">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="942d6-130">Если возникают проблемы с установкой Node.js и эти дополнительные средства разработки на Ubuntu разделе hello [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md) для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="942d6-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="942d6-131">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="942d6-131">Install Visual Studio Code</span></span>
<span data-ttu-id="942d6-132">[Скачайте](https://code.visualstudio.com/docs/setup/linux) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="942d6-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="942d6-133">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="942d6-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="942d6-134">Этот редактор используется далее в коде образец hello учебника tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="942d6-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="942d6-135">Сводка</span><span class="sxs-lookup"><span data-stu-id="942d6-135">Summary</span></span>
<span data-ttu-id="942d6-136">Установив hello необходимые средства разработки и программное обеспечение для первый пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="942d6-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="942d6-137">Следующая задача Hello-toocreate, развернуть и запустить пример приложения hello на Pi.</span><span class="sxs-lookup"><span data-stu-id="942d6-137">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="942d6-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="942d6-138">Next steps</span></span>
[<span data-ttu-id="942d6-139">Создание и развертывание образца приложения hello мерцания</span><span class="sxs-lookup"><span data-stu-id="942d6-139">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

