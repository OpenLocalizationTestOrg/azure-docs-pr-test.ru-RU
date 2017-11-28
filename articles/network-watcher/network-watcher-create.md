---
title: "aaaCreate экземпляр Наблюдатель сети Azure | Документы Microsoft"
description: "Эта страница предоставляет toocreate действия hello экземпляр Наблюдатель сети с помощью портала hello и Azure REST API"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="07224-103">Создание экземпляра Наблюдателя за сетями Azure</span><span class="sxs-lookup"><span data-stu-id="07224-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="07224-104">Наблюдатель сети региональные служба, которая позволяет вам toomonitor и диагностики условий уровнем сети сценарий в, чтобы и из Azure.</span><span class="sxs-lookup"><span data-stu-id="07224-104">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="07224-105">Мониторинг на уровне сценария позволяет toodiagnose проблемы tooend конец сетевого уровня представления.</span><span class="sxs-lookup"><span data-stu-id="07224-105">Scenario level monitoring enables you toodiagnose problems at an end tooend network level view.</span></span> <span data-ttu-id="07224-106">Диагностика сети и средств визуализации, доступных в Наблюдатель сети помогают понять, диагностики и получить аналитики tooyour сети в Azure.</span><span class="sxs-lookup"><span data-stu-id="07224-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="07224-107">Наблюдатель сети в настоящее время поддерживает только CLI 1.0, toocreate инструкции hello экземпляра Наблюдатель сети предоставляется CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="07224-107">As Network Watcher currently only supports CLI 1.0, hello instructions toocreate a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-hello-portal"></a><span data-ttu-id="07224-108">Создание Наблюдатель сети на портале hello</span><span class="sxs-lookup"><span data-stu-id="07224-108">Create a Network Watcher in hello portal</span></span>

<span data-ttu-id="07224-109">Перейдите в слишком**более служб** > **сети** > **Наблюдатель сети**.</span><span class="sxs-lookup"><span data-stu-id="07224-109">Navigate too**More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="07224-110">Можно выбрать все подписки hello требуется tooenable Наблюдатель сети для.</span><span class="sxs-lookup"><span data-stu-id="07224-110">You can select all hello subscriptions you want tooenable Network Watcher for.</span></span> <span data-ttu-id="07224-111">Это действие создаст экземпляр Наблюдателя за сетями в каждом регионе, который доступен.</span><span class="sxs-lookup"><span data-stu-id="07224-111">This action creates a Network Watcher in every region that is available.</span></span>

![Создание Наблюдателя за сетями][1]

<span data-ttu-id="07224-113">При включении Наблюдатель сети с помощью портала hello hello имя экземпляра hello Наблюдатель сети будет автоматически задан tooNetworkWatcher_region_name где region_name соответствует toohello регион Azure, где hello экземпляр был включен.</span><span class="sxs-lookup"><span data-stu-id="07224-113">When you enable Network Watcher using hello Portal, hello name of hello Network Watcher instance will automatically be set tooNetworkWatcher_region_name where region_name corresponds toohello Azure Region where hello instance was enabled.</span></span>  <span data-ttu-id="07224-114">Например, наблюдатель за сетями, включенный в западной части центрального региона США, получит имя NetworkWatcher_westcentralus</span><span class="sxs-lookup"><span data-stu-id="07224-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="07224-115">Кроме того экземпляр hello Наблюдатель сети, автоматически добавляется в группу ресурсов под названием NetworkWatcherRG.</span><span class="sxs-lookup"><span data-stu-id="07224-115">Additionally, hello Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="07224-116">Если эта группа ресурсов не существует, она будет создана.</span><span class="sxs-lookup"><span data-stu-id="07224-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="07224-117">При желании toocustomize hello имя экземпляра Наблюдатель сети и hello группы ресурсов, он помещается в, можно использовать Powershell, hello API-интерфейса REST или ARMClient описанных ниже методов.</span><span class="sxs-lookup"><span data-stu-id="07224-117">If you wish toocustomize hello name of a Network Watcher instance and hello Resource Group it's placed into, you can use Powershell, hello REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="07224-118">В каждом случае hello группы ресурсов должна существовать до установки hello Наблюдатель сети в него.</span><span class="sxs-lookup"><span data-stu-id="07224-118">In each option, hello Resource Group must exist before you place hello Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="07224-119">Создание Наблюдателя за сетями с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="07224-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="07224-120">toocreate экземпляр Наблюдатель сети, запустите следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="07224-120">toocreate an instance of Network Watcher, run hello following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a><span data-ttu-id="07224-121">Создайте Наблюдатель сети с hello REST API</span><span class="sxs-lookup"><span data-stu-id="07224-121">Create a Network Watcher with hello REST API</span></span>

<span data-ttu-id="07224-122">ARMclient — используется toocall hello REST API с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="07224-122">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="07224-123">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="07224-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="07224-124">Вход с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="07224-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a><span data-ttu-id="07224-125">Создание hello Наблюдатель сети</span><span class="sxs-lookup"><span data-stu-id="07224-125">Create hello network watcher</span></span>

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a><span data-ttu-id="07224-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07224-126">Next steps</span></span>

<span data-ttu-id="07224-127">Теперь, когда экземпляр Наблюдатель сети, сведения о доступных возможностях hello:</span><span class="sxs-lookup"><span data-stu-id="07224-127">Now that you have an instance of Network Watcher, learn about hello features available:</span></span>

* [<span data-ttu-id="07224-128">Топология</span><span class="sxs-lookup"><span data-stu-id="07224-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="07224-129">Запись пакетов</span><span class="sxs-lookup"><span data-stu-id="07224-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="07224-130">Проверка IP-потока</span><span class="sxs-lookup"><span data-stu-id="07224-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="07224-131">Определение следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="07224-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="07224-132">Представление групп безопасности</span><span class="sxs-lookup"><span data-stu-id="07224-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="07224-133">Ведение журнала потоков NSG</span><span class="sxs-lookup"><span data-stu-id="07224-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="07224-134">Устранение неполадок шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="07224-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="07224-135">После создания экземпляра Наблюдатель сети записи пакета можно задать в следующей статье hello: [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="07224-135">Once a Network Watcher instance has been created, package capture can be configured by following hello article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











