---
title: "Создание среды Linux с помощью Azure CLI 2.0 | Документация Майкрософт"
description: "Узнайте, как с помощью Azure CLI 2.0. создать \"с нуля\" хранилище, виртуальную машину Linux, виртуальную сеть и подсеть, балансировщик нагрузки, сетевой адаптер, общедоступный IP-адрес и группу безопасности сети."
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
ms.openlocfilehash: e5c4785428b2150e951923e98079e00808a82d87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="ff2c0-103">Создание полнофункциональной виртуальной машины Linux с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ff2c0-103">Create a complete Linux virtual machine with the Azure CLI</span></span>
<span data-ttu-id="ff2c0-104">Чтобы быстро создать виртуальную машину в Azure, можно использовать одну команду Azure CLI, использующую значения по умолчанию для создания любых необходимых вспомогательных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-104">To quickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values to create any required supporting resources.</span></span> <span data-ttu-id="ff2c0-105">Ресурсы, такие как виртуальная сеть, общедоступный IP-адрес и правила группы сетевой безопасности, создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="ff2c0-106">Чтобы получить дополнительные возможности управления в рабочей среде, можно создать эти ресурсы заранее и затем добавлять в них виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs to them.</span></span> <span data-ttu-id="ff2c0-107">В этой статье описывается, как создать виртуальную машину и каждый из вспомогательных ресурсов по одному.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-107">This article guides you through how to create a VM and each of the supporting resources one by one.</span></span>

