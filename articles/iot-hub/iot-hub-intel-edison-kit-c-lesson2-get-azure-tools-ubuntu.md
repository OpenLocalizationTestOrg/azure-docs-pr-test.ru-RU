---
title: "Подключение Intel Edison (C) к Интернету вещей Azure. Урок 2. Получение инструментов Azure (Ubuntu) | Документация Майкрософт"
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
ms.openlocfilehash: 897ab63af85a1f830ed49084ce7c3e74c84a4cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="f041d-104">Получение инструментов Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="f041d-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="f041d-105">[Windows 7 и более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="f041d-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="f041d-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="f041d-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="f041d-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="f041d-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f041d-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="f041d-108">What you will do</span></span>
<span data-ttu-id="f041d-109">Установите интерфейс командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="f041d-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="f041d-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="f041d-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f041d-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="f041d-111">What you will learn</span></span>
<span data-ttu-id="f041d-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="f041d-112">In this article, you will learn:</span></span>
* <span data-ttu-id="f041d-113">Как установить интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="f041d-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="f041d-114">Как добавить подгруппу команд интерфейса командной строки Azure для Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f041d-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f041d-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="f041d-115">What you need</span></span>
* <span data-ttu-id="f041d-116">Компьютер под управлением Ubuntu с подключением к Интернету.</span><span class="sxs-lookup"><span data-stu-id="f041d-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="f041d-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="f041d-117">An active Azure subscription.</span></span> <span data-ttu-id="f041d-118">Если у вас нет учетной записи, можно создать [бесплатную учетную запись](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f041d-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="f041d-119">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f041d-119">Install the Azure CLI</span></span>
<span data-ttu-id="f041d-120">Azure CLI — это кроссплатформенное средство для подготовки ресурсов и управлении ими непосредственно в командной строке Azure.</span><span class="sxs-lookup"><span data-stu-id="f041d-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="f041d-121">Чтобы установить последнюю версию Azure CLI, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f041d-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="f041d-122">Выполните следующие команды в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="f041d-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="f041d-123">Установка интерфейса командной строки Azure может занять около пяти минут.</span><span class="sxs-lookup"><span data-stu-id="f041d-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="f041d-124">Выполните следующую команду, чтобы проверить установку:</span><span class="sxs-lookup"><span data-stu-id="f041d-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="f041d-125">Если установка прошла успешно, отобразятся следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="f041d-125">You should see the following output if the installation is successful.</span></span>

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="f041d-127">Сводка</span><span class="sxs-lookup"><span data-stu-id="f041d-127">Summary</span></span>
<span data-ttu-id="f041d-128">Вы установили интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="f041d-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="f041d-129">Перейдите к следующей задаче: создайте Центр Интернета вещей Azure и удостоверение устройства с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="f041d-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f041d-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f041d-130">Next steps</span></span>
<span data-ttu-id="f041d-131">[Создание Центра Интернета вещей и регистрация Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="f041d-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
