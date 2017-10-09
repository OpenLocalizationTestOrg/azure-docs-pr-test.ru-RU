---
title: "aaaCreate и управление виртуальными машинами Windows в Azure, использовать несколько сетевых адаптеров | Документы Microsoft"
description: "Узнайте, как toocreate и управление виртуальной Машины Windows с несколькими tooit подключенных сетевых адаптеров, используя шаблоны Azure PowerShell или диспетчер ресурсов."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a>Создание виртуальной машины Windows, использующей несколько сетевых адаптеров, и управление ею
Виртуальные машины (ВМ в Azure) может иметь несколько toothem карты (NIC) присоединенного интерфейс виртуальной сети. Типичный сценарий состоит в разных подсетях toohave для внешнего и внутреннего интерфейса подключения или сеть, выделенная tooa наблюдения или решение для резервного копирования. В этой статье указаны как toocreate виртуальной Машины с несколькими сетевыми картами присоединенного tooit. Вы также узнаете, как tooadd или удаление сетевых адаптеров в существующей виртуальной Машины. Различные [размеры виртуальных машин](sizes.md) поддерживают разное число сетевых карт, так что выбирайте соответствующий размер виртуальной машины.

Дополнительные сведения, включая toocreate несколько сетевых адаптеров в собственных сценариев PowerShell см. в [развертывание виртуальных машин с несколькими сетевыми Картами](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="prerequisites"></a>Предварительные требования
Убедитесь, что имеется hello [последнюю версию Azure PowerShell устанавливается и настраивается](/powershell/azure/overview).

В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.


## <a name="create-a-vm-with-multiple-nics"></a>Создание виртуальной машины с несколькими сетевыми адаптерами
Сначала создайте группу ресурсов. Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *EastUs* расположение:

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a>Создание виртуальных сетей и подсетей
Распространенным сценарием является для toohave виртуальной сети двух или нескольких подсетях. Одна подсеть может быть трафика переднего плана, hello других для трафика серверной части. tooconnect tooboth подсети, после этого использовать несколько сетевых адаптеров на виртуальной Машине.

1. Определите две подсети виртуальной сети с помощью [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Hello следующий пример определяет hello подсетей для *mySubnetFrontEnd* и *mySubnetBackEnd*:

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. Создайте виртуальную сеть и подсети с помощью командлета [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hello следующий пример создает виртуальную сеть с именем *myVnet*:

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a>Создание нескольких сетевых карт
Создайте два сетевых адаптера с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Присоедините одну подсеть сетевого Адаптера toohello переднего плана и одной подсети внутренней toohello сетевого Адаптера. Hello следующий пример создает сетевых адаптеров с именем *myNic1* и *myNic2*:

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

Обычно также создать [сетевой группы безопасности](../../virtual-network/virtual-networks-nsg.md) или [подсистемы балансировки нагрузки](../../load-balancer/load-balancer-overview.md) toohelp управлять и распределять трафик между виртуальных машин. Hello [более подробные виртуальной Машины нескольких Сетевых](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) статье описывается создание группы безопасности сети и назначение сетевых адаптеров.

### <a name="create-hello-virtual-machine"></a>Создание виртуальной машины hello
Теперь запустите toobuild конфигурации своей виртуальной Машины. Размер каждой виртуальной Машины имеет ограничение hello общее количество сетевых адаптеров, вы можете добавить tooa виртуальной Машины. Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](sizes.md).

1. Задайте учетные данные вашей виртуальной Машины toohello `$cred` переменной следующим образом:

    ```powershell
    $cred = Get-Credential
    ```

2. Определите виртуальную машину с помощью [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig). Hello следующий пример определяет Виртуальную машину с именем *myVM* и использует размер виртуальной Машины, которая поддерживает более двух сетевых адаптеров (*Standard_DS3_v2*):

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. Создание hello остальной части конфигурации своей виртуальной Машины с [набор AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) и [AzureRmVMSourceImage набор](/powershell/module/azurerm.compute/set-azurermvmsourceimage). Следующий пример Hello создает виртуальную Машину Windows Server 2016:

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. Присоединение hello двух сетевых адаптеров, которые были созданы ранее с [AzureRmVMNetworkInterface добавить](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. Наконец, создайте виртуальную машину с помощью [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a>Добавьте сетевой Адаптер tooan существующей виртуальной Машины
tooadd виртуального сетевого Адаптера tooan существующих виртуальных Машин, deallocate hello виртуальной Машины, добавьте hello виртуальный сетевой Адаптер, а затем запустить hello виртуальной Машины.

1. DEALLOCATE hello виртуальной Машины с [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM* в *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Получить конфигурацию существующего hello hello виртуальной Машины с [Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Hello следующий пример получает сведения для виртуальной Машины с именем hello *myVM* в *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Hello следующем примере создается виртуальный сетевой Адаптер с [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) с именем *myNic3* слишком присоединяется*mySubnetBackEnd*. Привет, виртуальный сетевой Адаптер будет подключен toohello виртуальной Машины с именем *myVM* в *myResourceGroup* с [AzureRmVMNetworkInterface добавить](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a>Главные виртуальные сетевые карты
    Один из сетевых адаптеров на виртуальной Машине multi-NIC hello должен toobe первичной. Если один из hello существующих виртуальных сетевых адаптеров на hello виртуальная машина уже задан как первичный, этот шаг можно пропустить. Hello в примере предполагается, что два виртуальных сетевых адаптеров на виртуальной Машине теперь присутствуют и вы хотите tooadd hello первый сетевой Адаптер (`[0]`) как основной hello:
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. Запуск hello виртуальной Машины с [AzureRmVm начала](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a>Удаление сетевой карты из существующей виртуальной машины
tooremove виртуальный сетевой Адаптер из существующей виртуальной Машины, можно освободить hello виртуальной Машины, удалите hello виртуальный сетевой Адаптер, а затем hello запуска виртуальной Машины.

1. DEALLOCATE hello виртуальной Машины с [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM* в *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Получить конфигурацию существующего hello hello виртуальной Машины с [Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Hello следующий пример получает сведения для виртуальной Машины с именем hello *myVM* в *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Получение сведений о hello, удалите сетевой Адаптер с [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface). Hello следующий пример возвращает сведения *myNic3*:

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. Удалите hello сетевого Адаптера с [удаление AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) и только затем hello виртуальной Машины с [AzureRmVm обновление](/powershell/module/azurerm.compute/update-azurermvm). Hello следующий пример удаляет *myNic3* полученных `$nicId` в hello предшествующий шаг:

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. Запуск hello виртуальной Машины с [AzureRmVm начала](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a>Создание нескольких сетевых адаптеров с помощью шаблонов
Шаблоны Azure Resource Manager предоставить несколько экземпляров ресурса toocreate образом во время развертывания, таких как создание нескольких сетевых адаптеров. Шаблоны диспетчера ресурсов среду использовать декларативные toodefine файлы JSON. Дополнительные сведения см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md). Можно использовать *копирования* toospecify hello число экземпляров toocreate:

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

Дополнительные сведения см. в статье [Развертывание нескольких экземпляров ресурса или свойства в шаблонах Azure Resource Manager*копирования*](../../resource-group-create-multiple.md). 

Можно также использовать `copyIndex()` tooappend номеров tooa имя ресурса. Затем вы можете создать сетевые адаптеры с именами *myNic1*, *MyNic2* и т. д. Hello следующий код является примером добавления hello значение индекса:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Вы можете ознакомиться с полным примером [создания нескольких сетевых адаптеров с помощью шаблонов Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите [размеры виртуальных Машин Windows](sizes.md) когда вы пытаетесь toocreate виртуальной Машины, которая имеет несколько сетевых адаптеров. Обратите внимание toohello максимальное количество сетевых адаптеров, поддерживаемых для каждого размера виртуальной Машины. 


