---
title: "Следующий прыжок aaaFind с Azure сети наблюдателя следующего прыжка — Azure CLI 1.0 | Документы Microsoft"
description: "В этой статье описывается, как можно найти какие hello тип следующего прыжка — и адрес ip с помощью следующего прыжка с помощью Azure CLI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="11214-103">Узнать, какой тип следующего прыжка hello является использование возможностей следующего прыжка hello в Наблюдатель сети Azure с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="11214-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="11214-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="11214-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="11214-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="11214-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="11214-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="11214-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="11214-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="11214-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="11214-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="11214-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="11214-109">Следующий прыжок является компонентом Наблюдатель сети, который предоставляет возможность hello получить тип следующего прыжка hello и IP-адрес, на основе указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="11214-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="11214-110">Эта функция полезна при определении Если пакетов, отправляемых виртуальная машина проходит через шлюз, Интернет или назначения tooits tooget виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="11214-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="11214-111">В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="11214-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="11214-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="11214-112">Before you begin</span></span>

<span data-ttu-id="11214-113">В этом сценарии используется hello тип следующего прыжка Azure CLI toofind hello и IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="11214-113">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="11214-114">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="11214-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="11214-115">сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.</span><span class="sxs-lookup"><span data-stu-id="11214-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="11214-116">Сценарий</span><span class="sxs-lookup"><span data-stu-id="11214-116">Scenario</span></span>

<span data-ttu-id="11214-117">Hello сценарии, описанные в данной статье используется следующего прыжка, функция Наблюдатель сети, извлекают тип следующего прыжка hello и IP-адрес для ресурса.</span><span class="sxs-lookup"><span data-stu-id="11214-117">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="11214-118">Посетите toolearn Дополнительные сведения о следующего прыжка [следующего прыжка Обзор](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11214-118">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="11214-119">Получение следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="11214-119">Get Next Hop</span></span>

<span data-ttu-id="11214-120">Следующий прыжок tooget hello мы называем hello `azure netowrk watcher next-hop` командлета.</span><span class="sxs-lookup"><span data-stu-id="11214-120">tooget hello next hop we call hello `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="11214-121">Мы передаем группы ресурсов Наблюдатель сети hello командлет hello, hello NetworkWatcher, виртуальной машины идентификатор, исходный IP-адрес и IP-адрес назначения.</span><span class="sxs-lookup"><span data-stu-id="11214-121">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="11214-122">В этом примере hello конечный IP-адрес — tooa виртуальной Машины в другой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="11214-122">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="11214-123">Нет шлюза виртуальной сети между двумя виртуальными сетями hello.</span><span class="sxs-lookup"><span data-stu-id="11214-123">There is a virtual network gateway between hello two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="11214-124">Если hello виртуальной Машины имеет несколько сетевых адаптеров и IP-пересылки включен на всех сетевых адаптеров hello, hello параметров сетевого Адаптера (-я nic-id) должно быть указано.</span><span class="sxs-lookup"><span data-stu-id="11214-124">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="11214-125">В противном случае этот параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="11214-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="11214-126">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="11214-126">Review results</span></span>

<span data-ttu-id="11214-127">По завершении приведены результаты hello.</span><span class="sxs-lookup"><span data-stu-id="11214-127">When complete, hello results are provided.</span></span> <span data-ttu-id="11214-128">а также hello тип ресурса, который является возвращается IP-адрес следующего прыжка Hello.</span><span class="sxs-lookup"><span data-stu-id="11214-128">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="11214-129">Hello ниже перечислены в настоящее время доступных значений NextHopType hello.</span><span class="sxs-lookup"><span data-stu-id="11214-129">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="11214-130">**Типы следующего прыжка**</span><span class="sxs-lookup"><span data-stu-id="11214-130">**Next Hop Type**</span></span>

* <span data-ttu-id="11214-131">Интернет</span><span class="sxs-lookup"><span data-stu-id="11214-131">Internet</span></span>
* <span data-ttu-id="11214-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="11214-132">VirtualAppliance</span></span>
* <span data-ttu-id="11214-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="11214-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="11214-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="11214-134">VnetLocal</span></span>
* <span data-ttu-id="11214-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="11214-135">HyperNetGateway</span></span>
* <span data-ttu-id="11214-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="11214-136">VnetPeering</span></span>
* <span data-ttu-id="11214-137">None</span><span class="sxs-lookup"><span data-stu-id="11214-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="11214-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="11214-138">Next steps</span></span>

<span data-ttu-id="11214-139">Узнайте, как tooreview параметров группы безопасности сети программным способом, посетив [NSG аудита и Наблюдатель сети](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="11214-139">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
