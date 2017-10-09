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
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="ad753-103">Управление группами безопасности сети с помощью Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="ad753-103">Manage network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ad753-104">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="ad753-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="ad753-105">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="ad753-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="ad753-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) — нашей CLI для hello классический и ресурсов развертывания модели управления</span><span class="sxs-lookup"><span data-stu-id="ad753-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="ad753-107">[Azure CLI 2.0](#View-existing-NSGs) -нашей нового поколения CLI для модели развертывания управления hello ресурсов (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="ad753-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for hello resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="ad753-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ad753-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ad753-109">В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ad753-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="ad753-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ad753-110">Prerequisite</span></span>
<span data-ttu-id="ad753-111">Если еще не еще, установить и настроить hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ad753-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="ad753-112">Просмотр существующих групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="ad753-112">View existing NSGs</span></span>
<span data-ttu-id="ad753-113">tooview списка Nsg hello в определенной группе ресурсов, запустите hello [az сетевой nsg список](/cli/azure/network/nsg#list) с `-o table` формат вывода:</span><span class="sxs-lookup"><span data-stu-id="ad753-113">tooview hello list of NSGs in a specific resource group, run hello [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="ad753-114">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ad753-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="ad753-115">Перечисление всех правил для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="ad753-115">List all rules for an NSG</span></span>
<span data-ttu-id="ad753-116">tooview hello правила NSG с именем **NSG-FrontEnd**, запустите hello [nsg Показать az сети](/cli/azure/network/nsg#show) команду с помощью [фильтр запроса JMESPATH](/cli/azure/query-az-cli2) и hello `-o table` формат вывода:</span><span class="sxs-lookup"><span data-stu-id="ad753-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and hello `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="ad753-117">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ad753-117">Expected output:</span></span>

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
> <span data-ttu-id="ad753-118">Можно также использовать [список правил az сети nsg](/cli/azure/network/nsg/rule#list) toolist только hello настраиваемые правила из NSG.</span><span class="sxs-lookup"><span data-stu-id="ad753-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) toolist only hello custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="ad753-119">Просмотр связей для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="ad753-119">View NSG associations</span></span>

<span data-ttu-id="ad753-120">tooview какие ресурсы hello **NSG-FrontEnd** NSG — hello связан с, запустите `az network nsg show` команды, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ad753-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="ad753-121">Найдите hello **сетевых интерфейсов** и **подсети** свойства, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="ad753-121">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

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

<span data-ttu-id="ad753-122">В приведенном выше примере hello, hello NSG не связан tooany сетевых интерфейсов (NIC), и это связанный tooa подсеть с именем **переднего плана**.</span><span class="sxs-lookup"><span data-stu-id="ad753-122">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="ad753-123">Добавление правила</span><span class="sxs-lookup"><span data-stu-id="ad753-123">Add a rule</span></span>
<span data-ttu-id="ad753-124">tooadd правило, что позволяет **входящий** tooport трафика **443** с любого компьютера toohello **NSG-FrontEnd** NSG, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ad753-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

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

<span data-ttu-id="ad753-125">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ad753-125">Expected output:</span></span>

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

## <a name="change-a-rule"></a><span data-ttu-id="ad753-126">Изменение правила</span><span class="sxs-lookup"><span data-stu-id="ad753-126">Change a rule</span></span>
<span data-ttu-id="ad753-127">правило toochange hello, созданной ранее tooallow входящий трафик от hello **Internet** выполняться hello [обновления правила nsg сети az](/cli/azure/network/nsg/rule#update) команды:</span><span class="sxs-lookup"><span data-stu-id="ad753-127">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="ad753-128">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ad753-128">Expected output:</span></span>

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

## <a name="delete-a-rule"></a><span data-ttu-id="ad753-129">Удаление правила</span><span class="sxs-lookup"><span data-stu-id="ad753-129">Delete a rule</span></span>
<span data-ttu-id="ad753-130">toodelete hello создано правило выше, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ad753-130">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="ad753-131">Связывание NSG tooa сетевого Адаптера</span><span class="sxs-lookup"><span data-stu-id="ad753-131">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="ad753-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** сетевого Адаптера, используйте hello [обновления сетевого адаптера сети az](/cli/azure/network/nic#update) команды:</span><span class="sxs-lookup"><span data-stu-id="ad753-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, use hello [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="ad753-133">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ad753-133">Expected output:</span></span>

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

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="ad753-134">Отмена связи с сетевым адаптером для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="ad753-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="ad753-135">toodissociate hello **NSG-FrontEnd** NSG из hello **TestNICWeb1** сетевого Адаптера, запустите hello [обновления правила nsg сети az](/cli/azure/network/nsg/rule#update) еще раз, но заменить hello `--network-security-group` аргумент с пустой строкой (`""`).</span><span class="sxs-lookup"><span data-stu-id="ad753-135">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="ad753-136">В выходных данных hello hello `networkSecurityGroup` toonull задан ключ.</span><span class="sxs-lookup"><span data-stu-id="ad753-136">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="ad753-137">Отмена связи с подсетью для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="ad753-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="ad753-138">toodissociate hello **NSG-FrontEnd** NSG из hello **переднего плана** подсети, снова запустите hello [обновления правила nsg сети az](/cli/azure/network/nsg/rule#update) еще раз, но заменить hello `--network-security-group` аргумент с пустой строкой (`""`).</span><span class="sxs-lookup"><span data-stu-id="ad753-138">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, again run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="ad753-139">В выходных данных hello hello `networkSecurityGroup` toonull задан ключ.</span><span class="sxs-lookup"><span data-stu-id="ad753-139">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="ad753-140">Связывание NSG tooa подсети</span><span class="sxs-lookup"><span data-stu-id="ad753-140">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="ad753-141">tooassociate hello **NSG-FrontEnd** NSG toohello **переднего плана** подсети опять-таки выполняются hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ad753-141">tooassociate hello **NSG-FrontEnd** NSG toohello **FrontEnd** subnet again, run hello following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="ad753-142">В выходных данных hello hello `networkSecurityGroup` ключ имеет аналогичную для hello значения:</span><span class="sxs-lookup"><span data-stu-id="ad753-142">In hello output, hello `networkSecurityGroup` key has something similar for hello value:</span></span>

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

## <a name="delete-an-nsg"></a><span data-ttu-id="ad753-143">Удаление группы NSG</span><span class="sxs-lookup"><span data-stu-id="ad753-143">Delete an NSG</span></span>
<span data-ttu-id="ad753-144">NSG можно удалить только в том случае, если она не сопоставлена tooany ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ad753-144">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="ad753-145">toodelete NSG, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="ad753-145">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="ad753-146">ресурсы hello toocheck связанные tooan NSG, запустите hello `azure network nsg show` как показано в [связи Nsg представление](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="ad753-146">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="ad753-147">Если hello NSG связанные tooany сетевых адаптеров, запустите hello `azure network nic set` как показано в [связь между Сетевыми NSG](#Dissociate-an-NSG-from-a-NIC) для каждого сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="ad753-147">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="ad753-148">Если hello NSG связанные tooany подсети, запустите hello `azure network vnet subnet set` как показано в [связь NSG из подсети](#Dissociate-an-NSG-from-a-subnet) для каждой подсети.</span><span class="sxs-lookup"><span data-stu-id="ad753-148">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="ad753-149">hello toodelete NSG, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ad753-149">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="ad753-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad753-150">Next steps</span></span>
* <span data-ttu-id="ad753-151">[Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="ad753-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

