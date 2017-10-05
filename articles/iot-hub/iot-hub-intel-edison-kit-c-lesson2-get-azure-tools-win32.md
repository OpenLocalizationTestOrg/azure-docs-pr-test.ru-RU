---
title: "Подключение Intel Edison (C) к Интернету вещей Azure. Урок 2. Получение инструментов Azure (Windows) | Документация Майкрософт"
description: "С помощью этой статьи вы установите Python и интерфейс командной строки Azure (Azure CLI) в Windows 7 и более поздних версиях."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure CLI, облачная служба Интернета вещей, облако Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 1035760e-cdd1-4d99-8003-067e98b29762
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 90ef113ae84ccc8cb3cbdbe8c245e138320a93c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="eb574-104">Получение инструментов Azure (Windows 7 и более поздние версии)</span><span class="sxs-lookup"><span data-stu-id="eb574-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="eb574-105">[Windows 7 и более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="eb574-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="eb574-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="eb574-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="eb574-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="eb574-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="eb574-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="eb574-108">What you will do</span></span>
<span data-ttu-id="eb574-109">Установка Python и интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="eb574-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="eb574-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="eb574-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="eb574-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="eb574-111">What you will learn</span></span>
<span data-ttu-id="eb574-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="eb574-112">In this article, you will learn:</span></span>
* <span data-ttu-id="eb574-113">Как установить Python.</span><span class="sxs-lookup"><span data-stu-id="eb574-113">How to install Python.</span></span>
* <span data-ttu-id="eb574-114">Как установить интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="eb574-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="eb574-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="eb574-115">What you need</span></span>
* <span data-ttu-id="eb574-116">Компьютер под управлением Windows с подключением к Интернету.</span><span class="sxs-lookup"><span data-stu-id="eb574-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="eb574-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="eb574-117">An active Azure subscription.</span></span> <span data-ttu-id="eb574-118">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="eb574-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="eb574-119">Установка Python</span><span class="sxs-lookup"><span data-stu-id="eb574-119">Install Python</span></span>
<span data-ttu-id="eb574-120">[Установите Python](https://www.python.org/downloads/) на компьютере под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="eb574-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="eb574-121">Установить можно такие версии Python: 2.7, 3.4 или 3.5.</span><span class="sxs-lookup"><span data-stu-id="eb574-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="eb574-122">Это руководство основано на версии Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="eb574-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="eb574-123">Если вы уже установили Python, перейдите к следующему разделу и установите интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="eb574-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="eb574-124">Кроме того, в системную переменную среды `PATH` необходимо добавить путь к папкам установки python.exe и pip.exe.</span><span class="sxs-lookup"><span data-stu-id="eb574-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="eb574-125">По умолчанию файл python.exe устанавливается в папку `C:\Python27`, а pip.exe — в `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="eb574-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="eb574-126">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eb574-126">Install the Azure CLI</span></span>
<span data-ttu-id="eb574-127">Azure CLI — это кроссплатформенное средство для работы с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="eb574-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="eb574-128">С его помощью можно подготавливать ресурсы для Azure и управлять ими непосредственно в командной строке.</span><span class="sxs-lookup"><span data-stu-id="eb574-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="eb574-129">Для установки Azure CLI выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="eb574-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="eb574-130">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="eb574-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="eb574-131">Выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="eb574-131">Run the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="eb574-132">Проверьте установку, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="eb574-132">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="eb574-133">Если установка прошла успешно, отобразятся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="eb574-133">You see the following output if the installation is successful.</span></span>

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="eb574-135">Сводка</span><span class="sxs-lookup"><span data-stu-id="eb574-135">Summary</span></span>
<span data-ttu-id="eb574-136">Вы установили интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="eb574-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="eb574-137">Перейдите к следующей задаче: создайте Центр Интернета вещей Azure и удостоверение устройства с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="eb574-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb574-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb574-138">Next steps</span></span>
<span data-ttu-id="eb574-139">[Создание Центра Интернета вещей и регистрация Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="eb574-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
