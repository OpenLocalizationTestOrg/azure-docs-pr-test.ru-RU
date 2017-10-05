---
title: "Получение таблиц ARP. Устранение неполадок ExpressRoute (классическая модель) | Документация Майкрософт"
description: "На этой странице приводятся инструкции по получению таблиц ARP для канала ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: fcc847b7e30fd55ca759830e0254ab7542e7663e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-classic-deployment-model"></a><span data-ttu-id="1f513-103">Получение таблиц ARP в классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="1f513-103">Getting ARP tables in the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f513-104">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f513-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="1f513-105">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="1f513-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="1f513-106">В этой статье представлены пошаговые указания по получению таблиц протокола ARP для канала Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1f513-106">This article walks you through the steps for getting the Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f513-107">Данный документ предназначен для диагностики и устранения простых проблем.</span><span class="sxs-lookup"><span data-stu-id="1f513-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="1f513-108">Он не заменит услуг службы поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="1f513-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="1f513-109">Если проблему не удается устранить с помощью приведенных указаний, отправьте запрос на поддержку с помощью функции [Справка и поддержка Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="1f513-109">If you can't solve the problem by using the following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="1f513-110">Протокол ARP и таблицы ARP</span><span class="sxs-lookup"><span data-stu-id="1f513-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="1f513-111">ARP — это протокол уровня 2, который определен в [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="1f513-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="1f513-112">Протокол ARP используется для сопоставления адреса Ethernet (MAC-адреса) с IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="1f513-112">ARP is used to map an Ethernet address (MAC address) to an IP address.</span></span>

<span data-ttu-id="1f513-113">Таблица ARP обеспечивает сопоставление IPv4-адреса и MAC-адреса для конкретного пиринга.</span><span class="sxs-lookup"><span data-stu-id="1f513-113">An ARP table provides a mapping of the IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="1f513-114">Таблица ARP для пиринга канала ExpressRoute содержит следующие сведения о каждом интерфейсе (первичном и вторичном).</span><span class="sxs-lookup"><span data-stu-id="1f513-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="1f513-115">Сопоставление IP-адреса локального интерфейса маршрутизатора с MAC-адресом.</span><span class="sxs-lookup"><span data-stu-id="1f513-115">Mapping of an on-premises router interface IP address to a MAC address</span></span>
2. <span data-ttu-id="1f513-116">Сопоставление IP-адреса интерфейса ExpressRoute маршрутизатора с MAC-адресом.</span><span class="sxs-lookup"><span data-stu-id="1f513-116">Mapping of an ExpressRoute router interface IP address to a MAC address</span></span>
3. <span data-ttu-id="1f513-117">Длительность сопоставления.</span><span class="sxs-lookup"><span data-stu-id="1f513-117">The age of the mapping</span></span>

<span data-ttu-id="1f513-118">Таблицы ARP помогают проверять конфигурацию уровня 2 и устранять проблемы с подключением на базовом уровне 2.</span><span class="sxs-lookup"><span data-stu-id="1f513-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="1f513-119">Ниже приведен пример таблицы ARP.</span><span class="sxs-lookup"><span data-stu-id="1f513-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="1f513-120">В следующем разделе приведены сведения о том, как просмотреть таблицы ARP, видимые на пограничных маршрутизаторах ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1f513-120">The following section provides information about how to view the ARP tables that are seen by the ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="1f513-121">Необходимые условия для использования таблиц ARP</span><span class="sxs-lookup"><span data-stu-id="1f513-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="1f513-122">Прежде чем продолжить, убедитесь, что выполнены следующие условия.</span><span class="sxs-lookup"><span data-stu-id="1f513-122">Ensure that you have the following before you continue:</span></span>

* <span data-ttu-id="1f513-123">Настроен действительный канал ExpressRoute по крайней мере с одним пирингом.</span><span class="sxs-lookup"><span data-stu-id="1f513-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="1f513-124">Канал должен быть полностью настроен поставщиком услуг подключения.</span><span class="sxs-lookup"><span data-stu-id="1f513-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="1f513-125">Вы (или ваш поставщик услуг подключения) должны настроить хотя бы один из пирингов (частный или общедоступный пиринг Azure либо пиринг Майкрософт) для этого канала.</span><span class="sxs-lookup"><span data-stu-id="1f513-125">You (or your connectivity provider) must configure at least one of the peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="1f513-126">Настроены диапазоны IP-адресов, используемые для настройки пирингов (частных или общедоступных пирингов Azure либо пирингов Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="1f513-126">IP address ranges that are used for configuring the peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="1f513-127">Просмотрите примеры назначения IP-адресов на [странице требований к маршрутизации ExpressRoute](expressroute-routing.md) , чтобы понять, как IP-адреса сопоставляются с интерфейсами на вашей стороне и на стороне ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1f513-127">Review the IP address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how IP addresses are mapped to interfaces on your aise and on the ExpressRoute side.</span></span> <span data-ttu-id="1f513-128">Сведения о конфигурации пиринга можно получить, просмотрев [страницу настройки пиринга ExpressRoute](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="1f513-128">You can get information about the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="1f513-129">От вашей группы сетевых администраторов или поставщика услуг подключения получена информация о MAC-адресах интерфейсов, используемых для этих IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1f513-129">Information from your networking team or connectivity provider about the MAC addresses of the interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="1f513-130">Последняя версия модуля PowerShell для Azure (1.50 или более поздняя версия).</span><span class="sxs-lookup"><span data-stu-id="1f513-130">The latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="1f513-131">Таблицы ARP для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1f513-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="1f513-132">Этот раздел содержит инструкции о том, как просмотреть таблицы ARP для каждого типа пиринга с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f513-132">This section provides instructions about how to view the ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="1f513-133">Прежде чем продолжить, вам или вашему поставщику услуг подключения необходимо настроить пиринг.</span><span class="sxs-lookup"><span data-stu-id="1f513-133">Before you continue, either you or your connectivity provider needs to configure the peering.</span></span> <span data-ttu-id="1f513-134">Каждый канал имеет два пути (первичный и вторичный).</span><span class="sxs-lookup"><span data-stu-id="1f513-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="1f513-135">Вы можете просмотреть эти пути в таблице ARP независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="1f513-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="1f513-136">Таблицы ARP для частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="1f513-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="1f513-137">Следующий командлет предоставляет таблицы ARP для частного пиринга Azure.</span><span class="sxs-lookup"><span data-stu-id="1f513-137">The following cmdlet provides the ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="1f513-138">Ниже приведен пример выходных данных для одного из путей.</span><span class="sxs-lookup"><span data-stu-id="1f513-138">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="1f513-139">Таблицы ARP для общедоступного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="1f513-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="1f513-140">Следующий командлет предоставляет таблицы ARP для общедоступного пиринга Azure.</span><span class="sxs-lookup"><span data-stu-id="1f513-140">The following cmdlet provides the ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="1f513-141">Ниже приведен пример выходных данных для одного из путей.</span><span class="sxs-lookup"><span data-stu-id="1f513-141">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="1f513-142">Ниже приведен пример выходных данных для одного из путей.</span><span class="sxs-lookup"><span data-stu-id="1f513-142">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="1f513-143">Таблицы ARP для пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="1f513-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="1f513-144">Следующий командлет предоставляет таблицы ARP для пиринга Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="1f513-144">The following cmdlet provides the ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="1f513-145">Ниже приведен пример выходных данных для одного из путей.</span><span class="sxs-lookup"><span data-stu-id="1f513-145">Sample output is shown below for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="1f513-146">Как использовать эти сведения</span><span class="sxs-lookup"><span data-stu-id="1f513-146">How to use this information</span></span>
<span data-ttu-id="1f513-147">С помощью таблицы ARP для пиринга можно проверить конфигурацию и возможности подключения уровня 2.</span><span class="sxs-lookup"><span data-stu-id="1f513-147">The ARP table of a peering can be used to validate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="1f513-148">В этом разделе описывается, как выглядят таблицы ARP в различных сценариях.</span><span class="sxs-lookup"><span data-stu-id="1f513-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="1f513-149">Таблица ARP, когда канал находится в рабочем состоянии (ожидаемое состояние)</span><span class="sxs-lookup"><span data-stu-id="1f513-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="1f513-150">В таблице ARP отображается запись для локальной стороны с действительным IP-адресом и MAC-адресом, а также аналогичная запись со стороны сети Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="1f513-150">The ARP table has an entry for the on-premises side with a valid IP and MAC address, and a similar entry for the Microsoft side.</span></span>
* <span data-ttu-id="1f513-151">Последний октет локального IP-адреса всегда является нечетным числом.</span><span class="sxs-lookup"><span data-stu-id="1f513-151">The last octet of the on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="1f513-152">Последний октет локального IP-адреса сети Майкрософт всегда является четным числом.</span><span class="sxs-lookup"><span data-stu-id="1f513-152">The last octet of the Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="1f513-153">Одинаковый MAC-адрес отображается на стороне сети Майкрософт для всех 3 пирингов (первичных или вторичных).</span><span class="sxs-lookup"><span data-stu-id="1f513-153">The same MAC address appears on the Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-the-connectivity-provider-side-has-problems"></a><span data-ttu-id="1f513-154">Таблица ARP, когда она находится в локальной среде или когда на стороне поставщика услуг подключения возникли проблемы</span><span class="sxs-lookup"><span data-stu-id="1f513-154">ARP table when it's on-premises or when the connectivity-provider side has problems</span></span>
 <span data-ttu-id="1f513-155">В таблице ARP отображается только одна запись.</span><span class="sxs-lookup"><span data-stu-id="1f513-155">Only one entry appears in the ARP table.</span></span> <span data-ttu-id="1f513-156">Она содержит сопоставление MAC-адреса и IP-адреса, используемого на стороне сети Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="1f513-156">It shows the mapping between the MAC address and the IP address that's used on the Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="1f513-157">В случае возникновения подобной проблемы отправьте запрос на поддержку своему поставщику услуг подключения, чтобы устранить ее.</span><span class="sxs-lookup"><span data-stu-id="1f513-157">If you experience an issue like this, open a support request with your connectivity provider to resolve it.</span></span>
> 
> 

### <a name="arp-table-when-the-microsoft-side-has-problems"></a><span data-ttu-id="1f513-158">Таблица ARP в случае проблем на стороне сети Майкрософт</span><span class="sxs-lookup"><span data-stu-id="1f513-158">ARP table when the Microsoft side has problems</span></span>
* <span data-ttu-id="1f513-159">Вы не увидите таблицу ARP для пиринга при наличии проблем на стороне сети Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="1f513-159">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span>
* <span data-ttu-id="1f513-160">Отправьте запрос на поддержку с помощью функции [Справка и поддержка Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="1f513-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="1f513-161">Укажите, что у вас возникла проблема с возможностями подключения уровня 2.</span><span class="sxs-lookup"><span data-stu-id="1f513-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f513-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f513-162">Next steps</span></span>
* <span data-ttu-id="1f513-163">Проверка конфигураций уровня 3 для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1f513-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="1f513-164">Получение сводки маршрутов для определения состояния сеансов BGP.</span><span class="sxs-lookup"><span data-stu-id="1f513-164">Get a route summary to determine the state of BGP sessions.</span></span>
  * <span data-ttu-id="1f513-165">Получение таблицы маршрутов для определения того, какие префиксы объявляются в ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1f513-165">Get a route table to determine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="1f513-166">Проверка передачи данных путем просмотра входящих и исходящих байтов.</span><span class="sxs-lookup"><span data-stu-id="1f513-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="1f513-167">Отправьте запрос на поддержку с помощью функции [Справка и поддержка Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) , если у вас по-прежнему возникают проблемы.</span><span class="sxs-lookup"><span data-stu-id="1f513-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

