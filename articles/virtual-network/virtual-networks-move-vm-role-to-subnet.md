---
title: "aaaMove (классические) виртуальной Машины или облачные службы роли экземпляра tooa другой подсети - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как toomove виртуальные машины (классические) и облачные службы роли экземпляров tooa другой подсети, с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a>Перемещение виртуальной Машины (классические) или облачные службы роли экземпляра tooa другой подсети с помощью PowerShell
В можно использовать PowerShell toomove виртуальные машины (классические) из одной подсети tooanother hello одной виртуальной сети (VNet). Экземпляры роли можно перемещать путем редактирования файла CSCFG hello, а не с помощью PowerShell.

> [!NOTE]
> В этой статье объясняется, как развернутые виртуальные машины toomove с помощью hello классической модели развертывания только.
> 
> 

Зачем перемещать виртуальные машины подсети tooanother? Подсеть миграции полезно, когда старая подсеть hello слишком мал и не могут быть развернуты из-за tooexisting работающих виртуальных машин в этой подсети. В этом случае можно создать новый, больший подсети и перенести hello виртуальные машины toohello новую подсеть, а затем после завершения миграции можно удалить старые пустой подсети hello.

## <a name="how-toomove-a-vm-tooanother-subnet"></a>Как toomove tooanother подсеть виртуальной Машины
toomove виртуальную Машину, выполните командлет PowerShell Set-AzureSubnet hello, используя в качестве шаблона пример hello ниже. В следующем примере hello, выполняется перемещение TestVM из старой подсети tooSubnet-2. Быть убедиться, что tooreflect пример hello tooedit вашей среде. Обратите внимание, что при каждом выполнении командлета Update-AzureVM hello в рамках процедуры, она будет перезагружать вашу ВМ в рамках процесса обновления hello.

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

Если указан статический внутренний частных IP-адрес для ВМ, вы получите tooclear эту настройку перед перемещением hello ВМ tooa новую подсеть. В этом случае используйте hello ниже:

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a>toomove подсети tooanother экземпляра роли
toomove экземпляра роли, измените файл CSCFG hello. В следующем примере hello, выполняется перемещение «Role0» в виртуальной сети *VNETName* из старой подсети слишком*Subnet-2*. Поскольку экземпляр роли hello уже был развернут, достаточно изменить имя подсети hello = Subnet-2. Быть убедиться, что tooreflect пример hello tooedit вашей среде.

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
