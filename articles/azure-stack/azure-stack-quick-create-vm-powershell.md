---
title: "aaaCreate виртуальной машины Windows с помощью PowerShell в стек Azure | Документы Microsoft"
description: "Создание виртуальной машины Windows с помощью PowerShell Azure стека."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: de063eae6f0782d8916da991f285a9de6b41def4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-by-using-powershell-in-azure-stack"></a><span data-ttu-id="58c9c-103">Создание виртуальной машины Windows с помощью PowerShell в стек Azure</span><span class="sxs-lookup"><span data-stu-id="58c9c-103">Create a Windows virtual machine by using PowerShell in Azure Stack</span></span>

<span data-ttu-id="58c9c-104">Виртуальные машины в стек Azure обеспечивает hello гибкие возможности виртуализации без необходимости toobuy и поддерживать hello физического оборудования, который запускает задача.</span><span class="sxs-lookup"><span data-stu-id="58c9c-104">Virtual machines in Azure Stack give you hello flexibility of virtualization without having toobuy and maintain hello physical hardware that runs it.</span></span> <span data-ttu-id="58c9c-105">При использовании виртуальных машин следует понимать, что существуют некоторые различия между hello функции, доступные в Azure и Azure стека см. в toohello [рекомендации для виртуальных машин в Azure стека](azure-stack-vm-considerations.md) toolearn статьи о Эти различия.</span><span class="sxs-lookup"><span data-stu-id="58c9c-105">When you use Virtual Machines, understand that there are some differences between hello features that are available in Azure and Azure Stack, refer toohello [Considerations for virtual machines in Azure Stack](azure-stack-vm-considerations.md) topic toolearn about these differences.</span></span> 

<span data-ttu-id="58c9c-106">Сведения, с помощью PowerShell toocreate руководства виртуальной машины Windows Server 2016 в стек Azure.</span><span class="sxs-lookup"><span data-stu-id="58c9c-106">This guide details using PowerShell toocreate a Windows Server 2016 virtual machine in Azure Stack.</span></span> <span data-ttu-id="58c9c-107">Можно запустить hello действия, описанные в этой статье из пакета средств разработки Azure стека hello или из внешнего клиента на основе Windows, при подключении через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="58c9c-107">You can run hello steps described in this article either from hello Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="58c9c-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="58c9c-108">Prerequisites</span></span>

1. <span data-ttu-id="58c9c-109">Стек Azure marketplace Hello не содержит hello Windows Server 2016 изображения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="58c9c-109">hello Azure Stack marketplace doesn't contain hello Windows Server 2016 image by default.</span></span> <span data-ttu-id="58c9c-110">Перед созданием виртуальной машины, убедитесь, что оператор hello Azure стека [добавляет hello Windows Server 2016 изображения toohello стека Azure marketplace](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="58c9c-110">So, before you can create a virtual machine, make sure that hello Azure Stack operator [adds hello Windows Server 2016 image toohello Azure Stack marketplace](azure-stack-add-default-image.md).</span></span> 
2. <span data-ttu-id="58c9c-111">Стек Azure требует определенной версии toocreate модуля Azure PowerShell и управлять ресурсами hello.</span><span class="sxs-lookup"><span data-stu-id="58c9c-111">Azure Stack requires specific version of Azure PowerShell module toocreate and manage hello resources.</span></span> <span data-ttu-id="58c9c-112">Используйте hello действия, описанные в [Установка PowerShell для Azure стека](azure-stack-powershell-install.md) разделе tooinstall hello требуемой версии.</span><span class="sxs-lookup"><span data-stu-id="58c9c-112">Use hello steps described in [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) topic tooinstall hello required version.</span></span>
3. [<span data-ttu-id="58c9c-113">Настройка среды PowerShell hello Azure стека пользователя</span><span class="sxs-lookup"><span data-stu-id="58c9c-113">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md) 

## <a name="create-a-resource-group"></a><span data-ttu-id="58c9c-114">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="58c9c-114">Create a resource group</span></span>

<span data-ttu-id="58c9c-115">Группы ресурсов — это логический контейнер, в какой стек Azure ресурсы развертываются и управляются.</span><span class="sxs-lookup"><span data-stu-id="58c9c-115">A resource group is a logical container into which Azure Stack resources are deployed and managed.</span></span> <span data-ttu-id="58c9c-116">Используйте hello, следующий блок кода toocreate группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="58c9c-116">Use hello following code block toocreate a resource group.</span></span> <span data-ttu-id="58c9c-117">Мы присвоили значения для всех переменных в этом документе, можно использовать их как есть или назначить другое значение.</span><span class="sxs-lookup"><span data-stu-id="58c9c-117">We have assigned values for all variables in this document, you can use them as is or assign a different value.</span></span>  

```powershell
# Create variables toostore hello location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a><span data-ttu-id="58c9c-118">Создание ресурсов хранилища</span><span class="sxs-lookup"><span data-stu-id="58c9c-118">Create storage resources</span></span> 

<span data-ttu-id="58c9c-119">Создайте учетную запись хранения и образ Windows Server 2016 hello toostore контейнера хранилища.</span><span class="sxs-lookup"><span data-stu-id="58c9c-119">Create a storage account, and a storage container toostore hello Windows Server 2016 image.</span></span>

```powershell
# Create variables toostore hello storage account name and hello storage account SKU information
$StorageAccountName = "mystorageaccount"
$SkuName = "Standard_LRS"

# Create a new storage account
$StorageAccount = New-AzureRMStorageAccount `
  -Location $location `
  -ResourceGroupName $ResourceGroupName `
  -Type $SkuName `
  -Name $StorageAccountName

