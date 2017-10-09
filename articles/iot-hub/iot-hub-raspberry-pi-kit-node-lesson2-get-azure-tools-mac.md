---
title: "Подключения Raspberry Pi (узел) tooAzure IoT — Lesson 2: средства (Ubuntu) | Документы Microsoft"
description: "Установите Python и hello Azure командной строки (CLI Azure) на macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "облачная служба Интернета вещей, azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 1814b703-2d81-45db-aff0-eb338c97f120
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3f35fae53a360a758bc8f61ed2063f7e2f2dc067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="aa977-104">Получение инструментов Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="aa977-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa977-105">Windows 7 и более поздние версии</span><span class="sxs-lookup"><span data-stu-id="aa977-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="aa977-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="aa977-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="aa977-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="aa977-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="aa977-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="aa977-108">What you will do</span></span>
<span data-ttu-id="aa977-109">Установите hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="aa977-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="aa977-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="aa977-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="aa977-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="aa977-111">What you will learn</span></span>
<span data-ttu-id="aa977-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="aa977-112">In this article, you will learn:</span></span>
* <span data-ttu-id="aa977-113">Как tooinstall Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="aa977-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="aa977-114">Как tooadd IoT подгруппой hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="aa977-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="aa977-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="aa977-115">What you need</span></span>
* <span data-ttu-id="aa977-116">Компьютер под управлением Mac с подключением к Интернету.</span><span class="sxs-lookup"><span data-stu-id="aa977-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="aa977-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="aa977-117">An active Azure subscription.</span></span> <span data-ttu-id="aa977-118">Если у вас нет учетной записи Azure, можно создать [бесплатную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="aa977-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="aa977-119">Установка Python</span><span class="sxs-lookup"><span data-stu-id="aa977-119">Install Python</span></span>
<span data-ttu-id="aa977-120">Несмотря на то, что macOS поставляется с Python 2.7 стандартной hello, рекомендуется установить Python через Homebrew.</span><span class="sxs-lookup"><span data-stu-id="aa977-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="aa977-121">См. статью [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/) (Установка Python на Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="aa977-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="aa977-122">Установите Python и pip, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="aa977-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="aa977-123">Установка hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aa977-123">Install hello Azure CLI</span></span>
<span data-ttu-id="aa977-124">Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure.</span><span class="sxs-lookup"><span data-stu-id="aa977-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="aa977-125">Работа непосредственно из вашего tooprovision командной строки и управления ресурсами.</span><span class="sxs-lookup"><span data-stu-id="aa977-125">You work directly from your command-line tooprovision and manage resources.</span></span> 

<span data-ttu-id="aa977-126">tooinstall Здравствуйте последнюю Azure CLI, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="aa977-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="aa977-127">Выполните следующие команды в окне терминала hello.</span><span class="sxs-lookup"><span data-stu-id="aa977-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="aa977-128">Может потребоваться пять минут tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="aa977-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="aa977-129">Проверка установки hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="aa977-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="aa977-130">Вы увидите следующее hello выходных данных, если hello успешно установлен.</span><span class="sxs-lookup"><span data-stu-id="aa977-130">You should see hello following output if hello installation is successful.</span></span>

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="aa977-132">Сводка</span><span class="sxs-lookup"><span data-stu-id="aa977-132">Summary</span></span>
<span data-ttu-id="aa977-133">После установки hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="aa977-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="aa977-134">Следующая задача — toocreate Azure IoT идентификаторов концентратора и устройств с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="aa977-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa977-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aa977-135">Next steps</span></span>
[<span data-ttu-id="aa977-136">Создание Центра Интернета вещей и регистрация Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="aa977-136">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

