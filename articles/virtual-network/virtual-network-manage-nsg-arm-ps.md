---
title: "aaaManage сетевых групп безопасности - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как toomanage сетевых групп безопасности, с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a>Управление группами безопасности сети с помощью PowerShell

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md). В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a>Извлечение информации
Вы можете просмотреть существующие группы безопасности сети, получить правила для существующей группы и узнать, с какими ресурсами она связана.

### <a name="view-existing-nsgs"></a>Просмотр существующих групп безопасности сети
tooview все существующие Nsg в подписке, запустите hello `Get-AzureRmNetworkSecurityGroup` командлета.

Ожидаемый результат:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


tooview списка Nsg hello в определенной группе ресурсов, запустите hello `Get-AzureRmNetworkSecurityGroup` командлета.

Ожидаемые выходные данные:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a>Перечисление всех правил для группы безопасности сети
tooview hello правила NSG с именем **NSG-FrontEnd**, введите следующую команду hello:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

Ожидаемые выходные данные:

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> Можно также использовать `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist правила по умолчанию hello из hello **NSG-FrontEnd** NSG.
> 

### <a name="view-nsgs-associations"></a>Просмотр связей для группы безопасности сети
tooview какие ресурсы hello **NSG-FrontEnd** NSG — связан с, запустите hello следующую команду:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

Найдите hello **сетевых интерфейсов** и **подсети** свойства, как показано ниже:

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

В предыдущем примере hello hello NSG не связан tooany сетевых интерфейсов (NIC); Это связанный tooa подсеть с именем **переднего плана**.

## <a name="manage-rules"></a>Управление правилами
Добавление существующей NSG tooan правила, изменять существующие правила и удалять правила.

### <a name="add-a-rule"></a>Добавление правила
tooadd правила, что позволяет **входящих** tooport трафика **443** с любого компьютера toohello **NSG-FrontEnd** NSG завершения hello, следующие шаги:

1. Выполните hello, следующая команда tooretrieve hello существующей NSG и сохранить его в переменной.

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Выполните следующие команды tooadd hello toohello правила NSG:

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. Запустите следующую команду hello toohello NSG, внесены изменения toosave hello.

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    Отображение только hello правила безопасности ожидаемый результат:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a>Изменение правила
правило toochange hello, созданной ранее tooallow входящий трафик от hello **Internet** , выполните следующие шаги hello.

1. Выполните hello, следующая команда tooretrieve hello существующей NSG и сохранить его в переменной.

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Выполните следующую команду с новыми настройками правило hello hello.

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. Запустите следующую команду hello toohello NSG, внесены изменения toosave hello.

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Отображение только hello правила безопасности ожидаемый результат:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a>Удаление правила
1. Выполните hello, следующая команда tooretrieve hello существующей NSG и сохранить его в переменной.

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Выполните следующую команду tooremove hello правила из hello NSG hello.

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. Сохраните изменения, внесенные hello toohello NSG, выполнив следующую команду hello:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Ожидаемый результат, отображаются только hello правил безопасности, уведомление hello **https правило** больше не отображается:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a>Управление связями
Можно связать NSG toosubnets и сетевых адаптеров. Можно также отменить связь группы безопасности сети с любым ресурсом.

### <a name="associate-an-nsg-tooa-nic"></a>Связывание NSG tooa сетевого Адаптера
tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** сетевого Адаптера, полный hello, следующие шаги:

1. Выполните hello, следующая команда tooretrieve hello существующей NSG и сохранить его в переменной.

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Выполните hello, следующая команда tooretrieve hello существующего сетевого Адаптера и сохранить его в переменной.

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. Набор hello **NetworkSecurityGroup** свойство hello **Сетевых** значение переменной toohello hello **NSG** переменных, введя следующую команду hello:

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. toohello сетевого Адаптера, запустите следующую команду hello внесены изменения toosave hello.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Ожидаемый результат отображение только hello **NetworkSecurityGroup** свойства:
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a>Отмена связи с сетевым адаптером для группы безопасности сети
toodissociate hello **NSG-FrontEnd** NSG из hello **TestNICWeb1** сетевого Адаптера, полный hello, следующие шаги:

1. Выполните hello, следующая команда tooretrieve hello существующего сетевого Адаптера и сохранить его в переменной.

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. Набор hello **NetworkSecurityGroup** свойство hello **Сетевых** переменной слишком**$null** , выполнив следующую команду hello:

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. toohello сетевого Адаптера, запустите следующую команду hello внесены изменения toosave hello.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Ожидаемый результат отображение только hello **NetworkSecurityGroup** свойства:
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a>Отмена связи с подсетью для группы безопасности сети
toodissociate hello **NSG-FrontEnd** NSG из hello **переднего плана** подсети, полный hello, следующие шаги:

1. Выполните hello, следующая команда tooretrieve hello существующей виртуальной сети и сохранить его в переменной.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Выполнения hello следующие команда hello tooretrieve **переднего плана** подсети и сохранить его в переменной:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Набор hello **NetworkSecurityGroup** свойство hello **подсети** переменной слишком**$null** , введя hello следующую команду:

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. toohello подсети, запустите следующую команду hello внесены изменения toosave hello.

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Ожидаемый результат, отображаются только hello свойств hello **переднего плана** подсети. Обратите внимание, что свойства **NetworkSecurityGroup**нет:
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a>Связывание NSG tooa подсети
tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** снова подсети, полный hello, следующие шаги:

1. Выполните hello, следующая команда tooretrieve hello существующей виртуальной сети и сохранить его в переменной.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Выполнения hello следующие команда hello tooretrieve **переднего плана** подсети и сохранить его в переменной:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Выполните hello, следующая команда tooretrieve hello существующей NSG и сохранить его в переменной.

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. Набор hello **NetworkSecurityGroup** свойство hello **подсети** переменной слишком**$null** , выполнив следующую команду hello:

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. toohello подсети, запустите следующую команду hello внесены изменения toosave hello.

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Ожидаемый результат отображение только hello **NetworkSecurityGroup** свойство hello **переднего плана** подсети:
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a>Удаление группы NSG
NSG можно удалить только в том случае, если она не сопоставлена tooany ресурсов. toodelete NSG, выполните следующие действия hello.

1. ресурсы hello toocheck связанные tooan NSG, запустите hello `azure network nsg show` как показано в [связи Nsg представление](#View-NSGs-associations).
2. Если hello NSG связанные tooany сетевых адаптеров, запустите hello `azure network nic set` как показано в [связь между Сетевыми NSG](#Dissociate-an-NSG-from-a-NIC) для каждого сетевого адаптера. 
3. Если hello NSG связанные tooany подсети, запустите hello `azure network vnet subnet set` как показано в [связь NSG из подсети](#Dissociate-an-NSG-from-a-subnet) для каждой подсети.
4. hello toodelete NSG, запустите hello следующую команду:

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > Hello `-Force` параметр гарантирует удаление hello tooconfirm не требуется.
   > 

## <a name="next-steps"></a>Дальнейшие действия
* [Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.

