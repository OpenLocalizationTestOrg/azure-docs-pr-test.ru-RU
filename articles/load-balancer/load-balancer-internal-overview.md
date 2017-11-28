---
title: "Подсистема балансировки нагрузки aaaInternal Обзор | Документы Microsoft"
description: "Общие сведения о внутренней подсистемы балансировки нагрузки и ее компоненты. Как работает подсистемы балансировки нагрузки для внутренних конечных точек tooconfigure Azure и возможных сценариев"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="b4cad-103">Обзор внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="b4cad-103">Internal load balancer overview</span></span>

<span data-ttu-id="b4cad-104">В отличие от hello Интернета с выходом балансировки нагрузки hello внутренней подсистемы балансировки нагрузки (ILB) направляет трафик только tooresources внутри hello облачной службы или с помощью VPN tooaccess hello инфраструктуры Azure.</span><span class="sxs-lookup"><span data-stu-id="b4cad-104">Unlike hello Internet facing load balancer, hello internal load balancer (ILB) directs traffic only tooresources inside hello cloud service or using VPN tooaccess hello Azure infrastructure.</span></span> <span data-ttu-id="b4cad-105">Инфраструктура Hello ограничивает доступ toohello балансировки нагрузки виртуального IP-адреса (VIP) облачной службы или виртуальной сети таким образом, чтобы они никогда не будет конечной точкой непосредственно предоставляется tooan Интернета.</span><span class="sxs-lookup"><span data-stu-id="b4cad-105">hello infrastructure restricts access toohello load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed tooan Internet endpoint.</span></span> <span data-ttu-id="b4cad-106">Это позволяет внутренней строки toorun бизнес-приложений в Azure и для доступа к из облака hello или локальные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b4cad-106">This enables internal line of business (LOB) applications toorun in Azure and be accessed from within hello cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="b4cad-107">Чем полезна внутренняя подсистема балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="b4cad-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="b4cad-108">Внутренняя балансировка нагрузки Azure обеспечивает балансировку нагрузки между виртуальными машинами, которые размещены в облачной службе или региональной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b4cad-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="b4cad-109">Сведения о hello использование и настройка виртуальных сетей с региональной областью см. в разделе [региональные виртуальные сети](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) в блоге Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b4cad-109">For information about hello use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure blog.</span></span> <span data-ttu-id="b4cad-110">В имеющихся виртуальных сетях, настроенных для территориальной группы, невозможно использовать внутреннюю балансировку нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b4cad-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="b4cad-111">ILB включает следующие типы балансировки нагрузки hello:</span><span class="sxs-lookup"><span data-stu-id="b4cad-111">ILB enables hello following types of load balancing:</span></span>

* <span data-ttu-id="b4cad-112">В облачной службе из набора tooa виртуальных машин, виртуальных машин, которые находятся в пределах hello же облачную службу (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="b4cad-112">Within a cloud service, from virtual machines tooa set of virtual machines that reside within hello same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="b4cad-113">В виртуальной сети из виртуальных машин в набор tooa hello виртуальной сети виртуальных машин, которые находятся в пределах hello же облачной службе из hello виртуальной сети (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="b4cad-113">Within a virtual network, from virtual machines in hello virtual network tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 2).</span></span>
* <span data-ttu-id="b4cad-114">Для виртуальной сети между организациями, из набора tooa локальных компьютеров виртуальных машин, которые находятся в пределах hello же облачную службу из hello виртуальной сети (см. рис. 3).</span><span class="sxs-lookup"><span data-stu-id="b4cad-114">For a cross-premises virtual network, from on-premises computers tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 3).</span></span>
* <span data-ttu-id="b4cad-115">С выходом в Интернет, многоуровневые приложения, в которых hello внутренней уровней не являются с выходом в Интернет, но требуют балансировки нагрузки для трафика с уровня hello с выходом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="b4cad-115">Internet-facing, multi-tier applications in which hello back-end tiers are not Internet-facing but require load balancing for traffic from hello Internet-facing tier.</span></span>
* <span data-ttu-id="b4cad-116">Для балансировки нагрузки в бизнес-приложениях, размещенных в Azure. При этом не требуется дополнительное оборудование или программное обеспечение для распределения нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b4cad-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="b4cad-117">Включая локальных серверов в hello набор компьютеров, трафик которого нагрузки равномерно.</span><span class="sxs-lookup"><span data-stu-id="b4cad-117">Including on-premises servers in hello set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="b4cad-118">Многоуровневые приложения, доступные в Интернете</span><span class="sxs-lookup"><span data-stu-id="b4cad-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="b4cad-119">Hello веб-уровень имеет конечных точек с выходом в Интернете для Интернет-клиентов и входит в набор с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b4cad-119">hello web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="b4cad-120">Подсистема балансировки нагрузки Hello распределяет входящий трафик от веб-клиентов для веб-серверов TCP порт 443 (HTTPS) toohello.</span><span class="sxs-lookup"><span data-stu-id="b4cad-120">hello load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) toohello web servers.</span></span>

