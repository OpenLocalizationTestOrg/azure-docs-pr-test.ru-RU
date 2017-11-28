---
title: "Параметры доступности и масштабирования в шаблонах Azure Resource Manager | Документация Майкрософт"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0c0250b8152ed31b9a5d8b42ae139c9b38da0984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="f23a9-103">Параметры доступности и масштабирования в шаблонах Azure Resource Manager для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="f23a9-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="f23a9-104">Доступность и масштабирование обозначают время непрерывной работы и возможность соответствия требованиям к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="f23a9-104">Availability and scale refer to uptime and the ability to meet demand.</span></span> <span data-ttu-id="f23a9-105">Если приложение должно быть доступным 99,9 % времени, его архитектура должна поддерживать несколько параллельных ресурсов вычислений.</span><span class="sxs-lookup"><span data-stu-id="f23a9-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="f23a9-106">Например, вместо одного веб-сайта конфигурация с высоким уровнем доступности содержит несколько экземпляров одного сайта и использует технологию балансировки.</span><span class="sxs-lookup"><span data-stu-id="f23a9-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span></span> <span data-ttu-id="f23a9-107">В этой конфигурации один экземпляр приложения может быть отключен для обслуживания, а другой продолжать работать.</span><span class="sxs-lookup"><span data-stu-id="f23a9-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span></span> <span data-ttu-id="f23a9-108">Масштабирование, в свою очередь, обозначает возможность приложения удовлетворять требованиям.</span><span class="sxs-lookup"><span data-stu-id="f23a9-108">Scale on the other hand refers to an applications ability to serve demand.</span></span> <span data-ttu-id="f23a9-109">Приложение балансировки нагрузки позволяет добавлять и удалять экземпляры из пула для масштабирования приложения в соответствии с требованиями.</span><span class="sxs-lookup"><span data-stu-id="f23a9-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span></span>

<span data-ttu-id="f23a9-110">В этой статье описано, как настроить развертывание приложения музыкального магазина, чтобы обеспечить доступность и масштабирование.</span><span class="sxs-lookup"><span data-stu-id="f23a9-110">This document details how the Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="f23a9-111">Здесь будут описаны все зависимости и уникальные настройки.</span><span class="sxs-lookup"><span data-stu-id="f23a9-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="f23a9-112">Чтобы оптимизировать процесс, заранее разверните экземпляр решения в подписке Azure, а затем установите шаблон Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f23a9-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="f23a9-113">Полный шаблон можно найти [здесь](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="f23a9-113">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="f23a9-114">Группа доступности</span><span class="sxs-lookup"><span data-stu-id="f23a9-114">Availability Set</span></span>
<span data-ttu-id="f23a9-115">Группа доступности логически охватывает виртуальные машины Azure на физических узлах и другие инфраструктурные компоненты, например источники питания и физическое сетевое оборудование.</span><span class="sxs-lookup"><span data-stu-id="f23a9-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="f23a9-116">Она гарантирует, что в случае обслуживания, сбоя устройства или простоя по другой причине не все виртуальные машины будут затронуты.</span><span class="sxs-lookup"><span data-stu-id="f23a9-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="f23a9-117">Чтобы добавить группу доступности в шаблон Azure Resource Manager, можно использовать мастер добавления нового ресурса в Visual Studio или вставить в шаблон допустимый объект JSON.</span><span class="sxs-lookup"><span data-stu-id="f23a9-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="f23a9-118">Чтобы увидеть пример JSON в шаблоне Resource Manager, щелкните следующую ссылку: [Группа доступности](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span><span class="sxs-lookup"><span data-stu-id="f23a9-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

