---
title: "Настройка статического внутреннего частного IP-адреса для классической виртуальной машины Azure"
description: "Основные сведения о статических внутренних IP-адресах (DIP) и управлении ими"
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
ms.openlocfilehash: cf9ee59ca4e44ed01836c2efb1f4df5f073bf6e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="c68ab-103">Как задать статический внутренний частный IP-адрес с помощью PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="c68ab-103">How to set a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="c68ab-104">В большинстве случаев для виртуальной машины не нужно указывать статический внутренний IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c68ab-104">In most cases, you won’t need to specify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="c68ab-105">Виртуальные машины в виртуальной сети будут автоматически получать внутренний IP-адрес из указанного вами диапазона.</span><span class="sxs-lookup"><span data-stu-id="c68ab-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="c68ab-106">Однако в некоторых случаях указание статического IP-адреса для конкретной виртуальной машины имеет смысл.</span><span class="sxs-lookup"><span data-stu-id="c68ab-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="c68ab-107">Например, если на виртуальной машине планируется запускать DNS или она будет контроллером домена.</span><span class="sxs-lookup"><span data-stu-id="c68ab-107">For example, if your VM is going to run DNS or will be a domain controller.</span></span> <span data-ttu-id="c68ab-108">Статический внутренний IP-адрес остается у виртуальной машины даже при переходе в состояние остановки или отзыва.</span><span class="sxs-lookup"><span data-stu-id="c68ab-108">A static internal IP address stays with the VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c68ab-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c68ab-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c68ab-110">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="c68ab-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="c68ab-111">Для большинства новых развертываний корпорация Майкрософт рекомендует [использовать модель развертывания с помощью Resource Manager](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c68ab-111">Microsoft recommends that most new deployments use the [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-to-verify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="c68ab-112">Проверка доступности определенного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="c68ab-112">How to verify if a specific IP address is available</span></span>
<span data-ttu-id="c68ab-113">Чтобы проверить, доступен ли IP-адрес *10.0.0.7* в виртуальной сети с именем *TestVnet*, выполните следующую команду PowerShell и проверьте значение для *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="c68ab-113">To verify if the IP address *10.0.0.7* is available in a vnet named *TestVnet*, run the following PowerShell command and verify the value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="c68ab-114">Если требуется протестировать указанную выше команду в защищенной среде, следуйте указаниям из статьи [Создание (классической) виртуальной сети с помощью портала предварительной версии Azure](virtual-networks-create-vnet-classic-pportal.md), чтобы создать виртуальную сеть *TestVnet* и убедиться в том, что она использует адресное пространство *10.0.0.0/8*.</span><span class="sxs-lookup"><span data-stu-id="c68ab-114">If you want to test the command above in a safe environment follow the guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) to create a vnet named *TestVnet* and ensure it uses the *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-to-specify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="c68ab-115">Указание статического внутреннего IP-адреса при создании виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c68ab-115">How to specify a static internal IP when creating a VM</span></span>
<span data-ttu-id="c68ab-116">Приведенный ниже сценарий PowerShell создает облачную службу *TestService*, затем получает образ из Azure, после чего создает виртуальную машину *TestVM* в новой облачной службе с использованием полученного образа, задает для этой виртуальной машины нахождение в подсети *Subnet-1* и устанавливает *10.0.0.7* статическим внутренним IP-адресом виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c68ab-116">The PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in the new cloud service using the retrieved image, sets the VM to be in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for the VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-to-retrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="c68ab-117">Получение сведений о статическом внутреннем IP-адресе виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c68ab-117">How to retrieve static internal IP information for a VM</span></span>
<span data-ttu-id="c68ab-118">Чтобы просмотреть сведения о статическом внутреннем IP-адресе виртуальной машины, созданной с помощью приведенного выше сценария, выполните следующую команду PowerShell и обратите внимание на значения *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="c68ab-118">To view the static internal IP information for the VM created with the script above, run the following PowerShell command and observe the values for *IpAddress*:</span></span>

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

## <a name="how-to-remove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="c68ab-119">Удаление статического внутреннего IP-адреса с виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c68ab-119">How to remove a static internal IP from a VM</span></span>
<span data-ttu-id="c68ab-120">Чтобы удалить статический внутренний IP-адрес, добавленный на виртуальную машину в приведенном выше сценарии, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c68ab-120">To remove the static internal IP added to the VM in the script above, run the following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-to-add-a-static-internal-ip-to-an-existing-vm"></a><span data-ttu-id="c68ab-121">Добавление статического внутреннего IP-адреса для существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c68ab-121">How to add a static internal IP to an existing VM</span></span>
<span data-ttu-id="c68ab-122">Чтобы добавить статический внутренний IP-адрес для виртуальной машины, созданной с помощью приведенного выше сценария, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c68ab-122">To add a static internal IP to the VM created using the script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="c68ab-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c68ab-123">Next steps</span></span>
[<span data-ttu-id="c68ab-124">Зарезервированный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="c68ab-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="c68ab-125">Общедоступный IP-адрес уровня экземпляра (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="c68ab-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="c68ab-126">API REST зарезервированных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="c68ab-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

