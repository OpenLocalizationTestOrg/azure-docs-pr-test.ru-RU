---
title: "Просмотр топологии Наблюдателя за сетями (PowerShell) | Документация Майкрософт"
description: "В этой статье вы узнаете, как создать запрос к топологии сети с помощью PowerShell."
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
ms.openlocfilehash: 40e01a7a6a2ea6127ab725f04649cec47b9d9422
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="6130e-103">Просмотр топологии Наблюдателя за сетями с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="6130e-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6130e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6130e-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="6130e-105">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="6130e-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="6130e-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6130e-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="6130e-107">REST API</span><span class="sxs-lookup"><span data-stu-id="6130e-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="6130e-108">Возможность просмотра топологии Наблюдателя за сетями позволяет получить визуальное представление сетевых ресурсов в подписке.</span><span class="sxs-lookup"><span data-stu-id="6130e-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="6130e-109">На портале эта визуализация отображается автоматически.</span><span class="sxs-lookup"><span data-stu-id="6130e-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="6130e-110">Сведения в представлении топологии на портале можно получить с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6130e-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="6130e-111">Эта возможность обеспечивает адаптивность данных, так как в таком случае их можно использовать в других средствах для создания визуализации.</span><span class="sxs-lookup"><span data-stu-id="6130e-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="6130e-112">Взаимодействие моделируется по двум связям.</span><span class="sxs-lookup"><span data-stu-id="6130e-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="6130e-113">**Вложение.** Например, виртуальная сеть содержит подсеть, которая, в свою очередь, содержит сетевую карту.</span><span class="sxs-lookup"><span data-stu-id="6130e-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="6130e-114">**Связь.** Например, сетевая карта связана с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="6130e-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="6130e-115">В следующем списке представлены свойства, которые возвращаются при запросе REST API топологии.</span><span class="sxs-lookup"><span data-stu-id="6130e-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="6130e-116">**name** — имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6130e-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="6130e-117">**id** — универсальный код ресурса (URI) группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6130e-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="6130e-118">**location** — расположение ресурса.</span><span class="sxs-lookup"><span data-stu-id="6130e-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="6130e-119">**associations** — список связей объекта, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="6130e-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="6130e-120">**name** — имя ресурса, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="6130e-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="6130e-121">**resourceId** — универсальный код ресурса (URI), на который ссылается связь.</span><span class="sxs-lookup"><span data-stu-id="6130e-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="6130e-122">**associationType** — значение, которое ссылается на связь между дочерним и родительским объектом.</span><span class="sxs-lookup"><span data-stu-id="6130e-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="6130e-123">Допустимые значения: **Contains** или **Associated**.</span><span class="sxs-lookup"><span data-stu-id="6130e-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6130e-124">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="6130e-124">Before you begin</span></span>

<span data-ttu-id="6130e-125">В этом сценарии командлет `Get-AzureRmNetworkWatcherTopology` используется для получения сведений о топологии.</span><span class="sxs-lookup"><span data-stu-id="6130e-125">In this scenario, you use the `Get-AzureRmNetworkWatcherTopology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="6130e-126">Вы также можете просмотреть статью о том, как [получить сведения о топологии сети с помощью REST API](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="6130e-126">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="6130e-127">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create an Azure Network Watcher instance](network-watcher-create.md) (Наблюдатель за сетями: создание экземпляра службы).</span><span class="sxs-lookup"><span data-stu-id="6130e-127">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="6130e-128">Сценарий</span><span class="sxs-lookup"><span data-stu-id="6130e-128">Scenario</span></span>

<span data-ttu-id="6130e-129">В сценарии, описанном в этой статье, вы получаете ответ топологии для указанной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6130e-129">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="6130e-130">Извлечение Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="6130e-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="6130e-131">Сначала необходимо получить экземпляр Наблюдателя за сетями.</span><span class="sxs-lookup"><span data-stu-id="6130e-131">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="6130e-132">Переменная `$networkWatcher` передается в командлет `Get-AzureRmNetworkWatcherTopology`.</span><span class="sxs-lookup"><span data-stu-id="6130e-132">The `$networkWatcher` variable is passed to the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="6130e-133">Получение топологии</span><span class="sxs-lookup"><span data-stu-id="6130e-133">Retrieve topology</span></span>

<span data-ttu-id="6130e-134">Командлет `Get-AzureRmNetworkWatcherTopology` получает сведения о топологии для указанной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6130e-134">The `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves the topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="6130e-135">Результаты</span><span class="sxs-lookup"><span data-stu-id="6130e-135">Results</span></span>

<span data-ttu-id="6130e-136">В возвращенных результатах имеется имя свойства Resources, в котором содержится текст ответа JSON для командлета `Get-AzureRmNetworkWatcherTopology`.</span><span class="sxs-lookup"><span data-stu-id="6130e-136">The results returned have a property name "Resources", which contains the json response body for the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="6130e-137">Ответ содержит ресурсы в группе безопасности сети и их связи (то есть значения Contains, Associated).</span><span class="sxs-lookup"><span data-stu-id="6130e-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6130e-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6130e-138">Next steps</span></span>

<span data-ttu-id="6130e-139">Дополнительные сведения см. в статье [Визуализация журналов потоков для групп безопасности сети с помощью Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="6130e-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


