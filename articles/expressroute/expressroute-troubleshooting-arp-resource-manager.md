---
title: "Получение таблиц ARP. Устранение неполадок ExpressRoute (Resource Manager) | Документация Майкрософт"
description: "На этой странице приводятся инструкции по получению таблиц ARP для канала ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: a65b1ba2998eae33b3e73bd2492fbbf025eb5946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-resource-manager-deployment-model"></a><span data-ttu-id="3fe3b-103">Получение таблиц ARP в модели развертывания с помощью Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3fe3b-103">Getting ARP tables in the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3fe3b-104">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3fe3b-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="3fe3b-105">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="3fe3b-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="3fe3b-106">В этой статье описана процедура изучения таблиц ARP для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-106">This article walks you through the steps to learn the ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3fe3b-107">Данный документ предназначен для диагностики и устранения простых проблем.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="3fe3b-108">Он не заменит услуг службы поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="3fe3b-109">Если вам не удается устранить проблему, используя рекомендации, описанные ниже, то необходимо отправить запрос в [службу поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) .</span><span class="sxs-lookup"><span data-stu-id="3fe3b-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable to solve the problem using the guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="3fe3b-110">Протокол ARP и таблицы ARP</span><span class="sxs-lookup"><span data-stu-id="3fe3b-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="3fe3b-111">Протокол ARP — это протокол уровня 2, определенный в стандарте [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="3fe3b-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="3fe3b-112">Протокол ARP используется для сопоставления адреса Ethernet (MAC-адреса) с IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-112">ARP is used to map the Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="3fe3b-113">Таблица ARP обеспечивает сопоставление IPv4-адреса и MAC-адреса для конкретного пиринга.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-113">The ARP table provides a mapping of the ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="3fe3b-114">Таблица ARP для пиринга канала ExpressRoute содержит следующие сведения о каждом интерфейсе (первичном и вторичном).</span><span class="sxs-lookup"><span data-stu-id="3fe3b-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="3fe3b-115">Сопоставление локального IP-адреса интерфейса маршрутизатора с MAC-адресом.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-115">Mapping of on-premises router interface ip address to the MAC address</span></span>
2. <span data-ttu-id="3fe3b-116">Сопоставление IP-адреса интерфейса маршрутизатора ExpressRoute с MAC-адресом.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-116">Mapping of ExpressRoute router interface ip address to the MAC address</span></span>
3. <span data-ttu-id="3fe3b-117">Длительность сопоставления.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-117">Age of the mapping</span></span>

<span data-ttu-id="3fe3b-118">Таблицы ARP помогают проверить конфигурацию уровня 2 и устранить проблемы с подключением на базовом уровне 2.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="3fe3b-119">Пример таблицы ARP.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="3fe3b-120">В следующем разделе приведены сведения о том, как можно просмотреть таблицы ARP, видимые на граничных маршрутизаторах ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-120">The following section provides information on how you can view the ARP tables seen by the ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="3fe3b-121">Необходимые условия для изучения таблиц ARP</span><span class="sxs-lookup"><span data-stu-id="3fe3b-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="3fe3b-122">Прежде чем продолжить, убедитесь, что выполнены следующие условия.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-122">Ensure that you have the following before you progress further</span></span>

