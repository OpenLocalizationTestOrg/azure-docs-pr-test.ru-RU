---
title: "Топология Наблюдатель сети Azure aaaView - интерфейса API REST | Документы Microsoft"
description: "В этой статье описывается, как toouse REST API tooquery топологии сети."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="3ede7-103">Просмотр топологии Наблюдателя за сетями с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="3ede7-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3ede7-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ede7-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="3ede7-105">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="3ede7-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="3ede7-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3ede7-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="3ede7-107">REST API</span><span class="sxs-lookup"><span data-stu-id="3ede7-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="3ede7-108">компонент топологии Hello Наблюдатель сети предоставляет визуальное представление hello сетевым ресурсам в подписке.</span><span class="sxs-lookup"><span data-stu-id="3ede7-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="3ede7-109">На портале hello этой визуализации представлены tooyou автоматически.</span><span class="sxs-lookup"><span data-stu-id="3ede7-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="3ede7-110">Hello информации за представление топологии hello hello портала можно извлечь с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ede7-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="3ede7-111">Эта возможность обеспечивает сведения о топологии hello более универсально, как hello данных могут использоваться другие средства toobuild out hello визуализации.</span><span class="sxs-lookup"><span data-stu-id="3ede7-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="3ede7-112">взаимодействие Hello моделируется в две связи.</span><span class="sxs-lookup"><span data-stu-id="3ede7-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="3ede7-113">**Вложение.** Например, виртуальная сеть содержит подсеть, которая, в свою очередь, содержит сетевую карту.</span><span class="sxs-lookup"><span data-stu-id="3ede7-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="3ede7-114">**Связь.** Например, сетевая карта связана с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="3ede7-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="3ede7-115">Hello ниже представлена свойства, которые возвращаются при запросе hello топологии REST API.</span><span class="sxs-lookup"><span data-stu-id="3ede7-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="3ede7-116">**имя** - hello имя ресурса hello</span><span class="sxs-lookup"><span data-stu-id="3ede7-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="3ede7-117">**Идентификатор** -hello uri ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="3ede7-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="3ede7-118">**расположение** -hello расположение, где существует ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="3ede7-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="3ede7-119">**ассоциации** -список сопоставлений toohello ссылка на объект.</span><span class="sxs-lookup"><span data-stu-id="3ede7-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="3ede7-120">**имя** -hello объекта hello ссылка на имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="3ede7-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="3ede7-121">**resourceId** -hello resourceId является uri hello hello ресурса, на который ссылается связь hello.</span><span class="sxs-lookup"><span data-stu-id="3ede7-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="3ede7-122">**Тип associationType** -это значение ссылается на связь hello hello объекта дочернего и родительского hello.</span><span class="sxs-lookup"><span data-stu-id="3ede7-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="3ede7-123">Допустимые значения: **Contains** или **Associated**.</span><span class="sxs-lookup"><span data-stu-id="3ede7-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3ede7-124">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="3ede7-124">Before you begin</span></span>

<span data-ttu-id="3ede7-125">В этом случае можно получить сведения о топологии hello.</span><span class="sxs-lookup"><span data-stu-id="3ede7-125">In this scenario, you retrieve hello topology information.</span></span> <span data-ttu-id="3ede7-126">ARMclient — используется toocall hello REST API с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ede7-126">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="3ede7-127">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="3ede7-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="3ede7-128">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="3ede7-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="3ede7-129">Сценарий</span><span class="sxs-lookup"><span data-stu-id="3ede7-129">Scenario</span></span>

<span data-ttu-id="3ede7-130">Hello сценарий, описанный в этой статье получает ответ hello топологии для данной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3ede7-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="3ede7-131">Вход с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="3ede7-131">Log in with ARMClient</span></span>

<span data-ttu-id="3ede7-132">Войдите в tooarmclient с учетными данными Azure.</span><span class="sxs-lookup"><span data-stu-id="3ede7-132">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="3ede7-133">Получение топологии</span><span class="sxs-lookup"><span data-stu-id="3ede7-133">Retrieve topology</span></span>

<span data-ttu-id="3ede7-134">Следующий пример Hello запрашивает топологии hello hello REST API.</span><span class="sxs-lookup"><span data-stu-id="3ede7-134">hello following example requests hello topology from hello REST API.</span></span>  <span data-ttu-id="3ede7-135">пример Hello является параметризованный tooallow для гибкость при создании примера.</span><span class="sxs-lookup"><span data-stu-id="3ede7-135">hello example is parameterized tooallow for flexibility in creating an example.</span></span>  <span data-ttu-id="3ede7-136">Замените значения в угловых скобках (\< \>).</span><span class="sxs-lookup"><span data-stu-id="3ede7-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="3ede7-137">Hello после ответа является примером сокращенный ответ, который возвращается, если получить топологию группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="3ede7-137">hello following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="3ede7-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ede7-138">Next steps</span></span>

<span data-ttu-id="3ede7-139">Узнайте, каким образом toovisualize вашего потока NSG ведет журнал с помощью Power BI, посетив [визуализировать NSG потоки журналов с помощью Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="3ede7-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