<span data-ttu-id="f23a9-119">Группа доступности определяется как свойство ресурса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f23a9-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="f23a9-120">Чтобы увидеть пример JSON в шаблоне Resource Manager, щелкните следующую ссылку: [Сопоставление группы доступности с виртуальной машиной](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span><span class="sxs-lookup"><span data-stu-id="f23a9-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="f23a9-121">Ниже приведено представление группы доступности на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f23a9-121">The availability set as seen from the Azure portal.</span></span> <span data-ttu-id="f23a9-122">Здесь можно увидеть каждую виртуальную машину и сведения о конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f23a9-122">Each virtual machine and details about the configuration are detailed here.</span></span>

![Группа доступности](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="f23a9-124">Дополнительные сведения о группах доступности см. в статье [Управление доступностью виртуальных машин](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f23a9-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="f23a9-125">Балансировщик сетевой нагрузки</span><span class="sxs-lookup"><span data-stu-id="f23a9-125">Network Load Balancer</span></span>
<span data-ttu-id="f23a9-126">В то время как группа доступности обеспечивает отказоустойчивость приложения, балансировщик нагрузки обеспечивает доступность нескольких экземпляров приложения по одному сетевому адресу.</span><span class="sxs-lookup"><span data-stu-id="f23a9-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span></span> <span data-ttu-id="f23a9-127">Эти экземпляры могут размещаться на нескольких виртуальных машинах, каждая из которых подключена к балансировщику нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f23a9-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span></span> <span data-ttu-id="f23a9-128">При получении доступа к приложению балансировщик нагрузки направляет входящий запрос к подключенным экземплярам.</span><span class="sxs-lookup"><span data-stu-id="f23a9-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span></span> <span data-ttu-id="f23a9-129">Чтобы добавить балансировщик нагрузки в шаблон Azure Resource Manager, можно использовать мастер добавления нового ресурса в Visual Studio или вставить в шаблон правильно определенный ресурс JSON.</span><span class="sxs-lookup"><span data-stu-id="f23a9-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span></span>

<span data-ttu-id="f23a9-130">Чтобы увидеть пример JSON в шаблоне Resource Manager, щелкните следующую ссылку: [Балансировщик сетевой нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="f23a9-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

<span data-ttu-id="f23a9-131">Так как пример приложения доступен в Интернете по общедоступному IP-адресу, этот адрес связан с балансировщиком нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f23a9-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span></span> 

<span data-ttu-id="f23a9-132">Чтобы увидеть пример JSON в шаблоне Resource Manager, щелкните следующую ссылку: [Сопоставление балансировщика сетевой нагрузки с общедоступным IP-адресом](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span><span class="sxs-lookup"><span data-stu-id="f23a9-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

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

<span data-ttu-id="f23a9-133">На портале Azure в обзоре балансировщика сетевой нагрузки можно увидеть, что он связан с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="f23a9-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span></span>

![Балансировщик сетевой нагрузки](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="f23a9-135">Правило балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="f23a9-135">Load Balancer Rule</span></span>
<span data-ttu-id="f23a9-136">При использовании балансировщика нагрузки настраиваются правила для распределения трафика между целевыми ресурсами.</span><span class="sxs-lookup"><span data-stu-id="f23a9-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span></span> <span data-ttu-id="f23a9-137">В нашем примере приложения музыкального магазина трафик поступает по общедоступному IP-адресу на порт 80 и распределяется в рамках этого порта по всем виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="f23a9-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="f23a9-138">Чтобы увидеть пример JSON в шаблоне Resource Manager, щелкните следующую ссылку: [Правило балансировщика нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="f23a9-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

<span data-ttu-id="f23a9-139">Ниже приведено представление правила балансировщика сетевой нагрузки на портале.</span><span class="sxs-lookup"><span data-stu-id="f23a9-139">A view of the network load balancer rule from the portal.</span></span>

![Правило балансировщика сетевой нагрузки](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="f23a9-141">Проба балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="f23a9-141">Load Balancer Probe</span></span>
<span data-ttu-id="f23a9-142">Чтобы запросы обслуживались только в работающих системах, балансировщику нагрузки необходимо отслеживать каждую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="f23a9-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span></span> <span data-ttu-id="f23a9-143">Для этого он постоянно проверяет предопределенный порт.</span><span class="sxs-lookup"><span data-stu-id="f23a9-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="f23a9-144">Для развертывания приложения музыкального магазина настроено выполнение проверки порта 80 на всех включенных виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="f23a9-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="f23a9-145">Чтобы увидеть пример JSON в шаблоне Resource Manager, щелкните следующую ссылку: [Проба балансировщика нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span><span class="sxs-lookup"><span data-stu-id="f23a9-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

<span data-ttu-id="f23a9-146">Ниже приведено окно пробы балансировщика нагрузки на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f23a9-146">The load balancer probe seen from the Azure portal.</span></span>

![Проба балансировщика сетевой нагрузки](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="f23a9-148">Правила преобразования сетевых адресов для входящих подключений</span><span class="sxs-lookup"><span data-stu-id="f23a9-148">Inbound NAT Rules</span></span>
<span data-ttu-id="f23a9-149">При использовании балансировщика нагрузки правила следует поместить в расположение, обеспечивающее доступ без балансировки нагрузки к каждой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="f23a9-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span></span> <span data-ttu-id="f23a9-150">Например, при создании SSH-подключения к каждой виртуальной машине к этому трафику не следует применять балансировку нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f23a9-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="f23a9-151">Вместо этого необходимо настроить предопределенный путь с использованием ресурса правила NAT для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="f23a9-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="f23a9-152">С помощью этого ресурса входящий трафик можно сопоставить с отдельными виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="f23a9-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span></span> 

<span data-ttu-id="f23a9-153">При использовании приложения музыкального магазина порт, начиная с 5000, сопоставляется с портом 22 на каждой виртуальной машине для SSH-доступа.</span><span class="sxs-lookup"><span data-stu-id="f23a9-153">With the Music Store application, a port starting at 5000 is mapped to port 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="f23a9-154">Функция `copyindex()` используется для последовательного повышения номера входящего порта. Таким образом, вторая виртуальная машина получает входящий порт 5001, третья — 5002 и т. д.</span><span class="sxs-lookup"><span data-stu-id="f23a9-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span></span> 

<span data-ttu-id="f23a9-155">Чтобы увидеть пример JSON в шаблоне Resource Manager, щелкните следующую ссылку: [Правила NAT для входящего трафика](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="f23a9-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="f23a9-156">Ниже приведено представление правила NAT для входящего трафика на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f23a9-156">One example inbound NAT rule as seen in the Azure portal.</span></span> <span data-ttu-id="f23a9-157">Правило NAT SSH создается для каждой виртуальной машины в развертывании.</span><span class="sxs-lookup"><span data-stu-id="f23a9-157">An SSH NAT rule is created for each virtual machine in the deployment.</span></span>

![Правило NAT для входящего трафика](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="f23a9-159">Дополнительные сведения о балансировщике сетевой нагрузки Azure см. в статье [Балансировка нагрузки для служб инфраструктуры Azure](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f23a9-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="f23a9-160">Развертывание нескольких виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="f23a9-160">Deploy multiple VMs</span></span>
<span data-ttu-id="f23a9-161">Наконец, для эффективной работы группы доступности или балансировщика нагрузки необходимо несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f23a9-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="f23a9-162">Их можно развернуть с помощью функции копирования шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f23a9-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span></span> <span data-ttu-id="f23a9-163">В таком случае не нужно определять конечное число виртуальных машин. Это значение может быть предоставлено динамически во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="f23a9-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span></span> <span data-ttu-id="f23a9-164">Функция копирования принимает число экземпляров для создания и обрабатывает развертывание правильного количества виртуальных машин и связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f23a9-164">The copy function consumes the number of instances to created and handles deploying the proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="f23a9-165">В шаблоне примера приложения музыкального магазина определен параметр, принимающий число экземпляров.</span><span class="sxs-lookup"><span data-stu-id="f23a9-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="f23a9-166">Это число используется в шаблоне при создании виртуальных машин и связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f23a9-166">This number is used throughout the template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances to be created behind load balancer."
  }
}
```

<span data-ttu-id="f23a9-167">В ресурсе виртуальной машины циклу копирования присваивается имя и используется параметр числа экземпляров для управления количеством полученных копий.</span><span class="sxs-lookup"><span data-stu-id="f23a9-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span></span>

<span data-ttu-id="f23a9-168">Чтобы увидеть пример JSON в шаблоне Resource Manager, щелкните следующую ссылку: [Функция копирования виртуальной машины](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span><span class="sxs-lookup"><span data-stu-id="f23a9-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

<span data-ttu-id="f23a9-169">Доступ к текущей итерации функции копирования можно получить с помощью функции `copyIndex()` .</span><span class="sxs-lookup"><span data-stu-id="f23a9-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span></span> <span data-ttu-id="f23a9-170">Значение функции копирования индекса можно использовать для присвоения имен виртуальным машинам и другим ресурсам.</span><span class="sxs-lookup"><span data-stu-id="f23a9-170">The value of the copy index function can be used to name virtual machines and other resources.</span></span> <span data-ttu-id="f23a9-171">Например, если развернуты два экземпляра виртуальной машины, им необходимо присвоить разные имена.</span><span class="sxs-lookup"><span data-stu-id="f23a9-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="f23a9-172">Функцию `copyIndex()` можно использовать как часть имени виртуальной машины для создания уникального имени.</span><span class="sxs-lookup"><span data-stu-id="f23a9-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span></span> <span data-ttu-id="f23a9-173">Пример функции `copyindex()` , используемой для именования, можно увидеть в ресурсе виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f23a9-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span></span> <span data-ttu-id="f23a9-174">Здесь имя компьютера представляет собой объединение параметра `vmName` и функции `copyIndex()`.</span><span class="sxs-lookup"><span data-stu-id="f23a9-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span></span> 

<span data-ttu-id="f23a9-175">Чтобы увидеть пример JSON в шаблоне Resource Manager, щелкните следующую ссылку: [Функция копирования индекса](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span><span class="sxs-lookup"><span data-stu-id="f23a9-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

<span data-ttu-id="f23a9-176">В шаблоне примера приложения музыкального магазина функция `copyIndex` используется несколько раз.</span><span class="sxs-lookup"><span data-stu-id="f23a9-176">The `copyIndex` function is used several times in the Music Store sample template.</span></span> <span data-ttu-id="f23a9-177">Ресурсы и функции, использующие `copyIndex`, представлены такими компонентами отдельного экземпляра виртуальной машины, как сетевой интерфейс, правила подсистемы балансировки нагрузки и пр. (в зависимости от функций).</span><span class="sxs-lookup"><span data-stu-id="f23a9-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="f23a9-178">Дополнительные сведения о функции копирования см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f23a9-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="f23a9-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f23a9-179">Next step</span></span>
<hr>

[<span data-ttu-id="f23a9-180">Шаг 4. Развертывание приложений с использованием шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f23a9-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

