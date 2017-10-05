---
title: "Создание правила Azure Load Balancer для кластера"
description: "Настройте Azure Load Balancer, чтобы открыть порты для кластера Azure Service Fabric."
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: c99c4d9f343ca97fd3cd363fb54feaf5507bb77c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="48396-103">Открытие портов для кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="48396-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="48396-104">Подсистема балансировки нагрузки, развернутая вместе с кластером Azure Service Fabric, направляет трафик в ваше приложение, работающее на узле.</span><span class="sxs-lookup"><span data-stu-id="48396-104">The load balancer deployed with your Azure Service Fabric cluster directs traffic to your app running on a node.</span></span> <span data-ttu-id="48396-105">Если изменить настройки приложения, чтобы использовать другой порт, необходимо предоставить этот порт в Azure Load Balancer (или направлять трафик через другой порт).</span><span class="sxs-lookup"><span data-stu-id="48396-105">If you change your app to use a different port, you must expose that port (or route a different port) in the Azure Load Balancer.</span></span>

<span data-ttu-id="48396-106">Подсистема балансировки нагрузки была создана автоматически при развертывании кластера Service Fabric в Azure.</span><span class="sxs-lookup"><span data-stu-id="48396-106">When you deployed your service fabric cluster to Azure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="48396-107">Если у вас нет подсистемы балансировки нагрузки, ознакомьтесь с разделом [Создание балансировщика нагрузки для Интернета на портале Azure](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="48396-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="48396-108">Настройка Service Fabric</span><span class="sxs-lookup"><span data-stu-id="48396-108">Configure service fabric</span></span>

<span data-ttu-id="48396-109">Файл конфигурации **ServiceManifest.xml** приложения Service Fabric определяет конечные точки, которые будет использовать приложение.</span><span class="sxs-lookup"><span data-stu-id="48396-109">Your Service Fabric application **ServiceManifest.xml** config file defines the endpoints your application expects to use.</span></span> <span data-ttu-id="48396-110">После обновления файла конфигурации для определения конечной точки необходимо обновить подсистему балансировки нагрузки, чтобы предоставить этот (или другой) порт.</span><span class="sxs-lookup"><span data-stu-id="48396-110">After the config file has been updated to define an endpoint, the load balancer must be updated to expose that (or a different) port.</span></span> <span data-ttu-id="48396-111">Дополнительные сведения о том, как создать конечную точку Service Fabric, см. в разделе [Указание ресурсов в манифесте службы](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="48396-111">For more information on how to create the service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="48396-112">Создание правила балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="48396-112">Create a load balancer rule</span></span>

<span data-ttu-id="48396-113">Правило подсистемы балансировки нагрузки открывает порт с доступом к Интернету и перенаправляет трафик на порт внутреннего узла, используемый вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="48396-113">A load balancer rule opens up an internet-facing port and forwards traffic to the internal node's port used by your application.</span></span> <span data-ttu-id="48396-114">Если у вас нет подсистемы балансировки нагрузки, ознакомьтесь с разделом [Создание балансировщика нагрузки для Интернета на портале Azure](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="48396-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="48396-115">Чтобы создать правило подсистемы балансировки нагрузки, необходимо собрать следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="48396-115">To create a load balancer rule, you need to collect the following information:</span></span>

- <span data-ttu-id="48396-116">имя подсистемы балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="48396-116">Load balancer name.</span></span>
- <span data-ttu-id="48396-117">группа ресурсов подсистемы балансировки нагрузки и кластера Service Fabric;</span><span class="sxs-lookup"><span data-stu-id="48396-117">Resource group of the load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="48396-118">внешний порт;</span><span class="sxs-lookup"><span data-stu-id="48396-118">External port.</span></span>
- <span data-ttu-id="48396-119">внутренний порт.</span><span class="sxs-lookup"><span data-stu-id="48396-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="48396-120">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="48396-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="48396-121">Если требуется определить имя подсистемы балансировки нагрузки, выполните приведенную команду, чтобы быстро получить список всех подсистем балансировки нагрузки и связанных групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="48396-121">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and the associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="48396-122">Для создания правила подсистемы балансировки нагрузки требуется всего одна команда **Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="48396-122">It only takes a single command to create a load balancer rule with the **Azure CLI**.</span></span> <span data-ttu-id="48396-123">Чтобы создать правило, необходимо знать имя подсистемы балансировки нагрузки и имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="48396-123">You just need to know both the name of the load balancer and resource group to create a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="48396-124">В команде Azure CLI используется несколько параметров, которые описаны в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="48396-124">The Azure CLI command has a few parameters that are described in the following table:</span></span>

| <span data-ttu-id="48396-125">Параметр</span><span class="sxs-lookup"><span data-stu-id="48396-125">Parameter</span></span> | <span data-ttu-id="48396-126">Описание</span><span class="sxs-lookup"><span data-stu-id="48396-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="48396-127">Порт, через который приложение Service Fabric ожидает передачи данных.</span><span class="sxs-lookup"><span data-stu-id="48396-127">The port the service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="48396-128">Порт, который подсистема балансировки нагрузки предоставляет для внешних подключений.</span><span class="sxs-lookup"><span data-stu-id="48396-128">The port the load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="48396-129">Имя изменяемой подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="48396-129">The name of the load balancer to change.</span></span> |
| `-g`       | <span data-ttu-id="48396-130">Группа ресурсов, содержащая подсистему балансировки нагрузки и кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="48396-130">The resource group that has both the load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="48396-131">Выбранное имя правила.</span><span class="sxs-lookup"><span data-stu-id="48396-131">The chosen name of the rule.</span></span> |


>[!NOTE]
><span data-ttu-id="48396-132">Дополнительные сведения о создании подсистемы балансировки нагрузки с помощью Azure CLI см. в разделе [Создание балансировщика нагрузки для Интернета с помощью Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="48396-132">For more information on how to create a load balancer with the Azure CLI, see [Create a load balancer with the Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="48396-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48396-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="48396-134">Если требуется определить имя подсистемы балансировки нагрузки, выполните приведенную команду, чтобы быстро получить список всех подсистем балансировки нагрузки и связанных групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="48396-134">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="48396-135">PowerShell немного сложнее в использовании, чем Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="48396-135">PowerShell is a little more complicated than the Azure CLI.</span></span> <span data-ttu-id="48396-136">По существу, чтобы создать правило, необходимо выполнить приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="48396-136">Conceptually, do the following steps to create a rule.</span></span>

1. <span data-ttu-id="48396-137">Получите подсистему балансировки нагрузки из Azure.</span><span class="sxs-lookup"><span data-stu-id="48396-137">Get the load balancer from Azure.</span></span>
2. <span data-ttu-id="48396-138">Создайте правило.</span><span class="sxs-lookup"><span data-stu-id="48396-138">Create a rule.</span></span>
3. <span data-ttu-id="48396-139">Добавьте в подсистему балансировки нагрузки правило.</span><span class="sxs-lookup"><span data-stu-id="48396-139">Add the rule to the load balancer.</span></span>
4. <span data-ttu-id="48396-140">Обновите подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="48396-140">Update the load balancer.</span></span>

```powershell
# Get the load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create the rule based on information from the load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add the rule to the load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update the load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="48396-141">В команде `New-AzureRmLoadBalancerRuleConfig` `-FrontendPort` представляет порт, который подсистема балансировки нагрузки предоставляет для внешних подключений, а `-BackendPort` представляет порт, через который приложение Service Fabric ожидает передачи данных.</span><span class="sxs-lookup"><span data-stu-id="48396-141">Regarding the `New-AzureRmLoadBalancerRuleConfig` command, the `-FrontendPort` represents the port the load balancer exposes for external connections, and the `-BackendPort` represents the port the service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="48396-142">Дополнительные сведения о создании подсистемы балансировки нагрузки с помощью PowerShell см. в разделе [Создание балансировщика нагрузки для Интернета в Resource Manager с помощью PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="48396-142">For more information on how to create a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

