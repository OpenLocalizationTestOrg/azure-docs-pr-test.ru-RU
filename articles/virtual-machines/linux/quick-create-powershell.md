---
title: "Краткое руководство по Azure. Создание виртуальной машины с помощью PowerShell | Документация Майкрософт"
description: "Быстро научитесь создавать виртуальные машины Linux с помощью PowerShell."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: adcf492d4c2d935c880167675a1ed97566156ec7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="c8634-103">Создание виртуальной машины Linux с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8634-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="c8634-104">Модуль PowerShell используется для создания ресурсов Azure и управления ими с помощью командной строки PowerShell или сценариев.</span><span class="sxs-lookup"><span data-stu-id="c8634-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="c8634-105">В этом руководстве описывается, как с помощью модуля Azure PowerShell развернуть виртуальную машину под управлением сервера Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c8634-105">This guide details using the Azure PowerShell module to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="c8634-106">После развертывания сервера создается подключение по протоколу SSH и устанавливается веб-сервер NGINX.</span><span class="sxs-lookup"><span data-stu-id="c8634-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="c8634-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) , прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="c8634-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="c8634-108">Для работы с этим кратким руководством требуется модуль Azure PowerShell версии не ниже 3.6.</span><span class="sxs-lookup"><span data-stu-id="c8634-108">This quick start requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="c8634-109">Чтобы узнать версию, выполните команду ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="c8634-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="c8634-110">Если вам необходимо выполнить установку или обновление, см. статью [об установке модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c8634-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="c8634-111">Наконец, необходимо сохранить открытый ключ SSH *id_rsa.pub* в каталог *.ssh* профиля пользователя Windows.</span><span class="sxs-lookup"><span data-stu-id="c8634-111">Finally, a public SSH key with the name *id_rsa.pub* needs to be stored in the *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="c8634-112">Дополнительные сведения о создании ключей SSH для Azure см. в разделе [Создание пары из открытого и закрытого ключей SSH для виртуальных машин Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c8634-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="c8634-113">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="c8634-113">Log in to Azure</span></span>

<span data-ttu-id="c8634-114">Войдите в подписку Azure с помощью команды `Login-AzureRmAccount` и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="c8634-114">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="c8634-115">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="c8634-115">Create resource group</span></span>

<span data-ttu-id="c8634-116">Создайте группу ресурсов Azure с помощью командлета [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="c8634-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="c8634-117">Группа ресурсов — это логический контейнер, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="c8634-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="c8634-118">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="c8634-118">Create networking resources</span></span>

<span data-ttu-id="c8634-119">Создайте виртуальную сеть, подсеть и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c8634-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="c8634-120">Эти ресурсы используются для того, чтобы установить сетевое подключение к виртуальной машине и подключить ее к Интернету.</span><span class="sxs-lookup"><span data-stu-id="c8634-120">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

<span data-ttu-id="c8634-121">Создайте группу безопасности сети и правило группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="c8634-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="c8634-122">Группа безопасности сети обеспечивает защиту виртуальной машины с помощью правил для входящего и исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="c8634-122">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="c8634-123">В нашем случае создается правило для входящего трафика порта 22, которое разрешает входящие SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="c8634-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="c8634-124">Мы также создадим правило входящего трафика для порта 80, разрешающее входящий веб-трафик.</span><span class="sxs-lookup"><span data-stu-id="c8634-124">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

<span data-ttu-id="c8634-125">Создайте сетевую карту для виртуальной машины с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="c8634-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for the virtual machine.</span></span> <span data-ttu-id="c8634-126">Сетевая карта подключает виртуальную машину к подсети, группе безопасности сети и общедоступному IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="c8634-126">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="c8634-127">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c8634-127">Create virtual machine</span></span>

<span data-ttu-id="c8634-128">Создайте конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c8634-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="c8634-129">Эта конфигурация содержит параметры, которые используются при развертывании виртуальной машины, в том числе образ виртуальной машины, ее размер и настройки аутентификации.</span><span class="sxs-lookup"><span data-stu-id="c8634-129">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

<span data-ttu-id="c8634-130">Создайте виртуальную машину с помощью командлета [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="c8634-130">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="c8634-131">Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="c8634-131">Connect to virtual machine</span></span>

<span data-ttu-id="c8634-132">После завершения развертывания создайте SSH-подключение к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c8634-132">After the deployment has completed, create an SSH connection with the virtual machine.</span></span>

<span data-ttu-id="c8634-133">Получите общедоступный IP-адрес виртуальной машины, выполнив команду [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="c8634-133">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command to return the public IP address of the virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="c8634-134">Чтобы подключиться к виртуальной машине, в системе, в которой установлен протокол SSH, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c8634-134">From a system with SSH installed, used the following command to connect to the virtual machine.</span></span> <span data-ttu-id="c8634-135">В случае работы в Windows для создания подключения можно использовать [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty).</span><span class="sxs-lookup"><span data-stu-id="c8634-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used to create the connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="c8634-136">При появлении запроса на имя пользователя для входа введите *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="c8634-136">When prompted, the login user name is *azureuser*.</span></span> <span data-ttu-id="c8634-137">Если при создании ключей SSH была введена парольная фраза, необходимо также ввести и ее.</span><span class="sxs-lookup"><span data-stu-id="c8634-137">If a passphrase was entered when creating SSH keys, you need to enter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="c8634-138">Установка nginx</span><span class="sxs-lookup"><span data-stu-id="c8634-138">Install NGINX</span></span>

<span data-ttu-id="c8634-139">Чтобы обновить источники пакетов и установить последнюю версию пакета nginx, используйте следующий bash-скрипт:</span><span class="sxs-lookup"><span data-stu-id="c8634-139">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-ngix-welcome-page"></a><span data-ttu-id="c8634-140">Просмотр страницы приветствия nginx</span><span class="sxs-lookup"><span data-stu-id="c8634-140">View the NGIX welcome page</span></span>

<span data-ttu-id="c8634-141">Установив nginx и открыв через Интернет порт 80 на виртуальной машине, вы можете просмотреть страницу приветствия nginx по умолчанию в любом браузере.</span><span class="sxs-lookup"><span data-stu-id="c8634-141">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="c8634-142">Чтобы перейти на страницу по умолчанию, используйте общедоступный IP-адрес, записанный ранее.</span><span class="sxs-lookup"><span data-stu-id="c8634-142">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![Сайт nginx по умолчанию](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="c8634-144">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="c8634-144">Clean up resources</span></span>

<span data-ttu-id="c8634-145">Вы можете удалить ставшие ненужными группу ресурсов, виртуальную машину и все связанные с ней ресурсы, выполнив команду [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="c8634-145">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c8634-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8634-146">Next steps</span></span>

<span data-ttu-id="c8634-147">Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="c8634-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="c8634-148">Дополнительные сведения о виртуальных машинах Azure см. в руководстве для виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="c8634-148">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c8634-149">Создание виртуальных машин Linux и управление ими с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c8634-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
