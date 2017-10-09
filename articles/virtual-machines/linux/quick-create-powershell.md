---
title: "Быстрый запуск - aaaAzure создания виртуальной Машины PowerShell | Документы Microsoft"
description: "Быстро Узнайте toocreate виртуальных машин Linux, с помощью PowerShell"
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
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="e522b-103">Создание виртуальной машины Linux с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e522b-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="e522b-104">используется toocreate и управления ресурсами Azure из командной строки PowerShell hello, или в сценариях Hello модуля Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e522b-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="e522b-105">В этом руководстве рассматривается использование toodeploy модуля Azure PowerShell hello виртуальной машины, работающей Ubuntu server.</span><span class="sxs-lookup"><span data-stu-id="e522b-105">This guide details using hello Azure PowerShell module toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="e522b-106">После развертывания сервера hello SSH-подключения создается и устанавливается веб-сервер NGINX.</span><span class="sxs-lookup"><span data-stu-id="e522b-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="e522b-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="e522b-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="e522b-108">В этом кратком руководстве требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e522b-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="e522b-109">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="e522b-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="e522b-110">Если требуется tooinstall или обновления, см. раздел [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="e522b-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="e522b-111">Наконец, открытый ключ SSH с именем hello *id_rsa.pub* должен toobe, хранящихся в hello *.ssh* каталог профиля пользователя Windows.</span><span class="sxs-lookup"><span data-stu-id="e522b-111">Finally, a public SSH key with hello name *id_rsa.pub* needs toobe stored in hello *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="e522b-112">Дополнительные сведения о создании ключей SSH для Azure см. в разделе [Создание пары из открытого и закрытого ключей SSH для виртуальных машин Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e522b-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="e522b-113">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="e522b-113">Log in tooAzure</span></span>

<span data-ttu-id="e522b-114">Войдите в подписку Azure совместно с hello tooyour `Login-AzureRmAccount` команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="e522b-114">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="e522b-115">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="e522b-115">Create resource group</span></span>

<span data-ttu-id="e522b-116">Создайте группу ресурсов Azure с помощью командлета [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="e522b-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="e522b-117">Группа ресурсов — это логический контейнер, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="e522b-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="e522b-118">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="e522b-118">Create networking resources</span></span>

<span data-ttu-id="e522b-119">Создайте виртуальную сеть, подсеть и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e522b-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="e522b-120">Эти ресурсы, используемые tooprovide сетевого подключения toohello виртуальной машины и подключите его toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="e522b-120">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

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

<span data-ttu-id="e522b-121">Создайте группу безопасности сети и правило группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="e522b-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="e522b-122">группы безопасности сети Hello защищает hello виртуальной машины, с помощью правила входящего и исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="e522b-122">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="e522b-123">В нашем случае создается правило для входящего трафика порта 22, которое разрешает входящие SSH-подключения.</span><span class="sxs-lookup"><span data-stu-id="e522b-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="e522b-124">Также мы хотим toocreate входящее правило для порта 80, который позволяет входящего веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="e522b-124">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

<span data-ttu-id="e522b-125">Создание сетевого адаптера с [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e522b-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="e522b-126">Hello сетевой адаптер подключается подсети tooa hello виртуальных машин, группы безопасности сети и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e522b-126">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="e522b-127">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e522b-127">Create virtual machine</span></span>

<span data-ttu-id="e522b-128">Создайте конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e522b-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="e522b-129">Такая настройка включает hello параметров, используемых при развертывании виртуальной машины hello, такие как изображения, размер и проверку подлинности конфигурации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e522b-129">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

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

<span data-ttu-id="e522b-130">Создание виртуальной машины hello с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="e522b-130">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="e522b-131">Подключиться к компьютеру toovirtual</span><span class="sxs-lookup"><span data-stu-id="e522b-131">Connect toovirtual machine</span></span>

<span data-ttu-id="e522b-132">После завершения развертывания hello создания SSH-подключения с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="e522b-132">After hello deployment has completed, create an SSH connection with hello virtual machine.</span></span>

<span data-ttu-id="e522b-133">Используйте hello [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) команды tooreturn hello общедоступный IP-адрес виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="e522b-133">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="e522b-134">С компьютера, где установлен SSH используемые hello следующая команда tooconnect toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e522b-134">From a system with SSH installed, used hello following command tooconnect toohello virtual machine.</span></span> <span data-ttu-id="e522b-135">При работе в Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) может быть используется toocreate hello соединением.</span><span class="sxs-lookup"><span data-stu-id="e522b-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used toocreate hello connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="e522b-136">При появлении запроса является имя пользователя hello *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="e522b-136">When prompted, hello login user name is *azureuser*.</span></span> <span data-ttu-id="e522b-137">Если парольная фраза было введено при создании ключей SSH, необходимо tooenter этом также.</span><span class="sxs-lookup"><span data-stu-id="e522b-137">If a passphrase was entered when creating SSH keys, you need tooenter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="e522b-138">Установка nginx</span><span class="sxs-lookup"><span data-stu-id="e522b-138">Install NGINX</span></span>

<span data-ttu-id="e522b-139">Используйте hello ниже bash источники пакетов tooupdate сценария и установить последнюю версию пакета NGINX hello.</span><span class="sxs-lookup"><span data-stu-id="e522b-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a><span data-ttu-id="e522b-140">Просмотр hello NGIX начальной страницы</span><span class="sxs-lookup"><span data-stu-id="e522b-140">View hello NGIX welcome page</span></span>

<span data-ttu-id="e522b-141">NGINX установлен и порт 80, теперь открыт на ВМ из hello Интернет - можно использовать веб-браузер на выбор tooview hello по умолчанию NGINX начальной страницы.</span><span class="sxs-lookup"><span data-stu-id="e522b-141">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="e522b-142">Быть убедиться, что toouse hello общедоступный IP-адрес, описанных выше toovisit страница по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="e522b-142">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Сайт nginx по умолчанию](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="e522b-144">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="e522b-144">Clean up resources</span></span>

<span data-ttu-id="e522b-145">Если больше не нужны, можно использовать hello [AzureRmResourceGroup удаление](/powershell/module/azurerm.resources/remove-azurermresourcegroup) команд группы ресурсов tooremove hello, виртуальных Машин и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e522b-145">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="e522b-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e522b-146">Next steps</span></span>

<span data-ttu-id="e522b-147">Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="e522b-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="e522b-148">toolearn Дополнительные сведения о виртуальных машинах Azure, продолжить toohello учебника для виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="e522b-148">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e522b-149">Создание виртуальных машин Linux и управление ими с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e522b-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
