---
title: "Поиск следующего прыжка с помощью возможности определения следующего прыжка Наблюдателя за сетями Azure (REST) | Документация Майкрософт"
description: "В этой статье описано, как определить тип следующего прыжка и IP-адрес, используя возможность определения следующего прыжка с помощью Azure REST API."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 644713d365191bf5e51517d0cc565efbc2abc144
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="164ee-103">Определите тип следующего прыжка, используя возможность определения следующего прыжка Наблюдателя за сетями с помощью Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="164ee-103">Find out what the next hop type is using the Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="164ee-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="164ee-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="164ee-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="164ee-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="164ee-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="164ee-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="164ee-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="164ee-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="164ee-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="164ee-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="164ee-109">Определение следующего прыжка — это возможность Наблюдателя за сетями, позволяющая определить тип следующего прыжка и IP-адрес на основе указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="164ee-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="164ee-110">Эта возможность используется, чтобы определить путь передачи исходящего трафика виртуальной машины (шлюз, Интернет или виртуальные сети) к месту назначения.</span><span class="sxs-lookup"><span data-stu-id="164ee-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="164ee-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="164ee-111">Before you begin</span></span>

<span data-ttu-id="164ee-112">Чтобы вызвать REST API при помощи PowerShell, потребуется ARMClient.</span><span class="sxs-lookup"><span data-stu-id="164ee-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="164ee-113">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="164ee-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="164ee-114">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create a Network Watcher](network-watcher-create.md) (Создание Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="164ee-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="164ee-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="164ee-115">Scenario</span></span>

<span data-ttu-id="164ee-116">В сценарии, описанном в этой статье, используется определение следующего прыжка — возможность Наблюдателя за сетями, которая позволяет определить тип следующего перехода и IP-адрес для ресурса.</span><span class="sxs-lookup"><span data-stu-id="164ee-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="164ee-117">Дополнительные сведения об определении следующего прыжка см. в [этой статье](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="164ee-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="164ee-118">Вам предстоит:</span><span class="sxs-lookup"><span data-stu-id="164ee-118">In this scenario, you will:</span></span>

* <span data-ttu-id="164ee-119">получить следующий прыжок для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="164ee-119">Retrieve the next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="164ee-120">Вход с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="164ee-120">Log in with ARMClient</span></span>

<span data-ttu-id="164ee-121">Войдите в ARMClient, используя учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="164ee-121">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="164ee-122">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="164ee-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="164ee-123">Выполните следующий скрипт, чтобы получить сведения о виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="164ee-123">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="164ee-124">Эти данные потребуются при выполнении следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="164ee-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="164ee-125">Выполните приведенный ниже код, указав в нем значения следующих переменных:</span><span class="sxs-lookup"><span data-stu-id="164ee-125">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="164ee-126">**subscriptionId** — идентификатор используемой подписки.</span><span class="sxs-lookup"><span data-stu-id="164ee-126">**subscriptionId** - The subscription Id to use.</span></span>
- <span data-ttu-id="164ee-127">**resourceGroupName** — имя группы ресурсов, в которой содержатся виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="164ee-127">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="164ee-128">Идентификатор виртуальной машины используется в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="164ee-128">From the following output, the id of the virtual machine is used in the following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a><span data-ttu-id="164ee-129">Получение следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="164ee-129">Get Next Hop</span></span>

<span data-ttu-id="164ee-130">После создания заголовка авторизации вы можете получить следующий прыжок для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="164ee-130">Once the authorization header is created, the next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="164ee-131">Чтобы выполнить пример кода, необходимо заменить приведенные ниже значения.</span><span class="sxs-lookup"><span data-stu-id="164ee-131">The following values must be replaced for the code example to work.</span></span>

> [!Important]
> <span data-ttu-id="164ee-132">При вызовах REST API в URI запроса следует указать имя группы ресурсов, в которой содержится Наблюдатель за сетями, а не диагностируемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="164ee-132">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> <span data-ttu-id="164ee-133">Для получения следующего прыжка необходимо, чтобы ресурс виртуальной машины был выделен.</span><span class="sxs-lookup"><span data-stu-id="164ee-133">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="results"></a><span data-ttu-id="164ee-134">Результаты</span><span class="sxs-lookup"><span data-stu-id="164ee-134">Results</span></span>

<span data-ttu-id="164ee-135">Ниже приведен пример выходных данных.</span><span class="sxs-lookup"><span data-stu-id="164ee-135">The following snippet is an example of the output received.</span></span> <span data-ttu-id="164ee-136">Результаты содержат следующие значения:</span><span class="sxs-lookup"><span data-stu-id="164ee-136">The results contain the following values:</span></span>

* <span data-ttu-id="164ee-137">**nextHopType.** Этот параметр может иметь следующие значения: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway или None.</span><span class="sxs-lookup"><span data-stu-id="164ee-137">**nextHopType** - This value is one of the following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="164ee-138">**nextHopIpAddress.** IP-адрес следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="164ee-138">**nextHopIpAddress** - The IP address of the next hop.</span></span>
* <span data-ttu-id="164ee-139">**routeTableId.** Возможные значения: универсальный код ресурса (URI) таблицы маршрутизации, связанной с маршрутом, или *системный маршрут*, если не задан определяемый пользователем маршрут.</span><span class="sxs-lookup"><span data-stu-id="164ee-139">**routeTableId** - The value is either a uri for the route table associated with the route, or if no user-defined route is defined the value of *System Route* is returned.</span></span>

<span data-ttu-id="164ee-140">Результаты возвращаются в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="164ee-140">The following are the results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="164ee-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="164ee-141">Next steps</span></span>

<span data-ttu-id="164ee-142">Определив следующий прыжок для виртуальной машины, вы можете просмотреть параметры безопасности сетевых ресурсов. Дополнительные сведения см. в [этой статье](network-watcher-security-group-view-overview.md).</span><span class="sxs-lookup"><span data-stu-id="164ee-142">Once you have been able to find out the next hop for a virtual machine, you can view the security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














