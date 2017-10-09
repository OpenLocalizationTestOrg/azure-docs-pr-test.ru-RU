---
title: "aaaAzure виртуальных сетей и виртуальных машин Windows | Документы Microsoft"
description: "Руководство по управлению виртуальными сетями Azure и виртуальными машинами Windows с помощью Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Управление виртуальными сетями Azure и виртуальными машинами Windows с помощью Azure PowerShell

Виртуальные машины Azure осуществляют внутреннее и внешнее взаимодействие через сеть Azure. Это руководство содержит сведения о создании нескольких виртуальных машин (ВМ) в виртуальной сети и настройках сетевого взаимодействия между ними. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создать виртуальную сеть
> * Создание подсетей виртуальных сетей
> * Управление сетевым трафиком с помощью групп безопасности сети
> * Просмотр правил трафика в действии

Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).

## <a name="create-vnet"></a>Создание виртуальной сети

Виртуальная сеть — это представление сети в облаке hello. Виртуальная сеть является логической изоляции hello подписки tooyour выделенное облако Azure. В виртуальной сети найти подсетей правила подсети toothose подключения и подключения из подсети toohello hello виртуальных машин.

Перед созданием другие ресурсы Azure, необходимо toocreate группу ресурсов с [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello следующий пример создает группу ресурсов с именем *myRGNetwork* в hello *EastUS* расположение:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

Подсеть является дочерним ресурсом виртуальной сети, который помогает определить сегменты адресных пространств в пределах блока CIDR на основе префиксов IP-адресов. Сетевые адаптеры могут добавляться toosubnets и подключенных tooVMs, предоставляя возможность подключения к для различных рабочих нагрузок.

Создайте подсеть с помощью командлета [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

Создайте виртуальную сеть *myVNet*, использующую *myFrontendSubnet*, выполнив командлет [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a>Создание интерфейсной виртуальной машины

Для виртуальной Машины toocommunicate, в виртуальной сети он должен виртуального сетевого интерфейса (NIC). Hello *myFrontendVM* осуществляется из hello Интернета, поэтому он также требуется общедоступный IP-адрес. 

Создайте общедоступный IP-адрес с помощью командлета [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

Создайте сетевую карту с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

Укажите имя пользователя hello и пароль для учетной записи администратора hello hello виртуальной Машины с [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Создание виртуальных машин hello с [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [набор AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [AzureRmVMSourceImage набор](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Добавить AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), и [новый AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a>Установка веб-сервера

Установить службы IIS на *myFrontendVM* можно с помощью сеанса удаленного рабочего стола. Требуется tooget hello общедоступный IP-адрес виртуальной Машины tooaccess hello его.

Можно получить hello общедоступный IP-адрес *myFrontendVM* с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hello следующий пример извлекает hello IP-адрес для *myPublicIPAddress* созданную ранее:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

Запишите этот IP-адрес, чтобы использовать его в последующих шагах.

Используйте hello следующая команда toocreate сеанс удаленного рабочего стола с *myFrontendVM*. Замените  *<publicIPAddress>*  с адресом hello, ранее сохраненным. При появлении запроса введите hello учетные данные, используемые при создании hello виртуальной Машины.

```
mstsc /v:<publicIpAddress>
``` 

Теперь, когда был выполнен вход слишком*myFrontendVM*, можно использовать одну строку PowerShell tooinstall IIS и включить hello локальном брандмауэре правило tooallow веб-трафика. Откройте командную строку PowerShell и выполните следующую команду hello:

Используйте [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello настраиваемое расширение сценария, устанавливающий веб-сервер IIS hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Теперь можно использовать hello открытый IP адрес toobrowse toohello ВМ toosee hello узла IIS.

![Сайт IIS по умолчанию](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>Управление внутренним трафиком

Группа безопасности сети (NSG) содержит список правил безопасности, которые разрешают или запрещают tooa tooresources подключен сетевой трафик виртуальной сети. Nsg может быть связан toosubnets или tooVMs присоединенного отдельные сетевые адаптеры. Выполняется открытие или закрытие tooVMs доступа к портам с помощью правила NSG. При создании *myFrontendVM* входящий порт 3389 автоматически был открыт для RDP-подключений.

С помощью группы безопасности сети можно настроить взаимодействие внутри виртуальных машин. В этом разделе вы узнаете, как toocreate дополнительные подсети в hello сети и назначить соединение из NSG tooit tooallow *myFrontendVM* слишком*myBackendVM* через порт 1433. подсети Hello назначается toohello виртуальной Машины при ее создании.

Можно ограничить внутренний трафик слишком*myBackendVM* только от *myFrontendVM* путем создания NSG для hello внутренней подсети. Hello следующий пример создает NSG правило с именем *myBackendNSGRule* с [New AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

Добавьте группу безопасности сети *myBackendNSG* с помощью командлета [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a>Добавление внутренней подсети

Добавить *myBackEndSubnet* слишком*myVNet* с [AzureRmVirtualNetworkSubnetConfig добавить](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a>Создание внутренней виртуальной машины

Hello простым способом toocreate hello внутренней виртуальной Машины можно с помощью образа SQL Server. Этот учебник только создает hello виртуальной Машины с сервером базы данных hello, но не предоставляет сведения о доступе к базе данных hello.

Создайте *myBackendNic*.

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Задайте hello имя пользователя и пароль для учетной записи администратора hello hello виртуальной Машины с помощью Get-Credential.

```powershell
$cred = Get-Credential
```

Создайте *myBackendVM*.

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

Hello изображение, используемое установлен SQL Server, но не используется в этом учебнике. Это включается tooshow вы Настройка веб-трафик toohandle ВМ и управление виртуальными Машинами toohandle базы данных.

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике создается и защищенных сетей Azure как связанные toovirtual машины. 

> [!div class="checklist"]
> * Создать виртуальную сеть
> * Создание подсетей виртуальных сетей
> * Управление сетевым трафиком с помощью групп безопасности сети
> * Просмотр правил трафика в действии

Переместить следующий учебник toolearn toohello о наблюдении за обеспечение безопасности данных на виртуальных машинах с помощью резервного копирования Azure. .

> [!div class="nextstepaction"]
> [Архивация виртуальных машин Windows в Azure](./tutorial-backup-vms.md)
