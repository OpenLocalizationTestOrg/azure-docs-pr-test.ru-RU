---
title: "aaaMove ресурс виртуальной Машины Windows в Azure | Документы Microsoft"
description: "Переместите tooanother виртуальной Машины Windows Azure подписка или группа ресурсов в модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a>Перемещение виртуальной Машины Windows tooanother подписки Azure или группы ресурсов
В этой статье описано, как toomove ВМ Windows между группами ресурсов или подписок. Перемещение между подписками может оказаться удобным, которые использовались при создании виртуальной Машины в личные подписки, а теперь нужно toomove его toocontinue подписки компании tooyour свою работу.

> [!IMPORTANT]
>В настоящее время переместить управляемые диски невозможно. 
>
>В процессе перемещения hello создаются новые идентификаторы ресурсов. После hello ВМ был перемещен, вам потребуется tooupdate вашей средства и сценарии toouse hello новые идентификаторы ресурсов. 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a>Используйте Powershell toomove виртуальной Машины
toomove tooanother группы ресурсов виртуальной машины, необходимо убедиться, что также переместить все зависимые ресурсы hello toomake. командлет Move-AzureRMResource toouse hello, нужны имя ресурса hello и hello тип ресурса. Можно получить из командлета Find-AzureRMResource hello.

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


toomove мы должны toomove несколько ресурсов виртуальной Машины. Можно просто создать для каждого ресурса отдельные переменные, а затем перечислить их. В этом примере включает большую часть hello основные ресурсы для виртуальной Машины, но можно добавить несколько при необходимости.

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

toomove Здравствуйте подписки toodifferent ресурсы, включают hello **- DestinationSubscriptionId** параметра. 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



Будет выведено ресурсов, указанных tooconfirm, что требуется toomove hello. Тип **Y** tooconfirm, что требуется toomove hello ресурсы.

## <a name="next-steps"></a>Дальнейшие действия
Вы можете перемещать разные типы ресурсов между группами ресурсов и подписками. Дополнительные сведения см. в разделе [переместить группу ресурсов toonew ресурсов или подписку](../../resource-group-move-resources.md).    

