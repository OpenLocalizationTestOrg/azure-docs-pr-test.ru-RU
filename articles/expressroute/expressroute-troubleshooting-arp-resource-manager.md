---
title: "Получение таблиц ARP. Устранение неполадок ExpressRoute (Resource Manager) | Документация Майкрософт"
description: "Эта страница содержит инструкции по получении hello ARP таблицы за канал ExpressRoute"
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
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a><span data-ttu-id="65cfc-103">Получение ARP таблиц в модели развертывания диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="65cfc-103">Getting ARP tables in hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65cfc-104">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="65cfc-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="65cfc-105">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="65cfc-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="65cfc-106">В этой статье рассматриваются hello действия toolearn приветствия таблицы ARP для своего канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="65cfc-106">This article walks you through hello steps toolearn hello ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="65cfc-107">Данный документ является предполагаемым toohelp диагностики и устранения проблем простой.</span><span class="sxs-lookup"><span data-stu-id="65cfc-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="65cfc-108">Это не toobe предназначен для замены технической поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="65cfc-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="65cfc-109">Необходимо открыть запрос в службу поддержки с [поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) Если проблему не удается toosolve hello, с помощью hello рекомендации, описанные ниже.</span><span class="sxs-lookup"><span data-stu-id="65cfc-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable toosolve hello problem using hello guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="65cfc-110">Протокол ARP и таблицы ARP</span><span class="sxs-lookup"><span data-stu-id="65cfc-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="65cfc-111">Протокол ARP — это протокол уровня 2, определенный в стандарте [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="65cfc-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="65cfc-112">ARP — используется toomap hello Ethernet-адреса (MAC-адрес) IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="65cfc-112">ARP is used toomap hello Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="65cfc-113">Hello таблицы ARP содержит сопоставления hello ipv4-адреса и MAC-адрес для конкретного пиринга.</span><span class="sxs-lookup"><span data-stu-id="65cfc-113">hello ARP table provides a mapping of hello ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="65cfc-114">Hello таблицы ARP для пиринга ExpressRoute цепь предоставляет следующую информацию для каждого интерфейса (первичная и Вторичная) hello</span><span class="sxs-lookup"><span data-stu-id="65cfc-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="65cfc-115">Сопоставление локального маршрутизатора IP-адрес toohello MAC адрес интерфейса</span><span class="sxs-lookup"><span data-stu-id="65cfc-115">Mapping of on-premises router interface ip address toohello MAC address</span></span>
2. <span data-ttu-id="65cfc-116">Сопоставление ExpressRoute интерфейса IP-адрес toohello MAC адреса маршрутизатора</span><span class="sxs-lookup"><span data-stu-id="65cfc-116">Mapping of ExpressRoute router interface ip address toohello MAC address</span></span>
3. <span data-ttu-id="65cfc-117">Срок действия сопоставления hello</span><span class="sxs-lookup"><span data-stu-id="65cfc-117">Age of hello mapping</span></span>

<span data-ttu-id="65cfc-118">Таблицы ARP помогают проверить конфигурацию уровня 2 и устранить проблемы с подключением на базовом уровне 2.</span><span class="sxs-lookup"><span data-stu-id="65cfc-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="65cfc-119">Пример таблицы ARP.</span><span class="sxs-lookup"><span data-stu-id="65cfc-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="65cfc-120">Hello следующий раздел содержит сведения о том, как можно просмотреть hello таблицы ARP просмотрен hello ExpressRoute периметрическими маршрутизаторами.</span><span class="sxs-lookup"><span data-stu-id="65cfc-120">hello following section provides information on how you can view hello ARP tables seen by hello ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="65cfc-121">Необходимые условия для изучения таблиц ARP</span><span class="sxs-lookup"><span data-stu-id="65cfc-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="65cfc-122">Убедитесь, что следующие hello перед дальнейшей работе</span><span class="sxs-lookup"><span data-stu-id="65cfc-122">Ensure that you have hello following before you progress further</span></span>

