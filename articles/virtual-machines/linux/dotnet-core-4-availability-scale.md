---
title: "aaaAvailability и масштабирования в шаблоны диспетчера ресурсов Azure | Документы Microsoft"
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
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="cafec-103">Параметры доступности и масштабирования в шаблонах Azure Resource Manager для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="cafec-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="cafec-104">См. toouptime и hello запросу toomeet возможности высокой доступности и масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="cafec-104">Availability and scale refer toouptime and hello ability toomeet demand.</span></span> <span data-ttu-id="cafec-105">Если приложение должно быть 99,9% времени hello, он должен toohave архитектуру, которая позволяет нескольким ресурсам параллельных вычислений.</span><span class="sxs-lookup"><span data-stu-id="cafec-105">If an application must be up 99.9% of hello time, it needs toohave an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="cafec-106">Например вместо одного веб-сайта, конфигурации с более высоким уровнем доступности содержится несколько экземпляров hello же сайт, с технологией перед их балансировки.</span><span class="sxs-lookup"><span data-stu-id="cafec-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of hello same site, with balancing technology in front of them.</span></span> <span data-ttu-id="cafec-107">В этой конфигурации один экземпляр приложения hello можно отключить для обслуживания, прерывая toofunction оставшихся hello.</span><span class="sxs-lookup"><span data-stu-id="cafec-107">In this configuration, one instance of hello application can be taken down for maintenance, while hello remaining continue toofunction.</span></span> <span data-ttu-id="cafec-108">Масштаб на hello другой стороны относится возможность tooserve tooan приложений запросу.</span><span class="sxs-lookup"><span data-stu-id="cafec-108">Scale on hello other hand refers tooan applications ability tooserve demand.</span></span> <span data-ttu-id="cafec-109">С загрузкой балансировкой приложения, добавление или удаление экземпляров из пула hello позволяет запросу toomeet tooscale приложения.</span><span class="sxs-lookup"><span data-stu-id="cafec-109">With a load balanced application, adding or removing instances from hello pool allows an application tooscale toomeet demand.</span></span>

