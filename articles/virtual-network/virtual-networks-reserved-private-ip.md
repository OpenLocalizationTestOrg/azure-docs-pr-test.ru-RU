---
title: "aaaStatic внутренних частных IP - Azure VM - классический"
description: "Основные сведения о статического внутреннего IP-адреса (DIP) и как toomanage их"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="f019f-103">Как tooset статический внутренний частного IP адрес, с помощью PowerShell (классические)</span><span class="sxs-lookup"><span data-stu-id="f019f-103">How tooset a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="f019f-104">В большинстве случаев нет необходимости toospecify статический внутренний IP-адрес для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f019f-104">In most cases, you won’t need toospecify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="f019f-105">Виртуальные машины в виртуальной сети будут автоматически получать внутренний IP-адрес из указанного вами диапазона.</span><span class="sxs-lookup"><span data-stu-id="f019f-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="f019f-106">Однако в некоторых случаях указание статического IP-адреса для конкретной виртуальной машины имеет смысл.</span><span class="sxs-lookup"><span data-stu-id="f019f-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="f019f-107">Например, если ВМ является постоянной toorun DNS или будет контроллером домена.</span><span class="sxs-lookup"><span data-stu-id="f019f-107">For example, if your VM is going toorun DNS or will be a domain controller.</span></span> <span data-ttu-id="f019f-108">Статический внутренний IP-адрес остается с hello виртуальной Машины, даже в состоянии остановки или отзыва.</span><span class="sxs-lookup"><span data-stu-id="f019f-108">A static internal IP address stays with hello VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f019f-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f019f-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f019f-110">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="f019f-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="f019f-111">Корпорация Майкрософт рекомендует наиболее новые развертывания hello [модели развертывания диспетчера ресурсов](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f019f-111">Microsoft recommends that most new deployments use hello [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="f019f-112">Как tooverify, если доступен определенный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="f019f-112">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="f019f-113">tooverify Если hello IP-адрес *10.0.0.7* доступен в виртуальной сети с именем *TestVnet*, запустите следующую команду PowerShell hello и проверьте значение hello *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="f019f-113">tooverify if hello IP address *10.0.0.7* is available in a vnet named *TestVnet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="f019f-114">Команда hello tootest выше в безопасной среде выполните рекомендации hello в [Создание виртуальной сети (классические)](virtual-networks-create-vnet-classic-pportal.md) toocreate виртуальную сеть с именем *TestVnet* и убедитесь, он использует hello  *10.0.0.0/8* адресное пространство.</span><span class="sxs-lookup"><span data-stu-id="f019f-114">If you want tootest hello command above in a safe environment follow hello guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) toocreate a vnet named *TestVnet* and ensure it uses hello *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="f019f-115">Как toospecify статического внутреннего IP-адреса при создании виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="f019f-115">How toospecify a static internal IP when creating a VM</span></span>
<span data-ttu-id="f019f-116">Приведенный ниже сценарий PowerShell Hello создает новую облачную службу с именем *TestService*, затем извлекает изображение из Azure, а затем создает Виртуальную машину с именем *TestVM* в hello новой облачной службы с помощью образа получить hello Задает hello toobe виртуальной Машины в подсеть с именем *Subnet-1*и задает *10.0.0.7* как статический внутренний IP-адрес, для hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="f019f-116">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="f019f-117">Как tooretrieve статические внутренние IP сведения для виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="f019f-117">How tooretrieve static internal IP information for a VM</span></span>
<span data-ttu-id="f019f-118">tooview hello статические внутренние IP сведения для hello создания ВМ с hello-сценарий, приведенный выше, запустите следующую команду PowerShell hello и просмотрите значения hello *IP-адрес*:</span><span class="sxs-lookup"><span data-stu-id="f019f-118">tooview hello static internal IP information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="f019f-119">Как tooremove статического внутреннего IP-адреса, от виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="f019f-119">How tooremove a static internal IP from a VM</span></span>
<span data-ttu-id="f019f-120">tooremove hello статический внутренний IP-адрес добавлен toohello ВМ в скрипте hello выше, выполните следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="f019f-120">tooremove hello static internal IP added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a><span data-ttu-id="f019f-121">Как tooadd статического внутреннего IP tooan существующей виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="f019f-121">How tooadd a static internal IP tooan existing VM</span></span>
<span data-ttu-id="f019f-122">tooadd статические внутренние toohello IP виртуальной Машины, созданной с помощью скрипта hello выше runt следующей команды:</span><span class="sxs-lookup"><span data-stu-id="f019f-122">tooadd a static internal IP toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="f019f-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f019f-123">Next steps</span></span>
[<span data-ttu-id="f019f-124">Зарезервированный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="f019f-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="f019f-125">Общедоступный IP-адрес уровня экземпляра (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="f019f-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="f019f-126">API REST зарезервированных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="f019f-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

