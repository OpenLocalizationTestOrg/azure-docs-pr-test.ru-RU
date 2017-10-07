---
title: "aaaOpen порты tooa виртуальную Машину с помощью Azure PowerShell | Документы Microsoft"
description: "Узнайте, как tooopen порт / create tooyour конечной точки виртуальной Машины Windows с помощью режима развертывания диспетчера ресурсов Azure hello и Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a>Как tooopen портов и конечные точки tooa ВМ в Azure с помощью PowerShell
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Быстрые команды
Группы безопасности сети toocreate и правила ACL необходимо [hello последнюю версию Azure PowerShell установлена](/powershell/azureps-cmdlets-docs). Вы также можете [выполните следующие действия с помощью портала Azure hello](nsg-quickstart-portal.md).

Вход tooyour учетная запись Azure:

```powershell
Login-AzureRmAccount
```

В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.

Создайте правило с помощью командлета [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Hello следующий код создает правило с именем *myNetworkSecurityGroupRule* tooallow *tcp* трафик через порт *80*:

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

Создайте группу безопасности сети [New AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) и назначить правило hello HTTP, только что созданный следующим образом. Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup*:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

Теперь давайте назначить подсети tooa группы безопасности сети. Hello следующий пример назначает существующую виртуальную сеть с именем *myVnet* переменной toohello *$vnet* с [Get AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

Свяжите группу безопасности сети с подсетью с помощью командлета [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig): Hello следующий пример связывает hello подсеть с именем *mySubnet* с вашей сетевой группы безопасности:

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

Наконец, обновления виртуальной сети с [AzureRmVirtualNetwork набора](/powershell/module/azurerm.network/set-azurermvirtualnetwork) в порядке для изменения эффекта tootake:

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a>Дополнительная информация о группах безопасности сети
Hello здесь Быстрые команды позволяют tooget вверх и работает с tooyour передачу трафика виртуальных Машин. Сетевые группы безопасности предоставляют много замечательных функций и гранулярности для управления доступа к ресурсам tooyour. [Здесь](tutorial-virtual-network.md#manage-internal-traffic)вы можете больше прочитать о создании группы безопасности сети и правил ACL.

Для веб-приложений с высокой доступностью необходимо поместить виртуальную машину за Azure Load Balancer. Подсистема балансировки нагрузки Hello распределяет трафик tooVMs, с группой безопасности сети, которая обеспечивает фильтрацию трафика. Дополнительные сведения см. в разделе [как баланс tooload Linux виртуальных машин в Azure toocreate приложение с высокой доступностью](tutorial-load-balancer.md).

## <a name="next-steps"></a>Дальнейшие действия
В этом примере вы создали трафика tooallow HTTP простое правило. Можно найти сведения о создании более подробные сред в hello в следующих статьях:

* [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md)
* [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](../../load-balancer/load-balancer-arm.md)

