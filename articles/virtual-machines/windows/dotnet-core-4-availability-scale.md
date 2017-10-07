---
title: "aaaAvailability и масштабирования в шаблоны диспетчера ресурсов Azure | Документы Microsoft"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 494724b5-06af-4dea-a774-ba580cf27527
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a122d8e9536ea5fc2dc9c3f84042ed5c5179d783
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="8c6a9-103">Параметры доступности и масштабирования в шаблонах Azure Resource Manager для виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="8c6a9-103">Availability and scale in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="8c6a9-104">См. toouptime и hello запросу toomeet возможности высокой доступности и масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-104">Availability and scale refer toouptime and hello ability toomeet demand.</span></span> <span data-ttu-id="8c6a9-105">Если приложение должно быть 99,9% времени hello, он должен toohave архитектуру, которая позволяет нескольким ресурсам параллельных вычислений.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-105">If an application must be up 99.9% of hello time, it needs toohave an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="8c6a9-106">Например вместо одного веб-сайта, конфигурации с более высоким уровнем доступности содержится несколько экземпляров hello же сайт, с технологией перед их балансировки.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of hello same site, with balancing technology in front of them.</span></span> <span data-ttu-id="8c6a9-107">В этой конфигурации один экземпляр приложения hello можно отключить для обслуживания, прерывая toofunction оставшихся hello.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-107">In this configuration, one instance of hello application can be taken down for maintenance, while hello remaining continue toofunction.</span></span> <span data-ttu-id="8c6a9-108">Масштаб на hello другой стороны относится возможность tooserve tooan приложений запросу.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-108">Scale on hello other hand refers tooan applications ability tooserve demand.</span></span> <span data-ttu-id="8c6a9-109">С загрузкой балансировкой приложения, добавление или удаление экземпляров из пула hello позволяет запросу toomeet tooscale приложения.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-109">With a load balanced application, adding or removing instances from hello pool allows an application tooscale toomeet demand.</span></span>

<span data-ttu-id="8c6a9-110">В этом документе описаны как hello развертывания образца Music Store настраивается для высокой доступности и масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-110">This document details how hello Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="8c6a9-111">Здесь будут описаны все зависимости и уникальные настройки.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="8c6a9-112">Для получения наилучших результатов hello предварительно разверните экземпляр tooyour решения hello подписки Azure, работают вместе с hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-112">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="8c6a9-113">Полный шаблон Hello можно найти здесь — [музыка хранилища развертывания в Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-113">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="availability-set"></a><span data-ttu-id="8c6a9-114">Группа доступности</span><span class="sxs-lookup"><span data-stu-id="8c6a9-114">Availability Set</span></span>
<span data-ttu-id="8c6a9-115">Группа доступности логически охватывает виртуальные машины Azure на физических узлах и другие инфраструктурные компоненты, например источники питания и физическое сетевое оборудование.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="8c6a9-116">Она гарантирует, что в случае обслуживания, сбоя устройства или простоя по другой причине не все виртуальные машины будут затронуты.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="8c6a9-117">Группы доступности могут быть добавлены tooan шаблона Azure Resource Manager с помощью Visual Studio новый мастер добавления ресурсов hello или вставка допустимых данных JSON в шаблон.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-117">An Availability Set can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="8c6a9-118">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [набор доступности](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-118">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "availability-set"
  },
  "properties": {
  }
}
```

<span data-ttu-id="8c6a9-119">Группа доступности определяется как свойство ресурса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="8c6a9-120">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [набор доступности связи с виртуальной машиной](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-120">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="8c6a9-121">Hello доступности, как видно из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-121">hello availability set as seen from hello Azure portal.</span></span> <span data-ttu-id="8c6a9-122">Каждой виртуальной машине и сведения о конфигурации hello подробно описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-122">Each virtual machine and details about hello configuration are detailed here.</span></span>

![Группа доступности](./media/dotnet-core-4-availability-scale/ase-win.png)

<span data-ttu-id="8c6a9-124">Дополнительные сведения о группах доступности см. в статье [Управление доступностью виртуальных машин](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="8c6a9-125">Балансировщик сетевой нагрузки</span><span class="sxs-lookup"><span data-stu-id="8c6a9-125">Network Load Balancer</span></span>
<span data-ttu-id="8c6a9-126">В то время как группа доступности обеспечивает устойчивость к сбоям приложения, подсистемы балансировки нагрузки создает много экземпляров приложения hello на одного сетевого адреса.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of hello application available on a single network address.</span></span> <span data-ttu-id="8c6a9-127">Несколько экземпляров приложения могут размещаться на нескольких виртуальных машин, каждый из них подключен tooa подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-127">Multiple instances of an application can be hosted on many virtual machines, each one connected tooa load balancer.</span></span> <span data-ttu-id="8c6a9-128">Как осуществляется приложения hello, маршруты подсистемы балансировки нагрузки hello hello входящего запроса участниках присоединенного hello.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-128">As hello application is accessed, hello load balancer routes hello incoming request across hello attached members.</span></span> <span data-ttu-id="8c6a9-129">Подсистема балансировки нагрузки могут добавляться с помощью Visual Studio новый мастер добавления ресурсов hello или путем вставки должным образом в формате JSON ресурсов в шаблон диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-129">A Load Balancer can be added using hello Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into hello Azure Resource Manager template.</span></span>

<span data-ttu-id="8c6a9-130">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [балансировки сетевой нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer"
  },
  ........<truncated>
}
```

