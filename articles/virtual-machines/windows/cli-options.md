---
title: "aaaUsing hello Azure CLI в Windows | Документы Microsoft"
description: "С помощью Azure CLI hello в Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a><span data-ttu-id="63954-103">С помощью Azure CLI hello в Windows</span><span class="sxs-lookup"><span data-stu-id="63954-103">Using hello Azure CLI on Windows</span></span>

<span data-ttu-id="63954-104">Hello Azure интерфейс командной строки (CLI) предоставляет командной строки и среда сценариев для создания и управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="63954-104">hello Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="63954-105">Hello Azure CLI доступна для операционных систем Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="63954-105">hello Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="63954-106">В этих операционных систем команды CLI hello идентичны, однако сценариев синтаксиса операционной системы может отличаться.</span><span class="sxs-lookup"><span data-stu-id="63954-106">Across these operating systems, hello CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="63954-107">Этот документ сведения hello что образом hello Azure CLI могут устанавливаться и работать на Windows и сведения о синтаксических рекомендации для каждого.</span><span class="sxs-lookup"><span data-stu-id="63954-107">This document details hello ways that hello Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="63954-108">Подробную документацию по Azure CLI см. [здесь]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="63954-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="63954-109">Подсистема Windows для Linux</span><span class="sxs-lookup"><span data-stu-id="63954-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="63954-110">Hello подсистемы Windows для Linux (WSL) предоставляет среду Ubuntu Linux на годовщины Windows 10 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="63954-110">hello Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="63954-111">Включив подсистему Windows для Linux, вы можете воспользоваться Bash для создания и выполнения сценариев Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="63954-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="63954-112">Благодаря этой возможности сценарии Azure CLI можно использовать в macOS, Linux и Windows, не изменяя их.</span><span class="sxs-lookup"><span data-stu-id="63954-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="63954-113">toouse hello Azure CLI в WSL, выполните следующие hello.</span><span class="sxs-lookup"><span data-stu-id="63954-113">toouse hello Azure CLI in WSL, complete hello following.</span></span>

|<span data-ttu-id="63954-114">Задача</span><span class="sxs-lookup"><span data-stu-id="63954-114">Task</span></span> | <span data-ttu-id="63954-115">Указания</span><span class="sxs-lookup"><span data-stu-id="63954-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="63954-116">Включение подсистемы Windows для Linux</span><span class="sxs-lookup"><span data-stu-id="63954-116">Enable WSL</span></span> | [<span data-ttu-id="63954-117">Документация по установке подсистемы Windows для Linux</span><span class="sxs-lookup"><span data-stu-id="63954-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="63954-118">Установка hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="63954-118">Install hello Azure CLI</span></span> |[<span data-ttu-id="63954-119">Установите на WSL/Ubuntu 14.04 hello CLI</span><span class="sxs-lookup"><span data-stu-id="63954-119">Install hello CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="63954-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="63954-120">PowerShell</span></span>

<span data-ttu-id="63954-121">Hello Azure CLI могут выполняться в собственном коде в Windows.</span><span class="sxs-lookup"><span data-stu-id="63954-121">hello Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="63954-122">В этой конфигурации hello Azure CLI пакет установлен в операционной системе Windows hello и команды, которые могут быть запущены из PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63954-122">In this configuration, hello Azure CLI package is installed on hello Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="63954-123">В такой конфигурации команды и скрипты Azure CLI можно выполнять в любой поддерживаемой версии Windows, но для этого потребуется синтаксис скрипта для конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="63954-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="63954-124">Поэтому сценарии не обязательно совместно использовать в macOS, Linux и Windows, не изменяя их.</span><span class="sxs-lookup"><span data-stu-id="63954-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="63954-125">toouse hello Azure CLI в Windows, установите пакет hello, с помощью следующей процедуры [hello установить CLI в Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="63954-125">toouse hello Azure CLI on Windows, install hello package using these instructions, [Install hello CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="63954-126">Образ Docker</span><span class="sxs-lookup"><span data-stu-id="63954-126">Docker Image</span></span>

<span data-ttu-id="63954-127">При использовании Docker для Windows, образ Docker можно запустить, включающий hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="63954-127">When using Docker for Windows, a Docker image can be started that includes hello Azure CLI.</span></span> <span data-ttu-id="63954-128">Этот образ создан на основе Linux и позволяет работать с Bash.</span><span class="sxs-lookup"><span data-stu-id="63954-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="63954-129">При использовании Docker для Windows и hello Azure CLI изображения, toobe сценарии общим macOS, Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="63954-129">When using Docker for Windows and hello Azure CLI image, scripts toobe shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="63954-130">toouse hello Azure CLI в Docker для Windows, убедитесь, что Docker для Windows работает и запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="63954-130">toouse hello Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run hello following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="63954-131">После завершения с помощью средств Azure CLI hello предварительно Bash, то есть начала сеанса.</span><span class="sxs-lookup"><span data-stu-id="63954-131">Once completed, a Bash session will start that is preloaded with hello Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63954-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63954-132">Next Steps</span></span>

[<span data-ttu-id="63954-133">Примеры сценариев интерфейса командной строки для виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="63954-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="63954-134">Примеры сценариев интерфейса командной строки для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="63954-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="63954-135">Примеры сценариев интерфейса командной строки для SQL Azure</span><span class="sxs-lookup"><span data-stu-id="63954-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
