---
title: "Управление группами безопасности сети (Azure CLI 2.0) | Документация Майкрософт"
description: "Узнайте, как управлять группами безопасности сети с помощью интерфейса командной строки Azure (CLI) версии 2.0."
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
ms.openlocfilehash: 11ec0d3d9e33c06d4c0a164f7fba5dd5cca73872
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-cli-20"></a><span data-ttu-id="fef14-103">Управление группами безопасности сети с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fef14-103">Manage network security groups using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="fef14-104">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="fef14-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="fef14-105">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="fef14-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="fef14-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fef14-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="fef14-107">[Azure CLI 2.0](#View-existing-NSGs) — это интерфейс командной строки нового поколения для модели развертывания Resource Manager (описывается в этой статье).</span><span class="sxs-lookup"><span data-stu-id="fef14-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for the resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="fef14-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fef14-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fef14-109">В этой статье описывается использование модели развертывания c помощью Resource Manager. Для большинства новых развертываний мы рекомендуем использовать эту модель вместо классической.</span><span class="sxs-lookup"><span data-stu-id="fef14-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="fef14-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fef14-110">Prerequisite</span></span>
<span data-ttu-id="fef14-111">Установите и настройте последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) (если вы еще этого не сделали), а затем войдите с использованием учетной записи Azure, выполнив команду [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fef14-111">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="fef14-112">Просмотр существующих групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="fef14-112">View existing NSGs</span></span>
<span data-ttu-id="fef14-113">Чтобы просмотреть список групп безопасности сети в определенной группе ресурсов, выполните команду [az network nsg list](/cli/azure/network/nsg#list) с форматом выходных данных `-o table`:</span><span class="sxs-lookup"><span data-stu-id="fef14-113">To view the list of NSGs in a specific resource group, run the [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="fef14-114">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fef14-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="fef14-115">Перечисление всех правил для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="fef14-115">List all rules for an NSG</span></span>
<span data-ttu-id="fef14-116">Чтобы просмотреть группу безопасности сети **NSG-FrontEnd**, выполните команду [az network nsg show](/cli/azure/network/nsg#show), используя [фильтр запроса JMESPATH](/cli/azure/query-az-cli2) и формат выходных данных `-o table`:</span><span class="sxs-lookup"><span data-stu-id="fef14-116">To view the rules of an NSG named **NSG-FrontEnd**, run the [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and the `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="fef14-117">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fef14-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs to all VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs to Internet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="fef14-118">Кроме того, можно выполнить команду [az network nsg rule list](/cli/azure/network/nsg/rule#list), чтобы вывести список только пользовательских правил из группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="fef14-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) to list only the custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="fef14-119">Просмотр связей для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="fef14-119">View NSG associations</span></span>

<span data-ttu-id="fef14-120">Чтобы просмотреть, с какими ресурсами связана группа безопасности сети **NSG-FrontEnd`az network nsg show`, выполните команду** , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fef14-120">To view what resources the **NSG-FrontEnd** NSG is associate with, run the `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="fef14-121">Найдите свойства **networkInterfaces** и **subnets**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fef14-121">Look for the **networkInterfaces** and **subnets** properties as shown below:</span></span>

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

<span data-ttu-id="fef14-122">В приведенном выше примере группа безопасности сети не связана с сетевыми адаптерами, но связана с подсетью **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="fef14-122">In the example above, the NSG is not associated to any network interfaces (NICs), and it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="fef14-123">Добавление правила</span><span class="sxs-lookup"><span data-stu-id="fef14-123">Add a rule</span></span>
<span data-ttu-id="fef14-124">Чтобы добавить правило, разрешающее **входящий** трафик через порт **443** с любого компьютера в группу безопасности сети **NSG-FrontEnd**, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fef14-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, enter the following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access to port 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="fef14-125">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fef14-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access to port 443 for HTTPS",
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

## <a name="change-a-rule"></a><span data-ttu-id="fef14-126">Изменение правила</span><span class="sxs-lookup"><span data-stu-id="fef14-126">Change a rule</span></span>
<span data-ttu-id="fef14-127">Чтобы изменить ранее созданное правило, разрешающее входящий трафик только из **Интернета**, выполните команду [az network nsg rule update](/cli/azure/network/nsg/rule#update):</span><span class="sxs-lookup"><span data-stu-id="fef14-127">To change the rule created above to allow inbound traffic from the **Internet** only, run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="fef14-128">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fef14-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access to port 443 for HTTPS",
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

## <a name="delete-a-rule"></a><span data-ttu-id="fef14-129">Удаление правила</span><span class="sxs-lookup"><span data-stu-id="fef14-129">Delete a rule</span></span>
<span data-ttu-id="fef14-130">Чтобы удалить созданное ранее правило, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fef14-130">To delete the rule created above, run the following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="fef14-131">Связывание группы безопасности сети с сетевым адаптером</span><span class="sxs-lookup"><span data-stu-id="fef14-131">Associate an NSG to a NIC</span></span>
<span data-ttu-id="fef14-132">Чтобы связать группу безопасности сети **NSG-FrontEnd** с сетевой картой **TestNICWeb1**, выполните команду [az network nic update](/cli/azure/network/nic#update):</span><span class="sxs-lookup"><span data-stu-id="fef14-132">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, use the [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="fef14-133">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fef14-133">Expected output:</span></span>

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

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="fef14-134">Отмена связи с сетевым адаптером для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="fef14-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="fef14-135">Чтобы удалить связь между группой безопасности сети **NSG-FrontEnd** и сетевой картой **TestNICWeb1**, выполните команду [az network nsg rule update](/cli/azure/network/nsg/rule#update) еще раз, но замените аргумент `--network-security-group` пустой строкой (`""`).</span><span class="sxs-lookup"><span data-stu-id="fef14-135">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace the `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="fef14-136">В выходных данных для ключа `networkSecurityGroup` задано значение null.</span><span class="sxs-lookup"><span data-stu-id="fef14-136">In the output, the `networkSecurityGroup` key is set to null.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="fef14-137">Отмена связи с подсетью для группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="fef14-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="fef14-138">Чтобы удалить связь между группой безопасности сети **NSG-FrontEnd** и подсетью **FrontEnd**, выполните команду [az network nsg rule update](/cli/azure/network/nsg/rule#update) еще раз, но замените аргумент `--network-security-group` пустой строкой (`""`).</span><span class="sxs-lookup"><span data-stu-id="fef14-138">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, again run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace the `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="fef14-139">В выходных данных для ключа `networkSecurityGroup` задано значение null.</span><span class="sxs-lookup"><span data-stu-id="fef14-139">In the output, the `networkSecurityGroup` key is set to null.</span></span>

## <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="fef14-140">Связывание группы NSG с подсетью</span><span class="sxs-lookup"><span data-stu-id="fef14-140">Associate an NSG to a subnet</span></span>
<span data-ttu-id="fef14-141">Чтобы снова связать группу безопасности сети **NSG-FrontEnd** с подсетью **FrontEnd**, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fef14-141">To associate the **NSG-FrontEnd** NSG to the **FrontEnd** subnet again, run the following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="fef14-142">В выходных данных для ключа `networkSecurityGroup` задано значение, подобное следующему:</span><span class="sxs-lookup"><span data-stu-id="fef14-142">In the output, the `networkSecurityGroup` key has something similar for the value:</span></span>

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

## <a name="delete-an-nsg"></a><span data-ttu-id="fef14-143">Удаление группы NSG</span><span class="sxs-lookup"><span data-stu-id="fef14-143">Delete an NSG</span></span>
<span data-ttu-id="fef14-144">Группу безопасности сети можно удалить только в том случае, если она не связана с ресурсами.</span><span class="sxs-lookup"><span data-stu-id="fef14-144">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="fef14-145">Чтобы удалить группу безопасности сети, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fef14-145">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="fef14-146">Чтобы проверить ресурсы, связанные с группой, выполните команду `azure network nsg show` , как показано в разделе [Просмотр связей для группы безопасности сети](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="fef14-146">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="fef14-147">Если группа связана с сетевыми адаптерами, выполните `azure network nic set` , как показано в разделе [Отмена связи с сетевым адаптером для группы безопасности сети](#Dissociate-an-NSG-from-a-NIC) , для каждого сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="fef14-147">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="fef14-148">Если группа связана с подсетью, выполните `azure network vnet subnet set` , как показано в разделе [Отмена связи с подсетью для группы безопасности сети](#Dissociate-an-NSG-from-a-subnet) , для каждой подсети.</span><span class="sxs-lookup"><span data-stu-id="fef14-148">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="fef14-149">Чтобы удалить группу безопасности сети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fef14-149">To delete the NSG, run the following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="fef14-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fef14-150">Next steps</span></span>
* <span data-ttu-id="fef14-151">[Включите ведение журнала](virtual-network-nsg-manage-log.md) для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="fef14-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

