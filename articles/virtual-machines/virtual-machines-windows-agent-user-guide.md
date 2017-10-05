---
title: "Обзор агента виртуальной машины Azure | Документация Майкрософт"
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
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: accfd5f0fec69175e584528ff9f6db66402cb89e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="d9469-103">Обзор агента виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="d9469-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="d9469-104">Агент виртуальной машины Microsoft Azure — это защищенный упрощенный процесс, который управляет взаимодействием виртуальной машины с контроллером структуры Azure.</span><span class="sxs-lookup"><span data-stu-id="d9469-104">The Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="d9469-105">Основная роль агента виртуальной машины — это включение и выполнение расширений виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="d9469-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="d9469-106">Расширения виртуальной машины дают возможность выполнить дополнительные действия по настройке виртуальных машин после развертывания, например установить и настроить программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="d9469-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="d9469-107">Также они предоставляют возможности восстановления, такие как сброс пароля администратора виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d9469-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span></span> <span data-ttu-id="d9469-108">Расширения виртуальной машины не могут выполняться без агента виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="d9469-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="d9469-109">В этом документе описаны процессы установки, обнаружения и удаления агента виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="d9469-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span></span>

## <a name="install-the-vm-agent"></a><span data-ttu-id="d9469-110">"Установить агент виртуальной машины"</span><span class="sxs-lookup"><span data-stu-id="d9469-110">Install the VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="d9469-111">Образ из коллекции Azure</span><span class="sxs-lookup"><span data-stu-id="d9469-111">Azure gallery image</span></span>

<span data-ttu-id="d9469-112">По умолчанию агент виртуальной машины Azure устанавливается на любой виртуальной машине Windows, развернутой с помощью образа из коллекции Azure.</span><span class="sxs-lookup"><span data-stu-id="d9469-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="d9469-113">При развертывании образа из коллекции Azure с помощью портала, PowerShell, интерфейса командной строки или шаблона Azure Resource Manager также устанавливается агент виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d9469-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="d9469-114">Ручная установка</span><span class="sxs-lookup"><span data-stu-id="d9469-114">Manual installation</span></span>

<span data-ttu-id="d9469-115">Агент виртуальной машины Windows можно установить вручную с помощью пакета установщика Windows.</span><span class="sxs-lookup"><span data-stu-id="d9469-115">The Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="d9469-116">Ручная установка может потребоваться при создании пользовательского образа виртуальной машины, который будет развернут в Azure.</span><span class="sxs-lookup"><span data-stu-id="d9469-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="d9469-117">Чтобы установить агент виртуальной машины Windows вручную, скачайте установщик агента виртуальной машины из этого расположения: [Скачать агент виртуальной машины Azure для Windows](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="d9469-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="d9469-118">Чтобы установить агент виртуальной машины, дважды щелкните файл установщика Windows.</span><span class="sxs-lookup"><span data-stu-id="d9469-118">The VM Agent can be installed by double-clicking the windows installer file.</span></span> <span data-ttu-id="d9469-119">Для автоматической установки агента виртуальной машины выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d9469-119">For an automated or unattended installation of the VM agent, run the following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-the-vm-agent"></a><span data-ttu-id="d9469-120">Обнаружение агента виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d9469-120">Detect the VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="d9469-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9469-121">PowerShell</span></span>

<span data-ttu-id="d9469-122">Для получения сведений о виртуальных машинах Azure можно воспользоваться модулем PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d9469-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="d9469-123">Выполнение команды `Get-AzureRmVM` возвращает довольно много сведений, включая состояние подготовки для агента виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="d9469-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="d9469-124">Ниже приводится только часть выходных данных `Get-AzureRmVM`.</span><span class="sxs-lookup"><span data-stu-id="d9469-124">The following is just a subset of the `Get-AzureRmVM` output.</span></span> <span data-ttu-id="d9469-125">Обратите внимание на свойство `ProvisionVMAgent`, входящее в `OSProfile`. Это свойство можно использовать, чтобы определить, развернут ли на виртуальной машине агент виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d9469-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="d9469-126">Следующий сценарий можно использовать для получения краткого списка имен виртуальных машин и состояния агента виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d9469-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="d9469-127">Обнаружение вручную</span><span class="sxs-lookup"><span data-stu-id="d9469-127">Manual Detection</span></span>

<span data-ttu-id="d9469-128">После входа в виртуальную машину Azure под управлением Windows для проверки запущенных процессов можно использовать диспетчер задач.</span><span class="sxs-lookup"><span data-stu-id="d9469-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span></span> <span data-ttu-id="d9469-129">Чтобы проверить состояние агента виртуальной машины Azure, откройте диспетчер задач, перейдите на вкладку "Подробности" и найдите процесс с именем `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="d9469-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="d9469-130">Наличие этого процесса означает, что агент виртуальной машины установлен.</span><span class="sxs-lookup"><span data-stu-id="d9469-130">The presence of this process indicates that the VM agent is installed.</span></span>

## <a name="upgrade-the-vm-agent"></a><span data-ttu-id="d9469-131">Установка агента виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d9469-131">Upgrade the VM Agent</span></span>

<span data-ttu-id="d9469-132">Агент виртуальной машины Azure для Windows обновляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="d9469-132">The Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="d9469-133">Так как новые виртуальные машины развертываются в Azure, на них устанавливается последняя версия агента виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d9469-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span></span> <span data-ttu-id="d9469-134">Чтобы на пользовательских образах виртуальных машин была новая версия агента виртуальной машины, их необходимо обновлять вручную.</span><span class="sxs-lookup"><span data-stu-id="d9469-134">Custom VM images should be manually updated to include the new VM agent.</span></span>