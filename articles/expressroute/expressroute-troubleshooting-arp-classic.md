---
title: "Получение таблиц ARP. Устранение неполадок ExpressRoute (классическая модель) | Документация Майкрософт"
description: "Эта страница содержит инструкции по началу hello ARP таблицы за канал ExpressRoute."
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
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a><span data-ttu-id="138c1-103">Получение таблицы ARP в hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="138c1-103">Getting ARP tables in hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="138c1-104">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="138c1-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="138c1-105">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="138c1-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="138c1-106">В этой статье содержится описание этапов hello для получения таблиц hello протокола разрешения адресов (ARP) для своего канала Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="138c1-106">This article walks you through hello steps for getting hello Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="138c1-107">Данный документ является предполагаемым toohelp диагностики и устранения проблем простой.</span><span class="sxs-lookup"><span data-stu-id="138c1-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="138c1-108">Это не toobe предназначен для замены технической поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="138c1-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="138c1-109">Если не удается решить проблему hello с помощью hello следующие рекомендации, запрос в службу поддержки с [Microsoft Azure Справка и поддержка](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="138c1-109">If you can't solve hello problem by using hello following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="138c1-110">Протокол ARP и таблицы ARP</span><span class="sxs-lookup"><span data-stu-id="138c1-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="138c1-111">ARP — это протокол уровня 2, который определен в [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="138c1-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="138c1-112">ARP — используется toomap Ethernet (MAC-адрес) tooan IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="138c1-112">ARP is used toomap an Ethernet address (MAC address) tooan IP address.</span></span>

<span data-ttu-id="138c1-113">Таблицы ARP содержит сопоставления hello IPv4-адреса и MAC-адрес для конкретного пиринга.</span><span class="sxs-lookup"><span data-stu-id="138c1-113">An ARP table provides a mapping of hello IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="138c1-114">Hello таблицы ARP для пиринга ExpressRoute цепь предоставляет hello следующую информацию для каждого интерфейса (первичная и Вторичная).</span><span class="sxs-lookup"><span data-stu-id="138c1-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="138c1-115">Сопоставление локального маршрутизатора IP-адрес tooa MAC адрес интерфейса</span><span class="sxs-lookup"><span data-stu-id="138c1-115">Mapping of an on-premises router interface IP address tooa MAC address</span></span>
2. <span data-ttu-id="138c1-116">Сопоставление ExpressRoute маршрутизатора интерфейса IP-адрес tooa MAC адреса</span><span class="sxs-lookup"><span data-stu-id="138c1-116">Mapping of an ExpressRoute router interface IP address tooa MAC address</span></span>
3. <span data-ttu-id="138c1-117">Возраст Hello hello сопоставления</span><span class="sxs-lookup"><span data-stu-id="138c1-117">hello age of hello mapping</span></span>

<span data-ttu-id="138c1-118">Таблицы ARP помогают проверять конфигурацию уровня 2 и устранять проблемы с подключением на базовом уровне 2.</span><span class="sxs-lookup"><span data-stu-id="138c1-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="138c1-119">Ниже приведен пример таблицы ARP.</span><span class="sxs-lookup"><span data-stu-id="138c1-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="138c1-120">Hello следующий раздел содержит сведения о как tooview hello таблицы ARP, видимые hello ExpressRoute периметрическими маршрутизаторами.</span><span class="sxs-lookup"><span data-stu-id="138c1-120">hello following section provides information about how tooview hello ARP tables that are seen by hello ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="138c1-121">Необходимые условия для использования таблиц ARP</span><span class="sxs-lookup"><span data-stu-id="138c1-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="138c1-122">Убедитесь, что следующие hello перед продолжением:</span><span class="sxs-lookup"><span data-stu-id="138c1-122">Ensure that you have hello following before you continue:</span></span>

* <span data-ttu-id="138c1-123">Настроен действительный канал ExpressRoute по крайней мере с одним пирингом.</span><span class="sxs-lookup"><span data-stu-id="138c1-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="138c1-124">Hello канала должен быть настроен с поставщиком услуг подключения hello полностью.</span><span class="sxs-lookup"><span data-stu-id="138c1-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="138c1-125">Вы (или поставщиком соединения) необходимо настроить хотя бы один из пиринги hello (Azure открытого, закрытого, Azure или Майкрософт) для этой цепи.</span><span class="sxs-lookup"><span data-stu-id="138c1-125">You (or your connectivity provider) must configure at least one of hello peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="138c1-126">Диапазоны IP-адресов, которые используются для настройки пиринги hello (Azure открытого, закрытого, Azure и Microsoft).</span><span class="sxs-lookup"><span data-stu-id="138c1-126">IP address ranges that are used for configuring hello peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="138c1-127">Просмотрите примеры hello IP-адресов назначения в hello [странице требований маршрутизации ExpressRoute](expressroute-routing.md) tooget представление о том, как IP-адресов, сопоставленный toointerfaces на ваш aise и на стороне ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="138c1-127">Review hello IP address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how IP addresses are mapped toointerfaces on your aise and on hello ExpressRoute side.</span></span> <span data-ttu-id="138c1-128">Сведения о конфигурации пиринга hello можно получить, просмотрев hello [странице конфигурации пиринга ExpressRoute](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="138c1-128">You can get information about hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="138c1-129">Сведения от поставщика сетевых команды или подключения к MAC-адреса hello hello интерфейсов, которые используются с этих IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="138c1-129">Information from your networking team or connectivity provider about hello MAC addresses of hello interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="138c1-130">Hello последнюю версию модуля Windows PowerShell для Azure (версия 1.50 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="138c1-130">hello latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="138c1-131">Таблицы ARP для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="138c1-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="138c1-132">Этот раздел содержит инструкции о как tooview hello ARP таблицы для каждого типа пиринг с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="138c1-132">This section provides instructions about how tooview hello ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="138c1-133">Прежде чем продолжить, вы или поставщиком соединения должен пиринг tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="138c1-133">Before you continue, either you or your connectivity provider needs tooconfigure hello peering.</span></span> <span data-ttu-id="138c1-134">Каждый канал имеет два пути (первичный и вторичный).</span><span class="sxs-lookup"><span data-stu-id="138c1-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="138c1-135">Вы можете проверить hello таблицы ARP для каждого пути независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="138c1-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="138c1-136">Таблицы ARP для частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="138c1-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="138c1-137">Привет, выполнив командлет предоставляет hello ARP таблиц для открытого пиринга Azure:</span><span class="sxs-lookup"><span data-stu-id="138c1-137">hello following cmdlet provides hello ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="138c1-138">Ниже приведен пример выходных данных в один из путей hello.</span><span class="sxs-lookup"><span data-stu-id="138c1-138">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="138c1-139">Таблицы ARP для общедоступного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="138c1-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="138c1-140">Привет, выполнив командлет предоставляет hello ARP таблиц для частного пиринга Azure.</span><span class="sxs-lookup"><span data-stu-id="138c1-140">hello following cmdlet provides hello ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="138c1-141">Ниже приведен пример выходных данных в один из путей hello.</span><span class="sxs-lookup"><span data-stu-id="138c1-141">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="138c1-142">Ниже приведен пример выходных данных в один из путей hello.</span><span class="sxs-lookup"><span data-stu-id="138c1-142">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="138c1-143">Таблицы ARP для пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="138c1-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="138c1-144">Привет, выполнив командлет предоставляет hello ARP таблиц пиринг Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="138c1-144">hello following cmdlet provides hello ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="138c1-145">Ниже приведен пример выходных данных для одного пути hello:</span><span class="sxs-lookup"><span data-stu-id="138c1-145">Sample output is shown below for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="138c1-146">Как toouse эти сведения</span><span class="sxs-lookup"><span data-stu-id="138c1-146">How toouse this information</span></span>
<span data-ttu-id="138c1-147">Hello таблицы ARP пиринга может быть конфигурации используется toovalidate уровня 2 и подключение.</span><span class="sxs-lookup"><span data-stu-id="138c1-147">hello ARP table of a peering can be used toovalidate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="138c1-148">В этом разделе описывается, как выглядят таблицы ARP в различных сценариях.</span><span class="sxs-lookup"><span data-stu-id="138c1-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="138c1-149">Таблица ARP, когда канал находится в рабочем состоянии (ожидаемое состояние)</span><span class="sxs-lookup"><span data-stu-id="138c1-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="138c1-150">Hello таблицы ARP имеет запись hello локальной стороне с допустимым IP- и MAC-адресом и аналогичные запись для hello стороны Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="138c1-150">hello ARP table has an entry for hello on-premises side with a valid IP and MAC address, and a similar entry for hello Microsoft side.</span></span>
* <span data-ttu-id="138c1-151">последний октет Hello hello локального IP-адреса всегда является нечетным числом.</span><span class="sxs-lookup"><span data-stu-id="138c1-151">hello last octet of hello on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="138c1-152">последний октет Hello hello Microsoft IP-адреса всегда является четным числом.</span><span class="sxs-lookup"><span data-stu-id="138c1-152">hello last octet of hello Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="138c1-153">Здравствуйте, одинаковый MAC-адрес отображается на hello стороны Майкрософт для всех трех пиринги (первичный или вторичный).</span><span class="sxs-lookup"><span data-stu-id="138c1-153">hello same MAC address appears on hello Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a><span data-ttu-id="138c1-154">Таблицы ARP, когда она локальной или когда стороны поставщика услуг подключения hello имеется проблем</span><span class="sxs-lookup"><span data-stu-id="138c1-154">ARP table when it's on-premises or when hello connectivity-provider side has problems</span></span>
 <span data-ttu-id="138c1-155">В таблицы ARP hello отображается только одна запись.</span><span class="sxs-lookup"><span data-stu-id="138c1-155">Only one entry appears in hello ARP table.</span></span> <span data-ttu-id="138c1-156">Здесь показано сопоставление hello hello MAC-адрес и hello IP-адрес, который используется на стороне Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="138c1-156">It shows hello mapping between hello MAC address and hello IP address that's used on hello Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="138c1-157">При возникновении такую проблему, откройте поддержки запросов с вашей tooresolve подключения поставщика.</span><span class="sxs-lookup"><span data-stu-id="138c1-157">If you experience an issue like this, open a support request with your connectivity provider tooresolve it.</span></span>
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a><span data-ttu-id="138c1-158">Таблицы ARP hello Microsoft side проблемы при</span><span class="sxs-lookup"><span data-stu-id="138c1-158">ARP table when hello Microsoft side has problems</span></span>
* <span data-ttu-id="138c1-159">Таблицы ARP, показанный для пиринга при возникновении проблем на стороне Microsoft hello не будет.</span><span class="sxs-lookup"><span data-stu-id="138c1-159">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span>
* <span data-ttu-id="138c1-160">Отправьте запрос на поддержку с помощью функции [Справка и поддержка Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="138c1-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="138c1-161">Укажите, что у вас возникла проблема с возможностями подключения уровня 2.</span><span class="sxs-lookup"><span data-stu-id="138c1-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="138c1-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="138c1-162">Next steps</span></span>
* <span data-ttu-id="138c1-163">Проверка конфигураций уровня 3 для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="138c1-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="138c1-164">Отслеживает состояние hello маршрута сводки toodetermine сеансов BGP.</span><span class="sxs-lookup"><span data-stu-id="138c1-164">Get a route summary toodetermine hello state of BGP sessions.</span></span>
  * <span data-ttu-id="138c1-165">Получите toodetermine таблицы маршрутов, какие префиксов объявленных через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="138c1-165">Get a route table toodetermine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="138c1-166">Проверка передачи данных путем просмотра входящих и исходящих байтов.</span><span class="sxs-lookup"><span data-stu-id="138c1-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="138c1-167">Отправьте запрос на поддержку с помощью функции [Справка и поддержка Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) , если у вас по-прежнему возникают проблемы.</span><span class="sxs-lookup"><span data-stu-id="138c1-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

