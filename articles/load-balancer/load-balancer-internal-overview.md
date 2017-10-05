---
title: "Общие сведения о внутреннем балансировщике нагрузки | Документация Майкрософт"
description: "Обзор внутренней подсистемы балансировки нагрузки и ее функций, а также информация о том, как она работает в Azure и возможные сценарии настройки внутренних конечных точек."
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
ms.openlocfilehash: d324aaf8ec2c8766d5cf11452158d14c19cba4d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="81e21-103">Обзор внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="81e21-103">Internal load balancer overview</span></span>

<span data-ttu-id="81e21-104">В отличие от подсистемы балансировки нагрузки для Интернета, внутренняя подсистема балансировки нагрузки (ILB) направляет трафик только к ресурсам в пределах облачной службы или использует VPN для доступа к инфраструктуре Azure.</span><span class="sxs-lookup"><span data-stu-id="81e21-104">Unlike the Internet facing load balancer, the internal load balancer (ILB) directs traffic only to resources inside the cloud service or using VPN to access the Azure infrastructure.</span></span> <span data-ttu-id="81e21-105">Эта инфраструктура ограничивает доступ к виртуальным IP-адресам с балансировкой нагрузки для облачной службы или виртуальной сети. Таким образом, они никогда не будут доступны напрямую конечной точке в Интернете.</span><span class="sxs-lookup"><span data-stu-id="81e21-105">The infrastructure restricts access to the load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed to an Internet endpoint.</span></span> <span data-ttu-id="81e21-106">Это позволяет выполнять внутренние бизнес-приложения в Azure и получать к ним доступ в облаке или из локальных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="81e21-106">This enables internal line of business (LOB) applications to run in Azure and be accessed from within the cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="81e21-107">Чем полезна внутренняя подсистема балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="81e21-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="81e21-108">Внутренняя балансировка нагрузки Azure обеспечивает балансировку нагрузки между виртуальными машинами, которые размещены в облачной службе или региональной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="81e21-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="81e21-109">Информацию об использовании и настройке региональных виртуальных сетей см. в разделе блога Azure, посвященном [региональным виртуальным сетям](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).</span><span class="sxs-lookup"><span data-stu-id="81e21-109">For information about the use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in the Azure blog.</span></span> <span data-ttu-id="81e21-110">В имеющихся виртуальных сетях, настроенных для территориальной группы, невозможно использовать внутреннюю балансировку нагрузки.</span><span class="sxs-lookup"><span data-stu-id="81e21-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="81e21-111">Внутренняя подсистема балансировки нагрузки реализует следующие типы балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="81e21-111">ILB enables the following types of load balancing:</span></span>

* <span data-ttu-id="81e21-112">в облачной службе от виртуальных машин к набору виртуальных машин, размещенных в той же облачной службе (см. рис. 1);</span><span class="sxs-lookup"><span data-stu-id="81e21-112">Within a cloud service, from virtual machines to a set of virtual machines that reside within the same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="81e21-113">в виртуальной сети от виртуальных машин в виртуальной сети к набору виртуальных машин, размещенных в той же облачной службе виртуальной сети (см. рис. 2);</span><span class="sxs-lookup"><span data-stu-id="81e21-113">Within a virtual network, from virtual machines in the virtual network to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 2).</span></span>
* <span data-ttu-id="81e21-114">для распределенной виртуальной сети от локальных компьютеров к набору виртуальных машин, размещенных в той же облачной службе виртуальной сети (см. рис. 3).</span><span class="sxs-lookup"><span data-stu-id="81e21-114">For a cross-premises virtual network, from on-premises computers to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 3).</span></span>
* <span data-ttu-id="81e21-115">Доступные в Интернете многоуровневые приложения, серверные уровни в которых недоступны в Интернете, но требуют балансировки нагрузки для трафика на уровне, доступном в Интернете,</span><span class="sxs-lookup"><span data-stu-id="81e21-115">Internet-facing, multi-tier applications in which the back-end tiers are not Internet-facing but require load balancing for traffic from the Internet-facing tier.</span></span>
* <span data-ttu-id="81e21-116">Для балансировки нагрузки в бизнес-приложениях, размещенных в Azure. При этом не требуется дополнительное оборудование или программное обеспечение для распределения нагрузки.</span><span class="sxs-lookup"><span data-stu-id="81e21-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="81e21-117">включая локальные серверы в наборе компьютеров, чей трафик балансируется.</span><span class="sxs-lookup"><span data-stu-id="81e21-117">Including on-premises servers in the set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="81e21-118">Многоуровневые приложения, доступные в Интернете</span><span class="sxs-lookup"><span data-stu-id="81e21-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="81e21-119">Веб-уровень содержит конечные точки, доступные в Интернете, для интернет-клиентов и входит в набор балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="81e21-119">The web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="81e21-120">Подсистема балансировки нагрузки распределяет трафик от веб-клиентов на TCP-порт 443 (HTTPS) для веб-серверов.</span><span class="sxs-lookup"><span data-stu-id="81e21-120">The load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) to the web servers.</span></span>

<span data-ttu-id="81e21-121">Серверы баз данных находятся в пределах конечной точки внутренней балансировки нагрузки, которую веб-серверы используют для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="81e21-121">The database servers are behind an ILB endpoint which the web servers use for storage.</span></span> <span data-ttu-id="81e21-122">Это конечная точка с балансировкой нагрузки службы баз данных, трафик которой распределяется по серверам баз данных во внутреннем наборе балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="81e21-122">This database service load balanced endpoint, which traffic is load balanced across the database servers in the ILB set.</span></span>

