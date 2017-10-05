---
title: "Подключение Arduino к Интернету вещей Azure. Урок 2. Средства Azure (Windows) | Документация Майкрософт"
description: "С помощью этой статьи вы установите Python и интерфейс командной строки Azure (Azure CLI) в Windows 7 и более поздних версиях."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure CLI, облачная служба Интернета вещей, облако Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 70dfff14-4be1-468d-9919-e40f4bead308
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1f121d9f22f8a7c8582df4d2e62191cec364da46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="f38a4-104">Получение инструментов Azure (Windows 7 и более поздние версии)</span><span class="sxs-lookup"><span data-stu-id="f38a4-104">Get Azure tools (Windows 7 and later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="f38a4-105">[Windows 7 или более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="f38a4-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="f38a4-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="f38a4-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="f38a4-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="f38a4-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f38a4-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="f38a4-108">What you will do</span></span>

<span data-ttu-id="f38a4-109">Установка Python и интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="f38a4-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="f38a4-110">Если возникнут какие-либо проблемы в работе платы Adafruit Feather M0 WiFi Arduino, решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f38a4-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f38a4-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="f38a4-111">What you will learn</span></span>
<span data-ttu-id="f38a4-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="f38a4-112">In this article, you will learn:</span></span>
* <span data-ttu-id="f38a4-113">Как установить Python.</span><span class="sxs-lookup"><span data-stu-id="f38a4-113">How to install Python.</span></span>
* <span data-ttu-id="f38a4-114">Как установить интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="f38a4-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f38a4-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="f38a4-115">What you need</span></span>
* <span data-ttu-id="f38a4-116">Компьютер под управлением Windows с подключением к Интернету.</span><span class="sxs-lookup"><span data-stu-id="f38a4-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="f38a4-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="f38a4-117">An active Azure subscription.</span></span> <span data-ttu-id="f38a4-118">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f38a4-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="f38a4-119">Установка Python</span><span class="sxs-lookup"><span data-stu-id="f38a4-119">Install Python</span></span>
<span data-ttu-id="f38a4-120">[Установите Python](https://www.python.org/downloads/) на компьютере под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="f38a4-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="f38a4-121">Установить можно такие версии Python: 2.7, 3.4 или 3.5.</span><span class="sxs-lookup"><span data-stu-id="f38a4-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="f38a4-122">Это руководство основано на версии Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="f38a4-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="f38a4-123">Если вы уже установили Python, перейдите к следующему разделу и установите интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="f38a4-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="f38a4-124">Кроме того, в системную переменную среды `PATH` необходимо добавить путь к папкам установки python.exe и pip.exe.</span><span class="sxs-lookup"><span data-stu-id="f38a4-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="f38a4-125">По умолчанию файл python.exe устанавливается в папку `C:\Python27`, а pip.exe — в `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="f38a4-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="f38a4-126">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f38a4-126">Install the Azure CLI</span></span>
<span data-ttu-id="f38a4-127">Azure CLI — это кроссплатформенное средство для работы с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="f38a4-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="f38a4-128">С его помощью можно подготавливать ресурсы для Azure и управлять ими непосредственно в командной строке.</span><span class="sxs-lookup"><span data-stu-id="f38a4-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="f38a4-129">Для установки Azure CLI выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f38a4-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="f38a4-130">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="f38a4-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="f38a4-131">Выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="f38a4-131">Run the following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="f38a4-132">Проверьте установку, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f38a4-132">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="f38a4-133">Если установка прошла успешно, отобразятся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="f38a4-133">You see the following output if the installation is successful.</span></span>

![Выходные данные, указывающие на успешное выполнение][output]

## <a name="summary"></a><span data-ttu-id="f38a4-135">Сводка</span><span class="sxs-lookup"><span data-stu-id="f38a4-135">Summary</span></span>
<span data-ttu-id="f38a4-136">Вы установили интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="f38a4-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="f38a4-137">Перейдите к следующей задаче: создайте Центр Интернета вещей Azure и удостоверение устройства с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="f38a4-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f38a4-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f38a4-138">Next steps</span></span>
<span data-ttu-id="f38a4-139">[Создание Центра Интернета вещей и регистрация платы Arduino][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="f38a4-139">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_win.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md