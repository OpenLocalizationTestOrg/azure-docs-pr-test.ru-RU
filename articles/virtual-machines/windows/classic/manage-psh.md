---
title: "aaaManage виртуальные машины с помощью Azure PowerShell | Документы Microsoft"
description: "Дополнительные команды, которые можно использовать задачи tooautomate в управлении виртуальными машинами."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="51833-103">Управление виртуальными машинами с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="51833-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="51833-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="51833-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="51833-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="51833-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="51833-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="51833-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="51833-107">Стандартные команды PowerShell с помощью модели hello диспетчера ресурсов, в разделе [здесь](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51833-107">For common PowerShell commands using hello Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="51833-108">С помощью командлетов Azure PowerShell можно автоматизировать многие задачи, выполните каждый день toomanage виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="51833-108">Many tasks you do each day toomanage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="51833-109">В этой статье приводятся примеры команд для более простые задачи и tooarticles ссылок, отображение hello команд для более сложных задач.</span><span class="sxs-lookup"><span data-stu-id="51833-109">This article gives you example commands for simpler tasks, and links tooarticles that show hello commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="51833-110">Если вы еще не установлен и настроен Azure PowerShell, но инструкции можно получить в статье hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="51833-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-toouse-hello-example-commands"></a><span data-ttu-id="51833-111">Как toouse hello примеры команд</span><span class="sxs-lookup"><span data-stu-id="51833-111">How toouse hello example commands</span></span>
<span data-ttu-id="51833-112">Вам потребуется tooreplace некоторые из текста hello в hello команды с текстом, который подходит для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="51833-112">You'll need tooreplace some of hello text in hello commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="51833-113">Hello < и > символы указывают текст, необходимо tooreplace.</span><span class="sxs-lookup"><span data-stu-id="51833-113">hello < and > symbols indicate text you need tooreplace.</span></span> <span data-ttu-id="51833-114">При замене текста hello, удалите символы hello, но hello кавычки следует оставить на месте.</span><span class="sxs-lookup"><span data-stu-id="51833-114">When you replace hello text, remove hello symbols but leave hello quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="51833-115">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="51833-115">Get a VM</span></span>
<span data-ttu-id="51833-116">Вы будете выполнять эту основную задачу очень часто.</span><span class="sxs-lookup"><span data-stu-id="51833-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="51833-117">Использовать tooget сведения о виртуальной Машине, выполнять задачи на виртуальной Машине или получить toostore выходные данные в переменной.</span><span class="sxs-lookup"><span data-stu-id="51833-117">Use it tooget information about a VM, perform tasks on a VM, or get output toostore in a variable.</span></span>

<span data-ttu-id="51833-118">tooget сведения о hello виртуальной Машины, выполните следующую команду, заменив все, что заключено в кавычки hello, включая hello < и > символов:</span><span class="sxs-lookup"><span data-stu-id="51833-118">tooget information about hello VM, run this command, replacing everything in hello quotes, including hello < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="51833-119">выходные данные в переменной $vm hello toostore выполните:</span><span class="sxs-lookup"><span data-stu-id="51833-119">toostore hello output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a><span data-ttu-id="51833-120">Войдите на tooa виртуальной Машины на основе Windows</span><span class="sxs-lookup"><span data-stu-id="51833-120">Log on tooa Windows-based VM</span></span>
<span data-ttu-id="51833-121">Выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="51833-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="51833-122">Hello виртуальной машины и имя облачной службы можно получить из отображения hello hello **Get-AzureVM** команды.</span><span class="sxs-lookup"><span data-stu-id="51833-122">You can get hello virtual machine and cloud service name from hello display of hello **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="51833-123">$svcName = "<cloud service name>» $vmName ="<virtual machine name>» $localPath = «< диск и папку расположения toostore hello загрузить RDP-файл, пример: c:\temp >» $localFile = $localPath + "\" + $vmname + «.rdp» Get-AzureRemoteDesktopFile - ServiceName $svcName-имя $vmName - LocalPath $localFile-запуск</span><span class="sxs-lookup"><span data-stu-id="51833-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location toostore hello downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="51833-124">Остановка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="51833-124">Stop a VM</span></span>
<span data-ttu-id="51833-125">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="51833-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="51833-126">Использовать этот параметр tookeep hello, виртуальный IP-адрес (VIP) hello облачных служб в случае hello последняя виртуальная машина в указанной облачной службе.</span><span class="sxs-lookup"><span data-stu-id="51833-126">Use this parameter tookeep hello virtual IP (VIP) of hello cloud service in case it's hello last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="51833-127">При использовании параметра StayProvisioned hello, вам будет выставляться за hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="51833-127">If you use hello StayProvisioned parameter, you'll still be billed for hello VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="51833-128">Запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="51833-128">Start a VM</span></span>
<span data-ttu-id="51833-129">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="51833-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="51833-130">Присоединение диска данных</span><span class="sxs-lookup"><span data-stu-id="51833-130">Attach a data disk</span></span>
<span data-ttu-id="51833-131">Для этой задачи требуется несколько шагов.</span><span class="sxs-lookup"><span data-stu-id="51833-131">This task requires a few steps.</span></span> <span data-ttu-id="51833-132">Во-первых, используйте hello *** Add-AzureDataDisk *** командлет tooadd hello toohello $vm объект диска.</span><span class="sxs-lookup"><span data-stu-id="51833-132">First, you use hello ****Add-AzureDataDisk**** cmdlet tooadd hello disk toohello $vm object.</span></span> <span data-ttu-id="51833-133">Затем можно с помощью **Update-AzureVM** командлет tooupdate hello конфигурацию hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="51833-133">Then, you use **Update-AzureVM** cmdlet tooupdate hello configuration of hello VM.</span></span>

<span data-ttu-id="51833-134">Кроме того, потребуется toodecide tooattach новый диск или один, содержит ли данные.</span><span class="sxs-lookup"><span data-stu-id="51833-134">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="51833-135">Для нового диска hello команда создает hello VHD-файл и присоединяет его.</span><span class="sxs-lookup"><span data-stu-id="51833-135">For a new disk, hello command creates hello .vhd file and attaches it.</span></span>

<span data-ttu-id="51833-136">tooattach новый диск, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="51833-136">tooattach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="51833-137">tooattach существующий диск данных, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="51833-137">tooattach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="51833-138">tooattach диски с данными из существующего файла VHD в хранилище больших двоичных объектов, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="51833-138">tooattach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="51833-139">Создание виртуальной машины под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="51833-139">Create a Windows-based VM</span></span>
<span data-ttu-id="51833-140">новый на основе Windows виртуальной машины в Azure, используйте инструкции hello в toocreate [toocreate использовать Azure PowerShell и предварительной настройки виртуальных машин на основе Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="51833-140">toocreate a new Windows-based virtual machine in Azure, use hello instructions in [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="51833-141">Этот раздел действия можно выполнить с помощью Azure PowerShell, набор команд, создание hello создает к виртуальной Машине под управлением Windows, могут быть предварительно настроены:</span><span class="sxs-lookup"><span data-stu-id="51833-141">This topic steps you through hello creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="51833-142">членство в домене Active Directory;</span><span class="sxs-lookup"><span data-stu-id="51833-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="51833-143">дополнительные диски;</span><span class="sxs-lookup"><span data-stu-id="51833-143">With additional disks.</span></span>
* <span data-ttu-id="51833-144">членство в существующем наборе балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="51833-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="51833-145">статический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="51833-145">With a static IP address.</span></span>

