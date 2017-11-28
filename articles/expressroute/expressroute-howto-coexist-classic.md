---
title: "Настройка сосуществующих подключений VPN типа ExpressRoute и \"сеть — сеть\" с помощью классической модели Azure | Документация Майкрософт"
description: "В этой статье описывается настройка параллельных подключений ExpressRoute и VPN типа \"сеть-сеть\" для классической модели развертывания."
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
ms.openlocfilehash: 09d1649f0ca0cf4ca464d95b29461cad3fe51788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="3e7cd-103">Настройка параллельных подключений ExpressRoute и "сайт — сайт" (классическая версия)</span><span class="sxs-lookup"><span data-stu-id="3e7cd-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e7cd-104">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3e7cd-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="3e7cd-105">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="3e7cd-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="3e7cd-106">Возможность настройки VPN типа "сеть-сеть" и ExpressRoute дает целый ряд преимуществ.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-106">Having the ability to configure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="3e7cd-107">Вы можете настроить VPN типа "сеть — сеть" как защищенный путь отработки отказа для ExressRoute или использовать эту VPN для подключения к сайтам, не подключенным через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="3e7cd-108">В этой статье мы рассмотрим порядок действия в каждом из этих вариантов.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-108">We will cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="3e7cd-109">Эта статья относится к модели классического развертывания.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-109">This article applies to the classic deployment model.</span></span> <span data-ttu-id="3e7cd-110">Эта конфигурация недоступна на портале.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-110">This configuration is not available in the portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="3e7cd-111">**О моделях развертывания Azure**</span><span class="sxs-lookup"><span data-stu-id="3e7cd-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="3e7cd-112">Перед выполнением приведенных ниже инструкций необходимо настроить каналы ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-112">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="3e7cd-113">Прежде чем следовать дальше, выполните инструкции по [созданию канала ExpressRoute](expressroute-howto-circuit-classic.md) и [настройке маршрутизации](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="3e7cd-113">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow the steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="3e7cd-114">Квоты и ограничения</span><span class="sxs-lookup"><span data-stu-id="3e7cd-114">Limits and limitations</span></span>
* <span data-ttu-id="3e7cd-115">**Транзитная маршрутизация не поддерживается.**</span><span class="sxs-lookup"><span data-stu-id="3e7cd-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="3e7cd-116">Нельзя настроить маршрутизацию (через Azure) между локальной сетью, подключенной к VPN типа "сеть — сеть", и локальной сетью, подключенной к ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="3e7cd-117">**Соединение типа "точка — сеть" не поддерживается.**</span><span class="sxs-lookup"><span data-stu-id="3e7cd-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="3e7cd-118">Невозможно включить подключения VPN "точка — сеть" к одной виртуальной сети, подключенной к ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-118">You can't enable point-to-site VPN connections to the same VNet that is connected to ExpressRoute.</span></span> <span data-ttu-id="3e7cd-119">VPN типа "точка-сеть" и ExpressRoute не могут существовать в одной и той же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-119">Point-to-site VPN and ExpressRoute cannot coexist for the same VNet.</span></span>
* <span data-ttu-id="3e7cd-120">**Принудительное туннелирование нельзя включить в VPN-шлюзе типа "сеть — сеть".**</span><span class="sxs-lookup"><span data-stu-id="3e7cd-120">**Forced tunneling cannot be enabled on the Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="3e7cd-121">Весь интернет-трафик можно направить в локальную сеть через ExpressRoute только "принудительно".</span><span class="sxs-lookup"><span data-stu-id="3e7cd-121">You can only "force" all Internet-bound traffic back to your on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="3e7cd-122">**Номера SKU класса "Базовый" для шлюза не поддерживаются.**</span><span class="sxs-lookup"><span data-stu-id="3e7cd-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="3e7cd-123">Используйте для [ExpressRoute](expressroute-about-virtual-network-gateways.md) и [VPN-шлюза](../vpn-gateway/vpn-gateway-about-vpngateways.md) номера SKU другого класса.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-123">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="3e7cd-124">**Поддерживается только VPN-шлюз на основе маршрутов.**</span><span class="sxs-lookup"><span data-stu-id="3e7cd-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="3e7cd-125">Необходимо использовать [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md) на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="3e7cd-126">**Для VPN-шлюза необходимо настроить статический маршрут.**</span><span class="sxs-lookup"><span data-stu-id="3e7cd-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="3e7cd-127">Если локальная сеть подключена и к ExpressRoute, и к VPN типа "сеть — сеть", необходимо использовать статический маршрут, настроенный в локальной сети для маршрутизации VPN-подключения типа "сеть — сеть" к Интернету.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-127">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="3e7cd-128">**Шлюз ExpressRoute необходимо настроить в первую очередь.**</span><span class="sxs-lookup"><span data-stu-id="3e7cd-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="3e7cd-129">Сначала необходимо создать шлюз ExpressRoute, а затем — добавить VPN-шлюз типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="3e7cd-129">You must create the ExpressRoute gateway first before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="3e7cd-130">Схемы конфигурации</span><span class="sxs-lookup"><span data-stu-id="3e7cd-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="3e7cd-131">Настройка VPN типа "сеть-сеть" как пути отработки отказа для ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3e7cd-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="3e7cd-132">VPN-подключение типа "сеть-сеть" можно настроить как службу архивации для ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="3e7cd-133">Это относится только к виртуальным сетям, привязанным к пути пиринга Azure Private.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-133">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="3e7cd-134">Для служб, доступ к которым осуществляется через пиринг Azure Public или Microsoft, решения для отработки отказа на основе VPN не существует.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="3e7cd-135">Канал ExpressRoute всегда является основной ссылкой.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-135">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="3e7cd-136">Данные передаются по пути VPN типа "сеть-сеть" только в том случае, если канал ExpressRoute не справляется с этой задачей.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-136">Data will flow through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="3e7cd-137">Хотя канал ExpressRoute лучше использовать для VPN типа "сеть — сеть", когда оба маршрута одинаковы, Azure будет выбирать маршрут для назначения пакета по совпадению самого длинного префикса.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![Существуют одновременно](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="3e7cd-139">Настройка VPN типа "сеть-сеть" для подключения к сайтам, не подключенным через ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3e7cd-139">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="3e7cd-140">Сети можно настроить таким образом, чтобы одни из них подключались непосредственно к Azure по VPN типа "сеть-сеть", а другие — через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-140">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Существуют одновременно](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="3e7cd-142">Настроить виртуальную сеть как транзитный маршрутизатор нельзя.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="3e7cd-143">Выбор действий для использования</span><span class="sxs-lookup"><span data-stu-id="3e7cd-143">Selecting the steps to use</span></span>
<span data-ttu-id="3e7cd-144">Существует два различных набора процедур для настройки сосуществующих подключений.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-144">There are two different sets of procedures to choose from in order to configure connections that can coexist.</span></span> <span data-ttu-id="3e7cd-145">Выбор процедуры настройки зависит от того, существует ли уже виртуальная сеть, к которой необходимо подключиться, или требуется создать новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-145">The configuration procedure that you select will depend on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="3e7cd-146">У меня нет виртуальной сети, и мне нужно ее создать.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-146">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="3e7cd-147">Если у вас еще нет виртуальной сети, то, выполнив эту процедуру, вы сможете создать новую виртуальную сеть с помощью классической модели развертывания и новые подключения ExpressRoute и VPN типа "сеть-сеть".</span><span class="sxs-lookup"><span data-stu-id="3e7cd-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using the classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="3e7cd-148">Для настройки выполните действия из раздела [Создание новой виртуальной сети и параллельных подключений](#new).</span><span class="sxs-lookup"><span data-stu-id="3e7cd-148">To configure, follow the steps in the article section [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="3e7cd-149">У меня уже есть виртуальная сеть с классической моделью развертывания.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="3e7cd-150">Возможно, у вас уже имеется виртуальная сеть, а также подключения к VPN типа "сеть-сеть" или к ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="3e7cd-151">В разделе [Настройка параллельных подключений для существующей виртуальной сети](#add) этой статьи описано, как удалить шлюз, а затем создать новое подключение ExpressRoute и VPN-подключение "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="3e7cd-151">The article section [To configure coexsiting connections for an already existing VNet](#add) will walk you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="3e7cd-152">Обратите внимание, что при создании новых подключений, необходимо выполнять действия в строго определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-152">Note that when creating the new connections, the steps must be completed in a very specific order.</span></span> <span data-ttu-id="3e7cd-153">При создании шлюзов и подключений не пользуйтесь инструкциями, взятыми из других статей.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-153">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="3e7cd-154">В этой процедуре для создания одновременно существующих подключений потребуется удалить имеющийся шлюз, а затем настроить новые шлюзы.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-154">In this procedure, creating connections that can coexist will require you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="3e7cd-155">Это означает, что у вас будет перерыв в работе подключений между организациями, на время удаления и повторного создания шлюза и подключений, но вам не потребуется выполнять миграцию всех виртуальных машин и служб в новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="3e7cd-156">Виртуальные машины и службы смогут по-прежнему осуществлять связь через балансировщик нагрузки во время настройки шлюза, если они настроены соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-156">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="3e7cd-157"><a name="new"></a>Создание новой виртуальной сети и параллельных подключений</span><span class="sxs-lookup"><span data-stu-id="3e7cd-157"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="3e7cd-158">В этой процедуре подробно рассматривается создание виртуальной сети, а также параллельных подключений ExpressRoute и "сеть-сеть".</span><span class="sxs-lookup"><span data-stu-id="3e7cd-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="3e7cd-159">Вам потребуется установить последнюю версию командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-159">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3e7cd-160">Дополнительные сведения об установке командлетов PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3e7cd-160">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="3e7cd-161">Обратите внимание, что командлеты, которые будут использоваться для этой конфигурации, могут немного отличаться от знакомых вам.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-161">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="3e7cd-162">Обязательно используйте командлеты, указанные в инструкциях.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-162">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="3e7cd-163">Создайте схему для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="3e7cd-164">Дополнительные сведения о схеме конфигурации см. в статье [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx) (Схема конфигурации виртуальной сети Azure).</span><span class="sxs-lookup"><span data-stu-id="3e7cd-164">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="3e7cd-165">При создании схемы, убедитесь, что используются следующие значения.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-165">When you create your schema, make sure you use the following values:</span></span>
   
   * <span data-ttu-id="3e7cd-166">Подсеть шлюза для виртуальной сети должна иметь значение /27 или более короткий префикс (например, /26 или /25).</span><span class="sxs-lookup"><span data-stu-id="3e7cd-166">The gateway subnet for the virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="3e7cd-167">Тип подключения шлюза — "выделенное".</span><span class="sxs-lookup"><span data-stu-id="3e7cd-167">The gateway connection type is "Dedicated".</span></span>
     
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
3. <span data-ttu-id="3e7cd-168">После создания и настройки XML-файла схемы отправьте этот файл.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-168">After creating and configuring your xml schema file, upload the file.</span></span> <span data-ttu-id="3e7cd-169">Это будет созданием виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="3e7cd-170">Чтобы отправить файл с измененными значениями, используйте следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-170">Use the following cmdlet to upload your file, replacing the value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="3e7cd-171"><a name="gw"></a>Создайте шлюз ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="3e7cd-172">Не забудьте указать для номера SKU шлюза значение *Standard*, *HighPerformance* или *UltraPerformance*, а для типа шлюза — значение *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-172">Be sure to specify the GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="3e7cd-173">Используйте следующий пример, подставив собственные значения.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-173">Use the following sample, substituting the values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="3e7cd-174">Свяжите шлюз ExpressRoute с каналом ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-174">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="3e7cd-175">После выполнения этого действия подключение локальной сети к Azure через ExpressRoute будет установлено.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-175">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="3e7cd-176"><a name="vpngw"></a>Далее создайте VPN-шлюз типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="3e7cd-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="3e7cd-177">Номер SKU шлюза должен иметь значение *Standard*, *HighPerformance* или *UltraPerformance*, а тип шлюза должен быть *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-177">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="3e7cd-178">Чтобы получить параметры шлюза виртуальной сети, включая идентификатор шлюза и общедоступный IP-адрес, используйте командлет `Get-AzureVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-178">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for the following virtual network: GNSDesMoines
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
7. <span data-ttu-id="3e7cd-179">Создайте сущность VPN-шлюза локального сайта.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="3e7cd-180">Эта команда не настраивает локальный VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="3e7cd-181">Она только позволяет указать параметры локального шлюза, такие как общедоступный IP-адрес и локальное адресное пространство, чтобы VPN-шлюз Azure мог подключиться к нему.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="3e7cd-182">Локальный сайт для подключения VPN типа "сеть-сеть" не определяется в netcfg.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-182">The local site for the Site-to-Site VPN is not defined in the netcfg.</span></span> <span data-ttu-id="3e7cd-183">Этот командлет можно использовать только для указания параметров локального сайта.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-183">Instead, you must use this cmdlet to specify the local site parameters.</span></span> <span data-ttu-id="3e7cd-184">Его нельзя определить с помощью портала или файла netcfg.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-184">You cannot define it using either portal, or the netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="3e7cd-185">Используйте следующий пример, подставив собственные значения.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-185">Use the following sample, replacing the values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="3e7cd-186">Если локальная сеть имеет несколько маршрутов, их все можно передать как массив.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="3e7cd-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="3e7cd-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="3e7cd-188">Чтобы получить параметры шлюза виртуальной сети, включая идентификатор шлюза и общедоступный IP-адрес, используйте командлет `Get-AzureVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-188">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="3e7cd-189">См. указанный ниже пример.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-189">See the following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="3e7cd-190">Настройте локальное VPN-устройство для подключения к новому шлюзу.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-190">Configure your local VPN device to connect to the new gateway.</span></span> <span data-ttu-id="3e7cd-191">При настройке VPN-устройства используйте сведения, полученные на этапе 6.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-191">Use the information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="3e7cd-192">Дополнительные сведения о настройке VPN-устройства см. в статье [О VPN-устройствах для подключений VPN-шлюзов типа "сеть — сеть"](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="3e7cd-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="3e7cd-193">Свяжите VPN-шлюз к сети типа "сеть-сеть" в Azure с локальным шлюзом.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-193">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>
   
    <span data-ttu-id="3e7cd-194">В этом примере connectedEntityId — идентификатор локального шлюза, который можно узнать, выполнив `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-194">In this example, connectedEntityId is the local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="3e7cd-195">virtualNetworkGatewayId можно узнать с помощью командлета `Get-AzureVirtualNetworkGateway` .</span><span class="sxs-lookup"><span data-stu-id="3e7cd-195">You can find virtualNetworkGatewayId by using the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="3e7cd-196">После выполнения этого действия подключение локальной сети к Azure через сеть VPN типа "сеть-сеть" будет установлено.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-196">After this step, the connection between your local network and Azure via the Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="3e7cd-197"><a name="add"></a>Настройка параллельных подключений для существующей виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="3e7cd-197"><a name="add"></a>To configure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="3e7cd-198">При наличии существующей виртуальной сети проверьте размер подсети шлюза.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-198">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="3e7cd-199">Если размер подсети шлюза — /28 или /29, необходимо сначала удалить шлюз виртуальной сети и увеличить размер подсети шлюза.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-199">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="3e7cd-200">В этом разделе показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-200">The steps in this section will show you how to do that.</span></span>

<span data-ttu-id="3e7cd-201">Если размер подсети шлюза — /27 или больше, а виртуальная сеть подключается с помощью ExpressRoute, можно пропустить описанные ниже шаги и перейти к шагу 6 ( [Создание VPN-шлюза подключения типа "сеть — сеть"](#vpngw) ) в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-201">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="3e7cd-202">При удалении существующего шлюза локальные пользователи потеряют подключение к виртуальной сети на время выполнения этой настройки.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-202">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="3e7cd-203">Вам потребуется установить последнюю версию командлетов PowerShell диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-203">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="3e7cd-204">Дополнительные сведения об установке командлетов PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3e7cd-204">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="3e7cd-205">Обратите внимание, что командлеты, которые будут использоваться для этой конфигурации, могут немного отличаться от знакомых вам.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-205">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="3e7cd-206">Обязательно используйте командлеты, указанные в инструкциях.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-206">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="3e7cd-207">Удалите для сети типа "сеть — сеть" существующий VPN-шлюз или шлюз ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-207">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="3e7cd-208">Используйте командлет, приведенный ниже, подставив свои собственные значения.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-208">Use the following cmdlet, replacing the values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="3e7cd-209">Экспортируйте схему виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-209">Export the virtual network schema.</span></span> <span data-ttu-id="3e7cd-210">Используйте командлет PowerShell, приведенный ниже, подставив свои собственные значения.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-210">Use the following PowerShell cmdlet, replacing the values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="3e7cd-211">Измените схему файла конфигурации сети так, чтобы подсеть шлюза имела значение /27 или более короткий префикс (например, /26 или /25).</span><span class="sxs-lookup"><span data-stu-id="3e7cd-211">Edit the network configuration file schema so that the gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="3e7cd-212">См. указанный ниже пример.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-212">See the following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="3e7cd-213">Если в виртуальной сети недостаточно свободных IP-адресов для увеличения размера подсети шлюза, необходимо добавить дополнительные пространства IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-213">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span> <span data-ttu-id="3e7cd-214">Дополнительные сведения о схеме конфигурации см. в статье [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx) (Схема конфигурации виртуальной сети Azure).</span><span class="sxs-lookup"><span data-stu-id="3e7cd-214">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="3e7cd-215">Если ранее шлюз был к сети VPN типа «сеть-сеть», необходимо также изменить тип подключения на **выделенный**.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-215">If your previous gateway was a Site-to-Site VPN, you must also change the connection type to **Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="3e7cd-216">На этом этапе вы будете иметь виртуальную сеть без шлюзов.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="3e7cd-217">Чтобы создать новые шлюзы и завершить подключение, перейдите к шагу 4 ( [Создайте шлюз ExpressRoute](#gw)) из предыдущего раздела.</span><span class="sxs-lookup"><span data-stu-id="3e7cd-217">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e7cd-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3e7cd-218">Next steps</span></span>
<span data-ttu-id="3e7cd-219">Дополнительные сведения об ExpressRoute см. в статье [Вопросы и ответы по ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="3e7cd-219">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

