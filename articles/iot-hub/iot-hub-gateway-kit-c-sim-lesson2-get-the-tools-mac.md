---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 2. Получение инструментов (macOS) | Документация Майкрософт"
description: "Установка средств на компьютере Mac, создать центр IoT и зарегистрировать устройство в центре IoT hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, облачные службы Интернета вещей, ПО Интернета вещей, Azure CLI, установка Python на компьютере Mac, установка git на компьютере Mac, запуск инструмента Gulp, установка Node.js на компьютере Mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 391d60f3cbb209698cae53098efed360ac0f5fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a><span data-ttu-id="30d2d-104">Получить средства hello (macOS)</span><span class="sxs-lookup"><span data-stu-id="30d2d-104">Get hello tools (macOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30d2d-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="30d2d-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="30d2d-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="30d2d-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="30d2d-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="30d2d-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="30d2d-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="30d2d-108">What you will do</span></span>

- <span data-ttu-id="30d2d-109">Установка Git, Node.js, Gulp и Python.</span><span class="sxs-lookup"><span data-stu-id="30d2d-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="30d2d-110">Установите hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="30d2d-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="30d2d-111">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="30d2d-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="30d2d-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="30d2d-112">What you will learn</span></span>

<span data-ttu-id="30d2d-113">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="30d2d-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="30d2d-114">Как tooinstall [Git](https://git-scm.com/) и [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="30d2d-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="30d2d-115">Git — это распределенная система управления версиями с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="30d2d-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="30d2d-116">Пример приложения Hello на этом занятии будет храниться на Git.</span><span class="sxs-lookup"><span data-stu-id="30d2d-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="30d2d-117">Node.js — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="30d2d-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="30d2d-118">Как toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="30d2d-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="30d2d-119">Минимальная требуемая версия Hello Node.js — 4,5 LTS.</span><span class="sxs-lookup"><span data-stu-id="30d2d-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="30d2d-120">NPM является одним из диспетчеров пакетов приветствия для Node.js.</span><span class="sxs-lookup"><span data-stu-id="30d2d-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="30d2d-121">Как tooinstall кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30d2d-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="30d2d-122">Visual Studio Code — это упрощенный кроссплатформенный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="30d2d-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="30d2d-123">Он поддерживает возможности отладки, выделения синтаксиса, интеллектуального автозавершения кода, встроенные элементы управления Git, фрагменты кода, а также возможности рефакторинга кода.</span><span class="sxs-lookup"><span data-stu-id="30d2d-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="30d2d-124">Как tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="30d2d-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="30d2d-125">Python — это широко используемый высокоуровневый интерпретируемый и динамический язык программирования общего назначения.</span><span class="sxs-lookup"><span data-stu-id="30d2d-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="30d2d-126">Как tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="30d2d-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="30d2d-127">Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure.</span><span class="sxs-lookup"><span data-stu-id="30d2d-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="30d2d-128">Работа непосредственно из tooprovision командной строки и управления ресурсами.</span><span class="sxs-lookup"><span data-stu-id="30d2d-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="30d2d-129">Как toouse hello Azure CLI toocreate центр IoT.</span><span class="sxs-lookup"><span data-stu-id="30d2d-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="30d2d-130">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="30d2d-130">What you need</span></span>

- <span data-ttu-id="30d2d-131">Toodownload подключения Internet hello средств и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="30d2d-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="30d2d-132">Компьютер Mac под управлением OS X Yosemite (10.10) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="30d2d-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="30d2d-133">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="30d2d-133">Install Git and Node.js</span></span>