<span data-ttu-id="cafec-110">В этом документе описаны как hello развертывания образца Music Store настраивается для высокой доступности и масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="cafec-110">This document details how hello Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="cafec-111">Здесь будут описаны все зависимости и уникальные настройки.</span><span class="sxs-lookup"><span data-stu-id="cafec-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="cafec-112">Для получения наилучших результатов hello предварительно разверните экземпляр tooyour решения hello подписки Azure, работают вместе с hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="cafec-112">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="cafec-113">Полный шаблон Hello можно найти здесь — [музыка хранилища развертывания на Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="cafec-113">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="cafec-114">Группа доступности</span><span class="sxs-lookup"><span data-stu-id="cafec-114">Availability Set</span></span>
<span data-ttu-id="cafec-115">Группа доступности логически охватывает виртуальные машины Azure на физических узлах и другие инфраструктурные компоненты, например источники питания и физическое сетевое оборудование.</span><span class="sxs-lookup"><span data-stu-id="cafec-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="cafec-116">Она гарантирует, что в случае обслуживания, сбоя устройства или простоя по другой причине не все виртуальные машины будут затронуты.</span><span class="sxs-lookup"><span data-stu-id="cafec-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="cafec-117">Группы доступности могут быть добавлены tooan шаблона Azure Resource Manager с помощью Visual Studio новый мастер добавления ресурсов hello или вставка допустимых данных JSON в шаблон.</span><span class="sxs-lookup"><span data-stu-id="cafec-117">An Availability Set can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="cafec-118">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [набор доступности](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span><span class="sxs-lookup"><span data-stu-id="cafec-118">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

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

<span data-ttu-id="cafec-119">Группа доступности определяется как свойство ресурса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cafec-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="cafec-120">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [набор доступности связи с виртуальной машиной](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span><span class="sxs-lookup"><span data-stu-id="cafec-120">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="cafec-121">Hello доступности, как видно из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cafec-121">hello availability set as seen from hello Azure portal.</span></span> <span data-ttu-id="cafec-122">Каждой виртуальной машине и сведения о конфигурации hello подробно описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="cafec-122">Each virtual machine and details about hello configuration are detailed here.</span></span>

![Группа доступности](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="cafec-124">Дополнительные сведения о группах доступности см. в статье [Управление доступностью виртуальных машин](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cafec-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="cafec-125">Балансировщик сетевой нагрузки</span><span class="sxs-lookup"><span data-stu-id="cafec-125">Network Load Balancer</span></span>
<span data-ttu-id="cafec-126">В то время как группа доступности обеспечивает устойчивость к сбоям приложения, подсистемы балансировки нагрузки создает много экземпляров приложения hello на одного сетевого адреса.</span><span class="sxs-lookup"><span data-stu-id="cafec-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of hello application available on a single network address.</span></span> <span data-ttu-id="cafec-127">Несколько экземпляров приложения могут размещаться на нескольких виртуальных машин, каждый из них подключен tooa подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cafec-127">Multiple instances of an application can be hosted on many virtual machines, each one connected tooa load balancer.</span></span> <span data-ttu-id="cafec-128">Как осуществляется приложения hello, маршруты подсистемы балансировки нагрузки hello hello входящего запроса участниках присоединенного hello.</span><span class="sxs-lookup"><span data-stu-id="cafec-128">As hello application is accessed, hello load balancer routes hello incoming request across hello attached members.</span></span> <span data-ttu-id="cafec-129">Подсистема балансировки нагрузки могут добавляться с помощью Visual Studio новый мастер добавления ресурсов hello или путем вставки должным образом в формате JSON ресурсов в шаблон диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="cafec-129">A Load Balancer can be added using hello Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into hello Azure Resource Manager template.</span></span>

<span data-ttu-id="cafec-130">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [балансировки сетевой нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="cafec-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

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

<span data-ttu-id="cafec-131">Так как пример приложения hello предоставляется toohello Интернет, общий IP-адрес, этот адрес связан с подсистемой балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="cafec-131">Because hello sample application is exposed toohello internet with a public IP address, this address is associated with hello load balancer.</span></span> 

<span data-ttu-id="cafec-132">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [связь балансировки сетевой нагрузки с общедоступным IP-адресом](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span><span class="sxs-lookup"><span data-stu-id="cafec-132">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

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

<span data-ttu-id="cafec-133">От hello портал Azure hello Обзор балансировки сетевой нагрузки показывает hello связь с hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="cafec-133">From hello Azure portal, hello network load balancer overview shows hello association with hello public IP address.</span></span>

![Балансировщик сетевой нагрузки](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="cafec-135">Правило балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="cafec-135">Load Balancer Rule</span></span>
<span data-ttu-id="cafec-136">При использовании подсистемы балансировки нагрузки, настроены правила, определяющие, как трафик распределяется по всем ресурсам hello предназначен.</span><span class="sxs-lookup"><span data-stu-id="cafec-136">When using a load balancer, rules are configured that control how traffic is balanced across hello intended resources.</span></span> <span data-ttu-id="cafec-137">Приложение Music Store образец hello трафик порта 80 hello общедоступного IP-адреса и распределяется по порту 80 всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cafec-137">With hello sample Music Store application, traffic arrives on port 80 of hello public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="cafec-138">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [правило подсистемы балансировки нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="cafec-138">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

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

<span data-ttu-id="cafec-139">Представление в виде сети hello правило подсистемы балансировки нагрузки с портала hello.</span><span class="sxs-lookup"><span data-stu-id="cafec-139">A view of hello network load balancer rule from hello portal.</span></span>

![Правило балансировщика сетевой нагрузки](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="cafec-141">Проба балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="cafec-141">Load Balancer Probe</span></span>
<span data-ttu-id="cafec-142">Hello балансировки нагрузки также требуется toomonitor каждой виртуальной машины, чтобы запросы обслуживаются только toorunning системы.</span><span class="sxs-lookup"><span data-stu-id="cafec-142">hello load balancer also needs toomonitor each virtual machine so that requests are served only toorunning systems.</span></span> <span data-ttu-id="cafec-143">Для этого он постоянно проверяет предопределенный порт.</span><span class="sxs-lookup"><span data-stu-id="cafec-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="cafec-144">Развертывание Music Store Hello — tooprobe настроенный порт 80 на всех включенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cafec-144">hello Music Store deployment is configured tooprobe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="cafec-145">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [пробы подсистемы балансировки нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span><span class="sxs-lookup"><span data-stu-id="cafec-145">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

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

<span data-ttu-id="cafec-146">с портала Azure hello Hello зонд подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cafec-146">hello load balancer probe seen from hello Azure portal.</span></span>

![Проба балансировщика сетевой нагрузки](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="cafec-148">Правила преобразования сетевых адресов для входящих подключений</span><span class="sxs-lookup"><span data-stu-id="cafec-148">Inbound NAT Rules</span></span>
<span data-ttu-id="cafec-149">При использовании подсистемы балансировки нагрузки, правила должны toobe помещен на место, которые предоставляют Сбалансированный доступа без загрузки tooeach виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cafec-149">When using a Load Balancer, rules need toobe put into place that provide non-load balanced access tooeach Virtual Machine.</span></span> <span data-ttu-id="cafec-150">Например, при создании SSH-подключения к каждой виртуальной машине к этому трафику не следует применять балансировку нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cafec-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="cafec-151">Вместо этого необходимо настроить предопределенный путь с использованием ресурса правила NAT для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="cafec-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="cafec-152">Использовать этот ресурс, входящих сообщений может быть сопоставленных tooindividual виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cafec-152">Using this resource, inbound communication can be mapped tooindividual Virtual Machines.</span></span> 

<span data-ttu-id="cafec-153">С hello приложение Music Store начиная с 5000 порта — сопоставленных tooport 22 на каждой виртуальной машине для доступа по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="cafec-153">With hello Music Store application, a port starting at 5000 is mapped tooport 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="cafec-154">Hello `copyindex()` функция является используется tooincrement Здравствуйте входящий порт, таким образом, что hello второй виртуальной машины получит входящий порт 5001, hello 5002 третьей и т. д.</span><span class="sxs-lookup"><span data-stu-id="cafec-154">hello `copyindex()` function is used tooincrement hello incoming port, such that hello second Virtual Machine receives an incoming port of 5001, hello third 5002, and so on.</span></span> 

<span data-ttu-id="cafec-155">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [правила для входящих подключений NAT](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="cafec-155">Follow this link toosee hello JSON sample within hello Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

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

<span data-ttu-id="cafec-156">Один пример правила для входящего трафика NAT как hello возникающим в портале Azure.</span><span class="sxs-lookup"><span data-stu-id="cafec-156">One example inbound NAT rule as seen in hello Azure portal.</span></span> <span data-ttu-id="cafec-157">Правило SSH NAT создается для каждой виртуальной машины в развертывании hello.</span><span class="sxs-lookup"><span data-stu-id="cafec-157">An SSH NAT rule is created for each virtual machine in hello deployment.</span></span>

![Правило NAT для входящего трафика](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="cafec-159">Подробные сведения о hello Azure балансировки сетевой нагрузки см. в разделе [балансировки нагрузки для служб инфраструктуры Azure](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cafec-159">For in-depth information on hello Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="cafec-160">Развертывание нескольких виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="cafec-160">Deploy multiple VMs</span></span>
<span data-ttu-id="cafec-161">Наконец функция tooeffectively группе доступности или балансировки нагрузки необходимы несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cafec-161">Finally, for an Availability Set or Load Balancer tooeffectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="cafec-162">Несколько виртуальных машин можно развернуть с помощью функции копирования шаблона диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="cafec-162">Multiple VMs can be deployed using hello Azure Resource Manager template copy function.</span></span> <span data-ttu-id="cafec-163">С помощью функции копирования hello, это не требуется toodefine ограниченное число виртуальных машин, вместо этого значения могут быть предоставлены динамически во время развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="cafec-163">Using hello copy function, it is not necessary toodefine a finite number of Virtual Machines, rather this value can be dynamically provided at hello time of deployment.</span></span> <span data-ttu-id="cafec-164">функция копирования Hello потребляет hello число экземпляров toocreated и обрабатывает развертывание hello нужное число виртуальных машин и связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cafec-164">hello copy function consumes hello number of instances toocreated and handles deploying hello proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="cafec-165">В шаблоне музыка хранилища образец hello параметр определен, принимающий в число экземпляров.</span><span class="sxs-lookup"><span data-stu-id="cafec-165">In hello Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="cafec-166">Этот номер используется во всех hello шаблона при создании виртуальных машин и связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="cafec-166">This number is used throughout hello template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

<span data-ttu-id="cafec-167">На hello ресурса виртуальной машины цикл hello копии присваивается имя и hello число экземпляров параметра toocontrol hello число полученный копий.</span><span class="sxs-lookup"><span data-stu-id="cafec-167">On hello Virtual Machine resource, hello copy loop is given a name and hello number of instances parameter used toocontrol hello number of resulting copies.</span></span>

<span data-ttu-id="cafec-168">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [функции копирования виртуальной машины](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span><span class="sxs-lookup"><span data-stu-id="cafec-168">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

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

<span data-ttu-id="cafec-169">Текущая итерация Hello функции копирования hello можно осуществить с помощью hello `copyIndex()` функции.</span><span class="sxs-lookup"><span data-stu-id="cafec-169">hello current iteration of hello copy function can be accessed with hello `copyIndex()` function.</span></span> <span data-ttu-id="cafec-170">Hello значение индекса функции hello копирования может быть используется tooname виртуальные машины и другие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="cafec-170">hello value of hello copy index function can be used tooname virtual machines and other resources.</span></span> <span data-ttu-id="cafec-171">Например, если развернуты два экземпляра виртуальной машины, им необходимо присвоить разные имена.</span><span class="sxs-lookup"><span data-stu-id="cafec-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="cafec-172">Hello `copyIndex()` функция может использоваться как часть виртуальной машины hello имя toocreate уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="cafec-172">hello `copyIndex()` function can be used as part of hello virtual machine name toocreate a unique name.</span></span> <span data-ttu-id="cafec-173">Пример hello `copyindex()` функция, используемая для именования можно увидеть в hello ресурса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cafec-173">An example of hello `copyindex()` function used for naming purposes can be seen in hello Virtual Machine resource.</span></span> <span data-ttu-id="cafec-174">Здесь hello имя компьютера представляет собой объединение hello `vmName` параметр и hello `copyIndex()` функции.</span><span class="sxs-lookup"><span data-stu-id="cafec-174">Here, hello computer name is a concatenation of hello `vmName` parameter, and hello `copyIndex()` function.</span></span> 

<span data-ttu-id="cafec-175">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [функции копирования в индекс](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span><span class="sxs-lookup"><span data-stu-id="cafec-175">Follow this link toosee hello JSON sample within hello Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

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

<span data-ttu-id="cafec-176">Hello `copyIndex` функция используется несколько раз в шаблоне образец hello Music Store.</span><span class="sxs-lookup"><span data-stu-id="cafec-176">hello `copyIndex` function is used several times in hello Music Store sample template.</span></span> <span data-ttu-id="cafec-177">Ресурсы и использование функции `copyIndex` включать любые определенные tooa один экземпляр hello виртуальной машины, например сетевого интерфейса, правила подсистемы балансировки нагрузки, и любые зависит от функции.</span><span class="sxs-lookup"><span data-stu-id="cafec-177">Resources and functions utilizing `copyIndex` include anything specific tooa single instance of hello virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="cafec-178">Дополнительные сведения о функции копирования hello см. в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="cafec-178">For more information on hello copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="cafec-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cafec-179">Next step</span></span>
<hr>

[<span data-ttu-id="cafec-180">Шаг 4. Развертывание приложений с использованием шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cafec-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

