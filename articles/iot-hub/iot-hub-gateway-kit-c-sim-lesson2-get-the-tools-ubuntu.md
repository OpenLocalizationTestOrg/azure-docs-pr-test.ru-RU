---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 2. Получение инструментов (Ubuntu) | Документация Майкрософт"
description: "Установите на главный компьютер под управлением Ubuntu hello средств и программного обеспечения hello, создать центр IoT и зарегистрировать устройство в центре IoT hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, облачные службы Интернета вещей, ПО Интернета вещей, Azure CLI, установка git в Ubuntu, запуск инструмента Gulp, установка Node.js в Ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 38c4d5d9cceec47758f0641cc26b631a7b19d37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="b27f7-104">Получить средства hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="b27f7-104">Get hello tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b27f7-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="b27f7-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="b27f7-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="b27f7-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="b27f7-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="b27f7-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="b27f7-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="b27f7-108">What you will do</span></span>

- <span data-ttu-id="b27f7-109">Установка Git, Node.js, Gulp и Python.</span><span class="sxs-lookup"><span data-stu-id="b27f7-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="b27f7-110">Установите hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="b27f7-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="b27f7-111">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b27f7-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="b27f7-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="b27f7-112">What you will learn</span></span>

<span data-ttu-id="b27f7-113">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="b27f7-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="b27f7-114">Как tooinstall Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="b27f7-114">How tooinstall Git and Node.js.</span></span>
  - <span data-ttu-id="b27f7-115">Git — это распределенная система управления версиями с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="b27f7-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="b27f7-116">Пример приложения Hello на этом занятии будет храниться на Git.</span><span class="sxs-lookup"><span data-stu-id="b27f7-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="b27f7-117">Node.js — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="b27f7-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="b27f7-118">Как NPM tooinstall toouse Node.js-средств разработки.</span><span class="sxs-lookup"><span data-stu-id="b27f7-118">How toouse NPM tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="b27f7-119">Минимальная требуемая версия Hello Node.js — 4,5 LTS.</span><span class="sxs-lookup"><span data-stu-id="b27f7-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="b27f7-120">NPM является одним из диспетчеров пакетов приветствия для Node.js.</span><span class="sxs-lookup"><span data-stu-id="b27f7-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="b27f7-121">Как tooinstall кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b27f7-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="b27f7-122">Visual Studio Code — это упрощенный кроссплатформенный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="b27f7-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="b27f7-123">Он поддерживает возможности отладки, выделения синтаксиса, интеллектуального автозавершения кода, встроенные элементы управления Git, фрагменты кода, а также возможности рефакторинга кода.</span><span class="sxs-lookup"><span data-stu-id="b27f7-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="b27f7-124">Как tooinstall hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b27f7-124">How tooinstall hello Azure CLI</span></span>
  - <span data-ttu-id="b27f7-125">Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure.</span><span class="sxs-lookup"><span data-stu-id="b27f7-125">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="b27f7-126">Работа непосредственно из tooprovision командной строки и управления ресурсами.</span><span class="sxs-lookup"><span data-stu-id="b27f7-126">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="b27f7-127">Как toouse hello Azure CLI toocreate центр IoT.</span><span class="sxs-lookup"><span data-stu-id="b27f7-127">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b27f7-128">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="b27f7-128">What you need</span></span>

- <span data-ttu-id="b27f7-129">Toodownload подключения Internet hello средств и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="b27f7-129">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="b27f7-130">Компьютер под управлением Ubuntu 16.04 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b27f7-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="b27f7-131">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="b27f7-131">Install Git and Node.js</span></span>

<span data-ttu-id="b27f7-132">tooinstall Git и Node.js, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b27f7-132">tooinstall Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="b27f7-133">Нажмите клавишу `Ctrl + Alt + T` tooopen терминала.</span><span class="sxs-lookup"><span data-stu-id="b27f7-133">Press `Ctrl + Alt + T` tooopen a terminal.</span></span>
2. <span data-ttu-id="b27f7-134">Выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="b27f7-134">Run hello following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="b27f7-135">Установка инструментов разработки Node.js</span><span class="sxs-lookup"><span data-stu-id="b27f7-135">Install Node.js development tools</span></span>

<span data-ttu-id="b27f7-136">Вы используете [gulp.js](http://gulpjs.com/) tooautomate развертывания и выполнения скриптов.</span><span class="sxs-lookup"><span data-stu-id="b27f7-136">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="b27f7-137">gulp tooinstall, запустите следующую команду в терминале hello hello:</span><span class="sxs-lookup"><span data-stu-id="b27f7-137">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="b27f7-138">При возникновении проблем с установкой hello. в разделе hello [руководство по устранению неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md) для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="b27f7-138">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="b27f7-139">Узел, NPM и Gulp являются необходимые toorun сценариев автоматизации, разработанные в Node.js.</span><span class="sxs-lookup"><span data-stu-id="b27f7-139">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="b27f7-140">Установка hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b27f7-140">Install hello Azure CLI</span></span>

<span data-ttu-id="b27f7-141">tooinstall hello Azure CLI, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b27f7-141">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="b27f7-142">Выполните следующие команды в терминале hello hello.</span><span class="sxs-lookup"><span data-stu-id="b27f7-142">Run hello following commands in hello terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="b27f7-143">Hello установки может потребоваться 5 минут.</span><span class="sxs-lookup"><span data-stu-id="b27f7-143">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="b27f7-144">Проверка установки hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="b27f7-144">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="b27f7-145">Вы увидите следующее hello выходных данных, если hello успешно установлен.</span><span class="sxs-lookup"><span data-stu-id="b27f7-145">You should see hello following output if hello installation is successful.</span></span>
<span data-ttu-id="b27f7-146">![Проверка установки Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="b27f7-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="b27f7-147">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b27f7-147">Install Visual Studio Code</span></span>

<span data-ttu-id="b27f7-148">Использование кода Visual Studio в файлах конфигурации учебника tooedit hello в более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b27f7-148">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="b27f7-149">[Скачайте](https://code.visualstudio.com/docs/setup/linux) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b27f7-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="b27f7-150">Сводка</span><span class="sxs-lookup"><span data-stu-id="b27f7-150">Summary</span></span>

<span data-ttu-id="b27f7-151">Вы установили все необходимые hello средств и программного обеспечения на главный компьютер.</span><span class="sxs-lookup"><span data-stu-id="b27f7-151">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="b27f7-152">Следующая задача является toouse hello Azure CLI toocreate центр IoT и зарегистрировать устройство в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="b27f7-152">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b27f7-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b27f7-153">Next steps</span></span>
[<span data-ttu-id="b27f7-154">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="b27f7-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