<span data-ttu-id="b4cad-121">серверы баз данных Hello находящимися за ILB конечную точку, которая hello веб-серверы используют для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="b4cad-121">hello database servers are behind an ILB endpoint which hello web servers use for storage.</span></span> <span data-ttu-id="b4cad-122">Этой базы данных службы балансировки нагрузки конечной точки, какой трафик является Балансировка нагрузки для серверов баз данных hello в наборе ILB hello.</span><span class="sxs-lookup"><span data-stu-id="b4cad-122">This database service load balanced endpoint, which traffic is load balanced across hello database servers in hello ILB set.</span></span>

<span data-ttu-id="b4cad-123">следующие показано изображение Hello hello многоуровневого приложения в Интернете в hello же облачной службе.</span><span class="sxs-lookup"><span data-stu-id="b4cad-123">hello following image shows hello Internet facing multi-tier application within hello same cloud service.</span></span>

![Внутренняя балансировка нагрузки для одной облачной службы](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="b4cad-125">Рис. 1. Многоуровневое приложение для Интернета</span><span class="sxs-lookup"><span data-stu-id="b4cad-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="b4cad-126">Другим возможным вариантом использования многоуровневого приложения — при развертывании hello ILB tooa другой облачной службе, чем hello один hello служба-клиент для hello ILB.</span><span class="sxs-lookup"><span data-stu-id="b4cad-126">Another possible use for a multi-tier application is when hello ILB deployed tooa different cloud service than hello one consuming hello service for hello ILB.</span></span>

<span data-ttu-id="b4cad-127">Облачные службы, использующие hello одной виртуальной сети будут иметь доступа к конечной точке ILB toohello.</span><span class="sxs-lookup"><span data-stu-id="b4cad-127">Cloud services using hello same virtual network will have access toohello ILB endpoint.</span></span> <span data-ttu-id="b4cad-128">ILB конечной точки в hello hello Hello, следуя показаны изображения, интерфейсных веб-серверов, в другой облачной службе из внутренней базы данных hello и с помощью одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b4cad-128">hello following image shows front-end web servers are in a different cloud service from hello database back-end and using hello ILB endpoint within hello same virtual network.</span></span>

![Внутренняя балансировка нагрузки между облачными службами](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="b4cad-130">Рис. 2. Серверы переднего плана в другой облачной службе</span><span class="sxs-lookup"><span data-stu-id="b4cad-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="b4cad-131">Бизнес-приложения в интрасети</span><span class="sxs-lookup"><span data-stu-id="b4cad-131">Intranet line of business applications</span></span>

<span data-ttu-id="b4cad-132">Трафик от клиентов в локальной сети hello получить балансировки нагрузки во множестве hello серверов бизнес-ПРИЛОЖЕНИЙ с помощью сети tooAzure подключения VPN.</span><span class="sxs-lookup"><span data-stu-id="b4cad-132">Traffic from clients on hello on-premises network get load-balanced across hello set of LOB servers using VPN connection tooAzure network.</span></span>

<span data-ttu-id="b4cad-133">Hello клиентский компьютер будет иметь доступ tooan IP-адрес от службы Azure VPN с помощью VPN toosite точки.</span><span class="sxs-lookup"><span data-stu-id="b4cad-133">hello client machine will have access tooan IP address from Azure VPN service using point toosite VPN.</span></span> <span data-ttu-id="b4cad-134">Она позволяет hello используйте hello бизнес-приложения, размещенные за конечной точкой ILB hello.</span><span class="sxs-lookup"><span data-stu-id="b4cad-134">It allows hello use hello LOB application hosted behind hello ILB endpoint.</span></span>

![Внутренней балансировки с помощью VPN toosite точки](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="b4cad-136">Рисунок 3. бизнес-приложений, размещенных за конечной точкой hello балансировки Нагрузки</span><span class="sxs-lookup"><span data-stu-id="b4cad-136">Figure 3 - LOB applications hosted behind hello LB endpoint</span></span>

<span data-ttu-id="b4cad-137">Другим случаем hello LOB является toohave сайта toosite VPN toohello виртуальной сети где настроены конечные точки ILB hello.</span><span class="sxs-lookup"><span data-stu-id="b4cad-137">Another scenario for hello LOB is toohave a site toosite VPN toohello virtual network where hello ILB endpoint is configured.</span></span> <span data-ttu-id="b4cad-138">Это позволяет в локальной сети трафика маршрутизации toobe toohello ILB конечной точки.</span><span class="sxs-lookup"><span data-stu-id="b4cad-138">This allows on-premises network traffic toobe routed toohello ILB endpoint.</span></span>

![Внутренней балансировки с помощью сайта toosite VPN](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="b4cad-140">Рисунок 4 - локальной сетевой трафик направляться конечной точке ILB toohello</span><span class="sxs-lookup"><span data-stu-id="b4cad-140">Figure 4 - On-premises network traffic routed toohello ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="b4cad-141">Ограничения</span><span class="sxs-lookup"><span data-stu-id="b4cad-141">Limitations</span></span>

<span data-ttu-id="b4cad-142">Конфигурации с внутренней подсистемой балансировки нагрузки не поддерживают SNAT.</span><span class="sxs-lookup"><span data-stu-id="b4cad-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="b4cad-143">В контексте этого документа hello SNAT относится tooport подлинность источника преобразования сетевых адресов.</span><span class="sxs-lookup"><span data-stu-id="b4cad-143">In hello context of this document, SNAT refers tooport masquerading source  network address translation.</span></span>  <span data-ttu-id="b4cad-144">Это относится tooscenarios целей tooreach hello соответствующих внутренней подсистемы балансировки нагрузки интерфейсный IP-адрес виртуальной Машины в пул подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b4cad-144">This applies tooscenarios where a VM in a load balancer pool needs tooreach hello respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="b4cad-145">В настоящее время для внутренней подсистемы балансировки нагрузки такой сценарий не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b4cad-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="b4cad-146">При toohello балансировки нагрузки виртуальной Машины, запущенный потока hello hello потока, происходит сбой подключения.</span><span class="sxs-lookup"><span data-stu-id="b4cad-146">Connection failures will occur when hello flow is load balanced toohello VM which originated hello flow.</span></span> <span data-ttu-id="b4cad-147">В таких ситуациях следует использовать подсистему балансировки нагрузки, работающую по принципу прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="b4cad-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4cad-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b4cad-148">Next Steps</span></span>

[<span data-ttu-id="b4cad-149">Поддержка Azure Resource Manager для Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="b4cad-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="b4cad-150">Приступая к настройке подсистемы балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="b4cad-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="b4cad-151">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="b4cad-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="b4cad-152">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="b4cad-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b4cad-153">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="b4cad-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
