---
title: "aaaFind следующего прыжка с Azure сети наблюдателя следующего прыжка - REST | Документы Microsoft"
description: "В этой статье описывается, как можно найти какие hello тип следующего прыжка — и IP-адрес, с помощью следующего прыжка hello Azure REST API"
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
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="b5b15-103">Узнать, какой тип следующего прыжка hello является использование возможностей следующего прыжка hello в Aure Наблюдатель сети, с помощью Azure REST API</span><span class="sxs-lookup"><span data-stu-id="b5b15-103">Find out what hello next hop type is using hello Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b5b15-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b5b15-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="b5b15-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5b15-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="b5b15-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="b5b15-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="b5b15-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b5b15-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="b5b15-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="b5b15-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="b5b15-109">Следующий прыжок является компонентом Наблюдатель сети, который предоставляет возможность hello получить тип следующего прыжка hello и IP-адрес, на основе указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b5b15-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="b5b15-110">Эта возможность полезна в определении передачи трафика, оставляя виртуальной машины шлюза, Интернет или назначения tooits tooget виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="b5b15-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b5b15-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="b5b15-111">Before you begin</span></span>

<span data-ttu-id="b5b15-112">ARMclient — используется toocall hello REST API с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5b15-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="b5b15-113">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="b5b15-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="b5b15-114">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="b5b15-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="b5b15-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="b5b15-115">Scenario</span></span>

<span data-ttu-id="b5b15-116">Hello сценарии, описанные в данной статье используется следующего прыжка, функция Наблюдатель сети, извлекают тип следующего прыжка hello и IP-адрес для ресурса.</span><span class="sxs-lookup"><span data-stu-id="b5b15-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="b5b15-117">Посетите toolearn Дополнительные сведения о следующего прыжка [следующего прыжка Обзор](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5b15-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="b5b15-118">Вам предстоит:</span><span class="sxs-lookup"><span data-stu-id="b5b15-118">In this scenario, you will:</span></span>

* <span data-ttu-id="b5b15-119">Получить hello следующего прыжка для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b5b15-119">Retrieve hello next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="b5b15-120">Вход с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="b5b15-120">Log in with ARMClient</span></span>

<span data-ttu-id="b5b15-121">Войдите в tooarmclient с учетными данными Azure.</span><span class="sxs-lookup"><span data-stu-id="b5b15-121">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="b5b15-122">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b5b15-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="b5b15-123">Запустите следующий сценарий tooreturn hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b5b15-123">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="b5b15-124">Эти данные потребуются при выполнении следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="b5b15-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="b5b15-125">После кода Hello необходимые значения для hello следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="b5b15-125">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="b5b15-126">**subscriptionId** -hello toouse идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="b5b15-126">**subscriptionId** - hello subscription Id toouse.</span></span>
- <span data-ttu-id="b5b15-127">**resourceGroupName** — hello имя группы ресурсов, содержащем виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="b5b15-127">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="b5b15-128">Из hello следующие выходные данные, идентификатор hello hello виртуальной машины используется в hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="b5b15-128">From hello following output, hello id of hello virtual machine is used in hello following example:</span></span>

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

## <a name="get-next-hop"></a><span data-ttu-id="b5b15-129">Получение следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="b5b15-129">Get Next Hop</span></span>

<span data-ttu-id="b5b15-130">После создания заголовка авторизации hello hello следующего прыжка из виртуальной машины могут быть получены.</span><span class="sxs-lookup"><span data-stu-id="b5b15-130">Once hello authorization header is created, hello next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="b5b15-131">Hello следующие значения должно быть заменено toowork примере кода hello.</span><span class="sxs-lookup"><span data-stu-id="b5b15-131">hello following values must be replaced for hello code example toowork.</span></span>

> [!Important]
> <span data-ttu-id="b5b15-132">Для API-интерфейса REST Наблюдатель сети вызовы hello имя группы ресурсов в запросе hello, что URI является hello группы ресурсов, содержащий hello Наблюдатель сети не hello ресурсы при выполнении hello диагностических действий на.</span><span class="sxs-lookup"><span data-stu-id="b5b15-132">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

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
> <span data-ttu-id="b5b15-133">Следующий прыжок требуется что toorun распределения ресурсов виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="b5b15-133">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="results"></a><span data-ttu-id="b5b15-134">Результаты</span><span class="sxs-lookup"><span data-stu-id="b5b15-134">Results</span></span>

<span data-ttu-id="b5b15-135">Hello ниже приведен пример выходных данных hello получено.</span><span class="sxs-lookup"><span data-stu-id="b5b15-135">hello following snippet is an example of hello output received.</span></span> <span data-ttu-id="b5b15-136">Hello результаты содержат hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="b5b15-136">hello results contain hello following values:</span></span>

* <span data-ttu-id="b5b15-137">**nextHopType** -это значение является одним из hello следующие значения: Интернет, VirtualAppliance, задана как VirtualNetworkGateway, VnetLocal, HyperNetGateway или нет.</span><span class="sxs-lookup"><span data-stu-id="b5b15-137">**nextHopType** - This value is one of hello following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="b5b15-138">**nextHopIpAddress** -hello IP-адрес следующего прыжка hello.</span><span class="sxs-lookup"><span data-stu-id="b5b15-138">**nextHopIpAddress** - hello IP address of hello next hop.</span></span>
* <span data-ttu-id="b5b15-139">**routeTableId** - hello значение — uri для таблицы маршрутов hello, связанные с маршрутом hello, или если нет пользовательских маршрута определенных hello значение *маршрут системы* возвращается.</span><span class="sxs-lookup"><span data-stu-id="b5b15-139">**routeTableId** - hello value is either a uri for hello route table associated with hello route, or if no user-defined route is defined hello value of *System Route* is returned.</span></span>

<span data-ttu-id="b5b15-140">Здесь представлены Hello hello результаты в формате json.</span><span class="sxs-lookup"><span data-stu-id="b5b15-140">hello following are hello results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="b5b15-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5b15-141">Next steps</span></span>

<span data-ttu-id="b5b15-142">После может toofind out hello следующего прыжка для виртуальной машины, можно просмотреть hello безопасность сетевых ресурсов, посетив [Обзор представления безопасности](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b5b15-142">Once you have been able toofind out hello next hop for a virtual machine, you can view hello security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














