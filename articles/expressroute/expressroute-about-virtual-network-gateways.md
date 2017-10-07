---
title: "шлюзы виртуальной сети ExpressRoute aaaAbout | Документы Microsoft"
description: "Сведения о шлюзах виртуальных сетей ExpressRoute."
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="5ba7f-103">Сведения о шлюзах виртуальных сетей ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5ba7f-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="5ba7f-104">Шлюз виртуальной сети используется toosend сетевого трафика между виртуальными сетями Azure и расположения в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-104">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="5ba7f-105">В процессе настройки подключения ExpressRoute необходимо создать и настроить шлюз виртуальной сети и подключение для него.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="5ba7f-106">При создании шлюза виртуальной сети нужно указать несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="5ba7f-107">Один из параметров, необходимых hello указывает, будет ли использоваться hello шлюза для ExpressRoute или через виртуальную Частную сеть для трафика.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-107">One of hello required settings specifies whether hello gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="5ba7f-108">В модели развертывания диспетчера ресурсов hello приветствия равен "-тип шлюза".</span><span class="sxs-lookup"><span data-stu-id="5ba7f-108">In hello Resource Manager deployment model, hello setting is '-GatewayType'.</span></span>

<span data-ttu-id="5ba7f-109">При сетевой трафик отправляется на подключение к частной, используется тип шлюза hello «ExpressRoute».</span><span class="sxs-lookup"><span data-stu-id="5ba7f-109">When network traffic is sent on a private connection, you use hello gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="5ba7f-110">Это ссылка tooas шлюз ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-110">This is also referred tooas an ExpressRoute gateway.</span></span> <span data-ttu-id="5ba7f-111">Если сетевой трафик отправляется через зашифрованный Здравствуйте общедоступный Интернет, использовать тип шлюза hello «Vpn».</span><span class="sxs-lookup"><span data-stu-id="5ba7f-111">When network traffic is sent encrypted across hello public Internet, you use hello gateway type 'Vpn'.</span></span> <span data-ttu-id="5ba7f-112">Это ссылка tooas VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-112">This is referred tooas a VPN gateway.</span></span> <span data-ttu-id="5ba7f-113">При подключениях типа "сеть — сеть", "точка — сеть" и "виртуальная сеть — виртуальная сеть" используется VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="5ba7f-114">В виртуальной сети каждому типу шлюза может соответствовать только один шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="5ba7f-115">Например, у вас может быть только один шлюз виртуальной сети типа VPN и только один типа ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="5ba7f-116">Эта статья посвящена шлюз виртуальной сети hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-116">This article focuses on hello ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="5ba7f-117"><a name="gwsku"></a>SKU шлюзов</span><span class="sxs-lookup"><span data-stu-id="5ba7f-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="5ba7f-118">Если требуется tooupgrade tooa ваш шлюз более мощных шлюза SKU, в большинстве случаев, которые можно использовать hello командлета PowerShell «Изменение размера AzureRmVirtualNetworkGateway».</span><span class="sxs-lookup"><span data-stu-id="5ba7f-118">If you want tooupgrade your gateway tooa more powerful gateway SKU, in most cases you can use hello 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="5ba7f-119">Это будет работать для обновления tooStandard и высокопроизводительные SKU.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-119">This will work for upgrades tooStandard and HighPerformance SKUs.</span></span> <span data-ttu-id="5ba7f-120">Тем не менее, toohello tooupgrade UltraPerformance SKU, потребуется шлюз toorecreate hello.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-120">However, tooupgrade toohello UltraPerformance SKU, you will need toorecreate hello gateway.</span></span>

### <span data-ttu-id="5ba7f-121"><a name="aggthroughput"></a>Расчетная суммарная пропускная способность в зависимости от SKU шлюза</span><span class="sxs-lookup"><span data-stu-id="5ba7f-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="5ba7f-122">Hello следующей таблице показаны типы шлюзов hello и hello предполагаемое суммарную пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-122">hello following table shows hello gateway types and hello estimated aggregate throughput.</span></span> <span data-ttu-id="5ba7f-123">Эта таблица применяется tooboth hello диспетчера ресурсов и классическое развертывание модели.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-123">This table applies tooboth hello Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="5ba7f-124">Пропускная способность приложения зависит от нескольких факторов, таких как задержка начала до конца hello, а номер hello трафика перемещается откроется приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-124">Application throughput depends on multiple factors, such as hello end-to-end latency, and hello number of traffic flows hello application opens.</span></span> <span data-ttu-id="5ba7f-125">числа Hello в hello таблицы представляют Привет верхний предел, приложение hello может theorectically достичь в идеальную среду.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-125">hello numbers in hello table represent hello upper limit that hello application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="5ba7f-126"><a name="resources"></a>Интерфейсы REST API и командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ba7f-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="5ba7f-127">Дополнительные технические ресурсы и синтаксисе требования при использовании API-интерфейс REST и командлеты PowerShell для настройки шлюза виртуальной сети см. следующие страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="5ba7f-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="5ba7f-128">**Классический**</span><span class="sxs-lookup"><span data-stu-id="5ba7f-128">**Classic**</span></span> | <span data-ttu-id="5ba7f-129">**Диспетчер ресурсов**</span><span class="sxs-lookup"><span data-stu-id="5ba7f-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="5ba7f-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ba7f-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="5ba7f-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ba7f-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="5ba7f-132">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="5ba7f-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="5ba7f-133">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="5ba7f-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="5ba7f-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ba7f-134">Next steps</span></span>
<span data-ttu-id="5ba7f-135">Дополнительные сведения о доступных конфигурациях подключений см. в статье [Технический обзор ExpressRoute](expressroute-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5ba7f-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

