---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 2. Получение инструментов (macOS) | Документация Майкрософт"
description: "Установите инструменты на компьютере Mac, создайте Центр Интернета вещей и зарегистрируйте устройство в нем."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, облачные службы Интернета вещей, ПО Интернета вещей, Azure CLI, установка Python на компьютере Mac, установка git на компьютере Mac, запуск инструмента Gulp, установка Node.js на компьютере Mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 07bc5f2cf6542273c334371b77520c674c5d2f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a><span data-ttu-id="6da70-104">Получение инструментов (macOS)</span><span class="sxs-lookup"><span data-stu-id="6da70-104">Get the tools (MacOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6da70-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="6da70-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="6da70-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6da70-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="6da70-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="6da70-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="6da70-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="6da70-108">What you will do</span></span>

- <span data-ttu-id="6da70-109">Установка Git, Node.js, Gulp и Python.</span><span class="sxs-lookup"><span data-stu-id="6da70-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="6da70-110">Установите интерфейс командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="6da70-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="6da70-111">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="6da70-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6da70-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="6da70-112">What you will learn</span></span>

<span data-ttu-id="6da70-113">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="6da70-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="6da70-114">Как установить [Git](https://git-scm.com/) и [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="6da70-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="6da70-115">Git — это распределенная система управления версиями с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="6da70-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="6da70-116">Пример приложения, используемый в этом руководстве, хранится в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="6da70-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="6da70-117">Node.js — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="6da70-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="6da70-118">Как установить инструменты разработки для Node.js. с помощью [NPM](https://www.npmjs.com/).</span><span class="sxs-lookup"><span data-stu-id="6da70-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="6da70-119">Минимальная требуемая версия Node.js — 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="6da70-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="6da70-120">NPM — это один из диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="6da70-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="6da70-121">Как установить Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6da70-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="6da70-122">Visual Studio Code — это упрощенный кроссплатформенный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="6da70-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="6da70-123">Он поддерживает возможности отладки, выделения синтаксиса, интеллектуального автозавершения кода, встроенные элементы управления Git, фрагменты кода, а также возможности рефакторинга кода.</span><span class="sxs-lookup"><span data-stu-id="6da70-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="6da70-124">Как установить Python.</span><span class="sxs-lookup"><span data-stu-id="6da70-124">How to install Python.</span></span>
  - <span data-ttu-id="6da70-125">Python — это широко используемый высокоуровневый интерпретируемый и динамический язык программирования общего назначения.</span><span class="sxs-lookup"><span data-stu-id="6da70-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="6da70-126">Как установить интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="6da70-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="6da70-127">Azure CLI — это кроссплатформенное средство для работы с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="6da70-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="6da70-128">С его помощью можно подготавливать ресурсы для Azure и управлять ими непосредственно в командной строке.</span><span class="sxs-lookup"><span data-stu-id="6da70-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="6da70-129">Как создать Центр Интернета вещей с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6da70-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6da70-130">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="6da70-130">What you need</span></span>

- <span data-ttu-id="6da70-131">Подключение к Интернету для скачивания инструментов и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="6da70-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="6da70-132">Компьютер Mac под управлением OS X Yosemite (10.10) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6da70-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="6da70-133">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="6da70-133">Install Git and Node.js</span></span>

<span data-ttu-id="6da70-134">Чтобы установить Git и Node.js, используйте служебную программу управления пакетами Homebrew и сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="6da70-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="6da70-135">[Скачайте](http://brew.sh/) и установите Homebrew.</span><span class="sxs-lookup"><span data-stu-id="6da70-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="6da70-136">Если вы уже установили Homebrew, перейдите к шагу 2.</span><span class="sxs-lookup"><span data-stu-id="6da70-136">If you’ve already installed Homebrew, go to step 2.</span></span>
   1. <span data-ttu-id="6da70-137">Нажмите сочетание клавиш `Cmd + Space` и введите `Terminal`, чтобы открыть окно терминала.</span><span class="sxs-lookup"><span data-stu-id="6da70-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="6da70-138">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6da70-138">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="6da70-139">Установите Git и Node.js, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6da70-139">Install Git and Node.js by running the following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="6da70-140">Установка инструментов разработки Node.js</span><span class="sxs-lookup"><span data-stu-id="6da70-140">Install Node.js development tools</span></span>

<span data-ttu-id="6da70-141">Используйте [gulp.js](http://gulpjs.com/) для автоматизации развертывания и выполнения сценариев.</span><span class="sxs-lookup"><span data-stu-id="6da70-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="6da70-142">Чтобы установить Gulp, выполните следующую команду в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="6da70-142">To install gulp, run the following command in the terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="6da70-143">Если при установке возникают проблемы, способы их устранения см. в [этом руководстве по устранению неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="6da70-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="6da70-144">Для выполнения сценариев автоматизации, разработанных в Node.js, требуются Node, NPM и Gulp.</span><span class="sxs-lookup"><span data-stu-id="6da70-144">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="6da70-145">Установка Python</span><span class="sxs-lookup"><span data-stu-id="6da70-145">Install Python</span></span>

<span data-ttu-id="6da70-146">Несмотря на то что Mac OS X поставляется с версией Python 2.7, мы рекомендуем установить Python через Homebrew.</span><span class="sxs-lookup"><span data-stu-id="6da70-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="6da70-147">Ознакомьтесь со статьей [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/) (Установка Python на Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="6da70-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="6da70-148">Установите Python и pip, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6da70-148">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="6da70-149">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6da70-149">Install the Azure CLI</span></span>

<span data-ttu-id="6da70-150">Для установки Azure CLI выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6da70-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="6da70-151">Выполните следующие команды в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="6da70-151">Run the following commands in the terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="6da70-152">Установка может занять 5 минут.</span><span class="sxs-lookup"><span data-stu-id="6da70-152">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="6da70-153">Выполните следующую команду, чтобы проверить установку:</span><span class="sxs-lookup"><span data-stu-id="6da70-153">Verify the installation by running the following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="6da70-154">Если установка прошла успешно, отобразятся следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="6da70-154">You should see the following output if the installation is successful.</span></span>

   ![Проверка установки Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="6da70-156">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6da70-156">Install Visual Studio Code</span></span>

<span data-ttu-id="6da70-157">Позже в этом руководстве вы используете Visual Studio Code, чтобы изменить файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6da70-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="6da70-158">[Скачайте](https://code.visualstudio.com/docs/setup/osx) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6da70-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="6da70-159">Сводка</span><span class="sxs-lookup"><span data-stu-id="6da70-159">Summary</span></span>

<span data-ttu-id="6da70-160">Вы установили на компьютере Mac все необходимые инструменты и программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="6da70-160">You’ve installed all the required tools and software on your Mac computer.</span></span> <span data-ttu-id="6da70-161">Следующая задача заключается в создании Центра Интернета вещей и регистрации в нем устройства с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6da70-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6da70-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6da70-162">Next steps</span></span>
[<span data-ttu-id="6da70-163">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="6da70-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