Set-AzureRmCurrentStorageAccount `
  -StorageAccountName $storageAccountName `
  -ResourceGroupName $resourceGroupName

# Create a storage container toostore hello virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a><span data-ttu-id="58c9c-120">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="58c9c-120">Create networking resources</span></span>

<span data-ttu-id="58c9c-121">Создайте виртуальную сеть, подсеть и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="58c9c-121">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="58c9c-122">Эти ресурсы, используемые tooprovide сетевого подключения toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="58c9c-122">These resources are used tooprovide network connectivity toohello virtual machine.</span></span>  

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name MyVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -AllocationMethod Static `
  -IdleTimeoutInMinutes 4 `
  -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="58c9c-123">Создайте группу безопасности сети и правило группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="58c9c-123">Create a network security group and a network security group rule</span></span>

<span data-ttu-id="58c9c-124">группы безопасности сети Hello защищает hello виртуальной машины с помощью правила входящего и исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="58c9c-124">hello network security group secures hello virtual machine by using inbound and outbound rules.</span></span> <span data-ttu-id="58c9c-125">Позволяет создать правило для порта 3389 tooallow входящих подключений удаленного рабочего стола и входящее правило для порта 80 tooallow входящего веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="58c9c-125">Lets create an inbound rule for port 3389 tooallow incoming Remote Desktop connections and an inbound rule for port 80 tooallow incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleRDP `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleWWW `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRuleRDP,$nsgRuleWeb 
```
 
### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="58c9c-126">Создать карту сети для виртуальной машины hello</span><span class="sxs-lookup"><span data-stu-id="58c9c-126">Create a network card for hello virtual machine</span></span>

<span data-ttu-id="58c9c-127">Hello сетевой адаптер подключается подсети tooa hello виртуальных машин, группы безопасности сети и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="58c9c-127">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate it with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
  -Name myNic `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id `
  -NetworkSecurityGroupId $nsg.Id 
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="58c9c-128">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="58c9c-128">Create a virtual machine</span></span>

<span data-ttu-id="58c9c-129">Создайте конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="58c9c-129">Create a virtual machine configuration.</span></span> <span data-ttu-id="58c9c-130">Конфигурация Hello включает hello параметров, используемых при развертывании виртуальной машины hello, такие как образ виртуальной машины, размер, учетные данные.</span><span class="sxs-lookup"><span data-stu-id="58c9c-130">hello configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, credentials.</span></span>

```powershell
# Define a credential object toostore hello username and password for hello virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create hello virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_A1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize 

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Windows `
  -ComputerName "MainComputer" `
  -Credential $Credential 

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "MicrosoftWindowsServer" `
  -Offer "WindowsServer" `
  -Skus "2016-Datacenter" `
  -Version "latest"

$osDiskName = "OsDisk"
$osDiskUri = '{0}vhds/{1}-{2}.vhd' -f `
  $StorageAccount.PrimaryEndpoints.Blob.ToString(),`
  $vmName.ToLower(), `
  $osDiskName

# Sets hello operating system disk properties on a virtual machine. 
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id 

#Create hello virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="58c9c-131">Подключение toohello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="58c9c-131">Connect toohello virtual machine</span></span>

<span data-ttu-id="58c9c-132">После успешного создания виртуальной машины hello откройте виртуальной машины toohello подключения удаленного рабочего стола из пакета средств разработки hello, или из внешнего клиента на основе Windows при подключении через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="58c9c-132">After hello virtual machine is successfully created, open a Remote Desktop connection toohello virtual machine from hello development kit, or from a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="58c9c-133">tooremote hello виртуальную машину, созданную в предыдущем шаге hello, необходимо его общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="58c9c-133">tooremote into hello virtual machine that you created in hello previous step, you need its public IP address.</span></span> <span data-ttu-id="58c9c-134">Выполните следующие команды tooget hello общедоступный IP-адрес виртуальной машины hello hello.</span><span class="sxs-lookup"><span data-stu-id="58c9c-134">Run hello following command tooget hello public IP address of hello virtual machine:</span></span> 

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```
 
<span data-ttu-id="58c9c-135">Используйте hello следующая команда toocreate сеанс удаленного рабочего стола с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="58c9c-135">Use hello following command toocreate a Remote Desktop session with hello virtual machine.</span></span> <span data-ttu-id="58c9c-136">Замените hello IP-адрес publicIPAddress hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="58c9c-136">Replace hello IP address with hello publicIPAddress of your virtual machine.</span></span> <span data-ttu-id="58c9c-137">При появлении запроса введите hello имя пользователя и пароль, который использовался при создании виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="58c9c-137">When prompted, enter hello username and password that you used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```
## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="58c9c-138">Удалить виртуальную машину hello</span><span class="sxs-lookup"><span data-stu-id="58c9c-138">Delete hello virtual machine</span></span>

<span data-ttu-id="58c9c-139">Когда больше не нужен, hello используйте следующую команду, tooremove hello ресурсов группы, которая содержит hello виртуальной машины и его связанные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="58c9c-139">When no longer needed, use hello following command tooremove hello resource group that contains hello virtual machine and its related resources:</span></span>

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a><span data-ttu-id="58c9c-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58c9c-140">Next steps</span></span>

<span data-ttu-id="58c9c-141">toolearn о хранилище в стек Azure см. toohello [Обзор хранилища](azure-stack-storage-overview.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="58c9c-141">toolearn about Storage in Azure Stack, refer toohello [storage overview](azure-stack-storage-overview.md) topic.</span></span>

