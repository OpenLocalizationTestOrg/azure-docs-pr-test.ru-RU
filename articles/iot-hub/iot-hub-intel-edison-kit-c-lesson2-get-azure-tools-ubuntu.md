---
title: "Connect Intel Edison (C) tooAzure IoT — Lesson 2: инструменты Azure (Ubuntu) | Документы Microsoft"
description: "Установка Python и интерфейса командной строки Azure (Azure CLI) на компьютер под управлением Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure CLI, облачная служба Интернета вещей, облако Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 2463cb8e-5758-4d72-af98-62520d41f2f7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a7691c13d43aa6dfff24adf2b470728d5266713e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="e30b7-104">Получение инструментов Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="e30b7-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e30b7-105">[Windows 7 и более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="e30b7-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="e30b7-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="e30b7-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="e30b7-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="e30b7-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e30b7-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="e30b7-108">What you will do</span></span>
<span data-ttu-id="e30b7-109">Установите hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="e30b7-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="e30b7-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e30b7-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e30b7-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="e30b7-111">What you will learn</span></span>
<span data-ttu-id="e30b7-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="e30b7-112">In this article, you will learn:</span></span>
* <span data-ttu-id="e30b7-113">Как tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e30b7-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="e30b7-114">Как tooadd IoT подгруппой hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e30b7-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e30b7-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="e30b7-115">What you need</span></span>
* <span data-ttu-id="e30b7-116">Компьютер под управлением Ubuntu с подключением к Интернету.</span><span class="sxs-lookup"><span data-stu-id="e30b7-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="e30b7-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="e30b7-117">An active Azure subscription.</span></span> <span data-ttu-id="e30b7-118">Если у вас нет учетной записи, можно создать [бесплатную учетную запись](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e30b7-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="e30b7-119">Установка hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e30b7-119">Install hello Azure CLI</span></span>
<span data-ttu-id="e30b7-120">Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure, позволяя toowork непосредственно из вашего tooprovision командной строки и управлять ресурсами.</span><span class="sxs-lookup"><span data-stu-id="e30b7-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="e30b7-121">tooinstall Здравствуйте последнюю Azure CLI, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e30b7-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="e30b7-122">Выполните следующие команды в окне терминала hello.</span><span class="sxs-lookup"><span data-stu-id="e30b7-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="e30b7-123">Может потребоваться пять минут tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e30b7-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="e30b7-124">Проверка установки hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e30b7-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="e30b7-125">Вы увидите следующее hello выходных данных, если hello успешно установлен.</span><span class="sxs-lookup"><span data-stu-id="e30b7-125">You should see hello following output if hello installation is successful.</span></span>

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="e30b7-127">Сводка</span><span class="sxs-lookup"><span data-stu-id="e30b7-127">Summary</span></span>
<span data-ttu-id="e30b7-128">После установки hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e30b7-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="e30b7-129">Следующая задача — toocreate центр Azure IoT и устройствами с помощью удостоверения hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e30b7-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e30b7-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e30b7-130">Next steps</span></span>
<span data-ttu-id="e30b7-131">[Создание Центра Интернета вещей и регистрация Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="e30b7-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
