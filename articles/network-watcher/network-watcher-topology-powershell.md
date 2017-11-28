---
title: "Топология Наблюдатель сети Azure aaaView - PowerShell | Документы Microsoft"
description: "В этой статье описывается как toouse PowerShell tooquery топологии сети."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="f7d5f-103">Просмотр топологии Наблюдателя за сетями с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7d5f-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f7d5f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7d5f-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="f7d5f-105">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="f7d5f-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="f7d5f-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f7d5f-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="f7d5f-107">REST API</span><span class="sxs-lookup"><span data-stu-id="f7d5f-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="f7d5f-108">компонент топологии Hello Наблюдатель сети предоставляет визуальное представление hello сетевым ресурсам в подписке.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="f7d5f-109">На портале hello этой визуализации представлены tooyou автоматически.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="f7d5f-110">Hello информации за представление топологии hello hello портала можно извлечь с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="f7d5f-111">Эта возможность обеспечивает сведения о топологии hello более универсально, как hello данных могут использоваться другие средства toobuild out hello визуализации.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="f7d5f-112">взаимодействие Hello моделируется в две связи.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="f7d5f-113">**Вложение.** Например, виртуальная сеть содержит подсеть, которая, в свою очередь, содержит сетевую карту.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="f7d5f-114">**Связь.** Например, сетевая карта связана с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="f7d5f-115">Hello ниже представлена свойства, которые возвращаются при запросе hello топологии REST API.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="f7d5f-116">**имя** - hello имя ресурса hello</span><span class="sxs-lookup"><span data-stu-id="f7d5f-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="f7d5f-117">**Идентификатор** -hello uri ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="f7d5f-118">**расположение** -hello расположение, где существует ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="f7d5f-119">**ассоциации** -список сопоставлений toohello ссылка на объект.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="f7d5f-120">**имя** -hello объекта hello ссылка на имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="f7d5f-121">**resourceId** -hello resourceId является uri hello hello ресурса, на который ссылается связь hello.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="f7d5f-122">**Тип associationType** -это значение ссылается на связь hello hello объекта дочернего и родительского hello.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="f7d5f-123">Допустимые значения: **Contains** или **Associated**.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f7d5f-124">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="f7d5f-124">Before you begin</span></span>

<span data-ttu-id="f7d5f-125">В этом сценарии используется hello `Get-AzureRmNetworkWatcherTopology` сведения о топологии hello tooretrieve командлета.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-125">In this scenario, you use hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="f7d5f-126">Имеется также статью о том, как слишком[получить топология сети с помощью REST API](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="f7d5f-126">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="f7d5f-127">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-127">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="f7d5f-128">Сценарий</span><span class="sxs-lookup"><span data-stu-id="f7d5f-128">Scenario</span></span>

<span data-ttu-id="f7d5f-129">Hello сценарий, описанный в этой статье получает ответ hello топологии для данной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-129">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="f7d5f-130">Извлечение Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="f7d5f-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="f7d5f-131">Первым шагом Hello — экземпляр Наблюдатель сети tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-131">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="f7d5f-132">Hello `$networkWatcher` переменной передается toohello `Get-AzureRmNetworkWatcherTopology` командлета.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-132">hello `$networkWatcher` variable is passed toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="f7d5f-133">Получение топологии</span><span class="sxs-lookup"><span data-stu-id="f7d5f-133">Retrieve topology</span></span>

<span data-ttu-id="f7d5f-134">Hello `Get-AzureRmNetworkWatcherTopology` командлет извлекает hello топологии для данной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-134">hello `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves hello topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="f7d5f-135">Результаты</span><span class="sxs-lookup"><span data-stu-id="f7d5f-135">Results</span></span>

<span data-ttu-id="f7d5f-136">Hello возвращаемые результаты имеют свойство имени «ресурсы», содержащих hello текста ответа json для hello `Get-AzureRmNetworkWatcherTopology` командлета.</span><span class="sxs-lookup"><span data-stu-id="f7d5f-136">hello results returned have a property name "Resources", which contains hello json response body for hello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="f7d5f-137">Hello ответ содержит ресурсы hello hello сетевой группы безопасности и их связи (то есть Contains, связано).</span><span class="sxs-lookup"><span data-stu-id="f7d5f-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a><span data-ttu-id="f7d5f-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7d5f-138">Next steps</span></span>

<span data-ttu-id="f7d5f-139">Узнайте, каким образом toovisualize вашего потока NSG ведет журнал с помощью Power BI, посетив [визуализировать NSG потоки журналов с помощью Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="f7d5f-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


