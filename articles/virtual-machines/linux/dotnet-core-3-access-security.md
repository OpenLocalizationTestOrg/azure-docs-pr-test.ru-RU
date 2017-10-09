---
title: "aaaAccess и безопасности в Azure шаблоны виртуальных машин Linux | Документы Microsoft"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 07e47189-680e-4102-a8d4-5a8eb9c00213
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 88fedc8287c1f8ab8397a03ddefe1e60a686815e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="c8682-103">Доступ и безопасность в шаблонах Azure Resource Manager для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="c8682-103">Access and security in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="c8682-104">Приложения размещенных в Azure скорее всего, необходимость toobe доступ через hello Интернета или VPN-подключения Express Route с Azure.</span><span class="sxs-lookup"><span data-stu-id="c8682-104">Applications hosted in Azure likely need toobe access over hello internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="c8682-105">С образцом приложения hello Music Store, hello веб-сайта доступны на hello Интернета с общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c8682-105">With hello Music Store application sample, hello web site is made available on hello internet with a public IP address.</span></span> <span data-ttu-id="c8682-106">С уровнем доступа установления подключений toohello доступа к приложениям и toohello ресурсы виртуальной машины сами должны быть защищены.</span><span class="sxs-lookup"><span data-stu-id="c8682-106">With access established, connections toohello application and access toohello virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="c8682-107">Защиту доступа обеспечивает группа безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="c8682-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="c8682-108">В этом документе описаны как обеспечивается безопасность hello приложение Music Store в hello образец шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c8682-108">This document details how hello Music Store application is secured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="c8682-109">Здесь будут описаны все зависимости и уникальные настройки.</span><span class="sxs-lookup"><span data-stu-id="c8682-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="c8682-110">Для получения наилучших результатов hello предварительно разверните экземпляр tooyour решения hello подписки Azure, работают вместе с hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c8682-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="c8682-111">Полный шаблон Hello можно найти здесь — [музыка хранилища развертывания на Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="c8682-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="public-ip-address"></a><span data-ttu-id="c8682-112">Общедоступный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="c8682-112">Public IP Address</span></span>
<span data-ttu-id="c8682-113">можно использовать общий доступ tooprovide tooan ресурсов Azure, открытого ресурса IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="c8682-113">tooprovide public access tooan Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="c8682-114">Общедоступный IP-адрес может быть статическим или динамическим.</span><span class="sxs-lookup"><span data-stu-id="c8682-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="c8682-115">Если используется динамический адрес и останавливается и освобождается hello виртуальной машины, удаляется адреса hello.</span><span class="sxs-lookup"><span data-stu-id="c8682-115">If a dynamic address is used, and hello virtual machine is stopped and deallocated, hello addresses is removed.</span></span> <span data-ttu-id="c8682-116">При запуске машины hello снова, ее можно назначить другой общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c8682-116">When hello machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="c8682-117">tooprevent объект IP адрес изменять, можно использовать зарезервированный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c8682-117">tooprevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="c8682-118">Общедоступный IP-адрес можно добавить hello Visual Studio новый мастер добавления ресурсов, с помощью шаблона Azure Resource Manager tooan или путем вставки допустимых данных JSON в шаблон.</span><span class="sxs-lookup"><span data-stu-id="c8682-118">A Public IP Address can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="c8682-119">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [общедоступный IP-адрес](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).</span><span class="sxs-lookup"><span data-stu-id="c8682-119">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicipaddressName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "public-ip-front"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="c8682-120">Общедоступный IP-адрес может быть связан с виртуальным сетевым адаптером или с балансировщиком нагрузки.</span><span class="sxs-lookup"><span data-stu-id="c8682-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="c8682-121">В этом примере, поскольку hello Music Store веб-сайта является Балансировка нагрузки для нескольких виртуальных машин hello общедоступный IP-адрес является вложенного toohello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="c8682-121">In this example, because hello Music Store website is load balanced across several virtual machines, hello Public IP Address is attached toohello Load Balancer.</span></span>

<span data-ttu-id="c8682-122">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [ассоциации общедоступный IP-адрес с подсистемой балансировки нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="c8682-122">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="c8682-123">Hello общедоступный IP-адрес, как просматривать hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c8682-123">hello public IP Address as seen from hello Azure portal.</span></span> <span data-ttu-id="c8682-124">Обратите внимание, что hello общедоступный IP-адрес связанного tooa балансировки нагрузки и не на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c8682-124">Notice that hello public IP address is associated tooa load balancer and not a virtual machine.</span></span> <span data-ttu-id="c8682-125">В следующий документ hello этой серии приводится подробное описание подсистем балансировки нагрузки сети.</span><span class="sxs-lookup"><span data-stu-id="c8682-125">Network load balancers are detailed in hello next document of this series.</span></span>

![Общедоступный IP-адрес](./media/dotnet-core-3-access-security/pubip.png)

<span data-ttu-id="c8682-127">Дополнительные сведения об общедоступных IP-адресах Azure см. в статье [IP-адреса в Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c8682-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="c8682-128">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="c8682-128">Network Security Group</span></span>
<span data-ttu-id="c8682-129">После доступа к установленным tooAzure ресурсы, должны быть ограничены такой доступ.</span><span class="sxs-lookup"><span data-stu-id="c8682-129">Once access has been established tooAzure resources, this access should be limited.</span></span> <span data-ttu-id="c8682-130">Для виртуальных машин Azure безопасный доступ гарантирует группа безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="c8682-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="c8682-131">С образцом приложения hello Music Store все доступа toohello виртуальная машина является ограниченным доступом, за исключением через порт 80 для доступа по протоколу http и порт 22 для доступа по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="c8682-131">With hello Music Store application sample, all access toohello virtual machine is restricted except for over port 80 for http access, and port 22 for SSH access.</span></span> <span data-ttu-id="c8682-132">Tooan шаблона диспетчера ресурсов Azure, с использованием hello Visual Studio новый мастер добавления ресурсов, можно добавить сетевую группу безопасности или путем вставки допустимых данных JSON в шаблон.</span><span class="sxs-lookup"><span data-stu-id="c8682-132">A Network Security Group can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="c8682-133">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [сетевой группы безопасности](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).</span><span class="sxs-lookup"><span data-stu-id="c8682-133">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('nsgfront')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "nsg-front"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
}
```

<span data-ttu-id="c8682-134">В этом примере hello сетевая группа безопасности является, связанных с hello объекта подсети, объявленные в виртуальной сети ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="c8682-134">In this example, hello network security group is associate with hello subnet object declared in hello Virtual Network resource.</span></span> 

<span data-ttu-id="c8682-135">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [связь группы безопасности сети с помощью виртуальной сети](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).</span><span class="sxs-lookup"><span data-stu-id="c8682-135">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).</span></span>

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
```

<span data-ttu-id="c8682-136">Вот какие группы безопасности сети hello как выглядит из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c8682-136">Here is what hello network security group looks like from hello Azure portal.</span></span> <span data-ttu-id="c8682-137">Обратите внимание, что группу безопасности сети можно связать с подсетью и (или) с сетевым интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="c8682-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="c8682-138">В этом случае hello NSG — связанные tooa подсети.</span><span class="sxs-lookup"><span data-stu-id="c8682-138">In this case, hello NSG is associated tooa subnet.</span></span> <span data-ttu-id="c8682-139">В этой конфигурации hello правила для входящих подключений применяются tooall виртуальными машинами, подключенными toohello подсети.</span><span class="sxs-lookup"><span data-stu-id="c8682-139">In this configuration, hello inbound rules apply tooall virtual machines connected toohello subnet.</span></span>

![Группа безопасности сети](./media/dotnet-core-3-access-security/nsg.png)

<span data-ttu-id="c8682-141">Дополнительные сведения о группах безопасности сети см. в статье [Группа безопасности сети](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="c8682-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="c8682-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8682-142">Next step</span></span>
<hr>

[<span data-ttu-id="c8682-143">Шаг 3. Доступность и масштабирование в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c8682-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

