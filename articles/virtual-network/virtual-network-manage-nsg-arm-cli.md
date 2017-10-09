---
title: "aaaManage сетевых групп безопасности - CLI Azure 2.0 | Документы Microsoft"
description: "Узнайте, как с помощью групп безопасности сети toomanage hello Azure командной строки (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed17d314-07e6-4c7f-bcf1-a8a2535d7c14
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a3036b465e1e4049cba00e5e13ce1b479a2301d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a>Управление группами безопасности сети с помощью Azure CLI 2.0 hello

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI 

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello. 

- [Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления 
- [Azure CLI 2.0](#View-existing-NSGs) -нашей нового поколения CLI для модели развертывания управления hello ресурсов (в этой статье)


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md). В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a>Предварительные требования
Если еще не еще, установить и настроить hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login). 


## <a name="view-existing-nsgs"></a>Просмотр существующих групп безопасности сети
tooview списка Nsg hello в определенной группе ресурсов, запустите hello [az сетевой nsg список](/cli/azure/network/nsg#list) с `-o table` формат вывода:

```azurecli
az network nsg list -g RG-NSG -o table
```

Ожидаемые выходные данные:

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a>Перечисление всех правил для группы безопасности сети
tooview hello правила NSG с именем **NSG-FrontEnd**, запустите hello [nsg Показать az сети](/cli/azure/network/nsg#show) команду с помощью [фильтр запроса JMESPATH](/cli/azure/query-az-cli2) и hello `-o table` формат вывода:

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

Ожидаемые выходные данные:

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs tooall VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs tooInternet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> Можно также использовать [список правил az сети nsg](/cli/azure/network/nsg/rule#list) toolist только hello настраиваемые правила из NSG.
>

## <a name="view-nsg-associations"></a>Просмотр связей для группы безопасности сети

tooview какие ресурсы hello **NSG-FrontEnd** NSG — hello связан с, запустите `az network nsg show` команды, как показано ниже. 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

Найдите hello **сетевых интерфейсов** и **подсети** свойства, как показано ниже:

```json
[
  [
    {
      "addressPrefix": null,
      "etag": null,
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
      "ipConfigurations": null,
      "name": null,
      "networkSecurityGroup": null,
      "provisioningState": null,
      "resourceGroup": "RG-NSG",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  null
]
```

В приведенном выше примере hello, hello NSG не связан tooany сетевых интерфейсов (NIC), и это связанный tooa подсеть с именем **переднего плана**.

## <a name="add-a-rule"></a>Добавление правила
tooadd правило, что позволяет **входящий** tooport трафика **443** с любого компьютера toohello **NSG-FrontEnd** NSG, введите следующую команду hello:

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access tooport 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

Ожидаемые выходные данные:

```json
{
  "access": "Allow",
  "description": "Allow access tooport 443 for HTTPS",
  "destinationAddressPrefix": "*",
  "destinationPortRange": "443",
  "direction": "Inbound",
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
  "name": "allow-https",
  "priority": 102,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

## <a name="change-a-rule"></a>Изменение правила
правило toochange hello, созданной ранее tooallow входящий трафик от hello **Internet** выполняться hello [обновления правила nsg сети az](/cli/azure/network/nsg/rule#update) команды:

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

Ожидаемые выходные данные:

```json
{
"access": "Allow",
"description": "Allow access tooport 443 for HTTPS",
"destinationAddressPrefix": "*",
"destinationPortRange": "443",
"direction": "Inbound",
"etag": "W/\"<guid>\"",
"id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
"name": "allow-https",
"priority": 102,
"protocol": "Tcp",
"provisioningState": "Succeeded",
"resourceGroup": "RG-NSG",
"sourceAddressPrefix": "Internet",
"sourcePortRange": "*"
}
```

## <a name="delete-a-rule"></a>Удаление правила
toodelete hello создано правило выше, запустите hello следующую команду:

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a>Связывание NSG tooa сетевого Адаптера
tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** сетевого Адаптера, используйте hello [обновления сетевого адаптера сети az](/cli/azure/network/nic#update) команды:

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

Ожидаемые выходные данные:

```json
{
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": [],
    "internalDnsNameLabel": null,
    "internalDomainNameSuffix": "k0wkaguidnqrh0ud.gx.internal.cloudapp.net",
    "internalFqdn": null
  },
  "enableAcceleratedNetworking": false,
  "enableIpForwarding": false,
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1",
  "ipConfigurations": [
    {
      "applicationGatewayBackendAddressPools": null,
      "etag": "W/\"<guid>\"",
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1",
      "loadBalancerBackendAddressPools": null,
      "loadBalancerInboundNatRules": null,
      "name": "ipconfig1",
      "primary": true,
      "privateIpAddress": "192.168.1.6",
      "privateIpAddressVersion": "IPv4",
      "privateIpAllocationMethod": "Static",
      "provisioningState": "Succeeded",
      "publicIpAddress": null,
      "resourceGroup": "RG-NSG",
      "subnet": {
        "addressPrefix": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
        "ipConfigurations": null,
        "name": null,
        "networkSecurityGroup": null,
        "provisioningState": null,
        "resourceGroup": "RG-NSG",
        "resourceNavigationLinks": null,
        "routeTable": null
      }
    }
  ],
  "location": "centralus",
  "macAddress": "00-0D-3A-91-A9-60",
  "name": "TestNICWeb1",
  "networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  },
  "primary": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "resourceGuid": "<guid>",
  "tags": {},
  "type": "Microsoft.Network/networkInterfaces",
  "virtualMachine": null
}
```

## <a name="dissociate-an-nsg-from-a-nic"></a>Отмена связи с сетевым адаптером для группы безопасности сети

toodissociate hello **NSG-FrontEnd** NSG из hello **TestNICWeb1** сетевого Адаптера, запустите hello [обновления правила nsg сети az](/cli/azure/network/nsg/rule#update) еще раз, но заменить hello `--network-security-group` аргумент с пустой строкой (`""`).

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

В выходных данных hello hello `networkSecurityGroup` toonull задан ключ.

## <a name="dissociate-an-nsg-from-a-subnet"></a>Отмена связи с подсетью для группы безопасности сети
toodissociate hello **NSG-FrontEnd** NSG из hello **переднего плана** подсети, снова запустите hello [обновления правила nsg сети az](/cli/azure/network/nsg/rule#update) еще раз, но заменить hello `--network-security-group` аргумент с пустой строкой (`""`).

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

В выходных данных hello hello `networkSecurityGroup` toonull задан ключ.

## <a name="associate-an-nsg-tooa-subnet"></a>Связывание NSG tooa подсети
tooassociate hello **NSG-FrontEnd** NSG toohello **переднего плана** подсети опять-таки выполняются hello следующую команду:

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

В выходных данных hello hello `networkSecurityGroup` ключ имеет аналогичную для hello значения:

```json
"networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  }
  ```

## <a name="delete-an-nsg"></a>Удаление группы NSG
NSG можно удалить только в том случае, если она не сопоставлена tooany ресурсов. toodelete NSG, выполните следующие действия hello.

1. ресурсы hello toocheck связанные tooan NSG, запустите hello `azure network nsg show` как показано в [связи Nsg представление](#View-NSGs-associations).
2. Если hello NSG связанные tooany сетевых адаптеров, запустите hello `azure network nic set` как показано в [связь между Сетевыми NSG](#Dissociate-an-NSG-from-a-NIC) для каждого сетевого адаптера. 
3. Если hello NSG связанные tooany подсети, запустите hello `azure network vnet subnet set` как показано в [связь NSG из подсети](#Dissociate-an-NSG-from-a-subnet) для каждой подсети.
4. hello toodelete NSG, запустите hello следующую команду:

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a>Дальнейшие действия
* [Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.