* <span data-ttu-id="3fe3b-123">Настроен действительный канал ExpressRoute по крайней мере с одним пирингом.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="3fe3b-124">Канал должен быть полностью настроен поставщиком услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="3fe3b-125">Вы (или ваш поставщик услуг подключения) должны настроить хотя бы один из пирингов (частный или общедоступный пиринг Azure либо пиринг Майкрософт) для этого канала.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-125">You (or your connectivity provider) must have configured at least one of the peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="3fe3b-126">Настроены диапазоны IP-адресов, используемые для настройки пирингов (частных или общедоступных пирингов Azure либо пирингов Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="3fe3b-126">IP address ranges used for configuring the peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="3fe3b-127">Просмотрите примеры назначения IP-адресов на [странице требований к маршрутизации ExpressRoute](expressroute-routing.md) , чтобы понять, как IP-адреса сопоставляются с интерфейсами на вашей стороне и на стороне ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-127">Review the ip address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how ip addresses are mapped to interfaces on your side and on the ExpressRoute side.</span></span> <span data-ttu-id="3fe3b-128">Сведения о конфигурации пиринга можно получить, просмотрев [страницу настройки пиринга ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="3fe3b-128">You can get information on the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="3fe3b-129">Получена информация от вашей группы сетевых администраторов или поставщика услуг подключения о MAC-адресах интерфейсов, используемых для этих IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-129">Information from your networking team / connectivity provider on the MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="3fe3b-130">Требуется последняя версия модуля PowerShell для Azure (1.50 или более поздняя версия).</span><span class="sxs-lookup"><span data-stu-id="3fe3b-130">You must have the latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-the-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="3fe3b-131">Получение таблиц ARP для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3fe3b-131">Getting the ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="3fe3b-132">В этом разделе описано, как просмотреть таблицы ARP для пиринга с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-132">This section provides instructions on how you can view the ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="3fe3b-133">Прежде чем продолжить, вам или вашему поставщику услуг подключения нужно настроить пиринг.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-133">You or your connectivity provider must have configured the peering before progressing further.</span></span> <span data-ttu-id="3fe3b-134">Каждый канал имеет два пути (первичный и вторичный).</span><span class="sxs-lookup"><span data-stu-id="3fe3b-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="3fe3b-135">Вы можете просмотреть эти пути в таблице ARP независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="3fe3b-136">Таблицы ARP для частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="3fe3b-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="3fe3b-137">Следующий командлет предоставляет таблицы ARP для частного пиринга Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-137">The following cmdlet provides the ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="3fe3b-138">Ниже приведен пример выходных данных для одного из путей.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-138">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="3fe3b-139">Таблицы ARP для общедоступного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="3fe3b-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="3fe3b-140">Следующий командлет предоставляет таблицы ARP для общедоступного пиринга Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-140">The following cmdlet provides the ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="3fe3b-141">Ниже приведен пример выходных данных для одного из путей.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-141">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="3fe3b-142">Таблицы ARP для пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="3fe3b-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="3fe3b-143">Следующий командлет предоставляет таблицы ARP для пиринга Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-143">The following cmdlet provides the ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="3fe3b-144">Ниже приведен пример выходных данных для одного из путей.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-144">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="3fe3b-145">Как использовать эти сведения</span><span class="sxs-lookup"><span data-stu-id="3fe3b-145">How to use this information</span></span>
<span data-ttu-id="3fe3b-146">С помощью таблицы ARP для пиринга можно проверить конфигурацию и подключение уровня 2.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-146">The ARP table of a peering can be used to determine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="3fe3b-147">В этом разделе описывается, как будут выглядеть таблицы ARP в различных сценариях.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="3fe3b-148">Таблица ARP, когда канал находится в рабочем состоянии (ожидаемое состояние)</span><span class="sxs-lookup"><span data-stu-id="3fe3b-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="3fe3b-149">В таблице ARP будет отображаться запись для локальной стороны с действительным IP-адресом и MAC-адресом, а также аналогичная запись со стороны сети Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-149">The ARP table will have an entry for the on-premises side with a valid IP address and MAC address and a similar entry for the Microsoft side.</span></span> 
* <span data-ttu-id="3fe3b-150">Последний октет локального IP-адреса всегда будет нечетным числом.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-150">The last octet of the on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="3fe3b-151">Последний октет IP-адреса сети Майкрософт всегда будет четным числом.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-151">The last octet of the Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="3fe3b-152">Одинаковый MAC-адрес будет отображаться со стороны сети Майкрософт для всех 3 пирингов (первичных или вторичных).</span><span class="sxs-lookup"><span data-stu-id="3fe3b-152">The same MAC address will appear on the Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="3fe3b-153">Таблица ARP в случае проблем на стороне локальной сети или поставщика услуг подключения</span><span class="sxs-lookup"><span data-stu-id="3fe3b-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="3fe3b-154">В случае проблем с локальной средой или поставщиком услуг подключения в таблице ARP может быть отображена только одна запись или локальный MAC-адрес может быть отображен не полностью.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-154">If there are issues with the on-premises or connectivity provider you may see that either only one entry will appear in the ARP table or the on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="3fe3b-155">Это будет сопоставление MAC-адреса и IP-адреса, используемого на стороне сети Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-155">This will show the mapping between the MAC address and IP address used in the Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="3fe3b-156">или</span><span class="sxs-lookup"><span data-stu-id="3fe3b-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="3fe3b-157">Отправьте запрос в службу поддержки своего поставщика услуг подключения, чтобы устранить подобные проблемы.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-157">Open a support request with your connectivity provider to debug such issues.</span></span> <span data-ttu-id="3fe3b-158">Если в таблице ARP нет IP-адресов интерфейсов, сопоставленных с MAC-адресами, ознакомьтесь со следующими сведениями.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-158">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
> 
> 1. <span data-ttu-id="3fe3b-159">Если первый IP-адрес подсети /30 назначен для связи между маршрутизатором MSEE-PR и MSEE используется интерфейсом MSEE-PR,</span><span class="sxs-lookup"><span data-stu-id="3fe3b-159">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="3fe3b-160">Azure всегда использует второй IP-адрес для маршрутизаторов MSEE.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-160">Azure always uses the second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="3fe3b-161">Убедитесь, что клиентские (C-тег) и служебные теги (S-тег) виртуальной сети соответствуют паре MSEE-PR и MSEE.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-161">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="3fe3b-162">Таблица ARP в случае проблем на стороне сети Майкрософт</span><span class="sxs-lookup"><span data-stu-id="3fe3b-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="3fe3b-163">Вы не увидите таблицу ARP для пиринга при наличии проблем на стороне сети Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-163">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span> 
* <span data-ttu-id="3fe3b-164">Отправьте запрос в [службу поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="3fe3b-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="3fe3b-165">Укажите, что у вас проблема с подключением уровня 2.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3fe3b-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3fe3b-166">Next Steps</span></span>
* <span data-ttu-id="3fe3b-167">Проверка конфигураций уровня 3 для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="3fe3b-168">Получение сводки маршрутов для определения состояния сеансов BGP.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-168">Get route summary to determine the state of BGP sessions</span></span> 
  * <span data-ttu-id="3fe3b-169">Получение таблицы маршрутов для определения того, какие префиксы объявляются в ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-169">Get route table to determine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="3fe3b-170">Проверка передачи данных путем просмотра входящих и выходящих байтов.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="3fe3b-171">Отправьте запрос в [службу поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) , если у вас по-прежнему возникают проблемы.</span><span class="sxs-lookup"><span data-stu-id="3fe3b-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

