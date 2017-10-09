---
title: "Общие сведения об агенте виртуальной машины aaaAzure | Документы Microsoft"
description: "Обзор агента виртуальной машины Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: nepeters
ms.openlocfilehash: b03542b9a9c711000fab18ed82e9b17ee5510bbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="c284f-103">Обзор агента виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="c284f-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="c284f-104">Hello агент виртуальной машины Microsoft Azure (агент AM) является защищенным, простое процессом, который управляет взаимодействием виртуальной Машины с hello Azure Fabric Controller.</span><span class="sxs-lookup"><span data-stu-id="c284f-104">hello Microsoft Azure Virtual Machine Agent (AM Agent) is a secured, lightweight process that manages VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="c284f-105">Hello агент виртуальной Машины имеет основной роли в Включение и выполнении расширения виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="c284f-105">hello VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="c284f-106">Расширения виртуальной машины дают возможность выполнить дополнительные действия по настройке виртуальных машин после развертывания, например установить и настроить программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="c284f-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="c284f-107">Расширения виртуальных машин также включение функции восстановления, например, сбросить пароль администратора hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c284f-107">Virtual machine extensions also enable recovery features such as resetting hello administrative password of a virtual machine.</span></span> <span data-ttu-id="c284f-108">Без hello агента ВМ Azure невозможно запустить расширения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c284f-108">Without hello Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="c284f-109">В этом документе описаны установки, обнаружения и удаления hello агент виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="c284f-109">This document details installation, detection, and removal of hello Azure Virtual Machine Agent.</span></span>

## <a name="install-hello-vm-agent"></a><span data-ttu-id="c284f-110">Установить агент ВМ hello</span><span class="sxs-lookup"><span data-stu-id="c284f-110">Install hello VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="c284f-111">Образ из коллекции Azure</span><span class="sxs-lookup"><span data-stu-id="c284f-111">Azure gallery image</span></span>

<span data-ttu-id="c284f-112">Hello агента ВМ Azure устанавливается по умолчанию на любой виртуальной машине Windows, развернутых из образа Azure коллекции.</span><span class="sxs-lookup"><span data-stu-id="c284f-112">hello Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="c284f-113">При развертывании образа Azure коллекции из hello портала, PowerShell, интерфейс командной строки или шаблонов диспетчера ресурсов Azure, установить приветствия также является агента ВМ Azure.</span><span class="sxs-lookup"><span data-stu-id="c284f-113">When deploying an Azure gallery image from hello Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, hello Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="c284f-114">Ручная установка</span><span class="sxs-lookup"><span data-stu-id="c284f-114">Manual installation</span></span>

<span data-ttu-id="c284f-115">агент виртуальной Машины Windows Hello можно установить вручную с помощью пакета установщика Windows.</span><span class="sxs-lookup"><span data-stu-id="c284f-115">hello Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="c284f-116">Ручная установка может потребоваться при создании пользовательского образа виртуальной машины, который будет развернут в Azure.</span><span class="sxs-lookup"><span data-stu-id="c284f-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="c284f-117">hello toomanually установки агента виртуальной Машины Windows, загрузка установщика агента ВМ hello из этого расположения [загрузки агента ВМ Windows Azure](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="c284f-117">toomanually install hello Windows VM Agent, download hello VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="c284f-118">Hello агент виртуальной Машины можно установить, дважды щелкнув файл установщика windows hello.</span><span class="sxs-lookup"><span data-stu-id="c284f-118">hello VM Agent can be installed by double-clicking hello windows installer file.</span></span> <span data-ttu-id="c284f-119">Для автоматической или автоматической установки агента ВМ hello выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="c284f-119">For an automated or unattended installation of hello VM agent, run hello following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a><span data-ttu-id="c284f-120">Обнаружить hello агент виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="c284f-120">Detect hello VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="c284f-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c284f-121">PowerShell</span></span>

<span data-ttu-id="c284f-122">модуль PowerShell диспетчера ресурсов Azure Hello можно использовать tooretrieve сведения о виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="c284f-122">hello Azure Resource Manager PowerShell module can be used tooretrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="c284f-123">Под управлением `Get-AzureRmVM` возвращает довольно много информации, включая состояние для hello агента ВМ Azure подготовки hello.</span><span class="sxs-lookup"><span data-stu-id="c284f-123">Running `Get-AzureRmVM` returns quite a bit of information including hello provisioning state for hello Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="c284f-124">Hello ниже приведен только подмножество hello `Get-AzureRmVM` выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c284f-124">hello following is just a subset of hello `Get-AzureRmVM` output.</span></span> <span data-ttu-id="c284f-125">Обратите внимание hello `ProvisionVMAgent` свойство вложено в `OSProfile`, это свойство может быть toodetermine используется, если агент виртуальной Машины hello было toohello развернутой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c284f-125">Notice hello `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used toodetermine if hello VM agent has been deployed toohello virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="c284f-126">Привет, выполнив сценарий может быть используется tooreturn краткий список имен виртуальных машин и состояние hello hello агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c284f-126">hello following script can be used tooreturn a concise list of virtual machine names and hello state of hello VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="c284f-127">Обнаружение вручную</span><span class="sxs-lookup"><span data-stu-id="c284f-127">Manual Detection</span></span>

<span data-ttu-id="c284f-128">При регистрации в tooa виртуальной Машине Windows Azure, диспетчер задач может быть используется tooexamine запущенных процессов.</span><span class="sxs-lookup"><span data-stu-id="c284f-128">When logged in tooa Windows Azure VM, task manager can be used tooexamine running processes.</span></span> <span data-ttu-id="c284f-129">toocheck для hello агента ВМ Azure, откройте диспетчер задач > вкладку подробности hello и найдите имя процесса `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="c284f-129">toocheck for hello Azure VM Agent, open Task Manager > click hello details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="c284f-130">Присутствие этого процесса Hello указывает, что установлен агент ВМ, hello.</span><span class="sxs-lookup"><span data-stu-id="c284f-130">hello presence of this process indicates that hello VM agent is installed.</span></span>

## <a name="upgrade-hello-vm-agent"></a><span data-ttu-id="c284f-131">Обновление hello агент виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="c284f-131">Upgrade hello VM Agent</span></span>

<span data-ttu-id="c284f-132">Hello Azure VM агент для Windows обновляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="c284f-132">hello Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="c284f-133">Как новые виртуальные машины в развернутой tooAzure, они получают последнюю версию агента ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="c284f-133">As new virtual machines are deployed tooAzure, they receive hello latest VM agent.</span></span> <span data-ttu-id="c284f-134">Пользовательские образы виртуальных Машин следует вручную, добавив новые tooinclude hello новый агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c284f-134">Custom VM images should be manually updated tooinclude hello new VM agent.</span></span>
