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
# <a name="create-a-linux-virtual-machine-with-powershell"></a>Создание виртуальной машины Linux с помощью PowerShell

используется toocreate и управления ресурсами Azure из командной строки PowerShell hello, или в сценариях Hello модуля Azure PowerShell. В этом руководстве рассматривается использование toodeploy модуля Azure PowerShell hello виртуальной машины, работающей Ubuntu server. После развертывания сервера hello SSH-подключения создается и устанавливается веб-сервер NGINX.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

В этом кратком руководстве требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).

Наконец, открытый ключ SSH с именем hello *id_rsa.pub* должен toobe, хранящихся в hello *.ssh* каталог профиля пользователя Windows. Дополнительные сведения о создании ключей SSH для Azure см. в разделе [Создание пары из открытого и закрытого ключей SSH для виртуальных машин Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="log-in-tooazure"></a>Войдите в tooAzure

Войдите в подписку Azure совместно с hello tooyour `Login-AzureRmAccount` команды и выполните hello на экране инструкциям.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Создать группу ресурсов

Создайте группу ресурсов Azure с помощью командлета [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Группа ресурсов — это логический контейнер, в котором происходит развертывание ресурсов Azure и управление ими. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a>Создание сетевых ресурсов

Создайте виртуальную сеть, подсеть и общедоступный IP-адрес. Эти ресурсы, используемые tooprovide сетевого подключения toohello виртуальной машины и подключите его toohello Интернета.

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

Создайте группу безопасности сети и правило группы безопасности сети. группы безопасности сети Hello защищает hello виртуальной машины, с помощью правила входящего и исходящего трафика. В нашем случае создается правило для входящего трафика порта 22, которое разрешает входящие SSH-подключения. Также мы хотим toocreate входящее правило для порта 80, который позволяет входящего веб-трафика.

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

Создание сетевого адаптера с [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) для hello виртуальной машины. Hello сетевой адаптер подключается подсети tooa hello виртуальных машин, группы безопасности сети и общедоступный IP-адрес.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Создание виртуальной машины

Создайте конфигурацию виртуальной машины. Такая настройка включает hello параметров, используемых при развертывании виртуальной машины hello, такие как изображения, размер и проверку подлинности конфигурации виртуальной машины.

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

Создание виртуальной машины hello с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Подключиться к компьютеру toovirtual

После завершения развертывания hello создания SSH-подключения с виртуальной машиной hello.

Используйте hello [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) команды tooreturn hello общедоступный IP-адрес виртуальной машины hello.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

С компьютера, где установлен SSH используемые hello следующая команда tooconnect toohello виртуальной машины. При работе в Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) может быть используется toocreate hello соединением. 

```bash 
ssh <Public IP Address>
```

При появлении запроса является имя пользователя hello *azureuser*. Если парольная фраза было введено при создании ключей SSH, необходимо tooenter этом также.


## <a name="install-nginx"></a>Установка nginx

Используйте hello ниже bash источники пакетов tooupdate сценария и установить последнюю версию пакета NGINX hello. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a>Просмотр hello NGIX начальной страницы

NGINX установлен и порт 80, теперь открыт на ВМ из hello Интернет - можно использовать веб-браузер на выбор tooview hello по умолчанию NGINX начальной страницы. Быть убедиться, что toouse hello общедоступный IP-адрес, описанных выше toovisit страница по умолчанию hello. 

![Сайт nginx по умолчанию](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Очистка ресурсов

Если больше не нужны, можно использовать hello [AzureRmResourceGroup удаление](/powershell/module/azurerm.resources/remove-azurermresourcegroup) команд группы ресурсов tooremove hello, виртуальных Машин и все связанные ресурсы.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера. toolearn Дополнительные сведения о виртуальных машинах Azure, продолжить toohello учебника для виртуальных машин Linux.

> [!div class="nextstepaction"]
> [Создание виртуальных машин Linux и управление ими с помощью Azure CLI](./tutorial-manage-vm.md)
