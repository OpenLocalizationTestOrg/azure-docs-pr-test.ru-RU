---
title: "aaaCreate правило балансировки нагрузки Azure для кластера"
description: "Настройте порты tooopen подсистемы балансировки нагрузки Azure для кластера Azure Service Fabric."
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
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="fbd0f-103">Открытие портов для кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fbd0f-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="fbd0f-104">Hello подсистемы балансировки нагрузки развернуты вместе с Azure Service Fabric кластера направляет трафик tooyour приложение, работающее на узле.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-104">hello load balancer deployed with your Azure Service Fabric cluster directs traffic tooyour app running on a node.</span></span> <span data-ttu-id="fbd0f-105">При изменении вашего приложения toouse другой порт, предоставлять этот порт (или маршрутизации другой порт) в hello подсистемы балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-105">If you change your app toouse a different port, you must expose that port (or route a different port) in hello Azure Load Balancer.</span></span>

<span data-ttu-id="fbd0f-106">При развертывании вашей tooAzure кластера service fabric подсистемы балансировки нагрузки была автоматически создана для вас.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-106">When you deployed your service fabric cluster tooAzure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="fbd0f-107">Если у вас нет подсистемы балансировки нагрузки, ознакомьтесь с разделом [Создание балансировщика нагрузки для Интернета на портале Azure](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fbd0f-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="fbd0f-108">Настройка Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fbd0f-108">Configure service fabric</span></span>

<span data-ttu-id="fbd0f-109">Приложение Service Fabric **ServiceManifest.xml** файл конфигурации определяет конечные точки hello toouse ожидает приложение.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-109">Your Service Fabric application **ServiceManifest.xml** config file defines hello endpoints your application expects toouse.</span></span> <span data-ttu-id="fbd0f-110">После того, файл конфигурации hello была обновленные toodefine конечной точки, балансировки нагрузки hello должно быть обновленные tooexpose, (или другой) порт.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-110">After hello config file has been updated toodefine an endpoint, hello load balancer must be updated tooexpose that (or a different) port.</span></span> <span data-ttu-id="fbd0f-111">Дополнительные сведения о как toocreate hello конечной точки службы fabric. в разделе [установки конечной точки](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="fbd0f-111">For more information on how toocreate hello service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="fbd0f-112">Создание правила балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="fbd0f-112">Create a load balancer rule</span></span>

<span data-ttu-id="fbd0f-113">Правило подсистемы балансировки нагрузки открывает порт с выходом в Интернет и перенаправляет трафик toohello внутреннего узла порт, используемый вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-113">A load balancer rule opens up an internet-facing port and forwards traffic toohello internal node's port used by your application.</span></span> <span data-ttu-id="fbd0f-114">Если у вас нет подсистемы балансировки нагрузки, ознакомьтесь с разделом [Создание балансировщика нагрузки для Интернета на портале Azure](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fbd0f-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="fbd0f-115">toocreate правило балансировки нагрузки, требуется hello toocollect следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="fbd0f-115">toocreate a load balancer rule, you need toocollect hello following information:</span></span>

- <span data-ttu-id="fbd0f-116">имя подсистемы балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="fbd0f-116">Load balancer name.</span></span>
- <span data-ttu-id="fbd0f-117">Группа ресурсов для hello Подсистема балансировки нагрузки и кластера service fabric.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-117">Resource group of hello load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="fbd0f-118">внешний порт;</span><span class="sxs-lookup"><span data-stu-id="fbd0f-118">External port.</span></span>
- <span data-ttu-id="fbd0f-119">внутренний порт.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="fbd0f-120">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="fbd0f-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="fbd0f-121">Если требуется имя hello toodetermine подсистемы балансировки нагрузки hello используйте tooquickly этой команды get список всех подсистем балансировки нагрузки и hello связанных групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-121">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and hello associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="fbd0f-122">Он принимает только toocreate отдельную команду правило подсистемы балансировки нагрузки с hello **Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-122">It only takes a single command toocreate a load balancer rule with hello **Azure CLI**.</span></span> <span data-ttu-id="fbd0f-123">Необходимо просто tooknow hello, вызывающую нагрузки hello балансировки и ресурсов toocreate группы новое правило.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-123">You just need tooknow both hello name of hello load balancer and resource group toocreate a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="fbd0f-124">Hello Azure CLI команда имеет несколько параметров, описанных в следующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-124">hello Azure CLI command has a few parameters that are described in hello following table:</span></span>

| <span data-ttu-id="fbd0f-125">Параметр</span><span class="sxs-lookup"><span data-stu-id="fbd0f-125">Parameter</span></span> | <span data-ttu-id="fbd0f-126">Описание</span><span class="sxs-lookup"><span data-stu-id="fbd0f-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="fbd0f-127">приложение hello service fabric для Hello порт прослушивания.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-127">hello port hello service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="fbd0f-128">порт hello Hello загрузить предоставляет балансировки для внешних соединений.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-128">hello port hello load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="fbd0f-129">Имя Hello hello загрузить toochange балансировки.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-129">hello name of hello load balancer toochange.</span></span> |
| `-g`       | <span data-ttu-id="fbd0f-130">Группа ресурсов Hello hello балансировки нагрузки и кластера service fabric.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-130">hello resource group that has both hello load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="fbd0f-131">Здравствуйте, выбрать имя правила hello.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-131">hello chosen name of hello rule.</span></span> |


>[!NOTE]
><span data-ttu-id="fbd0f-132">Дополнительные сведения о toocreate балансировки нагрузки с hello Azure CLI. в статье [создать подсистемы балансировки нагрузки с hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fbd0f-132">For more information on how toocreate a load balancer with hello Azure CLI, see [Create a load balancer with hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="fbd0f-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbd0f-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="fbd0f-134">Если вам требуется toodetermine hello имя подсистемы балансировки нагрузки hello, используйте tooquickly этой команды get список всех подсистем балансировки нагрузки и группы связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-134">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="fbd0f-135">PowerShell немного сложнее, чем hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-135">PowerShell is a little more complicated than hello Azure CLI.</span></span> <span data-ttu-id="fbd0f-136">По существу выполните следующие шаги toocreate hello правило.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-136">Conceptually, do hello following steps toocreate a rule.</span></span>

1. <span data-ttu-id="fbd0f-137">Получите hello балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-137">Get hello load balancer from Azure.</span></span>
2. <span data-ttu-id="fbd0f-138">Создайте правило.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-138">Create a rule.</span></span>
3. <span data-ttu-id="fbd0f-139">Добавьте правило для hello toohello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-139">Add hello rule toohello load balancer.</span></span>
4. <span data-ttu-id="fbd0f-140">Обновление подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-140">Update hello load balancer.</span></span>

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="fbd0f-141">О hello `New-AzureRmLoadBalancerRuleConfig` команды hello `-FrontendPort` подсистемы балансировки нагрузки представляет hello порт hello предоставляет внешние подключения и hello `-BackendPort` прослушивают структуры представляет hello порт hello службы приложений.</span><span class="sxs-lookup"><span data-stu-id="fbd0f-141">Regarding hello `New-AzureRmLoadBalancerRuleConfig` command, hello `-FrontendPort` represents hello port hello load balancer exposes for external connections, and hello `-BackendPort` represents hello port hello service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="fbd0f-142">Дополнительные сведения о toocreate балансировки нагрузки с помощью PowerShell, в статье [создание подсистемы балансировки нагрузки с помощью PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fbd0f-142">For more information on how toocreate a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

