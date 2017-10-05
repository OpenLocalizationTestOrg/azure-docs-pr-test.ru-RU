---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Урок 2. Получение инструментов Azure (Windows) | Документация Майкрософт"
description: "С помощью этой статьи вы установите Python и интерфейс командной строки Azure (Azure CLI) в Windows 7 и более поздних версиях."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "облачная служба Интернета вещей, azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a3c083b5-0d76-46af-bc77-2ad7d8aadc1e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aa96000cb676c088a90f2b3d45c159913185a2e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="cb1b0-104">Получение инструментов Azure (Windows 7 и более поздние версии)</span><span class="sxs-lookup"><span data-stu-id="cb1b0-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb1b0-105">Windows 7 и более поздние версии</span><span class="sxs-lookup"><span data-stu-id="cb1b0-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="cb1b0-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="cb1b0-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="cb1b0-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="cb1b0-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="cb1b0-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="cb1b0-108">What you will do</span></span>
<span data-ttu-id="cb1b0-109">Установка Python и интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="cb1b0-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="cb1b0-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cb1b0-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cb1b0-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="cb1b0-111">What you will learn</span></span>
<span data-ttu-id="cb1b0-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="cb1b0-112">In this article, you will learn:</span></span>
* <span data-ttu-id="cb1b0-113">Как установить Python.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-113">How to install Python.</span></span>
* <span data-ttu-id="cb1b0-114">Как установить интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cb1b0-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="cb1b0-115">What you need</span></span>
* <span data-ttu-id="cb1b0-116">Компьютер под управлением Windows с подключением к Интернету.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="cb1b0-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-117">An active Azure subscription.</span></span> <span data-ttu-id="cb1b0-118">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="cb1b0-119">Установка Python</span><span class="sxs-lookup"><span data-stu-id="cb1b0-119">Install Python</span></span>
<span data-ttu-id="cb1b0-120">[Установите Python](https://www.python.org/downloads/) на компьютере под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="cb1b0-121">Установить можно такие версии Python: 2.7, 3.4 или 3.5.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="cb1b0-122">Это руководство основано на версии Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="cb1b0-123">Если вы уже установили Python, перейдите к следующему разделу и установите интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="cb1b0-124">Кроме того, в системную переменную среды `PATH` необходимо добавить путь к папкам установки python.exe и pip.exe.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="cb1b0-125">По умолчанию файл python.exe устанавливается в папку `C:\Python27`, а pip.exe — в `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="cb1b0-126">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cb1b0-126">Install the Azure CLI</span></span>
<span data-ttu-id="cb1b0-127">Azure CLI — это кроссплатформенное средство для работы с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="cb1b0-128">С его помощью можно подготавливать ресурсы для Azure и управлять ими непосредственно в командной строке.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="cb1b0-129">Для установки Azure CLI выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="cb1b0-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="cb1b0-130">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="cb1b0-131">Выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="cb1b0-131">Run the following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="cb1b0-132">Проверьте установку, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cb1b0-132">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="cb1b0-133">Если установка прошла успешно, отобразятся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="cb1b0-133">You see the following output if the installation is successful.</span></span>

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="cb1b0-135">Сводка</span><span class="sxs-lookup"><span data-stu-id="cb1b0-135">Summary</span></span>
<span data-ttu-id="cb1b0-136">Вы установили интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="cb1b0-137">Перейдите к следующей задаче: создайте Центр Интернета вещей Azure и удостоверение устройства с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="cb1b0-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb1b0-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cb1b0-138">Next steps</span></span>
[<span data-ttu-id="cb1b0-139">Создание Центра Интернета вещей и регистрация Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="cb1b0-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

