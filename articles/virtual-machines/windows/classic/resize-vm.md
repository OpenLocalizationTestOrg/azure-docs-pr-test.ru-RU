---
title: "Изменение размера виртуальной машины Windows в классической модели развертывания Azure | Документация Майкрософт"
description: "Изменение размера виртуальной машины Windows, созданной в классической модели развертывания, с использованием Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 4277bc8394c7ba140291e9dc776162e87deab96b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-windows-vm-created-in-the-classic-deployment-model"></a><span data-ttu-id="ed6ec-103">Изменение размера виртуальной машины Windows, созданной в классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="ed6ec-103">Resize a Windows VM created in the classic deployment model</span></span>
<span data-ttu-id="ed6ec-104">В этой статье описано изменение размера виртуальной машины Windows, созданной в классической модели развертывания, с использованием Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-104">This article shows you how to resize a Windows VM, created in the classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="ed6ec-105">Собираясь изменять размер виртуальной машины, обратите внимание на два фактора, которые определяют диапазон размеров, доступных для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-105">When considering the ability to resize a VM, there are two concepts which control the range of sizes available to resize the virtual machine.</span></span> <span data-ttu-id="ed6ec-106">Первый фактор — регион, в котором развернута виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-106">The first concept is the region in which your VM is deployed.</span></span> <span data-ttu-id="ed6ec-107">Список размеров виртуальных машин, доступных в регионе, находится на вкладке "Службы" веб-страницы "Регионы Azure".</span><span class="sxs-lookup"><span data-stu-id="ed6ec-107">The list of VM sizes available in region is under the Services tab of the Azure Regions web page.</span></span> <span data-ttu-id="ed6ec-108">Второй фактор — физическое оборудование, на котором размещена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-108">The second concept is the physical hardware currently hosting your VM.</span></span> <span data-ttu-id="ed6ec-109">Физические серверы, на которых размещены виртуальные машины, группируются в кластеры общего физического оборудования.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-109">The physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="ed6ec-110">Метод изменения размера виртуальной машины зависит от того, поддерживает ли оборудование кластера, в котором размещена виртуальная машина, новый размер.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-110">The method of changing a VM size differs depending on if the desired new VM size is supported by the hardware cluster currently hosting the VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ed6ec-111">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ed6ec-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ed6ec-112">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-112">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ed6ec-113">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-113">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ed6ec-114">Кроме того, можно [изменить размер виртуальной машины, созданной с использованием модели развертывания на основе Resource Manager](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed6ec-114">You can also [resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="ed6ec-115">Добавление учетной записи</span><span class="sxs-lookup"><span data-stu-id="ed6ec-115">Add your account</span></span>
<span data-ttu-id="ed6ec-116">Для работы с классическими ресурсами Azure необходимо настроить Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-116">You must configure Azure PowerShell to work with classic Azure resources.</span></span> <span data-ttu-id="ed6ec-117">Выполните следующие действия, чтобы настроить Azure PowerShell для управления классическими ресурсами.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-117">Follow the steps below to configure Azure PowerShell to manage classic resources.</span></span>

1. <span data-ttu-id="ed6ec-118">В командной строке PowerShell введите `Add-AzureAccount` и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-118">At the PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="ed6ec-119">Введите адрес электронной почты, связанный с подпиской Azure, и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-119">Type in the email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="ed6ec-120">Введите пароль к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-120">Type in the password for your account.</span></span> 
4. <span data-ttu-id="ed6ec-121">Щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-121">Click **Sign in**.</span></span> 

## <a name="resize-in-the-same-hardware-cluster"></a><span data-ttu-id="ed6ec-122">Изменение размеров в том же кластере оборудования</span><span class="sxs-lookup"><span data-stu-id="ed6ec-122">Resize in the same hardware cluster</span></span>
<span data-ttu-id="ed6ec-123">Чтобы изменить размер виртуальной машины до размера, доступного в кластере оборудования, в котором размещена машина, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-123">To resize a VM to a size available in the hardware cluster hosting the VM, perform the following steps.</span></span>

1. <span data-ttu-id="ed6ec-124">Выполните следующую команду PowerShell, чтобы получить список размеров виртуальных машин, доступных в оборудовании кластера облачной службы, в которой находится машина.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-124">Run the following PowerShell command to list the VM sizes available in the hardware cluster hosting the cloud service which contains the VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="ed6ec-125">Выполните следующие команды, чтобы изменить размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-125">Run the following commands to resize the VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="ed6ec-126">Изменение размера в новом кластере оборудования</span><span class="sxs-lookup"><span data-stu-id="ed6ec-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="ed6ec-127">Для изменения размера виртуальной машины до размера, недоступного в оборудовании кластера, в котором размещена эта виртуальная машина, необходимо заново создать облачную службу и все виртуальные машины в ней.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-127">To resize a VM to a size not available in the hardware cluster hosting the VM, the cloud service and all VMs in the cloud service must be recreated.</span></span> <span data-ttu-id="ed6ec-128">Каждая облачная служба размещается в одном кластере оборудования, поэтому все виртуальные машины в облачной службе должны иметь размер, поддерживаемый этим кластером.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-128">Each cloud service is hosted on a single hardware cluster so all VMs in the cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="ed6ec-129">Ниже описано изменение размера виртуальной машины путем удаления и повторного создания облачной службы.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-129">The following steps will describe how to resize a VM by deleting and then recreating the cloud service.</span></span>

1. <span data-ttu-id="ed6ec-130">Выполните следующую команду PowerShell, чтобы получить список размеров виртуальных машин, доступных в регионе.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-130">Run the following PowerShell command to list the VM sizes available in the region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="ed6ec-131">Зафиксируйте все параметры каждой виртуальной машины в облачной службе, содержащей виртуальную машину, размер которой необходимо изменить.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-131">Make note of all configuration settings for each VM in the cloud service which contains the VM to be resized.</span></span> 
3. <span data-ttu-id="ed6ec-132">Удалите все виртуальные машины в облачной службе, выбрав параметр сохранения дисков для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-132">Delete all VMs in the cloud service selecting the option to retain the disks for each VM.</span></span>
4. <span data-ttu-id="ed6ec-133">Повторно создайте виртуальную машину, размер которой следует изменить, указав необходимый размер машины.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-133">Recreate the VM to be resized using the desired VM size.</span></span>
5. <span data-ttu-id="ed6ec-134">Заново создайте все остальные виртуальные машины, которые были в облачной службе. При этом укажите размер виртуальной машины, доступный в кластере оборудования, в котором теперь размещается облачная служба.</span><span class="sxs-lookup"><span data-stu-id="ed6ec-134">Recreate all other VMs which were in the cloud service using a VM size available in the hardware cluster now hosting the cloud service.</span></span>

<span data-ttu-id="ed6ec-135">Пример сценария для удаления и повторного создания облачной службы с использованием нового размера виртуальной машины можно найти [здесь](https://github.com/Azure/azure-vm-scripts).</span><span class="sxs-lookup"><span data-stu-id="ed6ec-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ed6ec-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ed6ec-136">Next steps</span></span>
* <span data-ttu-id="ed6ec-137">[Resize a Windows VM](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Изменение размера виртуальной машины Windows).</span><span class="sxs-lookup"><span data-stu-id="ed6ec-137">[Resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

