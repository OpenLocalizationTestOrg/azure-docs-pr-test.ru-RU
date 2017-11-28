---
title: "Подключение Arduino к Интернету вещей Azure. Урок 1. Получение инструментов (Ubuntu) | Документация Майкрософт"
description: "Скачайте и установите необходимые инструменты и программное обеспечение для работы с первым примером приложения на Adafruit Feather M0 WiFi под управлением Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "инструменты для разработки Arduino, разработка для Интернета вещей, программное обеспечение Интернета вещей, ПО Интернета вещей, установка git в Ubuntu, установка Node.js в Ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 7572f191-420d-41f0-923b-7ea86c0bfa73
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 90b1c12659c33517142e2048d8f5f629f6d6b4c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="dc29b-104">Получение инструментов (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="dc29b-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="dc29b-105">[Windows 7 или более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="dc29b-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="dc29b-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="dc29b-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="dc29b-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="dc29b-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="dc29b-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="dc29b-108">What you will do</span></span>

<span data-ttu-id="dc29b-109">Скачайте инструменты для разработки и программное обеспечение для работы с первым примером приложения на плате Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="dc29b-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="dc29b-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="dc29b-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="dc29b-111">Хотя Arduino является языком программирования основного приложения логики, в уроках используются инструменты Node.js, позволяющие ознакомиться со списком устройств, а также выполнить сборку и развертывание примеров приложений.</span><span class="sxs-lookup"><span data-stu-id="dc29b-111">Although the programming language of the main logic is Arduino, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="dc29b-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="dc29b-112">What you will learn</span></span>
<span data-ttu-id="dc29b-113">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="dc29b-113">In this article, you will learn:</span></span>

* <span data-ttu-id="dc29b-114">Как установить Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="dc29b-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="dc29b-115">[Git](https://git-scm.com) — это распределенная система управления версиями с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="dc29b-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="dc29b-116">Пример приложения, используемый в этой статье, хранится в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="dc29b-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="dc29b-117">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="dc29b-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="dc29b-118">Как использовать NPM, чтобы установить дополнительные средства разработки для Node.js.</span><span class="sxs-lookup"><span data-stu-id="dc29b-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="dc29b-119">Минимальная требуемая версия Node.js — 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="dc29b-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="dc29b-120">[NPM](https://www.npmjs.com) — это один из диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="dc29b-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="dc29b-121">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="dc29b-121">What you need</span></span>
<span data-ttu-id="dc29b-122">Для выполнения этой операции требуется:</span><span class="sxs-lookup"><span data-stu-id="dc29b-122">To complete this operation, you will need:</span></span>
* <span data-ttu-id="dc29b-123">Подключение к Интернету для скачивания средств разработки и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="dc29b-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="dc29b-124">Компьютер под управлением Ubuntu 16.04 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="dc29b-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="dc29b-125">Установка Git, Node.js и NPM</span><span class="sxs-lookup"><span data-stu-id="dc29b-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="dc29b-126">Сочетанием клавиш `Ctrl + Alt + T` откройте окно терминала и выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="dc29b-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="dc29b-127">Установка дополнительных средств разработки для Node.js</span><span class="sxs-lookup"><span data-stu-id="dc29b-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="dc29b-128">Используйте [gulp.js](http://gulpjs.com) для автоматизации развертывания примера приложения на плате Arduino.</span><span class="sxs-lookup"><span data-stu-id="dc29b-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span></span>

<span data-ttu-id="dc29b-129">Установите `gulp` и `device-discovery-cli`, выполнив следующую команду в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="dc29b-129">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="dc29b-130">Если у вас возникли проблемы с установкой Node.js и этих дополнительных инструментов для разработки на компьютер под управлением Ubuntu, способы решения распространенных проблем см. [руководство по устранению неполадок][troubleshooting], где приведены способы решения распространенных проблем.</span><span class="sxs-lookup"><span data-stu-id="dc29b-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="dc29b-131">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="dc29b-131">Install Visual Studio Code</span></span>
<span data-ttu-id="dc29b-132">[Скачайте](https://code.visualstudio.com/docs/setup/linux) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dc29b-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="dc29b-133">Visual Studio Code — это легковесный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="dc29b-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="dc29b-134">Вы будете использовать этот редактор позже, чтобы изменить кода примера.</span><span class="sxs-lookup"><span data-stu-id="dc29b-134">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="dc29b-135">Сводка</span><span class="sxs-lookup"><span data-stu-id="dc29b-135">Summary</span></span>
<span data-ttu-id="dc29b-136">Вы установили требуемые средства разработки и программное обеспечение для работы с примером приложения.</span><span class="sxs-lookup"><span data-stu-id="dc29b-136">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="dc29b-137">Следующей задачей является создание, развертывание и запуск примера приложения на плате Arduino.</span><span class="sxs-lookup"><span data-stu-id="dc29b-137">The next task is to create, deploy, and run the sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc29b-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc29b-138">Next steps</span></span>
<span data-ttu-id="dc29b-139">[Создание и развертывание приложения для включения индикатора][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="dc29b-139">[Create and deploy the blink sample application][create-and-deploy-the-blink-sample-application]</span></span>

<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md