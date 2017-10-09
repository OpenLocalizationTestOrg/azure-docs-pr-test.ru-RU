---
title: "Подключения Arduino tooAzure IoT — Lesson 2: инструменты Azure (macOS) | Документы Microsoft"
description: "Установка Python и интерфейса командной строки Azure (Azure CLI) на компьютер под управлением macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure CLI, облачная служба Интернета вещей, облако Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9b719293-01d2-4a2d-9c49-476e67f4816d
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0ec4131e54af5475cd0b4240480c3fda497e14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="f915d-104">Получение инструментов Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="f915d-104">Get Azure tools (macOS 10.10)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="f915d-105">[Windows 7 или более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="f915d-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="f915d-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="f915d-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="f915d-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="f915d-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f915d-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="f915d-108">What you will do</span></span>

<span data-ttu-id="f915d-109">Установите hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="f915d-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="f915d-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit Растушевка M0 Wi-Fi Arduino плата.</span><span class="sxs-lookup"><span data-stu-id="f915d-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f915d-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="f915d-111">What you will learn</span></span>
<span data-ttu-id="f915d-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="f915d-112">In this article, you will learn:</span></span>
* <span data-ttu-id="f915d-113">Как tooinstall Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f915d-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="f915d-114">Как tooadd IoT подгруппой hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f915d-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f915d-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="f915d-115">What you need</span></span>
* <span data-ttu-id="f915d-116">Компьютер под управлением Mac с подключением к Интернету.</span><span class="sxs-lookup"><span data-stu-id="f915d-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="f915d-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="f915d-117">An active Azure subscription.</span></span> <span data-ttu-id="f915d-118">Если у вас нет учетной записи Azure, можно создать [бесплатную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f915d-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="f915d-119">Установка Python</span><span class="sxs-lookup"><span data-stu-id="f915d-119">Install Python</span></span>
<span data-ttu-id="f915d-120">Несмотря на то, что macOS поставляется с Python 2.7 стандартной hello, рекомендуется установить Python через Homebrew.</span><span class="sxs-lookup"><span data-stu-id="f915d-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="f915d-121">См. статью [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/) (Установка Python на Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="f915d-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="f915d-122">Установите Python и pip, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="f915d-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="f915d-123">Установка hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f915d-123">Install hello Azure CLI</span></span>
<span data-ttu-id="f915d-124">Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure.</span><span class="sxs-lookup"><span data-stu-id="f915d-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="f915d-125">Работа непосредственно из вашего tooprovision командной строки и управления ресурсами.</span><span class="sxs-lookup"><span data-stu-id="f915d-125">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="f915d-126">tooinstall Здравствуйте последнюю Azure CLI, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f915d-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="f915d-127">Выполните следующие команды в окне терминала hello.</span><span class="sxs-lookup"><span data-stu-id="f915d-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="f915d-128">Может потребоваться пять минут tooinstall hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f915d-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="f915d-129">Проверка установки hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="f915d-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="f915d-130">Вы увидите следующее hello выходных данных, если hello успешно установлен.</span><span class="sxs-lookup"><span data-stu-id="f915d-130">You should see hello following output if hello installation is successful.</span></span>

![Выходные данные, указывающие на успешное выполнение][output]

## <a name="summary"></a><span data-ttu-id="f915d-132">Сводка</span><span class="sxs-lookup"><span data-stu-id="f915d-132">Summary</span></span>
<span data-ttu-id="f915d-133">После установки hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f915d-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="f915d-134">Следующая задача — toocreate Azure IoT идентификаторов концентратора и устройств с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f915d-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f915d-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f915d-135">Next steps</span></span>
<span data-ttu-id="f915d-136">[Создание Центра Интернета вещей и регистрация платы Arduino][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="f915d-136">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_osx.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md