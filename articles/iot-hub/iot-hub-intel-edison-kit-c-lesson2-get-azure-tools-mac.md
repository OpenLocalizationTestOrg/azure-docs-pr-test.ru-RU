---
title: "Подключение Intel Edison к Интернету вещей Azure. Урок 2. Получение инструментов Azure (macOS) | Документация Майкрософт"
description: "Установка Python и интерфейса командной строки Azure (Azure CLI) на компьютер под управлением macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure CLI, облачная служба Интернета вещей, облако Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97beb04781f3f9809cdafc945d9499e71cbbd9b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="bd4f2-104">Получение инструментов Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="bd4f2-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="bd4f2-105">[Windows 7 и более поздние версии][windows]</span><span class="sxs-lookup"><span data-stu-id="bd4f2-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="bd4f2-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="bd4f2-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="bd4f2-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="bd4f2-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="bd4f2-108">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="bd4f2-108">What you will do</span></span>
<span data-ttu-id="bd4f2-109">Установите интерфейс командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="bd4f2-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="bd4f2-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="bd4f2-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bd4f2-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="bd4f2-111">What you will learn</span></span>
<span data-ttu-id="bd4f2-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="bd4f2-112">In this article, you will learn:</span></span>
* <span data-ttu-id="bd4f2-113">Как установить Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="bd4f2-114">Как добавить подгруппу команд интерфейса командной строки Azure для Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bd4f2-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="bd4f2-115">What you need</span></span>
* <span data-ttu-id="bd4f2-116">Компьютер под управлением Mac с подключением к Интернету.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="bd4f2-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-117">An active Azure subscription.</span></span> <span data-ttu-id="bd4f2-118">Если у вас нет учетной записи Azure, можно создать [бесплатную учетную запись Azure](http://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="bd4f2-119">Установка Python</span><span class="sxs-lookup"><span data-stu-id="bd4f2-119">Install Python</span></span>
<span data-ttu-id="bd4f2-120">Несмотря на то, что macOS поставляется уже с установленной версией Python 2.7, рекомендуется установить Python через Homebrew.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="bd4f2-121">См. статью [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/) (Установка Python на Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="bd4f2-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="bd4f2-122">Установите Python и pip, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bd4f2-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="bd4f2-123">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bd4f2-123">Install the Azure CLI</span></span>
<span data-ttu-id="bd4f2-124">Azure CLI — это кроссплатформенное средство для работы с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="bd4f2-125">С его помощью можно подготавливать ресурсы для Azure и управлять ими непосредственно в командной строке.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-125">You work directly from your command line to provision and manage resources.</span></span> 

<span data-ttu-id="bd4f2-126">Чтобы установить последнюю версию Azure CLI, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bd4f2-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="bd4f2-127">Выполните следующие команды в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="bd4f2-128">Установка интерфейса командной строки Azure может занять около пяти минут.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="bd4f2-129">Выполните следующую команду, чтобы проверить установку:</span><span class="sxs-lookup"><span data-stu-id="bd4f2-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="bd4f2-130">Если установка прошла успешно, отобразятся следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-130">You should see the following output if the installation is successful.</span></span>

![Выходные данные, указывающие на успешное выполнение](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="bd4f2-132">Сводка</span><span class="sxs-lookup"><span data-stu-id="bd4f2-132">Summary</span></span>
<span data-ttu-id="bd4f2-133">Вы установили интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="bd4f2-134">Перейдите к следующей задаче: создайте Центр Интернета вещей Azure и удостоверение устройства с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="bd4f2-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd4f2-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bd4f2-135">Next steps</span></span>
<span data-ttu-id="bd4f2-136">[Создание Центра Интернета вещей и регистрация Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="bd4f2-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
