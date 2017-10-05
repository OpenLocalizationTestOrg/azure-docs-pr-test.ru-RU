---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 2. Получение инструментов (Windows) | Документация Майкрософт"
description: "Установите инструменты и программное обеспечение на главном компьютере под управлением Windows, создайте Центр Интернета вещей и зарегистрируйте устройство в нем."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, облачная служба Интернета вещей, программное обеспечение Интернета вещей, Azure CLI, ПО Интернета вещей, установка git в Windows, запуск инструмента Gulp, установка Node.js в Windows, установка Npm в Windows, установка Python в Windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0d8ba03df63d0b8657a9e275fc636e806c66b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a><span data-ttu-id="95ca1-104">Получение инструментов (Windows 7 и более поздние версии)</span><span class="sxs-lookup"><span data-stu-id="95ca1-104">Get the tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95ca1-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="95ca1-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="95ca1-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="95ca1-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="95ca1-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="95ca1-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="95ca1-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="95ca1-108">What you will do</span></span>

- <span data-ttu-id="95ca1-109">Установка Git, Node.js, Gulp и Python.</span><span class="sxs-lookup"><span data-stu-id="95ca1-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="95ca1-110">Установите интерфейс командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="95ca1-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="95ca1-111">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="95ca1-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="95ca1-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="95ca1-112">What you will learn</span></span>

<span data-ttu-id="95ca1-113">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="95ca1-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="95ca1-114">Как установить [Git](https://git-scm.com/) и [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="95ca1-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="95ca1-115">Git — это распределенная система управления версиями с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="95ca1-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="95ca1-116">Пример приложения, используемый в этом руководстве, хранится в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="95ca1-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="95ca1-117">Node.js — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="95ca1-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="95ca1-118">Как установить инструменты разработки для Node.js. с помощью [NPM](https://www.npmjs.com/).</span><span class="sxs-lookup"><span data-stu-id="95ca1-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="95ca1-119">Минимальная требуемая версия Node.js — 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="95ca1-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="95ca1-120">NPM — это один из диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="95ca1-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="95ca1-121">Как установить Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="95ca1-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="95ca1-122">Visual Studio Code — это упрощенный кроссплатформенный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="95ca1-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="95ca1-123">Он поддерживает возможности отладки, выделения синтаксиса, интеллектуального автозавершения кода, встроенные элементы управления Git, фрагменты кода, а также возможности рефакторинга кода.</span><span class="sxs-lookup"><span data-stu-id="95ca1-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="95ca1-124">Как установить Python.</span><span class="sxs-lookup"><span data-stu-id="95ca1-124">How to install Python.</span></span>
  - <span data-ttu-id="95ca1-125">Python — это широко используемый высокоуровневый интерпретируемый и динамический язык программирования общего назначения.</span><span class="sxs-lookup"><span data-stu-id="95ca1-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="95ca1-126">Как установить интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="95ca1-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="95ca1-127">Azure CLI — это кроссплатформенное средство для работы с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="95ca1-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="95ca1-128">С его помощью можно подготавливать ресурсы для Azure и управлять ими непосредственно в командной строке.</span><span class="sxs-lookup"><span data-stu-id="95ca1-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="95ca1-129">Как создать Центр Интернета вещей с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="95ca1-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="95ca1-130">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="95ca1-130">What you need</span></span>

- <span data-ttu-id="95ca1-131">Подключение к Интернету для скачивания инструментов и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="95ca1-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="95ca1-132">Компьютер Windows.</span><span class="sxs-lookup"><span data-stu-id="95ca1-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="95ca1-133">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="95ca1-133">Install Git and Node.js</span></span>

