---
title: "Быстрый запуск - aaaAzure создания виртуальной Машины Windows PowerShell | Документы Microsoft"
description: "Быстро Узнайте toocreate виртуальных машинах с помощью PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a>Создание виртуальной машины Windows с помощью PowerShell

используется toocreate и управления ресурсами Azure из командной строки PowerShell hello, или в сценариях Hello модуля Azure PowerShell. В этом руководстве рассматривается использование PowerShell toocreate и виртуальная машина Azure под управлением Windows Server 2016. После завершения развертывания мы подключения toohello сервера и установить службы IIS.  

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

В этом кратком руководстве требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).

## <a name="log-in-tooazure"></a>Войдите в tooAzure

Войдите в подписку Azure совместно с hello tooyour `Login-AzureRmAccount` команды и выполните hello на экране инструкциям.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Создать группу ресурсов

Создайте группу ресурсов Azure с помощью командлета [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Группа ресурсов — это логический контейнер, в котором происходит развертывание ресурсов Azure и управление ими. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a>Создание сетевых ресурсов

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>Создайте виртуальную сеть, подсеть и общедоступный IP-адрес. 
Эти ресурсы, используемые tooprovide сетевого подключения toohello виртуальной машины и подключите его toohello Интернета.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Создайте группу безопасности сети и правило группы безопасности сети. 
группы безопасности сети Hello защищает hello виртуальной машины, с помощью правила входящего и исходящего трафика. В нашем случае создается правило для входящего трафика порта 3389, которое разрешает входящие подключения к удаленному рабочему столу. Также мы хотим toocreate входящее правило для порта 80, который позволяет входящего веб-трафика.

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a>Создайте сетевой карты для hello виртуальной машины. 
Создание сетевого адаптера с [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) для hello виртуальной машины. Hello сетевой адаптер подключается подсети tooa hello виртуальных машин, группы безопасности сети и общедоступный IP-адрес.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Создание виртуальной машины

Создайте конфигурацию виртуальной машины. Такая настройка включает hello параметров, используемых при развертывании виртуальной машины hello, такие как изображения, размер и проверку подлинности конфигурации виртуальной машины. При выполнении этого шага будут запрошены учетные данные. вводимые значения Hello настраиваются как hello имя пользователя и пароль для виртуальной машины hello.

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

Создание виртуальной машины hello с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Подключиться к компьютеру toovirtual

После завершения развертывания hello создания удаленного рабочего стола с виртуальной машиной hello.

Используйте hello [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) команды tooreturn hello общедоступный IP-адрес виртуальной машины hello. Запишите этот IP-адрес для подключения tooit с вашего браузера tootest соединения через сеть на следующем шаге.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

Используйте hello следующая команда toocreate сеанс удаленного рабочего стола с виртуальной машиной hello. Замените hello hello IP-адрес *publicIPAddress* вашей виртуальной машины. При появлении запроса введите hello учетные данные, используемые при создании виртуальной машины hello.

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>Установка IIS с помощью PowerShell

Теперь, когда вы вошли в toohello виртуальной Машине Azure, можно использовать одну строку PowerShell tooinstall IIS и включить hello локальном брандмауэре правило tooallow веб-трафика. Откройте командную строку PowerShell и выполните следующую команду hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Представление hello страницу приветствия IIS

С установленными службами IIS и порт 80, теперь открыт на ВМ из hello Интернета можно использовать веб-браузере choice tooview hello по умолчанию службы IIS страницу приветствия. Быть убедиться, что hello toouse *publicIpAddress* приведенной выше toovisit страница по умолчанию hello. 

![Сайт IIS по умолчанию](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Очистка ресурсов

Если больше не нужны, можно использовать hello [AzureRmResourceGroup удаление](/powershell/module/azurerm.resources/remove-azurermresourcegroup) команд группы ресурсов tooremove hello, виртуальных Машин и все связанные ресурсы.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера. toolearn Дополнительные сведения о виртуальных машинах Azure, продолжить toohello учебника для виртуальных машин Windows.

> [!div class="nextstepaction"]
> [Создание виртуальных машин Windows и управление ими с помощью модуля Azure PowerShell](./tutorial-manage-vm.md)
