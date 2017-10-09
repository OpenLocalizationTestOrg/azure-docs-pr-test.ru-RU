---
title: "aaaResize виртуальной Машины Windows в hello классической модели развертывания - Azure | Документы Microsoft"
description: "Измените размер виртуальной машины Windows, созданных в hello классической модели развертывания, с помощью Azure Powershell."
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
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a><span data-ttu-id="f4ad6-103">Изменение размера виртуальной Машины Windows, созданных в hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="f4ad6-103">Resize a Windows VM created in hello classic deployment model</span></span>
<span data-ttu-id="f4ad6-104">В этой статье показано, как tooresize ВМ Windows, созданные в hello классической модели развертывания с помощью Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-104">This article shows you how tooresize a Windows VM, created in hello classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="f4ad6-105">При рассмотрении возможности tooresize hello виртуальной Машины, существует два понятия, которые управляют hello диапазон размеров доступных tooresize hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-105">When considering hello ability tooresize a VM, there are two concepts which control hello range of sizes available tooresize hello virtual machine.</span></span> <span data-ttu-id="f4ad6-106">Первое базовое понятие Hello — hello регион, в котором развернута ВМ.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-106">hello first concept is hello region in which your VM is deployed.</span></span> <span data-ttu-id="f4ad6-107">Список доступных размеров виртуальных Машин в регионе Hello находится под hello вкладку "службы" Привет регионы Azure веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-107">hello list of VM sizes available in region is under hello Services tab of hello Azure Regions web page.</span></span> <span data-ttu-id="f4ad6-108">Концепция второй Hello является hello физического оборудования, в настоящее время размещения виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-108">hello second concept is hello physical hardware currently hosting your VM.</span></span> <span data-ttu-id="f4ad6-109">физические серверы Hello размещение виртуальных машин группируются в кластеры общих физического оборудования.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-109">hello physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="f4ad6-110">метод Hello изменение размера виртуальной Машины отличается в зависимости от того, если hello желательный размер новой виртуальной Машины поддерживается hello оборудования кластера в настоящее время размещается hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-110">hello method of changing a VM size differs depending on if hello desired new VM size is supported by hello hardware cluster currently hosting hello VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f4ad6-111">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f4ad6-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f4ad6-112">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-112">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f4ad6-113">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f4ad6-114">Вы также можете [изменения размера виртуальных Машин, созданных в модели развертывания диспетчера ресурсов hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f4ad6-114">You can also [resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="f4ad6-115">Добавление учетной записи</span><span class="sxs-lookup"><span data-stu-id="f4ad6-115">Add your account</span></span>
<span data-ttu-id="f4ad6-116">Необходимо настроить Azure PowerShell toowork классические ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-116">You must configure Azure PowerShell toowork with classic Azure resources.</span></span> <span data-ttu-id="f4ad6-117">Выполните действия hello ниже tooconfigure Azure PowerShell toomanage классические ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-117">Follow hello steps below tooconfigure Azure PowerShell toomanage classic resources.</span></span>

1. <span data-ttu-id="f4ad6-118">Введите в командной строке PowerShell hello `Add-AzureAccount` и нажмите кнопку **ввод**.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-118">At hello PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="f4ad6-119">Введите адрес электронной почты hello, связанных с подпиской Azure и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="f4ad6-120">Введите в hello пароль своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="f4ad6-121">Щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-121">Click **Sign in**.</span></span> 

## <a name="resize-in-hello-same-hardware-cluster"></a><span data-ttu-id="f4ad6-122">Изменение размеров в hello же оборудования кластера</span><span class="sxs-lookup"><span data-stu-id="f4ad6-122">Resize in hello same hardware cluster</span></span>
<span data-ttu-id="f4ad6-123">tooresize tooa размер виртуальной Машины, доступных в кластере оборудования hello размещение hello виртуальной Машины, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-123">tooresize a VM tooa size available in hello hardware cluster hosting hello VM, perform hello following steps.</span></span>

1. <span data-ttu-id="f4ad6-124">Выполните следующую команду PowerShell, что в кластере оборудования hello размещение hello облачную службу, которая содержит размеры виртуальных Машин hello toolist hello виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-124">Run hello following PowerShell command toolist hello VM sizes available in hello hardware cluster hosting hello cloud service which contains hello VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="f4ad6-125">Выполните следующие команды tooresize hello ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-125">Run hello following commands tooresize hello VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="f4ad6-126">Изменение размера в новом кластере оборудования</span><span class="sxs-lookup"><span data-stu-id="f4ad6-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="f4ad6-127">tooresize tooa размер виртуальной Машины, недоступен в hello оборудования кластера размещения Здравствуйте виртуальной Машины, hello облачную службу и все виртуальные машины в облачной службе hello должны быть созданы заново.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-127">tooresize a VM tooa size not available in hello hardware cluster hosting hello VM, hello cloud service and all VMs in hello cloud service must be recreated.</span></span> <span data-ttu-id="f4ad6-128">Каждая облачная служба размещается в кластере один аппаратный поэтому все виртуальные машины в облачной службе hello должно иметь размер, который поддерживается в кластере оборудования.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-128">Each cloud service is hosted on a single hardware cluster so all VMs in hello cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="f4ad6-129">Hello Далее будет описывается, как tooresize к виртуальной Машине по удалению и повторному созданию затем hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-129">hello following steps will describe how tooresize a VM by deleting and then recreating hello cloud service.</span></span>

1. <span data-ttu-id="f4ad6-130">Запустите следующие PowerShell команды toolist hello ВМ размеры, доступные в области hello hello.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-130">Run hello following PowerShell command toolist hello VM sizes available in hello region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="f4ad6-131">Запишите все параметры конфигурации для каждой виртуальной Машины в hello облачную службу, которая содержит toobe ВМ hello изменения размеров.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-131">Make note of all configuration settings for each VM in hello cloud service which contains hello VM toobe resized.</span></span> 
3. <span data-ttu-id="f4ad6-132">Удалите все виртуальные машины в облачной службе hello, выбрав hello параметр tooretain hello дисков для каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-132">Delete all VMs in hello cloud service selecting hello option tooretain hello disks for each VM.</span></span>
4. <span data-ttu-id="f4ad6-133">Повторно создайте hello ВМ toobe изменяется с помощью hello желаемый размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-133">Recreate hello VM toobe resized using hello desired VM size.</span></span>
5. <span data-ttu-id="f4ad6-134">Повторное создание других виртуальных машин, которые были в облачной службе hello размер виртуальной Машины, доступных в кластере оборудования hello, теперь размещение hello облачной службы с помощью.</span><span class="sxs-lookup"><span data-stu-id="f4ad6-134">Recreate all other VMs which were in hello cloud service using a VM size available in hello hardware cluster now hosting hello cloud service.</span></span>

<span data-ttu-id="f4ad6-135">Пример сценария для удаления и повторного создания облачной службы с использованием нового размера виртуальной машины можно найти [здесь](https://github.com/Azure/azure-vm-scripts).</span><span class="sxs-lookup"><span data-stu-id="f4ad6-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f4ad6-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4ad6-136">Next steps</span></span>
* <span data-ttu-id="f4ad6-137">[Изменить размер виртуальных Машин, созданных в модели развертывания диспетчера ресурсов hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f4ad6-137">[Resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