<span data-ttu-id="81e21-123">На следующем рисунке показано многоуровневое приложение, доступное в Интернете, в пределах одной и той же облачной службы.</span><span class="sxs-lookup"><span data-stu-id="81e21-123">The following image shows the Internet facing multi-tier application within the same cloud service.</span></span>

![Внутренняя балансировка нагрузки для одной облачной службы](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="81e21-125">Рис. 1. Многоуровневое приложение для Интернета</span><span class="sxs-lookup"><span data-stu-id="81e21-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="81e21-126">Другой возможный сценарий для многоуровневого приложения: внутренняя подсистема балансировки нагрузки развертывается в облачной службе, отличной от той, которая использует службу для внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="81e21-126">Another possible use for a multi-tier application is when the ILB deployed to a different cloud service than the one consuming the service for the ILB.</span></span>

<span data-ttu-id="81e21-127">Облачные службы, использующие одну и ту же виртуальную сеть, будут иметь доступ к конечной точке внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="81e21-127">Cloud services using the same virtual network will have access to the ILB endpoint.</span></span> <span data-ttu-id="81e21-128">На следующем изображении показано, что веб-серверы переднего плана размещены в облачной службе, отличной от той, в которой размещен сервер базы данных. Кроме того, они используют конечную точку внутреннего балансировщика нагрузки в пределах одной и той же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="81e21-128">The following image shows front-end web servers are in a different cloud service from the database back-end and using the ILB endpoint within the same virtual network.</span></span>

![Внутренняя балансировка нагрузки между облачными службами](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="81e21-130">Рис. 2. Серверы переднего плана в другой облачной службе</span><span class="sxs-lookup"><span data-stu-id="81e21-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="81e21-131">Бизнес-приложения в интрасети</span><span class="sxs-lookup"><span data-stu-id="81e21-131">Intranet line of business applications</span></span>

<span data-ttu-id="81e21-132">Трафик от клиентов в локальной сети распределяется по набору серверов бизнес-приложений с помощью VPN-подключения к сети Azure.</span><span class="sxs-lookup"><span data-stu-id="81e21-132">Traffic from clients on the on-premises network get load-balanced across the set of LOB servers using VPN connection to Azure network.</span></span>

<span data-ttu-id="81e21-133">Клиентский компьютер получит доступ к IP-адресу из службы VPN Azure, используя VPN подключение типа "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="81e21-133">The client machine will have access to an IP address from Azure VPN service using point to site VPN.</span></span> <span data-ttu-id="81e21-134">Это позволит использовать бизнес-приложение, размещенное за конечной точкой внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="81e21-134">It allows the use the LOB application hosted behind the ILB endpoint.</span></span>

![Внутренняя балансировка нагрузки с использованием VPN типа «точка-сеть»](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="81e21-136">Рис. 3. Бизнес-приложение, размещенное за конечной точкой подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="81e21-136">Figure 3 - LOB applications hosted behind the LB endpoint</span></span>

<span data-ttu-id="81e21-137">Другой сценарий для бизнес-приложения: использование VPN подключения типа "сеть —сеть" для виртуальной сети, в которой настроена конечная точка внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="81e21-137">Another scenario for the LOB is to have a site to site VPN to the virtual network where the ILB endpoint is configured.</span></span> <span data-ttu-id="81e21-138">Это позволит направлять локальный сетевой трафик к конечной точке внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="81e21-138">This allows on-premises network traffic to be routed to the ILB endpoint.</span></span>

![Внутренняя балансировка нагрузки с помощью VPN типа «сеть-сеть»](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="81e21-140">Рис. 4. Локальной сетевой трафик направляется к конечной точке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="81e21-140">Figure 4 - On-premises network traffic routed to the ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="81e21-141">Ограничения</span><span class="sxs-lookup"><span data-stu-id="81e21-141">Limitations</span></span>

<span data-ttu-id="81e21-142">Конфигурации с внутренней подсистемой балансировки нагрузки не поддерживают SNAT.</span><span class="sxs-lookup"><span data-stu-id="81e21-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="81e21-143">В контексте этого документа под SNAT следует понимать преобразование сетевых адресов маскирующего порты источника.</span><span class="sxs-lookup"><span data-stu-id="81e21-143">In the context of this document, SNAT refers to port masquerading source  network address translation.</span></span>  <span data-ttu-id="81e21-144">Такое преобразование требуется в ситуациях, когда виртуальной машине в пуле подсистем балансировки нагрузки необходимо установить связь с соответствующим интерфейсным IP-адресом внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="81e21-144">This applies to scenarios where a VM in a load balancer pool needs to reach the respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="81e21-145">В настоящее время для внутренней подсистемы балансировки нагрузки такой сценарий не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="81e21-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="81e21-146">Когда в ходе балансировки нагрузка, создаваемая потоком, переносится на виртуальную машину, которая создала этот поток, происходит сбой подключения.</span><span class="sxs-lookup"><span data-stu-id="81e21-146">Connection failures will occur when the flow is load balanced to the VM which originated the flow.</span></span> <span data-ttu-id="81e21-147">В таких ситуациях следует использовать подсистему балансировки нагрузки, работающую по принципу прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="81e21-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81e21-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="81e21-148">Next Steps</span></span>

[<span data-ttu-id="81e21-149">Поддержка Azure Resource Manager для Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="81e21-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="81e21-150">Приступая к настройке подсистемы балансировки нагрузки, доступной в Интернете</span><span class="sxs-lookup"><span data-stu-id="81e21-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="81e21-151">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="81e21-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="81e21-152">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="81e21-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="81e21-153">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="81e21-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
