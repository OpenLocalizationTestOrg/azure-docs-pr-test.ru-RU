---
title: "в среде Linux с hello Azure CLI 2.0 aaaCreate | Документы Microsoft"
description: "Создайте хранилища, виртуальной Машины Linux, виртуальной сети и подсети, подсистемы балансировки нагрузки, сетевой Адаптер, общедоступный IP-адрес и группу безопасности сети из hello основание, с помощью Azure CLI 2.0 hello."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="cfd17-103">Создать полный виртуальной машины Linux с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cfd17-103">Create a complete Linux virtual machine with hello Azure CLI</span></span>
<span data-ttu-id="cfd17-104">tooquickly Создание виртуальной машины (VM) в Azure, можно использовать одну команду Azure CLI, использующий все необходимые ресурсы поддержки toocreate значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cfd17-104">tooquickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values toocreate any required supporting resources.</span></span> <span data-ttu-id="cfd17-105">Ресурсы, такие как виртуальная сеть, общедоступный IP-адрес и правила группы сетевой безопасности, создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="cfd17-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="cfd17-106">Дополнительные возможности управления в рабочей среде использовать, можно создать эти ресурсы заранее и затем добавить к toothem виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cfd17-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs toothem.</span></span> <span data-ttu-id="cfd17-107">В этой статье поможет как toocreate виртуальной Машины и каждый из hello вспомогательные ресурсы по одному.</span><span class="sxs-lookup"><span data-stu-id="cfd17-107">This article guides you through how toocreate a VM and each of hello supporting resources one by one.</span></span>