<span data-ttu-id="30d2d-134">tooinstall Git и Node.js, используйте программу управления пакетов Homebrew hello, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="30d2d-134">tooinstall Git and Node.js, use hello Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="30d2d-135">[Скачайте](http://brew.sh/) и установите Homebrew.</span><span class="sxs-lookup"><span data-stu-id="30d2d-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="30d2d-136">Если Homebrew уже установлен, воспользуйтесь toostep 2.</span><span class="sxs-lookup"><span data-stu-id="30d2d-136">If you’ve already installed Homebrew, go toostep 2.</span></span>
   1. <span data-ttu-id="30d2d-137">Нажмите клавишу `Cmd + Space` и введите `Terminal` tooopen терминала.</span><span class="sxs-lookup"><span data-stu-id="30d2d-137">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="30d2d-138">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="30d2d-138">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="30d2d-139">Установите Git и Node.js, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="30d2d-139">Install Git and Node.js by running hello following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="30d2d-140">Установка инструментов разработки Node.js</span><span class="sxs-lookup"><span data-stu-id="30d2d-140">Install Node.js development tools</span></span>

<span data-ttu-id="30d2d-141">Вы используете [gulp.js](http://gulpjs.com/) tooautomate развертывания и выполнения скриптов.</span><span class="sxs-lookup"><span data-stu-id="30d2d-141">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="30d2d-142">gulp tooinstall, запустите следующую команду в терминале hello hello:</span><span class="sxs-lookup"><span data-stu-id="30d2d-142">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="30d2d-143">При возникновении проблем с установкой hello. в разделе hello [руководство по устранению неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md) для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="30d2d-143">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="30d2d-144">Узел, NPM и Gulp являются необходимые toorun сценариев автоматизации, разработанные в Node.js.</span><span class="sxs-lookup"><span data-stu-id="30d2d-144">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="30d2d-145">Установка Python</span><span class="sxs-lookup"><span data-stu-id="30d2d-145">Install Python</span></span>

<span data-ttu-id="30d2d-146">Несмотря на то что Mac OS X поставляется с версией Python 2.7, мы рекомендуем установить Python через Homebrew.</span><span class="sxs-lookup"><span data-stu-id="30d2d-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="30d2d-147">Ознакомьтесь со статьей [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/) (Установка Python на Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="30d2d-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="30d2d-148">Установите Python и pip, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="30d2d-148">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="30d2d-149">Установка hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="30d2d-149">Install hello Azure CLI</span></span>

<span data-ttu-id="30d2d-150">tooinstall hello Azure CLI, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="30d2d-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="30d2d-151">Выполните следующие команды в терминале hello hello.</span><span class="sxs-lookup"><span data-stu-id="30d2d-151">Run hello following commands in hello terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="30d2d-152">Hello установки может потребоваться 5 минут.</span><span class="sxs-lookup"><span data-stu-id="30d2d-152">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="30d2d-153">Проверка установки hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="30d2d-153">Verify hello installation by running hello following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="30d2d-154">Вы увидите следующее hello выходных данных, если hello успешно установлен.</span><span class="sxs-lookup"><span data-stu-id="30d2d-154">You should see hello following output if hello installation is successful.</span></span>

   ![Проверка установки Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="30d2d-156">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="30d2d-156">Install Visual Studio Code</span></span>

<span data-ttu-id="30d2d-157">Использование кода Visual Studio в файлах конфигурации учебника tooedit hello в более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="30d2d-157">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="30d2d-158">[Скачайте](https://code.visualstudio.com/docs/setup/osx) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="30d2d-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="30d2d-159">Сводка</span><span class="sxs-lookup"><span data-stu-id="30d2d-159">Summary</span></span>

<span data-ttu-id="30d2d-160">Вы установили все необходимые hello средств и программного обеспечения на компьютере Mac.</span><span class="sxs-lookup"><span data-stu-id="30d2d-160">You’ve installed all hello required tools and software on your Mac computer.</span></span> <span data-ttu-id="30d2d-161">Следующая задача является toouse hello Azure CLI toocreate центр IoT и зарегистрировать устройство в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="30d2d-161">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30d2d-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="30d2d-162">Next steps</span></span>
[<span data-ttu-id="30d2d-163">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="30d2d-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