* <span data-ttu-id="65cfc-123">Настроен действительный канал ExpressRoute по крайней мере с одним пирингом.</span><span class="sxs-lookup"><span data-stu-id="65cfc-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="65cfc-124">Hello канала должен быть настроен с поставщиком услуг подключения hello полностью.</span><span class="sxs-lookup"><span data-stu-id="65cfc-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="65cfc-125">Вы (или поставщиком соединения) необходимо настроить хотя бы один из пиринги hello (Azure открытого, закрытого, Azure и Microsoft) для этой цепи.</span><span class="sxs-lookup"><span data-stu-id="65cfc-125">You (or your connectivity provider) must have configured at least one of hello peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="65cfc-126">Диапазоны IP-адресов, используемым для настройки пиринги hello (Azure открытого, закрытого, Azure и Microsoft).</span><span class="sxs-lookup"><span data-stu-id="65cfc-126">IP address ranges used for configuring hello peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="65cfc-127">Просмотрите примеры hello IP-адресов назначения в hello [странице требований маршрутизации ExpressRoute](expressroute-routing.md) tooget представление о том, как IP-адресов, сопоставленный toointerfaces с вашей стороны и на стороне ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="65cfc-127">Review hello ip address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how ip addresses are mapped toointerfaces on your side and on hello ExpressRoute side.</span></span> <span data-ttu-id="65cfc-128">Сведения о конфигурации пиринга hello можно получить, просмотрев hello [странице конфигурации пиринга ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="65cfc-128">You can get information on hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="65cfc-129">Сведения для команды, сети и использовать поставщика услуг подключения на hello MAC-адреса интерфейсов с этих IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="65cfc-129">Information from your networking team / connectivity provider on hello MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="65cfc-130">Необходимо иметь hello последнюю версию модуля PowerShell для Azure (версия 1,50 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="65cfc-130">You must have hello latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="65cfc-131">Получение таблиц hello ARP для своего канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="65cfc-131">Getting hello ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="65cfc-132">Этот раздел предоставляет инструкции по как можно просмотреть hello таблицы ARP на пиринг с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65cfc-132">This section provides instructions on how you can view hello ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="65cfc-133">Вы или поставщиком соединения следует настроить пиринг hello, прежде чем углубляться в дальнейшей.</span><span class="sxs-lookup"><span data-stu-id="65cfc-133">You or your connectivity provider must have configured hello peering before progressing further.</span></span> <span data-ttu-id="65cfc-134">Каждый канал имеет два пути (первичный и вторичный).</span><span class="sxs-lookup"><span data-stu-id="65cfc-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="65cfc-135">Вы можете проверить hello таблицы ARP для каждого пути независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="65cfc-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="65cfc-136">Таблицы ARP для частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="65cfc-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="65cfc-137">Привет, выполнив командлет предоставляет hello ARP таблиц для открытого пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="65cfc-137">hello following cmdlet provides hello ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="65cfc-138">Ниже приведен пример выходных данных для одного пути hello</span><span class="sxs-lookup"><span data-stu-id="65cfc-138">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="65cfc-139">Таблицы ARP для общедоступного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="65cfc-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="65cfc-140">Привет, выполнив командлет предоставляет hello ARP таблиц для частного пиринга Azure</span><span class="sxs-lookup"><span data-stu-id="65cfc-140">hello following cmdlet provides hello ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="65cfc-141">Ниже приведен пример выходных данных для одного пути hello</span><span class="sxs-lookup"><span data-stu-id="65cfc-141">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="65cfc-142">Таблицы ARP для пиринга Майкрософт</span><span class="sxs-lookup"><span data-stu-id="65cfc-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="65cfc-143">Привет, выполнив командлет предоставляет hello ARP таблиц для пиринг Майкрософт</span><span class="sxs-lookup"><span data-stu-id="65cfc-143">hello following cmdlet provides hello ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="65cfc-144">Ниже приведен пример выходных данных для одного пути hello</span><span class="sxs-lookup"><span data-stu-id="65cfc-144">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="65cfc-145">Как toouse эти сведения</span><span class="sxs-lookup"><span data-stu-id="65cfc-145">How toouse this information</span></span>
<span data-ttu-id="65cfc-146">Hello таблицы ARP пиринга используется toodetermine проверить подключение и настройка уровня 2.</span><span class="sxs-lookup"><span data-stu-id="65cfc-146">hello ARP table of a peering can be used toodetermine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="65cfc-147">В этом разделе описывается, как будут выглядеть таблицы ARP в различных сценариях.</span><span class="sxs-lookup"><span data-stu-id="65cfc-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="65cfc-148">Таблица ARP, когда канал находится в рабочем состоянии (ожидаемое состояние)</span><span class="sxs-lookup"><span data-stu-id="65cfc-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="65cfc-149">Hello таблицы ARP будет создана запись с допустимым IP-адреса и MAC-адрес на стороне локальной hello и аналогичный элемент для hello стороны Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="65cfc-149">hello ARP table will have an entry for hello on-premises side with a valid IP address and MAC address and a similar entry for hello Microsoft side.</span></span> 
* <span data-ttu-id="65cfc-150">последний октет Hello hello локального IP-адреса всегда будет нечетным числом.</span><span class="sxs-lookup"><span data-stu-id="65cfc-150">hello last octet of hello on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="65cfc-151">последний октет hello IP-адрес Microsoft Hello всегда будет четное число.</span><span class="sxs-lookup"><span data-stu-id="65cfc-151">hello last octet of hello Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="65cfc-152">Здравствуйте, одинаковый MAC-адрес будет отображаться в hello стороны Майкрософт для всех 3 пиринги (первичного или вторичного).</span><span class="sxs-lookup"><span data-stu-id="65cfc-152">hello same MAC address will appear on hello Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="65cfc-153">Таблица ARP в случае проблем на стороне локальной сети или поставщика услуг подключения</span><span class="sxs-lookup"><span data-stu-id="65cfc-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="65cfc-154">Если возникли проблемы с hello в локальной или поставщика услуг подключения может появиться, либо только одна запись появится в hello ARP таблицы или hello локальный MAC-адрес будет отображать неполные.</span><span class="sxs-lookup"><span data-stu-id="65cfc-154">If there are issues with hello on-premises or connectivity provider you may see that either only one entry will appear in hello ARP table or hello on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="65cfc-155">При этом будут отображены сопоставление hello hello MAC-адрес и IP-адреса в hello стороны Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="65cfc-155">This will show hello mapping between hello MAC address and IP address used in hello Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="65cfc-156">или</span><span class="sxs-lookup"><span data-stu-id="65cfc-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="65cfc-157">Запрос в службу поддержки с вашей toodebug подключения поставщика подобные проблемы.</span><span class="sxs-lookup"><span data-stu-id="65cfc-157">Open a support request with your connectivity provider toodebug such issues.</span></span> <span data-ttu-id="65cfc-158">Если hello таблицы ARP отсутствует IP-адресов интерфейсов hello сопоставляются tooMAC адреса, hello просмотрите следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="65cfc-158">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
> 
> 1. <span data-ttu-id="65cfc-159">Если назначена hello первый IP-адрес подсети hello /30 для hello связь между hello MSEE PR и MSEE используется в интерфейсе hello MSEE PR.</span><span class="sxs-lookup"><span data-stu-id="65cfc-159">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="65cfc-160">Azure всегда использует hello второй IP-адрес для MSEEs.</span><span class="sxs-lookup"><span data-stu-id="65cfc-160">Azure always uses hello second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="65cfc-161">Убедитесь, если hello клиента (C-тег) и теги VLAN службы (S-Tag) соответствуют на пару MSEE PR и MSEE.</span><span class="sxs-lookup"><span data-stu-id="65cfc-161">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="65cfc-162">Таблица ARP в случае проблем на стороне сети Майкрософт</span><span class="sxs-lookup"><span data-stu-id="65cfc-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="65cfc-163">Таблицы ARP, показанный для пиринга при возникновении проблем на стороне Microsoft hello не будет.</span><span class="sxs-lookup"><span data-stu-id="65cfc-163">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span> 
* <span data-ttu-id="65cfc-164">Отправьте запрос в [службу поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="65cfc-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="65cfc-165">Укажите, что у вас проблема с подключением уровня 2.</span><span class="sxs-lookup"><span data-stu-id="65cfc-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="65cfc-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65cfc-166">Next Steps</span></span>
* <span data-ttu-id="65cfc-167">Проверка конфигураций уровня 3 для канала ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="65cfc-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="65cfc-168">Получение состояния hello маршрута сводки toodetermine сеансов BGP</span><span class="sxs-lookup"><span data-stu-id="65cfc-168">Get route summary toodetermine hello state of BGP sessions</span></span> 
  * <span data-ttu-id="65cfc-169">Получить какие префиксов объявленных через ExpressRoute toodetermine таблицы маршрутов</span><span class="sxs-lookup"><span data-stu-id="65cfc-169">Get route table toodetermine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="65cfc-170">Проверка передачи данных путем просмотра входящих и выходящих байтов.</span><span class="sxs-lookup"><span data-stu-id="65cfc-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="65cfc-171">Отправьте запрос в [службу поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) , если у вас по-прежнему возникают проблемы.</span><span class="sxs-lookup"><span data-stu-id="65cfc-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