<span data-ttu-id="95ca1-134">Воспользуйтесь приведенными ниже ссылками, чтобы скачать и установить Git и LTS Node.js для Windows.</span><span class="sxs-lookup"><span data-stu-id="95ca1-134">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="95ca1-135">Скачать Git для Windows</span><span class="sxs-lookup"><span data-stu-id="95ca1-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="95ca1-136">Скачать Node.js LTS для Windows</span><span class="sxs-lookup"><span data-stu-id="95ca1-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="95ca1-137">Установка инструментов разработки Node.js</span><span class="sxs-lookup"><span data-stu-id="95ca1-137">Install Node.js development tools</span></span>

<span data-ttu-id="95ca1-138">Используйте [gulp.js](http://gulpjs.com/) для автоматизации развертывания и выполнения сценариев.</span><span class="sxs-lookup"><span data-stu-id="95ca1-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="95ca1-139">Нажмите клавиши `Windows + R`, введите `cmd`, а затем нажмите клавишу `Enter`, чтобы открыть окно командной строки, и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="95ca1-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="95ca1-140">Если при установке возникают проблемы, способы их устранения см. в [этом руководстве по устранению неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="95ca1-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="95ca1-141">Для выполнения сценариев автоматизации, разработанных в Node.js, требуются Node, NPM и Gulp.</span><span class="sxs-lookup"><span data-stu-id="95ca1-141">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="95ca1-142">Установка Python</span><span class="sxs-lookup"><span data-stu-id="95ca1-142">Install Python</span></span>

<span data-ttu-id="95ca1-143">Вы можете выбрать одну из следующих версий Python: 2.7, 3.4 или 3.5.</span><span class="sxs-lookup"><span data-stu-id="95ca1-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="95ca1-144">В этом руководстве мы используем Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="95ca1-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="95ca1-145">Если вы уже установили Python, перейдите к следующему разделу.</span><span class="sxs-lookup"><span data-stu-id="95ca1-145">If you've already installed python, go to the next section.</span></span>

[<span data-ttu-id="95ca1-146">Скачать Python для Windows</span><span class="sxs-lookup"><span data-stu-id="95ca1-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="95ca1-147">Кроме того, в системную переменную среды `PATH` необходимо добавить путь к папкам установки python.exe и pip.exe.</span><span class="sxs-lookup"><span data-stu-id="95ca1-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="95ca1-148">По умолчанию файл python.exe устанавливается в папку `C:\Python27`, а pip.exe — в `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="95ca1-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="95ca1-149">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="95ca1-149">Install the Azure CLI</span></span>

<span data-ttu-id="95ca1-150">Для установки Azure CLI выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="95ca1-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="95ca1-151">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="95ca1-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="95ca1-152">Установите Azure CLI, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="95ca1-152">Install the Azure CLI by running the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="95ca1-153">Установка может занять 5 минут.</span><span class="sxs-lookup"><span data-stu-id="95ca1-153">The installation might take 5 minutes.</span></span>

3. <span data-ttu-id="95ca1-154">Выполните следующую команду, чтобы проверить установку:</span><span class="sxs-lookup"><span data-stu-id="95ca1-154">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="95ca1-155">Если установка прошла успешно, отобразятся следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="95ca1-155">You should see the following output if the installation is successful.</span></span>

   ![Проверка установки Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="95ca1-157">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="95ca1-157">Install Visual Studio Code</span></span>

<span data-ttu-id="95ca1-158">Позже в этом руководстве вы используете Visual Studio Code, чтобы изменить файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="95ca1-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="95ca1-159">[Скачайте](https://code.visualstudio.com/docs/setup/windows) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="95ca1-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="95ca1-160">Сводка</span><span class="sxs-lookup"><span data-stu-id="95ca1-160">Summary</span></span>

<span data-ttu-id="95ca1-161">Вы установили на главном компьютере все необходимые инструменты и программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="95ca1-161">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="95ca1-162">Следующая задача заключается в создании Центра Интернета вещей и регистрации в нем устройства с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="95ca1-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95ca1-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="95ca1-163">Next steps</span></span>
[<span data-ttu-id="95ca1-164">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="95ca1-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
