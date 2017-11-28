---
title: "Подключение Raspberry Pi (Node) к Интернету вещей Azure. Урок 1. Получение инструментов (macOS) | Документация Майкрософт"
description: "Скачайте и установите необходимые инструменты и программное обеспечение для работы с примером приложения на устройстве Pi под управлением macOS."
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
ms.openlocfilehash: 6c2338baa8e88bab4c4be64568220f53178943cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="a08fa-104">Получение инструментов (MacOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="a08fa-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a08fa-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="a08fa-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="a08fa-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="a08fa-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="a08fa-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="a08fa-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="a08fa-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="a08fa-108">What you will do</span></span>
<span data-ttu-id="a08fa-109">Скачаете средства разработки и программное обеспечение для работы с примером приложения на компьютере Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a08fa-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="a08fa-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a08fa-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a08fa-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="a08fa-111">What you will learn</span></span>
<span data-ttu-id="a08fa-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="a08fa-112">In this article, you will learn:</span></span>

* <span data-ttu-id="a08fa-113">Как установить Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="a08fa-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="a08fa-114">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="a08fa-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="a08fa-115">Пример приложения, используемый в этой статье, хранится в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="a08fa-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="a08fa-116">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="a08fa-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="a08fa-117">Как использовать NPM, чтобы установить дополнительные средства разработки для Node.js.</span><span class="sxs-lookup"><span data-stu-id="a08fa-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="a08fa-118">Минимальная требуемая версия Node.js — 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="a08fa-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="a08fa-119">[NPM](https://www.npmjs.com) — это один из диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="a08fa-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a08fa-120">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="a08fa-120">What you need</span></span>
<span data-ttu-id="a08fa-121">Для выполнения этой операции требуется:</span><span class="sxs-lookup"><span data-stu-id="a08fa-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="a08fa-122">Подключение к Интернету для скачивания средств разработки и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="a08fa-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="a08fa-123">Компьютер Mac под управлением Yosemite macOS (10.10) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a08fa-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="a08fa-124">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="a08fa-124">Install Git and Node.js</span></span>
<span data-ttu-id="a08fa-125">Чтобы установить Git и Node.js, используйте пакет управления [Homebrew](http://brew.sh), выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a08fa-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="a08fa-126">Установите Homebrew.</span><span class="sxs-lookup"><span data-stu-id="a08fa-126">Install Homebrew.</span></span> <span data-ttu-id="a08fa-127">Если вы уже установили Homebrew, перейдите к шагу 2.</span><span class="sxs-lookup"><span data-stu-id="a08fa-127">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="a08fa-128">Нажмите сочетание клавиш `Cmd + Space` и введите `Terminal`, чтобы открыть окно терминала.</span><span class="sxs-lookup"><span data-stu-id="a08fa-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="a08fa-129">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a08fa-129">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="a08fa-130">Установите Git и Node.js, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a08fa-130">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="a08fa-131">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="a08fa-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="a08fa-132">Используйте [gulp.js](http://gulpjs.com) для автоматизации развертывания примера приложения на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="a08fa-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="a08fa-133">Используйте средство [device-discovery-cli](https://github.com/Azure/device-discovery-cli), чтобы получить сведения о сети для устройств Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a08fa-133">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="a08fa-134">Установите `gulp` и `device-discovery-cli`, выполнив следующую команду в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="a08fa-134">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="a08fa-135">При возникновении проблем с установкой Node.js и этими дополнительными средствами разработки на компьютер под управлением macOS, см. [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md). Там приведены способы решения распространенных проблем.</span><span class="sxs-lookup"><span data-stu-id="a08fa-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="a08fa-136">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a08fa-136">Install Visual Studio Code</span></span>
<span data-ttu-id="a08fa-137">[Скачайте](https://code.visualstudio.com/docs/setup/osx) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a08fa-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="a08fa-138">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="a08fa-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="a08fa-139">Вы будете использовать этот редактор позже, чтобы изменить кода примера.</span><span class="sxs-lookup"><span data-stu-id="a08fa-139">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="a08fa-140">Сводка</span><span class="sxs-lookup"><span data-stu-id="a08fa-140">Summary</span></span>
<span data-ttu-id="a08fa-141">Вы установили требуемые средства разработки и программное обеспечение для работы с примером приложения.</span><span class="sxs-lookup"><span data-stu-id="a08fa-141">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="a08fa-142">Следующей задачей является создание, развертывание и запуск примера приложения на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="a08fa-142">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a08fa-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a08fa-143">Next steps</span></span>
<span data-ttu-id="a08fa-144">[Create and deploy the blink sample application](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md) (Создание и развертывание примера приложения для включения индикатора)</span><span class="sxs-lookup"><span data-stu-id="a08fa-144">[Create and deploy the blink sample application](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)</span></span>

