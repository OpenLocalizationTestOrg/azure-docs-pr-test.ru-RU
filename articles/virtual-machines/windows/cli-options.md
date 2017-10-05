---
title: "Использование Azure CLI в Windows | Документация Майкрософт"
description: "Использование Azure CLI в Windows"
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
ms.openlocfilehash: be02ad0d7752cb08f092deeb5a86dcd126403237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-on-windows"></a><span data-ttu-id="7a9ee-103">Использование Azure CLI в Windows</span><span class="sxs-lookup"><span data-stu-id="7a9ee-103">Using the Azure CLI on Windows</span></span>

<span data-ttu-id="7a9ee-104">Интерфейс командной строки Azure (CLI) представляет собой интерфейс командной строки и среду скриптов для создания ресурсов Azure и управления ими.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-104">The Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="7a9ee-105">Azure CLI доступен для операционных систем macOS, Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-105">The Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="7a9ee-106">Для этих операционных систем команды CLI идентичны. Однако синтаксис конкретного скрипта операционной системы может отличаться.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-106">Across these operating systems, the CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="7a9ee-107">В этом документе представлены сведения об установке Azure CLI и его запуске в Windows, а также сведения о синтаксисе для каждого сценария.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-107">This document details the ways that the Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="7a9ee-108">Подробную документацию по Azure CLI см. [здесь]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7a9ee-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="7a9ee-109">Подсистема Windows для Linux</span><span class="sxs-lookup"><span data-stu-id="7a9ee-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="7a9ee-110">Подсистема Windows для Linux предоставляет среду Ubuntu Linux для юбилейного выпуска Windows 10 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-110">The Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="7a9ee-111">Включив подсистему Windows для Linux, вы можете воспользоваться Bash для создания и выполнения сценариев Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="7a9ee-112">Благодаря этой возможности сценарии Azure CLI можно использовать в macOS, Linux и Windows, не изменяя их.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="7a9ee-113">Чтобы использовать Azure CLI в подсистеме Windows для Linux, выполните следующие задания.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-113">To use the Azure CLI in WSL, complete the following.</span></span>

|<span data-ttu-id="7a9ee-114">Задача</span><span class="sxs-lookup"><span data-stu-id="7a9ee-114">Task</span></span> | <span data-ttu-id="7a9ee-115">Указания</span><span class="sxs-lookup"><span data-stu-id="7a9ee-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="7a9ee-116">Включение подсистемы Windows для Linux</span><span class="sxs-lookup"><span data-stu-id="7a9ee-116">Enable WSL</span></span> | [<span data-ttu-id="7a9ee-117">Документация по установке подсистемы Windows для Linux</span><span class="sxs-lookup"><span data-stu-id="7a9ee-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="7a9ee-118">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7a9ee-118">Install the Azure CLI</span></span> |<span data-ttu-id="7a9ee-119">[Install the CLI on WSL/Ubuntu 14.04](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu) (Установка интерфейса командной строки в подсистеме Windows для Linux или в Ubuntu 14.04)</span><span class="sxs-lookup"><span data-stu-id="7a9ee-119">[Install the CLI on WSL/Ubuntu 14.04](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)</span></span>|

## <a name="powershell"></a><span data-ttu-id="7a9ee-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a9ee-120">PowerShell</span></span>

<span data-ttu-id="7a9ee-121">Azure CLI можно запускать в собственном коде в Windows.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-121">The Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="7a9ee-122">В такой конфигурации пакет Azure CLI устанавливается в операционной системе Windows, а команды можно выполнять из PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-122">In this configuration, the Azure CLI package is installed on the Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="7a9ee-123">В такой конфигурации команды и скрипты Azure CLI можно выполнять в любой поддерживаемой версии Windows, но для этого потребуется синтаксис скрипта для конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="7a9ee-124">Поэтому сценарии не обязательно совместно использовать в macOS, Linux и Windows, не изменяя их.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="7a9ee-125">[Установите Azure CLI в Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows), следуя инструкциям, для использования Azure CLI в Windows.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-125">To use the Azure CLI on Windows, install the package using these instructions, [Install the CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="7a9ee-126">Образ Docker</span><span class="sxs-lookup"><span data-stu-id="7a9ee-126">Docker Image</span></span>

<span data-ttu-id="7a9ee-127">При использовании Docker для Windows можно запустить образ Docker, содержащий Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-127">When using Docker for Windows, a Docker image can be started that includes the Azure CLI.</span></span> <span data-ttu-id="7a9ee-128">Этот образ создан на основе Linux и позволяет работать с Bash.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="7a9ee-129">При использовании Docker для Windows и образа Azure CLI сценарии нужно совместно использовать в macOS, Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-129">When using Docker for Windows and the Azure CLI image, scripts to be shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="7a9ee-130">Чтобы использовать Azure CLI на основе Docker для Windows, убедитесь, что Docker для Windows работает, и выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-130">To use the Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run the following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="7a9ee-131">После завершения начнется сеанс Bash, в котором предварительно скачаны средства Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7a9ee-131">Once completed, a Bash session will start that is preloaded with the Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a9ee-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7a9ee-132">Next Steps</span></span>

[<span data-ttu-id="7a9ee-133">Примеры сценариев интерфейса командной строки для виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="7a9ee-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="7a9ee-134">Примеры сценариев интерфейса командной строки для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="7a9ee-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="7a9ee-135">Примеры сценариев интерфейса командной строки для SQL Azure</span><span class="sxs-lookup"><span data-stu-id="7a9ee-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