<span data-ttu-id="ff2c0-108">Обязательно установите последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войдите в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-108">Make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged to an Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="ff2c0-109">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-109">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ff2c0-110">Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="ff2c0-111">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="ff2c0-111">Create resource group</span></span>
<span data-ttu-id="ff2c0-112">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="ff2c0-113">Группу ресурсов нужно создать перед виртуальной машиной и вспомогательными ресурсами виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="ff2c0-114">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-114">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ff2c0-115">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ff2c0-116">По умолчанию выходные данные команд Azure CLI в формате JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-116">By default, the output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="ff2c0-117">Например, чтобы изменить назначение выходных данных на таблицу или список, используйте команду [az configure --output](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-117">To change the default output to a list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="ff2c0-118">Параметр `--output` можно добавлять к любой команде — он один раз изменяет формат выходных данных.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-118">You can also add `--output` to any command for a one time change in output format.</span></span> <span data-ttu-id="ff2c0-119">В следующем примере показаны выходные данные JSON из команды `az group create`:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-119">The following example shows the JSON output from the `az group create` command:</span></span>

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

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="ff2c0-120">Создание виртуальной сети и подсети</span><span class="sxs-lookup"><span data-stu-id="ff2c0-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="ff2c0-121">Затем создается виртуальная сеть в Azure и подсеть, в которой можно создать виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-121">Next you create a virtual network in Azure and a subnet in to which you can create your VMs.</span></span> <span data-ttu-id="ff2c0-122">Используйте команду [az network vnet create](/cli/azure/network/vnet#create), чтобы создать виртуальную сеть с именем *myVnet* с префиксом адреса *192.168.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-122">Use [az network vnet create](/cli/azure/network/vnet#create) to create a virtual network named *myVnet* with the *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="ff2c0-123">Кроме того, можно добавить подсеть с именем *mySubnet* с префиксом адреса *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-123">You also add a subnet named *mySubnet* with the address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="ff2c0-124">В выходных данных отображается подсеть, логически созданная внутри виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-124">The output shows the subnet as logically created inside the virtual network:</span></span>

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


## <a name="create-a-public-ip-address"></a><span data-ttu-id="ff2c0-125">Создание общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="ff2c0-125">Create a public IP address</span></span>
<span data-ttu-id="ff2c0-126">Теперь создайте общедоступный IP-адрес с помощью команды [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="ff2c0-127">Этот общедоступный IP-адрес позволяет подключаться к виртуальной машине через Интернет.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-127">This public IP address enables you to connect to your VMs from the Internet.</span></span> <span data-ttu-id="ff2c0-128">Так как адрес по умолчанию является динамическим, мы также создадим запись DNS с параметром `--domain-name-label`.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-128">Because the default address is dynamic, we also create a named DNS entry with the `--domain-name-label` option.</span></span> <span data-ttu-id="ff2c0-129">В следующем примере создается общедоступный IP-адрес *myPublicIP* с DNS-именем *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-129">The following example creates a public IP named *myPublicIP* with the DNS name of *mypublicdns*.</span></span> <span data-ttu-id="ff2c0-130">Так как DNS-имя должно быть уникальным, укажите собственное уникальное имя:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-130">Because the DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="ff2c0-131">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-131">Output:</span></span>

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


## <a name="create-a-network-security-group"></a><span data-ttu-id="ff2c0-132">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="ff2c0-132">Create a network security group</span></span>
<span data-ttu-id="ff2c0-133">Для управления потоком трафика в виртуальную машину и из нее создайте группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-133">To control the flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="ff2c0-134">Группу безопасности сети можно применить к сетевому адаптеру или подсети.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-134">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="ff2c0-135">В следующем примере с помощью команды [az network nsg create](/cli/azure/network/nsg#create) создается группа безопасности сети с именем *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-135">The following example uses [az network nsg create](/cli/azure/network/nsg#create) to create a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="ff2c0-136">Вы определяете правила, разрешающие или запрещающие определенный трафик.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-136">You define rules that allow or deny the specific traffic.</span></span> <span data-ttu-id="ff2c0-137">Чтобы разрешить входящие подключения через порт 22 (для поддержки SSH), создайте правило входящих подключений для группы безопасности сети с помощью команды [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-137">To allow inbound connections on port 22 (to support SSH), create an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="ff2c0-138">В следующем примере создается правило *myNetworkSecurityGroupRuleSSH*.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-138">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

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

<span data-ttu-id="ff2c0-139">Чтобы разрешить входящие подключения через порт 80 (для поддержки веб-трафика), добавьте еще одно правило группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-139">To allow inbound connections on port 80 (to support web traffic), add another network security group rule.</span></span> <span data-ttu-id="ff2c0-140">В следующем примере создается правило *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-140">The following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

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

<span data-ttu-id="ff2c0-141">Чтобы проверить группу безопасности сети и правила, выполните команду [az network nsg show](/cli/azure/network/nsg#show).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-141">Examine the network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="ff2c0-142">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-142">Output:</span></span>

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
      "description": "Allow outbound traffic from all VMs to all VMs in VNET",
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
      "description": "Allow outbound traffic from all VMs to Internet",
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

## <a name="create-a-virtual-nic"></a><span data-ttu-id="ff2c0-143">Создание виртуального сетевого адаптера</span><span class="sxs-lookup"><span data-stu-id="ff2c0-143">Create a virtual NIC</span></span>
<span data-ttu-id="ff2c0-144">Работой сетевых адаптеров можно управлять программно, так как к ним можно применить правила.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="ff2c0-145">Кроме того, можно использовать несколько сетевых карт.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-145">You can also have more than one.</span></span> <span data-ttu-id="ff2c0-146">С помощью команды [az network nic create](/cli/azure/network/nic#create) создается сетевой адаптер с именем *myNic* и связывается с группой безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-146">In the following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with the network security group.</span></span> <span data-ttu-id="ff2c0-147">Общедоступный IP-адрес *myPublicIP* также связывается с виртуальным сетевым адаптером.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-147">The public IP address *myPublicIP* is also associated with the virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="ff2c0-148">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-148">Output:</span></span>

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


## <a name="create-an-availability-set"></a><span data-ttu-id="ff2c0-149">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="ff2c0-149">Create an availability set</span></span>
<span data-ttu-id="ff2c0-150">Группы доступности помогают распределить виртуальные машины между доменами сбоя и доменами обновления.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="ff2c0-151">Несмотря на то, что прямо сейчас можно создать только одну виртуальную машину, рекомендуется использовать группы доступности для упрощения расширения в будущем.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-151">Even though you only create one VM right now, it's best practice to use availability sets to make it easier to expand in the future.</span></span> 

<span data-ttu-id="ff2c0-152">Домены сбоя определяют группу виртуальных машин, совместно использующих общий источник питания и сетевой коммутатор.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="ff2c0-153">По умолчанию виртуальные машины, настроенные в группе доступности, разделяются между несколькими доменами сбоя, которых может быть не больше трех.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-153">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="ff2c0-154">Сбой оборудования в одном из этих доменов сбоя не влияет на все виртуальные машины, на которых выполняется ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="ff2c0-155">Домены обновления — это группы виртуальных машин и базовое физическое оборудование, которое может быть перезагружено одновременно.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="ff2c0-156">Перезагрузка доменов обновления при запланированном обслуживании может выполняться не по порядку, но одновременно перезагружается только один домен обновления.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-156">During planned maintenance, the order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="ff2c0-157">Azure автоматически распределяет виртуальные машины между доменами сбоя и обновления при помещении их в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-157">Azure automatically distributes VMs across the fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="ff2c0-158">Дополнительные сведения см. в статье [Управление доступностью виртуальных машин Linux](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-158">For more information, see [managing the availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="ff2c0-159">Создайте группу доступности для виртуальных машин с помощью команды [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="ff2c0-160">В следующем примере создается группа доступности *myAvailabilitySet*.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-160">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="ff2c0-161">В выводе указаны домены ошибок и домены обновления:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-161">The output notes fault domains and update domains:</span></span>

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


## <a name="create-the-linux-vms"></a><span data-ttu-id="ff2c0-162">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="ff2c0-162">Create the Linux VMs</span></span>
<span data-ttu-id="ff2c0-163">Вы создали ресурсы сети для доступных через Интернет виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-163">You've created the network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="ff2c0-164">Теперь создайте виртуальную машину и защитите ее с помощью ключа SSH.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="ff2c0-165">В этом случае мы создадим виртуальную машину Ubuntu на базе последней версии LTS.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-165">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="ff2c0-166">Дополнительные образы можно найти с помощью команды [az vm image list](/cli/azure/vm/image#list), как это описано в статье о [поиске образов виртуальных машин Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="ff2c0-167">Кроме того, мы укажем ключ SSH для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-167">We also specify an SSH key to use for authentication.</span></span> <span data-ttu-id="ff2c0-168">Если у вас нет пары открытых ключей SSH, их [можно создать](mac-create-ssh-keys.md) или использовать параметр `--generate-ssh-keys` для их создания.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use the `--generate-ssh-keys` parameter to create them for you.</span></span> <span data-ttu-id="ff2c0-169">Если у вас уже есть пара ключей, этот параметр будет использовать имеющиеся ключи в `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="ff2c0-170">Создайте виртуальную машину, собрав воедино все ресурсы и информацию с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-170">Create the VM by bringing all our resources and information together with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="ff2c0-171">В следующем примере создается виртуальная машина с именем *myVM*.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-171">The following example creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="ff2c0-172">Подключитесь к виртуальной машине по протоколу SSH с записью DNS, указанной при создании общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-172">SSH to your VM with the DNS entry you provided when you created the public IP address.</span></span> <span data-ttu-id="ff2c0-173">`fqdn` отображается в выходных данных при создании виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-173">This `fqdn` is shown in the output as you create your VM:</span></span>

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

<span data-ttu-id="ff2c0-174">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-174">Output:</span></span>

```bash
The authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="ff2c0-175">Вы можете установить NGINX и просмотреть, как трафик проходит к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-175">You can install NGINX and see the traffic flow to the VM.</span></span> <span data-ttu-id="ff2c0-176">Установите NGINX следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="ff2c0-177">Для просмотра сайта NGINX по умолчанию откройте браузер и введите полное доменное имя:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-177">To see the default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Сайт NGINX по умолчанию на виртуальной машине](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="ff2c0-179">Экспорт в качестве шаблона</span><span class="sxs-lookup"><span data-stu-id="ff2c0-179">Export as a template</span></span>
<span data-ttu-id="ff2c0-180">Допустим, вам требуется создать дополнительную среду разработки с теми же параметрами или соответствующую рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-180">What if you now want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="ff2c0-181">Resource Manager использует шаблоны JSON, которые определяют все параметры среды.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-181">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="ff2c0-182">Можно полностью создавать среды, ссылаясь на этот шаблон JSON.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="ff2c0-183">Вы можете [создавать шаблоны JSON вручную](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или экспортировать существующую среду для создания шаблона JSON автоматически.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you.</span></span> <span data-ttu-id="ff2c0-184">Чтобы экспортировать группу ресурсов, используйте команду [az group export](/cli/azure/group#export) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-184">Use [az group export](/cli/azure/group#export) to export your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="ff2c0-185">С помощью этой команды в текущем рабочем каталоге создается файл `myResourceGroup.json`.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-185">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="ff2c0-186">При создании среды на основе этого шаблона запрашиваются все имена ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-186">When you create an environment from this template, you are prompted for all the resource names.</span></span> <span data-ttu-id="ff2c0-187">Эти имена можно указать в файле шаблона, добавив параметр `--include-parameter-default-value` в команду `az group export`.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-187">You can populate these names in your template file by adding the `--include-parameter-default-value` parameter to the `az group export` command.</span></span> <span data-ttu-id="ff2c0-188">Измените шаблон JSON, чтобы указать имена ресурсов, или [создайте файл parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , задающий их.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-188">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="ff2c0-189">Чтобы создать среду с помощью шаблона, используйте команду [az group deployment create](/cli/azure/group/deployment#create) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ff2c0-189">To create an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="ff2c0-190">Вы можете прочитать [дополнительные сведения о развертывании из шаблонов](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff2c0-190">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="ff2c0-191">Узнайте, как поэтапно обновлять среды, использовать файл параметров и обращаться к шаблонам из единого места хранения.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-191">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff2c0-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ff2c0-192">Next steps</span></span>
<span data-ttu-id="ff2c0-193">Теперь вы готовы приступить к работе с несколькими сетевыми компонентами и виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-193">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="ff2c0-194">Используя этот пример среды, можно создать приложение на основе представленных здесь основных компонентов.</span><span class="sxs-lookup"><span data-stu-id="ff2c0-194">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