<span data-ttu-id="cfd17-108">Убедитесь, что hello установлена последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) и учетной записи вошедшего tooan Azure с помощью [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="cfd17-108">Make sure that you have installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged tooan Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="cfd17-109">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="cfd17-109">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="cfd17-110">Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="cfd17-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="cfd17-111">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="cfd17-111">Create resource group</span></span>
<span data-ttu-id="cfd17-112">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="cfd17-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="cfd17-113">Группу ресурсов нужно создать перед виртуальной машиной и вспомогательными ресурсами виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="cfd17-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="cfd17-114">Создать группу ресурсов hello с [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="cfd17-114">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="cfd17-115">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="cfd17-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="cfd17-116">По умолчанию hello Azure CLI команд выводится в формате JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="cfd17-116">By default, hello output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="cfd17-117">Список tooa вывода по умолчанию hello toochange или таблице, например, использовать [настроить az — вывод](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="cfd17-117">toochange hello default output tooa list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="cfd17-118">Можно также добавить `--output` изменить tooany команды один раз в выходном формате.</span><span class="sxs-lookup"><span data-stu-id="cfd17-118">You can also add `--output` tooany command for a one time change in output format.</span></span> <span data-ttu-id="cfd17-119">Hello пример hello выходных данных JSON из hello `az group create` команды:</span><span class="sxs-lookup"><span data-stu-id="cfd17-119">hello following example shows hello JSON output from hello `az group create` command:</span></span>

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="cfd17-120">Создание виртуальной сети и подсети</span><span class="sxs-lookup"><span data-stu-id="cfd17-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="cfd17-121">Затем создайте виртуальную сеть в Azure и подсети в toowhich можно создать виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="cfd17-121">Next you create a virtual network in Azure and a subnet in toowhich you can create your VMs.</span></span> <span data-ttu-id="cfd17-122">Используйте [создания az сети vnet](/cli/azure/network/vnet#create) toocreate виртуальная сеть с именем *myVnet* с hello *192.168.0.0/16* префикс адреса.</span><span class="sxs-lookup"><span data-stu-id="cfd17-122">Use [az network vnet create](/cli/azure/network/vnet#create) toocreate a virtual network named *myVnet* with hello *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="cfd17-123">Можно также добавить подсеть с именем *mySubnet* с префикс адреса hello *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="cfd17-123">You also add a subnet named *mySubnet* with hello address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="cfd17-124">Hello выходные данные показывают, как логически создан внутри виртуальной сети hello подсети hello:</span><span class="sxs-lookup"><span data-stu-id="cfd17-124">hello output shows hello subnet as logically created inside hello virtual network:</span></span>

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a><span data-ttu-id="cfd17-125">Создание общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="cfd17-125">Create a public IP address</span></span>
<span data-ttu-id="cfd17-126">Теперь создайте общедоступный IP-адрес с помощью команды [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="cfd17-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="cfd17-127">Этот общедоступный IP-адрес позволяет вам tooconnect tooyour виртуальных машин из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="cfd17-127">This public IP address enables you tooconnect tooyour VMs from hello Internet.</span></span> <span data-ttu-id="cfd17-128">Так как адрес по умолчанию hello является динамическим, мы также создать именованный DNS-запись с hello `--domain-name-label` параметр.</span><span class="sxs-lookup"><span data-stu-id="cfd17-128">Because hello default address is dynamic, we also create a named DNS entry with hello `--domain-name-label` option.</span></span> <span data-ttu-id="cfd17-129">Hello следующий пример создает общедоступный IP-адрес с именем *myPublicIP* с именем DNS hello *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="cfd17-129">hello following example creates a public IP named *myPublicIP* with hello DNS name of *mypublicdns*.</span></span> <span data-ttu-id="cfd17-130">Поскольку hello DNS-имя должно быть уникальным, укажите уникальное имя DNS:</span><span class="sxs-lookup"><span data-stu-id="cfd17-130">Because hello DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="cfd17-131">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="cfd17-131">Output:</span></span>

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a><span data-ttu-id="cfd17-132">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="cfd17-132">Create a network security group</span></span>
<span data-ttu-id="cfd17-133">toocontrol hello поток трафика и из нее виртуальные машины, создайте группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="cfd17-133">toocontrol hello flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="cfd17-134">Группа безопасности сети может быть применен tooa сетевой Адаптер или подсети.</span><span class="sxs-lookup"><span data-stu-id="cfd17-134">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="cfd17-135">Hello следующий пример использует [создать az сети nsg](/cli/azure/network/nsg#create) toocreate сетевой группы безопасности с именем *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="cfd17-135">hello following example uses [az network nsg create](/cli/azure/network/nsg#create) toocreate a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="cfd17-136">Можно определить правила, которые разрешают или запрещают трафик конкретных hello.</span><span class="sxs-lookup"><span data-stu-id="cfd17-136">You define rules that allow or deny hello specific traffic.</span></span> <span data-ttu-id="cfd17-137">tooallow входящие соединения через порт 22 (toosupport SSH), создайте правило входящего трафика для hello сетевой группы безопасности с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="cfd17-137">tooallow inbound connections on port 22 (toosupport SSH), create an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="cfd17-138">Hello следующий код создает правило с именем *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="cfd17-138">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

<span data-ttu-id="cfd17-139">tooallow входящие соединения через порт 80 (toosupport веб-трафик), добавить новое правило группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="cfd17-139">tooallow inbound connections on port 80 (toosupport web traffic), add another network security group rule.</span></span> <span data-ttu-id="cfd17-140">Hello следующий код создает правило с именем *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="cfd17-140">hello following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="cfd17-141">Изучите hello сетевой группы безопасности и правила с [nsg Показать az сети](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="cfd17-141">Examine hello network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="cfd17-142">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="cfd17-142">Output:</span></span>

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooInternet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a><span data-ttu-id="cfd17-143">Создание виртуального сетевого адаптера</span><span class="sxs-lookup"><span data-stu-id="cfd17-143">Create a virtual NIC</span></span>
<span data-ttu-id="cfd17-144">Виртуальных сетевых плат (NIC) программно недоступны, так как можно применять правила использования tootheir.</span><span class="sxs-lookup"><span data-stu-id="cfd17-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="cfd17-145">Кроме того, можно использовать несколько сетевых карт.</span><span class="sxs-lookup"><span data-stu-id="cfd17-145">You can also have more than one.</span></span> <span data-ttu-id="cfd17-146">В следующих hello [Создание сетевого адаптера сети az](/cli/azure/network/nic#create) команду создать сетевой Адаптер с именем *myNic* и связать его с hello сетевой группы безопасности.</span><span class="sxs-lookup"><span data-stu-id="cfd17-146">In hello following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with hello network security group.</span></span> <span data-ttu-id="cfd17-147">Здравствуйте, общедоступный IP-адрес *myPublicIP* также связана с hello виртуального сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="cfd17-147">hello public IP address *myPublicIP* is also associated with hello virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="cfd17-148">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="cfd17-148">Output:</span></span>

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a><span data-ttu-id="cfd17-149">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="cfd17-149">Create an availability set</span></span>
<span data-ttu-id="cfd17-150">Группы доступности помогают распределить виртуальные машины между доменами сбоя и доменами обновления.</span><span class="sxs-lookup"><span data-stu-id="cfd17-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="cfd17-151">Несмотря на то, что можно создать только одну виртуальную Машину прямо сейчас, это лучший подход toouse доступности наборы toomake его проще tooexpand в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="cfd17-151">Even though you only create one VM right now, it's best practice toouse availability sets toomake it easier tooexpand in hello future.</span></span> 

<span data-ttu-id="cfd17-152">Домены сбоя определяют группу виртуальных машин, совместно использующих общий источник питания и сетевой коммутатор.</span><span class="sxs-lookup"><span data-stu-id="cfd17-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="cfd17-153">По умолчанию hello виртуальных машин, настроенных в наборе доступности должны быть разделены между toothree домены сбоя.</span><span class="sxs-lookup"><span data-stu-id="cfd17-153">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="cfd17-154">Сбой оборудования в одном из этих доменов сбоя не влияет на все виртуальные машины, на которых выполняется ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="cfd17-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="cfd17-155">Домены обновления указания групп виртуальных машин и физического оборудования, можно перезагрузить в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="cfd17-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="cfd17-156">Во время планового обслуживания hello порядок, в которой обновления доменов перезагружаются могут быть непоследовательными, но только одно обновление домена перезагружается одновременно.</span><span class="sxs-lookup"><span data-stu-id="cfd17-156">During planned maintenance, hello order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="cfd17-157">Azure автоматически распределяет виртуальные машины hello доменов сбоя и обновления при помещении их в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="cfd17-157">Azure automatically distributes VMs across hello fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="cfd17-158">Дополнительные сведения см. в разделе [управление hello доступности виртуальных машин](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="cfd17-158">For more information, see [managing hello availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="cfd17-159">Создайте группу доступности для виртуальных машин с помощью команды [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="cfd17-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="cfd17-160">Hello следующий пример создает именованный набор доступности *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="cfd17-160">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="cfd17-161">Здравствуйте домены сбоя заметки выходные данные и доменами обновления:</span><span class="sxs-lookup"><span data-stu-id="cfd17-161">hello output notes fault domains and update domains:</span></span>

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-hello-linux-vms"></a><span data-ttu-id="cfd17-162">Создание виртуальных машин Linux hello</span><span class="sxs-lookup"><span data-stu-id="cfd17-162">Create hello Linux VMs</span></span>
<span data-ttu-id="cfd17-163">Вы создали toosupport ресурсы hello сети ВМ, доступном через Интернет.</span><span class="sxs-lookup"><span data-stu-id="cfd17-163">You've created hello network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="cfd17-164">Теперь создайте виртуальную машину и защитите ее с помощью ключа SSH.</span><span class="sxs-lookup"><span data-stu-id="cfd17-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="cfd17-165">В этом случае мы будем toocreate Виртуальной машине Ubuntu на основании hello последних Результатов.</span><span class="sxs-lookup"><span data-stu-id="cfd17-165">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="cfd17-166">Дополнительные образы можно найти с помощью команды [az vm image list](/cli/azure/vm/image#list), как это описано в статье о [поиске образов виртуальных машин Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="cfd17-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="cfd17-167">Кроме того, указывается toouse ключа SSH для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="cfd17-167">We also specify an SSH key toouse for authentication.</span></span> <span data-ttu-id="cfd17-168">Если у вас пара открытых ключей SSH, вы можете [их создания](mac-create-ssh-keys.md) или использовать hello `--generate-ssh-keys` параметр toocreate ими.</span><span class="sxs-lookup"><span data-stu-id="cfd17-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use hello `--generate-ssh-keys` parameter toocreate them for you.</span></span> <span data-ttu-id="cfd17-169">Если у вас уже есть пара ключей, этот параметр будет использовать имеющиеся ключи в `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="cfd17-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="cfd17-170">Создать hello виртуальной Машине путем подключения к нашей ресурсы и сведения, а также hello [создания виртуальной машины az](/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="cfd17-170">Create hello VM by bringing all our resources and information together with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="cfd17-171">Hello следующий пример создает Виртуальную машину с именем *myVM*:</span><span class="sxs-lookup"><span data-stu-id="cfd17-171">hello following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="cfd17-172">Tooyour SSH виртуальной Машины с hello запись DNS, предоставленный при создании hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="cfd17-172">SSH tooyour VM with hello DNS entry you provided when you created hello public IP address.</span></span> <span data-ttu-id="cfd17-173">Это `fqdn` отображается в выходных данных hello при создании виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="cfd17-173">This `fqdn` is shown in hello output as you create your VM:</span></span>

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="cfd17-174">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="cfd17-174">Output:</span></span>

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="cfd17-175">Можно установить NGINX и увидеть toohello поток трафика hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cfd17-175">You can install NGINX and see hello traffic flow toohello VM.</span></span> <span data-ttu-id="cfd17-176">Установите NGINX следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cfd17-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="cfd17-177">узел по умолчанию NGINX toosee hello в действии, откройте браузер и введите полное доменное имя:</span><span class="sxs-lookup"><span data-stu-id="cfd17-177">toosee hello default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Сайт NGINX по умолчанию на виртуальной машине](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="cfd17-179">Экспорт в качестве шаблона</span><span class="sxs-lookup"><span data-stu-id="cfd17-179">Export as a template</span></span>
<span data-ttu-id="cfd17-180">Теперь нужно, чтобы toocreate среде дополнительная разработка с hello такими же параметрами или рабочей среде, которая сопоставляет его?</span><span class="sxs-lookup"><span data-stu-id="cfd17-180">What if you now want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="cfd17-181">Диспетчер ресурсов использует JSON шаблонов, определяющих все параметры hello для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="cfd17-181">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="cfd17-182">Можно полностью создавать среды, ссылаясь на этот шаблон JSON.</span><span class="sxs-lookup"><span data-stu-id="cfd17-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="cfd17-183">Вы можете [вручную построить шаблоны JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или экспортировать существующий шаблон JSON hello toocreate среды для вас.</span><span class="sxs-lookup"><span data-stu-id="cfd17-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you.</span></span> <span data-ttu-id="cfd17-184">Используйте [экспорта группы az](/cli/azure/group#export) tooexport ресурс группы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cfd17-184">Use [az group export](/cli/azure/group#export) tooexport your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="cfd17-185">Эта команда создает hello `myResourceGroup.json` файла в текущий рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="cfd17-185">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="cfd17-186">При создании среды на основе этого шаблона, запрашиваются все имена ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="cfd17-186">When you create an environment from this template, you are prompted for all hello resource names.</span></span> <span data-ttu-id="cfd17-187">Эти имена можно заполнить в файле шаблона, добавляя hello `--include-parameter-default-value` toohello параметр `az group export` команды.</span><span class="sxs-lookup"><span data-stu-id="cfd17-187">You can populate these names in your template file by adding hello `--include-parameter-default-value` parameter toohello `az group export` command.</span></span> <span data-ttu-id="cfd17-188">Редактирование JSON шаблона toospecify hello имена ресурсов, или [создайте файл parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , указывающий имена ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="cfd17-188">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="cfd17-189">toocreate среды из шаблона, используйте [создания развертывания группы az](/cli/azure/group/deployment#create) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cfd17-189">toocreate an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="cfd17-190">Может потребоваться tooread [Дополнительные сведения о том, как toodeploy из шаблонов](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cfd17-190">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="cfd17-191">Сведения о средах обновление tooincrementally, использовать файл параметров hello и получить доступ к шаблонам с единым хранилища.</span><span class="sxs-lookup"><span data-stu-id="cfd17-191">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfd17-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cfd17-192">Next steps</span></span>
<span data-ttu-id="cfd17-193">Теперь вы готовы toobegin работа с несколькими сетевыми компонентами и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="cfd17-193">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="cfd17-194">Toobuild среды этот образец можно использовать из приложения с помощью hello основные компоненты представленные здесь.</span><span class="sxs-lookup"><span data-stu-id="cfd17-194">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
