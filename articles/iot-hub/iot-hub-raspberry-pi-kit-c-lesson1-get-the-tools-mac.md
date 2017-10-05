---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Урок 1. Получение инструментов (macOS) | Документация Майкрософт"
description: "Скачайте и установите необходимые инструменты и программное обеспечение для работы с примером приложения на устройстве Pi под управлением macOS."
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
ms.openlocfilehash: 64db77040ef3482f213bd622320fdb5df243fa93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="f031c-104">Получение инструментов (MacOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="f031c-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f031c-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="f031c-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="f031c-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f031c-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="f031c-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="f031c-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="f031c-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="f031c-108">What you will do</span></span>
<span data-ttu-id="f031c-109">Скачаете средства разработки и программное обеспечение для работы с примером приложения на компьютере Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="f031c-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="f031c-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f031c-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f031c-111">Хотя С является языком программирования основного приложения логики, в уроках используются инструменты Node.js, позволяющие ознакомиться со списком устройств, а также выполнить сборку и развертывание примеров приложений.</span><span class="sxs-lookup"><span data-stu-id="f031c-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f031c-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="f031c-112">What you will learn</span></span>
<span data-ttu-id="f031c-113">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="f031c-113">In this article, you will learn:</span></span>

* <span data-ttu-id="f031c-114">Как установить Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="f031c-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="f031c-115">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="f031c-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="f031c-116">Пример приложения, используемый в этой статье, хранится в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="f031c-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="f031c-117">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="f031c-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="f031c-118">Как использовать NPM, чтобы установить дополнительные средства разработки для Node.js.</span><span class="sxs-lookup"><span data-stu-id="f031c-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="f031c-119">Минимальная требуемая версия Node.js — 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="f031c-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="f031c-120">[NPM](https://www.npmjs.com) — это один из диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="f031c-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f031c-121">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="f031c-121">What you need</span></span>
<span data-ttu-id="f031c-122">Для выполнения этой операции требуется:</span><span class="sxs-lookup"><span data-stu-id="f031c-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="f031c-123">Подключение к Интернету для скачивания средств разработки и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="f031c-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="f031c-124">Компьютер Mac под управлением Yosemite macOS (10.10) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f031c-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="f031c-125">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="f031c-125">Install Git and Node.js</span></span>
<span data-ttu-id="f031c-126">Чтобы установить Git и Node.js, используйте пакет управления [Homebrew](http://brew.sh), выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f031c-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="f031c-127">Установите Homebrew.</span><span class="sxs-lookup"><span data-stu-id="f031c-127">Install Homebrew.</span></span> <span data-ttu-id="f031c-128">Если вы уже установили Homebrew, перейдите к шагу 2.</span><span class="sxs-lookup"><span data-stu-id="f031c-128">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="f031c-129">Нажмите сочетание клавиш `Cmd + Space` и введите `Terminal`, чтобы открыть окно терминала.</span><span class="sxs-lookup"><span data-stu-id="f031c-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="f031c-130">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f031c-130">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="f031c-131">Установите Git и Node.js, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f031c-131">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="f031c-132">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="f031c-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="f031c-133">Используйте [gulp.js](http://gulpjs.com) для автоматизации развертывания примера приложения на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="f031c-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Pi.</span></span> <span data-ttu-id="f031c-134">Используйте средство [device-discovery-cli](https://github.com/Azure/device-discovery-cli), чтобы получить сведения о сети для устройств Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f031c-134">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="f031c-135">Установите `gulp` и `device-discovery-cli`, выполнив следующую команду в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="f031c-135">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="f031c-136">При возникновении проблем с установкой Node.js и этими дополнительными средствами разработки на компьютер под управлением macOS, см. [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md). Там приведены способы решения распространенных проблем.</span><span class="sxs-lookup"><span data-stu-id="f031c-136">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="f031c-137">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f031c-137">Install Visual Studio Code</span></span>
<span data-ttu-id="f031c-138">[Скачайте](https://code.visualstudio.com/docs/setup/osx) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f031c-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="f031c-139">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="f031c-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="f031c-140">Вы будете использовать этот редактор позже, чтобы изменить кода примера.</span><span class="sxs-lookup"><span data-stu-id="f031c-140">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="f031c-141">Сводка</span><span class="sxs-lookup"><span data-stu-id="f031c-141">Summary</span></span>
<span data-ttu-id="f031c-142">Вы установили требуемые средства разработки и программное обеспечение для работы с примером приложения.</span><span class="sxs-lookup"><span data-stu-id="f031c-142">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="f031c-143">Следующей задачей является создание, развертывание и запуск примера приложения на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="f031c-143">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f031c-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f031c-144">Next steps</span></span>
[<span data-ttu-id="f031c-145">Создание и развертывание приложения для включения индикатора</span><span class="sxs-lookup"><span data-stu-id="f031c-145">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

