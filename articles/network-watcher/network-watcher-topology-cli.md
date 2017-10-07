---
title: "Топология Наблюдатель сети Azure aaaView - Azure CLI | Документы Microsoft"
description: "В этой статье описывается как tooquery Azure CLI toouse топологии сети."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a><span data-ttu-id="600be-103">Просмотр топологии Наблюдателя за сетями с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="600be-103">View Network Watcher topology with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="600be-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="600be-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="600be-105">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="600be-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="600be-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="600be-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="600be-107">REST API</span><span class="sxs-lookup"><span data-stu-id="600be-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="600be-108">компонент топологии Hello Наблюдатель сети предоставляет визуальное представление hello сетевым ресурсам в подписке.</span><span class="sxs-lookup"><span data-stu-id="600be-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="600be-109">На портале hello этой визуализации представлены tooyou автоматически.</span><span class="sxs-lookup"><span data-stu-id="600be-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="600be-110">Hello информации за представление топологии hello hello портала можно извлечь с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="600be-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="600be-111">Эта возможность обеспечивает сведения о топологии hello более универсально, как hello данных могут использоваться другие средства toobuild out hello визуализации.</span><span class="sxs-lookup"><span data-stu-id="600be-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="600be-112">В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="600be-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="600be-113">Наблюдатель за сетями в настоящее время использует Azure CLI 1.0 в качестве интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="600be-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="600be-114">взаимодействие Hello моделируется в две связи.</span><span class="sxs-lookup"><span data-stu-id="600be-114">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="600be-115">**Вложение.** Например, виртуальная сеть содержит подсеть, которая, в свою очередь, содержит сетевую карту.</span><span class="sxs-lookup"><span data-stu-id="600be-115">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="600be-116">**Связь.** Например, сетевая карта связана с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="600be-116">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="600be-117">Hello ниже представлена свойства, которые возвращаются при запросе hello топологии REST API.</span><span class="sxs-lookup"><span data-stu-id="600be-117">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="600be-118">**имя** - hello имя ресурса hello</span><span class="sxs-lookup"><span data-stu-id="600be-118">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="600be-119">**Идентификатор** -hello uri ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="600be-119">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="600be-120">**расположение** -hello расположение, где существует ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="600be-120">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="600be-121">**ассоциации** -список сопоставлений toohello ссылка на объект.</span><span class="sxs-lookup"><span data-stu-id="600be-121">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="600be-122">**имя** -hello объекта hello ссылка на имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="600be-122">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="600be-123">**resourceId** -hello resourceId является uri hello hello ресурса, на который ссылается связь hello.</span><span class="sxs-lookup"><span data-stu-id="600be-123">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="600be-124">**Тип associationType** -это значение ссылается на связь hello hello объекта дочернего и родительского hello.</span><span class="sxs-lookup"><span data-stu-id="600be-124">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="600be-125">Допустимые значения: **Contains** или **Associated**.</span><span class="sxs-lookup"><span data-stu-id="600be-125">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="600be-126">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="600be-126">Before you begin</span></span>

<span data-ttu-id="600be-127">В этом сценарии используется hello `network watcher topology` сведения о топологии hello tooretrieve командлета.</span><span class="sxs-lookup"><span data-stu-id="600be-127">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="600be-128">Имеется также статью о том, как слишком[получить топология сети с помощью REST API](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="600be-128">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="600be-129">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="600be-129">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="600be-130">Сценарий</span><span class="sxs-lookup"><span data-stu-id="600be-130">Scenario</span></span>

<span data-ttu-id="600be-131">Hello сценарий, описанный в этой статье получает ответ hello топологии для данной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="600be-131">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="600be-132">Получение топологии</span><span class="sxs-lookup"><span data-stu-id="600be-132">Retrieve topology</span></span>

<span data-ttu-id="600be-133">Hello `network watcher topology` командлет извлекает hello топологии для данной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="600be-133">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="600be-134">Добавьте аргумент hello «--json» tooview oput hello в формате json</span><span class="sxs-lookup"><span data-stu-id="600be-134">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="600be-135">Результаты</span><span class="sxs-lookup"><span data-stu-id="600be-135">Results</span></span>

<span data-ttu-id="600be-136">Hello возвращаемые результаты имеют свойство имени «ресурсы», содержащих hello текста ответа json для hello `network watcher topology` командлета.</span><span class="sxs-lookup"><span data-stu-id="600be-136">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="600be-137">Hello ответ содержит ресурсы hello hello сетевой группы безопасности и их связи (то есть Contains, связано).</span><span class="sxs-lookup"><span data-stu-id="600be-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="600be-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="600be-138">Next steps</span></span>

<span data-ttu-id="600be-139">Дополнительные сведения о правилах безопасности hello, которые будут применяться tooyour сетевым ресурсам, посетив [Общие сведения о представлении группы безопасности](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="600be-139">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
