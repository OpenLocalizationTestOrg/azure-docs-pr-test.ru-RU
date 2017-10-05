---
title: "Настройка частных IP-адресов для виртуальных машин с помощью Azure PowerShell | Документация Майкрософт"
description: "Узнайте, как настроить частные IP-адреса для виртуальных машин с помощью PowerShell."
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
ms.openlocfilehash: 2810190897c44c944912ef3325b1f40479aa3078
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="b0c9a-103">Настройка частных IP-адресов для виртуальной машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0c9a-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="b0c9a-104">Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="b0c9a-105">Для создания ресурсов корпорация Майкрософт рекомендует использовать модель развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="b0c9a-106">Дополнительные сведения о различиях между двумя моделями см. в статье [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md) (Azure Resource Manager и классическое развертывание. Общие сведения о моделях развертывания и состоянии ресурсов).</span><span class="sxs-lookup"><span data-stu-id="b0c9a-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="b0c9a-107">В этой статье описывается модель развертывания с использованием менеджера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="b0c9a-108">Кроме того, вы можете [управлять статическим частным IP-адресом в классической модели развертывания](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b0c9a-108">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="b0c9a-109">Для приведенных ниже примеров команд PowerShell требуется уже созданная простая среда, основанная на приведенном выше сценарии.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="b0c9a-110">Чтобы выполнять команды в соответствии с указаниями, представленными в этом документе, сначала постройте тестовую среду, как описано в статье [Создание виртуальной сети](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b0c9a-110">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="b0c9a-111">Создание виртуальной машины со статическим частным IP-адресом</span><span class="sxs-lookup"><span data-stu-id="b0c9a-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="b0c9a-112">Чтобы создать виртуальную машину с именем *DNS01* в подсети *FrontEnd* виртуальной сети *TestVNet* со статическим частным IP-адресом *192.168.1.101*, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-112">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="b0c9a-113">Задайте переменные для учетной записи хранения, расположения, группы ресурсов и используемых учетных данных.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-113">Set variables for the storage account, location, resource group, and credentials to be used.</span></span> <span data-ttu-id="b0c9a-114">Понадобится ввести имя пользователя и пароль для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-114">You will need to enter a user name and password for the VM.</span></span> <span data-ttu-id="b0c9a-115">Учетная запись хранения и группа ресурсов уже должны существовать.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-115">The storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type the name and password of the local administrator account."
    ```

2. <span data-ttu-id="b0c9a-116">Получите виртуальную сеть и подсеть, в которой хотите создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-116">Retrieve the virtual network and subnet you want to create the VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="b0c9a-117">При необходимости создайте общедоступный IP-адрес для доступа к виртуальной машине из Интернета.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-117">If necessary, create a public IP address to access the VM from the Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="b0c9a-118">Создайте сетевую карту, используя статический частный IP-адрес, который хотите назначить виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-118">Create a NIC using the static private IP address you want to assign to the VM.</span></span> <span data-ttu-id="b0c9a-119">Убедитесь, что IP-адрес находится в диапазоне подсети, в которую добавляется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-119">Make sure the IP is from the subnet range you are adding the VM to.</span></span> <span data-ttu-id="b0c9a-120">Это основной шаг для данной статьи, где частный IP-адрес задается как статический.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-120">This is the main step for this article, where you set the private IP to be static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="b0c9a-121">Создайте виртуальную машину с помощью сетевой карты, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-121">Create the VM using the NIC created above.</span></span>

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

    <span data-ttu-id="b0c9a-122">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="b0c9a-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="b0c9a-123">Получение сведений о статическом частном IP-адресе сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="b0c9a-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="b0c9a-124">Чтобы просмотреть сведения о статическом частном IP-адресе виртуальной машины, созданной с помощью приведенного выше скрипта, выполните следующую команду PowerShell и обратите внимание на значения *PrivateIpAddress* и *PrivateIpAllocationMethod*.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-124">To view the static private IP address information for the VM created with the script above, run the following PowerShell command and observe the values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="b0c9a-125">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="b0c9a-125">Expected output:</span></span>

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

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="b0c9a-126">Удаление статического частного IP-адреса из сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="b0c9a-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="b0c9a-127">Чтобы удалить статический частный IP-адрес, добавленный на виртуальную машину в приведенном выше сценарии, выполните следующие команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b0c9a-127">To remove the static private IP address added to the VM in the script above, run the following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="b0c9a-128">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="b0c9a-128">Expected output:</span></span>

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

## <a name="add-a-static-private-ip-address-to-a-network-interface"></a><span data-ttu-id="b0c9a-129">Добавление статического частного IP-адреса в сетевой интерфейс</span><span class="sxs-lookup"><span data-stu-id="b0c9a-129">Add a static private IP address to a network interface</span></span>
<span data-ttu-id="b0c9a-130">Чтобы добавить статический частный IP-адрес для виртуальной машины, созданной с помощью приведенного ранее скрипта, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="b0c9a-130">To add a static private IP address to the VM created using the script above, run the following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-the-allocation-method-for-a-private-ip-address-assigned-to-a-network-interface"></a><span data-ttu-id="b0c9a-131">Изменение метода распределения для частного IP-адреса, назначенного сетевому интерфейсу</span><span class="sxs-lookup"><span data-stu-id="b0c9a-131">Change the allocation method for a private IP address assigned to a network interface</span></span>

<span data-ttu-id="b0c9a-132">Частный IP-адрес назначается сетевой карте с помощью статического или динамического метода распределения.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-132">A private IP address is assigned to a NIC with the static or dynamic allocation method.</span></span> <span data-ttu-id="b0c9a-133">Динамические IP-адреса можно изменить после запуска виртуальной машины, ранее пребывавшей в состоянии "Остановлено" ("Освобождено").</span><span class="sxs-lookup"><span data-stu-id="b0c9a-133">Dynamic IP addresses can change after starting a VM that was previously in the stopped (deallocated) state.</span></span> <span data-ttu-id="b0c9a-134">Это может вызвать проблемы, если в виртуальной машине размещается служба, требующая один и тот же IP-адрес даже после перезапуска виртуальной машины, пребывающей в состоянии "Остановлено" ("Освобождено").</span><span class="sxs-lookup"><span data-stu-id="b0c9a-134">This can potentially cause issues if the VM is hosting a service that requires the same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="b0c9a-135">Статические IP-адреса хранятся до удаления виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-135">Static IP addresses are retained until the VM is deleted.</span></span> <span data-ttu-id="b0c9a-136">Чтобы изменить метод распределения IP-адреса, выполните следующий скрипт, который изменяет метод распределения с динамического на статический.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-136">To change the allocation method of an IP address, run the following script, which changes the allocation method from dynamic to static.</span></span> <span data-ttu-id="b0c9a-137">Если метод распределения для текущего частного IP-адреса *статический*, измените его на *динамический* перед выполнением скрипта.</span><span class="sxs-lookup"><span data-stu-id="b0c9a-137">If the allocation method for the current private IP address is static, change *Static* to *Dynamic* before executing the script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "The allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for the IP address" $IP"." -NoNewline
```

<span data-ttu-id="b0c9a-138">Если имя сетевой карты вам неизвестно, можно просмотреть список сетевых карт в группе ресурсов, введя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b0c9a-138">If you don't know the name of the NIC, you can view a list of NICs within a resource group by entering the following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="b0c9a-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0c9a-139">Next steps</span></span>
* <span data-ttu-id="b0c9a-140">Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="b0c9a-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="b0c9a-141">Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="b0c9a-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="b0c9a-142">Ознакомьтесь с информацией о [REST API зарезервированных IP-адресов](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0c9a-142">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

