---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 2. Получение инструментов (Windows) | Документация Майкрософт"
description: "Установите на главный компьютер под управлением Windows hello средств и программного обеспечения hello, создать центр IoT и зарегистрировать устройство в центре IoT hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, облачная служба Интернета вещей, программное обеспечение Интернета вещей, Azure CLI, ПО Интернета вещей, установка git в Windows, запуск инструмента Gulp, установка Node.js в Windows, установка Npm в Windows, установка Python в Windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7ca3c9f11eb232f853fc8fd921b0a49ae37d0184
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a><span data-ttu-id="547de-104">Получить средства hello (Windows 7 и более поздние версии)</span><span class="sxs-lookup"><span data-stu-id="547de-104">Get hello tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="547de-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="547de-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="547de-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="547de-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="547de-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="547de-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="547de-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="547de-108">What you will do</span></span>

- <span data-ttu-id="547de-109">Установка Git, Node.js, Gulp и Python.</span><span class="sxs-lookup"><span data-stu-id="547de-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="547de-110">Установите hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="547de-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="547de-111">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="547de-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="547de-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="547de-112">What you will learn</span></span>

<span data-ttu-id="547de-113">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="547de-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="547de-114">Как tooinstall [Git](https://git-scm.com/) и [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="547de-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="547de-115">Git — это распределенная система управления версиями с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="547de-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="547de-116">Пример приложения Hello на этом занятии будет храниться на Git.</span><span class="sxs-lookup"><span data-stu-id="547de-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="547de-117">Node.js — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="547de-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="547de-118">Как toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span><span class="sxs-lookup"><span data-stu-id="547de-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="547de-119">Минимальная требуемая версия Hello Node.js — 4,5 LTS.</span><span class="sxs-lookup"><span data-stu-id="547de-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="547de-120">NPM является одним из диспетчеров пакетов приветствия для Node.js.</span><span class="sxs-lookup"><span data-stu-id="547de-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="547de-121">Как tooinstall кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="547de-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="547de-122">Visual Studio Code — это упрощенный кроссплатформенный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="547de-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="547de-123">Он поддерживает возможности отладки, выделения синтаксиса, интеллектуального автозавершения кода, встроенные элементы управления Git, фрагменты кода, а также возможности рефакторинга кода.</span><span class="sxs-lookup"><span data-stu-id="547de-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="547de-124">Как tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="547de-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="547de-125">Python — это широко используемый высокоуровневый интерпретируемый и динамический язык программирования общего назначения.</span><span class="sxs-lookup"><span data-stu-id="547de-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="547de-126">Как tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="547de-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="547de-127">Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure.</span><span class="sxs-lookup"><span data-stu-id="547de-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="547de-128">Работа непосредственно из tooprovision командной строки и управления ресурсами.</span><span class="sxs-lookup"><span data-stu-id="547de-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="547de-129">Как toouse hello Azure CLI toocreate центр IoT.</span><span class="sxs-lookup"><span data-stu-id="547de-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="547de-130">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="547de-130">What you need</span></span>

- <span data-ttu-id="547de-131">Toodownload подключения Internet hello средств и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="547de-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="547de-132">Компьютер Windows.</span><span class="sxs-lookup"><span data-stu-id="547de-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="547de-133">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="547de-133">Install Git and Node.js</span></span>

<span data-ttu-id="547de-134">Щелкните следующие ссылки toodownload hello и установите Git и LTS Node.js для Windows.</span><span class="sxs-lookup"><span data-stu-id="547de-134">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="547de-135">Скачать Git для Windows</span><span class="sxs-lookup"><span data-stu-id="547de-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="547de-136">Скачать Node.js LTS для Windows</span><span class="sxs-lookup"><span data-stu-id="547de-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="547de-137">Установка инструментов разработки Node.js</span><span class="sxs-lookup"><span data-stu-id="547de-137">Install Node.js development tools</span></span>

<span data-ttu-id="547de-138">Вы используете [gulp.js](http://gulpjs.com/) tooautomate развертывания и выполнения скриптов.</span><span class="sxs-lookup"><span data-stu-id="547de-138">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="547de-139">Нажмите клавишу `Windows + R`, тип `cmd` и нажмите клавишу `Enter` tooopen окно командной строки и затем выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="547de-139">Press `Windows + R`, type `cmd` and press `Enter` tooopen a Command Prompt window, and then run hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="547de-140">При возникновении проблем с установкой hello. в разделе hello [руководство по устранению неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md) для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="547de-140">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="547de-141">Узел, NPM и Gulp являются необходимые toorun сценариев автоматизации, разработанные в Node.js.</span><span class="sxs-lookup"><span data-stu-id="547de-141">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="547de-142">Установка Python</span><span class="sxs-lookup"><span data-stu-id="547de-142">Install Python</span></span>

<span data-ttu-id="547de-143">Вы можете выбрать одну из следующих версий Python: 2.7, 3.4 или 3.5.</span><span class="sxs-lookup"><span data-stu-id="547de-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="547de-144">В этом руководстве мы используем Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="547de-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="547de-145">Если python уже установлен, перейдите следующему разделу toohello.</span><span class="sxs-lookup"><span data-stu-id="547de-145">If you've already installed python, go toohello next section.</span></span>

[<span data-ttu-id="547de-146">Скачать Python для Windows</span><span class="sxs-lookup"><span data-stu-id="547de-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="547de-147">Необходимо также tooadd hello путь к папкам hello, где Python.exe и pip.exe — установленных toohello системы `PATH` переменной среды.</span><span class="sxs-lookup"><span data-stu-id="547de-147">You also need tooadd hello path of hello folders where Python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="547de-148">По умолчанию файл python.exe устанавливается в папку `C:\Python27`, а pip.exe — в `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="547de-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="547de-149">Установка hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="547de-149">Install hello Azure CLI</span></span>

<span data-ttu-id="547de-150">tooinstall hello Azure CLI, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="547de-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="547de-151">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="547de-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="547de-152">Установите hello Azure CLI, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="547de-152">Install hello Azure CLI by running hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="547de-153">Hello установки может потребоваться 5 минут.</span><span class="sxs-lookup"><span data-stu-id="547de-153">hello installation might take 5 minutes.</span></span>

3. <span data-ttu-id="547de-154">Проверка установки hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="547de-154">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="547de-155">Вы увидите следующее hello выходных данных, если hello успешно установлен.</span><span class="sxs-lookup"><span data-stu-id="547de-155">You should see hello following output if hello installation is successful.</span></span>

   ![Проверка установки Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="547de-157">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="547de-157">Install Visual Studio Code</span></span>

<span data-ttu-id="547de-158">Использование кода Visual Studio в файлах конфигурации учебника tooedit hello в более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="547de-158">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="547de-159">[Скачайте](https://code.visualstudio.com/docs/setup/windows) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="547de-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="547de-160">Сводка</span><span class="sxs-lookup"><span data-stu-id="547de-160">Summary</span></span>

<span data-ttu-id="547de-161">Вы установили все необходимые hello средств и программного обеспечения на главный компьютер.</span><span class="sxs-lookup"><span data-stu-id="547de-161">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="547de-162">Следующая задача является toouse hello Azure CLI toocreate центр IoT и зарегистрировать устройство в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="547de-162">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="547de-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="547de-163">Next steps</span></span>
[<span data-ttu-id="547de-164">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="547de-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
