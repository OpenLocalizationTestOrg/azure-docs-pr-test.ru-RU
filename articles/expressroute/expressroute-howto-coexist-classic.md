---
title: "Настройка сосуществующих подключений VPN типа ExpressRoute и \"сеть — сеть\" с помощью классической модели Azure | Документация Майкрософт"
description: "В этой статье описывается настройка ExpressRoute и через виртуальную Частную сеть для подключения, могут сосуществовать для hello классической модели развертывания."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="ee0b2-103">Настройка параллельных подключений ExpressRoute и "сайт — сайт" (классическая версия)</span><span class="sxs-lookup"><span data-stu-id="ee0b2-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee0b2-104">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee0b2-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="ee0b2-105">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="ee0b2-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="ee0b2-106">Наличие возможности hello tooconfigure через виртуальную Частную сеть для и ExpressRoute имеет несколько преимуществ.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-106">Having hello ability tooconfigure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="ee0b2-107">Можно настроить через виртуальную Частную сеть — как путь безопасный переход на другой ресурс для ExressRoute или использовать toosites tooconnect VPN на сайт-сайт, не подключен через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="ee0b2-108">Hello tooconfigure действия будут рассмотрены оба сценария в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-108">We will cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="ee0b2-109">Эта статья относится toohello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-109">This article applies toohello classic deployment model.</span></span> <span data-ttu-id="ee0b2-110">Эта конфигурация не доступна на портале hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-110">This configuration is not available in hello portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="ee0b2-111">**О моделях развертывания Azure**</span><span class="sxs-lookup"><span data-stu-id="ee0b2-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="ee0b2-112">Каналы ExpressRoute должен быть предварительно настроен, прежде чем выполнять приведенные ниже инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-112">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="ee0b2-113">Убедитесь в том, чтобы были выполнены направляющие hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-classic.md) и [Настройка маршрутизации](expressroute-howto-routing-classic.md) перед выполнением приведенных ниже шагов hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-113">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow hello steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="ee0b2-114">Квоты и ограничения</span><span class="sxs-lookup"><span data-stu-id="ee0b2-114">Limits and limitations</span></span>
* <span data-ttu-id="ee0b2-115">**Транзитная маршрутизация не поддерживается.**</span><span class="sxs-lookup"><span data-stu-id="ee0b2-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="ee0b2-116">Нельзя настроить маршрутизацию (через Azure) между локальной сетью, подключенной к VPN типа "сеть — сеть", и локальной сетью, подключенной к ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="ee0b2-117">**Соединение типа "точка — сеть" не поддерживается.**</span><span class="sxs-lookup"><span data-stu-id="ee0b2-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="ee0b2-118">Не удается включить toohello подключений VPN точки сайтами одной виртуальной сети, подключенной tooExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-118">You can't enable point-to-site VPN connections toohello same VNet that is connected tooExpressRoute.</span></span> <span data-ttu-id="ee0b2-119">Точка сеть VPN и ExpressRoute не может использоваться совместно для hello же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-119">Point-to-site VPN and ExpressRoute cannot coexist for hello same VNet.</span></span>
* <span data-ttu-id="ee0b2-120">**Принудительное туннелирование нельзя включить hello через виртуальную Частную сеть для шлюза.**</span><span class="sxs-lookup"><span data-stu-id="ee0b2-120">**Forced tunneling cannot be enabled on hello Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="ee0b2-121">Можно только «принудительно» все Интернета трафика задней tooyour локальной сети с помощью ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-121">You can only "force" all Internet-bound traffic back tooyour on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="ee0b2-122">**Номера SKU класса "Базовый" для шлюза не поддерживаются.**</span><span class="sxs-lookup"><span data-stu-id="ee0b2-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="ee0b2-123">Необходимо использовать основные SKU, отличного от шлюза для обоих hello [шлюз ExpressRoute](expressroute-about-virtual-network-gateways.md) и hello [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="ee0b2-123">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="ee0b2-124">**Поддерживается только VPN-шлюз на основе маршрутов.**</span><span class="sxs-lookup"><span data-stu-id="ee0b2-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="ee0b2-125">Необходимо использовать [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md) на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="ee0b2-126">**Для VPN-шлюза необходимо настроить статический маршрут.**</span><span class="sxs-lookup"><span data-stu-id="ee0b2-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="ee0b2-127">Если локальной сети — подключенных tooboth ExpressRoute и сеть-сеть VPN, должен иметь статический маршрут настроен в вашей локальной сети tooroute hello сеть-сеть VPN подключения toohello общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-127">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="ee0b2-128">**Шлюз ExpressRoute необходимо настроить в первую очередь.**</span><span class="sxs-lookup"><span data-stu-id="ee0b2-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="ee0b2-129">Сначала необходимо создать шлюз ExpressRoute hello, перед добавлением hello через виртуальную Частную сеть для шлюза.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-129">You must create hello ExpressRoute gateway first before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="ee0b2-130">Схемы конфигурации</span><span class="sxs-lookup"><span data-stu-id="ee0b2-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="ee0b2-131">Настройка VPN типа "сеть-сеть" как пути отработки отказа для ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ee0b2-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="ee0b2-132">VPN-подключение типа "сеть-сеть" можно настроить как службу архивации для ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="ee0b2-133">Это относится только toovirtual сетей связанного toohello Azure частным путем пиринга.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-133">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="ee0b2-134">Для служб, доступ к которым осуществляется через пиринг Azure Public или Microsoft, решения для отработки отказа на основе VPN не существует.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="ee0b2-135">Hello канал ExpressRoute всегда является основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-135">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="ee0b2-136">Только в том случае, если происходит сбой hello канал ExpressRoute через hello через виртуальную Частную сеть для пути будет потока данных.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-136">Data will flow through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="ee0b2-137">Пока канал ExpressRoute предпочтительнее через виртуальную Частную сеть для, когда обоих маршрутах являются одинаковыми hello, Azure будет использовать hello длинного префикса соответствия toochoose hello маршрута к назначения hello пакета.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Существуют одновременно](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="ee0b2-139">Настройка toosites через виртуальную Частную сеть для tooconnect, не подключен через ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ee0b2-139">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="ee0b2-140">Можно настроить сети, где некоторые узлы подключаются непосредственно tooAzure через сеть-сеть VPN, и некоторые узлы подключаются через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-140">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Существуют одновременно](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="ee0b2-142">Настроить виртуальную сеть как транзитный маршрутизатор нельзя.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="ee0b2-143">При выборе действия toouse hello</span><span class="sxs-lookup"><span data-stu-id="ee0b2-143">Selecting hello steps toouse</span></span>
<span data-ttu-id="ee0b2-144">Существует два разных набора toochoose процедуры из заказа tooconfigure подключений, которые могут сосуществовать.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-144">There are two different sets of procedures toochoose from in order tooconfigure connections that can coexist.</span></span> <span data-ttu-id="ee0b2-145">процедуры настройки Hello выбранного будет зависеть от наличия у существующей виртуальной сети, которые должны tooconnect в, или вы хотите toocreate новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-145">hello configuration procedure that you select will depend on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="ee0b2-146">Я нет виртуальной сети и требуется toocreate один.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-146">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="ee0b2-147">Если у вас еще нет виртуальной сети, эта процедура поможет создать новую виртуальную сеть с помощью hello классической модели развертывания и создание новых ExpressRoute "и" сеть-сеть VPN-подключений.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using hello classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="ee0b2-148">tooconfigure hello приведенным ниже инструкциям в разделе статьи hello [toocreate новую виртуальную сеть и существующих соединений](#new).</span><span class="sxs-lookup"><span data-stu-id="ee0b2-148">tooconfigure, follow hello steps in hello article section [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="ee0b2-149">У меня уже есть виртуальная сеть с классической моделью развертывания.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="ee0b2-150">Возможно, у вас уже имеется виртуальная сеть, а также подключения к VPN типа "сеть-сеть" или к ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="ee0b2-151">Здравствуйте раздела статьи [tooconfigure coexsiting соединений для уже существующей виртуальной сети](#add) поможет выполнить удаление шлюза hello и затем создавать новые ExpressRoute и через виртуальную Частную сеть для подключения.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-151">hello article section [tooconfigure coexsiting connections for an already existing VNet](#add) will walk you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="ee0b2-152">Обратите внимание, что при создании новых подключений hello, hello действия должны выполняться очень определенным образом.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-152">Note that when creating hello new connections, hello steps must be completed in a very specific order.</span></span> <span data-ttu-id="ee0b2-153">Не используйте инструкции hello в других статьях toocreate, шлюзы и подключения.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-153">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="ee0b2-154">В этой процедуре создания соединений, которые могут сосуществовать потребуется вы toodelete шлюз и затем настройте новых шлюзов.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-154">In this procedure, creating connections that can coexist will require you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="ee0b2-155">Это означает, что имеется время простоя для подключений между организациями во время удаления и повторного создания шлюза и подключения, но не потребуется toomigrate любой из виртуальных машин и служб tooa новой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="ee0b2-156">Виртуальные машины и службы будут иметь доступ toocommunicate out через hello балансировки нагрузки во время настройки шлюза, если они являются toodo настроенный таким образом.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-156">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="ee0b2-157"><a name="new"></a>toocreate новую виртуальную сеть и существующих соединений</span><span class="sxs-lookup"><span data-stu-id="ee0b2-157"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="ee0b2-158">В этой процедуре подробно рассматривается создание виртуальной сети, а также параллельных подключений ExpressRoute и "сеть-сеть".</span><span class="sxs-lookup"><span data-stu-id="ee0b2-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="ee0b2-159">Вам потребуется tooinstall hello последняя версия командлетов Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-159">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ee0b2-160">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-160">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="ee0b2-161">Обратите внимание, что командлеты hello, который будет использоваться для этой конфигурации может быть немного отличается от что вы не знакомы с.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-161">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="ee0b2-162">Указать командлеты hello toouse убедиться, что в этих инструкциях.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-162">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="ee0b2-163">Создайте схему для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="ee0b2-164">Дополнительные сведения о схеме конфигурации hello см. в разделе [схема конфигурации виртуальной сети Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee0b2-164">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="ee0b2-165">При создании схемы, убедитесь, что используется hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="ee0b2-165">When you create your schema, make sure you use hello following values:</span></span>
   
   * <span data-ttu-id="ee0b2-166">Hello подсеть шлюза для виртуальной сети hello должно быть /27 или короткое префикс (например, /26 или /25).</span><span class="sxs-lookup"><span data-stu-id="ee0b2-166">hello gateway subnet for hello virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="ee0b2-167">Тип подключения шлюза Hello» выделенные».</span><span class="sxs-lookup"><span data-stu-id="ee0b2-167">hello gateway connection type is "Dedicated".</span></span>
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. <span data-ttu-id="ee0b2-168">После создания и настройки файла схемы xml, отправьте файл hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-168">After creating and configuring your xml schema file, upload hello file.</span></span> <span data-ttu-id="ee0b2-169">Это будет созданием виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="ee0b2-170">Используйте следующий командлет tooupload hello файл, заменив значение hello свои собственные.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-170">Use hello following cmdlet tooupload your file, replacing hello value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="ee0b2-171"><a name="gw"></a>Создайте шлюз ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="ee0b2-172">Быть toospecify убедиться, что hello GatewaySKU как *стандартные*, *HighPerformance*, или *UltraPerformance* и hello тип шлюза как *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-172">Be sure toospecify hello GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="ee0b2-173">Здравствуйте, используйте следующий образец, подставив собственные значения hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-173">Use hello following sample, substituting hello values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="ee0b2-174">Свяжите канал ExpressRoute toohello шлюз ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-174">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="ee0b2-175">После завершения этого шага hello между локальной сетью и Azure через ExpressRoute, подключение выполняется.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-175">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="ee0b2-176"><a name="vpngw"></a>Далее создайте VPN-шлюз типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="ee0b2-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="ee0b2-177">Hello GatewaySKU должно быть *Стандартная*, *HighPerformance*, или *UltraPerformance* и hello тип шлюза должен быть *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-177">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="ee0b2-178">tooretrieve hello виртуальной сети шлюза параметров, включая идентификатор шлюза hello и hello открытый IP-адрес использовать hello `Get-AzureVirtualNetworkGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-178">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. <span data-ttu-id="ee0b2-179">Создайте сущность VPN-шлюза локального сайта.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="ee0b2-180">Эта команда не настраивает локальный VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="ee0b2-181">Вместо этого позволяет tooprovide hello локального шлюза параметры, такие как общедоступный IP-адрес hello и hello локального адресного пространства, hello VPN-шлюз Azure для подключения tooit.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ee0b2-182">локальном сайте hello через виртуальную Частную сеть для Hello не определен в hello netcfg.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-182">hello local site for hello Site-to-Site VPN is not defined in hello netcfg.</span></span> <span data-ttu-id="ee0b2-183">Вместо этого необходимо использовать это параметры командлета toospecify hello локального сайта.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-183">Instead, you must use this cmdlet toospecify hello local site parameters.</span></span> <span data-ttu-id="ee0b2-184">Нельзя определить с помощью портала или файла netcfg hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-184">You cannot define it using either portal, or hello netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="ee0b2-185">Следующий пример, заменив значения hello собственные используйте hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-185">Use hello following sample, replacing hello values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="ee0b2-186">Если локальная сеть имеет несколько маршрутов, их все можно передать как массив.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="ee0b2-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="ee0b2-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="ee0b2-188">tooretrieve hello виртуальной сети шлюза параметров, включая идентификатор шлюза hello и hello открытый IP-адрес использовать hello `Get-AzureVirtualNetworkGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-188">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="ee0b2-189">См. следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-189">See hello following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="ee0b2-190">Настройка локального устройства tooconnect toohello нового шлюза VPN.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-190">Configure your local VPN device tooconnect toohello new gateway.</span></span> <span data-ttu-id="ee0b2-191">Используйте сведения hello, полученный на шаге 6, при настройке VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-191">Use hello information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="ee0b2-192">Дополнительные сведения о настройке VPN-устройства см. в статье [О VPN-устройствах для подключений VPN-шлюзов типа "сеть — сеть"](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="ee0b2-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="ee0b2-193">Шлюз через виртуальную Частную сеть для hello ссылку на Azure toohello локального шлюза.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-193">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>
   
    <span data-ttu-id="ee0b2-194">В этом примере connectedEntityId — идентификатор hello локального шлюза, который можно получить, выполнив `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-194">In this example, connectedEntityId is hello local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="ee0b2-195">VirtualNetworkGatewayId можно найти с помощью hello `Get-AzureVirtualNetworkGateway` командлета.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-195">You can find virtualNetworkGatewayId by using hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="ee0b2-196">После выполнения этого шага hello между локальной сетью и Azure через hello подключение через виртуальную Частную сеть для подключения.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-196">After this step, hello connection between your local network and Azure via hello Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="ee0b2-197"><a name="add"></a>tooconfigure coexsiting соединений для уже существующей виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="ee0b2-197"><a name="add"></a>tooconfigure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="ee0b2-198">При наличии существующей виртуальной сети, проверьте размер подсети шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-198">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="ee0b2-199">Если подсеть шлюза hello /28 или /29, необходимо сначала удалить шлюз виртуальной сети hello и увеличьте размер подсети шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-199">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="ee0b2-200">Hello действия, описанные в этом разделе будет показано, как toodo.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-200">hello steps in this section will show you how toodo that.</span></span>

<span data-ttu-id="ee0b2-201">Если подсеть шлюза hello /27 или больше и виртуальной сети hello подключен через ExpressRoute, можно пропустить шаги hello и продолжить слишком[«Шаг 6 — создать шлюз VPN сеть-сеть»](#vpngw) в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-201">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="ee0b2-202">При удалении существующего шлюза hello ваших локальных машинах будут потеряны hello подключения tooyour виртуальной сети, при работе в этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-202">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="ee0b2-203">Вам потребуется tooinstall hello последнюю версию hello командлеты PowerShell диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-203">You'll need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="ee0b2-204">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-204">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="ee0b2-205">Обратите внимание, что командлеты hello, который будет использоваться для этой конфигурации может быть немного отличается от что вы не знакомы с.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-205">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="ee0b2-206">Указать командлеты hello toouse убедиться, что в этих инструкциях.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-206">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="ee0b2-207">Удалите шлюз ExpressRoute или через виртуальную Частную сеть для существующих hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-207">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="ee0b2-208">Используйте hello следующий командлет, заменив значения hello собственные.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-208">Use hello following cmdlet, replacing hello values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="ee0b2-209">Экспорт схемы hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-209">Export hello virtual network schema.</span></span> <span data-ttu-id="ee0b2-210">Используйте hello следующий командлет PowerShell, заменив значения hello собственные.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-210">Use hello following PowerShell cmdlet, replacing hello values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="ee0b2-211">Схема файла конфигурации сети hello следует измените, чтобы подсеть шлюза hello /27 или короткое префикс (например, /26 или /25).</span><span class="sxs-lookup"><span data-stu-id="ee0b2-211">Edit hello network configuration file schema so that hello gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="ee0b2-212">См. следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-212">See hello following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ee0b2-213">При отсутствии недостаточно IP-адресов в вашей виртуальной сети шлюза hello tooincrease подсети размер tooadd необходимо больше пространства IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-213">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span> <span data-ttu-id="ee0b2-214">Дополнительные сведения о схеме конфигурации hello см. в разделе [схема конфигурации виртуальной сети Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee0b2-214">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="ee0b2-215">Если предыдущие шлюза VPN сайт-сайт, необходимо также изменить тип подключения hello слишком**Dedicated**.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-215">If your previous gateway was a Site-to-Site VPN, you must also change hello connection type too**Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="ee0b2-216">На этом этапе вы будете иметь виртуальную сеть без шлюзов.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="ee0b2-217">toocreate новых шлюзов и завершения подключения, можно продолжить [шаг 4. Создайте шлюз ExpressRoute](#gw)в hello предшествующий набор шагов.</span><span class="sxs-lookup"><span data-stu-id="ee0b2-217">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee0b2-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ee0b2-218">Next steps</span></span>
<span data-ttu-id="ee0b2-219">Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="ee0b2-219">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

