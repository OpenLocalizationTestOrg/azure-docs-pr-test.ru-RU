---
title: "aaaConfigure частных IP-адресов для виртуальных машин - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как tooconfigure частных IP-адресов виртуальных машин с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4a3eb67de583e08208fcab40de1c2a8a9b65618c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="66f3d-103">Настройка частных IP-адресов для виртуальной машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="66f3d-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="66f3d-104">Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую.</span><span class="sxs-lookup"><span data-stu-id="66f3d-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="66f3d-105">Корпорация Майкрософт рекомендует создать ресурсы с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="66f3d-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="66f3d-106">Дополнительные сведения о toolearn hello различий между моделями hello двух чтения hello [модели развертывания Azure понять](../azure-resource-manager/resource-manager-deployment-model.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="66f3d-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="66f3d-107">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="66f3d-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="66f3d-108">Вы также можете [управление статический частный IP-адрес в hello классической модели развертывания](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="66f3d-108">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="66f3d-109">Образец Hello PowerShell приведенную ниже команду ожидать простой среде уже создан на основании hello сценарии выше.</span><span class="sxs-lookup"><span data-stu-id="66f3d-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="66f3d-110">Если требуется toorun hello команд, отображаемых в этом документе, вначале построить hello тестовой среды, описанные в [создании виртуальной сети](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="66f3d-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="66f3d-111">Создание виртуальной машины со статическим частным IP-адресом</span><span class="sxs-lookup"><span data-stu-id="66f3d-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="66f3d-112">toocreate Виртуальную машину с именем *DNS01* в hello *переднего плана* подсети виртуальной сети с именем *TestVNet* с статических частного IP-адреса *192.168.1.101*, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="66f3d-112">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="66f3d-113">Задайте переменные для учетной записи хранилища hello, местоположение, группа ресурсов и toobe учетные данные используются.</span><span class="sxs-lookup"><span data-stu-id="66f3d-113">Set variables for hello storage account, location, resource group, and credentials toobe used.</span></span> <span data-ttu-id="66f3d-114">Необходимо будет tooenter имя пользователя и пароль для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="66f3d-114">You will need tooenter a user name and password for hello VM.</span></span> <span data-ttu-id="66f3d-115">Группа учетных записей и ресурсов хранилища Hello уже должна существовать.</span><span class="sxs-lookup"><span data-stu-id="66f3d-115">hello storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type hello name and password of hello local administrator account."
    ```

2. <span data-ttu-id="66f3d-116">Получение hello виртуальной сети и подсети требуется toocreate hello виртуальной Машины в.</span><span class="sxs-lookup"><span data-stu-id="66f3d-116">Retrieve hello virtual network and subnet you want toocreate hello VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="66f3d-117">При необходимости создайте открытый tooaccess hello IP адрес виртуальной Машины из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="66f3d-117">If necessary, create a public IP address tooaccess hello VM from hello Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="66f3d-118">Создайте сетевую КАРТУ с помощью hello статический частный IP-адрес нужно tooassign toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="66f3d-118">Create a NIC using hello static private IP address you want tooassign toohello VM.</span></span> <span data-ttu-id="66f3d-119">Убедитесь, что hello IP из диапазона подсети hello, добавляемый hello виртуальной Машины для.</span><span class="sxs-lookup"><span data-stu-id="66f3d-119">Make sure hello IP is from hello subnet range you are adding hello VM to.</span></span> <span data-ttu-id="66f3d-120">Это основной шаг hello для данной статьи, задаются hello частного IP toobe статический.</span><span class="sxs-lookup"><span data-stu-id="66f3d-120">This is hello main step for this article, where you set hello private IP toobe static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="66f3d-121">Создайте приветствия созданную виртуальную Машину с помощью hello сетевого Адаптера.</span><span class="sxs-lookup"><span data-stu-id="66f3d-121">Create hello VM using hello NIC created above.</span></span>

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    <span data-ttu-id="66f3d-122">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="66f3d-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="66f3d-123">Получение сведений о статическом частном IP-адресе сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="66f3d-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="66f3d-124">tooview hello статических частного IP-адреса сведения для hello создания ВМ с hello-сценарий, приведенный выше, запустите следующую команду PowerShell hello и просмотрите значения hello для *адрес PrivateIpAddress* и  *Метод PrivateIpAllocationMethod*:</span><span class="sxs-lookup"><span data-stu-id="66f3d-124">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="66f3d-125">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="66f3d-125">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="66f3d-126">Удаление статического частного IP-адреса из сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="66f3d-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="66f3d-127">tooremove hello статический частный IP-адрес добавлен toohello ВМ в скрипте hello выше выполнения hello, следующие команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="66f3d-127">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="66f3d-128">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="66f3d-128">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-tooa-network-interface"></a><span data-ttu-id="66f3d-129">Добавьте статический частного IP адрес tooa сетевой интерфейс</span><span class="sxs-lookup"><span data-stu-id="66f3d-129">Add a static private IP address tooa network interface</span></span>
<span data-ttu-id="66f3d-130">tooadd статические частного IP адрес toohello виртуальной Машины, созданной с помощью скрипта hello выше, запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="66f3d-130">tooadd a static private IP address toohello VM created using hello script above, run hello following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-hello-allocation-method-for-a-private-ip-address-assigned-tooa-network-interface"></a><span data-ttu-id="66f3d-131">Изменение способа выделения hello частный IP-адрес, назначенный tooa сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="66f3d-131">Change hello allocation method for a private IP address assigned tooa network interface</span></span>

<span data-ttu-id="66f3d-132">Частный IP-адрес назначается tooa сетевого Адаптера с помощью метода выделения статической или динамической hello.</span><span class="sxs-lookup"><span data-stu-id="66f3d-132">A private IP address is assigned tooa NIC with hello static or dynamic allocation method.</span></span> <span data-ttu-id="66f3d-133">Динамические IP-адреса можно изменить после запуска виртуальной Машины, который ранее был в hello остановлена (освобождена) состояние.</span><span class="sxs-lookup"><span data-stu-id="66f3d-133">Dynamic IP addresses can change after starting a VM that was previously in hello stopped (deallocated) state.</span></span> <span data-ttu-id="66f3d-134">Это потенциально может вызвать проблемы, если hello виртуальной Машины размещается служба, которая требует hello же IP-адрес, даже после перезагрузки компьютера из остановлена (освобождена).</span><span class="sxs-lookup"><span data-stu-id="66f3d-134">This can potentially cause issues if hello VM is hosting a service that requires hello same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="66f3d-135">Статические IP-адреса, сохраняются до удаления hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="66f3d-135">Static IP addresses are retained until hello VM is deleted.</span></span> <span data-ttu-id="66f3d-136">метод распределения hello toochange IP-адреса, запустите следующий сценарий, который изменяет способ распределения hello из динамического toostatic hello.</span><span class="sxs-lookup"><span data-stu-id="66f3d-136">toochange hello allocation method of an IP address, run hello following script, which changes hello allocation method from dynamic toostatic.</span></span> <span data-ttu-id="66f3d-137">Если метод распределения hello для hello текущего частный IP-адрес является статическим, измените *статических* слишком*динамического* перед выполнением скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="66f3d-137">If hello allocation method for hello current private IP address is static, change *Static* too*Dynamic* before executing hello script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "hello allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for hello IP address" $IP"." -NoNewline
```

<span data-ttu-id="66f3d-138">Если вы не знаете имя hello hello сетевого Адаптера, можно просмотреть список сетевых адаптеров в группу ресурсов, введя hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="66f3d-138">If you don't know hello name of hello NIC, you can view a list of NICs within a resource group by entering hello following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="66f3d-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66f3d-139">Next steps</span></span>
* <span data-ttu-id="66f3d-140">Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="66f3d-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="66f3d-141">Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="66f3d-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="66f3d-142">Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="66f3d-142">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

