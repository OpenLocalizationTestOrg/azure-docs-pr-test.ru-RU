---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Урок 1. Получение инструментов (Ubuntu) | Документация Майкрософт"
description: "Скачайте и установите необходимые инструменты и программное обеспечение для работы с примером приложения на устройстве Pi под управлением Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git в ubuntu, gulp run, установка node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 28ebba82e90d91470518cd830c96e6da39d8b9b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="acfa8-104">Получение инструментов (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="acfa8-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="acfa8-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="acfa8-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="acfa8-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="acfa8-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="acfa8-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="acfa8-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="acfa8-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="acfa8-108">What you will do</span></span>
<span data-ttu-id="acfa8-109">Скачаете средства разработки и программное обеспечение для работы с примером приложения на компьютере Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="acfa8-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="acfa8-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="acfa8-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="acfa8-111">Хотя С является языком программирования основного приложения логики, в уроках используются инструменты Node.js, позволяющие ознакомиться со списком устройств, а также выполнить сборку и развертывание примеров приложений.</span><span class="sxs-lookup"><span data-stu-id="acfa8-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="acfa8-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="acfa8-112">What you will learn</span></span>
<span data-ttu-id="acfa8-113">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="acfa8-113">In this article, you will learn:</span></span>

* <span data-ttu-id="acfa8-114">Как установить Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="acfa8-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="acfa8-115">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="acfa8-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="acfa8-116">Пример приложения, используемый в этой статье, хранится в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="acfa8-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="acfa8-117">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="acfa8-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="acfa8-118">Как использовать NPM, чтобы установить дополнительные средства разработки для Node.js.</span><span class="sxs-lookup"><span data-stu-id="acfa8-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="acfa8-119">Минимальная требуемая версия Node.js — 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="acfa8-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="acfa8-120">[NPM](https://www.npmjs.com) — это один из диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="acfa8-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="acfa8-121">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="acfa8-121">What you need</span></span>
<span data-ttu-id="acfa8-122">Для выполнения этой операции требуется:</span><span class="sxs-lookup"><span data-stu-id="acfa8-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="acfa8-123">Подключение к Интернету для скачивания средств разработки и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="acfa8-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="acfa8-124">Компьютер под управлением Ubuntu 16.04 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="acfa8-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="acfa8-125">Установка Git, Node.js и NPM</span><span class="sxs-lookup"><span data-stu-id="acfa8-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="acfa8-126">Сочетанием клавиш `Ctrl + Alt + T` откройте окно терминала и выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="acfa8-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="acfa8-127">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="acfa8-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="acfa8-128">Используйте [gulp.js](http://gulpjs.com) для автоматизации развертывания примера приложения на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="acfa8-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="acfa8-129">Используйте средство [device-discovery-cli](https://github.com/Azure/device-discovery-cli), чтобы получить сведения о сети для устройств Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="acfa8-129">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="acfa8-130">Установите `gulp` и `device-discovery-cli`, выполнив следующую команду в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="acfa8-130">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="acfa8-131">При возникновении проблем с установкой Node.js и этих дополнительных средств разработки на компьютер под управлением Ubuntu см. [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md), где приведены способы решения распространенных проблем.</span><span class="sxs-lookup"><span data-stu-id="acfa8-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="acfa8-132">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="acfa8-132">Install Visual Studio Code</span></span>
<span data-ttu-id="acfa8-133">[Скачайте](https://code.visualstudio.com/docs/setup/linux) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="acfa8-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="acfa8-134">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="acfa8-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="acfa8-135">Вы будете использовать этот редактор позже, чтобы изменить кода примера.</span><span class="sxs-lookup"><span data-stu-id="acfa8-135">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="acfa8-136">Сводка</span><span class="sxs-lookup"><span data-stu-id="acfa8-136">Summary</span></span>
<span data-ttu-id="acfa8-137">Вы установили требуемые средства разработки и программное обеспечение для работы с примером приложения.</span><span class="sxs-lookup"><span data-stu-id="acfa8-137">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="acfa8-138">Следующей задачей является создание, развертывание и запуск примера приложения на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="acfa8-138">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acfa8-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="acfa8-139">Next steps</span></span>
[<span data-ttu-id="acfa8-140">Создание и развертывание приложения для включения индикатора</span><span class="sxs-lookup"><span data-stu-id="acfa8-140">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

