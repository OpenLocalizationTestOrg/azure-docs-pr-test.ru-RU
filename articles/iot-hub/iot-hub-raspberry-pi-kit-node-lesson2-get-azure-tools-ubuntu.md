---
title: "Подключения Raspberry Pi (узел) tooAzure IoT — Lesson 2: средства (Ubuntu) | Документы Microsoft"
description: "Установите Python и hello Azure командной строки (CLI Azure) на Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "облачная служба Интернета вещей, azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2f98923a-5274-4220-87d4-77ac8beb4d0f
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0adf91bef41f502e1333fdcc75cfb2fe912364c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="a3500-104">Получение инструментов Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="a3500-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a3500-105">Windows 7 и более поздние версии</span><span class="sxs-lookup"><span data-stu-id="a3500-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="a3500-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="a3500-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="a3500-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="a3500-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="a3500-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="a3500-108">What you will do</span></span>
<span data-ttu-id="a3500-109">Установите hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="a3500-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="a3500-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a3500-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a3500-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="a3500-111">What you will learn</span></span>
<span data-ttu-id="a3500-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="a3500-112">In this article, you will learn:</span></span>
* <span data-ttu-id="a3500-113">Как tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a3500-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="a3500-114">Как tooadd IoT подгруппой hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a3500-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a3500-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="a3500-115">What you need</span></span>
* <span data-ttu-id="a3500-116">Компьютер под управлением Ubuntu с подключением к Интернету.</span><span class="sxs-lookup"><span data-stu-id="a3500-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="a3500-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="a3500-117">An active Azure subscription.</span></span> <span data-ttu-id="a3500-118">Если у вас нет учетной записи, можно создать [бесплатную учетную запись](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a3500-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="a3500-119">Установка hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a3500-119">Install hello Azure CLI</span></span>
<span data-ttu-id="a3500-120">Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure, позволяя toowork непосредственно из вашего командной строки tooprovision ресурсы и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="a3500-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command-line tooprovision and manage resources.</span></span>

<span data-ttu-id="a3500-121">tooinstall Здравствуйте последнюю Azure CLI, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a3500-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="a3500-122">Выполните следующие команды в окне терминала hello.</span><span class="sxs-lookup"><span data-stu-id="a3500-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="a3500-123">Может потребоваться пять минут tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a3500-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="a3500-124">Проверка установки hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="a3500-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="a3500-125">Вы увидите следующее hello выходных данных, если hello успешно установлен.</span><span class="sxs-lookup"><span data-stu-id="a3500-125">You should see hello following output if hello installation is successful.</span></span>

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="a3500-127">Сводка</span><span class="sxs-lookup"><span data-stu-id="a3500-127">Summary</span></span>
<span data-ttu-id="a3500-128">После установки hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a3500-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="a3500-129">Следующая задача — toocreate центр Azure IoT и устройствами с помощью удостоверения hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a3500-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3500-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3500-130">Next steps</span></span>
[<span data-ttu-id="a3500-131">Создание Центра Интернета вещей и регистрация Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="a3500-131">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

