---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 2. Получение инструментов (Ubuntu) | Документация Майкрософт"
description: "Установите инструменты и программное обеспечение на главном компьютере под управлением Ubuntu, создайте Центр Интернета вещей и зарегистрируйте устройство в нем."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, облачные службы Интернета вещей, ПО Интернета вещей, Azure CLI, установка git в Ubuntu, запуск инструмента Gulp, установка Node.js в Ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 234b60e1f8eaff52ce07f54d4d12de2421cc1a52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="0b4ee-104">Получение инструментов (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="0b4ee-104">Get the tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b4ee-105">Windows 7 или более поздние версии</span><span class="sxs-lookup"><span data-stu-id="0b4ee-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="0b4ee-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="0b4ee-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="0b4ee-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="0b4ee-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="0b4ee-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="0b4ee-108">What you will do</span></span>

- <span data-ttu-id="0b4ee-109">Установка Git, Node.js, Gulp и Python.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="0b4ee-110">Установите интерфейс командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="0b4ee-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="0b4ee-111">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0b4ee-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="0b4ee-112">Новые знания</span><span class="sxs-lookup"><span data-stu-id="0b4ee-112">What you will learn</span></span>

<span data-ttu-id="0b4ee-113">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="0b4ee-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="0b4ee-114">Как установить Git и Node.js.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-114">How to install Git and Node.js.</span></span>
  - <span data-ttu-id="0b4ee-115">Git — это распределенная система управления версиями с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="0b4ee-116">Пример приложения, используемый в этом руководстве, хранится в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="0b4ee-117">Node.js — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="0b4ee-118">Как установить инструменты разработки для Node.js. с помощью NPM.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-118">How to use NPM to install Node.js development tools.</span></span>
  - <span data-ttu-id="0b4ee-119">Минимальная требуемая версия Node.js — 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="0b4ee-120">NPM — это один из диспетчеров пакетов для Node.js.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="0b4ee-121">Как установить Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="0b4ee-122">Visual Studio Code — это упрощенный кроссплатформенный, но мощный редактор исходного кода для платформ Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="0b4ee-123">Он поддерживает возможности отладки, выделения синтаксиса, интеллектуального автозавершения кода, встроенные элементы управления Git, фрагменты кода, а также возможности рефакторинга кода.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="0b4ee-124">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0b4ee-124">How to install the Azure CLI</span></span>
  - <span data-ttu-id="0b4ee-125">Azure CLI — это кроссплатформенное средство для работы с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="0b4ee-126">С его помощью можно подготавливать ресурсы для Azure и управлять ими непосредственно в командной строке.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-126">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="0b4ee-127">Как создать Центр Интернета вещей с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-127">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0b4ee-128">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="0b4ee-128">What you need</span></span>

- <span data-ttu-id="0b4ee-129">Подключение к Интернету для скачивания инструментов и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-129">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="0b4ee-130">Компьютер под управлением Ubuntu 16.04 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="0b4ee-131">Установка Git и Node.js</span><span class="sxs-lookup"><span data-stu-id="0b4ee-131">Install Git and Node.js</span></span>

<span data-ttu-id="0b4ee-132">Чтобы установить Git и Node.js, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="0b4ee-132">To install Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="0b4ee-133">Нажмите клавиши `Ctrl + Alt + T`, чтобы открыть окно терминала.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-133">Press `Ctrl + Alt + T` to open a terminal.</span></span>
2. <span data-ttu-id="0b4ee-134">Выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="0b4ee-134">Run the following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="0b4ee-135">Установка инструментов разработки Node.js</span><span class="sxs-lookup"><span data-stu-id="0b4ee-135">Install Node.js development tools</span></span>

<span data-ttu-id="0b4ee-136">Используйте [gulp.js](http://gulpjs.com/) для автоматизации развертывания и выполнения сценариев.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="0b4ee-137">Чтобы установить Gulp, выполните следующую команду в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="0b4ee-137">To install gulp, run the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="0b4ee-138">Если при установке возникают проблемы, способы их устранения см. в [этом руководстве по устранению неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0b4ee-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="0b4ee-139">Для выполнения сценариев автоматизации, разработанных в Node.js, требуются Node, NPM и Gulp.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-139">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="0b4ee-140">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0b4ee-140">Install the Azure CLI</span></span>

<span data-ttu-id="0b4ee-141">Для установки Azure CLI выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0b4ee-141">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="0b4ee-142">Выполните следующие команды в окне терминала:</span><span class="sxs-lookup"><span data-stu-id="0b4ee-142">Run the following commands in the terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="0b4ee-143">Установка может занять 5 минут.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-143">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="0b4ee-144">Выполните следующую команду, чтобы проверить установку:</span><span class="sxs-lookup"><span data-stu-id="0b4ee-144">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="0b4ee-145">Если установка прошла успешно, отобразятся следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-145">You should see the following output if the installation is successful.</span></span>
<span data-ttu-id="0b4ee-146">![Проверка установки Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="0b4ee-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="0b4ee-147">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0b4ee-147">Install Visual Studio Code</span></span>

<span data-ttu-id="0b4ee-148">Позже в этом руководстве вы используете Visual Studio Code, чтобы изменить файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="0b4ee-149">[Скачайте](https://code.visualstudio.com/docs/setup/linux) и установите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="0b4ee-150">Сводка</span><span class="sxs-lookup"><span data-stu-id="0b4ee-150">Summary</span></span>

<span data-ttu-id="0b4ee-151">Вы установили на главном компьютере все необходимые инструменты и программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-151">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="0b4ee-152">Следующая задача заключается в создании Центра Интернета вещей и регистрации в нем устройства с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0b4ee-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b4ee-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0b4ee-153">Next steps</span></span>
[<span data-ttu-id="0b4ee-154">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="0b4ee-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
