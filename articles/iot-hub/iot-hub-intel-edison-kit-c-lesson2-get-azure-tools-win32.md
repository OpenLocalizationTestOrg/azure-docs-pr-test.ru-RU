---
title: "Connect Intel Edison (C) tooAzure IoT — Lesson 2: инструменты Azure (Windows) | Документы Microsoft"
description: "Установите Python и hello Azure командной строки (CLI Azure) на Windows 7 и более поздних версиях."
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
ms.openlocfilehash: 46f964541c00674500e4f6a072a9a2547b5b24d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="6c417-104">Получение инструментов Azure (Windows 7 и более поздние версии)</span><span class="sxs-lookup"><span data-stu-id="6c417-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="6c417-105">[Windows 7 и более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="6c417-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="6c417-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="6c417-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="6c417-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="6c417-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="6c417-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="6c417-108">What you will do</span></span>
<span data-ttu-id="6c417-109">Установите Python и hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="6c417-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="6c417-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="6c417-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6c417-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="6c417-111">What you will learn</span></span>
<span data-ttu-id="6c417-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="6c417-112">In this article, you will learn:</span></span>
* <span data-ttu-id="6c417-113">Как tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="6c417-113">How tooinstall Python.</span></span>
* <span data-ttu-id="6c417-114">Как tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6c417-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6c417-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="6c417-115">What you need</span></span>
* <span data-ttu-id="6c417-116">Компьютер под управлением Windows с подключением к Интернету.</span><span class="sxs-lookup"><span data-stu-id="6c417-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="6c417-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="6c417-117">An active Azure subscription.</span></span> <span data-ttu-id="6c417-118">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6c417-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="6c417-119">Установка Python</span><span class="sxs-lookup"><span data-stu-id="6c417-119">Install Python</span></span>
<span data-ttu-id="6c417-120">[Установите Python](https://www.python.org/downloads/) на компьютере под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="6c417-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="6c417-121">Установить можно такие версии Python: 2.7, 3.4 или 3.5.</span><span class="sxs-lookup"><span data-stu-id="6c417-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="6c417-122">Это руководство основано на версии Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="6c417-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="6c417-123">Если Python уже установлен, перейдите следующему разделу toohello и установите hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6c417-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="6c417-124">Необходимо также tooadd hello путь к папкам hello, где python.exe и pip.exe — установленных toohello системы `PATH` переменной среды.</span><span class="sxs-lookup"><span data-stu-id="6c417-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="6c417-125">По умолчанию файл python.exe устанавливается в папку `C:\Python27`, а pip.exe — в `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="6c417-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="6c417-126">Установка hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6c417-126">Install hello Azure CLI</span></span>
<span data-ttu-id="6c417-127">Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure.</span><span class="sxs-lookup"><span data-stu-id="6c417-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="6c417-128">Работа непосредственно из вашего tooprovision командной строки и управления ресурсами.</span><span class="sxs-lookup"><span data-stu-id="6c417-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="6c417-129">tooinstall hello Azure CLI, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6c417-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="6c417-130">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="6c417-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="6c417-131">Выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="6c417-131">Run hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="6c417-132">Проверка установки hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="6c417-132">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="6c417-133">Вы увидите, что hello следующие выходные данные, если hello успешно установлен.</span><span class="sxs-lookup"><span data-stu-id="6c417-133">You see hello following output if hello installation is successful.</span></span>

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="6c417-135">Сводка</span><span class="sxs-lookup"><span data-stu-id="6c417-135">Summary</span></span>
<span data-ttu-id="6c417-136">После установки hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6c417-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="6c417-137">Следующего задач toocreate вашу личность Azure IoT hub и устройств с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6c417-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c417-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c417-138">Next steps</span></span>
<span data-ttu-id="6c417-139">[Создание Центра Интернета вещей и регистрация Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="6c417-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
