---
title: "Управление виртуальными машинами с помощью Azure PowerShell | Документация Майкрософт"
description: "Узнайте о командах, которые можно использовать для автоматизации задач управления виртуальными машинами."
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
ms.openlocfilehash: fd2df7e1029ced11974d0b832258bed2cf3bbb27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="bd54c-103">Управление виртуальными машинами с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd54c-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="bd54c-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bd54c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bd54c-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="bd54c-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="bd54c-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bd54c-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="bd54c-107">Общие команды PowerShell, использующиеся с моделью Resource Manager, см. [здесь](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd54c-107">For common PowerShell commands using the Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="bd54c-108">Многие повседневные задачи управления виртуальными машинами можно автоматизировать с помощью командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd54c-108">Many tasks you do each day to manage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="bd54c-109">В этой статье приводятся примеры команд для простых задач, а также ссылки на статьи о командах для более сложных задач.</span><span class="sxs-lookup"><span data-stu-id="bd54c-109">This article gives you example commands for simpler tasks, and links to articles that show the commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="bd54c-110">Если вы еще не установили и не настроили Azure PowerShell, соответствующие указания см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bd54c-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in the article [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-to-use-the-example-commands"></a><span data-ttu-id="bd54c-111">Как использовать примеры команд</span><span class="sxs-lookup"><span data-stu-id="bd54c-111">How to use the example commands</span></span>
<span data-ttu-id="bd54c-112">Вам понадобится заменить определенный текст в командах в соответствии с вашей средой.</span><span class="sxs-lookup"><span data-stu-id="bd54c-112">You'll need to replace some of the text in the commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="bd54c-113">Знаки < и > обозначают текст, который необходимо заменить.</span><span class="sxs-lookup"><span data-stu-id="bd54c-113">The < and > symbols indicate text you need to replace.</span></span> <span data-ttu-id="bd54c-114">При замене текста удалите символы, но оставьте на месте кавычки.</span><span class="sxs-lookup"><span data-stu-id="bd54c-114">When you replace the text, remove the symbols but leave the quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="bd54c-115">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bd54c-115">Get a VM</span></span>
<span data-ttu-id="bd54c-116">Вы будете выполнять эту основную задачу очень часто.</span><span class="sxs-lookup"><span data-stu-id="bd54c-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="bd54c-117">Используйте ее, чтобы получить информацию о виртуальной машине, выполнить задачи в виртуальной машине или получить выходные данные, которые необходимо сохранить в переменной.</span><span class="sxs-lookup"><span data-stu-id="bd54c-117">Use it to get information about a VM, perform tasks on a VM, or get output to store in a variable.</span></span>

<span data-ttu-id="bd54c-118">Чтобы получить информацию о виртуальной машине, выполните эту команду и замените все, что заключено в кавычки, в том числе знаки < и >.</span><span class="sxs-lookup"><span data-stu-id="bd54c-118">To get information about the VM, run this command, replacing everything in the quotes, including the < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="bd54c-119">Чтобы сохранить выходные данные в переменной $vm, выполните:</span><span class="sxs-lookup"><span data-stu-id="bd54c-119">To store the output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-to-a-windows-based-vm"></a><span data-ttu-id="bd54c-120">Вход в виртуальную машину под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="bd54c-120">Log on to a Windows-based VM</span></span>
<span data-ttu-id="bd54c-121">Выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="bd54c-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="bd54c-122">Имя виртуальной машины и облачной службы можно получить из вывода команды **Get-AzureVM** .</span><span class="sxs-lookup"><span data-stu-id="bd54c-122">You can get the virtual machine and cloud service name from the display of the **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="bd54c-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<расположение диска и файла для хранения скачанного RDP-файла, например c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span><span class="sxs-lookup"><span data-stu-id="bd54c-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location to store the downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="bd54c-124">Остановка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bd54c-124">Stop a VM</span></span>
<span data-ttu-id="bd54c-125">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bd54c-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="bd54c-126">Используйте этот параметр, чтобы сохранить виртуальный IP-адрес (VIP) облачной службы, если эта виртуальная машина является последней в этой службе.</span><span class="sxs-lookup"><span data-stu-id="bd54c-126">Use this parameter to keep the virtual IP (VIP) of the cloud service in case it's the last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="bd54c-127">При использовании параметра StayProvisioned вам по-прежнему будут выставлять счета за использование виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bd54c-127">If you use the StayProvisioned parameter, you'll still be billed for the VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="bd54c-128">Запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bd54c-128">Start a VM</span></span>
<span data-ttu-id="bd54c-129">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bd54c-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="bd54c-130">Присоединение диска данных</span><span class="sxs-lookup"><span data-stu-id="bd54c-130">Attach a data disk</span></span>
<span data-ttu-id="bd54c-131">Для этой задачи требуется несколько шагов.</span><span class="sxs-lookup"><span data-stu-id="bd54c-131">This task requires a few steps.</span></span> <span data-ttu-id="bd54c-132">Сначала используйте командлет ****Add-AzureDataDisk**** , чтобы добавить диск в объект $vm.</span><span class="sxs-lookup"><span data-stu-id="bd54c-132">First, you use the ****Add-AzureDataDisk**** cmdlet to add the disk to the $vm object.</span></span> <span data-ttu-id="bd54c-133">Затем используйте командлет **Update-AzureVM** , чтобы обновить конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bd54c-133">Then, you use **Update-AzureVM** cmdlet to update the configuration of the VM.</span></span>

<span data-ttu-id="bd54c-134">Вам необходимо решить, какой диск подключать — новый диск или диск с данными.</span><span class="sxs-lookup"><span data-stu-id="bd54c-134">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="bd54c-135">При подключении нового диска команда создает и присоединяет VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="bd54c-135">For a new disk, the command creates the .vhd file and attaches it.</span></span>

<span data-ttu-id="bd54c-136">Чтобы подключить новый диск, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bd54c-136">To attach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="bd54c-137">Чтобы подключить существующий диск, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bd54c-137">To attach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="bd54c-138">Чтобы подключить диски данных из существующего VHD-файла в хранилище больших двоичных объектов, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bd54c-138">To attach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="bd54c-139">Создание виртуальной машины под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="bd54c-139">Create a Windows-based VM</span></span>
<span data-ttu-id="bd54c-140">Чтобы создать виртуальную машину под управлением Windows в Azure, используйте указания в статье [Использование Azure PowerShell для создания и предварительной настройки виртуальных машин под управлением Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bd54c-140">To create a new Windows-based virtual machine in Azure, use the instructions in [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="bd54c-141">В этом разделе последовательно описано создание набора команд Azure PowerShell, создающего виртуальную машину под управлением Windows, для которой можно предварительно настроить:</span><span class="sxs-lookup"><span data-stu-id="bd54c-141">This topic steps you through the creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="bd54c-142">членство в домене Active Directory;</span><span class="sxs-lookup"><span data-stu-id="bd54c-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="bd54c-143">дополнительные диски;</span><span class="sxs-lookup"><span data-stu-id="bd54c-143">With additional disks.</span></span>
* <span data-ttu-id="bd54c-144">членство в существующем наборе балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="bd54c-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="bd54c-145">статический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="bd54c-145">With a static IP address.</span></span>

