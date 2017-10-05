---
title: "Создание виртуальных машин Windows, использующих несколько сетевых адаптеров, и управление ими в Azure | Документация Майкрософт"
description: "Узнайте, как создать виртуальную машину Windows с несколькими сетевыми адаптерами с помощью Azure PowerShell или шаблонов Resource Manager, а также, как управлять ими."
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
ms.openlocfilehash: 3bd99a67dae41de3533d7f6e244eb7ee3ecc4049
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a>Создание виртуальной машины Windows, использующей несколько сетевых адаптеров, и управление ею
Виртуальные машины (VM) в Azure могут иметь несколько виртуальных сетевых адаптеров (NIC). Распространен сценарий, когда разные подсети используются для интерфейсных и внутренних подключений или когда для решения мониторинга либо архивации используется выделенная сеть. В этой статье подробно описывается, как создать виртуальную машину с несколькими сетевыми адаптерами. Вы также узнаете, как добавить или удалить сетевые адаптеры на существующей виртуальной машине. Различные [размеры виртуальных машин](sizes.md) поддерживают разное число сетевых карт, так что выбирайте соответствующий размер виртуальной машины.

Различные дополнительные сведения, а также сведения о том, как создать несколько сетевых адаптеров в собственных сценариях PowerShell, см. в статье [Создание виртуальной машины с несколькими сетевыми интерфейсами с помощью PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="prerequisites"></a>Предварительные требования
Убедитесь, что у вас установлена и настроена [последняя версия Azure PowerShell](/powershell/azure/overview).

В следующих примерах замените имена параметров собственными значениями. Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.


## <a name="create-a-vm-with-multiple-nics"></a>Создание виртуальной машины с несколькими сетевыми адаптерами
Сначала создайте группу ресурсов. В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *EastUs*:

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a>Создание виртуальных сетей и подсетей
Общий сценарий для виртуальной сети с двумя или большим количеством подсетей. Одна подсеть может предназначаться для интерфейсного трафика, а другая — для внутреннего. Чтобы подключиться к двум подсетям, вам необходимо будет использовать несколько сетевых адаптеров на виртуальной машине.

1. Определите две подсети виртуальной сети с помощью [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). В следующем примере определяются подсети для *mySubnetFrontEnd* и *mySubnetBackEnd*:

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. Создайте виртуальную сеть и подсети с помощью командлета [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). В следующем примере создается виртуальная сеть с именем *myVnet*:

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a>Создание нескольких сетевых карт
Создайте два сетевых адаптера с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Подключите один сетевой адаптер к интерфейсной подсети, а другой — к внутренней. В следующем примере создаются два сетевых адаптера с именами *myNic1* и *myNic2*:

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

Обычно также создается [группа безопасности сети](../../virtual-network/virtual-networks-nsg.md) или [балансировщик нагрузки](../../load-balancer/load-balancer-overview.md) для управления трафиком и его распределения между виртуальными машинами. Дополнительные сведения о создании группы безопасности сети и назначении сетевых адаптеров см. в статье [Создание виртуальной машины с несколькими сетевыми интерфейсами с помощью PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

### <a name="create-the-virtual-machine"></a>Создание виртуальной машины
Теперь начните создание конфигурации виртуальной машины. Для каждого размера виртуальной машины существует ограничение на общее количество сетевых карт, которые можно в нее добавить. Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](sizes.md).

1. Задайте переменной `$cred` учетные данные виртуальной машины, как показано ниже:

    ```powershell
    $cred = Get-Credential
    ```

2. Определите виртуальную машину с помощью [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig). В следующем примере определяется виртуальная машина с именем *myVM* и используется размер виртуальной машины, поддерживающий более двух сетевых адаптеров (*Standard_DS3_v2*):

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. Создайте оставшуюся часть конфигурации виртуальной машины с помощью [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) и [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage). В следующем примере создается виртуальная машина Windows Server 2016:

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

4. Подключите два созданных ранее сетевых адаптера с помощью [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. Наконец, создайте виртуальную машину с помощью [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-to-an-existing-vm"></a>Добавление сетевой карты в существующую виртуальную машину
Чтобы добавить виртуальный сетевой адаптер в имеющуюся виртуальную машину, освободите ее, добавьте виртуальный сетевой адаптер, а затем запустите виртуальную машину.

1. Освободите виртуальную машину с помощью командлета [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). В следующем примере освобождается виртуальная машина с именем *myVM* в группе ресурсов *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Получите имеющуюся конфигурацию виртуальной машины с помощью командлета [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). В следующем примере возвращаются сведения для виртуальной машины с именем *myVM* в *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. В следующем примере создается виртуальный сетевой адаптер с помощью [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) с именем *myNic3*, подключенный к *mySubnetBackEnd*. Затем с помощью [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) он подключается к виртуальной машине с именем *myVM* в *myResourceGroup*.

    ```powershell
    # Get info for the back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get the ID of the new virtual NIC and add to VM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a>Главные виртуальные сетевые карты
    Один из сетевых адаптеров на виртуальной машине с несколькими сетевыми картами должен быть главным. Если один из имеющихся виртуальных сетевых адаптеров на виртуальной машине уже используется в качестве главного, вы можете пропустить этот шаг. Чтобы перейти к следующему примеру, предполагается, что на виртуальной машине используются два виртуальных сетевых адаптера. Добавим первый сетевой адаптер (`[0]`) в качестве главного:
        
    ```powershell
    # List existing NICs on the VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 to be primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update the VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. Запустите виртуальную машину с помощью [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a>Удаление сетевой карты из существующей виртуальной машины
Чтобы удалить виртуальный сетевой адаптер с имеющейся виртуальной машины, освободите ее, удалите виртуальный сетевой адаптер, а затем запустите виртуальную машину.

1. Освободите виртуальную машину с помощью командлета [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). В следующем примере освобождается виртуальная машина с именем *myVM* в группе ресурсов *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Получите имеющуюся конфигурацию виртуальной машины с помощью командлета [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). В следующем примере возвращаются сведения для виртуальной машины с именем *myVM* в *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. С помощью [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface) получите сведения об удалении сетевого адаптера. В следующем примере возвращаются сведения о *myNic3*:

    ```powershell
    # List existing NICs on the VM if you need to determine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. Удалите сетевой адаптер с помощью [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface), а затем обновите виртуальную машину с помощью [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm). В следующем примере удаляется сетевой адаптер *myNic3*, полученный `$nicId` на предыдущем шаге:

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. Запустите виртуальную машину с помощью [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a>Создание нескольких сетевых адаптеров с помощью шаблонов
Шаблоны Azure Resource Manager дают возможность создать несколько экземпляров ресурса во время развертывания, в том числе создать несколько сетевых адаптеров. В шаблонах Azure Resource Manager используются декларативные JSON-файлы для определения среды. Дополнительные сведения см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md). Чтобы указать число создаваемых экземпляров, вы можете использовать объект *copy*:

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

Дополнительные сведения см. в статье [Развертывание нескольких экземпляров ресурса или свойства в шаблонах Azure Resource Manager*копирования*](../../resource-group-create-multiple.md). 

Вы также можете использовать `copyIndex()`, чтобы добавить номер к имени ресурса. Затем вы можете создать сетевые адаптеры с именами *myNic1*, *MyNic2* и т. д. Ниже показан пример добавления значения индекса.

```json
"name": "[concat('myNic', copyIndex())]", 
```

Вы можете ознакомиться с полным примером [создания нескольких сетевых адаптеров с помощью шаблонов Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Дальнейшие действия
При создании виртуальной машины с несколькими сетевыми адаптерами ознакомьтесь со статьей [Размеры виртуальных машин Windows в Azure](sizes.md). Обратите внимание на максимальное число сетевых адаптеров, поддерживаемых каждым из размеров виртуальной машины. 