<span data-ttu-id="8c6a9-131">Так как пример приложения hello предоставляется toohello Интернет, общий IP-адрес, этот адрес связан с подсистемой балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-131">Because hello sample application is exposed toohello internet with a public IP address, this address is associated with hello load balancer.</span></span> 

<span data-ttu-id="8c6a9-132">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [связь балансировки сетевой нагрузки с общедоступным IP-адресом](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-132">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="8c6a9-133">От hello портал Azure hello Обзор балансировки сетевой нагрузки показывает hello связь с hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-133">From hello Azure portal, hello network load balancer overview shows hello association with hello public IP address.</span></span>

![Балансировщик сетевой нагрузки](./media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="8c6a9-135">Правило балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="8c6a9-135">Load Balancer Rule</span></span>
<span data-ttu-id="8c6a9-136">При использовании подсистемы балансировки нагрузки, настроены правила, определяющие, как трафик распределяется по всем ресурсам hello предназначен.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-136">When using a load balancer, rules are configured that control how traffic is balanced across hello intended resources.</span></span> <span data-ttu-id="8c6a9-137">Приложение Music Store образец hello трафик порта 80 hello общедоступного IP-адреса и распределяется по порту 80 всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-137">With hello sample Music Store application, traffic arrives on port 80 of hello public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="8c6a9-138">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [правило подсистемы балансировки нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-138">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span></span>

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

<span data-ttu-id="8c6a9-139">Представление в виде сети hello правило подсистемы балансировки нагрузки с портала hello.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-139">A view of hello network load balancer rule from hello portal.</span></span>

![Правило балансировщика сетевой нагрузки](./media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="8c6a9-141">Проба балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="8c6a9-141">Load Balancer Probe</span></span>
<span data-ttu-id="8c6a9-142">Hello балансировки нагрузки также требуется toomonitor каждой виртуальной машины, чтобы запросы обслуживаются только toorunning системы.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-142">hello load balancer also needs toomonitor each virtual machine so that requests are served only toorunning systems.</span></span> <span data-ttu-id="8c6a9-143">Для этого он постоянно проверяет предопределенный порт.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="8c6a9-144">Развертывание Music Store Hello — tooprobe настроенный порт 80 на всех включенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-144">hello Music Store deployment is configured tooprobe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="8c6a9-145">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [пробы подсистемы балансировки нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-145">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span></span>

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

<span data-ttu-id="8c6a9-146">с портала Azure hello Hello зонд подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-146">hello load balancer probe seen from hello Azure portal.</span></span>

![Проба балансировщика сетевой нагрузки](./media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="8c6a9-148">Правила преобразования сетевых адресов для входящих подключений</span><span class="sxs-lookup"><span data-stu-id="8c6a9-148">Inbound NAT Rules</span></span>
<span data-ttu-id="8c6a9-149">При использовании подсистемы балансировки нагрузки, правила должны toobe помещен на место, которые предоставляют Сбалансированный доступа без загрузки tooeach виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-149">When using a Load Balancer, rules need toobe put into place that provide non-load balanced access tooeach Virtual Machine.</span></span> <span data-ttu-id="8c6a9-150">Например, при создании RDP-подключения к каждой виртуальной машине для этого трафика не следует применять балансировку нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-150">For instance, when creating an RDP connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="8c6a9-151">Вместо этого необходимо настроить предопределенный путь с использованием ресурса правила NAT для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-151">Pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="8c6a9-152">Использовать этот ресурс, входящих сообщений может быть сопоставленных tooindividual виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-152">Using this resource, inbound communication can be mapped tooindividual Virtual Machines.</span></span> 

<span data-ttu-id="8c6a9-153">С hello приложение Music Store начиная с 5000 порта — сопоставленных tooport 3389 на каждой виртуальной машине для RDP-доступ.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-153">With hello Music Store application, a port starting at 5000 is mapped tooport 3389 on each Virtual Machine for RDP access.</span></span> <span data-ttu-id="8c6a9-154">Hello `copyindex()` функция является используется tooincrement Здравствуйте входящий порт, таким образом, что hello второй виртуальной машины получит входящий порт 5001, hello 5002 третьей и т. д.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-154">hello `copyindex()` function is used tooincrement hello incoming port, such that hello second Virtual Machine receives an incoming port of 5001, hello third 5002, and so on.</span></span>

<span data-ttu-id="8c6a9-155">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [правила для входящих подключений NAT](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-155">Follow this link toosee hello JSON sample within hello Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'RDP-VM', copyIndex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
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
    "backendPort": 3389,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="8c6a9-156">Один пример правила для входящего трафика NAT как hello возникающим в портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-156">One example inbound NAT rule as seen in hello Azure portal.</span></span> <span data-ttu-id="8c6a9-157">Правило NAT протокола удаленного рабочего СТОЛА создается для каждой виртуальной машины в развертывании hello.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-157">An RDP NAT rule is created for each virtual machine in hello deployment.</span></span>

![Правило NAT для входящего трафика](./media/dotnet-core-4-availability-scale/natrule-win.png)

<span data-ttu-id="8c6a9-159">Подробные сведения о hello Azure балансировки сетевой нагрузки см. в разделе [балансировки нагрузки для служб инфраструктуры Azure](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-159">For in-depth information on hello Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="8c6a9-160">Развертывание нескольких виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="8c6a9-160">Deploy multiple VMs</span></span>
<span data-ttu-id="8c6a9-161">Наконец функция tooeffectively группе доступности или балансировки нагрузки необходимы несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-161">Finally, for an Availability Set or Load Balancer tooeffectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="8c6a9-162">Несколько виртуальных машин можно развернуть с помощью функции копирования шаблона диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-162">Multiple VMs can be deployed using hello Azure Resource Manager template copy function.</span></span> <span data-ttu-id="8c6a9-163">С помощью функции копирования hello, это не требуется toodefine ограниченное число виртуальных машин, вместо этого значения могут быть предоставлены динамически во время развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-163">Using hello copy function, it is not necessary toodefine a finite number of Virtual Machines, rather this value can be dynamically provided at hello time of deployment.</span></span> <span data-ttu-id="8c6a9-164">функция копирования Hello потребляет hello число экземпляров toobe создан и обрабатывает развертывание hello нужное число виртуальных машин и связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-164">hello copy function consumes hello number of instances toobe created and handles deploying hello proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="8c6a9-165">В шаблоне музыка хранилища образец hello параметр определен, принимающий в число экземпляров.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-165">In hello Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="8c6a9-166">Этот номер используется во всех hello шаблона при создании виртуальных машин и связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-166">This number is used throughout hello template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
},
```

<span data-ttu-id="8c6a9-167">На hello ресурса виртуальной машины цикл hello копии присваивается имя и hello число экземпляров параметра toocontrol hello число полученный копий.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-167">On hello Virtual Machine resource, hello copy loop is given a name and hello number of instances parameter used toocontrol hello number of resulting copies.</span></span>

<span data-ttu-id="8c6a9-168">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [функции копирования виртуальной машины](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-168">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  }
```

<span data-ttu-id="8c6a9-169">Текущая итерация Hello функции копирования hello можно осуществить с помощью hello `copyIndex()` функции.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-169">hello current iteration of hello copy function can be accessed with hello `copyIndex()` function.</span></span> <span data-ttu-id="8c6a9-170">Hello значение индекса функции hello копирования может быть используется tooname виртуальные машины и другие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-170">hello value of hello copy index function can be used tooname virtual machines and other resources.</span></span> <span data-ttu-id="8c6a9-171">Например, если развернуты два экземпляра виртуальной машины, им необходимо присвоить разные имена.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="8c6a9-172">Hello `copyIndex()` функция может использоваться как часть виртуальной машины hello имя toocreate уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-172">hello `copyIndex()` function can be used as part of hello virtual machine name toocreate a unique name.</span></span> <span data-ttu-id="8c6a9-173">Пример hello `copyindex()` функция, используемая для именования можно увидеть в hello ресурса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-173">An example of hello `copyindex()` function used for naming purposes can be seen in hello Virtual Machine resource.</span></span> <span data-ttu-id="8c6a9-174">Здесь hello имя компьютера представляет собой объединение hello `vmName` параметр и hello `copyIndex()` функции.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-174">Here, hello computer name is a concatenation of hello `vmName` parameter, and hello `copyIndex()` function.</span></span> 

<span data-ttu-id="8c6a9-175">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [функции копирования в индекс](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-175">Follow this link toosee hello JSON sample within hello Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

<span data-ttu-id="8c6a9-176">Hello `copyIndex` функция используется несколько раз в шаблоне образец hello Music Store.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-176">hello `copyIndex` function is used several times in hello Music Store sample template.</span></span> <span data-ttu-id="8c6a9-177">Ресурсы и использование функции `copyIndex` включают один экземпляр hello виртуальной машины такой что-либо конкретных tooa и сетевого интерфейса, правила подсистемы балансировки нагрузки, и любые зависит от функции.</span><span class="sxs-lookup"><span data-stu-id="8c6a9-177">Resources and functions utilizing `copyIndex` include anything specific tooa single instance of hello virtual machine such and network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="8c6a9-178">Дополнительные сведения о функции копирования hello см. в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8c6a9-178">For more information on hello copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="8c6a9-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8c6a9-179">Next step</span></span>
<hr>

[<span data-ttu-id="8c6a9-180">Шаг 4. Развертывание приложений с использованием шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8c6a9-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

