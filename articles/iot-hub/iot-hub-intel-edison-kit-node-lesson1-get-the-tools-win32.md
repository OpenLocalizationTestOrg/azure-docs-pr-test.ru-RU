---
title: "Подключение Intel Edison (Node) к Интернету вещей Azure. Урок 1. Получение инструментов (Windows) | Документация Майкрософт"
description: "Скачайте и установите необходимые инструменты и программное обеспечение для работы с примером приложения на устройстве Edison под управлением Windows 7 и более поздних версий."
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
ms.openlocfilehash: 35b7ae24f8616848eaa6affccb96630603b823b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="9e9d1-104">Получение инструментов (Windows 7 или более поздние версии)</span><span class="sxs-lookup"><span data-stu-id="9e9d1-104">Get the tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="9e9d1-105">[Windows 7 или более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="9e9d1-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="9e9d1-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="9e9d1-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="9e9d1-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="9e9d1-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9e9d1-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="9e9d1-108">What you will do</span></span>
<span data-ttu-id="9e9d1-109">Скачайте инструменты для разработки и программное обеспечение для работы с примером приложения на устройстве Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-109">Download the development tools and the software for the first sample application for Intel Edison.</span></span> <span data-ttu-id="9e9d1-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="9e9d1-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9e9d1-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="9e9d1-111">What you will learn</span></span>
<span data-ttu-id="9e9d1-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="9e9d1-112">In this article, you will learn:</span></span>

* <span data-ttu-id="9e9d1-113">Как установить Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="9e9d1-114">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="9e9d1-115">Пример приложения, используемый в этой статье, хранится в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="9e9d1-116">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="9e9d1-117">Как использовать NPM, чтобы установить дополнительные средства разработки для Node.js.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="9e9d1-118">Минимальная требуемая версия Node.js — 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-118">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="9e9d1-119">[NPM](https://www.npmjs.com) — это один из диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9e9d1-120">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="9e9d1-120">What you need</span></span>

<span data-ttu-id="9e9d1-121">Для выполнения этой операции требуется:</span><span class="sxs-lookup"><span data-stu-id="9e9d1-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="9e9d1-122">Подключение к Интернету для скачивания средств разработки и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="9e9d1-123">Компьютер под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="9e9d1-124">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="9e9d1-124">Install Git and Node.js</span></span>

<span data-ttu-id="9e9d1-125">Щелкните ссылки ниже, чтобы скачать и установить Git и LTS Node.js для Windows.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-125">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="9e9d1-126">Скачать Git для Windows</span><span class="sxs-lookup"><span data-stu-id="9e9d1-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="9e9d1-127">Скачать Node.js LTS для Windows</span><span class="sxs-lookup"><span data-stu-id="9e9d1-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="9e9d1-128">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="9e9d1-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="9e9d1-129">Используйте [gulp.js](http://gulpjs.com) для автоматизации развертывания примера приложения на устройстве Edison.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-129">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="9e9d1-130">Запустите командную строку от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="9e9d1-131">Установите `gulp`, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9e9d1-131">Install `gulp` by running the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="9e9d1-132">Если у вас возникли проблемы с установкой Node.js и этих дополнительных инструментов для разработки для Node.js на компьютер, способы решения распространенных проблем см. [руководство по устранению неполадок][troubleshooting]. Там приведены способы решения распространенных проблем.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="9e9d1-133">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9e9d1-133">Install Visual Studio Code</span></span>

<span data-ttu-id="9e9d1-134">[Скачайте](https://code.visualstudio.com/docs/setup/windows) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="9e9d1-135">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="9e9d1-136">Вы будете использовать этот редактор позже, чтобы изменить кода примера.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-136">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="9e9d1-137">Сводка</span><span class="sxs-lookup"><span data-stu-id="9e9d1-137">Summary</span></span>

<span data-ttu-id="9e9d1-138">Вы установили требуемые средства разработки и программное обеспечение для работы с примером приложения.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-138">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="9e9d1-139">Следующей задачей является создание, развертывание и запуск примера приложения на устройстве Edison.</span><span class="sxs-lookup"><span data-stu-id="9e9d1-139">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e9d1-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e9d1-140">Next steps</span></span>

<span data-ttu-id="9e9d1-141">[Создание и развертывание приложения для включения индикатора][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="9e9d1-141">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
